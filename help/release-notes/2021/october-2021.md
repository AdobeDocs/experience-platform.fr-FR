---
title: Notes de mise à jour d’Adobe Experience Platform
description: Dernières notes de mise à jour pour Adobe Experience Platform.
source-git-commit: 0c507a26f551af1eb17889e8e77a036e3c106240
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 66%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 27 octobre 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Sources](#sources)

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| --- | --- |
| Améliorations de la source [!DNL Amazon S3] | Vous pouvez désormais utiliser la variable `s3SessionToken` pour connecter votre [!DNL Amazon S3] compte vers Platform à l’aide d’informations d’identification de sécurité temporaires. Ce jeton vous permet de fournir un accès temporaire à court terme à votre [!DNL Amazon S3] aux utilisateurs dans des environnements non approuvés. Pour plus d’informations, voir la [[!DNL Amazon S3] documentation ](../../sources/connectors/cloud-storage/s3.md#prerequisites). |
| [!DNL Generic REST API] (version bêta) | Vous pouvez désormais créer une [!DNL Generic REST API] connexion source à l’aide de la fonction [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) ou le [interface utilisateur](../../sources/tutorials/ui/create/protocols/generic-rest.md) pour importer des données d’une application REST générique vers Platform. Pour plus d’informations, consultez la [[!DNL Generic REST API] présentation](../../sources/connectors/protocols/generic-rest.md). |
| [!DNL Zoho CRM] (version bêta) | Vous pouvez désormais créer une [!DNL Zoho CRM] connexion source à l’aide de la fonction [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) ou le [interface utilisateur](../../sources/tutorials/ui/create/crm/zoho.md) pour importer des données de [!DNL Zoho CRM] compte à Platform. Pour plus d’informations, consultez la [[!DNL Zoho CRM] présentation](../../sources/connectors/crm/zoho.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
