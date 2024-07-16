---
title: Présentation du connecteur Source de diffusion en continu Snowflake
description: Découvrez comment créer une connexion source et un flux de données pour ingérer des données en continu de votre instance de Snowflake vers Adobe Experience Platform
badgeBeta: label="Version bêta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: c80535cbb5dda55f1cf145f9f40bbcd40c78e63e
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 11%

---

# [!DNL Snowflake] source de diffusion en continu

>[!IMPORTANT]
>
>* La source de diffusion [!DNL Snowflake] est en version bêta. Pour plus d’informations sur l’utilisation de sources étiquetées bêta, consultez la [Présentation des sources](../../home.md#terms-and-conditions).
>* La source de diffusion en continu [!DNL Snowflake] est disponible dans l’API pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge la diffusion en continu de données à partir d’une base de données [!DNL Snowflake].

## Présentation de la source de diffusion en continu [!DNL Snowflake]

La source de diffusion en continu [!DNL Snowflake] fonctionne en chargeant des données en exécutant régulièrement une requête SQL et en créant un enregistrement de sortie pour chaque ligne de l’ensemble obtenu.

En utilisant [!DNL Kafka Connect], la source de diffusion [!DNL Snowflake] effectue le suivi des derniers enregistrements qu’elle reçoit de chaque table, de sorte qu’elle puisse commencer à l’emplacement correct pour l’itération suivante. La source utilise cette fonctionnalité pour filtrer les données et obtenir uniquement les lignes mises à jour d’un tableau à chaque itération.

## Conditions préalables

La section suivante décrit les étapes préalables à suivre pour que vous puissiez diffuser des données de votre base de données [!DNL Snowflake] vers l’Experience Platform :

### Collecter les informations d’identification requises

Pour que [!DNL Flow Service] se connecte à [!DNL Snowflake], vous devez fournir les propriétés de connexion suivantes :

| Informations d’identification | Description |
| --- | --- |
| `account` | Nom complet du compte associé à votre compte [!DNL Snowflake]. Un nom de compte [!DNL Snowflake] entièrement qualifié inclut le nom de votre compte, votre région et votre plateforme cloud. Par exemple : `cj12345.east-us-2.azure`. Pour plus d&#39;informations sur les noms de compte, consultez cet [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | L’entrepôt [!DNL Snowflake] gère le processus d’exécution de requête pour l’application. Chaque entrepôt [!DNL Snowflake] est indépendant l’un de l’autre et doit être accessible individuellement lors de la transmission de données à Platform. |
| `database` | La base de données [!DNL Snowflake] contient les données que vous souhaitez importer dans Platform. |
| `username` | Nom d’utilisateur du compte [!DNL Snowflake]. |
| `password` | Mot de passe du compte utilisateur [!DNL Snowflake]. |
| `role` | (Facultatif) Rôle personnalisé pouvant être fourni à un utilisateur, pour une connexion donnée. Si elle n’est pas fournie, cette valeur est définie par défaut sur `public`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’ID de spécification de connexion pour [!DNL Snowflake] est `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |


### Configuration des paramètres des rôles {#configure-role-settings}

Vous devez configurer des privilèges sur un rôle, même si le rôle public par défaut est attribué, pour permettre à votre connexion source d’accéder à la base de données, au schéma et à la table [!DNL Snowflake] appropriés. Les différents privilèges pour différentes entités [!DNL Snowflake] sont les suivants :

| [!DNL Snowflake] entité | Privilège du rôle Require |
| --- | --- |
| Entrepôt | OPÉRATION, UTILISATION |
| Base de données | UTILISATION |
| Schéma | UTILISATION |
| Tableau | SELECT |

>[!NOTE]
>
>La reprise automatique et la suspension automatique doivent être activées dans la configuration avancée de votre entrepôt.

Pour plus d’informations sur la gestion des rôles et des privilèges, reportez-vous à la [[!DNL Snowflake] référence API](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Limites et questions fréquentes {#limitations-and-frequently-asked-questions}

* Le débit de données de la source [!DNL Snowflake] est de 2 000 enregistrements par seconde.
* Les tarifs peuvent varier en fonction de la durée d’activité d’un entrepôt et de sa taille. Pour l’intégration de la source [!DNL Snowflake], le plus petit entrepôt x-petit est suffisant. Il est conseillé d’activer la suspension automatique afin que l’entrepôt puisse être suspendu seul lorsqu’il n’est pas utilisé.
* La source [!DNL Snowflake] interroge la base de données pour obtenir de nouvelles données toutes les 10 secondes.
* Options de configuration :
   * Vous pouvez activer un indicateur booléen `backfill` pour votre source [!DNL Snowflake] lors de la création d’une connexion source.
      * Si le renvoi est défini sur true, la valeur de timestamp.initial est définie sur 0. Cela signifie que les données dont la colonne d’horodatage est supérieure à 0 heure sont récupérées.
      * Si le renvoi est défini sur false, la valeur de timestamp.initial est définie sur -1. Cela signifie que les données dont la colonne d’horodatage est supérieure à l’heure actuelle (l’heure à laquelle la source commence l’ingestion) sont récupérées.
   * La colonne d’horodatage doit être formatée comme type : `TIMESTAMP_LTZ` ou `TIMESTAMP_NTZ`. Si la colonne d’horodatage est définie sur `TIMESTAMP_NTZ`, le fuseau horaire correspondant dans lequel les valeurs sont stockées doit être transmis via le paramètre `timezoneValue` . Si elle n’est pas fournie, la valeur est définie par défaut sur UTC.
      * `TIMESTAMP_TZ` ne peut pas être utilisé dans une colonne d’horodatage ou dans un mappage.

## Étapes suivantes

Le tutoriel suivant explique comment connecter votre source de diffusion en continu [!DNL Snowflake] à Experience Platform à l’aide de l’API :

* [Diffusion en continu des données d’une base de données  [!DNL Snowflake] vers un Experience Platform à l’aide de l’API Flow Service](../../tutorials/api/create/databases/snowflake-streaming.md)
* [Diffusez des données d’une base de données  [!DNL Snowflake] vers un Experience Platform à l’aide de l’espace de travail sources dans l’interface utilisateur de l’Experience Platform.](../../tutorials/ui/create/databases/snowflake-streaming.md)
