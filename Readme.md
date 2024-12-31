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

- **Création d'une colonne "distance"** : Cette colonne représente la distance entre chaque client et l'usine d'approvisionnement.  


---

### **Exploration**

#### **map.html**
Représentation des clients sur une carte.  
Cette visualisation permet d’identifier facilement l'emplacement des clients.  

<img src="images/map.png" alt="Carte des clients" />

---

#### **heatmap.html**
Ce graphique montre la densité des clients sur la carte.  
Les zones plus intenses indiquent une concentration plus élevée de clients.  

<img src="images/heatmap.png" alt="Carte de densité des clients" />

---


### **route.html**  
Ce graphique trace une ligne reliant chaque usine à ses clients.  
Cela permet de visualiser la distance entre les usines et leurs clients, offrant une vue claire pour l'analyse.  

<img style="width:80%;height:80%;" src="images/route.png" alt="Carte de densité des clients" />

Par exemple, ce graphique peut recommander la suppression de l’usine **"Sugar Shrack"**, qui n’a eu que **11 clients en 4 ans**, tout en étant située à de grandes distances de ses clients.  
<img style="width:80%;height:80%;" src="images/sugar-route.png" alt="Carte de densité des clients" />


---


Ce graphique est un **boxplot** qui compare la distribution des ventes (`Sales`) pour différentes catégories de produits représentées par les divisions (`Division`) : **Chocolate**, **Other**, et **Sugar**.
<img src="images/box1.png" alt="Boxplot" />

### Ce que montre ce graphique :

   - **Chocolate :**  
     Les ventes sont concentrées autour d'une plage étroite avec une médiane basse et quelques valeurs atypiques.  
     Cela indique que les ventes de produits au chocolat sont relativement faibles et homogènes.  
   - **Other :**  
     Cette catégorie a une plage beaucoup plus large, avec de nombreuses ventes élevées (outliers) et une médiane supérieure à celle de "Chocolate".  
     Cela indique une plus grande variabilité dans les ventes pour cette catégorie.  
   - **Sugar :**  
     Les ventes de produits sucrés sont très faibles, avec une médiane proche de zéro et peu de variabilité. Il y a cependant quelques outliers.  
     Cela suggère une faible performance des produits de cette catégorie.


---

## 1- Optimisation des Routes d’Exp ́edition

D'après nos analyses, les coûts d'expédition n'affectent pas la rentabilité de **US Candy**. En effet, quel que soit la distance du client, le nombre de commandes ou le type de produit, le profit reste inchangé. Cela pourrait s'expliquer par le fait que :

1. **La livraison des produits a peut-être été confiée à une autre entreprise**, et les frais de livraison sont donc facturés séparément du prix de vente.  
2. **Les coûts d'expédition sont directement inclus dans le coût d'achat**, ce qui les rend invisibles dans l'analyse des marges.

Cependant, quel que soit le cas de figure, une usine plus proche des clients entraînerait automatiquement :

- **Une réduction des frais de livraison**, ce qui pourrait rendre les produits encore plus compétitifs.  
- **Une réception plus rapide des produits par les clients**, améliorant ainsi leur satisfaction.  

Ces avantages bénéficient autant à **US Candy** qu'à ses clients, renforçant la relation commerciale et la compétitivité de l’entreprise.

**La suite de notre analyse se concentrera donc davantage sur comment rapprocher les usines des clients, plutôt que sur l'optimisation des trajets de livraison.**



## 2- Analyse des Marges par Produit ; 

**Nombre total de commande par produit**
<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>productname</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Wonka Bar - Milk Chocolate</td>
      <td>1768</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Wonka Bar -Scrumdiddlyumptious</td>
      <td>1704</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wonka Bar - Triple Dazzle Caramel</td>
      <td>1677</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Wonka Bar - Nutty Crunch Surprise</td>
      <td>1529</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Wonka Bar - Fudge Mallows</td>
      <td>1527</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wonka Gum</td>
      <td>118</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Kazookles</td>
      <td>94</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Lickable Wallpaper</td>
      <td>92</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Laffy Taffy</td>
      <td>10</td>
    </tr>
    <tr>
      <th>9</th>
      <td>SweeTARTS</td>
      <td>10</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Fizzy Lifting Drinks</td>
      <td>6</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Hair Toffee</td>
      <td>4</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Nerds</td>
      <td>4</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Everlasting Gobstopper</td>
      <td>3</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Fun Dip</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>
<img src="images/count-by-produit.png" alt="bar" />
---

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>grossprofit</th>
    </tr>
    <tr>
      <th>productname</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Everlasting Gobstopper</th>
      <td>104.00</td>
    </tr>
    <tr>
      <th>Fizzy Lifting Drinks</th>
      <td>47.25</td>
    </tr>
    <tr>
      <th>Fun Dip</th>
      <td>4.80</td>
    </tr>
    <tr>
      <th>Hair Toffee</th>
      <td>59.50</td>
    </tr>
    <tr>
      <th>Kazookles</th>
      <td>91.50</td>
    </tr>
    <tr>
      <th>Laffy Taffy</th>
      <td>33.48</td>
    </tr>
    <tr>
      <th>Lickable Wallpaper</th>
      <td>3830.00</td>
    </tr>
    <tr>
      <th>Nerds</th>
      <td>7.00</td>
    </tr>
    <tr>
      <th>SweeTARTS</th>
      <td>28.70</td>
    </tr>
    <tr>
      <th>Wonka Bar - Fudge Mallows</th>
      <td>13903.20</td>
    </tr>
    <tr>
      <th>Wonka Bar - Milk Chocolate</th>
      <td>14426.07</td>
    </tr>
    <tr>
      <th>Wonka Bar - Nutty Crunch Surprise</th>
      <td>14250.27</td>
    </tr>
    <tr>
      <th>Wonka Bar - Triple Dazzle Caramel</th>
      <td>15501.15</td>
    </tr>
    <tr>
      <th>Wonka Bar -Scrumdiddlyumptious</th>
      <td>15867.50</td>
    </tr>
    <tr>
      <th>Wonka Gum</th>
      <td>303.55</td>
    </tr>
  </tbody>
