---
title: Notes de mise à jour d’Adobe Experience Platform - Avril 2023
description: Les notes de mise à jour d’avril 2023 pour Adobe Experience Platform.
source-git-commit: 9f50ca4b2a4c576af5ce8ee5c085a7603fed2560
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 48%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 26 avril 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Préparation de données](#data-prep)
- [Sources](#sources)

## Préparation des données {#data-prep}

La préparation des données permet aux personnes travaillant dans l’ingénierie de données de mapper, de transformer et de valider les données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mises à jour de la période de renvoi d’Adobe Analytics dans les environnements de test hors production | La période de renvoi d’Adobe Analytics dans les environnements de test hors production a été réduite à trois mois. Le renvoi des environnements de test de production reste le même au bout de 13 mois. Cette modification s’applique uniquement aux nouveaux flux et n’affecte pas les flux existants. Pour plus d’informations, reportez-vous à la section [Présentation d’Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Nouvelle fonction de mappeur pour convertir les chaînes FPID en ECID | Utilisez la variable `fpid_to_ecid` pour convertir des chaînes FPID en ECID en vue de les utiliser dans des applications Experience Platform et Experience Cloud. Pour plus d’informations, consultez le [guide des fonctions de préparation de données](../../data-prep/functions.md). |

{style="table-layout:auto"}

Pour plus d’informations sur la préparation des données, consultez la [présentation de la préparation des données](../../data-prep/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de l’API pour le filtrage des données au niveau des lignes pour Microsoft Dynamics, Salesforce CRM et le Marketing Cloud Salesforce | Utilisez des opérateurs logiques et de comparaison pour filtrer les données de niveau ligne pour les sources de Marketing Cloud Microsoft Dynamics, Salesforce CRM et Salesforce. Pour plus d’informations, lisez le guide sur le [filtrage des données d’une source à l’aide de l’API](../../sources/tutorials/api/filter.md). |
| Disponibilité bêta de Shopify Streaming | Le [Shopify Streaming source](../../sources/connectors/ecommerce/shopify-streaming.md) est désormais disponible en version bêta. Utilisez la source de diffusion en continu Shopify pour diffuser des données de votre compte de partenaires Shopify vers Experience Platform. |
| Disponibilité générale de l’intégration OneTrust | Le [Source d’intégration OneTrust](../../sources/connectors/consent-and-preferences/onetrust.md) est désormais GA. Utilisez la source d’intégration OneTrust pour importer les données de consentement et de préférences de votre compte d’intégration OneTrust vers Experience Platform. |
| Disponibilité générale d’Oracle Service Cloud | Le [Source Oracle Service Cloud](../../sources/connectors/customer-success/oracle-service-cloud.md) est désormais GA. Utilisez la source Oracle Service Cloud pour importer vos données Oracle Service Cloud dans Experience Platform. |

{style="table-layout:auto"}

Pour en savoir plus sur les sources, lisez la [présentation des sources](../../sources/home.md).
