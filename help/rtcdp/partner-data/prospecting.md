---
title: (Version bêta) Interagir et acquérir de nouveaux clients au moyen de cas d’utilisation de prospection
description: Découvrez comment interagir et acquérir de nouveaux clients grâce à des cas d’utilisation de prospection, activés par le support des données des partenaires dans Real-Time CDP.
hide: true
hidefromtoc: true
badgeBeta: label="Version Beta" type="informative" before-title="true"
source-git-commit: 2e2a473efd247cb235ee7e8f94058baa48fd1b1a
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 16%

---

# Interagir et acquérir de nouveaux clients au moyen de cas d’utilisation de prospection

>[!AVAILABILITY]
>
>* Cette fonctionnalité Beta est disponible pour les clientes et clients qui disposent d’une licence Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-time CDP, Real-Time CDP Prime et Real-Time CDP Ultimate. Consultez la [description des produits](https://helpx.adobe.com/fr/legal/product-descriptions.html) pour en savoir plus sur ces packages et contactez votre représentant ou représentante Adobe pour obtenir plus d’informations.

Utilisez la prise en charge de données tierces dans Real-Time CDP pour développer votre base de profils avec les profils de prospect des partenaires de données et interagissez avec eux pour acquérir ou atteindre de nouveaux clients.

![Présentation visuelle de haut niveau du cas d’utilisation de la prospection client.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## Prérequis et planification {#prerequisites-and-planning}

Lorsque vous envisagez de contacter et d’acquérir de nouveaux clients en utilisant la prise en charge des données des partenaires dans Real-Time CDP, tenez compte des conditions préalables suivantes dans votre processus de planification :

* Quel est le rythme auquel vous prévoyez que les profils fournis par les partenaires soient ingérés et actualisés dans Real-Time CDP ?
* Quelles identités ont besoin vos destinations en aval ?
* Assurez-vous que les identifiants ingérés sont activables en aval
* Les données du partenaire que vous ingérez sont-elles liées à un identifiant durable largement accepté, tel que les informations d’identification personnelles, les informations d’identification personnelles hachées ou un identifiant de partenaire ?
* Quelles politiques d’utilisation des données devez-vous connaître du point de vue du partenaire et de votre propre équipe juridique, de confidentialité ou de conformité ?

## Comment réaliser le cas d’utilisation : aperçu de haut niveau {#achieve-the-use-case-high-level}

Avant de développer Real-Time CDP pour engager et acquérir de nouveaux clients, veillez à utiliser Real-Time CDP pour créer une base solide pour vos données de première partie. Les workflows pour réaliser ce cas d’utilisation sont similaires aux workflows pour interagir avec vos clients connus.

![Présentation visuelle de haut niveau du cas d’utilisation de la prospection client.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. Comme **client**, vous disposez d’une licence pour les profils de prospect d’un ou de plusieurs **partenaires de données** pour vous aider à tirer le meilleur parti de l’acquisition client de l’entonnoir.
2. Comme **client**, vous étendez vos données de profil et votre modèle de gouvernance pour ingérer la variable **partenaire** Liste fournie des profils de prospect.
3. Comme **client**, vous chargez des profils de prospect dans Real-Time CDP et créez des stratégies de gouvernance pour garantir une utilisation responsable.
4. Comme **client**, vous créez des audiences ciblées à partir de la liste des profils de prospect.
5. Comme **client**, vous activez les audiences de prospects vers les destinations qui acceptent les identités disponibles dans votre liste de prospects.
6. Si nécessaire, travaillez avec la fonction **partenaire de données** pour l’activation du dernier kilomètre des audiences vers les destinations de médias payants souhaitées.

## Comment réaliser le cas d’utilisation : instructions détaillées {#step-by-step-instructions}

Parcourez les sections ci-dessous, qui contiennent des liens vers d’autres documents, pour suivre chacune des étapes de la vue d’ensemble de haut niveau ci-dessus.

### Fonctionnalités et éléments de l’interface utilisateur que vous utiliserez {#ui-functionality-and-elements}

À mesure que vous réalisez les étapes de mise en oeuvre du cas d’utilisation, vous utiliserez les fonctionnalités et éléments d’interface utilisateur de Real-Time CDP suivants (répertoriés dans l’ordre dans lequel vous les utiliserez). Assurez-vous de disposer des autorisations de contrôle d’accès en fonction des attributs nécessaires pour toutes ces zones ou demandez à votre administrateur système de vous accorder les autorisations nécessaires.

* [Identités](/help/identity-service/namespaces.md)
* [Schémas](/help/xdm/home.md)
* [Libellés d’utilisation des données](/help/data-governance/labels/overview.md)
* [Jeux de données](/help/catalog/datasets/overview.md)
* [Sources](/help/sources/home.md)
* Profils (lien vers les profils de prospect)
* Audiences (lien vers les audiences prospects)
* [Destinations](/help/destinations/home.md)

### Obtention d’une licence pour les détails du profil tiers du partenaire {#license-profiles-from-partner}

Cette étape est décrite dans la section [conditions préalables](#prerequisites-and-planning) et Adobe suppose que vous avez mis en place les accords contractuels appropriés avec les fournisseurs de données de confiance pour ingérer les profils de prospect fournis par le partenaire de données.

### Étendre vos données de profil et votre modèle de gouvernance pour adapter les profils de prospect fournis par les partenaires {#extend-governance-model}

Pour vous préparer à recevoir des profils de prospect de votre partenaire de données, vous devez étendre votre structure de gestion des données dans Real-Time CDP afin de tenir compte de ce nouveau type de profil.

Les composants d’identité, de gestion des données et de gouvernance que vous utiliserez sont les suivants :

* Une nouvelle **[!UICONTROL Identifiant du partenaire]** type d’identité des profils fournis par le partenaire
* Une nouvelle **[!UICONTROL Profil XDM Individual Prospect]** Classe XDM
* **(Documentation à venir)** Groupes de champs personnalisés pour la prise en charge des données des partenaires
* **(Documentation à venir)** Étiquettes tierces que vous ajouterez aux attributs provenant des partenaires

#### Création d’un espace de noms d’identité Identifiant de partenaire {#create-partner-id-namespace}

Commencez par créer un nouveau type d’identité pour les profils que vous recevrez du partenaire. Pour ce faire, dans la section Identité , vous devez créer un espace de noms d’identité du type **[!UICONTROL Identifiant du partenaire]**.

![Créez un espace de noms d’identité du Partner ID.](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* En savoir plus sur les espaces de noms des identifiants de partenaire dans la section [section types d’identité](/help/identity-service/namespaces.md).
* Découvrez [comment définir des champs d’identité](/help/xdm/ui/fields/identity.md) dans l’interface utilisateur d’Experience Platform.

#### Créez un nouveau schéma avec le **[!UICONTROL Profil XDM Individual Prospect]** class

Ensuite, dans **[!UICONTROL Data Management]** > **[!UICONTROL Schémas]**, créez un nouveau schéma et attribuez-lui le **[!UICONTROL Profil XDM Individual Prospect]** classe .

![Recherchez la classe XDM Individual Prospect Profile dans le créateur de schémas XDM.](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

Lire comment [création et modification de schémas dans l’interface utilisateur](/help/xdm/ui/resources/schemas.md) et obtenir des informations complètes sur la classe XDM Individual Prospect Profile (lien à venir).

La variable **[!UICONTROL Profil XDM Individual Prospect]** est préconfigurée avec les champs illustrés ci-dessous. Pour enrichir votre schéma avec des attributs fournis par le partenaire pour les profils de prospect, vous pouvez soit créer un nouveau groupe de champs avec les attributs attendus et l’ajouter au schéma, soit utiliser l’un des groupes de champs préconfigurés fournis par Adobe.

![Champs préconfigurés pour la classe XDM Individual Prospect Profile.](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

Ensuite, vous devez sélectionner l’identité partnerID que vous avez créée précédemment comme identité Principale pour le schéma. Les enregistrements de profil doivent comporter un identifiant Principal. Cette étape est nécessaire pour s’assurer que les données de prospect peuvent être chargées dans l’entrepôt de profils et mises à disposition pour la segmentation et l’activation.

>[!AVAILABILITY]
>
>Les profils potentiels sont automatiquement limités pour utiliser uniquement les espaces de noms d’ID du type Identifiant de partenaire. Cela s’effectue par conception et garantit une séparation nette entre vos profils propriétaires et prospects.

![Sélectionnez l’identifiant de partenaire configuré précédemment comme identité Principale dans le schéma.](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

Notez que le schéma n’est pas encore activé pour profile. Activez le bouton Profil pour activer l’inclusion de ce schéma dans le service de profil. Pour plus d’informations sur l’activation du schéma à utiliser dans Real-Time Customer Profile, consultez la section [tutoriel sur la création de schéma.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Activer un schéma pour le profil.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### Ajout de l’étiquette de gouvernance des données tierces à tous les champs du schéma

Envisagez d’ajouter des étiquettes de gouvernance des données tierces à tous les champs qui constituent le schéma. Ceci est important pour garantir une utilisation responsable de données tierces et minimiser le risque de fuite de données. En savoir plus sur les étiquettes de gouvernance des données tierces (ajout d’un lien vers des documents par la Jordanie)

Pour ce faire, procédez comme suit :

1. Accédez au schéma que vous avez créé et sélectionnez le **[!UICONTROL Étiquettes]** .
2. Sélectionnez tous les champs de ce schéma à l’aide de la case à cocher située tout en haut, puis cliquez sur l’icône en forme de crayon à droite pour appliquer des libellés de gouvernance des données à ce schéma.
3. Sélectionnez la variable **[!UICONTROL Écosystème partenaire]** Libellé des catégories sur la gauche.
4. Choisissez le libellé appelé **[!UICONTROL Troisième niveau]** et sélectionnez **[!UICONTROL Enregistrer]**.
5. Notez que tous les champs du schéma portent désormais le libellé que vous avez sélectionné à l’étape précédente.

>[!SUCCESS]
>
>Votre schéma est maintenant prêt à l’emploi et vous pouvez passer à l’étape suivante pour ingérer les données de prospect de votre partenaire de données.

Au cours de cette étape, réfléchissez également à la manière dont votre modèle de gouvernance des données change à mesure que vous développez votre politique de gestion des données pour inclure les données tierces fournies par le partenaire. Consultez les points à prendre en compte dans la documentation ci-dessous :

* (**Bientôt disponible**) Conservez les données tierces dans un jeu de données distinct afin de faciliter la suppression et l’annulation des intégrations.
* (**Bientôt disponible**) Utilisez la fonctionnalité [expiration du jeu de données](/help/hygiene/ui/dataset-expiration.md) du jeu de données pour les clientes et clients qui ont acheté le module complémentaire d’hygiène des données.
* (**Bientôt disponible**) Agissez avec prudence lors de la création de jeux de données dérivés qui contiennent des données tierces, car une fois intégrés, la seule façon de supprimer les données tierces consiste à supprimer l’ensemble du jeu de données dérivé.

### Charger la liste des profils de prospects et examiner la vue des profils de prospects

Une fois votre modèle de données préparé pour la gestion des profils de prospect, il est temps d’ingérer des données.

#### Création d’un jeu de données et chargement d’exemples de données de prospects

Pour charger des exemples de données et remplir des profils de prospect, créez un jeu de données et chargez un fichier que vous avez reçu du partenaire de données. Procédez comme suit :

1. Accédez à **[!UICONTROL Data Management]** > **[!UICONTROL Jeux de données]** et sélectionnez **[!UICONTROL Création d’un jeu de données]**.
2. Sélectionnez Créer un jeu de données à partir d&#39;un schéma
3. Sélectionner le schéma que vous avez créé lors d’une étape précédente
4. Attribuez un nom à votre jeu de données et éventuellement une description.
5. Sélectionnez **[!UICONTROL Terminer]**.

![Enregistrement des étapes de création d’un jeu de données pour les profils de prospect.](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

Notez que, comme à l’étape de création d’un schéma, vous devez activer l’inclusion du jeu de données dans le profil client en temps réel. Pour plus d’informations sur l’activation du jeu de données à utiliser dans Real-Time Customer Profile, consultez la section [tutoriel sur la création de schéma.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Activez le jeu de données pour le profil.](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

Pour charger un fichier que vous avez reçu du partenaire dans le jeu de données, sélectionnez le jeu de données, faites défiler la page vers le bas dans le rail de droite, puis sélectionnez **[!UICONTROL Ajouter des données]**. Vous pouvez faire glisser votre fichier ou sélectionner **[!UICONTROL Sélection de fichiers]** pour accéder à l’emplacement du fichier et le sélectionner.

![Ajoutez un fichier au jeu de données.](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

Après avoir chargé la liste des profils du partenaire de données dans Real-Time CDP, passez à la [Inspect de la section Profils de prospect chargés](#inspect-profiles) pour vérifier que les profils de prospect sont renseignés dans l’interface utilisateur.

#### Ingestion de données de prospect via les connecteurs source

Vous pouvez configurer des imports de fichiers récurrents pour ingérer des données du partenaire par le biais d&#39;un connecteur source et importer la liste des profils de prospect dans Real-Time CDP.

Certains connecteurs source recommandés à cet effet sont répertoriés ci-dessous, mais notez que toute méthode d’ingestion basée sur des fichiers dans Real-Time CDP fonctionne à votre place.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

Après avoir chargé la liste des profils du partenaire de données dans Real-Time CDP, passez à la section suivante pour vérifier que les profils de prospect sont renseignés dans l’interface utilisateur.

#### Inspect des profils de prospect chargés {#inspect-profiles}

Pour afficher la liste des profils de prospect, accédez à **[!UICONTROL Perspectives]** > **[!UICONTROL Profils]** dans le rail de gauche.

Notez que les profils de prospect que vous venez de charger dans Real-Time CDP peuvent prendre jusqu’à deux heures pour s’afficher dans la variable **[!UICONTROL Parcourir]** vue de l’écran Profil de projet. Si la page affiche le message &quot;Il n’y a aucun profil de prospect à parcourir en ce moment&quot;, veuillez réessayer après un certain temps. Après un certain temps d’attente, les profils de prospect doivent commencer à apparaître dans la variable **[!UICONTROL Parcourir]** vue.

>[!TIP]
>
>Notez la présence de la variable **[!UICONTROL Identity Namespace]** colonne . Si vous travaillez avec plusieurs fournisseurs de données, utilisez cette colonne pour déduire l’origine des profils de prospect.

![Vue des profils de prospect chargés dans Real-Time CDP.](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

Vous pouvez également sélectionner n’importe quel profil de prospect pour une inspection ultérieure, comme illustré ci-dessous.

![Vue de la manière d’inspecter les profils de prospect.](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

(**Bientôt disponible**) En savoir plus sur les profils de prospect.

### Créer des audiences de prospects {#create-prospect-audiences}

Utilisez la fonctionnalité de segmentation de Real-Time CDP pour créer des audiences à partir de vos profils de prospect. Utilisez les règles de segmentation souhaitées pour créer des audiences personnalisées.

Pour commencer et créer des audiences composées de profils de prospect, accédez à **[!UICONTROL Perspectives]** > **[!UICONTROL Audiences]**.

![Vue des audiences de prospects.](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

Notez que l’expérience de création d’audiences pour les profils de prospect diffère de l’expérience de création d’audiences à partir de vos clients propriétaires connus. Cette vue est limitée à :

* Attributs de la classe prospect que vous avez créée précédemment.
* Évaluation de profil par lots uniquement.
* Ne prend pas en charge la création d’audiences basées sur des événements de série temporelle.

(**Bientôt disponible**) En savoir plus sur les audiences de prospects.

### Activation des profils de prospect vers des destinations {#activate-to-destinations}

Utilisez les audiences de prospects en les exportant vers des destinations. Actuellement, seules certaines destinations, telles que [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) ou le [!BADGE Alpha]{type=Informative}[LiveRamp](/help/destinations/catalog/advertising/liveramp-onboarding.md) l’activation de la prise en charge des destinations pour les profils de prospect.

## Autres cas d’utilisation réalisés grâce à la prise en charge des données des partenaires {#other-use-cases}

Explorez d’autres cas d’utilisation activés grâce à la prise en charge des données des partenaires dans Real-Time CDP :

* [!BADGE Version bêta]{type=Informative}[Complétez les profils propriétaires avec les attributs des partenaires de données de confiance pour améliorer votre base de données, obtenir de nouvelles informations sur votre base de clientes et clients et optimiser l’audience.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* (**Bientôt disponible**) [!BADGE Beta]{type=Informative}**Utilisez la reconnaissance assistée par le partenaire** pour personnaliser les expériences sur site au cours de la visite et pour le reciblage hors site après une visite, sans que l’utilisateur ou l’utilisatrice s’authentifie ou ait déjà interagi avec votre marque.