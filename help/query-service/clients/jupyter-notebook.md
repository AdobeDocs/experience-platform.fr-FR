---
title: Connexion de Jupyter Notebook à Query Service
description: Découvrez comment connecter Jupyter Notebook à Adobe Experience Platform Query Service.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 4%

---

# Connecter [!DNL Jupyter Notebook] à Query Service

Ce document décrit les étapes requises pour se connecter à [!DNL Jupyter Notebook] avec Adobe Experience Platform Query Service.

## Commencer

Ce guide nécessite que vous ayez déjà accès à [!DNL Jupyter Notebook] et que vous connaissiez son interface. Pour télécharger [!DNL Jupyter Notebook] ou plus d&#39;informations, consultez la [documentation officielle [!DNL Jupyter Notebook] 3}.](https://jupyter.org/)

Pour obtenir les informations d’identification nécessaires à la connexion de [!DNL Jupyter Notebook] à l’Experience Platform, vous devez avoir accès à l’espace de travail [!UICONTROL Requêtes] dans l’interface utilisateur de Platform. Contactez l’administrateur de votre organisation si vous n’avez pas actuellement accès à l’espace de travail [!UICONTROL Requêtes].

>[!TIP]
>
>[!DNL Anaconda Navigator] est une interface utilisateur graphique de bureau (GUI) qui permet d’installer et de lancer plus facilement des programmes [!DNL Python] courants tels que [!DNL Jupyter Notebook]. Il permet également de gérer des packages, des environnements et des canaux sans utiliser de commandes de ligne de commande.
>Suivez le processus d’installation guidé sur leur site web pour [installer la version préférée de l’application](https://docs.anaconda.com/anaconda/install/).
>Sur l’écran d’accueil du navigateur Anaconda, sélectionnez **[!DNL Jupyter Notebook]** dans la liste des applications prises en charge pour lancer le programme.
>Vous trouverez plus d&#39;informations dans la [documentation officielle d&#39;Anaconda](https://docs.anaconda.com/anaconda/navigator/).

La documentation officielle de Jupyter fournit des instructions pour [exécuter le notebook à partir de l’interface de ligne de commande](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI).

## Launch [!DNL Jupyter Notebook]

Après avoir ouvert une nouvelle application web [!DNL Jupyter Notebook], sélectionnez la liste déroulante **[!DNL New]** de l’interface utilisateur, puis **[!DNL Python 3]** pour créer un nouveau notebook. L’éditeur [!DNL Notebook] s’affiche.

Sur la première ligne de l&#39;éditeur [!DNL Notebook], saisissez la valeur suivante : `pip install psycopg2-binary` et sélectionnez **[!DNL Run]** dans la barre de commande. Un message de réussite s’affiche sous la ligne d’entrée.

>[!IMPORTANT]
>
>Dans le cadre de ce processus pour former une connexion, vous devez sélectionner **[!DNL Run]** pour exécuter chaque ligne de code.

Importez ensuite un adaptateur de base de données [!DNL PostgreSQL] pour [!DNL Python]. Saisissez la valeur : `import psycopg2` et sélectionnez **[!DNL Run]**. Il n’existe aucun message de réussite pour ce processus. En l’absence de message d’erreur, passez à l’étape suivante.

Vous devez maintenant fournir vos informations d’identification Adobe Experience Platform en saisissant la valeur : `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Vos informations d’identification de connexion se trouvent dans la section [!UICONTROL Requêtes], sous l’onglet [!UICONTROL Informations d’identification] de l’interface utilisateur de Platform. Pour obtenir des instructions détaillées, consultez la documentation sur la [recherche des informations d’identification de votre organisation](../ui/credentials.md) .

Il est recommandé d’utiliser des informations d’identification non arrivant à expiration lors de l’utilisation de clients tiers afin d’économiser l’effort de saisie répétée de vos informations. Consultez la documentation pour obtenir des instructions sur [la génération et l’utilisation des informations d’identification non arrivant à expiration](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Lors de la copie des informations d’identification à partir de l’interface utilisateur de Platform, il n’est pas nécessaire d’effectuer une mise en forme supplémentaire des informations d’identification. Elles peuvent être données sur une seule ligne, avec un seul espace entre les propriétés et les valeurs. Les informations d’identification sont incluses entre guillemets et **not** séparées par des virgules.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

Votre instance [!DNL Jupyter Notebook] est maintenant connectée à Query Service.

## Exemple d&#39;exécution de requête

Maintenant que vous avez connecté [!DNL Jupyter Notebook] à Query Service, vous pouvez exécuter des requêtes sur vos jeux de données à l’aide de vos entrées [!DNL Notebook]. L’exemple suivant utilise une requête simple pour démontrer le processus.

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

Saisissez et exécutez la fonction `df.head()` pour afficher les résultats de la requête tabularisée.

## Étapes suivantes

Maintenant que vous êtes connecté à Query Service, vous pouvez utiliser [!DNL Jupyter Notebook] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
