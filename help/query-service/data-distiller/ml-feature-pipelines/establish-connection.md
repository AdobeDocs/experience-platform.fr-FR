---
title: Connexion à Data Distiller à partir d’un notebook Jupyter
description: Découvrez comment vous connecter à Data Distiller à partir d’un notebook Jupyter.
exl-id: e6238b00-aaeb-40c0-a90f-9aebb1a1c421
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Connexion à Data Distiller à partir d’un notebook Jupyter

Pour enrichir vos pipelines de machine learning avec des données d’expérience client à forte valeur ajoutée, vous devez d’abord vous connecter à Data Distiller à partir de [!DNL Jupyter Notebooks]. Ce document décrit les étapes à suivre pour se connecter à Data Distiller à partir d’un notebook [!DNL Python] dans votre environnement de machine learning.

## Commencer

Ce guide suppose que vous connaissez les notebooks [!DNL Python] interactifs et que vous avez accès à un environnement de notebook. Le notebook peut être hébergé dans un environnement de machine learning basé sur le cloud ou localement avec [[!DNL Jupyter Notebook]](https://jupyter.org/).

### Obtention des informations de connexion {#obtain-credentials}

Pour vous connecter à Data Distiller et à d’autres services Adobe Experience Platform, vous avez besoin d’informations d’identification d’API Experience Platform. Les informations d&#39;identification d&#39;API peuvent être créées dans [Adobe Developer Console](https://developer.adobe.com/console/home) par une personne disposant d&#39;un accès développeur à Experience Platform. Il est recommandé de créer des informations d’identification d’API Oauth2 spécifiquement pour les workflows de science des données et de demander à un administrateur système Adobe de votre organisation d’affecter les informations d’identification à un rôle avec les autorisations appropriées.

Consultez [Authentification et accès aux API Experience Platform](../../../landing/api-authentication.md) pour obtenir des instructions détaillées sur la création d’informations d’identification d’API et l’obtention des autorisations requises.

Les autorisations recommandées pour la science des données sont les suivantes :

- Sandbox(s) qui seront utilisés pour la science des données (généralement `prod`)
- Modélisation des données : [!UICONTROL Gérer les schémas]
- Gestion des données : [!UICONTROL  Gérer les jeux de données ]
- Ingestion des données : [!UICONTROL Afficher les sources]
- Destinations : [!UICONTROL Gérer et activer des destinations de jeu de données]
- Query Service : [!UICONTROL Gérer les requêtes]

Par défaut, un rôle (et les informations d’identification d’API affectées à ce rôle) ne peut accéder à aucune donnée libellée. Sous réserve des politiques de gouvernance des données de l’organisation, un administrateur système peut accorder au rôle l’accès à certaines données libellées jugées appropriées à l’utilisation de la science des données. Il est de la responsabilité des clients d’Experience Platform de gérer les politiques et l’accès aux libellés de manière appropriée afin de se conformer aux réglementations et aux politiques organisationnelles pertinentes.

### Stockez les informations d’identification dans un fichier de configuration distinct. {#store-credentials}

Pour garantir la sécurité de vos informations d’identification, il est recommandé d’éviter d’écrire des informations d’identification directement dans votre code. Conservez plutôt les informations d’identification dans un fichier de configuration distinct et lisez les valeurs nécessaires pour vous connecter à Experience Platform et à Data Distiller.

Par exemple, vous pouvez créer un fichier appelé `config.ini` et inclure les informations suivantes (ainsi que d’autres informations, telles que les identifiants de jeu de données, qui seraient utiles pour enregistrer entre les sessions) :

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

Dans votre notebook, vous pouvez ensuite lire les informations d’identification en mémoire à l’aide du package `configParser` de la bibliothèque de [!DNL Python] standard :

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)
```

Vous pouvez ensuite référencer des valeurs d’identification dans votre code comme suit :

```python
org_id = config.get('Credential', 'ims_org_id')
```

## Installer la bibliothèque AEP Python {#install-python-library}

[aepp](https://github.com/adobe/aepp/tree/main) est une bibliothèque de [!DNL Python] open source gérée par Adobe qui fournit des fonctions permettant de se connecter à Data Distiller et d’envoyer des requêtes, comme pour envoyer des requêtes à d’autres services Experience Platform. La bibliothèque `aepp` s’appuie à son tour sur le package d’adaptateur de base de données PostgreSQL `psycopg2` pour les requêtes interactives de Data Distiller. Il est possible de se connecter à Data Distiller et d’interroger des jeux de données Experience Platform avec `psycopg2` seul, mais `aepp` offre davantage de commodité et de fonctionnalités supplémentaires pour adresser des requêtes à tous les services d’API Experience Platform.

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

Une fois `aepp` a configuré vos informations d’identification, vous pouvez utiliser le code suivant pour établir une connexion à Data Distiller et démarrer une session interactive comme suit :

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

Vous pouvez ensuite interroger les jeux de données dans votre sandbox Experience Platform. Compte tenu de l’identifiant d’un jeu de données sur lequel vous souhaitez effectuer une requête, vous pouvez récupérer le nom de la table correspondante à partir du service de catalogue et exécuter des requêtes sur la table :

```python
table_name = 'ecommerce_events'
simple_query = f'''SELECT * FROM {table_name} LIMIT 5'''
dd_cursor.query(simple_query)
```

### Connexion à un seul jeu de données pour des performances de requête plus rapides {#connect-to-single-dataset}

Par défaut, la connexion au Distiller de données se connecte à tous les jeux de données de votre sandbox. Pour des requêtes plus rapides et une utilisation réduite des ressources, vous pouvez plutôt vous connecter à un jeu de données spécifique ciblé. Pour ce faire, modifiez la `dbname` dans l’objet de connexion de Distiller de données en `{sandbox}:{table_name}` :

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## Étapes suivantes

En lisant ce document, vous avez appris à vous connecter à Data Distiller à partir d’un notebook [!DNL Python] dans votre environnement de machine learning. L’étape suivante de la création de pipelines de fonctionnalités à partir d’Experience Platform pour alimenter des modèles personnalisés dans votre environnement de machine learning consiste à [explorer et analyser vos jeux de données](./exploratory-analysis.md).
