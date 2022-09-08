---
title: Connexion de Jupyter Notebook à Query Service
description: Découvrez comment connecter Jupyter Notebook à Adobe Experience Platform Query Service.
source-git-commit: f910deca43ac49d3a3452b8dbafda20ffdf3bf48
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 3%

---

# Connexion [!DNL Jupyter Notebook] vers Query Service

Ce document décrit les étapes requises pour se connecter. [!DNL Jupyter Notebook] avec Adobe Experience Platform Query Service.

## Prise en main

Ce guide nécessite que vous ayez déjà accès à [!DNL Jupyter Notebook] et connaissent bien son interface. Pour télécharger [!DNL Jupyter Notebook] ou pour plus d’informations, voir [officiel [!DNL Jupyter Notebook] documentation](https://jupyter.org/).

Pour acquérir les informations d’identification nécessaires à la connexion [!DNL Jupyter Notebook] pour être Experience Platform, vous devez avoir accès au [!UICONTROL Requêtes] dans l’interface utilisateur de Platform. Contactez l’administrateur de votre entreprise si vous n’avez pas actuellement accès à la variable [!UICONTROL Requêtes] workspace.

>[!TIP]
>
>[!DNL Anaconda Navigator] est une interface utilisateur graphique de bureau qui permet d’installer et de lancer plus facilement des [!DNL Python] des programmes tels que [!DNL Jupyter Notebook]. Il permet également de gérer des packages, des environnements et des canaux sans utiliser de commandes de ligne de commande.
>Vous pouvez [installez la version préférée de l’application.](https://docs.anaconda.com/anaconda/install/) de leur site web.
>Suivez le processus d’installation assisté. Dans l’écran d’accueil du navigateur Anaconda, sélectionnez **[!DNL Jupyter Notebook]** dans la liste des applications prises en charge pour lancer le programme.
>![Le [!DNL Anaconda Navigator] écran d’accueil avec [!DNL Jupyter Notebook] surlignée.](../images/clients/jupyter-notebook/anaconda-navigator-home.png)
>Vous trouverez plus d’informations dans leur [documentation officielle](https://docs.anaconda.com/anaconda/navigator/).

## Launch [!DNL Jupyter Notebook]

Après avoir ouvert une nouvelle [!DNL Jupyter Notebook] application web, sélectionnez **[!DNL New]** menu déroulant suivi de **[!DNL Python 3]** pour créer un nouveau notebook. Le [!DNL Notebook] s’affiche.

![Le [!DNL Jupiter Notebook] l’onglet Fichier avec la fonction [!DNL New dropdown] et [!DNL Python] 3 surligné.](../images/clients/jupyter-notebook/new-notebook.png)

Sur la première ligne de la variable [!DNL Notebook] , saisissez la valeur suivante : `pip install psycopg2-binary` et sélectionnez **[!DNL Run]** dans la barre de commande. Un message de réussite s’affiche sous la ligne d’entrée.

>[!IMPORTANT]
>
>Pour établir une connexion, vous devez sélectionner **[!DNL Run]** pour exécuter chaque ligne de code.

![Le [!DNL Notebook] Interface utilisateur avec la commande d’installation des bibliothèques mise en surbrillance.](../images/clients/jupyter-notebook/install-library.png)

Importez ensuite un [!DNL PostgreSQL] adaptateur de base de données pour [!DNL Python]. Saisissez la valeur : `import psycopg2`et sélectionnez **[!DNL Run]**. Il n’existe aucun message de réussite pour ce processus. En l’absence de message d’erreur, passez à l’étape suivante.

![Le [!DNL Notebook] Interface utilisateur avec le code du pilote de la base de données d’importation en surbrillance.](../images/clients/jupyter-notebook/import-dbdriver.png)

Vous devez maintenant fournir vos informations d’identification Adobe Experience Platform en saisissant la valeur : `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Vos informations d’identification de connexion se trouvent dans la section [!UICONTROL Requêtes] , sous [!UICONTROL Informations d’identification] de l’interface utilisateur de Platform. Consultez la documentation sur la manière de [recherche des informations d’identification de votre organisation](../ui/credentials.md) pour obtenir des instructions détaillées.

Il est recommandé d’utiliser des informations d’identification non arrivant à expiration lors de l’utilisation de clients tiers afin d’économiser l’effort de saisie répétée de vos informations. Consultez la documentation pour obtenir des instructions sur [comment générer et utiliser des informations d’identification non arrivées à expiration](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Lors de la copie des informations d’identification à partir de l’interface utilisateur de Platform, assurez-vous qu’il n’existe aucune mise en forme supplémentaire des informations d’identification. Elles doivent toutes se trouver sur une seule ligne, avec un seul espace entre les propriétés et les valeurs. Les informations d’identification sont entourées de guillemets et **not** séparés par des virgules.

![Le [!DNL Notebook] Interface utilisateur avec les informations d’identification de connexion mises en surbrillance.](../images/clients/jupyter-notebook/provide-credentials.png)

Votre [!DNL Jupyter Notebook] est désormais connectée à Query Service.

## Exemple d&#39;exécution de requête

Maintenant que vous êtes connecté [!DNL Jupyter Notebook] vers Query Service, vous pouvez exécuter des requêtes sur vos jeux de données à l’aide de votre [!DNL Notebook] entrées. L’exemple suivant utilise une requête simple pour démontrer le processus.

Saisissez les valeurs suivantes :

```console
cur = conn.cursor()
cur.execute('''{YOUR_QUERY_HERE}''')
data = [r for r in cur]
```

Appelez ensuite le paramètre (`data` dans l’exemple ci-dessus) pour afficher les résultats de la requête dans une réponse non formatée.

![Le [!DNL Notebook] Interface utilisateur avec des commandes pour renvoyer et afficher les résultats SQL dans le notebook.](../images/clients/jupyter-notebook/example-query.png)

Pour formater les résultats de manière plus lisible, utilisez les commandes suivantes :

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`

Ces commandes ne génèrent pas de message de réussite. S&#39;il n&#39;y a pas de message d&#39;erreur, vous pouvez alors utiliser une fonction pour générer les résultats de votre requête SQL dans un format de tableau.

![Commandes requises pour formater les résultats SQL.](../images/clients/jupyter-notebook/format-results-commands.png)

Saisissez et exécutez le `df.head()` pour afficher les résultats de la requête tabulée.

![Résultats tabulés de votre requête SQL dans [!DNL Jupyter Notebook].](../images/clients/jupyter-notebook/format-results-output.png)

## Étapes suivantes

Maintenant que vous êtes connecté à Query Service, vous pouvez utiliser [!DNL Jupyter Notebook] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
