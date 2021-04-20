---
keywords: Experience Platform ; JupyterLab ; blocs-notes ; Espace de travail des données ; rubriques populaires ; analyser les blocs-notes de données
solution: Experience Platform
title: Analyse de vos données à l'aide de portables
topic: tutorial
type: Tutorial
description: Ce didacticiel se concentre sur l’utilisation des ordinateurs portables Jupyter, construits dans Data Science Workspace, pour accéder à vos données, les explorer et les visualiser.
translation-type: tm+mt
source-git-commit: 6908c582cb7e0d60b82112dbc0854411d76b4fd4
workflow-type: tm+mt
source-wordcount: '1733'
ht-degree: 76%

---


# Analyse de vos données à l’aide de notebooks

Ce didacticiel se concentre sur l’utilisation des ordinateurs portables Jupyter, construits dans Data Science Workspace, pour accéder à vos données, les explorer et les visualiser. D&#39;ici la fin de ce tutoriel, vous devriez avoir une bonne connaissance de certaines des fonctionnalités de l&#39;offre des portables Jupyter pour mieux comprendre vos données.

Les concepts suivants sont présentés :

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) est l&#39;interface web de nouvelle génération pour Project Jupyter et est étroitement intégrée dans  [!DNL Adobe Experience Platform].
- **Lots :** les jeux de données sont constitués de lots. Un lot est un ensemble de données collectées sur une période donnée et traitées ensemble comme une seule unité. De nouveaux lots sont créés lorsque des données sont ajoutées à un jeu de données.
- **SDK Data Access (obsolète) :** le SDK Data Access est désormais obsolète. Veuillez utiliser le guide [[!DNL Platform SDK]](../authoring/platform-sdk.md).

## Exploration de notebooks dans Data Science Workspace

Dans cette section, nous explorons les données qui ont été précédemment intégrées au schéma de ventes au détail.

Data Science Workspace permet aux utilisateurs de créer [!DNL Jupyter Notebooks] via la plate-forme [!DNL JupyterLab] où ils peuvent créer et modifier des workflows d’apprentissage automatique. [!DNL JupyterLab] est un outil de collaboration serveur-client qui permet aux utilisateurs de modifier des documents de notebooks par le biais d’un navigateur web. Ces notebooks peuvent contenir à la fois du code exécutable et des éléments de texte enrichi. Pour nos besoins, nous utiliserons Markdown pour la description de l&#39;analyse et le code exécutable [!DNL Python] pour effectuer l&#39;exploration et l&#39;analyse des données.

### Sélection de votre espace de travail

Lors du lancement de [!DNL JupyterLab], une interface Web est présentée pour les portables Jupyter. Selon le type de notebook sélectionné, un noyau correspondant sera lancé.

