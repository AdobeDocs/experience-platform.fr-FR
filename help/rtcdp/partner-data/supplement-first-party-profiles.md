---
title: (Version bêta) Complémentation de profils propriétaires avec des attributs fournis par le partenaire
description: Découvrez comment compléter les profils propriétaires avec des attributs de partenaires de données de confiance pour améliorer vos bases de données, obtenir de nouvelles informations sur votre base de clients et optimiser l’audience.
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: 019ebe0c1cf11a7fb30dced1e10b511bab9b5100
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 0%

---

# Complémentation de profils propriétaires avec des attributs fournis par le partenaire

>[!AVAILABILITY]
>
>* Cette fonctionnalité bêta est disponible pour les clients qui disposent d’une licence Real-Time CDP (App Service), Adobe Experience Platform Activation, la plateforme de données clients en temps réel, Real-Time CDP Prime, Real-Time CDP Ultimate. Pour en savoir plus sur ces packages, voir [description des produits](https://helpx.adobe.com/legal/product-descriptions.html) et contactez votre représentant d’Adobe pour plus d’informations.

Complétez les profils propriétaires avec les attributs des partenaires de données de confiance afin d’améliorer votre base de données et d’obtenir de nouvelles informations sur votre base de clients et d’optimiser l’audience.

![Enrichissez les profils avec des attributs fournis par les partenaires en utilisant un cas d’utilisation d’aperçu visuel de haut niveau.](/help/rtcdp/assets/partner-data/enrichment-use-case-overview.png)

## Prérequis et planification {#prerequisites-and-planning}

Lorsque vous envisagez de compléter vos propres profils propriétaires avec des attributs des partenaires de données, vous devez discuter et traiter les détails suivants sur la boucle d’enrichissement des données avec le partenaire de données :

* Pensez à l’emplacement où la liste d’audiences sera exportée hors de Real-Time CDP, pour être partagée avec le fournisseur de données. Cet emplacement doit prendre en charge l’exportation de fichiers.
* Quels sont les identifiants attendus par le fournisseur de données pour qu’il puisse effectuer une couche sur des attributs supplémentaires ?
* Comment le fichier contenant les attributs fournis par le partenaire sera-t-il ingéré à nouveau dans la plateforme de données clients en temps réel ? Par exemple, les fichiers peuvent être ingérés par le biais des connecteurs source de stockage dans le cloud tels que [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) ou [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* Quelle est la cadence à laquelle vous prévoyez que les attributs fournis par les partenaires soient réintroduits dans Real-Time CDP et actualisés ?

>[!WARNING]
>
>Les attributs supplémentaires fournis par le partenaire ingérés dans Real-Time CDP ont un impact sur votre *richesse moyenne du profil*. Lisez le [Description du produit Real-time Customer Data Platform](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) pour plus d’informations sur la richesse du profil.

## Comment réaliser le cas d’utilisation : présentation de haut niveau {#achieve-the-use-case-high-level}

![Enrichissez les profils avec des attributs fournis par les partenaires en utilisant un cas d’utilisation d’aperçu visuel de haut niveau.](/help/rtcdp/assets/partner-data/enrichment-use-case-steps.png)

1. Comme **client**, vous autorisez les attributs à partir de la variable **partenaire de données**.
2. Comme **client**, vous étendez vos données de profil et votre modèle de gouvernance pour les adapter **partenaire** Attributs fournis par .
3. Comme **client**, vous intégrez les audiences que vous souhaitez enrichir avec le partenaire de données. En règle générale, ces audiences sont composées d’identifiants d’entrée comme des éléments d’informations d’identification personnelle (PII) tels que l’adresse électronique, le nom, l’adresse ou d’autres.
4. Le **partenaire** ajoute des attributs sous licence pour les profils avec lesquels ils peuvent établir une correspondance. Si vous le souhaitez, une [Identifiant du partenaire](/help/identity-service/namespaces.md) peut être inclus et ingéré dans l’espace de noms de l’ID de portée du partenaire.
5. Comme **client**, vous chargez des attributs du partenaire de données dans les profils client de Real-Time CDP.

## Comment réaliser le cas d’utilisation : Instructions détaillées {#step-by-step-instructions}

Lisez les sections ci-dessous, qui contiennent des liens vers d’autres documents, pour suivre chacune des étapes de la présentation de haut niveau ci-dessus.

### Attributs de licence du partenaire {#license-attributes-from-partner}

Cette étape est décrite dans la section [conditions préalables](#prerequisites-and-planning) et Adobe suppose que vous avez mis en place les accords contractuels appropriés avec des fournisseurs de données de confiance pour augmenter vos profils propriétaires.

### Étendez vos données de profil et votre modèle de gouvernance pour prendre en compte les attributs fournis par les partenaires. {#extend-governance-model}

À ce stade, vous étendez votre structure de gestion des données dans Real-Time CDP pour prendre en compte les attributs fournis par les partenaires.

Vous avez la possibilité de créer un nouveau schéma du **[!UICONTROL XDM Individual Profile]** ou étendre un schéma existant du même type pour inclure des attributs fournis par le partenaire. Adobe recommande vivement de créer un nouveau schéma avec un nouvel ensemble de groupes de champs qui représentent le mieux les attributs supplémentaires du fournisseur de données. Cela garantit que vos schémas de données sont propres et peuvent évoluer indépendamment les uns des autres.

Pour inclure des attributs fournis par un partenaire dans un schéma, vous pouvez soit créer un groupe de champs avec les attributs attendus, soit utiliser l’un des groupes de champs préconfigurés fournis par Adobe.

Pour plus d’informations, consultez les pages de documentation ci-dessous :

* [Principes de base de la composition des schémas](/help/xdm/schema/composition.md)
* [Présentation de la variable [!UICONTROL XDM Individual Profile] class](/help/xdm/classes/individual-profile.md)
* [Création et modification de schémas dans l’interface utilisateur](/help/xdm/ui/resources/schemas.md)
* [Création et modification de groupes de champs de schéma dans l’interface utilisateur](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

Au cours de cette étape également, réfléchissez à la manière dont votre modèle de gouvernance des données change à mesure que vous développez votre stratégie de gestion des données pour inclure les données tierces fournies par le partenaire. Consultez les points à prendre en compte dans les liens de documentation ci-dessous :

* (**Bientôt disponible**) Conserver les données tierces dans un jeu de données distinct afin de faciliter la suppression et l’annulation des intégrations.
* (**Bientôt disponible**) Utilisez la variable [expiration du jeu de données](/help/hygiene/ui/dataset-expiration.md) fonctionnalité du jeu de données pour les clients qui ont acheté le module complémentaire d’hygiène des données.
* (**Bientôt disponible**) Soyez prudent lors de la création de jeux de données dérivés qui extraient des données tierces, car une fois mélangés, la seule solution pour supprimer les données tierces consiste à supprimer l’ensemble du jeu de données dérivé.

>[!TIP]
>
>Si vous choisissez de compléter vos profils client avec un identifiant basé sur la personne du fournisseur de données, vous pouvez créer un nouveau type d’identité du type . **[[!UICONTROL Identifiant du partenaire]](/help/identity-service/namespaces.md)**.
>
>En savoir plus sur l’identifiant de partenaire dans la section [section types d’identité](/help/identity-service/namespaces.md).
>En savoir plus [comment définir des champs d’identité](/help/xdm/ui/fields/identity.md) dans l’interface utilisateur de l’Experience Platform.

### Exporter les audiences que vous souhaitez enrichir en saisissant des informations d’identification personnelles (PII) ou des informations d’identification hachées {#export-audiences}

Exportez les audiences que le partenaire doit enrichir. Utilisez les destinations de stockage dans le cloud fournies par la plateforme de données clients en temps réel, telles qu’Amazon S3 ou SFTP. Lisez les pages de documentation suivantes pour terminer cette étape :

* [Destination Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) page de documentation
* [Destination SFTP](/help/destinations/catalog/cloud-storage/sftp.md) page de documentation
* Comment [se connecter à une destination](/help/destinations/ui/connect-destination.md)
* Comment [exporter des données vers une destination de stockage dans le cloud](/help/destinations/ui/activate-batch-profile-destinations.md)

### Votre partenaire de données ajoute des attributs sous licence pour les profils contre lesquels il peut établir une correspondance. {#partner-appends-attributes}

Au cours de cette étape, votre partenaire de données ajoute des attributs sous licence pour l’audience exportée. La sortie est généralement disponible sous la forme d’un fichier plat qui peut être ingéré à nouveau dans Real-Time CDP. En savoir plus sur [ingestion de fichiers dans Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### Real-Time CDP ajoute des attributs enrichis dans le profil du client {#ingest-data}

Vous devez désormais ingérer des données du partenaire par le biais d’un connecteur source pour réintroduire les données enrichies dans Real-Time CDP et compléter vos profils avec les données fournies par le partenaire.

Voici quelques connecteurs source recommandés à cet effet :

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## Limites et dépannage {#limitations-and-troubleshooting}

Notez les limites suivantes lorsque vous explorez le cas d’utilisation décrit sur cette page :

* Si vous choisissez d’utiliser des identifiants de partenaire, sachez que ces identifiants ne sont pas utilisés lors de la création de votre [graphique d’identités](/help/identity-service/ui/identity-graph-viewer.md).

## Autres cas d’utilisation réalisés grâce à la prise en charge des données des partenaires {#other-use-cases}

Explorez d’autres cas d’utilisation activés grâce à la prise en charge des données des partenaires dans Real-Time CDP :

* (**Bientôt disponible**) [!BADGE Beta]{type=Informative}**Utiliser la reconnaissance assistée par le partenaire** pour personnaliser les expériences sur site au cours de la visite et pour recibler une visite de publication hors site, sans que l’utilisateur s’authentifie ou n’ait jamais eu d’historique avec votre marque.
* (**Bientôt disponible**) [!BADGE Beta]{type=Informative}**Activation étendue** l’utilisation d’identifiants de partenaire pour publier des écosystèmes qui n’acceptent pas les informations d’identification personnelle ou les informations d’identification personnelles hachées.