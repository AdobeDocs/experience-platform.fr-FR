---
title: Filtrage des robots dans Query Service avec le machine learning
description: Ce document présente un aperçu de l’utilisation de Query Service et du machine learning pour déterminer l’activité des robots et filtrer leurs actions du trafic réel des visiteurs et visiteuses de sites Web.
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
TQID: https://experienceleague.adobe.com/bi7a-XL3awI6OtBZTugcoSq4yjfOWJTzIiLvLlA0DFg
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b4dd41a7-ccf8-4e9d-918e-acaab534a307
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 913
ht-degree: 5%

---

# Filtrage des robots en [!DNL Query Service] avec le machine learning

Les activités de robots peuvent avoir un impact sur les mesures d’analyse et nuire à l’intégrité des données. Adobe Experience Platform [!DNL Query Service] peut être utilisé pour préserver la qualité de vos données grâce au processus de filtrage des robots.

Le filtrage des robots vous permet de maintenir la qualité de vos données en supprimant globalement la contamination des données résultant d’interactions non humaines avec votre site web. Ce processus est réalisé à l’aide de la combinaison de requêtes SQL et de machine learning.

L’activité des robots peut être identifiée de différentes manières. L’approche adoptée dans ce document se concentre sur les pics d’activité, dans ce cas, le nombre d’actions entreprises par un utilisateur ou une utilisatrice au cours d’une période donnée. Au départ, une requête SQL définit arbitrairement un seuil pour que le nombre d’actions entreprises sur une période donnée soit considéré comme une activité de robots. Ce seuil est ensuite affiné dynamiquement à l’aide d’un modèle de machine learning pour améliorer la précision de ces ratios.

Ce document présente et fournit des exemples détaillés des requêtes de filtrage des robots SQL et des modèles de machine learning nécessaires pour configurer le processus dans votre environnement.

## Prise en main

Dans le cadre de ce processus, qui nécessite l’entraînement d’un modèle de machine learning, ce document suppose une connaissance pratique d’un ou de plusieurs environnements de machine learning.

