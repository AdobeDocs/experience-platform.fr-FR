---
title: Connexion de Jupyter Notebook à Query Service
description: Découvrez comment connecter Jupyter Notebook à Adobe Experience Platform Query Service.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 10%

---

# Connecter [!DNL Jupyter Notebook] à Query Service

Ce document décrit les étapes requises pour se connecter. [!DNL Jupyter Notebook] avec Adobe Experience Platform Query Service.

## Prise en main

Ce guide nécessite que vous ayez déjà accès à [!DNL Jupyter Notebook] et connaissent bien son interface. Pour télécharger [!DNL Jupyter Notebook] ou pour plus d’informations, consultez la [documentation officielle de  [!DNL Jupyter Notebook] ](https://jupyter.org/).

Pour acquérir les informations d’identification nécessaires à la connexion de [!DNL Jupyter Notebook] à Experience Platform, vous devez avoir accès à l’espace de travail Requêtes dans l’interface utilisateur de Platform.  Contactez l’administrateur de votre entreprise si vous n’avez pas actuellement accès à la variable [!UICONTROL Requêtes] workspace.

>[!TIP]
>
>[!DNL Anaconda Navigator] est une interface utilisateur graphique de bureau qui permet d’installer et de lancer plus facilement des [!DNL Python] des programmes tels que [!DNL Jupyter Notebook]. Il permet également de gérer des packages, des environnements et des canaux sans utiliser de commandes de ligne de commande.
>Suivez le processus d’installation guidé de leur site web pour [installez la version préférée de l’application.](https://docs.anaconda.com/anaconda/install/).
>Dans l’écran d’accueil du navigateur Anaconda, sélectionnez **[!DNL Jupyter Notebook]** dans la liste des applications prises en charge pour lancer le programme.
>Vous trouverez plus d’informations dans la section [documentation officielle d’Anaconda](https://docs.anaconda.com/anaconda/navigator/).

La documentation officielle de Jupyter fournit des instructions à [exécuter le notebook à partir de l’interface de ligne de commande ;](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (interface en ligne de commande).

## Launch [!DNL Jupyter Notebook]

Après avoir ouvert une nouvelle [!DNL Jupyter Notebook] application web, sélectionnez **[!DNL New]** de l’interface utilisateur, suivie de **[!DNL Python 3]** pour créer un nouveau notebook. Le [!DNL Notebook] s’affiche.

Sur la première ligne de la variable [!DNL Notebook] , saisissez la valeur suivante : `pip install psycopg2-binary` et sélectionnez **[!DNL Run]** dans la barre de commande. Un message de réussite s’affiche sous la ligne d’entrée.

>[!IMPORTANT]
>
>Pour établir une connexion, vous devez sélectionner **[!DNL Run]** pour exécuter chaque ligne de code.

Importez ensuite un [!DNL PostgreSQL] adaptateur de base de données pour [!DNL Python]. Saisissez la valeur : `import psycopg2`et sélectionnez **[!DNL Run]**. Il n’existe aucun message de réussite pour ce processus. En l’absence de message d’erreur, passez à l’étape suivante.

Vous devez maintenant fournir vos informations d’identification Adobe Experience Platform en saisissant la valeur : `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Vos informations d’identification de connexion se trouvent dans la section [!UICONTROL Requêtes] , sous [!UICONTROL Informations d’identification] de l’interface utilisateur de Platform. Consultez la documentation sur la manière de [recherche des informations d’identification de votre organisation](../ui/credentials.md) pour obtenir des instructions détaillées.

Il est recommandé d’utiliser des informations d’identification non arrivant à expiration lors de l’utilisation de clients tiers afin d’économiser l’effort de saisie répétée de vos informations. Consultez la documentation pour obtenir des instructions sur [comment générer et utiliser des informations d’identification non arrivées à expiration](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Lors de la copie des informations d’identification à partir de l’interface utilisateur de Platform, il n’est pas nécessaire d’effectuer une mise en forme supplémentaire des informations d’identification. Elles peuvent être données sur une seule ligne, avec un seul espace entre les propriétés et les valeurs. Les informations d’identification sont entourées de guillemets et **not** séparés par des virgules.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

Votre [!DNL Jupyter Notebook] est désormais connectée à Query Service.

## Exemple d&#39;exécution de requête

Maintenant que vous êtes connecté [!DNL Jupyter Notebook] vers Query Service, vous pouvez exécuter des requêtes sur vos jeux de données à l’aide de votre [!DNL Notebook] entrées. L’exemple suivant utilise une requête simple pour démontrer le processus.

Saisissez les valeurs suivantes :

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

Appelez ensuite le paramètre (`data` dans l’exemple ci-dessus) pour afficher les résultats de la requête dans une réponse non formatée.

Pour formater les résultats de manière plus lisible, utilisez les commandes suivantes :

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

Ces commandes ne génèrent pas de message de réussite. S&#39;il n&#39;y a pas de message d&#39;erreur, vous pouvez alors utiliser une fonction pour générer les résultats de votre requête SQL dans un format de tableau.

Saisissez et exécutez le `df.head()` pour afficher les résultats de la requête tabulée.

## Étapes suivantes

Maintenant que vous êtes connecté à Query Service, vous pouvez utiliser [!DNL Jupyter Notebook] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
