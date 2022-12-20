---
title: Gestion des données de plateforme à l’aide de Python et SQLAlchemy
description: Découvrez comment utiliser SQLAlchemy pour gérer vos données Platform à l’aide de Python au lieu de SQL.
source-git-commit: 6b7de4236982181eaac2aa37d525604cba31198e
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Gestion des données Platform à l’aide de [!DNL Python] et [!DNL SQLAlchemy]

Découvrez comment utiliser SQLAlchemy pour une plus grande flexibilité dans la gestion de vos données Adobe Experience Platform. Pour ceux qui ne sont pas aussi familiers avec SQL, SQLAlchemy peut améliorer considérablement le temps de développement lors de l’utilisation de bases de données relationnelles. Ce document fournit des instructions et des exemples de connexion. [!DNL SQLAlchemy] à Query Service et commencez à utiliser Python pour interagir avec vos bases de données.

[!DNL SQLAlchemy] est un mappeur relationnel d’objet (ORM) et un [!DNL Python] Bibliothèque de code qui peut transférer des données stockées dans une base de données SQL vers [!DNL Python] objets. Vous pouvez ensuite effectuer des opérations CRUD sur les données contenues dans le lac de données Platform à l’aide de [!DNL Python] code. Cela supprime la nécessité de gérer les données à l’aide de PSQL uniquement.

## Prise en main

Pour acquérir les informations d’identification nécessaires à la connexion [!DNL SQLAlchemy] pour Experience Platform, vous devez avoir accès à l’espace de travail Requêtes dans l’interface utilisateur de Platform. Contactez l’administrateur de votre organisation si vous n’avez pas actuellement accès à l’espace de travail Requêtes .

## [!DNL Query Service] informations {#credentials}

Pour trouver vos informations d’identification, connectez-vous à l’interface utilisateur de Platform et sélectionnez **[!UICONTROL Requêtes]** à partir du volet de navigation de gauche, suivi de **[!UICONTROL Informations d’identification]**. Pour obtenir des instructions complètes sur la manière de trouver vos informations de connexion, veuillez lire le [guide des informations d’identification](../ui/credentials.md).

![L’onglet Informations d’identification avec les informations d’identification arrivant à expiration pour Query Service est mis en surbrillance.](../images/use-cases/credentials.png)

Bien que le port 80 soit le port recommandé pour une connexion à Query Service, vous pouvez également utiliser le port 5432.

>[!IMPORTANT]
>
>Si vous utilisez des informations d’identification arrivant à expiration (comme illustré dans l’image ci-dessus) pour vous connecter à Query Service, la durée de session de votre connexion expire après la période définie dans les paramètres de votre organisation. Par défaut, cette période est de 24 heures. Consultez la documentation pour savoir comment [connexion d’un client avec des informations d’identification non arrivant à expiration](../ui/credentials.md#non-expiring-credentials)ou comment [modifier la durée de vie de la session pour vos informations d’identification arrivant à expiration ;](../ui/credentials.md#expiring-credentials).

Une fois que vous avez accès à vos informations d’identification QS, ouvrez votre [!DNL Python] éditeur de choix.

### Stocker les informations d’identification dans [!DNL Python] {#store-credentials}

Dans votre [!DNL Python] éditeur, importez `urllib.parse.quote` et enregistrez chaque variable d’identification en tant que paramètre. Le `urllib.parse` fournit une interface standard pour ventiler les chaînes URL en composants. La fonction de guillemet remplace les caractères spéciaux dans la chaîne de l’URL pour que les données puissent être utilisées en toute sécurité comme composants d’URL. Vous trouverez ci-dessous un exemple du code requis :

>[!TIP]
>
>Utilisation [!DNL Python]Guillemets triple pour saisir votre chaîne de mot de passe multi-lignes.

```python
from urllib.parse import quote

host = "<YOUR_HOST>"

port = "<YOUR_PORT>"

dbname = "<YOUR_DATABASE>"

user = "<YOUR_USERNAME>"

password = quote('''
<YOUR_PASSWORD>
''')
```

>[!NOTE]
>
>Mot de passe que vous fournissez pour vous connecter [!DNL SQLAlchemy] pour Experience Platform expirera si vous utilisez des informations d’identification arrivant à expiration. Voir [section informations d’identification](#credentials) pour plus d’informations.

### Création d’une instance de moteur [#create-engine]

Une fois les variables créées, importez la variable `create_engine` et créez une chaîne pour compiler et formater vos informations d’identification Query Service dans SQLAlchemy. Le `create_engine` est ensuite utilisée pour construire une instance de moteur.

>[!NOTE]
>
>`create_engine`renvoie une instance d’un moteur. Toutefois, elle n’ouvre pas la connexion à Query Service tant qu’une requête ne nécessite pas de connexion.

SSL doit être activé lors de l’accès à Platform à l’aide de clients tiers. Dans le cadre de votre moteur, utilisez la variable `connect_args` pour saisir des arguments de mot-clé supplémentaires. Il est recommandé de définir le mode SSL sur `require`. Voir [Documentation sur les modes SSL](../clients/ssl-modes.md) pour plus d’informations sur les valeurs acceptées.

L’exemple ci-dessous illustre le [!DNL Python] code nécessaire pour initialiser un moteur et une chaîne de connexion.

```python
from sqlalchemy import create_engine

db_string = "postgresql://{user}:{password}@{host}:{port}/{dbname}".format(
    user=user,
    password=password,
    host=host,
    port = port,
    dbname = dbname
)

engine = create_engine(db_string, connect_args={'sslmode':'require'})
```

>[!NOTE]
>
>Mot de passe que vous fournissez pour vous connecter [!DNL SQLAlchemy] pour Experience Platform expirera si vous utilisez des informations d’identification arrivant à expiration. Voir [section informations d’identification](#credentials) pour plus d’informations.

Vous êtes maintenant prêt à interroger les données de Platform à l’aide de [!DNL Python]. L’exemple ci-dessous renvoie un tableau de noms de table Query Service.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
