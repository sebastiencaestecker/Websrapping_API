import os
import pandas as pd
import logging
from twisted.internet import reactor
import scrapy
from scrapy.crawler import CrawlerProcess

# Charger le dataset
data = pd.read_csv("dataset_weather_per_city.csv")

class BookingSpider(scrapy.Spider):
    name = "bookingspider"

    def start_requests(self):
        # Générer les URLs de départ dynamiquement en fonction des villes
        for city in data['name']:
            url = f'https://www.booking.com/searchresults.fr.html?ss={city}'
            yield scrapy.Request(url=url, callback=self.parse, meta={'city': city})

    def parse(self, response):
        hotels = response.css('div[data-testid="property-card-container"]')
        for hotel in hotels:
            name = hotel.css('div.f6431b446c.a15b38c233::text').get()
            url = hotel.css('a.a78ca197d0::attr(href)').get()

            if url:
                hotel_url = response.urljoin(url)
                yield scrapy.Request(
                    url=hotel_url,
                    callback=self.parse_hotel,
                    meta={'url': hotel_url, 'name': name, 'city': response.meta['city']}
                )

    def parse_hotel(self, response):
        name = response.meta.get('name')
        url = response.meta.get('url')
        city = response.meta.get('city')
        
        score = response.css('div.a3b8729ab1.d86cee9b25::text').get()
        description = response.css('p.a53cbfa6de.b3efd73f69::text').getall()
        gps = response.css('a[data-atlas-latlng]::attr(data-atlas-latlng)').get()

        yield {
            'name': name,
            'url': url,
            'score': score,
            'description': description,
            'gps': gps
        }

# Nettoyer les anciens fichiers avant de démarrer
for city in data['name']:
    filename = f"2_hotels_{city}.json"
    if filename in os.listdir('src/'):
        os.remove('src/' + filename)

# Configurer le processus de Scrapy avec un fichier par ville
def run_spider_for_city(city):
    filename = f"src/2_hotels_{city}.json"
    
    process = CrawlerProcess(settings={
        'USER_AGENT': 'Chrome/109.0.0.0',
        'LOG_LEVEL': logging.INFO,
        'FEEDS': {
            filename: {"format": "json"},
        },
    })

    process.crawl(BookingSpider)
    process.start()

# Lancer le processus pour chaque ville
for city in data['name']:
    run_spider_for_city(city)

# Assurer l'arrêt du reactor si déjà démarré
if reactor._isRunning:
    reactor.stop()
