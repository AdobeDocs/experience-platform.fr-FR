---
keywords: Experience Platform ; accueil ; rubriques populaires ; Enregistrement de table Azure ; enregistrement de table azur ; ATS ; ats
solution: Experience Platform
title: Présentation du connecteur source d'Enregistrement Azure Table
topic: aperçu
description: Découvrez comment connecter Azure Table Enregistrement à Adobe Experience Platform à l'aide d'API ou de l'interface utilisateur.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 9%

---


# (Bêta) [!DNL Azure Table Storage] connecteur

>[!NOTE]
>
>Le connecteur [!DNL Azure Table Storage] est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../home.md#terms-and-conditions).

Adobe Experience Platform permet l’assimilation de données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de services [!DNL Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

[!DNL Experience Platform] prend en charge l’ingestion de données provenant d’une base de données tierce. [!DNL Platform] peut se connecter à différents types de bases de données, telles que relationnelles, NoSQL ou des entrepôts de données. Les fournisseurs de base de données prennent en charge [!DNL Azure Table Storage].

## LISTE AUTORISÉE d&#39;adresse IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas d’adresses IP spécifiques à votre région à votre liste autorisée, des erreurs ou des performances risquent d’apparaître lors de l’utilisation de sources. Pour plus d&#39;informations, consultez la page [liste autorisée d&#39;adresse IP](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>Le connecteur source [!DNL Azure Table Storage] ne prend actuellement pas en charge la connectivité de la même région à la plate-forme. Cela signifie que si votre instance Azure utilise la même région réseau que Platform, une connexion aux sources de la plateforme ne peut pas être établie. Actuellement, seule la connectivité inter-régions est prise en charge. Pour plus d&#39;informations, contactez votre gestionnaire de compte d&#39;Adobe.

La documentation ci-dessous fournit des informations sur la façon de se connecter [!DNL Azure Table Storage] à [!DNL Platform] à l&#39;aide d&#39;API ou de l&#39;interface utilisateur :

## Connectez [!DNL Azure Table Storage] à [!DNL Platform] à l’aide d’API.

- [Création d&#39;une connexion à la source d&#39;Enregistrement Azure Table à l&#39;aide de l&#39;API Flow Service](../../tutorials/api/create/databases/ats.md)
- [Exploration d’un système de base de données à l’aide de l’API du service de flux](../../tutorials/api/explore/database-nosql.md)
- [Collecte de données à partir d’une base de données à l’aide de l’API du service de flux](../../tutorials/api/collect/database-nosql.md)

## Connectez [!DNL Azure Table Storage] à [!DNL Platform] à l’aide de l’interface utilisateur.

- [Créer une connexion source d&#39;Enregistrement Azure Table dans l&#39;interface utilisateur](../../tutorials/ui/create/databases/ats.md)
- [Configuration d’un flux de données pour une connexion à une base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)