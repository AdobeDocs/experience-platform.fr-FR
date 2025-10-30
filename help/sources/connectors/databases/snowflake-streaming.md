---
title: Présentation Du Connecteur Source De Diffusion En Continu Snowflake
description: Découvrez comment créer une connexion source et un flux de données pour ingérer les données de diffusion en continu de votre instance Snowflake vers Adobe Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 6%

---

# [!DNL Snowflake] source de diffusion en continu

>[!IMPORTANT]
>
>* La source de diffusion en continu [!DNL Snowflake] est disponible dans l’API pour les utilisateurs qui ont acheté Real-Time CDP Ultimate.
>
>* Vous pouvez désormais utiliser la source de diffusion en continu [!DNL Snowflake] lors de l’exécution de Adobe Experience Platform sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge la diffusion en continu de données à partir d’une base de données [!DNL Snowflake].

## Présentation de la source de diffusion en continu [!DNL Snowflake]

La source de diffusion en continu [!DNL Snowflake] fonctionne en chargeant les données en exécutant régulièrement une requête SQL et en créant un enregistrement de sortie pour chaque ligne du jeu résultant.

En utilisant [!DNL Kafka Connect], la source de diffusion en continu [!DNL Snowflake] suit le dernier enregistrement qu’elle reçoit de chaque table, afin qu’elle puisse commencer à l’emplacement approprié pour l’itération suivante. La source utilise cette fonctionnalité pour filtrer les données et obtenir uniquement les lignes mises à jour d’un tableau à chaque itération.

## Conditions préalables

La section suivante décrit les étapes préalables à suivre avant de pouvoir diffuser des données de votre base de données [!DNL Snowflake] vers Experience Platform :

### Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform. Placer sur la liste autorisée Pour plus d’informations, consultez le guide sur la [connexion des adresses IP à Experience Platform](../../ip-address-allow-list.md).

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Amazon Redshift] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] puissiez vous connecter à [!DNL Snowflake], vous devez fournir les propriétés de connexion suivantes :

>[!BEGINTABS]

>[!TAB Authentification de base]

