---
title: Notes de mise à jour d’Adobe Experience Platform
description: Les notes de mise à jour d’octobre 2023 pour Adobe Experience Platform.
exl-id: e9cf5299-8350-4b40-8f56-05e598846875
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 43%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 25 octobre 2023**

Mises à jour des fonctionnalités existantes dans Experience Platform :

- [Tableaux de bord](#dashboards)
- [Collecte de données](#data-collection)
- [Destinations](#destinations)
- [Sandbox](#sandboxes)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Tableaux de bord {#dashboards}

Adobe Experience Platform fournit de nombreux tableaux de bord grâce auxquels vous pouvez afficher des informations importantes sur les données de votre organisation, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mesures d’utilisation des destinations | De nouvelles mesures de mesure ont été ajoutées au tableau de bord de l’utilisation des licences. La variable **[!UICONTROL Taille de l’Audience Activation]** et **[!UICONTROL Taille de l’exportation des données]** Les mesures offrent un moyen pratique de suivre la quantité de données que vous avez exportées hors de Platform par rapport à vos droits d’utilisation de licence. Voir [mesures disponibles](../../dashboards/guides/license-usage.md#available-metrics) documentation pour obtenir des descriptions de ces mesures et d’autres mesures d’utilisation des licences. |

{style="table-layout:auto"}

Pour plus dʼinformations sur les tableaux de bord, notamment sur la manière dʼoctroyer des autorisations dʼaccès et de créer des widgets personnalisés, commencez par lire la [Présentation des tableaux de bord](../../dashboards/home.md).

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Type | Fonctionnalité | Description |
| --- | --- | --- |
| Extension | [!DNL Meta] Amélioration de l’API de conversion | Trois améliorations ont été apportées au [API des conversions de métadonnées](/help/tags/extensions/server/meta/overview.md) extension : <ul><li>Intégration avec [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): crée une expérience de connexion transparente en vous permettant de partager votre pixelID et votre jeton d’accès pour l’intégration de l’API Conversions avec Adobe.</li><li>Intégration avec [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): vous permet de diffuser de la publicité aux personnes qui sont plus susceptibles de terminer une action souhaitée et de lier l’action aux publicités diffusées.</li><li>Intégration avec [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): permet de transmettre l’RampID de LiveRamp dans le champ CIP, éliminant ainsi la nécessité de partager les informations d’identification personnelles directement avec des partenaires ou des métadonnées. </li></ul> |
| Extension | [!DNL LinkedIn] API de conversion | La variable [[!DNL LinkedIn] API de conversion](../../tags/extensions/server/linkedin/overview.md) vous permet d’évaluer l’efficacité de vos campagnes marketing LinkedIn en transférant des données d’événement Experience Platform à LinkedIn. |
| Secret | [!DNL LinkedIn] Secret OAuth 2 | La variable [[!DNL LinkedIn] Secret OAuth 2](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2) vous permet d’envoyer des interactions serveur-serveur à [!DNL LinkedIn] dans le transfert d’événement. |

Pour plus d’informations sur la collecte de données, consultez la [vue d’ensemble des collectes de données](../../tags/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#new-updated-destinations}

| Destination | Nouveau ou mis à jour | Description |
| ----------- |----------------|----------- |
| [[!DNL MoEngage]](/help/destinations/catalog/mobile-engagement/moengage.md) | Nouveau  | Utilisez la destination Mobile pour connecter et mapper vos données d’Adobe (attributs utilisateur, segments et événements) à MoEngage en temps réel. Les clients peuvent alors agir sur ces données, en proposant des expériences ciblées et personnalisées. |
| [[!DNL Qualtrics Automations]](/help/destinations/catalog/survey/qualtrics-automations.md) | Nouveau | Utilisez l’agrégation de plusieurs sources de données opérationnelles dans Adobe Experience Platform en tant qu’entrée dans Qualtrics Experience ID pour mieux comprendre vos clients et permettre une sensibilisation ciblée pour combler le fossé en matière de compréhension des facteurs d’intention, d’émotion et d’expérience. |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonction | Description |
| ----------- | ----------- |
| (Version bêta) Prise en charge des fonctions de hachage dans les champs calculés | En plus des fonctions spécifiques à [exportation de tableaux](../../destinations/ui/export-arrays-calculated-fields.md) ou des éléments d’un tableau, vous pouvez désormais utiliser des [fonctions de hachage](../../destinations/ui/export-arrays-calculated-fields.md#hashing-functions) pour hacher des attributs dans les fichiers exportés. Les fonctions de hachage prises en charge sont les suivantes : `sha`, `sha256`, `sha512`, `hash`, `md5`, `crc32`. |
| (disponibilité générale limitée) Activation des audiences de compte vers certaines destinations | Les clients Real-Time CDP B2B peuvent désormais activer [audiences de compte](../../segmentation/ui/account-audiences.md) vers certaines destinations. Pour plus d’informations sur cette fonctionnalité, veuillez lire la section [tutoriel sur l’activation des audiences de compte](/help/destinations/ui/activate-account-audiences.md). |

{style="table-layout:auto"}

**Correctifs et améliorations** {#destinations-fixes-and-enhancements}

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, Experience Platform fournit des environnements de test qui divisent une instance de Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

**Nouvelle fonctionnalité**

| Fonctionnalité | Description |
| --- | --- |
| Outils Sandbox | La fonctionnalité d’outil d’environnement de test vous permet d’améliorer la précision de la configuration dans les environnements de test et d’exporter et d’importer en toute transparence des configurations d’environnement de test entre les environnements de test. Vous pouvez utiliser la fonction d’outils des environnements de test pour sélectionner différents objets et les exporter dans un package. Pour plus d’informations, voir [guide de l’interface utilisateur de l’outil Sandbox](../../sandboxes/ui/sandbox-tooling.md). |

Pour plus d’informations sur les sandbox, consultez la [présentation des sandbox](../../sandboxes/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] permet de segmenter en audiences les données stockées dans [!DNL Experience Platform] qui se rapportent aux personnes (tels que les clientes et clients, les prospects, les utilisateurs et utilisatrices ou les organisations). Vous pouvez créer des audiences par le biais de définitions de segment ou d’autres sources à partir de vos données [!DNL Real-Time Customer Profile]. Ces audiences sont configurées et conservées de manière centralisée sur [!DNL Platform] et sont facilement accessibles à partir de n’importe quelle solution Adobe.

**Nouvelle fonctionnalité**

| Fonctionnalité | Description |
| ------- | ----------- |
| Audiences de compte (disponibilité générale limitée) | Dans l’édition B2B de Real-time Customer Data Platform, vous pouvez désormais utiliser la segmentation de compte pour offrir une expérience de segmentation marketing aisée et sophistiquée, depuis les audiences basées sur les personnes vers les audiences basées sur les comptes. Pour plus d’informations sur cette fonctionnalité, veuillez lire la section [présentation des audiences de compte](../../segmentation/ui/account-audiences.md). |

Pour en savoir plus sur Segmentation Service, consultez la [vue d’ensemble de Segmentation Service](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mise à jour de l’authentification pour la zone d’entrée des données | Vous pouvez désormais voir la date d’expiration désignée de votre zone d’entrée de données lors de l’affichage de vos informations d’identification. Vous devez actualiser votre jeton avant la date d’expiration afin de continuer à l’utiliser dans votre application. Si vous n’actualisez pas manuellement votre jeton avant la date d’expiration indiquée, celui-ci s’actualisera automatiquement et vous fournira un nouveau jeton la prochaine fois que vous récupérerez vos informations d’identification. Pour plus d’informations, consultez la documentation relative à [utilisation de la zone d’entrée des données](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Pour en savoir plus sur les sources, lisez la [vue d’ensemble des sources](../../sources/home.md).
