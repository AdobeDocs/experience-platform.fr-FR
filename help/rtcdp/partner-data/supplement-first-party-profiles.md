---
title: Complémenter les profils propriétaires avec des attributs fournis par les partenaires
description: Découvrez comment compléter les profils propriétaires avec des attributs de partenaires de données de confiance pour améliorer vos bases de données, obtenir de nouvelles informations sur votre base de clientes et de clients et optimiser l’audience.
feature: Use Cases, Profile Enrichment
exl-id: ee21b988-88f9-4c8e-bd82-7fc55c37ec24
source-git-commit: 7ee472294e8f255d9de3c15982a6f5d2d3654755
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 72%

---

# Complémenter les profils propriétaires avec des attributs fournis par le partenaire

>[!AVAILABILITY]
>
>* Cette fonctionnalité est disponible pour les clients qui disposent d’une licence Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Consultez la [description des produits](https://helpx.adobe.com/fr/legal/product-descriptions.html) pour en savoir plus sur ces packages et contactez votre représentant ou représentante Adobe pour obtenir plus d’informations.

Complétez les profils propriétaires avec les attributs des partenaires de données de confiance pour améliorer votre base de données, obtenir de nouvelles informations sur votre base de clientes et clients et optimiser l’audience.

![Enrichissez les profils avec des attributs fournis par les partenaires en utilisant le cas d’utilisation d’aperçu visuel de haut niveau.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-overview.png)

## Pourquoi envisager ce cas d’utilisation {#why-this-use-case}

La plupart des marques, même celles qui sont riches en données propriétaires, peuvent tirer parti d’une rationalisation de leurs données et d’une compréhension plus nuancée de leurs clients, de leurs comportements, modèles et préférences.

Adobe Real-time Customer Data Platform peut aider les marques à compléter de manière responsable leurs données propriétaires par des informations, des identifiants et des attributs précieux provenant d’un ou de plusieurs partenaires de confiance.

Adobe comprend qu’il n’existe pas d’approche unique et permet une interopérabilité transparente avec les partenaires de données et d’identité afin de favoriser un engagement personnalisé et réfléchi à toutes les étapes du cycle de vie du client. Ces fonctionnalités sont étayées par un cadre de gouvernance des données fiable, qui permet un contrôle nuancé sur le lieu et la manière dont les données des partenaires sont utilisées. Par exemple, vous pouvez vouloir utiliser les informations fournies par le partenaire pour la segmentation, mais pas pour la personnalisation.

Par exemple, suivez les étapes décrites dans ce cas d’utilisation lorsque vous devez enrichir les enregistrements de vos clients avec des signaux démographiques et d’intention.

## Prérequis et planification

Lorsque vous envisagez de compléter vos propres profils propriétaires avec des attributs des partenaires de données, vous devez discuter et traiter des détails suivants concernant la boucle d’enrichissement des données avec le partenaire de données :

* Pensez à l’emplacement où la liste d’audiences sera exportée à partir de Real-Time CDP, en vue du partage avec le fournisseur de données. Cet emplacement doit prendre en charge l’exportation de fichiers.
* Quels sont les identifiants attendus par le fournisseur de données pour qu’il puisse ajouter des attributs supplémentaires ?
* Comment le fichier contenant les attributs fournis par le partenaire sera-t-il réingéré dans Real-Time CDP ? Par exemple, les fichiers peuvent être ingérés par le biais des connecteurs source d’espaces de stockage tels qu’[Amazon S3](/help/sources/connectors/cloud-storage/s3.md) ou [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* Quelle est la cadence à laquelle vous prévoyez que les attributs fournis par les partenaires soient réintroduits dans Real-Time CDP et actualisés ?

>[!WARNING]
>
>Les attributs supplémentaires fournis par les partenaires ingérés dans Real-Time CDP ont un impact sur votre *volume total de données*. Lisez la Description du produit [Real-Time Customer Data Platform](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) pour plus d&#39;informations sur le volume total de données.

## Présentation vidéo {#video-walkthrough}

Regardez le tutoriel vidéo ci-dessous pour une présentation détaillée de la manière de compléter les audiences propriétaires par des attributs fournis par les partenaires :

>[!VIDEO](https://video.tv.adobe.com/v/3423075/?learn=on)

## Comment réaliser le cas d’utilisation : aperçu de haut niveau {#achieve-the-use-case-high-level}

![Enrichissez les profils avec des attributs fournis par les partenaires en utilisant un cas d’utilisation d’aperçu visuel de haut niveau.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-steps.png)

1. En tant que **client ou cliente**, vous obtenez les attributs sous licence du **partenaire de données**.
2. En tant que **client ou cliente**, vous étendez vos données de profil et votre modèle de gouvernance afin de prendre en compte les attributs fournis par le **partenaire**.
3. En tant que **client ou cliente**, vous intégrez les audiences que vous souhaitez enrichir avec le partenaire de données. En règle générale, ces audiences sont composées d’identifiants d’entrée comme des éléments d’informations d’identification personnelle (PII) tels que l’e-mail, le nom, l’adresse ou autres.
4. Le **partenaire** ajoute des attributs sous licence pour les profils avec lesquels il peut établir une correspondance. Si vous le souhaitez, un [Identifiant de partenaire](/help/identity-service/features/namespaces.md) peut être inclus et ingéré dans l’espace de noms de l’ID de portée du partenaire.
5. En tant que **client ou cliente**, vous chargez des attributs du partenaire de données dans les profils client de Real-Time CDP.

## Comment réaliser le cas d’utilisation : instructions détaillées {#step-by-step-instructions}

Parcourez les sections ci-dessous, qui contiennent des liens vers d’autres documents, pour suivre chacune des étapes de la vue d’ensemble de haut niveau ci-dessus.

### Attributs sous licence du partenaire {#license-attributes-from-partner}

Cette étape est décrite dans la section [conditions préalables](#prerequisites-and-planning). Adobe suppose que vous disposez des accords contractuels appropriés avec des fournisseurs de données de confiance pour enrichir vos profils propriétaires.

### Étendez vos données de profil et votre modèle de gouvernance pour prendre en compte les attributs fournis par les partenaires. {#extend-governance-model}

À ce stade, vous étendez votre structure de gestion des données dans Real-Time CDP pour prendre en compte les attributs fournis par les partenaires.

Vous avez la possibilité de créer un nouveau schéma de la classe **[!UICONTROL XDM Individual Profile]** ou d’étendre un schéma existant du même type afin d’inclure des attributs fournis par le partenaire. Adobe recommande vivement de créer un schéma avec un nouvel ensemble de groupes de champs qui représentent le mieux les attributs supplémentaires du fournisseur de données. Cela garantit que vos schémas de données sont propres et peuvent évoluer indépendamment les uns des autres.

Pour inclure des attributs fournis par un partenaire dans un schéma, vous pouvez créer un groupe de champs avec les attributs attendus ou utiliser l’un des groupes de champs préconfigurés fournis par Adobe.

Pour plus d’informations, consultez la documentation ci-dessous :

* [Principes de base de la composition des schémas](/help/xdm/schema/composition.md)
* [Présentation de la classe [!UICONTROL XDM Individual Profile]](/help/xdm/classes/individual-profile.md)
* [Créer et modifier les schémas dans l’interface utilisateur](/help/xdm/ui/resources/schemas.md)
* [Créer et modifier les groupes de champs de schéma dans l’interface utilisateur](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

Au cours de cette étape, réfléchissez également à la manière dont votre modèle de gouvernance des données change à mesure que vous développez votre politique de gestion des données pour inclure les données tierces fournies par le partenaire. Consultez les points à prendre en compte dans la documentation ci-dessous :

* (**Bientôt disponible**) Conservez les données tierces dans un jeu de données distinct afin de faciliter la suppression et l’annulation des intégrations.
* (**Bientôt disponible**) Utilisez la fonctionnalité [expiration du jeu de données](/help/hygiene/ui/dataset-expiration.md) du jeu de données pour les clientes et clients qui ont acheté le module complémentaire d’hygiène des données.
* (**Bientôt disponible**) Agissez avec prudence lors de la création de jeux de données dérivés qui contiennent des données tierces, car une fois intégrés, la seule façon de supprimer les données tierces consiste à supprimer l’ensemble du jeu de données dérivé.

>[!TIP]
>
>Si vous choisissez de compléter vos profils client avec un identifiant basé sur la personne du fournisseur de données, vous pouvez créer un nouveau type d’identité de type **[[!UICONTROL Partner ID]](/help/identity-service/features/namespaces.md)**.
>
>En savoir plus sur l’identifiant de partenaire dans la [section Types d’identité](/help/identity-service/features/namespaces.md).
>Découvrez [comment définir des champs d’identité](/help/xdm/ui/fields/identity.md) dans l’interface utilisateur d’Experience Platform.

### Exportez les audiences que vous souhaitez enrichir en saisissant des informations d’identification personnelles (PII) ou hachées {#export-audiences}

Exportez les audiences que le partenaire doit enrichir. Utilisez les destinations de stockage dans le cloud fournies par Real-Time CDP, telles qu’Amazon S3 ou SFTP. Consultez la documentation suivante pour terminer cette étape :

* Documentation de la [destination Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* Documentation de la [destination SFTP](/help/destinations/catalog/cloud-storage/sftp.md)
* Comment [se connecter à une destination](/help/destinations/ui/connect-destination.md)
* Comment [exporter des données vers une destination d’espace de stockage](/help/destinations/ui/activate-batch-profile-destinations.md)

### Votre partenaire de données ajoute des attributs sous licence pour les profils contre lesquels il peut établir une correspondance {#partner-appends-attributes}

Au cours de cette étape, votre partenaire de données ajoute des attributs sous licence pour l’audience exportée. La sortie est généralement disponible sous la forme d’un fichier plat qui peut être ingéré à nouveau dans Real-Time CDP. En savoir plus sur l’[ingestion de fichiers dans Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### Real-Time CDP ajoute des attributs enrichis dans le profil client {#ingest-data}

Vous devez désormais ingérer des données du partenaire par le biais d’un connecteur source pour réintroduire les données enrichies dans Real-Time CDP et compléter vos profils avec les données fournies par le partenaire.

Voici quelques connecteurs source recommandés à cette fin :

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## Limites et dépannage {#limitations-and-troubleshooting}

Notez que les limites suivantes s’appliquent lorsque vous utilisez le cas d’utilisation décrit sur cette page :

* Si vous choisissez d’utiliser des identifiants de partenaire, sachez que ceux-ci ne sont pas utilisés lors de la création de votre [graphique d’identité](/help/identity-service/features/identity-graph-viewer.md).

## Autres cas d’utilisation réalisés grâce à la prise en charge des données des partenaires {#other-use-cases}

Explorez d’autres cas d’utilisation activés grâce à la prise en charge des données des partenaires dans Real-Time CDP :

* Utilisez la prise en charge de données tierces dans Real-Time CDP pour [développer votre base de profils avec les profils de prospects des partenaires de données et interagissez avec eux pour acquérir ou atteindre une nouvelle clientèle](/help/rtcdp/partner-data/prospecting.md).
* [Personnalisez les expériences sur site pour les visiteurs inconnus à l’aide de la reconnaissance des visiteurs assistée par un partenaire](/help/rtcdp/partner-data/onsite-personalization.md) au cours de la visite sans que l’utilisateur ne s’authentifie ou n’ait d’historique avec votre marque.
* [Activation étendue des profils et des audiences de prospects](/help/destinations/ui/activate-prospect-audiences.md) pour sélectionner des destinations.
