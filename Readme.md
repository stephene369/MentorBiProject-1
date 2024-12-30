## A Propos du projet

Il s'agit d'un projet d'analyse commerciale basé sur une base de données proposée par Marven : 
<img src="US+Candy+Distributor/Maven Logo.png">
<img/>


### Description de la base de données : 
**Distributeur de bonbons aux États-Unis**  
Données de ventes et d'expédition géospatiales entre les usines et les clients pour un distributeur national de bonbons aux États-Unis. Cela inclut des informations sur les emplacements des clients et des usines, les commandes de vente et les objectifs, ainsi que les détails des produits.  

**Analyses recommandées**  
1. Quelles sont les routes d'expédition les plus efficaces entre les usines et les clients ?  
2. Quelles sont les routes les moins efficaces ?  
3. Quels segments de produits offrent les meilleures marges bénéficiaires ?  
4. Quels segments de produits devraient être transférés à une autre usine pour optimiser les itinéraires d'expédition ?  

**Vous souhaitez un retour sur vos solutions ?**  
Partagez vos visualisations (et, le cas échéant, vos tableaux croisés dynamiques, votre code, etc.) sur LinkedIn en mentionnant **@Maven Analytics**. Nous serons ravis de voir votre travail et de vous donner notre avis !




Voici les descriptions en français :

| Table      | Champ             | Description                                                                                 |
|------------|--------------------|---------------------------------------------------------------------------------------------|
| Sales      | Row ID            | Identifiant unique de ligne                                                                 |
| Sales      | Order ID          | Identifiant unique de commande                                                              |
| Sales      | Order Date        | Date de la commande                                                                         |
| Sales      | Ship Date         | Date d'expédition                                                                           |
| Sales      | Ship Mode         | Méthode d'expédition de la commande                                                         |
| Sales      | Customer ID       | Identifiant unique du client                                                                |
| Sales      | Country/Region    | Pays ou région du client                                                                    |
| Sales      | City              | Ville du client                                                                             |
| Sales      | State/Province    | État/province du client                                                                     |
| Sales      | Postal Code       | Code postal / code ZIP du client                                                            |
| Sales      | Division          | Division du produit                                                                         |
| Sales      | Region            | Région du client                                                                            |
| Sales      | Product ID        | Identifiant unique du produit                                                               |
| Sales      | Product Name      | Nom complet du produit                                                                      |
| Sales      | Sales             | Valeur totale des ventes de la commande                                                     |
| Sales      | Units             | Nombre total d'unités de la commande                                                        |
| Sales      | Gross Profit      | Bénéfice brut de la commande (Ventes - Coût)                                                |
| Sales      | Cost              | Coût de fabrication                                                                         |
| Factories  | Factory           | Nom de l'usine                                                                              |
| Factories  | Latitude          | Coordonnées de latitude                                                                     |
| Factories  | Longitude         | Coordonnées de longitude                                                                    |
| Products   | Division          | Division du produit                                                                         |
| Products   | Product Name      | Nom descriptif du produit                                                                   |
| Products   | Factory           | Nom de l'usine                                                                              |
| Products   | Product ID        | Identifiant unique du produit                                                               |
| Products   | Unit Price        | Prix de vente du produit                                                                    |
| Products   | Unit Cost         | Coût de production du produit                                                               |
| Targets    | Division          | Division du produit                                                                         |
| Targets    | Target            | Objectif de ventes 2024                                                                     |
| US Zips    | zip               | Le code postal à 5 chiffres attribué par le service postal des États-Unis                   |
| US Zips    | lat               | Latitude du code postal (en savoir plus)                                                    |
| US Zips    | lng               | Longitude du code postal (en savoir plus)                                                   |
| US Zips    | city              | Nom officiel de la ville selon l'USPS                                                      |
| US Zips    | state_id          | Abréviation officielle de l'État selon l'USPS                                               |
| US Zips    | state_name        | Nom de l'État                                                                               |
| US Zips    | zcta              | TRUE si le code postal est une zone de tabulation des codes postaux (en savoir plus)       |
| US Zips    | parent_zcta       | ZCTA qui contient ce code postal. Existe uniquement si zcta est FALSE, utile pour inférer des informations d'un code postal situé dans un ZCTA. |
| US Zips    | population        | Estimation de la population du code postal. Existe uniquement si zcta est TRUE             |
| US Zips    | density           | Densité de population estimée par kilomètre carré. Existe uniquement si zcta est TRUE      |
| US Zips    | county_fips       | Comté principal du code postal au format FIPS                                              |
| US Zips    | county_name       | Nom du comté (county_fips)                                                                 |
| US Zips    | county_weights    | Dictionnaire JSON listant tous les county_fips et leurs poids (par zone) associés au code postal |
| US Zips    | imprecise         | TRUE si la latitude/longitude a été géolocalisée en utilisant la ville (rare)               |
| US Zips    | military          | TRUE si le code postal est utilisé par l'armée américaine (latitude/longitude non disponible) |
| US Zips    | timezone          | Fuseau horaire de la ville au format de la base de données tz (ex. America/Los_Angeles)    |



## Data exploring & cleaning 
En explorant les données fournies, nous avons remarqué que les bases de données étaient un peu dispersées. Il a donc été nécessaire d'effectuer un travail de nettoyage et de reconstruction pour obtenir une nouvelle base de données propre et prête pour notre analyse.  

### Cleaning
- **Correspondance des "zip" de la base "uszips.csv" avec la colonne "Postal Code" de la base "Candy_Sales.csv"** : Cette étape nous a permis d’obtenir la longitude et la latitude de tous les points de livraison associés aux commandes.  

- **Remplacement des données manquantes** : La base "uszips" contient uniquement les adresses des clients situés aux États-Unis. Cependant, nous avons identifié des commandes provenant du Canada. Nous avons donc demandé à une intelligence artificielle de nous aider à retrouver les longitudes et latitudes correspondant aux adresses des clients situés au Canada.  


### Exploration

#### **map.html**
<img src="images/map.png">
<img/>







## Contribution:

<div style= "display:flex; gap:2rem; "  >

<a href="https://github.com/MARA1976/Git-Hikayat_data">
  <img style='height:80px; border-radius:50px;' src="https://avatars.githubusercontent.com/u/131023019?v=4" alt="contrib.rocks image" />
  
</a>


<a href="https://github.com/stephene369/">
  <img style='height:80px; border-radius:50px;' src="https://avatars.githubusercontent.com/u/81186886?v=4" alt="contrib.rocks image" />
</a>



<div/>

