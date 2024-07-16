---
title: Gestion des données de plateforme à l’aide de Python et SQLAlchemy
description: Découvrez comment utiliser SQLAlchemy pour gérer vos données Platform à l’aide de Python au lieu de SQL.
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: 8644b78c947fd015f6a169c9440b8d1df71e5e17
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 7%

---

# Gérer les données de Platform à l’aide de [!DNL Python] et [!DNL SQLAlchemy]

Découvrez comment utiliser SQLAlchemy pour une plus grande flexibilité dans la gestion de vos données Adobe Experience Platform. Pour ceux qui ne sont pas aussi familiers avec SQL, SQLAlchemy peut améliorer considérablement le temps de développement lors de l’utilisation de bases de données relationnelles. Ce document fournit des instructions et des exemples pour connecter [!DNL SQLAlchemy] à Query Service et commencer à utiliser Python pour interagir avec vos bases de données.

[!DNL SQLAlchemy] est une bibliothèque de code ORM (Object Relational Mapper) et [!DNL Python] qui peut transférer des données stockées dans une base de données SQL dans des objets [!DNL Python]. Vous pouvez ensuite effectuer des opérations CRUD sur les données contenues dans le lac de données Platform à l’aide du code [!DNL Python]. Cela supprime la nécessité de gérer les données à l’aide de PSQL uniquement.

## Commencer

Pour acquérir les informations d’identification nécessaires à la connexion de [!DNL SQLAlchemy] à Experience Platform, vous devez avoir accès à l’espace de travail Requêtes dans l’interface utilisateur de Platform. Contactez l’administrateur de votre organisation si vous n’avez pas actuellement accès à l’espace de travail Requêtes .

## [!DNL Query Service] credentials {#credentials}

Pour trouver vos informations d’identification, connectez-vous à l’interface utilisateur de Platform et sélectionnez **[!UICONTROL Requêtes]** à partir du volet de navigation de gauche, puis **[!UICONTROL Informations d’identification]**. Pour obtenir des instructions complètes sur la manière de trouver vos informations de connexion, consultez le [guide des informations d’identification](../ui/credentials.md).

![L’onglet Informations d’identification avec les informations d’identification arrivant à expiration pour Query Service est surligné.](../images/use-cases/credentials.png)

Bien que le port 80 soit le port recommandé pour une connexion à Query Service, vous pouvez également utiliser le port 5432.

>[!IMPORTANT]
>
>Si vous utilisez des informations d’identification arrivant à expiration (comme illustré dans l’image ci-dessus) pour vous connecter à Query Service, la durée de session de votre connexion expire après la période définie dans les paramètres de votre organisation. Par défaut, cette période est de 24 heures. Consultez la documentation pour savoir comment [connecter un client avec des informations d’identification non arrivant à expiration](../ui/credentials.md#non-expiring-credentials) ou [modifier la durée de session de vos informations d’identification arrivant à expiration](../ui/credentials.md#expiring-credentials).

Une fois que vous avez accès à vos informations d’identification QS, ouvrez votre éditeur [!DNL Python] de votre choix.

### Stocker les informations d’identification dans [!DNL Python] {#store-credentials}

Dans votre éditeur [!DNL Python], importez la bibliothèque `urllib.parse.quote` et enregistrez chaque variable d’identification comme paramètre. Le module `urllib.parse` fournit une interface standard pour ventiler les chaînes URL en composants. La fonction de guillemet remplace les caractères spéciaux dans la chaîne de l’URL pour que les données puissent être utilisées en toute sécurité comme composants d’URL. Vous trouverez ci-dessous un exemple du code requis :

>[!TIP]
>
>Utilisez les guillemets triple de [!DNL Python] pour saisir la chaîne de mot de passe multi-lignes.

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
>Le mot de passe que vous fournissez pour vous connecter [!DNL SQLAlchemy] à l’Experience Platform expirera si vous utilisez des informations d’identification arrivant à expiration. Pour plus d’informations, consultez la [section des informations d’identification](#credentials) .

### Créez une instance de moteur [#create-engine]

Une fois les variables créées, importez la fonction `create_engine` et créez une chaîne pour compiler et formater vos informations d’identification Query Service dans SQLAlchemy. La fonction `create_engine` est ensuite utilisée pour construire une instance de moteur.

>[!NOTE]
>
>`create_engine`renvoie une instance d’un moteur. Toutefois, elle n’ouvre pas la connexion à Query Service tant qu’une requête ne nécessite pas de connexion.

SSL doit être activé lors de l’accès à Platform à l’aide de clients tiers. Dans le cadre de votre moteur, utilisez `connect_args` pour saisir des arguments de mots-clés supplémentaires. Il est recommandé de définir le mode SSL sur `require`. Pour plus d’informations sur les valeurs acceptées, consultez la [documentation sur les modes SSL](../clients/ssl-modes.md).

L’exemple ci-dessous affiche le code [!DNL Python] nécessaire à l’initialisation d’un moteur et d’une chaîne de connexion.

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
>Le mot de passe que vous fournissez pour vous connecter [!DNL SQLAlchemy] à l’Experience Platform expirera si vous utilisez des informations d’identification arrivant à expiration. Pour plus d’informations, consultez la [section des informations d’identification](#credentials) .

Vous êtes maintenant prêt à interroger les données de Platform à l’aide de [!DNL Python]. L’exemple ci-dessous renvoie un tableau de noms de table Query Service.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
