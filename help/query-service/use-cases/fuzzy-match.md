---
title: Correspondance floue dans Query Service
description: Découvrez comment effectuer une correspondance sur vos données Platform qui combine les résultats de plusieurs jeux de données en faisant correspondre approximativement une chaîne de votre choix.
exl-id: ec1e2dda-9b80-44a4-9fd5-863c45bc74a7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 0%

---

# Correspondance floue dans Query Service

Utilisez une correspondance approximative sur vos données Adobe Experience Platform pour renvoyer les correspondances les plus probables et les plus approximatives sans avoir à rechercher des chaînes avec des caractères identiques. Cela permet une recherche beaucoup plus flexible de vos données et rend vos données plus accessibles en gagnant du temps et en faisant des efforts.

Au lieu d’essayer de reformater les chaînes de recherche afin de les faire correspondre, la correspondance approximative analyse le rapport de similarité entre deux séquences et renvoie le pourcentage de similarité. [[!DNL FuzzyWuzzy]](https://pypi.org/project/fuzzywuzzy/) est recommandé pour ce processus, car ses fonctions sont plus adaptées à la correspondance de chaînes dans des situations plus complexes que [!DNL regex] ou [!DNL difflib].

L’exemple fourni dans ce cas d’utilisation se concentre sur la mise en correspondance d’attributs similaires à partir d’une recherche de chambre d’hôtel dans deux jeux de données d’agence de voyages différents. Le document indique comment faire correspondre des chaînes en fonction de leur degré de similarité à partir de sources de données distinctes volumineuses. Dans cet exemple, une correspondance approximative compare les résultats de recherche des fonctionnalités d’une pièce des agences de voyage Luma et Acme.

## Commencer {#getting-started}

Dans le cadre de ce processus, vous devez entraîner un modèle d’apprentissage automatique. Ce document suppose une connaissance pratique d’un ou de plusieurs environnements d’apprentissage automatique.

Cet exemple utilise [!DNL Python] et l’environnement de développement [!DNL Jupyter Notebook]. Bien qu’il existe de nombreuses options disponibles, [!DNL Jupyter Notebook] est recommandé car il s’agit d’une application web open source qui a de faibles exigences en matière de calcul. Il peut être téléchargé à partir du [site officiel de Jupyter](https://jupyter.org/).

Avant de commencer, vous devez importer les bibliothèques nécessaires. [!DNL FuzzyWuzzy] est une bibliothèque [!DNL Python] Open Source construite sur la bibliothèque [!DNL difflib] et utilisée pour faire correspondre des chaînes. Il utilise [!DNL Levenshtein Distance] pour calculer les différences entre les séquences et les motifs. [!DNL FuzzyWuzzy] a les exigences suivantes :

- [!DNL Python] 2.4 (ou version ultérieure)
- [!DNL Python-Levenshtein]

Sur la ligne de commande, utilisez la commande suivante pour installer [!DNL FuzzyWuzzy] :

```console
pip install fuzzywuzzy
```

Ou utilisez la commande suivante pour installer [!DNL Python-Levenshtein] également :

```console
pip install fuzzywuzzy[speedup]
```

Vous trouverez plus d&#39;informations techniques sur [!DNL Fuzzywuzzy] dans leur [documentation officielle](https://pypi.org/project/fuzzywuzzy/).

### Connexion à Query Service

Vous devez connecter votre modèle d’apprentissage automatique à Query Service en fournissant vos informations de connexion. Les informations d’identification arrivant à expiration et non arrivant à expiration peuvent être fournies. Pour plus d’informations sur la manière d’acquérir les informations d’identification nécessaires, consultez le [guide d’identification](../ui/credentials.md) . Si vous utilisez [!DNL Jupyter Notebook], veuillez lire le guide complet sur [la connexion à Query Service](../clients/jupyter-notebook.md).

Veillez également à importer le package [!DNL numpy] dans votre environnement [!DNL Python] pour activer l’algèbre linéaire.

```python
import numpy as np
```

Les commandes ci-dessous sont nécessaires pour se connecter à Query Service à partir de [!DNL Jupyter Notebook] :

```python
import psycopg2
conn = psycopg2.connect('''
sslmode=require
host=<YOUR_ORGANIZATION_ID>
port=80
dbname=prod:all
user=<YOUR_ADOBE_ID_TO_CONNECT_TO_QUERY_SERVICE>
password=<YOUR_QUERY_SERVICE_PASSWORD>
''')
cur = conn.cursor()
```

Votre instance [!DNL Jupyter Notebook] est maintenant connectée à Query Service. Si la connexion est établie, aucun message ne s’affiche. Si la connexion a échoué, une erreur s’affiche.

### Données Draw du jeu de données Luma {#luma-dataset}

Les données à analyser sont extraites du premier jeu de données avec les commandes suivantes. Pour plus de concision, les exemples se sont limités aux 10 premiers résultats de la colonne.

```python
cur.execute('''SELECT * FROM luma;
''')    
luma = np.array([r[0] for r in cur])

luma[:10]
```

Sélectionnez **Output** pour afficher le tableau renvoyé.

+++Output

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Données Draw du jeu de données Acme {#acme-dataset}

Les données à analyser sont désormais extraites du deuxième jeu de données avec les commandes suivantes. Pour être plus concis, les exemples se sont limités aux 10 premiers résultats de la colonne.

```python
cur.execute('''SELECT * FROM acme;
''')    
acme = np.array([r[0] for r in cur])

acme[:10]
```

Sélectionnez **Output** pour afficher le tableau renvoyé.

+++Output

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Créer une fonction de notation floue {#fuzzy-scoring}

Ensuite, vous devez importer `fuzz` à partir de la bibliothèque FuzzyWuzzy et exécuter une comparaison des proportions partielles des chaînes. La fonction de rapport partiel vous permet d’effectuer une correspondance sous-chaîne. Cette chaîne prend la chaîne la plus courte et correspond à toutes les sous-chaînes de même longueur. La fonction renvoie un pourcentage de similarité allant jusqu’à 100 %. Par exemple, la fonction de rapport partiel compare les chaînes suivantes &quot;chambre de luxe&quot;, &quot;lit de roi&quot; et &quot;chambre de roi de luxe&quot; et renvoie un score de similarité de 69 %.

Dans le cas d’utilisation de la correspondance de chambre d’hôtel, cela se fait à l’aide des commandes suivantes :

```python
from fuzzywuzzy import fuzz
def compute_match_score(x,y):
    return fuzz.partial_ratio(x,y)
```

Importez ensuite `cdist` depuis la bibliothèque [!DNL SciPy] pour calculer la distance entre chaque paire dans les deux collections d’entrées. Cela calcule les scores parmi toutes les paires de chambres d’hôtel fournies par chacune des agences de voyage.

```python
from scipy.spatial.distance import cdist
pairwise_distance =  cdist(luma.reshape((-1,1)),acme.reshape((-1,1)),compute_match_score)
```

### Créez des mappages entre les deux colonnes à l’aide du score de jointure flou.

Maintenant que les colonnes ont été notées en fonction de la distance, vous pouvez indexer les paires et ne conserver que les correspondances ayant obtenu un score supérieur à un certain pourcentage. Cet exemple conserve uniquement les paires qui correspondent avec un score de 70 % ou plus.

```python
matched_pairs = []
for i,c1 in enumerate(luma):
    idx = np.where(pairwise_distance[i,:] > 70)[0]
    for j in idx:
        matched_pairs.append((luma[i].replace("'","''"),acme[j].replace("'","''")))
```

Les résultats peuvent être affichés avec la commande suivante. Pour plus de concision, les résultats sont limités à dix lignes.

```python
matched_pairs[:10]
```

Sélectionnez **Output** pour afficher les résultats.

+++Output

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio')]
```

+++

Les résultats sont ensuite associés à l’aide de SQL avec la commande suivante :

<!-- Q) Why and is this accurate? -->

```python
matching_sql = ' OR '.join(["(e.luma = '{}' AND b.acme = '{}')".format(c1,c2) for c1,c2 in matched_pairs])
```

## Application des mappages pour effectuer une jointure floue dans Query Service {#mappings-for-query-service}

Ensuite, les paires de correspondance à score élevé sont unies à l’aide de SQL pour créer un nouveau jeu de données.

```python
:
cur.execute('''
SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{}
'''.format(matching_sql)) 
[r for r in cur]
```

Sélectionnez **Output** pour afficher les résultats de cette jointure.

+++Output

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio'),
 ('Deluxe Suite', 'Deluxe Suite'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Business King Room'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds',
  'Business Double Room With Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Deluxe Double Room'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Deluxe Suite, 1 Bedroom', 'Deluxe Suite'),
 ('City Room, City View', 'Room With City View'),
 ('City Room, City View', 'Queen Room With City View'),
 ('City Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Club Room, Premium 2 Queen Beds', 'Club Premium Two Queen'),
 ('Club Room, Premium 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, Lake View', 'Deluxe King Or Queen Room with Lake View'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('Deluxe Suite, 1 King Bed, Non Smoking, Kitchen', 'Deluxe Suite'),
 ('Junior Suite, 1 King Bed, Accessible (Roll-in Shower)', 'Junior Suite'),
 ('Regency Club, Mountain View', 'Regency Club Ocean View'),
 ('Regency Club, Mountain View', 'Regency Club Mountain View'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Room, Partial Ocean View', 'Room With Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View With Two Double Beds'),
 ('Room, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, Partial Ocean View', 'Waikiki Tower Partial Ocean View'),
 ('Premium Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Grand Corner King Room, 1 King Bed', 'Grand Corner King Room'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, 1 King Bed, Non Smoking', 'Deluxe Room - One King Bed'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Accessible Partial Ocean View With Two Double Beds'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Partial Ocean View Room'),
 ('Room, Ocean View ', 'Room With Ocean View'),
 ('Room, Ocean View ', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View ', 'Standard Room With Ocean View'),
 ('Signature Suite, 1 Bedroom', 'Signature King'),
 ('Room, 2 Queen Beds (Waikiki View)',
  'Queen Room With Two Queen Beds and Waikiki View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean View'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean Front View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('High-Floor Premium Room, 1 King Bed', 'High-Floor Premium King Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Junior Suite'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Deluxe King Suite With Sofa Bed'),
 ('Deluxe Room, City View', 'Queen Room With City View'),
 ('Deluxe Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, 1 Queen Bed, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Room, Ocean View', 'Room With Ocean View'),
 ('Room, Ocean View', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Partial Ocean View Room'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Standard Room, Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Regency Club, Ocean View',
  'Accessible Club Ocean View Suite With One King Bed'),
 ('Regency Club, Ocean View', 'Regency Club Ocean View'),
 ('Regency Club, Ocean View', 'Regency Club Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Ocean View'),
 ('Room, 1 Queen Bed', 'Deluxe Room - Two Queen Beds'),
 ('Double Room', 'Luxury Double Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Queen Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Business Double Room With Two Double Beds'),
 ('Double Room', 'Deluxe Double Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Twin Room', 'High-Floor Premium King Room'),
 ('Premier Twin Room', 'Premier King Room'),
 ('Premier Twin Room', 'Premier Queen Room With Two Queen Beds'),
 ('Premier Twin Room', 'Premium King Room With Free Wi-Fi'),
 ('Premium Room, 1 Queen Bed', 'Premium Two Queen'),
 ('Premium Room, 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, 1 Queen Bed (High Floor)', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, Garden View',
  'Queen Room With Two Queen Beds and Garden View'),
 ('Signature Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Signature Room, 2 Queen Beds', 'Signature Two Queen'),
 ('Standard Room, Ocean View', 'Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean Front View')]
```

+++

### Enregistrer les résultats de correspondance approximative dans Platform {#save-to-platform}

Enfin, les résultats de la correspondance approximative peuvent être enregistrés en tant que jeu de données à utiliser dans Adobe Experience Platform à l’aide de SQL.

```python
cur.execute(''' 
Create table luma_acme_join
AS
(SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{})
'''.format(matching_sql))
```
