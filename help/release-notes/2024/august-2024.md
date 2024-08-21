---
title: Notes de mise à jour d’Adobe Experience Platform - Août 2024
description: Les notes de mise à jour d’août 2024 pour Adobe Experience Platform.
source-git-commit: d6eb2050cdc3d51cf8ff4189c6b9f78469f14fa9
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 30%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : mercredi 20 août 2024**

>[!TIP]
>
>Affichez un [aperçu de la documentation d’exemples de cas d’utilisation](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/use-cases/overview) pour en savoir plus sur divers cas d’utilisation tels que la prospection, l’acquisition, etc., que votre entreprise peut réaliser avec Real-Time CDP.

Mises à jour des fonctionnalités et de la documentation existantes dans Experience Platform :

- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Service d’identités](#identity-service)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonctionnalité | Description |
| ----------- | ----------- |
| L’exportation de fichiers à la demande vers des destinations par lot est désormais disponible dans l’ensemble. | L’option permettant d’exporter des fichiers à la demande vers des destinations par lots est désormais disponible pour tous les clients. Pour plus d’informations, consultez la [documentation dédiée](../../destinations/ui/export-file-now.md) . |
| Modifiez les plannings d’exportation pour plusieurs audiences exportées dans l’ [étape de planification](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | L’option permettant de modifier les plannings d’export pour plusieurs audiences exportées directement à partir de l’étape de planification du workflow d’activation des audiences est désormais disponible pour tous les clients. ![Image de l’interface utilisateur de l’Experience Platform soulignant l’option Modifier le planning de l’étape de planification.](assets/august/edit-schedule.png) {width="250" align="center" zoomable="yes"} |
| Modifiez les noms de fichiers pour plusieurs audiences exportées dans l’ [étape de planification](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | L’option permettant de modifier les noms de plusieurs fichiers exportés directement à partir de l’étape de planification du workflow d’activation de l’audience est désormais disponible pour tous les clients. ![ Image de l&#39;interface utilisateur de l&#39;Experience Platform qui met en surbrillance l&#39;option Modifier le nom du fichier lors de l&#39;étape de planification.](assets/august/edit-file-name.png) {width="250" align="center" zoomable="yes"} |
| Supprimez plusieurs audiences d’un flux de données de la page [Destination Details](../../destinations/ui/destination-details-page.md#bulk-remove). | L’option de suppression de plusieurs audiences des flux de données existants de la page **[!UICONTROL Détails de la destination]** est désormais disponible pour tous les clients. ![Image de l’interface utilisateur de l’Experience Platform qui met en surbrillance l’option Supprimer les audiences dans la page Détails de la destination.](assets/august/bulk-remove-audiences.png) {width="250" align="center" zoomable="yes"} |
| Exportez plusieurs fichiers à la demande vers des destinations par lots à partir de la page [Destination Details](../../destinations/ui/destination-details-page.md#bulk-export). | L’option permettant d’exporter plusieurs fichiers à la demande vers des destinations par lots à partir de la page **[!UICONTROL Détails de la destination]** est désormais disponible pour tous les clients. ![Image de l’interface utilisateur de l’Experience Platform mettant en surbrillance l’option Exporter le fichier maintenant dans la page Détails de la destination.](assets/august/bulk-export-file-now.png) {width="250" align="center" zoomable="yes"} |
| Modifiez les noms de fichiers de plusieurs audiences exportées à partir de la page [Destination Details](../../destinations/ui/destination-details-page.md#bulk-edit-file-names). | Vous pouvez désormais modifier les noms de plusieurs fichiers exportés directement à partir de la page **[!UICONTROL Destination Details]**. ![Image de l’interface utilisateur de l’Experience Platform mettant en surbrillance l’option de modification du nom de fichier dans la page de détails des destinations.](assets/august/edit-file-name-destination-details.png) {width="250" align="center" zoomable="yes"} |
| Supprimez plusieurs jeux de données d’un flux de données de la page [Destination Details](../../destinations/ui/export-datasets.md#remove-dataset). | L’option de suppression de plusieurs jeux de données d’un flux de données est désormais disponible pour tous les clients. ![Image de l’interface utilisateur de l’Experience Platform qui met en surbrillance l’option Supprimer les jeux de données dans la page de détails des destinations.](assets/august/bulk-remove-datasets.png) {width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Flux de création de schéma assisté ML | Utilisez des algorithmes avancés d’apprentissage automatique pour analyser vos exemples de fichiers de données CSV et créer automatiquement des schémas optimisés à l’aide de champs standard et personnalisés.<br>Principales fonctionnalités :<br><ul><li>Création plus rapide de schémas : générez des schémas directement à partir d’exemples de fichiers de données à l’aide de champs XDM générés et recommandés par ML.</li><li>Flexibilité de l’évolution des schémas : ajoutez ou mettez facilement à jour des champs dans le schéma généré.</li><li>Intégration transparente : entièrement intégrée au flux de création de schéma de base dans l’URL des schémas, ce qui garantit une expérience utilisateur fluide et cohérente.</li><li>Révision et modification efficaces : affichez et mettez à jour rapidement votre schéma à l’aide de l’éditeur d’affichage plat, ce qui rend le processus de création plus efficace et convivial.</li></ul> |

{style="table-layout:auto"}

Pour en savoir plus, consultez la [présentation de la création de schéma assistée par ML](../../xdm/ui/ml-assisted-schema-creation.md)

Pour plus d’informations sur XDM dans Platform, consultez la [présentation du système XDM](../../xdm/home.md).

## Service d’identités {#identity-service}

Utilisez Adobe Experience Platform Identity Service pour créer une vue d’ensemble complète de vos clients et de leurs comportements en rapprochant des identités entre les appareils et les systèmes, ce qui vous permet de fournir des expériences numériques personnelles et percutantes en temps réel.

**Documentation mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Guide des configurations de graphique | Lisez le [guide de configuration de graphique](../../identity-service/identity-graph-linking-rules/example-configurations.md) pour plus d’informations sur les scénarios de graphiques courants que vous pouvez rencontrer lors de l’utilisation des règles de liaison de graphiques d’identités et des données d’identité. Le guide de configuration de graphique fournit des exemples allant de scénarios graphiques simples à une seule personne à des scénarios graphiques à plusieurs personnes complexes et hiérarchiques. Vous pouvez également utiliser ce guide pour obtenir des exemples d’événements et de configurations d’algorithme que vous pouvez saisir dans l’ [ interface utilisateur de la simulation graphique ](../../identity-service/identity-graph-linking-rules/graph-simulation.md), ainsi que des ventilations de la manière dont les identités primaires sont sélectionnées selon certains scénarios de graphique. |

{style="table-layout:auto"}

Pour plus d’informations sur le service d’identités, consultez la [présentation du service d’identités](../../identity-service/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] permet de segmenter en audiences les données stockées dans [!DNL Experience Platform] qui se rapportent aux personnes (tels que les clientes et clients, les prospects, les utilisateurs et utilisatrices ou les organisations). Vous pouvez créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur [!DNL Platform] et sont facilement accessibles à partir de n’importe quelle solution Adobe.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Détails d’ingestion | Pour les audiences ayant une origine de chargement personnalisée, vous pouvez afficher plus en détail les détails de l’ingestion de l’audience dans la page des détails de l’audience. De plus, vous pouvez appliquer des libellés aux attributs de payload en sélectionnant le schéma et en sélectionnant les attributs souhaités pour l’étiquetage. Vous trouverez plus d’informations sur la section des détails de l’ingestion dans le [guide d’Audience Portal](../../segmentation/ui/audience-portal.md#ingestion-details). |

{style="table-layout:auto"}

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Utilisez les sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.

**Documentation mise à jour**

| Documentation mise à jour | Description |
| --- | --- |
| Documentation étendue sur la mise à jour des flux de données | Le guide sur la [mise à jour des flux de données de sources existantes dans l’interface utilisateur](../../sources/tutorials/ui/update-dataflows.md) a été mis à jour afin de fournir plus d’informations sur la variété de configurations que vous pouvez effectuer dans un flux de données existant. Le guide a également été mis à jour afin de clarifier le comportement attendu lorsqu’un flux de données désactivé est réactivé. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [présentation des sources](../../sources/home.md).