Lors de la comparaison des environnements à utiliser, il faut tenir compte des limites de chaque service. Par exemple, si nous utilisons la bibliothèque [pandas](https://pandas.pydata.org/) avec , la limite de RAM pour les utilisateurs réguliers est de 2 Go. [!DNL Python] Les utilisateurs avancés sont eux limités à 20 Go de RAM. S&#39;il s&#39;agit de calculs plus volumineux, il serait logique d&#39;utiliser [!DNL Spark] qui offre 1,5 To et qui est partagé avec toutes les instances d&#39;ordinateur portable.

Par défaut, la recette Tensorflow fonctionne dans un cluster GPU et Python s’exécute dans un cluster CPU.

### Création d’un nouveau filtre

Dans l&#39;interface utilisateur [!DNL Adobe Experience Platform], cliquez sur l&#39;onglet Data Science dans le menu supérieur pour accéder à Data Science Workspace. Dans cette page, cliquez sur l&#39;onglet [!DNL JupyterLab] qui ouvre le lanceur [!DNL JupyterLab]. Vous devriez voir une page similaire à celle-ci.

![](../images/jupyterlab/analyze-data/jupyterlab-launcher.png)

Dans notre tutoriel, nous utiliserons [!DNL Python] 3 dans le carnet Jupyter pour montrer comment accéder aux données et les explorer. Sur la page du lanceur, vous trouverez des notebooks d’exemple. Nous utiliserons la recette Ventes au détail pour [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

La recette Ventes au détail constitue un exemple autonome qui utilise le même jeu de données Ventes au détail pour illustrer la manière dont les données peuvent être explorées et visualisées dans Jupyter Notebook. En outre, le notebook approfondit encore la formation et la vérification. Vous trouverez plus d’informations sur ce notebook en particulier dans cette [présentation détaillée](../walkthrough.md).

### Accès aux données

>[!NOTE]
>
>Le paramètre `data_access_sdk_python` est obsolète et n’est plus recommandé. Consultez le tutoriel de [conversion du SDK Data Access vers SDK Platform](../authoring/platform-sdk.md) pour convertir votre code. Les étapes décrites ci-dessous s’appliquent également à ce tutoriel.

Nous allons passer en revue l&#39;accès aux données en interne à partir de [!DNL Adobe Experience Platform] et aux données en externe. Nous passerons par la bibliothèque `data_access_sdk_python` pour accéder aux données internes telles que les jeux de données et les schémas XDM. Pour les données externes, nous utiliserons la bibliothèque pandas [!DNL Python].

#### Données externes

Une fois le notebook Ventes au détail ouvert, cherchez l’en-tête « Charger les données ». Le code [!DNL Python] suivant utilise la structure de données pandas&#39; `DataFrame` et la fonction [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) pour lire le fichier CSV hébergé sur [!DNL Github] dans DataFrame :

![](../images/jupyterlab/analyze-data/read_csv.png)

La structure de données du DataFrame de pandas est une structure de données étiquetées en deux dimensions. Pour voir rapidement les dimensions de nos données, nous pouvons utiliser `df.shape`. Cette opération renvoie un tuple qui représente les dimensions du DataFrame :

![](../images/jupyterlab/analyze-data/df_shape.png)

Enfin, nous pouvons avoir un aperçu de l’apparence de nos données. Nous pouvons utiliser `df.head(n)` pour voir les `n` premières lignes du DataFrame :

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] data

Nous allons maintenant passer en revue l&#39;accès aux données [!DNL Experience Platform].

##### Par identifiant du jeu de données

Pour cette section, nous utilisons le jeu de données Ventes au détail, le même que celui utilisé dans le notebook d’exemple Ventes au détail.

Dans Jupyter Notebook, vous pouvez accéder à vos données à partir de l&#39;onglet **Data** ![data](../images/jupyterlab/analyze-data/dataset-tab.png) sur la gauche. Deux dossiers sont fournis lors de la sélection de l’onglet. Sélectionnez le dossier **[!UICONTROL Datasets]**.

![](../images/jupyterlab/analyze-data/dataset_tab.png)

Désormais, dans le répertoire Datasets, vous pouvez voir tous les jeux de données assimilés. Remarque : le chargement de toutes les entrées peut prendre quelques instants si de nombreux jeux de données sont présents dans votre répertoire.

Puisque le jeu de données est le même, nous voulons remplacer les données chargées au cours de la section précédente qui utilise des données externes. Sélectionnez le bloc de code sous **Charger les données** et appuyez deux fois sur la touche **« D »** de votre clavier. Assurez-vous que vous avez bien sélectionné le bloc et non le texte. Vous pouvez appuyer sur **« Echap »** pour désélectionner le texte avant d’appuyer deux fois sur **« D »**.

Nous pouvons maintenant cliquer avec le bouton droit sur le jeu de données `Retail-Training-<your-alias>` et sélectionner l’option « Explorer les données dans le notebook » de la liste déroulante. Une entrée de code exécutable apparaîtra dans votre notebook.

>[!TIP]
>
>Consultez le guide [[!DNL Platform SDK]](../authoring/platform-sdk.md) pour convertir votre code.

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

Si vous travaillez sur d&#39;autres noyaux autres que [!DNL Python], veuillez consulter [cette page](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) pour accéder aux données de [!DNL Adobe Experience Platform].

Sélectionnez la cellule exécutable, puis cliquez sur le bouton de lecture dans la barre d’outils pour exécuter le code exécutable. La sortie pour `head()` sera un tableau comprenant les clés de votre jeu de données sous forme de colonnes et les n premières lignes du jeu de données. `head()` accepte un argument entier pour spécifier le nombre de lignes à générer. Par défaut, cette valeur est définie sur 5.

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

Si vous redémarrez votre noyau et exécutez à nouveau toutes les cellules, vous devriez obtenir les mêmes sorties qu’auparavant.

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### Exploration de vos données

Maintenant que vos données sont accessibles, intéressons-nous aux données elles-mêmes en utilisant les statistiques et la visualisation. Le jeu de données que nous utilisons est un jeu de données relatif aux ventes qui fournit des informations diverses sur 45 boutiques différentes pour un jour donné. Voici quelques caractéristiques pour une `date` et un `store` spécifiques :
- `storeType`
- `weeklySales`
- `storeSize`
- `temperature`
- `regionalFuelPrice`
- `markDown`
- `cpi`
- `unemployment`
- `isHoliday`

#### Résumé statistique

Nous pouvons exploiter la bibliothèque [!DNL Python's] pandas pour obtenir le type de données de chaque attribut. La sortie de l’appel suivant nous donnera des informations sur le nombre d’entrées et le type de données pour chacune des colonnes :

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

Ces informations sont utiles, car elles aident à identifier la méthode de traitement de ces données.

Regardons maintenant le résumé statistique. Seuls les types de données numériques s’affichent. `date`, `storeType` et `isHoliday` ne sont donc pas générés :

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

Grâce à cela, nous pouvons voir qu’il existe 6 435 instances pour chaque caractéristique. Nous obtenons également des informations statistiques, telles que la moyenne, l’écart type, le minimum, le maximum et les plages interquartiles. Cela nous permet d’identifier les variations de données. Dans la section suivante, nous allons passer en revue la visualisation qui accompagne ces informations, afin d’avoir une bonne compréhension de nos données.

En examinant les valeurs minimale et maximale pour `store`, nous voyons que les données représentent 45 boutiques uniques. Les `storeTypes` permettent également de différencier les boutiques. Nous pouvons voir la distribution des `storeTypes` en procédant comme suit :

![](../images/jupyterlab/analyze-data/df_groupby.png)

Ici, nous avons 22 boutiques `storeType` `A`, 17 boutiques `storeType` `B` et 6 boutiques `storeType` `C`.

#### Visualisation des données

Maintenant que nous connaissons les valeurs de notre DataFrame, nous voulons les compléter par des visualisations, afin de rendre les choses plus claires et d’identifier plus facilement les motifs. Les graphiques servent également à transmettre les résultats à une audience. Voici quelques bibliothèques [!DNL Python] utiles pour la visualisation :
- [Matplotlib](https://matplotlib.org/)
- [pandas](https://pandas.pydata.org/)
- [seaborn](https://seaborn.pydata.org/)
- [ggplot](https://ggplot2.tidyverse.org/)

Dans cette section, nous passerons rapidement en revue certains avantages qu’apporte l’utilisation de chaque bibliothèque.

[Matplotlib](https://matplotlib.org/)[!DNL Python] est le plus ancien paquet de visualisation Il a pour but de « simplifier les tâches faciles sans rendre les tâches difficiles impossibles ». Cette affirmation tend à se vérifier, puisque le paquet est extrêmement puissant, mais aussi relativement complexe. Il n’est pas toujours simple d’obtenir un graphique à l’apparence satisfaisante sans y consacrer beaucoup de temps et d’efforts.

[Pandas](https://pandas.pydata.org/) est principalement utilisé pour son objet DataFrame qui permet la manipulation de données avec l’indexation intégrée. Cependant, pandas inclut également une fonctionnalité de traçage intégrée basée sur matplotlib.

[seaborn](https://seaborn.pydata.org/) est un paquet élaboré sur la base de matplotlib. Son principal objectif est de rendre les graphiques par défaut plus attrayants visuellement et de simplifier la création de graphiques complexes.

[ggplot](https://ggplot2.tidyverse.org/) est un paquet également élaboré sur la base de matplotlib. Cependant, sa principale différence est que l’outil est un port de ggplot2 pour R. Tout comme seaborn, l’objectif est de se baser sur matplotlib pour y apporter des améliorations par la suite. Les utilisateurs connaissant bien ggplot2 pour R devraient envisager l’utilisation de cette bibliothèque.


##### Graphiques unidimensionnels

Les graphiques unidimensionnels sont des tracés représentant une seule variable. La boîte à moustaches est un graphique unidimensionnel couramment utilisé pour visualiser les données.

En utilisant le même jeu de données relatif aux ventes, nous pouvons générer un graphique de boîte à moustaches pour chacune des 45 boutiques et leurs ventes hebdomadaires. Le graphique est généré à l’aide de la fonction `seaborn.boxplot`.

![](../images/jupyterlab/analyze-data/box_whisker.png)

Un graphique de boîte à moustaches sert à illustrer la distribution des données. Les lignes extérieures du graphique représentent les quartiles supérieur et inférieur, tandis que la boîte s’étend sur la plage interquartile. La ligne dans la zone indique la médiane. Tout point de données plus de 1,5 fois supérieur ou inférieur au quartile est marqué sous forme de cercle. Ces points sont considérés comme des valeurs aberrantes.

##### Graphiques multidimensionnels

Les graphiques multidimensionnels servent à visualiser les interactions entre les variables. Grâce à cette visualisation, les spécialistes des données peuvent vérifier s’il existe des corrélations ou des motifs entre les variables. La matrice de corrélation est un graphique multidimensionnel couramment utilisé. Avec une matrice de corrélation, les dépendances entre les différentes variables sont quantifiées à l’aide d’un coefficient de corrélation.

En utilisant le même jeu de données relatif aux ventes, nous pouvons générer la matrice de corrélation.

![](../images/jupyterlab/analyze-data/correlation_1.png)

Notez la diagonale de 1 au centre. Elle indique que lorsqu’une variable est comparée à elle-même, elle présente une corrélation positive entière. Une corrélation positive élevée aura une magnitude proche de 1, tandis que les corrélations faibles seront plus proches de 0. Une corrélation négative s’affiche sous la forme d’un coefficient négatif, indiquant une tendance inverse.


## Étapes suivantes

Ce didacticiel explique comment créer un nouveau bloc-notes Jupyter dans Data Science Workspace et comment accéder aux données à l&#39;extérieur ainsi qu&#39;à partir de [!DNL Adobe Experience Platform]. Plus précisément, nous avons réalisé les actions suivantes :
- Créer un nouveau portable Jupyter
- Accès aux jeux de données et aux schémas
- Exploration des jeux de données

Vous êtes maintenant prêt à passer à la [section suivante](../models-recipes/package-source-files-recipe.md) pour empaqueter une recette et importer dans Data Science Workspace.