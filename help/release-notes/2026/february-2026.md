---
title: Notes de mise à jour d’Adobe Experience Platform - Février 2026
description: Les notes de mise à jour de février 2026 pour Adobe Experience Platform.
source-git-commit: afb1e0266b4c5485ba574f95aab3a56485d176b3
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 47%

---

# Notes de mise à jour d’Adobe Experience Platform

>[!TIP]
>
>Reportez-vous à la documentation suivante pour les notes de mise à jour des autres applications Adobe Experience Platform :
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/fr/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/latest)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de mise à jour : mercredi 17 février 2026**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Alertes](#alerts)
- [Destinations](#destinations)
- [Sources](#sources)

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités Experience Platform. Vous pouvez vous abonner à différentes règles d’alerte via l’onglet [!UICONTROL Alerts] de l’interface utilisateur d’Experience Platform et choisir de recevoir des messages d’alerte dans l’interface utilisateur elle-même ou par e-mail de notification.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Intégration d’[!DNL Slack] pour les alertes destinées aux clients et clientes | Vous pouvez désormais envoyer des alertes destinées aux clients et clientes à [!DNL Slack]. Suivez le [tutoriel détaillé](../../observability/alerts/slack-integration.md) pour configurer l’intégration [!DNL Slack] et recevoir des notifications d’alerte directement dans votre espace de travail [!DNL Slack]. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [[!DNL Observability Insights] vue d’ensemble](../../observability/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Destination | Description |
| --- | --- |
| [[!DNL Snowflake] Lot](../../destinations/catalog/warehouses/snowflake-batch.md) généralement disponible | La destination [!DNL Snowflake] par lots est désormais disponible pour tous. Les clients Real-Time CDP du monde entier peuvent désormais utiliser ce connecteur pour activer des données dans leurs comptes Snowflake sans avoir à copier physiquement les données. Toutes les limitations de la version limitée ont été levées (disponibilité pour les clients américains uniquement, prise en charge des audiences appartenant à la politique de fusion par défaut uniquement). |

{style="table-layout:auto"}

**Correctifs et améliorations**

| Correction | Description |
| --- | --- |
| Alerte Taux d’échec de l’activation dépassé | L’alerte de destination Taux d’échec de l’activation dépassé utilise désormais correctement le seuil que vous configurez lors de l’évaluation et de l’envoi de l’alerte. Auparavant, l’alerte se déclenchait à un taux d’échec de 1 %, quel que soit le pourcentage que vous avez configuré. Voir [règles d’alerte standard](../../observability/alerts/rules.md#destinations) pour plus d’informations sur cette alerte. |
| Compte rendu des performances des identités exclues de la correspondance client Google | Correction d’un bug dans la logique de comptage des enregistrements ignorés en raison duquel un nombre exagéré de profils exclus s’affichait pour les destinations de correspondance client Google. Le comportement d’activation et d’exportation n’a pas été affecté ; seuls les nombres signalés étaient incorrects. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des destinations](../../destinations/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Sources nouvelles ou mises à jour**

| Source | Description |
| --- | --- |
| Prise en charge du catalogue Unity dans [!DNL Databricks] connecteur source | Le connecteur source [!DNL Databricks] prend désormais en charge le catalogue Unity. Lisez la documentation [[!DNL Databricks]](../../sources/connectors/databases/databricks.md) mise à jour pour savoir comment utiliser le catalogue Unity lorsque vous configurez votre connexion source. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des sources](../../sources/home.md).
