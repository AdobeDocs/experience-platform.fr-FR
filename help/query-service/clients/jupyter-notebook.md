---
title: Connecter le notebook Jupyter à Query Service
description: Découvrez comment connecter le notebook Jupyter à Adobe Experience Platform Query Service.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 4%

---

# Connecter [!DNL Jupyter Notebook] à Query Service

Ce document décrit les étapes à suivre pour connecter [!DNL Jupyter Notebook] à Adobe Experience Platform Query Service.

## Commencer

Ce guide nécessite que vous ayez déjà accès à [!DNL Jupyter Notebook] et que vous connaissiez son interface. Pour télécharger [!DNL Jupyter Notebook] ou pour plus d’informations, consultez la [documentation  [!DNL Jupyter Notebook] officielle](https://jupyter.org/).

Pour acquérir les informations d’identification nécessaires à la connexion de [!DNL Jupyter Notebook] à Experience Platform, vous devez avoir accès à l’espace de travail [!UICONTROL Requêtes] dans l’interface utilisateur d’Experience Platform. Veuillez contacter l’administrateur de votre organisation si vous n’avez pas actuellement accès à l’espace de travail [!UICONTROL Requêtes].

>[!TIP]
>
>[!DNL Anaconda Navigator] est une interface utilisateur graphique (GUI) de bureau qui permet d’installer et de lancer plus facilement des programmes de [!DNL Python] courants tels que [!DNL Jupyter Notebook]. Il permet également de gérer les packages, les environnements et les canaux sans utiliser de commandes de ligne de commande.
>Suivez le processus d’installation guidé sur leur site web pour [installer la version de l’application que vous préférez](https://docs.anaconda.com/anaconda/install/).
>Sur l&#39;écran d&#39;accueil du Navigateur Anaconda, sélectionnez **[!DNL Jupyter Notebook]** dans la liste des applications prises en charge pour lancer le programme.
>Vous trouverez plus d’informations dans la [documentation officielle d’Anaconda](https://docs.anaconda.com/anaconda/navigator/).

La documentation officielle de Jupyter fournit des instructions pour [&#x200B; exécuter le notebook à partir de l’interface de ligne de commande &#x200B;](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI).

## Launch [!DNL Jupyter Notebook]

Après avoir ouvert une nouvelle application web [!DNL Jupyter Notebook], sélectionnez la liste déroulante **[!DNL New]** dans l’interface utilisateur, puis **[!DNL Python 3]** pour créer un notebook. L’éditeur de [!DNL Notebook] s’affiche.

Sur la première ligne de l’éditeur de [!DNL Notebook], saisissez la valeur suivante : `pip install psycopg2-binary` et sélectionnez **[!DNL Run]** dans la barre de commandes. Un message de réussite s’affiche sous la ligne de saisie.

>[!IMPORTANT]
>
>Dans le cadre de ce processus de création d’une connexion, vous devez sélectionner **[!DNL Run]** pour exécuter chaque ligne de code.

Importez ensuite un adaptateur de base de données [!DNL PostgreSQL] pour [!DNL Python]. Saisissez la valeur : `import psycopg2` et sélectionnez **[!DNL Run]**. Il n’y a aucun message de réussite pour ce processus. S’il n’y a aucun message d’erreur, passez à l’étape suivante.

Vous devez maintenant fournir vos identifiants Adobe Experience Platform en saisissant la valeur : `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Vos informations d’identification de connexion se trouvent dans la section [!UICONTROL Requêtes], sous l’onglet [!UICONTROL Informations d’identification] de l’interface utilisateur d’Experience Platform. Consultez la documentation sur la façon de [trouver les informations d’identification de votre organisation](../ui/credentials.md) pour obtenir des instructions détaillées.

L’utilisation d’informations d’identification non expirantes est recommandée lors de l’utilisation de clients tiers afin d’éviter la saisie répétée de vos informations. Consultez la documentation pour obtenir des instructions sur [comment générer et utiliser des informations d’identification non expirantes](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Lors de la copie d’informations d’identification depuis l’interface utilisateur d’Experience Platform, aucune mise en forme supplémentaire des informations d’identification n’est nécessaire. Elles peuvent être données sur une seule ligne, avec un seul espace entre les propriétés et les valeurs. Les informations d’identification sont placées entre guillemets et **non** séparées par des virgules.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

Votre instance [!DNL Jupyter Notebook] est maintenant connectée à Query Service.

## Exemple d’exécution de requête

Maintenant que vous avez connecté [!DNL Jupyter Notebook] à Query Service, vous pouvez exécuter des requêtes sur vos jeux de données à l’aide de vos entrées [!DNL Notebook]. L’exemple suivant utilise une requête simple pour démontrer le processus .

Saisissez les valeurs suivantes :

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

Ensuite, appelez le paramètre (`data` dans l’exemple ci-dessus) pour afficher les résultats de la requête dans une réponse non formatée.

Pour formater les résultats de manière plus lisible, utilisez les commandes suivantes :

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

Ces commandes ne génèrent pas de message de réussite. S’il n’existe aucun message d’erreur, vous pouvez utiliser une fonction pour générer les résultats de votre requête SQL sous la forme d’une table.

Saisissez et exécutez la fonction `df.head()` pour afficher les résultats de la requête tabulée.

## Étapes suivantes

Maintenant que vous êtes connecté à Query Service, vous pouvez utiliser [!DNL Jupyter Notebook] pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, veuillez lire le [guide relatif aux requêtes en cours d’exécution](../best-practices/writing-queries.md).
