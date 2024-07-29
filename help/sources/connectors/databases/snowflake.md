---
title: Présentation du connecteur Source Snowflake
description: Découvrez comment connecter Snowflake à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 8d6baef1549498e137d336ac2c8a42428496dedf
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 21%

---

# Source [!DNL Snowflake]

>[!IMPORTANT]
>
>* La source [!DNL Snowflake] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.
>* Par défaut, la source [!DNL Snowflake] interprète `null` comme une chaîne vide. Contactez votre représentant d’Adobe pour vous assurer que vos valeurs `null` sont correctement écrites en tant que `null` dans Adobe Experience Platform.
>* Pour que l’Experience Platform puisse ingérer des données, les fuseaux horaires de toutes les sources par lots basées sur un tableau doivent être configurés en UTC. Le seul horodatage pris en charge pour la source [!DNL Snowflake] est TIMESTAMP_NTZ avec l’heure UTC.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’une base de données tierce. Platform peut se connecter à différents types de bases de données comme les entrepôts relationnels, NoSQL ou de données. [!DNL Snowflake] est compatible avec les fournisseurs de base de données.

## Conditions préalables {#prerequisites}

Cette section décrit les tâches de configuration que vous devez effectuer avant de pouvoir connecter votre source [!DNL Snowflake] à Experience Platform.

### Récupération de votre identifiant de compte {#retrieve-your-account-identifier}

Vous devez récupérer l’identifiant de votre compte dans le tableau de bord de l’interface utilisateur [!DNL Snowflake], car vous utiliserez l’identifiant de compte pour authentifier votre instance [!DNL Snowflake] sur Experience Platform.

Pour récupérer votre identifiant de compte :

* Accédez à votre compte sur le [[!DNL Snowflake] tableau de bord de l’interface utilisateur de l’application](https://app.snowflake.com/).
* Dans le volet de navigation de gauche, sélectionnez **[!DNL Accounts]**, suivi de **[!DNL Active Accounts]** dans l’en-tête.
* Sélectionnez ensuite l’icône d’information, puis sélectionnez et copiez le nom de domaine de l’URL active.

![Tableau de bord de l’interface utilisateur du Snowflake avec le nom de domaine sélectionné.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Récupération de votre clé privée {#retrieve-your-private-key}

Si vous utilisez l’authentification paire de clés pour votre connexion [!DNL Snowflake], vous devez également générer votre clé privée avant de vous connecter à Experience Platform.

>[!BEGINTABS]

>[!TAB  Créez une clé privée chiffrée ]

Pour générer votre clé privée [!DNL Snowflake] chiffrée, exécutez la commande suivante sur votre terminal :

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

En cas de réussite, vous devriez recevoir votre clé privée au format PEM.

```shell
-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB  Créez une clé privée non chiffrée ]

Pour générer votre clé privée [!DNL Snowflake] non chiffrée, exécutez la commande suivante sur votre terminal :

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

En cas de réussite, vous devriez recevoir votre clé privée au format PEM.

```shell
-----BEGIN PRIVATE KEY-----
MIIE6T...
-----END PRIVATE KEY-----
```

>[!ENDTABS]

Ensuite, prenez votre clé privée et codez-la dans [!DNL Base64]. Assurez-vous de ne pas effectuer de transformations ou de conversions de format sur votre clé privée [!DNL Snowflake]. De plus, vous devez vous assurer qu’il n’existe aucun caractère de saut de page à la fin de votre clé privée, avant de le coder dans [!DNL Base64].

### Vérification des configurations

Avant de pouvoir créer une connexion source pour vos données [!DNL Snowflake], vous devez également vous assurer que les configurations suivantes sont remplies :

* L’entrepôt par défaut attribué à un utilisateur donné doit être le même que celui saisi lors de l’authentification auprès d’un Experience Platform.
* Le rôle par défaut attribué à un utilisateur donné doit avoir accès à la même base de données que celle saisie lors de l’authentification auprès d’un Experience Platform.

Pour vérifier votre rôle et votre entrepôt :

* Sélectionnez **[!DNL Admin]** dans le volet de navigation de gauche, puis **[!DNL Users & Roles]**.
* Sélectionnez l’utilisateur approprié, puis sélectionnez les ellipses (`...`) dans le coin supérieur droit.
* Dans la fenêtre [!DNL Edit user] qui s’affiche, accédez à [!DNL Default Role] pour afficher le rôle associé à l’utilisateur donné.
* Dans la même fenêtre, accédez à [!DNL Default Warehouse] pour afficher l’entrepôt associé à l’utilisateur donné.

![ Interface utilisateur du Snowflake dans laquelle vous pouvez vérifier votre rôle et votre entrepôt.](../../images/tutorials/create/snowflake/snowflake-configs.png)

Une fois le codage effectué, vous pouvez ensuite utiliser cette clé privée encodée [!DNL Base64] sur Experience Platform pour authentifier votre compte [!DNL Snowflake].

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

La documentation ci-dessous fournit des informations sur la connexion d’[!DNL Snowflake] à Platform à l’aide d’API ou de l’interface utilisateur :

## Connecter [!DNL Snowflake] à Platform à l’aide d’API

* [Création d’une connexion de base de Snowflake à l’aide de l’API Flow Service](../../tutorials/api/create/databases/snowflake.md)
* [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
* [Création d’un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

## Connecter [!DNL Snowflake] à Platform à l’aide de l’interface utilisateur

* [Création d’une connexion source de Snowflake dans l’interface utilisateur](../../tutorials/ui/create/databases/snowflake.md)
* [Création d’un flux de données pour une connexion source de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)
