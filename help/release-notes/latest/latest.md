---
title: Notes de mise à jour d’Adobe Experience Platform
description: Dernières notes de mise à jour pour Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: e9d5f24bec8cd2793ce30245b46c1d912bf17cc7
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 37%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 25 août 2021**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Destinations](#destinations)
- [Observability Insights](#observability)
- [Profil client en temps réel](#profile)
- [Sources](#sources)

## Destinations {#destinations}

Les destinations sont des intégrations préconfigurées à des plateformes de destination qui permettent dʼactiver facilement des données provenant dʼAdobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations**

| Destination | Description |
| ----------- | ----------- |
| [[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md) | La destination Attributs des appareils, qui était auparavant en version bêta, est désormais disponible en général. |
| [[!DNL Airship Tags]](../../destinations/catalog/mobile-engagement/airship-tags.md) | La destination Balises aériennes, qui était auparavant en version bêta, est désormais disponible en général. |
| [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | La destination de braze, précédemment en version bêta, est désormais disponible en général. |
| [[!DNL Pinterest Customer List]](../../destinations/catalog/advertising/pinterest.md) | Avec la destination de liste de clients Pinterest, vous pouvez créer des audiences à partir de vos listes de clients, des personnes qui ont visité votre site ou des personnes qui ont déjà interagi avec votre contenu sur Pinterest. |
| [[!DNL Twitter Custom Audiences]](../../destinations/catalog/social/twitter.md) | Ciblez vos abonnés et clients existants dans Twitter et créez des campagnes de remarketing pertinentes en activant vos audiences créées dans Adobe Experience Platform. |
| [[!DNL Verizon Media/Yahoo DataX]](../../destinations/catalog/advertising/datax.md) | DataX est une infrastructure Verizon Media/Yahoo agrégée qui héberge divers composants qui permettent à Verizon Media/Yahoo d’échanger des données avec ses partenaires externes de manière sécurisée, automatisée et évolutive. |

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| [[!DNL Destination SDK]](../../destinations/destination-sdk/overview.md) | Le SDK de destination Adobe Experience Platform est une suite d’API de configuration qui vous permet de configurer des modèles d’intégration de destination pour que l’Experience Platform puisse fournir des données d’audience et de profil à votre point de terminaison, en fonction des données et des formats d’authentification de votre choix. Les configurations sont stockées dans Experience Platform et peuvent être récupérées via l’API pour des mises à jour supplémentaires. |
| [Améliorations de l’utilisation des destinations](../../destinations/ui/activation-overview.md) | Les améliorations de l’utilisation des destinations permettent aux marketeurs d’activer facilement des segments vers des destinations existantes. |

Pour des informations plus générales sur les destinations, reportez-vous à la [présentation des destinations](../../destinations/home.md).

## Observability Insights {#observability}

Observability Insights vous permet de surveiller les activités de Platform à l’aide de mesures statistiques et de notifications d’événement.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Alertes | Vous pouvez désormais vous abonner à des alertes importantes liées aux workflows exécutés sur Platform. Après vous être abonné à des règles d’alerte spécifiques, vous recevrez des notifications et des e-mails dans l’interface utilisateur lorsqu’un événement de cycle de vie important se produit (par exemple, une ingestion de données réussie) ou si des problèmes nécessitent votre attention (par exemple, un échec du flux d’ingestion ou une tâche de segmentation qui prend plus de temps que prévu). Pour plus d’informations, consultez la [présentation des alertes](../../observability/alerts/overview.md). |

Pour plus d’informations sur le service, consultez la [présentation d’Observability Insights](../../observability/home.md) .

## Real-time Customer Profile {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Real-time Customer Profile offre une vue d’ensemble de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Profile vous permet de consolider les données client dans une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

| Fonctionnalité | Description |
| ------- | ----------- |
| Parcourir les profils par stratégie ou identité de fusion | Lors de l’exploration des profils dans Experience Platform, vous pouvez désormais naviguer par stratégie de fusion pour prévisualiser 20 profils d’exemple en fonction de la stratégie de fusion sélectionnée. Vous pouvez également naviguer par identité afin de rechercher un profil spécifique à l’aide d’un espace de noms d’identité et d’une valeur d’identité associée. Pour plus d’informations, consultez le [guide de l’interface utilisateur de Real-time Customer Profile](../../profile/ui/user-guide.md). |

Pour en savoir plus sur Real-time Customer Profile, y compris des tutoriels et des bonnes pratiques concernant l’utilisation des données de profil, commencez par lire la [présentation de Real-time Customer Profile](../../profile/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| ------- | ----------- |
| Connecteur source de chargement de fichier local | La catégorie d’ingestion de fichiers a été renommée système local, ce qui vous permet d’importer directement des fichiers locaux dans Platform à l’aide du connecteur de téléchargement de fichiers local. Les données ingérées par ce connecteur peuvent être surveillées via le tableau de bord de surveillance. Pour plus d’informations, consultez la [présentation de la source de chargement de fichier locale](../../sources/connectors/local-system/local-file-upload.md) . |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
