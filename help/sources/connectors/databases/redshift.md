---
title: Présentation Du Connecteur Source Amazon Redshift
description: Découvrez comment connecter Amazon Redshift à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
TQID: https://experienceleague.adobe.com/F8KPhV2REwdWCOO7TULLH7Pe9lPIn5EI12pA-5Mp0A0
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 403
ht-degree: 18%

---

# Source [!DNL Amazon Redshift]

>[!IMPORTANT]
>
>- La source [!DNL Amazon Redshift] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time CDP Ultimate.
>
>- Vous pouvez désormais utiliser la source [!DNL Amazon Redshift] lors de l’exécution de Adobe Experience Platform sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).


Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’une base de données tierce. Experience Platform peut se connecter à différents types de bases de données tels que des entrepôts relationnels, NoSQL ou de données. La prise en charge des fournisseurs de base de données inclut [!DNL Amazon Redshift].

## Configurer votre source de [!DNL Amazon Redshift] pour Experience Platform sur Azure {#azure}

Suivez les étapes ci-dessous pour savoir comment configurer votre compte [!DNL Amazon Redshift] pour Experience Platform sur Azure.

### Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform sur Azure. Pour plus d’informations, consultez le guide sur [la liste autorisée d’adresses IP pour se connecter à Experience Platform sur Azure](../../ip-address-allow-list.md).

## Configurer votre source de [!DNL Amazon Redshift] pour Experience Platform sur Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).

### Adresse IP utilisée pour la connexion à AWS

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform sur AWS. Pour plus d’informations, consultez le guide sur [la liste autorisée d’adresses IP pour se connecter à Experience Platform sur AWS](../../ip-address-allow-list.md).

## Connexion de [!DNL Amazon Redshift] à Experience Platform à l’aide d’API

- [Connecter Amazon Redshift à Experience Platform à l’aide de l’API Flow Service](../../tutorials/api/create/databases/redshift.md)
- [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Créer un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

## Connexion d’[!DNL Amazon Redshift] à Experience Platform à l’aide de l’interface utilisateur

- [Créer une connexion source Amazon Redshift dans l’interface utilisateur](../../tutorials/ui/create/databases/redshift.md)
- [Créer un flux de données pour une connexion source de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)
