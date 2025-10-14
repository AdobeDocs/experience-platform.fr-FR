---
title: Notes de mise à jour préliminaires d’Experience Platform
description: Aperçu des dernières notes de mise à jour de Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 9cf809f8fd6e424b4dcd800c3d554e4eb0e337dc
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 33%

---

# Notes de mise à jour préliminaires de Adobe Experience Platform

>[!IMPORTANT]
>
>Ce document est conçu comme un **aperçu** des notes de mise à jour du mois en cours. Les éléments de version peuvent faire l’objet de modifications et peuvent être ajoutés ou supprimés dans la version finale.

>[!TIP]
>
>Reportez-vous à la documentation suivante pour les notes de mise à jour des autres applications Adobe Experience Platform :
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/fr/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/e-release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de publication : octobre 2025**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Alertes](#alerts)
- [Destinations](#destinations)
- [Service de segmentation](#segmentation-service)
- [Sources](#sources)

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités Experience Platform. Vous pouvez vous abonner à différentes règles d’alerte à l’aide de l’onglet [!UICONTROL Alertes] dans l’interface d’utilisation d’Experience Platform. Vous pouvez aussi choisir de recevoir les messages d’alerte dans l’UI elle-même ou par le biais de notifications par e-mail.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Alerte relative au taux d’échec de destination | Une nouvelle alerte a été ajoutée pour les destinations : **Le taux d’échec de la destination dépasse le seuil**. Cette alerte vous avertit lorsque le nombre d’enregistrements ayant échoué lors de l’activation des données a dépassé le seuil autorisé, ce qui vous permet de répondre rapidement aux problèmes d’activation. |

{style="table-layout:auto"}

Pour plus d’informations sur les alertes, consultez la [[!DNL Observability Insights] vue d’ensemble](../observability/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Destination | Description |
| --- | --- |
| [!DNL AdForm] | Utilisez cette destination pour envoyer des audiences Adobe Real-Time CDP à [!DNL AdForm] pour activation en fonction de l’Experience Cloud ID (ECID) et de l’ID Fusion de [!DNL AdForm]. ID Fusion de [!DNL AdForm] est un service de résolution d’ID qui vous permet d’activer vos audiences propriétaires en fonction de l’Experience Cloud ID (ECID). |
| `Amazon Ads` | Nous avons ajouté la prise en charge d’identifiants personnels supplémentaires tels que `firstName`, `lastName`, `street`, `city`, `state`, `zip` et `country`. Le mappage de ces champs en tant qu’identités cibles peut améliorer les taux de correspondance d’audience. |

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge du chiffrement côté serveur [!DNL AES256] dans les destinations [!DNL Amazon S3] | Les destinations [!DNL Amazon S3] prennent désormais en charge [!DNL AES256] chiffrement côté serveur, ce qui renforce la sécurité des données exportées. Vous pouvez configurer cette méthode de chiffrement lors de la configuration ou de la mise à jour de vos connexions de destination [!DNL Amazon S3], en veillant à ce que vos données soient chiffrées au repos à l’aide d’algorithmes de chiffrement [!DNL AES256] standard. Pour plus d’informations, consultez la [[!DNL Amazon] documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingEncryption.html). |
| [Plusieurs nouvelles destinations qui prennent en charge la surveillance au niveau de l’audience](../dataflows/ui/monitor-destinations.md#audience-level-view) | Les destinations suivantes prennent désormais en charge la surveillance au niveau de l’audience : <ul><li>[!DNL Airship Tags]</li><li>[!DNL Salesforce Marketing Cloud] (API)</li><li>[!DNL Marketo Engage]</li><li>[!DNL Microsoft Bing]</li><li>(V1) [!DNL Pega CDH Realtime Audience]</li><li>(V2) [!DNL Pega CDH Realtime Audience]</li><li>Engagement de compte [!DNL Salesforce Marketing Cloud]</li><li>[!DNL The Trade Desk]</li></ul> |
| Correctif des mécanismes de sécurisation de l’exportation des jeux de données | Un correctif a été implémenté pour les mécanismes de sécurisation d’exportation des jeux de données. Auparavant, certains jeux de données qui incluaient une colonne d’horodatage mais n’étaient _pas_ basés sur le schéma XDM Experience Events étaient incorrectement traités comme des jeux de données Experience Events, ce qui limitait les exportations à un intervalle de recherche en amont de 365 jours. Le mécanisme de sécurisation de recherche en amont documenté de 365 jours s’applique désormais exclusivement aux jeux de données d’événements d’expérience. Les jeux de données utilisant un schéma autre que le schéma XDM Experience Events sont désormais régis par le mécanisme de sécurisation de 10 milliards d’enregistrements. Certains clients peuvent voir des nombres d’exportation accrus pour les jeux de données qui se trouvaient par erreur sous l’intervalle de recherche en amont de 365 jours. Vous pouvez ainsi exporter des jeux de données pour les workflows prédictifs disposant d’un long intervalle de recherche en amont. Pour plus d’informations, consultez la section [ Mécanismes de sécurisation d’exportation de jeux de données ](../destinations/guardrails.md#dataset-exports). |
| Rapports améliorés au niveau de l’audience pour les destinations d’entreprise | Amélioration de la logique de création de rapports au niveau des audiences pour les destinations d’entreprise. Après cette version, les clients verront des chiffres de création de rapports d’audience plus précis qui incluent uniquement les audiences pertinentes pour la destination sélectionnée. Cet ajustement de surveillance garantit que les rapports incluent uniquement les audiences mappées sur le flux de données, ce qui fournit des informations plus claires sur l’activation réelle des données. Cela n’a aucune incidence sur la quantité de données activées. Il s’agit simplement d’une amélioration de la surveillance visant à améliorer la précision des rapports. |

Pour plus d’informations, consultez la [vue d’ensemble des destinations](../destinations/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Surveillance de la segmentation en flux continu | La surveillance en temps réel de la segmentation en flux continu offre une transparence sur les mesures de taux d’évaluation, de latence et de qualité des données au niveau des sandbox, des jeux de données et de l’audience. Cela participe à des alertes proactives et à des informations exploitables pour aider les ingénieures et ingénieurs de données à identifier les violations de capacité et les problèmes d’ingestion. Les mesures de surveillance incluent le taux d’évaluation, la latence d’ingestion P95, ainsi que les enregistrements reçus, évalués, en échec et ignorés. Les fonctionnalités d’affichage par jeu de données et d’affichage par audience offrent une visibilité complète sur les nouveaux profils qualifiés et disqualifiés. |

Pour plus d’informations, consultez la [[!DNL Segmentation Service] vue d’ensemble](../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Sources nouvelles ou mises à jour**

| Source | Description |
| --- | --- |
| [!BADGE Beta ]{type=Informative} sources de [!DNL Talon.one] pour les données de fidélité | Utilisez les sources de [!DNL Talon.One] pour ingérer des données de fidélité par lots et par flux dans Experience Platform. Le connecteur prend en charge la diffusion en continu des données de profil, des données de transaction et des données de fidélité, y compris les points gagnés, les points échangés, les points expirés et les données de niveau. |

**Sources mises à jour**

| Source | Description |
| --- | --- |
| Disponibilité générale de la source [!DNL Google Ads] (API uniquement) | La version de l’API de la source [!DNL Google Ads] est désormais en disponibilité générale. La documentation de l’API a été mise à jour afin de refléter le fait que la dernière version est désormais `v21` et qu’Experience Platform prend en charge toutes les versions v19 et ultérieures. La version de l’interface utilisateur reste en version bêta et ne prend en charge qu’une ingestion unique. Pour utiliser l’ingestion de données incrémentielle, utilisez l’itinéraire d’API. |
| Prise en charge du réseau virtuel [!DNL Azure Event Hubs] | Adobe prend désormais explicitement en charge les connexions réseau virtuelles à Azure Event Hubs, ce qui permet le transfert de données sur des réseaux privés plutôt que publics. Placer sur la liste autorisée Les clients peuvent utiliser Experience Platform VNet pour acheminer le trafic Event Hubs de manière privée via la dorsale principale privée Azure, offrant ainsi une sécurité et une conformité améliorées aux workflows d’ingestion de données. |

Pour plus d’informations, consultez la [vue d’ensemble des sources](../sources/home.md).
