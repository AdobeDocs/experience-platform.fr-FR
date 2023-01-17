---
title: Notes de mise à jour d’Adobe Experience Platform
description: Dernières notes de mise à jour pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f8e8ec0fb13fc988d47bb3bbe85f953e66b33f13
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 100%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 23 novembre 2022.**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Collecte de données](#data-collection)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Sources](#sources)

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Extension [!DNL AWS] pour le transfert d’événement | Vous pouvez désormais envoyer des données à [!DNL Amazon Web Services] ([!DNL AWS]) à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations, consultez la présentation de l’extension [[!DNL AWS] ](../../tags/extensions/server/aws/overview.md). |
| Extension [!DNL Google Ads Enhanced Conversions] pour le transfert d’événement | Vous pouvez désormais envoyer des données de conversion à [!DNL Google Ads] à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations, consultez la présentation de l’extension [[!DNL Google Ads Enhanced Conversions] ](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md). |
| Extension [!DNL Microsoft Azure] pour le transfert d’événement | Vous pouvez désormais envoyer des données à [!DNL Microsoft Azure] à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations, consultez la présentation de l’extension [[!DNL Microsoft Azure] ](../../tags/extensions/server/azure/overview.md). |

Pour plus d’informations sur les fonctionnalités de collecte de données de Platform, consultez la [présentation de la collecte de données](../../collection/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Attribuer des champs à des classes personnalisées lors de l’ajout direct à un schéma | Auparavant, lorsque vous [ajoutiez directement un champ individuel à un schéma](../../xdm/ui/resources/schemas.md#add-individual-fields), vous ne pouviez attribuer le champ qu’à un groupe de champs en tant que sa ressource parente. Désormais, en plus des groupes de champs, vous pouvez [attribuer le champ à une classe personnalisée](../../xdm/ui/resources/schemas.md#add-to-class) en tant que sa ressource parente. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur XDM dans Platform, consultez la [présentation du système XDM](../../xdm/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- | 
| Disponibilité Beta de la source Oracle Service Cloud | Utilisez la source Oracle Service Cloud pour ingérer des données de votre compte Oracle Service Cloud vers Experience Platform. Pour plus d’informations, consultez la documentation relative à la [source Oracle Service Cloud](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Pour en savoir plus sur les sources, lisez la [présentation des sources](../../sources/home.md).