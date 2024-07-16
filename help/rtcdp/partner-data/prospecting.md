---
title: Interagir et acquérir de nouveaux clients sans dépendre de cookies tiers
description: Découvrez comment interagir et acquérir de nouveaux clientes et clients grâce à des cas d’utilisation de prospection, sans recourir à des cookies tiers.
feature: Use Cases, Customer Acquisition
exl-id: b9e7b3af-2a13-4904-bd12-e3ed05a1988e
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2074'
ht-degree: 85%

---

# Interagir et acquérir de nouveaux clients sans dépendre de cookies tiers

>[!AVAILABILITY]
>
>* Cette fonctionnalité est disponible pour les clients qui disposent d’une licence Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Consultez la [description des produits](https://helpx.adobe.com/fr/legal/product-descriptions.html) pour en savoir plus sur ces packages et contactez votre représentant ou représentante Adobe pour obtenir plus d’informations.

Utilisez la prise en charge de données tierces dans Real-Time CDP pour développer votre base de profils avec les profils de prospects des partenaires de données et interagissez avec eux pour acquérir ou atteindre une nouvelle clientèle.

![Vue d’ensemble détaillée du cas d’utilisation de la prospection de clientèle.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## Pourquoi tenir compte de ce cas pratique ? {#why-this-use-case}

Les marques font face simultanément à des défis intimidants liés à l’exécution responsable des cas d’utilisation d’acquisition client haut de gamme sans dépendance à l’égard des cookies tiers, à des budgets limités et à une demande plus élevée en matière de transparence et de retour sur dépenses publicitaires.

Adobe Real-Time Customer Data Platform peut aider les marques à passer en toute sécurité leurs cas d’utilisation pris en charge par la plateforme de gestion des données (DMP) à des solutions sans cookie et ce, d’une manière qui apporte toute la sophistication et la puissance de la segmentation en libre-service, du traitement de l’audience et de l’activation dans un seul système. Tout cela sans compromettre l&#39;insistance inébranlable de l&#39;Adobe sur une utilisation responsable des données via un cadre de gouvernance et de consentement des données breveté.

Par exemple, suivez les étapes décrites dans ce cas pratique lorsque vous devez exécuter une campagne pour attirer des prospects afin qu’ils deviennent des utilisateurs ou des clients connus.

## Prérequis et planification {#prerequisites-and-planning}

Lorsque vous envisagez de contacter et d’acquérir de nouveaux clients, tenez compte des conditions préalables suivantes dans votre processus de planification :

* Quelle est la cadence à laquelle vous prévoyez que les profils fournis par les partenaires soient introduits dans Real-Time CDP et actualisés ?
* Quelles sont les identités requises par vos destinations en aval ?
* Assurez-vous que les identifiants ingérés sont activables en aval
* Les données du partenaire que vous ingérez sont-elles liées à un identifiant durable largement accepté, tel que les informations d’identification personnelles, les informations d’identification personnelles hachées ou un identifiant de partenaire ?
* Quelles politiques d’utilisation des données devez-vous connaître du point de vue du partenaire et de votre propre équipe juridique, de confidentialité ou de conformité ?

## Comment réaliser le cas d’utilisation : vue d’ensemble de haut niveau {#achieve-the-use-case-high-level}

Avant de développer Real-Time CDP pour atteindre et acquérir une nouvelle clientèle, veillez à utiliser Real-Time CDP afin de créer une base solide pour vos données propriétaires. Les workflows permettant d’appliquer ce cas d’utilisation sont similaires aux workflows visant à atteindre votre clientèle existante.

![Vue d’ensemble détaillée du cas d’utilisation de la prospection de clientèle.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. En tant que **client ou cliente**, vous obtenez des profils de prospects d’un ou de plusieurs **partenaires de données** afin de favoriser l’acquisition de clientèle au sommet de l’entonnoir.
2. En tant que **client ou cliente**, vous étendez vos données de profil et votre modèle de gouvernance afin d’ingérer la liste des profils de prospects fournie par le **partenaire**.
3. En tant que **client ou cliente**, vous chargez des profils de prospects dans Real-Time CDP et créez des politiques de gouvernance garantissant une utilisation responsable.
4. En tant que **client ou cliente**, vous créez des audiences ciblées à partir de la liste des profils de prospects.
5. En tant que **client ou cliente**, vous activez les audiences de prospect vers des destinations qui acceptent les identités disponibles dans votre liste de prospects.
6. Si nécessaire, travaillez avec le **partenaire de données** pour l’activation des audiences vers les destinations de médias payants de votre choix sur le dernier kilomètre.

## Présentation vidéo {#video-walkthrough}

Consultez le tutoriel vidéo ci-dessous pour découvrir comment atteindre et interagir avec les audiences de prospects :

>[!VIDEO](https://video.tv.adobe.com/v/3423071/?learn=on)

## Comment réaliser le cas d’utilisation : instructions détaillées {#step-by-step-instructions}

Parcourez les sections ci-dessous, qui contiennent des liens vers d’autres documents, pour suivre chacune des étapes de la vue d’ensemble de haut niveau ci-dessus.

### Fonctionnalités et éléments de l’interface utilisateur que vous utiliserez {#ui-functionality-and-elements}

À mesure que vous réalisez les étapes de mise en œuvre du cas d’utilisation, vous utiliserez les fonctionnalités et éléments suivants de l’interface utilisateur de Real-Time CDP (répertoriés dans leur ordre d’utilisation). Assurez-vous de disposer des autorisations de contrôle d’accès en fonction des attributs nécessaires pour toutes ces zones ou demandez à votre administrateur ou administratrice système de vous accorder les autorisations nécessaires.

* [Identités](/help/identity-service/features/namespaces.md)
* [Schémas](/help/xdm/home.md)
* [Libellés d’utilisation des données](/help/data-governance/labels/overview.md)
* [Jeux de données](/help/catalog/datasets/overview.md)
* [Sources](/help/sources/home.md)
* [Profils de prospects](/help/profile/ui/prospect-profile.md)
* [Audiences de prospects](/help/segmentation/ui/prospect-audience.md)
* [Destinations](/help/destinations/home.md)

### Détails sous licence des profils tiers obtenus du partenaire {#license-profiles-from-partner}

Cette étape est décrite dans la section [Conditions préalables](#prerequisites-and-planning). Adobe suppose que vous disposez des accords contractuels appropriés avec des fournisseurs de données de confiance pour ingérer les profils de prospects fournis par le partenaire de données.

### Étendez vos données de profil et votre modèle de gouvernance pour prendre en compte les profils de prospects fournis par les partenaires {#extend-governance-model}

Pour vous préparer à recevoir des profils de prospects de votre partenaire de données, vous devez étendre votre cadre de gestion des données dans Real-Time CDP afin de prendre en compte ce nouveau type de profil.

Les composants d’identité, de gestion des données et de gouvernance que vous utiliserez sont les suivants :

* Un nouveau type d’identité **[!UICONTROL Identifiant de partenaire]** pour les profils fournis par le partenaire
* Une nouvelle classe **[!UICONTROL XDM Individual Prospect Profile]**
* **(Documentation à venir)** Des groupes de champs personnalisés pour la prise en charge des données des partenaires
* **(Documentation à venir)** Des libellés tiers que vous ajouterez aux attributs provenant des partenaires

#### Créer un espace de noms d’identité de l’ID du partenaire {#create-partner-id-namespace}

Commencez par créer un type d’identité pour les profils que vous recevrez du partenaire. Pour ce faire, dans la section Identité, créez un espace de noms d’identité du type **[!UICONTROL Identifiant de partenaire]**.

![Création d’un espace de noms d’identité Identifiant de partenaire.](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* En savoir plus sur l’identifiant de partenaire dans la [section Types d’identité](/help/identity-service/features/namespaces.md).
* Découvrez [comment définir des champs d’identité](/help/xdm/ui/fields/identity.md) dans l’interface utilisateur d’Experience Platform.

#### Créer un schéma avec la classe **[!UICONTROL XDM Individual Prospect Profile]**

Ensuite, dans **[!UICONTROL Gestion des données]** > **[!UICONTROL Schémas]**, créez un schéma et attribuez-lui la classe **[!UICONTROL XDM Individual Prospect Profile]**.

![Recherchez la classe XDM Individual Prospect Profile dans le créateur de schémas XDM.](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

Voici comment [créer et modifier des schémas dans l’interface utilisateur](/help/xdm/ui/resources/schemas.md) et obtenir des informations complètes sur la classe XDM Individual Prospect Profile (lien à venir).

La classe **[!UICONTROL XDM Individual Prospect Profile]** est préconfigurée avec les champs illustrés ci-dessous. Pour enrichir votre schéma avec des attributs fournis par le partenaire quant aux profils de prospects, vous pouvez soit créer un nouveau groupe de champs avec les attributs attendus et l’ajouter au schéma, soit utiliser l’un des groupes de champs préconfigurés fournis par Adobe.

![Champs préconfigurés pour la classe XDM Individual Prospect Profile.](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

Ensuite, vous devez sélectionner l’identité partnerID que vous avez créée précédemment comme identité principale du schéma. Les enregistrements de profil doivent comporter un identifiant principal. Cette étape est nécessaire pour s’assurer que les données de prospect peuvent être chargées dans la banque de profils et mises à disposition pour la segmentation et l’activation.

>[!AVAILABILITY]
>
>Les profils de prospects sont automatiquement limités pour utiliser uniquement les espaces de noms d’ID du type Identifiant de partenaire. Ce détail de conception garantit une séparation nette entre vos profils propriétaires et de prospect.

![Sélection de l’ID de partenaire configuré précédemment comme identité principale dans le schéma.](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

Notez que le schéma n’est pas encore activé pour le profil. Activez le bouton (bascule) Profil pour activer l’inclusion de ce schéma dans le service de profil. Pour plus d’informations sur l’activation du schéma à utiliser dans le profil client en temps réel, consultez le [tutoriel sur la création de schéma.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Activation d’un schéma pour le profil.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### Ajouter le libellé de gouvernance des données tierces à tous les champs du schéma

Envisagez d’ajouter des libellés de gouvernance des données tierces à tous les champs qui constituent le schéma. Vous garantissez ainsi une utilisation responsable de données tierces et minimisez le risque de fuite de données. Pour en savoir plus sur les [étiquettes de gouvernance des données tierces](../../data-governance/labels/reference.md#partner-ecosystem-labels).

Pour ce faire, procédez comme suit :

1. Accédez au schéma que vous avez créé et sélectionnez l’onglet **[!UICONTROL Libellés]**.
2. Sélectionnez tous les champs de ce schéma à l’aide de la case à cocher située tout en haut, puis cliquez sur l’icône en forme de crayon à droite pour appliquer des libellés de gouvernance des données à ce schéma.
3. Sélectionnez le libellé **[!UICONTROL Réseau partenaire]** dans les catégories sur la gauche.
4. Choisissez le libellé **[!UICONTROL Tiers]** et sélectionnez **[!UICONTROL Enregistrer]**.
5. Notez que tous les champs du schéma portent désormais le libellé que vous avez sélectionné à l’étape précédente.

>[!SUCCESS]
>
>Votre schéma est maintenant prêt à l’emploi et vous pouvez passer à l’étape suivante afin d’ingérer les données des prospects transmises par votre partenaire de données.

Au cours de cette étape, réfléchissez également à la manière dont votre modèle de gouvernance des données change à mesure que vous développez votre politique de gestion des données pour inclure les données tierces fournies par le partenaire. Consultez les points à prendre en compte dans la documentation ci-dessous :

* (**Bientôt disponible**) Conservez les données tierces dans un jeu de données distinct afin de faciliter la suppression et l’annulation des intégrations.
* (**Bientôt disponible**) Utilisez la fonctionnalité [expiration du jeu de données](/help/hygiene/ui/dataset-expiration.md) du jeu de données pour les clientes et clients qui ont acheté le module complémentaire d’hygiène des données.
* (**Bientôt disponible**) Agissez avec prudence lors de la création de jeux de données dérivés qui contiennent des données tierces, car une fois intégrés, la seule façon de supprimer les données tierces consiste à supprimer l’ensemble du jeu de données dérivé.

### Charger la liste des profils de prospects et inspecter la vue des profils de prospects

Après avoir préparé votre modèle de données pour la gestion des profils de prospects, vous pouvez y ingérer des données.

#### Créer un jeu de données et charger des données d’exemple de prospects

Pour charger des données d’exemple et remplir des profils de prospects, créez un jeu de données et chargez un fichier reçu du partenaire de données. Suivez les étapes ci-dessous :

1. Accédez à **[!UICONTROL Gestion des données]** > **[!UICONTROL Jeux de données]** et sélectionnez **[!UICONTROL Créer un jeu de données]**.
2. Sélectionnez Créer un jeu de données à partir d’un schéma
3. Sélectionner le schéma créé lors d’une étape précédente
4. Attribuez un nom à votre jeu de données et éventuellement une description.
5. Sélectionnez **[!UICONTROL Terminer]**.

![Enregistrement des étapes de création d’un jeu de données pour les profils de prospects.](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

Notez que, comme à l’étape de création d’un schéma, vous devez activer l’inclusion du jeu de données dans le profil client en temps réel. Pour plus d’informations sur l’activation du jeu de données à utiliser dans le profil client en temps réel, consultez le [tutoriel sur la création de schéma.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Activation d’un jeu de données pour le profil.](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

Pour charger un fichier que vous avez reçu du partenaire dans le jeu de données, sélectionnez le jeu de données, faites défiler la page vers le bas dans le rail de droite, puis sélectionnez **[!UICONTROL Ajouter des données]**. Vous pouvez faire glisser votre fichier ou sélectionner **[!UICONTROL Choisir des fichiers]** pour accéder à l’emplacement du fichier et le sélectionner.

![Ajout d’un fichier au jeu de données.](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

Après avoir chargé la liste des profils du partenaire de données dans Real-Time CDP, passez à la [section Inspecter les profils de prospects chargés](#inspect-profiles) pour vérifier que les profils de prospects sont renseignés dans l’interface utilisateur.

#### Ingérer des données de prospect via les connecteurs source

Vous pouvez configurer des imports de fichiers récurrents pour ingérer des données du partenaire par le biais d’un connecteur source et importer la liste des profils de prospects dans Real-Time CDP.

Certains connecteurs source recommandés à cet effet sont répertoriés ci-dessous, mais notez que toute méthode d’ingestion dans Real-Time CDP basée sur des fichiers peut ici convenir.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

Après avoir chargé la liste des profils du partenaire de données dans Real-Time CDP, passez à la section suivante pour vérifier que les profils de prospects sont renseignés dans l’interface utilisateur.

#### Inspecter les profils de prospects chargés {#inspect-profiles}

Pour afficher la liste des profils de prospects, accédez à **[!UICONTROL Prospects]** > **[!UICONTROL Profils]** dans le rail de gauche.

Notez que les profils de prospects que vous venez de charger dans Real-Time CDP peuvent prendre jusqu’à deux heures pour s’afficher dans la vue **[!UICONTROL Parcourir]** de l’écran Profil de prospects. Si la page affiche le message « Il n’y a pas de profil de prospect à parcourir pour le moment. », veuillez réessayer après un certain temps. Après un certain temps d’attente, les profils de prospects doivent commencer à s’afficher dans la vue **[!UICONTROL Parcourir]**.

>[!TIP]
>
>Notez la présence de la colonne **[!UICONTROL Espace de noms d’identité]**. Si vous travaillez avec plusieurs fournisseurs de données, utilisez cette colonne pour déduire l’origine des profils de prospects.

![Vue des profils de prospects chargés dans Real-Time CDP.](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

Vous pouvez également sélectionner n’importe quel profil de prospect pour une inspection ultérieure, comme illustré ci-dessous.

![Vue de la méthode d’inspection des profils de prospects.](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

En savoir plus sur les [profils de prospect](/help/profile/ui/prospect-profile.md).

### Créer des audiences de prospects {#create-prospect-audiences}

Utilisez la fonctionnalité de segmentation de Real-Time CDP pour créer des audiences à partir de vos profils de prospects. Utilisez les règles de segmentation souhaitées pour créer des audiences personnalisées.

Pour commencer et créer des audiences composées de profils de prospects, accédez à **[!UICONTROL Prospects]** > **[!UICONTROL Audiences]**.

![Vue des audiences de prospects.](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

Notez que l’expérience de création d’audiences pour les profils de prospects diffère de l’expérience de création d’audiences à partir de votre clientèle propriétaire existante. Cette vue est limitée par les éléments suivants :

* Attributs de la classe Prospect que vous avez créée précédemment.
* Évaluation de profil par lots uniquement.
* Pas de prise en charge de la création d’audiences basées sur des événements de série temporelle.

En savoir plus sur les [audiences prospect](/help/segmentation/ui/prospect-audience.md).

### Activer les profils de prospects vers des destinations {#activate-to-destinations}

Utilisez les audiences de prospects en les exportant vers des destinations. Actuellement, seules certaines destinations de stockage dans le cloud prennent en charge l’activation des profils de prospect.

![Destinations qui prennent en charge les audiences de prospects.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

[En savoir plus](/help/destinations/ui/activate-prospect-audiences.md) sur l’activation des prospects vers les destinations de stockage dans le cloud.

## Autres cas d’utilisation réalisés grâce à la prise en charge des données des partenaires {#other-use-cases}

Explorez d’autres cas d’utilisation activés grâce à la prise en charge des données des partenaires dans Real-Time CDP :

* [Complétez les profils propriétaires avec les attributs des partenaires de données de confiance pour améliorer votre base de données, obtenir de nouvelles informations sur votre base de clientèle et optimiser l’audience.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* [Personnalisez des expériences sur site pour des visiteurs inconnus à l’aide de la reconnaissance de visiteurs avec l’aide d’un partenaire](/help/rtcdp/partner-data/onsite-personalization.md) pendant la visite sans que l’utilisateur s’authentifie ou n’ait un historique antérieur avec votre marque.
* [Activation étendue des profils de prospects et des audiences de prospects](/help/destinations/ui/activate-prospect-audiences.md) pour sélectionner des destinations.
