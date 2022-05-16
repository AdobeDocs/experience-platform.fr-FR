---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;profil unifié;Profil unifié;unifié;Profil;rtcp;graphiques XDM
title: Présentation du profil client en temps réel
topic-legacy: guide
description: Real-time Customer Profile fusionne des données provenant de diverses sources et permet d’accéder à ces données sous la forme de profils clients individuels et d’événements de séries temporelles associés. Cette fonctionnalité permet aux spécialistes marketing d’offrir à leur audience des expériences coordonnées, cohérentes et pertinentes sur plusieurs canaux.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: d2182b48e21de059f12ad8923bb3b420ed87bcfc
workflow-type: tm+mt
source-wordcount: '2046'
ht-degree: 92%

---

# Présentation du [!DNL Real-time Customer Profile]

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le [!DNL Real-time Customer Profile] offre une vision holistique de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le [!DNL Profile] vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client. Cette présentation vous aidera à comprendre le rôle et l’utilisation du [!DNL Real-time Customer Profile] dans [!DNL Experience Platform].

## Le [!DNL Profile] dans Experience Platform

La relation entre Real-time Customer Profile et les autres services dans Experience Platform est mise en évidence dans le schéma suivant :

![La relation entre Real-time Customer Profile et les autres services dans Adobe Experience Platform. Ce diagramme montre que Profile est l’un des composants principaux de Adobe Experience Platform.](images/profile-overview/profile-in-platform.png)

## Présentation des profils

Le [!DNL Real-time Customer Profile] fusionne les données de divers systèmes d’entreprise, puis fournit un accès à ces données sous la forme de profils client avec des événements de série temporelle associés. Cette fonctionnalité permet aux spécialistes marketing d’offrir à leur audience des expériences coordonnées, cohérentes et pertinentes sur plusieurs canaux. Les sections suivantes mettent en avant certains concepts de base que vous devez connaître afin de créer et de gérer efficacement des profils au sein de Platform.

### Composition de l’entité de profil

Un profil client en temps réel est composé d’une entité principale, appelée **Principale entité**, et diverses entités annexes. L’entité Principale est composée des caractéristiques, des comportements et des appartenances aux segments d’un profil. D’autres entités permettent au moteur de segmentation d’utiliser des données en dehors de l’entité Principale du profil, et incluent les éléments suivants :

- **Entité dimensionnelle**: L’entité utilisée pour simplifier le processus de modélisation des données pour les informations partagées entre les événements ou les enregistrements de profil. On parle également d’entité de recherche ou d’entité de classification.
- **Entité B2B**: Entités qui décrivent la relation du profil avec les comptes et opportunités d’entreprise à entreprise.

