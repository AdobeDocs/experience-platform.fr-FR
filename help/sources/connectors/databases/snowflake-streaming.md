---
title: Présentation du connecteur source de diffusion en continu Snowflake
description: Découvrez comment créer une connexion source et un flux de données pour ingérer des données en continu de votre instance de Snowflake vers Adobe Experience Platform
badgeBeta: label="Version Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2023-05-25T00:00:00Z
exl-id: ed937689-e844-487e-85fb-e3536c851fe5
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 11%

---

# [!DNL Snowflake] source de diffusion

>[!IMPORTANT]
>
>* La variable [!DNL Snowflake] source en continu est en version bêta. Veuillez lire la [Présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.
>* La variable [!DNL Snowflake] La source de diffusion en continu est disponible dans l’API pour les utilisateurs qui ont acheté Real-time Customer Data Platform Ultimate.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge la diffusion en continu de données depuis un [!DNL Snowflake] base de données.

## Présentation de la fonction [!DNL Snowflake] source de diffusion

La variable [!DNL Snowflake] la source de diffusion en continu fonctionne en chargeant des données en exécutant régulièrement une requête SQL et en créant un enregistrement de sortie pour chaque ligne de l’ensemble obtenu.

En utilisant [!DNL Kafka Connect], la variable [!DNL Snowflake] source de diffusion continue effectue le suivi des derniers enregistrements qu’elle reçoit de chaque table, de sorte qu’elle puisse commencer à l’emplacement approprié pour la prochaine itération. La source utilise cette fonctionnalité pour filtrer les données et obtenir uniquement les lignes mises à jour d’un tableau à chaque itération.

## Conditions préalables

La section suivante décrit les étapes préalables requises à suivre pour que vous puissiez diffuser des données à partir de votre [!DNL Snowflake] base de données vers Experience Platform :

### Collecter les informations d’identification requises

Pour [!DNL Flow Service] pour vous connecter à [!DNL Snowflake], vous devez fournir les propriétés de connexion suivantes :

| Informations d’identification | Description |
| --- | --- |
| `account` | Le nom complet du compte associé à votre [!DNL Snowflake] compte . Une personne entièrement qualifiée [!DNL Snowflake] nom du compte inclut le nom de votre compte, votre région et votre plateforme cloud. Par exemple : `cj12345.east-us-2.azure`. Pour plus d&#39;informations sur les noms de compte, reportez-vous à cette section [[!DNL Snowflake document on account identifiers]](<https://docs.snowflake.com/en/user-guide/admin-account-identifier.html>). |
| `warehouse` | La variable [!DNL Snowflake] l’entrepôt gère le processus d’exécution des requêtes de l’application. Chaque [!DNL Snowflake] L’entrepôt est indépendant l’un de l’autre et doit être accessible individuellement lors de l’importation de données vers Platform. |
| `database` | La variable [!DNL Snowflake] La base de données contient les données que vous souhaitez importer dans Platform. |
| `username` | Nom d’utilisateur de la variable [!DNL Snowflake] compte . |
| `password` | Le mot de passe du [!DNL Snowflake] compte utilisateur. |
| `role` | (Facultatif) Rôle personnalisé pouvant être fourni à un utilisateur, pour une connexion donnée. Si elle n’est pas fournie, cette valeur est définie par défaut sur `public`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Snowflake] is `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

Pour plus d&#39;informations sur l&#39;authentification, reportez-vous à cette section [[!DNL Snowflake] document](<https://docs.snowflake.com/en/user-guide/key-pair-auth.html>).

### Configuration des paramètres des rôles {#configure-role-settings}

Vous devez configurer des privilèges sur un rôle, même si le rôle public par défaut est attribué, pour permettre à votre connexion source d’accéder aux [!DNL Snowflake] base de données, schéma et tableau. Les différents privilèges pour différents [!DNL Snowflake] entities se présente comme suit :

| [!DNL Snowflake] entity | Privilège du rôle Require |
| --- | --- |
| Entrepôt | OPÉRATION, UTILISATION |
| Base de données | UTILISATION |
| Schéma | UTILISATION |
| Tableau | SELECT |

>[!NOTE]
>
>La reprise automatique et la suspension automatique doivent être activées dans la configuration avancée de votre entrepôt.

Pour plus d’informations sur la gestion des rôles et des privilèges, voir [[!DNL Snowflake] Référence d’API](<https://docs.snowflake.com/en/sql-reference/sql/grant-privilege>).

## Limites et questions fréquentes {#limitations-and-frequently-asked-questions}

* Débit des données pour la variable [!DNL Snowflake] source : 2 000 enregistrements par seconde.
* Les tarifs peuvent varier en fonction de la durée d’activité d’un entrepôt et de sa taille. Pour le [!DNL Snowflake] l’intégration de la source, la plus petite taille, x-small warehouse est suffisante. Il est conseillé d’activer la suspension automatique afin que l’entrepôt puisse être suspendu seul lorsqu’il n’est pas utilisé.
* La variable [!DNL Snowflake] source interroge la base de données pour obtenir de nouvelles données toutes les 10 secondes.
* Options de configuration :
   * Vous pouvez activer une `backfill` indicateur booléen pour votre [!DNL Snowflake] source lors de la création d’une connexion source.
      * Si le renvoi est défini sur true, la valeur de timestamp.initial est définie sur 0. Cela signifie que les données dont la colonne d’horodatage est supérieure à 0 heure sont récupérées.
      * Si le renvoi est défini sur false, la valeur de timestamp.initial est définie sur -1. Cela signifie que les données dont la colonne d’horodatage est supérieure à l’heure actuelle (l’heure à laquelle la source commence l’ingestion) sont récupérées.
   * La colonne d’horodatage doit être formatée comme type : `TIMESTAMP_LTZ` ou `TIMESTAMP_NTZ`. Si la colonne d’horodatage est définie sur `TIMESTAMP_NTZ`, le fuseau horaire correspondant dans lequel les valeurs sont stockées doit être transmis via la variable `timezoneValue` . Si elle n’est pas fournie, la valeur est définie par défaut sur UTC.
      * `TIMESTAMP_TZ` ne peut pas être utilisé dans une colonne d’horodatage ou dans un mappage.

## Étapes suivantes

Le tutoriel suivant décrit les étapes à suivre pour connecter votre [!DNL Snowflake] source de diffusion en continu vers l’Experience Platform à l’aide de l’API :

* [Diffusion de données en continu à partir d’une [!DNL Snowflake] base de données à Experience Platform à l’aide de l’API Flow Service](../../tutorials/api/create/databases/snowflake-streaming.md)
