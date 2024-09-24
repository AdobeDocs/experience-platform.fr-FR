---
title: Notes de mise à jour d’Adobe Experience Platform - Août 2024
description: Les notes de mise à jour d’août 2024 pour Adobe Experience Platform.
exl-id: 153891e9-fd82-4894-a047-c8d82f214fef
source-git-commit: 4fecb47084a522b4eb9808dc317e0d70e7ef42c6
workflow-type: ht
source-wordcount: '1562'
ht-degree: 100%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 20 août 2024**

>[!TIP]
>
>Consultez une [vue d’ensemble de la documentation d’exemples de cas d’utilisation](https://experienceleague.adobe.com/fr/docs/experience-platform/rtcdp/use-cases/overview) pour en savoir plus sur divers cas d’utilisation tels que la prospection, l’acquisition, etc., que votre entreprise peut réaliser avec Real-Time CDP.

Mises à jour des fonctionnalités et de la documentation existantes dans Experience Platform :

- [Contrôle d’accès basé sur les attributs](#abac)
- [Ingestion des données](#data-ingestion)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Service d’identités](#identity-service)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Contrôle d’accès basé sur les attributs {#abac}

Le contrôle d’accès basé sur les attributs est une fonctionnalité d’Adobe Experience Platform qui offre aux marques soucieuses de la confidentialité une plus grande flexibilité pour gérer l’accès utilisateur. Les objets individuels tels que les champs de schéma et les segments peuvent être affectés à des rôles d’utilisateur. Cette fonctionnalité vous permet d’accorder ou de révoquer l’accès à des objets individuels pour des utilisateurs Platform spécifiques au sein de votre organisation.

Grâce au contrôle d’accès basé sur les attributs, l’administration de votre organisation peut contrôler l’accès des utilisateurs et utilisatrices aux données personnelles sensibles (SPD), aux informations d’identification personnelle (PII) et à d’autres types de données personnalisées sur l’ensemble des workflows et ressources de Platform. Les administrateurs et administratrices peuvent définir des rôles d’utilisateur ou d’utilisatrice qui n’ont accès qu’à des champs spécifiques et aux données correspondant à ces champs.

**Nouvelle fonctionnalité**

| Mise à jour des fonctionnalités | Description |
| --- | --- |
| Nouvelle fonctionnalité Gestionnaire d’autorisations | Vous pouvez désormais utiliser le [Gestionnaire d’autorisations](../../access-control/abac/permission-manager/overview.md) pour générer des rapports à l’aide de requêtes simples, ce qui vous permettra de comprendre la gestion des accès et de gagner du temps en vérifiant les autorisations d’accès sur plusieurs workflows et niveaux de granularité. Pour plus d’informations sur la création de rapports pour les personnes et les rôles, consultez le [guide d’utilisation du Gestionnaire d’autorisations](../../access-control/abac/permission-manager/permissions.md). ![Image de l’interface d’utilisation d’Experience Platform qui met en surbrillance le Gestionnaire d’autorisations dans le volet de navigation de gauche.](assets/august/permission-manager-rn.png "Gestionnaire d’autorisations dans l’interface d’utilisation."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Pour plus d’informations sur le contrôle d’accès basé sur les attributs, consultez la [présentation du contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md). Pour consulter un guide complet sur le workflow de contrôle d’accès basé sur les attributs, reportez-vous au [guide complet du contrôle d’accès basé sur les attributs](../../access-control/abac/end-to-end-guide.md).

## Ingestion de données (mise à jour le 23 août) {#data-ingestion}

Adobe Experience Platform propose un ensemble riche de fonctionnalités permettant d’ingérer n’importe quel type et n’importe quelle latence de données. Vous pouvez les ingérer à l’aide des API Batch ou Streaming, des sources intégrées Adobe, des partenaires d’intégration de données ou de l’interface utilisateur d’Adobe Experience Platform.

**Mise à jour de la gestion du format de date lors de l’ingestion de données par lots**

Cette version corrige un problème lié à la *gestion du format de date* dans l’ingestion de données par lots. Auparavant, le système transformait les champs de date insérés par la clientèle au format `Date` en format `DateTime`. Cela signifie que le fuseau horaire était automatiquement ajouté aux champs et qu’il causait des difficultés aux personnes préférant ou demandant le format `Date`. Dorénavant, le fuseau horaire ne sera pas automatiquement ajouté aux champs de type `Date`. Cette mise à jour garantit que le format exporté des données correspond au format représenté sur le profil pour ce champ, comme le demande la clientèle.

Champs `Date` avant la version : `"birthDate": "2018-01-12T00:00:00Z"`
Champs `Date` après la version : `"birthDate": "2018-01-12"`

En savoir plus sur l’[ingestion par lots](/help/ingestion/batch-ingestion/overview.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#new-updated-destinations}

| Destination | Description |
| ----------- | ----------- |
| [Braze](/help/destinations/catalog/mobile-engagement/braze.md) | [!UICONTROL Braze] gère plusieurs instances différentes pour leur tableau de bord et leurs points d’entrée REST. Les clients et clientes [!UICONTROL Braze] doivent utiliser le point d’entrée REST correct en fonction de l’instance sur laquelle se fait votre approvisionnement. Cette version ajoute un nouveau point d’entrée US-07 que vous pouvez sélectionner lors de la connexion à [!UICONTROL Braze]. |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonctionnalité | Description |
| ----------- | ----------- |
| L’export de fichiers à la demande vers des destinations par lot est désormais disponible de façon générale. | L’option permettant d’exporter des fichiers à la demande vers des destinations par lots est désormais disponible pour l’ensemble de la clientèle. Pour plus d’informations, consultez la [documentation appropriée](../../destinations/ui/export-file-now.md). |
| Modifier les plannings d’export pour plusieurs audiences exportées à l’[étape de planification](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | L’option permettant de modifier les plannings d’export pour plusieurs audiences exportées directement à partir de l’étape de planification du workflow d’activation des audiences est désormais disponible pour l’ensemble de la clientèle. ![Image de l’interface d’utilisation d’Experience Platform qui illustre l’option Modifier le planning de l’étape de planification.](assets/august/edit-schedule.png "Option Modifier le planning à l’étape de planification."){width="250" align="center" zoomable="yes"} |
| Modifier les noms de fichiers pour plusieurs audiences exportées à l’[étape de planification](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | L’option permettant de modifier les noms de plusieurs fichiers exportés directement à partir de l’étape de planification du workflow d’activation de l’audience est désormais disponible pour l’ensemble de la clientèle. ![Image de l’interface d’utilisation d’Experience Platform qui met en surbrillance l’option Modifier le nom de fichier de l’étape de planification.](assets/august/edit-file-name.png "Option Modifier le nom de fichier à l’étape de planification."){width="250" align="center" zoomable="yes"} |
| Supprimer plusieurs audiences d’un flux de données de la page [Détails de la destination](../../destinations/ui/destination-details-page.md#bulk-remove). | L’option de suppression de plusieurs audiences des flux de données existants de la page **[!UICONTROL Détails de la destination]** est désormais disponible pour l’ensemble de la clientèle. ![Image de l’interface d’utilisation d’Experience Platform qui met en surbrillance l’option Supprimer les audiences de la page Détails de la destination.](assets/august/bulk-remove-audiences.png "Option Supprimer des audiences de la page Détails de la destination."){width="250" align="center" zoomable="yes"} |
| Exporter plusieurs fichiers à la demande vers des destinations par lots à partir de la page [Détails de la destination](../../destinations/ui/destination-details-page.md#bulk-export). | L’option permettant d’exporter plusieurs fichiers à la demande vers des destinations par lots à partir de la page **[!UICONTROL Détails de la destination]** est désormais disponible pour l’ensemble de la clientèle. ![Image de l’interface d’utilisation d’Experience Platform mettant en surbrillance l’option Exporter le fichier maintenant de la page Détails de la destination.](assets/august/bulk-export-file-now.png "Option Exporter le fichier maintenant de la page Détails de la destination."){width="250" align="center" zoomable="yes"} |
| Modifier les noms de fichiers de plusieurs audiences exportées à partir de la page [Détails de la destination](../../destinations/ui/destination-details-page.md#bulk-edit-file-names). | Vous pouvez désormais modifier les noms de plusieurs fichiers exportés directement à partir de la page **[!UICONTROL Détails de la destination]**. ![Image de l’interface d’utilisation d’Experience Platform qui met en surbrillance l’option Modifier le nom de fichier de la page Détails de la destination.](assets/august/edit-file-name-destination-details.png "Option Modifier le nom de fichier de la page Détails de la destination."){width="250" align="center" zoomable="yes"} |
| Supprimer plusieurs jeux de données d’un flux de données de la page [Détails de la destination](../../destinations/ui/export-datasets.md#remove-dataset). | L’option de suppression de plusieurs jeux de données d’un flux de données est désormais disponible pour toutes l’ensemble de la clientèle. ![Image de l’interface d’utilisation d’Experience Platform qui met en surbrillance l’option Supprimer les jeux de données de la page Détails de la destination.](assets/august/bulk-remove-datasets.png "Option Supprimer les jeux de données de la page Détails de la destination."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Flux de création de schéma assisté par ML | Utilisez des algorithmes avancés de machine learning pour analyser vos fichiers de données d’exemple et créer automatiquement des schémas optimisés à l’aide de champs standard et personnalisés.<br>Fonctionnalités clés :<br><ul><li>Création plus rapide de schémas : générez des schémas directement à partir de fichiers de données d’exemple à l’aide de champs XDM générés et recommandés par ML.</li><li>Flexibilité de l’évolution des schémas : ajoutez ou mettez facilement à jour des champs dans le schéma généré.</li><li>Intégration transparente : intégration complète au flux de création de schéma de base dans l’IU des schémas, ce qui garantit une expérience client fluide et cohérente.</li><li>Révision et modification efficaces : affichez et mettez à jour rapidement votre schéma à l’aide de l’éditeur d’affichage plat, ce qui rend le processus de création plus efficace et convivial.</li></ul><br>Pour en savoir plus, consultez le [guide de processus de création de schémas assisté par ML](../../xdm/ui/ml-assisted-schema-creation.md). |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Platform, consultez la [présentation du système XDM](../../xdm/home.md).

## Service d’identités {#identity-service}

Utilisez le service d’identités d’Adobe Experience Platform pour créer une vue complète de votre clientèle et de ses comportements en reliant les identités entre les appareils et les systèmes, vous permettant ainsi de proposer des expériences numériques personnelles et percutantes en temps réel.

**Documentation mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Guide des configurations de graphiques | Lisez le [guide des configurations de graphiques](../../identity-service/identity-graph-linking-rules/example-configurations.md) pour plus d’informations sur les scénarios de graphiques courants que vous pouvez rencontrer lors de l’utilisation des règles de liaison de graphiques d’identité et des données d’identité. Le guide des configurations de graphiques fournit des exemples allant de scénarios graphiques simples à une seule personne à des scénarios graphiques à plusieurs personnes complexes et hiérarchiques. Vous pouvez également utiliser ce guide pour obtenir des exemples d’événements et de configurations d’algorithme que vous pouvez saisir dans l’[IU de simulation graphique](../../identity-service/identity-graph-linking-rules/graph-simulation.md), ainsi que des répartitions de la manière dont les identités principales sont sélectionnées selon certains scénarios de graphique. |

{style="table-layout:auto"}

Pour plus d’informations sur le service d’identités, consultez la [vue d’ensemble du service d’identités](../../identity-service/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] permet de segmenter en audiences les données stockées dans [!DNL Experience Platform] qui se rapportent aux personnes (tels que les clientes et clients, les prospects, les utilisateurs et utilisatrices ou les organisations). Vous pouvez créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur [!DNL Platform] et sont facilement accessibles à partir de n’importe quelle solution Adobe.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Détails d’ingestion | Pour les audiences dont l’origine de chargement est personnalisée, vous pouvez afficher les détails de l’ingestion de l’audience dans la page des détails de l’audience. De plus, vous pouvez appliquer des libellés aux attributs de payload en sélectionnant le schéma et les attributs souhaités pour la labellisation. Vous trouverez plus d’informations sur la section des détails de l’ingestion dans le [guide du portail d’audience](../../segmentation/ui/audience-portal.md#ingestion-details). |

{style="table-layout:auto"}

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

Utilisez les sources dans Experience Platform pour ingérer des données à partir d’une application Adobe ou d’une source de données tierce.

**Fonctionnalité mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mises à jour du connecteur source Adobe Analytics | La page de l’activité du jeu de données n’affiche pas d’informations sur les lots, car le connecteur source Analytics est entièrement géré par Adobe. Vous pouvez vérifier que les données circulent en examinant les mesures relatives aux enregistrements ingérés. Pour plus d’informations, consultez le guide sur la création d’une [connexion source pour les données Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

**Documentation mise à jour**

| Documentation mise à jour | Description |
| --- | --- |
| Enrichissement de la documentation sur la mise à jour des flux de données | Le guide sur la [mise à jour des flux de données sources existants dans l’interface d’utilisation](../../sources/tutorials/ui/update-dataflows.md) a été mis à jour afin de fournir plus d’informations sur les configurations que vous pouvez effectuer dans un flux de données existant. Le guide a également été mis à jour afin de clarifier le comportement attendu lorsqu’un flux de données désactivé est réactivé. |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des sources](../../sources/home.md).
