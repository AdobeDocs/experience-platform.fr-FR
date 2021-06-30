---
keywords: Experience Platform;accueil;rubriques populaires;Data Explorer Azure;explorateur de données Azure
solution: Experience Platform
title: Présentation du connecteur source Azure Data Explorer
topic-legacy: overview
description: Découvrez comment connecter Azure Data Explorer à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: 869bd8bb-51e6-4e0c-a3ec-ff083dda5789
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# (Version bêta) Connecteur [!DNL Azure Data Explorer]

>[!NOTE]
>
>Le connecteur [!DNL Azure Data Explorer] est en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez la [Présentation des sources](../../home.md#terms-and-conditions) .

Adobe Experience Platform fournit une connectivité native pour les fournisseurs de base de données tels que [!DNL Microsoft], MySQL et [!DNL Azure]. Vous pouvez importer vos données de ces systèmes dans [!DNL Platform].

Différents types de bases de données tierces sont pris en charge, y compris les entrepôts de données relationnels, NoSQL ou de données. La prise en charge des fournisseurs de base de données inclut [!DNL Azure Data Explorer].

## LISTE AUTORISÉE d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou des performances peuvent se produire lors de l’utilisation de sources. Pour plus d’informations, consultez la page [liste autorisée d’adresses IP](../../ip-address-allow-list.md) .

>[!IMPORTANT]
>
>Le connecteur source [!DNL Azure Data Explorer] ne prend actuellement pas en charge la connectivité de la même région à Platform. Cela signifie que si votre instance Azure utilise la même région réseau que Platform, une connexion aux sources Platform ne peut pas être établie. Actuellement, seule la connectivité inter-régions est prise en charge. Pour plus d’informations, contactez votre gestionnaire de compte d’Adobe.

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Azure Data Explorer] à [!DNL Platform] à l’aide des API ou de l’interface utilisateur :

## Connectez [!DNL Azure Data Explorer] à [!DNL Platform] à l’aide des API

- [Création d’une connexion de base de Data Explorer Azure à l’aide de l’API Flow Service](../../tutorials/api/create/databases/data-explorer.md)
- [Explorer la structure et le contenu des données d’une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/explore/database-nosql.md)
- [Création d’un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

## Connectez [!DNL Azure Data Explorer] à [!DNL Platform] à l’aide de l’interface utilisateur.

- [Création d’une connexion source de Data Explorer Azure dans l’interface utilisateur](../../tutorials/ui/create/databases/data-explorer.md)
- [Création d’un flux de données pour une connexion à la source de la base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)