| Informations d’identification | Description |
| --- | --- |
| `account` | L’identifiant complet du compte (nom du compte ou localisateur du compte) de votre compte [!DNL Snowflake] suivi du suffixe `snowflakecomputing.com`. L’identifiant de compte peut avoir différents formats : <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com (par exemple `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.snowflakecomputing.com (par exemple `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD}.snowflakecomputing.com (par exemple `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> Pour plus d’informations, consultez le [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | L’entrepôt de [!DNL Snowflake] gère le processus d’exécution de la requête pour l’application. Chaque entrepôt de [!DNL Snowflake] est indépendant les uns des autres et doit être accessible individuellement lors de l’importation de données dans Experience Platform. |
| `database` | La base de données [!DNL Snowflake] contient les données que vous souhaitez importer dans Experience Platform. |
| `username` | Nom d’utilisateur du compte [!DNL Snowflake]. |
| `password` | Mot de passe du compte utilisateur [!DNL Snowflake]. |
| `role` | (Facultatif) Rôle personnalisé défini qui peut être attribué à un utilisateur, pour une connexion donnée. Si elle n’est pas fournie, cette valeur est `public` par défaut. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Snowflake] est `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

>[!TAB Authentification par paire de clés]

Pour utiliser l’authentification par paire de clés, vous devez générer une paire de clés RSA 2 048 bits, puis fournir les valeurs suivantes lors de la création d’un compte pour votre source [!DNL Snowflake].

| Informations d’identification | Description |
| --- | --- |
| `account` | Un nom de compte identifie de manière unique un compte de votre organisation. Dans ce cas, vous devez identifier de manière unique un compte dans différentes organisations [!DNL Snowflake]. Pour ce faire, vous devez ajouter le nom de votre organisation au nom du compte. Par exemple : `orgname-account_name`. Lisez le guide sur la [récupération de l’identifiant  [!DNL Snowflake]  compte](./snowflake.md#retrieve-your-account-identifier) pour obtenir des conseils supplémentaires. Pour plus d’informations, consultez la [[!DNL Snowflake] documentation](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Nom d’utilisateur de votre compte [!DNL Snowflake]. |
| `privateKey` | Clé privée [!DNL Base64-]encodée) de votre compte [!DNL Snowflake]. Vous pouvez générer des clés privées chiffrées ou non chiffrées. Si vous utilisez une clé privée chiffrée, vous devez également fournir une phrase secrète de clé privée lors de l’authentification auprès d’Experience Platform. Pour plus d’informations, consultez le guide sur la [récupération  [!DNL Snowflake]  votre clé privée](./snowflake.md). |
| `passphrase` | La phrase secrète est une couche de sécurité supplémentaire que vous devez utiliser lors de l’authentification avec une clé privée chiffrée. Vous n’êtes pas tenu de fournir la phrase secrète si vous utilisez une clé privée non chiffrée. |
| `database` | Base de données [!DNL Snowflake] contenant les données à ingérer dans Experience Platform. |
| `warehouse` | L’entrepôt de [!DNL Snowflake] gère le processus d’exécution de la requête pour l’application. Chaque entrepôt de [!DNL Snowflake] est indépendant les uns des autres et doit être accessible individuellement lors de l’importation de données dans Experience Platform. |

Pour plus d’informations sur ces valeurs, consultez le [[!DNL Snowflake] guide d’authentification par paire de clés](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Récupérer l’identifiant de votre compte {#retrieve-your-account-identifier}

Pour authentifier votre instance [!DNL Snowflake] avec Experience Platform, vous devez obtenir votre identifiant de compte depuis le tableau de bord de l’interface utilisateur [!DNL Snowflake].

Pour trouver l’identifiant de votre compte, procédez comme suit :

* Accédez à votre compte dans le tableau de bord de l’interface utilisateur de l’application [[!DNL Snowflake] &#x200B;](https://app.snowflake.com/).
* Dans le volet de navigation de gauche, sélectionnez **[!DNL Accounts]**, puis **[!DNL Active Accounts]** dans l’en-tête.
* Sélectionnez ensuite l’icône d’information, puis sélectionnez et copiez le nom de domaine de l’URL active.

### Récupérer votre clé privée {#retrieve-your-private-key}

Si vous prévoyez d’utiliser l’authentification par paire de clés pour votre connexion [!DNL Snowflake], vous devez générer une clé privée avant de vous connecter à Experience Platform.

>[!BEGINTABS]

>[!TAB Créer une clé privée chiffrée]

Pour générer votre clé privée [!DNL Snowflake] chiffrée, exécutez la commande suivante sur votre terminal :

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

En cas de réussite, vous devriez recevoir votre clé privée au format PEM.

```shell
|-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
|-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB Créer une clé privée non chiffrée]

Pour générer votre clé privée [!DNL Snowflake] non chiffrée, exécutez la commande suivante sur votre terminal :

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

En cas de réussite, vous devriez recevoir votre clé privée au format PEM.

```shell
|-----BEGIN PRIVATE KEY-----
MIIE6T...
|-----END PRIVATE KEY-----
```

>[!ENDTABS]

Après avoir généré votre clé privée, codez-la directement en [!DNL Base64] sans apporter de modifications à son format ou à son contenu. Avant l’encodage, assurez-vous qu’il n’y a pas d’espaces ou de lignes vides supplémentaires (y compris les nouvelles lignes de fin) à la fin de la clé privée.

### Vérifier les configurations

Avant de pouvoir créer une connexion source pour vos données [!DNL Snowflake], vous devez également vous assurer que les configurations suivantes sont respectées :

* L’entrepôt par défaut affecté à un utilisateur donné doit être le même que celui que vous saisissez lors de l’authentification auprès d’Experience Platform.
* Le rôle par défaut attribué à un utilisateur donné doit avoir accès à la même base de données que celle que vous avez saisie lors de l’authentification auprès d’Experience Platform.

Pour vérifier votre rôle et votre entrepôt :

* Sélectionnez **[!DNL Admin]** dans le volet de navigation de gauche, puis sélectionnez **[!DNL Users & Roles]**.
* Sélectionnez l’utilisateur approprié, puis sélectionnez les points de suspension (`...`) dans le coin supérieur droit.
* Dans la fenêtre de [!DNL Edit user] qui s’affiche, accédez à [!DNL Default Role] pour afficher le rôle associé à l’utilisateur donné.
* Dans la même fenêtre, accédez à [!DNL Default Warehouse] pour afficher l&#39;entrepôt associé à l&#39;utilisateur donné.

Une fois le codage réussi, vous pouvez utiliser cette clé privée codée en [!DNL Base64] sur Experience Platform pour authentifier votre compte [!DNL Snowflake].

### Configurer les paramètres de rôle {#configure-role-settings}

Vous devez configurer des privilèges sur un rôle, même si le rôle public par défaut est affecté, pour permettre à votre connexion source d’accéder à la base de données, au schéma et à la table [!DNL Snowflake] appropriés. Les différents privilèges pour différentes entités [!DNL Snowflake] sont les suivants :

| entité [!DNL Snowflake] | Exiger un privilège de rôle |
| --- | --- |
| Entrepôt de données | FONCTIONNEMENT, UTILISATION |
| Base de données | UTILISATION |
| Schéma | UTILISATION |
| Tableau | SÉLECTIONNER |

>[!NOTE]
>
>La reprise automatique et la suspension automatique doivent être activées dans la configuration des paramètres avancés de votre entrepôt.

Pour plus d’informations sur la gestion des rôles et des privilèges, consultez la [[!DNL Snowflake] référence de l’API](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Convertir les champs d’heure en date au format Unix

Le [!DNL Snowflake Streaming] analyse et écrit `DATE` champs comme le nombre de jours depuis l’époque Unix (1970-01-01). Par exemple, une valeur `DATE` de 0 signifie le 1er janvier 1970, tandis qu’une valeur de 1 signifie le 2 janvier 1970. Par conséquent, lors de la préparation du fichier pour créer des mappages dans la source de [!DNL Snowflake Streaming], assurez-vous que la colonne `DATE` est représentée sous la forme d’un entier.

Vous pouvez utiliser les [fonctions de données et d’heure de la préparation des données](../../../data-prep/functions.md#date-and-time-functions) pour convertir l’heure Unix en champs de date pouvant être ingérés dans Experience Platform. Par exemple :

```shell
dformat({DATE_COLUMN} * 86400000, "yyyy-MM-dd")
```

Dans cette fonction :

* `{DATE_COLUMN}` est la colonne de date contenant l’entier du jour epoch.
* La multiplication par 86400000 convertit les jours de l’époque en millisecondes.
* « aaaa-MM-jj » indique le format de date souhaité.

Cette conversion garantit que la date est correctement représentée dans votre jeu de données.


## Restrictions et questions fréquentes {#limitations-and-frequently-asked-questions}

* Le débit de données de la source [!DNL Snowflake] est de 2 000 enregistrements par seconde.
* Le prix peut varier en fonction de la durée d&#39;activité d&#39;un entrepôt et de la taille de l&#39;entrepôt. Pour l’intégration de la source [!DNL Snowflake], la plus petite taille, x-petit entrepôt est suffisante. Il est suggéré d&#39;activer la suspension automatique afin que l&#39;entrepôt puisse être suspendu seul lorsqu&#39;il n&#39;est pas utilisé.
* La source [!DNL Snowflake] interroge la base de données pour obtenir de nouvelles données toutes les 10 secondes.
* Options de configuration :
   * Vous pouvez activer un indicateur booléen `backfill` pour votre source de [!DNL Snowflake] lors de la création d’une connexion source.
      * Si le renvoi est défini sur true, la valeur de timestamp.initial est définie sur 0. Cela signifie que les données avec une colonne d’horodatage supérieure à 0 heure d’époque sont récupérées.
      * Si le renvoi est défini sur false, la valeur de timestamp.initial est définie sur -1. Cela signifie que les données avec une colonne d’horodatage supérieure à l’heure actuelle (heure à laquelle la source commence l’ingestion) sont récupérées.
   * La colonne d’horodatage doit être au format de type : `TIMESTAMP_LTZ` ou `TIMESTAMP_NTZ`. Si la colonne timestamp est définie sur `TIMESTAMP_NTZ`, le fuseau horaire correspondant dans lequel les valeurs sont stockées doit être transmis via le paramètre `timezoneValue`. Si elle n’est pas fournie, la valeur est définie par défaut sur UTC.
      * `TIMESTAMP_TZ` ne peut pas être utilisé comme colonne d’horodatage ou dans un mappage.

## Étapes suivantes

>[!NOTE]
>
>Après avoir créé ou mis à jour un flux de données en continu, une brève pause de 5 minutes dans l’ingestion des données est nécessaire pour éviter toute instance potentielle de perte de données ou d’abandon de données.

Le tutoriel suivant décrit les étapes à suivre pour connecter votre source de diffusion en continu [!DNL Snowflake] à Experience Platform à l’aide de l’API :

* [Diffuser des données d’une base  [!DNL Snowflake]  données vers Experience Platform à l’aide de l’API Flow Service](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Diffusez des données d’une base  [!DNL Snowflake]  données vers Experience Platform à l’aide de l’espace de travail des sources dans l’interface utilisateur d’Experience Platform](../../tutorials/ui/create/databases/snowflake-streaming.md)
