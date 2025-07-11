---
title: Présentation Du Connecteur Source De Diffusion En Continu Snowflake
description: Découvrez comment créer une connexion source et un flux de données pour ingérer les données de diffusion en continu de votre instance Snowflake vers Adobe Experience Platform
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-09-24T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 11%

---

# [!DNL Snowflake] source de diffusion en continu

>[!IMPORTANT]
>
>* La source de diffusion en continu [!DNL Snowflake] est disponible dans l’API pour les utilisateurs qui ont acheté Real-Time CDP Ultimate.
>
>* Vous pouvez désormais utiliser la source de diffusion en continu [!DNL Snowflake] lors de l’exécution de Adobe Experience Platform sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).


Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge la diffusion en continu de données à partir d’une base de données [!DNL Snowflake].

## Présentation de la source de diffusion en continu [!DNL Snowflake]

La source de diffusion en continu [!DNL Snowflake] fonctionne en chargeant les données en exécutant régulièrement une requête SQL et en créant un enregistrement de sortie pour chaque ligne du jeu résultant.

En utilisant [!DNL Kafka Connect], la source de diffusion en continu [!DNL Snowflake] suit le dernier enregistrement qu’elle reçoit de chaque table, afin qu’elle puisse commencer à l’emplacement approprié pour l’itération suivante. La source utilise cette fonctionnalité pour filtrer les données et obtenir uniquement les lignes mises à jour d’un tableau à chaque itération.

## Conditions préalables

La section suivante décrit les étapes préalables à suivre avant de pouvoir diffuser des données de votre base de données [!DNL Snowflake] vers Experience Platform :

### Mise à jour de la liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md#ip-address-allow-list-for-streaming-sources) pour plus d’informations.

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Amazon Redshift] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] puissiez vous connecter à [!DNL Snowflake], vous devez fournir les propriétés de connexion suivantes :

| Informations d’identification | Description |
| --- | --- |
| `account` | L’identifiant complet du compte (nom du compte ou localisateur du compte) de votre compte [!DNL Snowflake] suivi du suffixe `snowflakecomputing.com`. L’identifiant de compte peut avoir différents formats : <ul><li>{ORG_NAME}-{ACCOUNT_NAME}.snowflakecomputing.com (par exemple `acme-abc12345.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.snowflakecomputing.com (par exemple `acme12345.ap-southeast-1.snowflakecomputing.com`)</li><li>{ACCOUNT_LOCATOR}.{CLOUD_REGION_ID}.{CLOUD}.snowflakecomputing.com (par exemple `acme12345.east-us-2.azure.snowflakecomputing.com`)</li></ul> Pour plus d’informations, consultez le [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | L’entrepôt de [!DNL Snowflake] gère le processus d’exécution de la requête pour l’application. Chaque entrepôt de [!DNL Snowflake] est indépendant les uns des autres et doit être accessible individuellement lors de l’importation de données dans Experience Platform. |
| `database` | La base de données [!DNL Snowflake] contient les données que vous souhaitez importer dans Experience Platform. |
| `username` | Nom d’utilisateur du compte [!DNL Snowflake]. |
| `password` | Mot de passe du compte utilisateur [!DNL Snowflake]. |
| `role` | (Facultatif) Rôle personnalisé défini qui peut être attribué à un utilisateur, pour une connexion donnée. Si elle n’est pas fournie, cette valeur est `public` par défaut. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Snowflake] est `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

{style="table-layout:auto"}

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
