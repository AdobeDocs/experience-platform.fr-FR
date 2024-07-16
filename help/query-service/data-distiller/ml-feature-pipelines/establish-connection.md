---
title: Connexion à Data Distiller à partir d’un notebook Jupyter
description: Découvrez comment vous connecter à Data Distiller à partir d’un notebook Jupyter.
exl-id: e6238b00-aaeb-40c0-a90f-9aebb1a1c421
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# Connexion à Data Distiller à partir d’un notebook Jupyter

Pour enrichir vos pipelines d’apprentissage automatique avec des données d’expérience client de grande valeur, vous devez d’abord vous connecter à Data Distiller à partir de [!DNL Jupyter Notebooks]. Ce document décrit les étapes à suivre pour se connecter à Data Distiller à partir d’un notebook [!DNL Python] dans votre environnement d’apprentissage automatique.

## Commencer

Ce guide suppose que vous connaissez les notebooks interactifs [!DNL Python] et que vous avez accès à un environnement de notebook. Le notebook peut être hébergé dans un environnement d’apprentissage automatique basé sur le cloud ou localement avec [[!DNL Jupyter Notebook]](https://jupyter.org/).

### Obtention des informations d’identification de connexion {#obtain-credentials}

Pour vous connecter à Data Distiller et à d’autres services Adobe Experience Platform, vous avez besoin d’informations d’identification d’API Experience Platform. Les informations d’identification d’API peuvent être créées dans le [Adobe Developer Console](https://developer.adobe.com/console/home) par une personne disposant d’un accès Développeur à l’Experience Platform. Il est recommandé de créer des informations d’identification d’API Oauth2 spécifiquement pour les processus de science des données et de demander à un administrateur système d’Adobe de votre entreprise d’attribuer les informations d’identification à un rôle avec les autorisations appropriées.

Pour obtenir des instructions détaillées sur la création d’informations d’identification d’API et l’obtention des autorisations requises, voir [Authentification et accès aux API Experience Platform](../../../landing/api-authentication.md) .

Voici quelques-unes des autorisations recommandées pour la science des données :

- Environnement(s) de test qui sera utilisé pour la science des données (généralement `prod`)
- Modélisation des données : [!UICONTROL Gérer les schémas]
- Gestion des données : [!UICONTROL Gérer les jeux de données]
- Ingestion de données : [!UICONTROL Afficher les sources]
- Destinations : [!UICONTROL Gérer et activer les destinations de jeu de données]
- Query Service : [!UICONTROL Gérer les requêtes]

Par défaut, un rôle (et les informations d’identification d’API affectées à ce rôle) ne peuvent pas accéder aux données étiquetées. Sous réserve des politiques de gouvernance des données de l’organisation, un administrateur système peut accorder au rôle l’accès à certaines données étiquetées jugées appropriées pour l’utilisation de la science des données. Les clients de Platform sont chargés de gérer l’accès aux étiquettes et les stratégies de manière appropriée afin de se conformer aux réglementations et aux politiques organisationnelles pertinentes.

### Stocker les informations d’identification dans un fichier de configuration distinct {#store-credentials}

Pour préserver la sécurité de vos informations d’identification, il est recommandé d’éviter d’écrire des informations d’identification directement dans votre code. Conservez plutôt les informations d’identification dans un fichier de configuration distinct et lisez les valeurs nécessaires pour vous connecter à l’Experience Platform et à Data Distiller.

Par exemple, vous pouvez créer un fichier appelé `config.ini` et inclure les informations suivantes (ainsi que toute autre information, comme les identifiants de jeu de données, qui serait utile pour enregistrer entre les sessions) :

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

Dans votre notebook, vous pouvez ensuite lire les informations d’identification en mémoire à l’aide du package `configParser` de la bibliothèque [!DNL Python] standard :

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)
```

Vous pouvez ensuite référencer des valeurs d’informations d’identification dans votre code comme suit :

```python
org_id = config.get('Credential', 'ims_org_id')
```

## Installation de la bibliothèque aepp Python {#install-python-library}

[aepp](https://github.com/adobe/aepp/tree/main) est une bibliothèque [!DNL Python] Open Source gérée par l’Adobe qui fournit des fonctions pour se connecter à Data Distiller et envoyer des requêtes, comme envoyer des requêtes à d’autres services Experience Platform. La bibliothèque `aepp` repose à son tour sur le package d’adaptateur de base de données PostgreSQL `psycopg2` pour les requêtes interactives Data Distiller. Il est possible de se connecter à Data Distiller et de lancer des requêtes sur des jeux de données Experience Platform avec `psycopg2` uniquement, mais `aepp` offre plus de commodité et des fonctionnalités supplémentaires pour envoyer des requêtes à tous les services API Experience Platform.

Pour installer ou mettre à niveau `aepp` et `psycopg2` dans votre environnement, vous pouvez utiliser la commande magique `%pip` dans votre notebook :

```python
%pip install --upgrade aepp
%pip install --upgrade psycopg2-binary
```

Vous pouvez ensuite configurer la bibliothèque `aepp` avec vos informations d’identification à l’aide du code suivant :

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)

# Configure aepp with your credentials
import aepp

aepp.configure(
  org_id=config.get('Credential', 'ims_org_id'),
  sandbox=config.get('Credential', 'sandbox_name'),
  client_id=config.get('Credential', 'client_id'), 
  secret=config.get('Credential', 'client_secret'),
  scopes=config.get('Credential', 'scopes'),
  tech_id=config.get('Credential', 'tech_acct_id')
)
```

## Création d’une connexion à Data Distiller {#create-connection}

Une fois `aepp` configuré avec vos informations d’identification, vous pouvez utiliser le code suivant pour créer une connexion à Data Distiller et démarrer une session interactive comme suit :

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

Vous pouvez ensuite interroger les jeux de données dans votre environnement de test Experience Platform. Étant donné l’identifiant d’un jeu de données que vous souhaitez interroger, vous pouvez récupérer le nom de table correspondant à partir du service de catalogue et exécuter des requêtes sur la table :

```python
table_name = 'ecommerce_events'
simple_query = f'''SELECT * FROM {table_name} LIMIT 5'''
dd_cursor.query(simple_query)
```

### Connexion à un seul jeu de données pour des performances de requête plus rapides {#connect-to-single-dataset}

Par défaut, la connexion à Data Distiller se connecte à tous les jeux de données de votre environnement de test. Pour accélérer les requêtes et réduire l’utilisation des ressources, vous pouvez vous connecter à un jeu de données spécifique qui vous intéresse. Pour ce faire, remplacez le `dbname` de l’objet de connexion de Data Distiller par `{sandbox}:{table_name}` :

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## Étapes suivantes

En lisant ce document, vous avez appris à vous connecter à Data Distiller à partir d’un notebook [!DNL Python] dans votre environnement d’apprentissage automatique. L’étape suivante de la création de pipelines de fonctionnalités à partir d’Experience Platform pour alimenter les modèles personnalisés dans votre environnement d’apprentissage automatique est d’ [explorer et analyser vos jeux de données](./exploratory-analysis.md).