</table>
</div>

**Profit total réaliser pour chaque produit au cours des 4ans**
<img src="images/gross-profit-perproduit.png" alt="bar" />





### Les plus rentables

Les analyses révèlent que les produits les plus rentables pour l'entreprise sont ceux de la division chocolat. En effet, cette catégorie se distingue par des performances exceptionnelles, tant en termes de volume de ventes que de rentabilité. 

* Le produit phare de l'entreprise est le **Wonka Bar - Milk Chocolate**, avec un total de 1 768 commandes. Ce produit se distingue par son succès auprès des consommateurs, surpassant largement ses concurrents directs dans la même catégorie. Parmi ces derniers, on trouve :

  - **Wonka Bar - Scrumdiddlyumptious** avec 1 704 commandes,
  - **Wonka Bar - Triple Dazzle Caramel** avec 1 677 commandes,
  - **Wonka Bar - Nutty Crunch Surprise** avec 1 529 commandes.

Ces produits, bien que légèrement moins populaires que le **Wonka Bar - Milk Chocolate**, restent des incontournables de la gamme, contribuant de manière significative au chiffre d'affaires de la division chocolat.

* En termes de rentabilité, les produits chocolatés se révèlent être les plus profitables pour l'entreprise **US Candy**. En particulier, le **Wonka Bar - Scrumdiddlyumptious** a généré un chiffre d'affaires impressionnant de **15 867,50 dollars** au cours des quatre dernières années. Cela montre que, bien que ce produit soit moins vendu que le **Wonka Bar - Milk Chocolate**, sa rentabilité est nettement plus élevée, ce qui en fait un atout stratégique pour l'entreprise. 

En somme, la division chocolat représente non seulement un fort volume de ventes mais aussi une rentabilité exceptionnelle pour l'entreprise, illustrée par le succès financier de ses produits phares, notamment le **Wonka Bar - Scrumdiddlyumptious**.



### Les moins rentables

Après avoir analysé les produits les plus rentables, nous nous penchons sur les produits les moins performants. Cette catégorie est principalement représentée par les divisions **Sugar** et **Other**, qui se distinguent par leurs faibles volumes de vente et leur rentabilité limitée.

- **Division Sugar** : Les produits de cette division affichent des chiffres de vente très faibles, avec souvent moins de 8 commandes sur l'ensemble des 4 années analysées. Par exemple :
  - **Everlasting Gobstopper** : seulement **3 commandes**,
  - **Fun Dip** : également limité à **3 commandes**.

Ces chiffres témoignent d'un faible attrait pour ces produits, suggérant qu'ils peinent à trouver leur place sur le marché.

- **Division Other** : Bien que moins documentée dans cette analyse, cette division semble également souffrir d'un manque d'intérêt de la part des consommateurs, contribuant peu à la rentabilité globale de l'entreprise.



## Prochaines étapes

Afin d'améliorer les performances des produits les moins rentables, une série d'analyses et de mesures seront envisagées :
1. **Études de marché** : Identifier les raisons derrière le faible intérêt pour ces produits. Cela peut inclure des enquêtes consommateurs pour comprendre leurs attentes et besoins.
2. **Stratégies de relance** : Tester de nouvelles stratégies marketing, repositionner ces produits ou explorer des opportunités de partenariats pour augmenter leur visibilité.
3. **Évaluation de la production** :
   - Analyser la viabilité des lignes de production dédiées à ces produits. 
   - Envisager une réaffectation des ressources à des produits plus prometteurs ou la création de nouvelles gammes en phase avec les tendances actuelles du marché.
4. **Décisions stratégiques** : Déterminer s’il serait plus avantageux de supprimer certains produits ou de transformer les usines concernées pour optimiser les opérations.

L’objectif est de minimiser les pertes associées à ces produits tout en explorant des opportunités pour relancer leur attractivité ou réorienter les efforts de production.



### Analyse de regles d'association pour sugerer et accroitre les ventes 










## Contribution:

<div style= "display:flex; gap:2rem; "  >

<a href="https://github.com/MARA1976/Git-Hikayat_data">
  <img style='height:80px; border-radius:50px;' src="https://avatars.githubusercontent.com/u/131023019?v=4" alt="contrib.rocks image" />
  
</a>


<a href="https://github.com/stephene369/">
  <img style='height:80px; border-radius:50px;' src="https://avatars.githubusercontent.com/u/81186886?v=4" alt="contrib.rocks image" />
</a>

<div/>

