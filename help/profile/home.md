---
title: Vue d’ensemble du profil client en temps réel
description: Le profil client en temps réel fusionne des données provenant de diverses sources et permet d’accéder à ces données sous la forme de profils clients individuels et d’événements de séries temporelles associés. Cette fonctionnalité permet aux spécialistes marketing d’offrir à leur audience des expériences coordonnées, cohérentes et pertinentes sur plusieurs canaux.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 99%

---

# Présentation du [!DNL Real-Time Customer Profile]

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le [!DNL Real-Time Customer Profile] offre une vision holistique de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le [!DNL Profile] vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client. Cette présentation vous aidera à comprendre le rôle et l’utilisation du [!DNL Real-Time Customer Profile] dans [!DNL Experience Platform].

## Le [!DNL Profile] dans Experience Platform

La relation entre le profil client en temps réel et les autres services dans Experience Platform est mise en évidence dans le schéma suivant :

![La relation entre le profil client en temps réel et les autres services d’Adobe Experience Platform. Ce diagramme montre que Profil est l’un des principaux composants d’Adobe Experience Platform.](images/profile-overview/profile-in-platform.png)

## Présentation des profils

Le [!DNL Real-Time Customer Profile] fusionne les données de divers systèmes d’entreprise, puis fournit un accès à ces données sous la forme de profils client avec des événements de série temporelle associés. Cette fonctionnalité permet aux spécialistes marketing d’offrir à leur audience des expériences coordonnées, cohérentes et pertinentes sur plusieurs canaux. Les sections suivantes mettent en avant certains concepts de base que vous devez connaître afin de créer et de gérer efficacement des profils au sein de Platform.

### Composition de l’entité de profil

Un profil client en temps réel est composé d’une entité principale, appelée l’**entité principale**, et de diverses entités annexes. Dans le contexte d’Experience Platform, l’entité principale est généralement une **entité de profil**, qui est composée des caractéristiques, des comportements et des appartenances à une audience d’une personne individuelle. D’autres entités permettent au moteur de segmentation d’utiliser des données en dehors de l’entité principale du profil, et incluent les éléments suivants :

- **Entité dimensionnelle** : l’entité utilisée pour simplifier le processus de modélisation des données pour les informations partagées entre les événements ou les enregistrements de profil. On parle également d’entité de recherche ou d’entité de classification.
- **Entité B2B** : entités qui décrivent la relation du profil avec les comptes et opportunités business-to-business.

