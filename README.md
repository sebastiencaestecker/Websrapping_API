# Websrapping_API

Projet pour une agence de voyage

## **Projet** 🚧

L'équipe marketing a besoin d'aide pour un nouveau projet. Après avoir effectué quelques recherches utilisateurs, l'équipe a découvert que 70 % de leurs utilisateurs qui planifient un voyage aimeraient avoir plus d'informations sur la destination qu'ils vont visiter.

De plus, les recherches utilisateurs montrent que les gens ont tendance à être méfiants vis-à-vis des informations qu'ils lisent s'ils ne connaissent pas la marque qui a produit le contenu.

Par conséquent, l'équipe marketing souhaite créer une application qui recommanderait aux gens où planifier leurs prochaines vacances. L'application devrait être basée sur des données réelles concernant :

- **La météo**
- **Les hôtels dans la région**

L'application devrait ensuite être capable de recommander les meilleures destinations et hôtels en fonction des variables ci-dessus à tout moment.

L'équipe marketing souhaite se concentrer d'abord sur les meilleures villes à visiter en France. Selon OneWeekIn.com, voici les 35 meilleures villes à visiter en France :

- Mont Saint Michel
- St Malo
- Bayeux
- Le Havre
- Rouen
- Paris
- Amiens
- Lille
- Strasbourg
- Chateau du Haut Koenigsbourg
- Colmar
- Eguisheim
- Besancon
- Dijon
- Annecy
- Grenoble
- Lyon
- Gorges du Verdon
- Bormes les Mimosas
- Cassis
- Marseille
- Aix en Provence
- Avignon
- Uzes
- Nimes
- Aigues Mortes
- Saintes Maries de la mer
- Collioure
- Carcassonne
- Ariege
- Toulouse
- Montauban
- Biarritz
- Bayonne
- La Rochelle

## **Objectifs** 🎯

Comme le projet vient de commencer, votre équipe ne dispose d'aucune donnée pouvant être utilisée pour créer cette application. Par conséquent, votre travail consistera à :

- Extraire des données sur les destinations
- Obtenir des données météorologiques pour chaque destination
- Obtenir des informations sur les hôtels de chaque destination

## **API**

### **Obtenir les coordonnées GPS des villes**

J'utilise l'API Nominatim pour obtenir les coordonnées GPS des 35 villes en France.

### **Obtenir les données météorologiques**

J'utilise l'API OpenWeatherMap pour récupérer les données météorologiques des 35 villes.

### **Analyser les données météorologiques**

Je détermine quelles villes auront le meilleur temps au cours des 7 prochains jours en fonction de critères tels que la pluie, la température, etc.

### **Sauvegarder les résultats dans un fichier CSV**

Je crée un DataFrame avec les informations importantes et le sauvegarde dans un fichier CSV.

### **Afficher les meilleures destinations sur une carte**

J'utilise Plotly pour afficher les meilleures destinations sur une carte.

## **Scrapping**

Je dois les informations suivantes pour chaque hôtel :

- Le nom de l'hôtel
- L'URL de sa page sur booking.com
- Ses coordonnées : latitude et longitude
- Le score donné par les utilisateurs du site
- Une description textuelle de l'hôtel
```

Cette version est structurée pour une meilleure lisibilité et compréhension sur GitHub.
