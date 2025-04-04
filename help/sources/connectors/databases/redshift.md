---
title: Présentation Du Connecteur Source Amazon Redshift
description: Découvrez comment connecter Amazon Redshift à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 22%

---

# Source [!DNL Amazon Redshift]

>[!IMPORTANT]
>
>- La source [!DNL Amazon Redshift] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time CDP Ultimate.
>
>- Vous pouvez désormais utiliser la source [!DNL Amazon Redshift] lors de l’exécution de Adobe Experience Platform sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).


Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’une base de données tierce. Experience Platform peut se connecter à différents types de bases de données tels que des entrepôts relationnels, NoSQL ou de données. La prise en charge des fournisseurs de base de données inclut [!DNL Amazon Redshift].

## Configurer votre source de [!DNL Amazon Redshift] pour Experience Platform sur Azure {#azure}

Suivez les étapes ci-dessous pour savoir comment configurer votre compte [!DNL Amazon Redshift] pour Experience Platform sur Azure.

### Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Configurer votre source de [!DNL Amazon Redshift] pour Experience Platform sur Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).

### PLACER SUR LA LISTE AUTORISÉE Adresse IP utilisée pour la connexion à AWS

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform sur AWS. Pour plus d’informations, consultez le guide sur [la liste autorisée d’adresses IP pour se connecter à Experience Platform sur AWS](../../ip-address-allow-list.md).

## Connexion de [!DNL Amazon Redshift] à Experience Platform à l’aide d’API

- [Connecter Amazon Redshift à Experience Platform à l’aide de l’API Flow Service](../../tutorials/api/create/databases/redshift.md)
- [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Créer un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

## Connexion d’[!DNL Amazon Redshift] à Experience Platform à l’aide de l’interface utilisateur

- [Créer une connexion source Amazon Redshift dans l’interface utilisateur](../../tutorials/ui/create/databases/redshift.md)
- [Créer un flux de données pour une connexion source de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)
