---
title: Notes de mise à jour d’Adobe Experience Platform - Août 2021
description: Les notes de mise à jour d’août 2021 pour Adobe Experience Platform.
doc-type: release notes
last-update: August 25, 2021
author: ens28527
exl-id: 0513b9dc-b16c-43b3-8e17-4be4499308d4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 87%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 25 août 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Destinations](#destinations)
- [Observability Insights](#observability)
- [Profil client en temps réel](#profile)
- [Sources](#sources)

## Destinations {#destinations}

Les destinations sont des intégrations préconfigurées à des plateformes de destination qui permettent dʼactiver facilement des données provenant dʼAdobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations**

| Destination | Description |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | La destination Attributs Airship, auparavant en version Beta, est désormais disponible pour tous. |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | La destination Balises Airship, auparavant en version Beta, est désormais disponible pour tous. |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | La destination Braze, auparavant en version Beta, est désormais disponible pour tous. |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | Grâce à la destination Liste de clients Pinterest, vous pouvez créer des audiences à partir de vos listes de clients, des personnes qui ont visité votre site ou des personnes qui ont déjà interagi avec votre contenu sur Pinterest. |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | Ciblez vos abonnés et clients existants sur Twitter et créez des campagnes de remarketing pertinentes en activant vos audiences créées dans Adobe Experience Platform. |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX, une infrastructure globale appartenant à Verizon Media/Yahoo, permet dʼhéberger différents composants et dʼéchanger des données avec les partenaires externes de Verizon Media/Yahoo, de manière sécurisée, automatisée et évolutive. |

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Le SDK Destination Adobe Experience Platform est un ensemble dʼAPI de configuration permettant de configurer des modèles dʼintégration de destination, afin quʼExperience Platform puisse envoyer des données dʼaudience et de profil à votre point dʼentrée, selon les formats de données et dʼauthentification choisis. Les configurations sont stockées dans Experience Platform et peuvent être récupérées via lʼAPI pour des mises à jour supplémentaires. |
| [Améliorations de lʼutilisation des destinations](../../destinations/ui/activation-overview.md) | Les améliorations apportées aux destinations afin de faciliter leur utilisation permettent aux spécialistes du marketing dʼactiver facilement des segments vers des destinations existantes. |

Pour des informations plus générales sur les destinations, reportez-vous à la [présentation des destinations](../../destinations/home.md).

## Observability Insights {#observability}

Observability Insights vous permet de surveiller les activités d’Experience Platform à l’aide de mesures statistiques et de notifications d’événement.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Alertes | Vous pouvez désormais vous abonner à des alertes importantes liées aux workflows s’exécutant sur Experience Platform. Après vous être abonné à des règles dʼalerte spécifiques, vous recevrez des notifications et des e-mails dans lʼinterface utilisateur dès quʼun événement de cycle de vie important se produit (par exemple, une ingestion de données réussie) ou si des problèmes nécessitent votre attention (par exemple, un échec du flux dʼingestion ou une tâche de segmentation qui prend plus de temps que prévu). Pour plus dʼinformations, voir la [présentation des alertes](../../observability/alerts/overview.md). |

Pour plus dʼinformations sur ce service, voir la [présentation dʼObservability Insights](../../observability/home.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le profil client en temps réel offre une vue holistique de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le Profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Parcourir les profils par politique de fusion ou identité | Lors de lʼexploration des profils dans Experience Platform, vous pouvez désormais naviguer par politique de fusion pour prévisualiser 20 profils dʼexemple en fonction de la politique de fusion sélectionnée. Vous pouvez également naviguer par identité afin de rechercher un profil spécifique à lʼaide dʼun espace de noms dʼidentité et dʼune valeur dʼidentité associée. Pour plus d’informations, consultez le [Guide de l’interface utilisateur du profil client en temps réel](../../profile/ui/user-guide.md). |

Pour en savoir plus sur le profil client en temps réel, notamment les bonnes pratiques et les tutoriels relatifs à lʼutilisation des données de profil, consultez la [vue d’ensemble de Real-Time Customer Profile](../../profile/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| ------- | ----------- |
| Connecteur source de téléchargement de fichiers locaux | La catégorie d’ingestion de fichiers a été renommée en système local, ce qui vous permet d’importer directement des fichiers locaux dans Experience Platform à l’aide du connecteur local de téléchargement de fichiers. Les données ingérées par ce connecteur peuvent être visualisées dans le tableau de bord de surveillance. Pour plus dʼinformations, consultez la [présentation de la source de téléchargement de fichiers locaux](../../sources/connectors/local-system/local-file-upload.md). |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
