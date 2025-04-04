---
title: Notes de mise à jour d’Adobe Experience Platform - Février 2022
description: Les notes de mise à jour de février 2022 pour Adobe Experience Platform.
exl-id: ae453f7d-ac75-4cc3-8435-57d25f086cc3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 92%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 7 mars 2022**

>[!NOTE]
>
>La publication a été décalée du 23 février au 7 mars.

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data collection]](#data-collection)
- [[!DNL Destinations]](#destinations)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform fournit de nombreux [!DNL dashboards] grâce auxquels vous pouvez afficher des informations importantes sur les données de votre entreprise, telles quʼelles sont capturées lors dʼinstantanés quotidiens.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouveaux widgets de destinations standard | Les widgets standard suivants vous permettent de visualiser différentes mesures liées à vos destinations.<ul><li>Segments récemment activés par destination. Ce widget affiche les cinq segments les plus récemment activés par ordre décroissant en fonction de la destination choisie.</li><li>Tendance de la taille de l’audience. Ce widget décrit l’évolution du nombre de profils sur une période donnée pour un segment qui a été mappé à ce compte de destination.</li><li>Segments non mappés par identité. Ce widget répertorie les cinq premiers segments non mappés classés par nombre d’identités décroissant pour une destination et une identité données.</li><li>Segments mappés par identité. Ce widget répertorie les cinq premiers segments mappés. Les segments sont classés de haut en bas en fonction de leur nombre respectif d’identifiants sources correspondant à l’identifiant de destination sélectionné dans le menu déroulant du widget.</li><li>Audiences courantes. Ce widget fournit une liste des cinq premiers segments activés sur le compte de destination choisi en haut de la page, ainsi que la destination sélectionnée dans la liste déroulante du widget.</li></ul> Pour plus d’informations sur les widgets standard disponibles, consultez la [documentation sur le tableau de bord des destinations](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/destinations.html#standard-widgets). |

Pour plus d’informations sur Query Service [!DNL Dashboards], consultez la [[!DNL Dashboards] présentation](../../dashboards/home.md) de Query Service.

## Collecte de données {#data-collection}

Experience Platform fournit un ensemble de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Workflow de l’interface utilisateur amélioré pour la configuration des flux de données | Le workflow de création d’un flux de données dans l’interface utilisateur de la collecte de données a été mis à jour. Lors de l’ajout de services à un flux de données, seuls les services auxquels vous avez accès seront inclus dans la liste des options. Pour plus d’informations, consultez le guide de [configuration dʼun flux de données](../../datastreams/overview.md). |
| Préparer des données pour la collecte de données | Si vous utilisez le SDK web Adobe Experience Platform, vous pouvez désormais réutiliser des fonctionnalités de préparation des données pour mapper vos données au modèle de données d’expérience (XDM) côté serveur. Pour plus d’informations, consultez la section [Préparer des données pour la collecte de données](../../datastreams/data-prep.md) dans le guide des flux de données. |
| Identifiants d’appareils propriétaires | Vous pouvez désormais envoyer vos propres identifiants d’appareil à Adobe Experience Platform Edge Network lors de la collecte de données client à l’aide d’Experience Platform Web SDK, ce qui permet de contourner les restrictions récentes imposées par les navigateurs sur la durée de vie des cookies tiers. Pour plus d’informations, consultez le guide des [Identifiants d’appareils propriétaires](../../web-sdk/identity/first-party-device-ids.md). |

Pour plus d’informations sur la collecte de données dans Experience Platform, consultez la [présentation de la collecte de données](../../collection/home.md).

## [!DNL Destinations] {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ----------- | ----------- |
| (Version bêta) Prise en charge par Destination SDK des destinations basées sur des fichiers  | La fonctionnalité [Prise en charge par Destination SDK des destinations basées sur des fichiers](../../destinations/destination-sdk/functionality/destination-server/server-specs.md) est actuellement en version bêta privée et n’est disponible que pour un certain nombre de partenaires et de clients. Les fonctionnalités et la documentation associée peuvent faire l’objet de modifications avant la mise à disposition d’une version générale.<br><br>Contactez votre représentant de compte Adobe pour découvrir comment accéder à la fonctionnalité. Les représentants du compte interne Adobe doivent contacter les équipes produit et ingénieur des destinations Experience Platform pour discuter des cas d’utilisation pris en charge. <br><br> Pendant la phase bêta de la prise en charge par Destination SDK des destinations basées sur des fichiers, les partenaires bêta et la clientèle peuvent utiliser [Destination SDK Experience Platform](../../destinations/destination-sdk/overview.md) pour créer des destinations privées afin de bénéficier des fonctionnalités suivantes : <ul><li>Créer une destination basée sur des fichiers (par lots) via Amazon S3, les serveurs SFTP, Azure Blob, Azure Data Lake Storage, le stockage des zones d’atterrissage des données.</li><li>Configurer et définir les options de planification et de fréquence d’exportation des fichiers par défaut.</li><li>Configurer et définir des options pour formater vos fichiers CSV exportés (délimiteurs, caractères d’échappement et autres options).</li><li>Possibilité de définir et de modifier des en-têtes de fichier personnalisés.</li><li>Possibilité de recevoir des notifications d’événement sur l’exportation de fichiers et de segments.</li><li>Possibilité d’exporter des types de fichiers supplémentaires tels que CSV, TSV, JSON, Parquet.</li></ul>  <br>Pour commencer à utiliser la nouvelle fonctionnalité, consultez la documentation [(Version bêta) Utilisation de Destination SDK pour configurer une destination basée sur des fichiers](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md). <br><br> La fonctionnalité de création de destinations de *diffusion en streaming* privées ou publiques à l’aide de Destination SDK est déjà disponible à l’ensemble de la clientèle et des partenaires d’Experience Platform. Pour en savoir plus, consultez le guide sur la façon d’[utiliser Destination SDK pour configurer une destination de diffusion en streaming](../../destinations/destination-sdk/guides/configure-destination-instructions.md). |

## [!DNL Identity Service] {#identity}

Proposer des expériences digitales pertinentes nécessite une compréhension complète de votre client. Cela devient plus difficile lorsque les données de vos clients sont fragmentées entre plusieurs systèmes, chaque client semble donc posséder plusieurs « identités ».

Adobe Experience Platform [!DNL Identity Service] vous permet de mieux connaître vos clients et leurs comportements, en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences digitales personnelles et percutantes en temps réel.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvelle autorisation pour `view-identity-graph` | Vous pouvez désormais utiliser l’autorisation `view-identity-graph` pour contrôler si les utilisateurs de votre entreprise peuvent afficher des données de graphique d’identités. Les utilisateurs ne disposant pas de cette autorisation ne pourront pas accéder à la visionneuse de graphiques d’identités dans l’interface utilisateur ou lors de l’accès aux API [!DNL Identity Service] qui renvoient des identités. Pour plus d’informations sur les autorisations, consultez la [Présentation du contrôle d’accès](../../access-control/home.md). |

Pour des informations plus générales sur le [!DNL Identity Service], reportez-vous à la [Présentation du service d’identités](../../identity-service/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Sources bêta passant à la version générale | Les sources suivantes ont été promues de la version bêta à la version générale : <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).