Cet exemple utilise [!DNL Jupyter Notebook] comme environnement de développement. Bien qu’il existe de nombreuses options disponibles, [!DNL Jupyter Notebook] est recommandé, car il s’agit d’une application web open source qui nécessite peu de calculs. Il peut être [téléchargé sur le site officiel](https://jupyter.org/).

## Utilisez des [!DNL Query Service] pour définir un seuil pour l’activité de robots

Les deux attributs utilisés pour extraire des données pour la détection des robots sont les suivants :

* Identifiant visiteur Experience Cloud (ECID, également appelé MCID) : il s’agit d’un identifiant universel et persistant qui identifie vos visiteurs dans toutes les solutions Adobe.
* Horodatage : fournit l’heure et la date au format UTC auxquelles une activité s’est produite sur le site web.

>[!NOTE]
>
>L’utilisation de `mcid` se trouve toujours dans les références d’espace de noms à l’identifiant visiteur Experience Cloud, comme illustré dans l’exemple ci-dessous.

L’instruction SQL suivante fournit un exemple initial pour identifier l’activité des robots. L’instruction suppose que si un visiteur effectue 50 clics en une minute, l’utilisateur est un robot.

```sql
SELECT * 
FROM   <YOUR_TABLE_NAME> 
WHERE  enduserids._experience.mcid NOT IN (SELECT enduserids._experience.mcid 
                                           FROM   <YOUR_TABLE_NAME> 
                                           GROUP  BY Unix_timestamp(timestamp) / 
                                                     60, 
                                                     enduserids._experience.mcid 
                                           HAVING Count(*) > 50);  
```

L’expression filtre les ECID (`mcid`) de tous les visiteurs qui respectent le seuil, mais ne traite pas les pics de trafic provenant d’autres intervalles.

## Amélioration de la détection des robots avec le machine learning

L’instruction SQL initiale peut être affinée pour devenir une requête d’extraction de fonctionnalité pour le machine learning. L’amélioration de la requête devrait produire davantage de fonctionnalités pour divers intervalles afin d’entraîner des modèles de machine learning avec une précision élevée.

L’exemple d’instruction est étendu d’une minute avec jusqu’à 60 clics, afin d’inclure des périodes de cinq minutes et de 30 minutes avec des nombres de clics de 300 et 1 800, respectivement.

L’exemple d’instruction collecte le nombre maximal de clics pour chaque ECID (`mcid`) sur les différentes durées. L’instruction initiale a été étendue pour inclure des périodes d’une minute (60 secondes), de 5 minutes (300 secondes) et d’une heure (1 800 secondes).

```sql
SELECT table_count_1_min.mcid AS id, 
       count_1_min, 
       count_5_mins, 
       count_30_mins 
FROM   ( ( (SELECT mcid, 
                 Max(count_1_min) AS count_1_min 
          FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                         Count(*)                       AS count_1_min 
                  FROM 
       <YOUR_TABLE_NAME> 
                  GROUP  BY Unix_timestamp(timestamp) / 60, 
                            enduserids._experience.mcid.id) 
          GROUP BY mcid) AS table_count_1_min 
           LEFT JOIN (SELECT mcid, 
                             Max(count_5_mins) AS count_5_mins 
                      FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                     Count(*)                       AS 
                                     count_5_mins 
                              FROM 
           <YOUR_TABLE_NAME> 
                              GROUP  BY Unix_timestamp(timestamp) / 300, 
                                        enduserids._experience.mcid.id) 
                      GROUP  BY mcid) AS table_count_5_mins 
                  ON table_count_1_min.mcid = table_count_5_mins.mcid ) 
         LEFT JOIN (SELECT mcid, 
                           Max(count_30_mins) AS count_30_mins 
                    FROM   (SELECT enduserids._experience.mcid.id AS mcid, 
                                   Count(*)                       AS 
                                   count_30_mins 
                            FROM 
         <YOUR_TABLE_NAME> 
                            GROUP  BY Unix_timestamp(timestamp) / 1800, 
                                      enduserids._experience.mcid.id) 
                    GROUP  BY mcid) AS table_count_30_mins 
                ON table_count_1_min.mcid = table_count_30_mins.mcid ) 
```

Le résultat de cette expression peut ressembler au tableau fourni ci-dessous.

| `id` | `count_1_min` | `count_5_min` | `count_30_min` |
|---|---|---|---|
| 4833075303848917832 | 1 | 1 | 1 |
| 1469109497068938520 | 1 | 1 | 1 |
| 5045682519445554093 | 1 | 1 | 1 |
| 7148203816406620066 | 3 | 3 | 3 |
| 1013065429311352386 | 1 | 1 | 1 |
| 3077475871984695013 | 7 | 7 | 7 |
| 4151486040344674930 | 2 | 2 | 2 |
| 6563366098591762751 | 6 | 6 | 6 |
| 2403566105776993627 | 4 | 4 | 4 |
| 5710530640819698543 | 1 | 1 | 1 |
| 3675089655839425960 | 1 | 1 | 1 |
| 9091930660723241307 | 1 | 1 | 1 |

## Identification de nouveaux seuils de pic à l’aide du machine learning

Ensuite, exportez le jeu de données de requête obtenu au format CSV, puis importez-le dans [!DNL Jupyter Notebook]. À partir de cet environnement, vous pouvez entraîner un modèle de machine learning à l’aide des bibliothèques de machine learning actuelles. Consultez le guide de dépannage pour plus d’informations sur [&#x200B; comment exporter des données de  [!DNL Query Service]  au format CSV &#x200B;](../troubleshooting-guide.md#export-csv)

Les seuils de pic ad hoc initialement établis ne sont pas pilotés par les données et manquent donc de précision. Les modèles de machine learning peuvent être utilisés pour entraîner des paramètres en tant que seuils. Par conséquent, vous pouvez augmenter l’efficacité des requêtes en réduisant le nombre de mots-clés `GROUP BY` en supprimant les fonctionnalités inutiles.

Cet exemple utilise la bibliothèque de machine learning Scikit-Learn qui est installée par défaut avec [!DNL Jupyter Notebook]. La bibliothèque Python « pandas » est également importée pour être utilisée ici. Les commandes suivantes sont entrées dans [!DNL Jupyter Notebook].

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

Ensuite, vous devez entraîner un classificateur d’arbre de décision sur le jeu de données et observer la logique résultant du modèle.

La bibliothèque « Matplotlib » est utilisée pour visualiser le classificateur d’arborescence de décision dans l’exemple ci-dessous.

```shell
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree
from matplotlib import pyplot as plt

X = df.iloc[:,:[1,3]]
y = df.iloc[:,-1]

clf = DecisionTreeClassifier(max_leaf_nodes=2, random_state=0)
clf.fit(X,y)

print("Model Accuracy: {:.5f}".format(clf.scre(X,y)))

tree.plot_tree(clf,feature_names=X.columns)
plt.show()
```

Les valeurs renvoyées par [!DNL Jupyter Notebook] pour cet exemple sont les suivantes.

```text
Model Accuracy: 0.99935
```

![Sortie statistique [!DNL Jupyter Notebook] modèle de machine learning.](../images/use-cases/jupiter-notebook-output.png)

Les résultats du modèle illustré dans l’exemple ci-dessus sont précis à plus de 99 %.

Comme le classificateur d’arborescence de décision peut être entraîné à l’aide de données provenant de [!DNL Query Service] à une cadence régulière à l’aide de requêtes planifiées, vous pouvez garantir l’intégrité des données en filtrant l’activité des robots avec un haut degré de précision. En utilisant les paramètres dérivés du modèle de machine learning , les requêtes originales peuvent être mises à jour avec les paramètres très précis créés par le modèle.

L’exemple de modèle a déterminé avec un haut degré de précision que tous les visiteurs avec plus de 130 interactions en cinq minutes sont des robots. Ces informations peuvent désormais être utilisées pour affiner le filtrage des requêtes SQL par les robots.

## Étapes suivantes

Grâce à la lecture de ce document, vous comprenez mieux comment utiliser le [!DNL Query Service] et le machine learning pour déterminer et filtrer l’activité des robots.

Le [cas d’utilisation de navigation abandonnée](./abandoned-browse.md) est un autre document qui démontre les avantages de l’[!DNL Query Service] aux informations commerciales stratégiques de votre organisation.
