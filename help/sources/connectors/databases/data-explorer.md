---
keywords: Experience Platform ; accueil ; rubriques populaires ; Data Explorer Azure ; explorateur de données azur
solution: Experience Platform
title: Présentation du connecteur source Azure Data Explorer
topic: aperçu
description: Découvrez comment connecter Azure Data Explorer à Adobe Experience Platform à l'aide d'API ou de l'interface utilisateur.
translation-type: tm+mt
source-git-commit: 0fb97fcf5d3f8230ff86906aeef245e4a7f44f30
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# (Bêta) [!DNL Azure Data Explorer] connecteur

>[!NOTE]
>
>Le connecteur [!DNL Azure Data Explorer] est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../home.md#terms-and-conditions).

Adobe Experience Platform fournit une connectivité native aux fournisseurs de base de données tels que [!DNL Microsoft], MySQL et [!DNL Azure]. Vous pouvez importer vos données de ces systèmes dans [!DNL Platform].

Différents types de bases de données tierces sont pris en charge, y compris les entrepôts de données relationnels, NoSQL ou Data Warehouse. La prise en charge des fournisseurs de base de données inclut [!DNL Azure Data Explorer].

## LISTE AUTORISÉE d&#39;adresse IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas d’adresses IP spécifiques à votre région à votre liste autorisée, des erreurs ou des performances risquent d’apparaître lors de l’utilisation de sources. Pour plus d&#39;informations, consultez la page [liste autorisée d&#39;adresse IP](../../ip-address-allow-list.md).

>[!IMPORTANT]
>
>Le connecteur source [!DNL Azure Data Explorer] ne prend actuellement pas en charge la connectivité de la même région à la plate-forme. Cela signifie que si votre instance Azure utilise la même région réseau que Platform, une connexion aux sources de la plateforme ne peut pas être établie. Actuellement, seule la connectivité inter-régions est prise en charge. Pour plus d&#39;informations, contactez votre gestionnaire de compte d&#39;Adobe.

La documentation ci-dessous fournit des informations sur la façon de se connecter [!DNL Azure Data Explorer] à [!DNL Platform] à l&#39;aide d&#39;API ou de l&#39;interface utilisateur :

## Connectez [!DNL Azure Data Explorer] à [!DNL Platform] à l’aide d’API.

- [Création d&#39;une connexion à la source Azure Data Explorer à l&#39;aide de l&#39;API Flow Service](../../tutorials/api/create/databases/data-explorer.md)
- [Exploration d’un système de base de données à l’aide de l’API du service de flux](../../tutorials/api/explore/database-nosql.md)
- [Collecte de données à partir d’une base de données à l’aide de l’API du service de flux](../../tutorials/api/collect/database-nosql.md)

## Connectez [!DNL Azure Data Explorer] à [!DNL Platform] à l’aide de l’interface utilisateur.

- [Création d&#39;une connexion à la source du Data Explorer Azure dans l&#39;interface utilisateur](../../tutorials/ui/create/databases/data-explorer.md)
- [Configuration d’un flux de données pour une connexion à une base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)