![Un diagramme expliquant la composition de l’entité de profil.](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>Étant donné que les entités dimensionnelles et B2B n’existent qu’en dehors de l’entité principale, elles sont uniquement utilisées pour la segmentation par lots.

Les entités dimensionnelles et B2B sont liées à l’entité principale par le biais de **relations de schéma**. Pour plus d’informations, reportez-vous à la documentation suivante :

- [Créer une relation de schéma un-à-un pour les entités de recherche](../xdm/tutorials/relationship-ui.md)
- [Créer une relation de schéma plusieurs-à-un pour les entités B2B](../xdm/tutorials/relationship-b2b.md)

### Banque de données de profil

Bien que le [!DNL Real-Time Customer Profile] traite les données ingérées et utilise Adobe Experience Platform [!DNL Identity Service] pour fusionner les données associées par le biais du mappage d’identité, il conserve ses propres données dans le magasin de données du [!DNL Profile]. Le magasin du [!DNL Profile] est distinct des données du catalogue qui se trouvent dans le lac de données et des données du [!DNL Identity Service] qui se trouvent dans le graphique d’identités.

Le magasin du profil utilise une infrastructure de base de données Microsoft Azure Cosmos et le lac de données de Platform utilise l’espace de stockage Microsoft Azure Data Lake.

### Mécanismes de sécurisation de profil

Experience Platform propose une série de mécanismes de sécurisation pour vous permettre d’éviter de créer des [schémas de modèle de données d’expérience (XDM)](../xdm/home.md) qui ne peuvent pas être pris en charge par le profil client en temps réel. Cela inclut des limites souples qui entraîneront une dégradation des performances, ainsi que des limites strictes qui entraîneront des erreurs et des pannes système. Pour plus d’informations, dont une liste de directives et des cas d’utilisation, consultez la documentation sur les [Mécanismes de sécurisation de profil](guardrails.md).

### Tableau de bord du profil {#profile-dashboard}

L’interface utilisateur d’Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur vos données de profil client en temps réel. Celles-ci sont présentées telles qu’elles sont capturées lors d’instantanés quotidiens. Pour découvrir comment accéder au tableau de bord du [!DNL Profile] et savoir comment l’utiliser dans l’interface utilisateur, ainsi que pour obtenir des informations détaillées sur les mesures affichées dans le tableau de bord, reportez-vous au [Guide de l’interface utilisateur du tableau de bord du profil](ui/profile-dashboard.md).

### Fragments de profil contre profils fusionnés {#profile-fragments-vs-merged-profiles}

Chaque profil client est composé de plusieurs fragments de profil qui ont été fusionnés dans le but de former une vue unique pour ce client. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre organisation dispose de plusieurs fragments de profil associés à ce client unique apparaissant dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans Platform, ils sont fusionnés afin de créer un profil unique pour ce client.

En d’autres termes, les fragments de profil représentent une identité principale unique et les données [enregistrement](#record-data) ou [événement](#time-series-events) correspondantes pour cet identifiant au sein d’un jeu de données spécifique.

Lorsque les données provenant de plusieurs jeux de données entrent en conflit (par exemple, si un fragment classe le client comme étant « célibataire » tandis qu’un autre le classe comme étant « marié »), la [politique de fusion](#merge-policies) détermine quelles informations doivent être prioritaires et être incluses dans le profil de l’individu. Par conséquent, il est probable que le nombre total de fragments de profil au sein de Platform soit toujours supérieur au nombre total de profils fusionnés, chaque profil étant composé de fragments multiples issus de multiples jeux de données.

### Données d’enregistrement {#record-data}

Un profil est la représentation d’un sujet, d’une organisation ou d’un individu. Il est composé de nombreux attributs également appelés données d’enregistrement. Par exemple, le profil d’un produit peut inclure un SKU et une description, tandis que le profil d’une personne contient des informations telles que le prénom, le nom et l’adresse e-mail. [!DNL Experience Platform] vous permet de personnaliser les profils afin d’utiliser des données spécifiques pertinentes pour votre entreprise. La classe standard du [!DNL Experience Data Model] (XDM), [!DNL XDM Individual Profile], est la classe privilégiée à partir de laquelle créer un schéma lors de la description des données d’enregistrement des clients. Elle fournit les données intégrées à de nombreuses interactions entre les services Platform. Pour plus d’informations sur l’utilisation des schémas dans [!DNL Experience Platform], consultez tout d’abord la [présentation du système XDM](../xdm/home.md).

### Événements de série temporelle {#time-series-events}

Les données de série temporelle fournissent un instantané du système au moment où une action a été entreprise, directement ou indirectement, par un objet, ainsi que des données détaillant l’événement lui-même. Représentées par la classe de schéma standard XDM ExperienceEvent, les données de série temporelle peuvent décrire des événements tels que l’ajout d’articles à un panier, l’utilisation de liens et la lecture de vidéos. Vous pouvez utiliser les données de série temporelle pour établir des règles de segmentation et consulter les événements individuellement dans le cadre d’un profil.

### Identités

Toutes les entreprises souhaitent s’adresser à leurs clients de manière personnalisée. Cependant, l’un des défis que représente la proposition d’expériences digitales pertinentes aux clients consiste à trouver un moyen de relier leurs données déconnectées. Celles-ci sont souvent réparties sur différents canaux numériques tels que les tablettes, les téléphones mobiles et les ordinateurs portables. Le [!DNL Identity Service] vous permet de rassembler l’image complète de votre client en liant les identités de plusieurs canaux et en créant un graphique d’identités pour chaque client. Consultez la [présentation du service d’identités](../identity-service/home.md) pour en savoir plus.

### Politiques de fusion

Lorsque vous rassemblez des fragments de données provenant de plusieurs sources et les combinez pour obtenir une vue complète de chaque client, les politiques de fusion sont les règles utilisées par [!DNL Platform] pour déterminer quelle est la priorité des données et quelles données seront combinées pour créer le profil client.

En cas de conflit de données provenant de plusieurs jeux de données, la politique de fusion détermine comment ces données doivent être traitées et quelle valeur doit être utilisée. À lʼaide dʼAPI RESTful ou de lʼinterface utilisateur, vous pouvez créer des politiques de fusion, gérer des politiques existantes et définir une politique de fusion par défaut pour votre organisation.

Pour en savoir plus sur les politiques de fusion et leur rôle dans Experience Platform, commencez par lire la [présentation des politiques de fusion](merge-policies/overview.md).

### Schémas d’union {#profile-fragments-and-union-schemas}

L’une des fonctionnalités clés du [!DNL Real-Time Customer Profile] est la possibilité d’unifier les données multicanales. Lorsque vous utilisez le [!DNL Real-Time Customer Profile] pour accéder à une entité, vous pouvez obtenir un affichage fusionné de tous les fragments de profil de cette entité dans les jeux de données, appelé « vue d’union » et obtenu grâce au schéma d’union.

Pour en savoir plus sur les schémas d’union, notamment sur la façon d’y accéder dans l’interface utilisateur, consultez le [guide de l’interface utilisateur des schémas d’union](ui/union-schema.md).

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## Profils et audiences

Le [!DNL Segmentation Service] d’Adobe Experience Platform fournit les audiences nécessaires à l’optimisation de l’expérience de chaque client et cliente. Lorsqu’une audience est créée, l’identifiant de cette audience est ajouté à la liste d’appartenance à l’audience pour tous les profils éligibles. Les règles de segmentation sont créées et appliquées aux données du [!DNL Real-Time Customer Profile] à l’aide des API RESTful et de l’interface utilisateur du créateur de segments. Pour en savoir plus sur la segmentation, commencez pas lire la [Présentation de Segmentation Service](../segmentation/home.md).

### Ingestion par flux et segmentation par flux

L’entrée en temps réel est possible grâce à un processus appelé ingestion par flux. À mesure que les données de profil et de série temporelle sont ingérées, le [!DNL Real-Time Customer Profile] décide automatiquement d’inclure ou d’exclure ces données des audiences par le biais d’un processus continu appelé la segmentation par flux, avant de les fusionner avec les données existantes et de mettre à jour la vue d’union. Par conséquent, vous pouvez instantanément effectuer des calculs et prendre des décisions pour offrir aux clients de meilleures expériences personnalisées lorsqu’ils interagissent avec votre marque. Lors de l’ingestion, les données sont également soumises à un processus de validation pour s’assurer qu’elles sont correctement ingérées et conformes au schéma sur lequel le jeu de données est basé. Pour plus d’informations sur la validation effectuée lors de l’ingestion, commencez par lire la [présentation de la qualité d’ingestion des données](../ingestion/quality/overview.md).

## Ingestion de données dans le [!DNL Profile]

Vous pouvez configurer [!DNL Platform] pour envoyer les données d’enregistrement et de série temporelle au [!DNL Profile]. Cela est compatible avec l’ingestion par lots et l’ingestion par flux en temps réel. Pour plus d’informations, consultez le tutoriel décrivant comment [ajouter des données au profil client en temps réel](tutorials/add-profile-data.md).

>[!NOTE]
>
>Les données collectées par l’intermédiaire des solutions Adobe, notamment [!DNL Analytics Cloud], [!DNL Marketing Cloud] et [!DNL Advertising Cloud], débordent dans [!DNL Experience Platform] et sont ingérées dans le [!DNL Profile].

### Mesures d’ingestion de profil

Observability Insights vous permet d’afficher les mesures clés dans Adobe Experience Platform. Outre les statistiques d’utilisation relatives à [!DNL Experience Platform] et les indicateurs de performances pour diverses fonctionnalités de [!DNL Platform], des mesures spécifiques liées au profil vous permettent d’obtenir des informations sur les taux de requêtes entrantes, les taux d’ingestion réussie, les tailles d’enregistrements ingérés, etc. Pour en savoir plus, consultez tout d’abord la [présentation de l’API Observability Insights](../observability/api/overview.md) et pour obtenir une liste complète des mesures du profil client en temps réel, consultez la documentation sur les [mesures disponibles](../observability/api/metrics.md#available-metrics).

## Mise à jour des données de magasin de profils

Il peut parfois être nécessaire de mettre à jour les données dans la banque de profils de votre entreprise. Vous pouvez par exemple avoir besoin de corriger des enregistrements ou de modifier une valeur d’attribut. Cette opération peut être effectuée par ingestion par lot et nécessite un jeu de données compatible avec les profils et configuré avec une balise upsert. Pour plus d’informations sur la façon de configurer un jeu de données pour les mises à jour d’attributs, veuillez vous référer au tutoriel concernant l’[activation d’un jeu de données pour Profile et upsert](../catalog/datasets/enable-upsert.md).

## Gouvernance des données et [!DNL Privacy]

La gouvernance des données est constituée d’une série de politiques et de technologies permettant de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données.

En ce qui concerne l’accès aux données, la gouvernance des données joue un rôle essentiel dans [!DNL Experience Platform], et ce, à différents niveaux :

- Application de libellés d’utilisation des données
- Politiques d’accès aux données
- Contrôle de l’accès aux données pour les actions marketing

La gouvernance des données est gérée sur plusieurs points. Il s’agit notamment de choisir les données à ingérer dans [!DNL Platform] et celles qui seront accessibles après l’ingestion pour une action marketing donnée. Pour plus d’informations, commencez par lire la [présentation de la gouvernance des données](../data-governance/home.md).

### Gestion des demandes d’exclusion et de confidentialité des données

[!DNL Experience Platform] permet à vos clients d’envoyer des demandes de désinscription associées à l’utilisation et au stockage de leurs données dans le [!DNL Real-Time Customer Profile]. Pour plus d’informations sur la gestion des demandes d’exclusion, consultez la documentation sur le [respect des demandes d’exclusion](../segmentation/consents.md).

## Étapes suivantes et ressources supplémentaires

Pour en savoir plus sur l’utilisation des données du profil client en temps réel à l’aide de l’interface utilisateur d’Experience Platform ou de l’API Profile, commencez par consulter respectivement le [guide de l’interface utilisateur Profil](ui/user-guide.md) ou le [guide de développement de l’API](api/overview.md).
