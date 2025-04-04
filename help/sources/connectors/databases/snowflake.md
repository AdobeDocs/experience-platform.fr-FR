---
title: Présentation du connecteur Source de Snowflake
description: Découvrez comment connecter Snowflake à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 13%

---

# Source [!DNL Snowflake]

>[!IMPORTANT]
>
>* La source [!DNL Snowflake] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.
>* Par défaut, la source de [!DNL Snowflake] interprète `null` comme une chaîne vide. Contactez votre représentant Adobe pour vous assurer que vos valeurs `null` sont correctement écrites comme `null` dans Adobe Experience Platform.
>* Pour qu’Experience Platform ingère des données, les fuseaux horaires de toutes les sources de lots basées sur un tableau doivent être configurés au format UTC. Le seul horodatage pris en charge pour la source [!DNL Snowflake] est TIMESTAMP_NTZ avec l’heure UTC.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’une base de données tierce. Experience Platform peut se connecter à différents types de bases de données tels que des entrepôts relationnels, NoSQL ou de données. La prise en charge des fournisseurs de base de données inclut [!DNL Snowflake].

## Conditions préalables {#prerequisites}

Cette section décrit les tâches de configuration que vous devez effectuer avant de connecter votre source [!DNL Snowflake] à Experience Platform.

### Récupérer l’identifiant de votre compte {#retrieve-your-account-identifier}

Vous devez récupérer l’identifiant de votre compte à partir du tableau de bord de l’interface utilisateur [!DNL Snowflake], car vous utiliserez l’identifiant du compte pour authentifier votre instance [!DNL Snowflake] sur Experience Platform.

Pour récupérer l’identifiant de votre compte :

* Accédez à votre compte dans le tableau de bord de l’interface utilisateur de l’application [[!DNL Snowflake] ](https://app.snowflake.com/).
* Dans le volet de navigation de gauche, sélectionnez **[!DNL Accounts]**, puis **[!DNL Active Accounts]** dans l’en-tête.
* Sélectionnez ensuite l’icône d’information, puis sélectionnez et copiez le nom de domaine de l’URL active.

![Tableau de bord de l’interface utilisateur de Snowflake avec le nom de domaine sélectionné.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Récupérer votre clé privée {#retrieve-your-private-key}

Si vous utilisez l’authentification par paire de clés pour votre connexion [!DNL Snowflake], vous devez également générer votre clé privée avant de vous connecter à Experience Platform.

>[!BEGINTABS]

>[!TAB Créer une clé privée chiffrée]

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

>[!TAB Créer une clé privée non chiffrée]

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

Ensuite, prenez votre clé privée et codez-la en [!DNL Base64]. Assurez-vous de ne pas effectuer de transformations ou de conversions de format sur votre clé privée [!DNL Snowflake]. En outre, vous devez vous assurer qu’il n’y a aucun caractère de nouvelle ligne à la fin de votre clé privée, avant de la coder en [!DNL Base64].

### Vérifier les configurations

Avant de pouvoir créer une connexion source pour vos données [!DNL Snowflake], vous devez également vous assurer que les configurations suivantes sont respectées :

* L’entrepôt par défaut affecté à un utilisateur donné doit être le même que celui que vous saisissez lors de l’authentification auprès d’Experience Platform.
* Le rôle par défaut attribué à un utilisateur donné doit avoir accès à la même base de données que celle que vous avez saisie lors de l’authentification auprès d’Experience Platform.

Pour vérifier votre rôle et votre entrepôt :

* Sélectionnez **[!DNL Admin]** dans le volet de navigation de gauche, puis sélectionnez **[!DNL Users & Roles]**.
* Sélectionnez l’utilisateur approprié, puis sélectionnez les points de suspension (`...`) dans le coin supérieur droit.
* Dans la fenêtre de [!DNL Edit user] qui s’affiche, accédez à [!DNL Default Role] pour afficher le rôle associé à l’utilisateur donné.
* Dans la même fenêtre, accédez à [!DNL Default Warehouse] pour afficher l&#39;entrepôt associé à l&#39;utilisateur donné.

![Interface utilisateur de Snowflake dans laquelle vous pouvez vérifier votre rôle et votre entrepôt de données.](../../images/tutorials/create/snowflake/snowflake-configs.png)

Une fois le codage réussi, vous pouvez utiliser cette clé privée codée en [!DNL Base64] sur Experience Platform pour authentifier votre compte [!DNL Snowflake].

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Snowflake] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

## Connexion de [!DNL Snowflake] à Experience Platform à l’aide d’API

* [Créer une connexion de base Snowflake à l’aide de l’API Flow Service](../../tutorials/api/create/databases/snowflake.md)
* [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
* [Créer un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

## Connexion d’[!DNL Snowflake] à Experience Platform à l’aide de l’interface utilisateur

* [Créer une connexion source Snowflake dans l’interface utilisateur](../../tutorials/ui/create/databases/snowflake.md)
* [Créer un flux de données pour une connexion source de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)
