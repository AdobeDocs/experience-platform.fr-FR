---
title: Filtrage des robots dans Query Service avec apprentissage automatique
description: Ce document fournit une vue d’ensemble de l’utilisation de Query Service et de l’apprentissage automatique pour déterminer l’activité des robots et filtrer leurs actions sur le véritable trafic des visiteurs du site Web en ligne.
exl-id: fc9dbc5c-874a-41a9-9b60-c926f3fd6e76
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 5%

---

# Filtrage des robots dans [!DNL Query Service] avec apprentissage automatique

L’activité des robots peut avoir un impact sur les mesures d’analyse et endommager l’intégrité des données. Adobe Experience Platform [!DNL Query Service] peut être utilisé pour maintenir la qualité de vos données par le biais du processus de filtrage des robots.

Le filtrage des robots permet de maintenir la qualité des données en supprimant largement la contamination des données résultant d’interactions non humaines avec votre site web. Ce processus est réalisé grâce à la combinaison de requêtes SQL et d’apprentissage automatique.

L’activité des robots peut être identifiée de différentes manières. L’approche adoptée dans ce document se concentre sur les pics d’activité, dans ce cas, sur le nombre d’actions entreprises par un utilisateur au cours d’une période donnée. Au départ, une requête SQL définit arbitrairement un seuil pour le nombre d’actions entreprises sur une période de temps pour être considérée comme une activité de robot. Ce seuil est ensuite affiné dynamiquement à l’aide d’un modèle d’apprentissage automatique afin d’améliorer la précision de ces ratios.

Ce document fournit un aperçu et des exemples détaillés des requêtes de filtrage de robots SQL et des modèles d’apprentissage automatique nécessaires pour configurer le processus dans votre environnement.

## Commencer

Dans le cadre de ce processus, vous devez entraîner un modèle d’apprentissage automatique. Ce document suppose une connaissance pratique d’un ou de plusieurs environnements d’apprentissage automatique.

Cet exemple utilise [!DNL Jupyter Notebook] comme environnement de développement. Bien qu’il existe de nombreuses options disponibles, [!DNL Jupyter Notebook] est recommandé car il s’agit d’une application web open source qui a de faibles exigences en matière de calcul. Il peut être [téléchargé à partir du site officiel](https://jupyter.org/).

## Utiliser [!DNL Query Service] pour définir un seuil pour l’activité de robot

Les deux attributs utilisés pour extraire les données pour la détection des robots sont les suivants :

* Identifiant visiteur Experience Cloud (ECID) : il fournit un identifiant universel et permanent qui identifie vos visiteurs dans toutes les solutions d’Adobe.
* Horodatage : indique l’heure et la date au format UTC où une activité s’est produite sur le site web.

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

L’expression filtre les ECID (`mcid`) de tous les visiteurs qui atteignent le seuil, mais ne résout pas les pics de trafic d’autres intervalles.

## Amélioration de la détection des robots grâce à l’apprentissage automatique

L’instruction SQL initiale peut être affinée afin de devenir une requête d’extraction de fonctionnalités pour l’apprentissage automatique. La requête améliorée doit produire plus de fonctionnalités pour une variété d’intervalles afin de former des modèles d’apprentissage automatique avec de grandes précision.

L’exemple d’instruction est développé d’une minute avec jusqu’à 60 clics, afin d’inclure des périodes de cinq minutes et de 30 minutes avec des nombres de clics de 300 et de 1 800 respectivement.

L’exemple d’instruction collecte le nombre maximal de clics pour chaque ECID (`mcid`) sur les différentes durées. L’instruction initiale a été développée pour inclure des périodes d’une minute (60 secondes), de 5 minutes (300 secondes) et d’une heure (1 800 secondes).

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

Le résultat de cette expression peut ressembler au tableau ci-dessous.

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

## Identifier les nouveaux seuils de pic à l’aide de l’apprentissage automatique

Ensuite, exportez le jeu de données de requête obtenu au format CSV, puis importez-le dans [!DNL Jupyter Notebook]. Dans cet environnement, vous pouvez entraîner un modèle d’apprentissage automatique à l’aide des bibliothèques d’apprentissage automatique actuelles. Consultez le guide de dépannage pour plus d’informations sur [la manière d’exporter des données de  [!DNL Query Service] au format CSV](../troubleshooting-guide.md#export-csv)

Les seuils de pic ad hoc initialement établis ne sont pas axés sur les données et manquent donc d’exactitude. Les modèles d’apprentissage automatique peuvent être utilisés pour former des paramètres en tant que seuils. Par conséquent, vous pouvez augmenter l’efficacité des requêtes en réduisant le nombre de `GROUP BY` mots-clés en supprimant les fonctionnalités superflues.

Cet exemple utilise la bibliothèque d’apprentissage automatique Scikit-Learn installée par défaut avec [!DNL Jupyter Notebook]. La bibliothèque python &quot;pandas&quot; est également importée pour être utilisée ici. Les commandes suivantes sont entrées dans [!DNL Jupyter Notebook].

```shell
import pandas as ps

df = pd_read.csv('data/bot.csv')
df = df[df['count_1-min'] > 1]
df['is_bot'] = 0
df.loc[df['count_1_min'] > 50,'is_bot'] = 1
df
```

Ensuite, vous devez entraîner une classification d’arborescence de décision sur le jeu de données et observer la logique résultant du modèle.

La bibliothèque &quot;Matplotlib&quot; est utilisée pour visualiser la classification de l’arborescence de décision dans l’exemple ci-dessous.

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

![Sortie statistique de [!DNL Jupyter Notebook] modèle d’apprentissage automatique.](../images/use-cases/jupiter-notebook-output.png)

Les résultats du modèle illustré dans l’exemple ci-dessus sont plus de 99 % précis.

Comme la classificateur de l’arbre de décision peut être formée à l’aide de données provenant de [!DNL Query Service] sur une cadence régulière à l’aide de requêtes planifiées, vous pouvez garantir l’intégrité des données en filtrant l’activité des robots avec un haut degré de précision. En utilisant les paramètres dérivés du modèle d’apprentissage automatique, les requêtes d’origine peuvent être mises à jour avec les paramètres très précis créés par le modèle.

L’exemple de modèle a déterminé avec une grande précision que tous les visiteurs ayant plus de 130 interactions en cinq minutes sont des robots. Ces informations peuvent maintenant être utilisées pour affiner vos requêtes SQL de filtrage de robots.

## Étapes suivantes

En lisant ce document, vous comprenez mieux comment utiliser [!DNL Query Service] et l’apprentissage automatique pour déterminer et filtrer l’activité des robots.

D’autres documents qui montrent les avantages de [!DNL Query Service] pour les informations stratégiques sur les entreprises de votre entreprise sont l’exemple [de cas d’utilisation de navigation abandonnée](./abandoned-browse.md).