![Diagramme expliquant la composition de l’entité de profil.](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>Comme les entités dimensionnelles et B2B n’existent qu’en dehors de l’entité Principale, elles ne sont utilisées que pour la segmentation par lots.

### Banque de données de profil

Bien que le [!DNL Real-time Customer Profile] traite les données ingérées et utilise Adobe Experience Platform [!DNL Identity Service] pour fusionner les données associées par le biais du mappage d’identité, il conserve ses propres données dans le magasin de données du [!DNL Profile]. Le magasin du [!DNL Profile] est distinct des données du catalogue qui se trouvent dans le lac de données et des données du [!DNL Identity Service] qui se trouvent dans le graphique d’identités.

Le magasin du profil utilise une infrastructure de base de données Microsoft Azure Cosmos et le lac de données de Platform utilise l’espace de stockage Microsoft Azure Data Lake.

### Garde-fous de profil

Experience Platform propose une série de garde-fous pour vous aider à éviter de créer des [schémas de modèle de données d’expérience (XDM)](../xdm/home.md) qui ne peuvent pas être pris en charge par le profil client en temps réel. Cela inclut des limites souples qui entraîneront une dégradation des performances, ainsi que des limites strictes qui entraîneront des erreurs et des pannes système. Pour plus d’informations, dont une liste de directives et des cas d’utilisation, consultez la documentation sur les [Garde-fous de profil](guardrails.md).

### Tableau de bord du profil {#profile-dashboard}

L’interface utilisateur d’Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur vos données de profil client en temps réel. Celles-ci sont présentées telles qu’elles sont capturées lors d’un aperçu quotidien. Pour découvrir comment accéder au tableau de bord du [!DNL Profile] et savoir comment l’utiliser dans l’interface utilisateur, ainsi que pour obtenir des informations détaillées sur les mesures affichées dans le tableau de bord, reportez-vous au [Guide de l’interface utilisateur du tableau de bord du profil](ui/profile-dashboard.md).

### Fragments de profil contre profils fusionnés {#profile-fragments-vs-merged-profiles}

Chaque profil client est composé de plusieurs fragments de profil qui ont été fusionnés dans le but de former une vue unique pour ce client. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre organisation dispose de plusieurs fragments de profil associés à ce client unique apparaissant dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans Platform, ils sont fusionnés afin de créer un profil unique pour ce client.

En d’autres termes, les fragments de profil représentent une identité principale unique et les données [enregistrement](#record-data) ou [événement](#time-series-events) correspondantes pour cet identifiant au sein d’un jeu de données spécifique.

Lorsque les données provenant de plusieurs sources entrent en conflit (par exemple, si un fragment classe le client comme étant « célibataire » tandis qu’un autre le classe comme étant « marié »), la [stratégie de fusion](#merge-policies) détermine quelles informations doivent être prioritaires et être incluses dans le profil de l’individu. Par conséquent, il est probable que le nombre total de fragments de profil au sein de Platform soit toujours supérieur au nombre total de profils fusionnés, chaque profil étant composé de fragments multiples issus de multiples jeux de données.

### Données d’enregistrement {#record-data}

Un profil est la représentation d’un sujet, d’une organisation ou d’un individu. Il est composé de nombreux attributs également appelés données d’enregistrement. Par exemple, le profil d’un produit peut inclure un SKU et une description, tandis que le profil d’une personne contient des informations telles que le prénom, le nom et l’adresse e-mail. [!DNL Experience Platform] vous permet de personnaliser les profils afin d’utiliser des données spécifiques pertinentes pour votre entreprise. La classe standard du [!DNL Experience Data Model] (XDM), [!DNL XDM Individual Profile], est la classe privilégiée à partir de laquelle créer un schéma lors de la description des données d’enregistrement des clients. Elle fournit les données intégrées à de nombreuses interactions entre les services Platform. Pour plus d’informations sur l’utilisation des schémas dans [!DNL Experience Platform], consultez tout d’abord la [présentation du système XDM](../xdm/home.md).

### Événements de série temporelle {#time-series-events}

Les données de série temporelle fournissent un instantané du système au moment où une action a été entreprise, directement ou indirectement, par un sujet, ainsi que des données détaillant l’événement lui-même. Représentées par la classe de schéma standard XDM ExperienceEvent, les données de série temporelle peuvent décrire des événements tels que l’ajout d’articles à un panier, l’utilisation de liens et la lecture de vidéos. Vous pouvez utiliser les données de série temporelle pour établir des règles de segmentation et consulter les événements individuellement dans le cadre d’un profil.

### Identités

Toutes les entreprises souhaitent s’adresser à leurs clients de manière personnalisée. Cependant, l’un des défis que représente la proposition d’expériences numériques pertinentes aux clients consiste à trouver un moyen de relier leurs données déconnectées. Celles-ci sont souvent réparties sur différents canaux numériques tels que les tablettes, les téléphones mobiles et les ordinateurs portables. Le [!DNL Identity Service] vous permet de rassembler l’image complète de votre client en liant les identités de plusieurs canaux et en créant un graphique d’identités pour chaque client. Consultez la [présentation d’Identity Service](../identity-service/home.md) pour en savoir plus.

### Stratégies de fusion

Lorsque vous rassemblez des fragments de données provenant de plusieurs sources et les combinez pour obtenir une vue complète de chaque client, les stratégies de fusion sont les règles utilisées par [!DNL Platform] pour déterminer quelle est la priorité des données et quelles données seront combinées pour créer le profil client.

En cas de conflit de données provenant de plusieurs jeux de données, la stratégie de fusion détermine comment ces données doivent être traitées et quelle valeur doit être utilisée. À lʼaide dʼAPI RESTful ou de lʼinterface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation.

Pour en savoir plus sur les stratégies de fusion et leur rôle dans Experience Platform, commencez par lire la [présentation des stratégies de fusion](merge-policies/overview.md).

### Schémas d’union {#profile-fragments-and-union-schemas}

L’une des fonctionnalités clés du [!DNL Real-time Customer Profile] est la possibilité d’unifier les données multicanales. Lorsque vous utilisez le [!DNL Real-time Customer Profile] pour accéder à une entité, vous pouvez obtenir un affichage fusionné de tous les fragments de profil de cette entité dans les jeux de données, appelé « vue d’union » et obtenu grâce au schéma d’union.

Pour en savoir plus sur les schémas d’union, notamment sur la façon d’y accéder dans l’interface utilisateur, consultez le [guide de l’interface utilisateur des schémas d’union](ui/union-schema.md).

### (Alpha) Attributs calculés

>[!IMPORTANT]
>
>La fonctionnalité d’attributs calculés est en version Alpha. La documentation et la fonctionnalité peuvent changer.

Les attributs calculés sont des fonctions utilisées pour regrouper des données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées au niveau de la segmentation, de l’activation et de la personnalisation. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat de durée de vie, le temps écoulé entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que ces informations sont nécessaires. Pour plus d’informations sur les attributs calculés, notamment la présentation du rôle qu’ils jouent dans Adobe Experience Platform, consultez tout d’abord la [présentation des attributs calculés](computed-attributes/overview.md).

## Profils et segments

Le [!DNL Segmentation Service] d’Adobe Experience Platform fournit les audiences nécessaires à l’optimisation de l’expérience de chaque client. Lorsqu’un segment ciblé est créé, l’identifiant de ce segment est ajouté à la liste des adhésions au segment pour tous les profils admissibles. Les règles de segmentation sont créées et appliquées aux données du [!DNL Real-time Customer Profile] à l’aide des API RESTful et de l’interface utilisateur du créateur de segments. Pour en savoir plus sur la segmentation, commencez pas lire la [Présentation de Segmentation Service](../segmentation/home.md).

### Ingestion par flux et segmentation par flux

L’entrée en temps réel est possible grâce à un processus appelé ingestion par flux. À mesure que les données de profil et de série temporelle sont ingérées, le [!DNL Real-time Customer Profile] décide automatiquement d’inclure ou d’exclure ces données des segments par le biais d’un processus continu appelé la segmentation par flux, avant de les fusionner avec les données existantes et de mettre à jour la vue d’union. Par conséquent, vous pouvez instantanément effectuer des calculs et prendre des décisions pour offrir aux clients de meilleures expériences personnalisées lorsqu’ils interagissent avec votre marque. Lors de l’ingestion, les données sont également soumises à un processus de validation pour s’assurer qu’elles sont correctement ingérées et conformes au schéma sur lequel le jeu de données est basé. Pour plus d’informations sur la validation effectuée lors de l’ingestion, commencez par lire la [présentation de la qualité d’ingestion des données](../ingestion/quality/overview.md).

## Projections de périphérie

Afin d’offrir à vos clients des expériences coordonnées, cohérentes et personnalisées sur plusieurs canaux en temps réel, les bonnes données doivent être facilement disponibles et mises à jour en continu, au fur et à mesure des changements. Adobe Experience Platform permet cet accès aux données en temps réel grâce à l’utilisation de ce que l’on appelle les périphéries. Une périphérie est un serveur réparti géographiquement qui stocke les données et les rend facilement accessibles aux applications. Par exemple, les applications Adobe telles qu’Adobe Target et Adobe Campaign utilisent des périphéries afin d’offrir des expériences client personnalisées en temps réel. Les données sont acheminées vers une périphérie par projection, une destination de projection définissant la périphérie vers laquelle les données sont envoyées, et une configuration de projection définissant les informations spécifiques rendues disponibles dans la périphérie. Pour en savoir plus sur les projections et commencer à les utiliser à l’aide de l’API du [!DNL Real-time Customer Profile], reportez-vous au [guide des points d’entrée de projection de périphérie](api/edge-projections.md).

## Ingestion de données dans le [!DNL Profile]

Vous pouvez configurer [!DNL Platform] pour envoyer les données d’enregistrement et de série temporelle au [!DNL Profile]. Cela est compatible avec l’ingestion par lots et l’ingestion par flux en temps réel. Pour plus d’informations, consultez le tutoriel décrivant comment [ajouter des données à Real-time Customer Profile](tutorials/add-profile-data.md).

>[!NOTE]
>
>Les données collectées par l’intermédiaire des solutions Adobe, notamment [!DNL Analytics Cloud], [!DNL Marketing Cloud] et [!DNL Advertising Cloud], débordent dans [!DNL Experience Platform] et sont ingérées dans le [!DNL Profile].

### Mesures d’ingestion de profil

Observability Insights vous permet d’afficher les mesures clés dans Adobe Experience Platform. Outre les statistiques d’utilisation relatives à [!DNL Experience Platform] et les indicateurs de performances pour diverses fonctionnalités de [!DNL Platform], des mesures spécifiques liées au profil vous permettent d’obtenir des éclairages sur les taux de requêtes entrantes, les taux d’ingestion réussie, les tailles d’enregistrements ingérés, etc. Pour en savoir plus, consultez tout d’abord la [présentation de l’API Observability Insights](../observability/api/overview.md) et pour obtenir une liste complète des mesures du profil client en temps réel, consultez la documentation sur les [mesures disponibles](../observability/api/metrics.md#available-metrics).

## Mise à jour des données du magasin de profils

Il peut parfois être nécessaire de mettre à jour les données du magasin de profils de votre organisation. Vous pouvez par exemple avoir besoin de corriger des enregistrements ou de modifier une valeur d’attribut. Cette opération peut être effectuée par ingestion par lot et nécessite un jeu de données compatible avec les profils et configuré avec une balise upsert. Pour plus d’informations sur la façon de configurer un jeu de données pour les mises à jour d’attributs, veuillez vous référer au tutoriel concernant l’[activation d’un jeu de données pour Profile et upsert](../catalog/datasets/enable-upsert.md).

## Gouvernance des données et [!DNL Privacy]

La gouvernance des données est constituée d’une série de stratégies et de technologies permettant de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux stratégies applicables à l’utilisation des données.

En ce qui concerne l’accès aux données, la gouvernance des données joue un rôle essentiel dans [!DNL Experience Platform], et ce, à différents niveaux :

- Application de libellés d’utilisation des données
- Stratégies d’accès aux données
- Contrôle de l’accès aux données pour les actions marketing

La gouvernance des données est gérée sur plusieurs points. Il s’agit notamment de choisir les données à ingérer dans [!DNL Platform] et celles qui seront accessibles après l’ingestion pour une action marketing donnée. Pour plus d’informations, commencez par lire la [présentation de la gouvernance des données](../data-governance/home.md).

### Gestion des demandes d’exclusion et de confidentialité des données

[!DNL Experience Platform] permet à vos clients d’envoyer des demandes de désinscription associées à l’utilisation et au stockage de leurs données dans le [!DNL Real-time Customer Profile]. Pour plus d’informations sur la gestion des demandes d’exclusion, consultez la documentation sur le [respect des demandes d’exclusion](../segmentation/consents.md).

## Étapes suivantes et ressources supplémentaires

Pour en savoir plus sur l’utilisation des données du profil client en temps réel à l’aide de l’interface utilisateur d’Experience Platform ou de l’API Profile, commencez par consulter respectivement le [guide de l’interface utilisateur Profil](ui/user-guide.md) ou le [guide développeur de l’API](api/overview.md).
