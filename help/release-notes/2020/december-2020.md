---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 9 décembre 2020
doc-type: release notes
last-update: December 9, 2020
author: ens60013
translation-type: tm+mt
source-git-commit: 25c162f50f0a66d77eb638dbf87893af3c543ddc
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 50%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de lancement : 9 décembre 2020**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Sources]](#sources)

## [!DNL Sources] {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mettre à jour les détails de compte et de connexion pour les sources de flux continu | Vous pouvez désormais mettre à jour les noms, descriptions et informations d’identification des connexions de flux continu existantes à l’aide de l’ [!DNL Flow Service] API et de l’interface utilisateur. Pour plus d’informations, voir le didacticiel sur la [mise à jour des connexions à l’aide de l’API](../../sources/tutorials/api/update.md) et la [modification des détails du compte à l’aide de l’interface utilisateur](../../sources/tutorials/ui/monitor.md). |
| Supprimer des flux de données | Les flux de données en flux continu contenant des erreurs ou devenus inutiles peuvent maintenant être supprimés à l’aide de l’ [!DNL Flow Service] API et de l’interface utilisateur. Pour plus d’informations, voir le didacticiel sur la [suppression de flux de données à l’aide de l’API](../../sources/tutorials/api/delete-dataflows.md) et la [suppression de flux de données à l’aide de l’interface utilisateur](../../sources/tutorials/ui/delete.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).