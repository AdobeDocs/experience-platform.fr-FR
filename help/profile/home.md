---
keywords: Experience Platform ; profil ; profil client en temps réel ; résolution des problèmes ; API ; profil unifié ; Profil unifié ; unifié ; Profil ; rtcp ; graphiques XDM
title: Présentation du Profil client en temps réel
topic-legacy: guide
description: Real-time Customer Profile est une banque d’entités de recherche générique qui fusionne les données de différentes ressources de données d’entreprise, puis fournit un accès à ces données sous la forme de profils client individuels et d’événements de série temporelle connexes. Cette fonctionnalité permet aux spécialistes marketing d’offrir à leur audience des expériences coordonnées, cohérentes et pertinentes sur plusieurs canaux.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 34%

---

# [!DNL Real-time Customer Profile] présentation

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. [!DNL Real-time Customer Profile] permet de visualiser une vue holistique de chaque client en combinant des données provenant de plusieurs canaux, notamment en ligne, hors ligne, CRM et tiers. [!DNL Profile] vous permet de consolider les données de vos clients dans une vue unifiée offrant un compte horodaté utilisable de chaque interaction de client. Cette présentation vous aidera à comprendre le rôle et l&#39;utilisation de [!DNL Real-time Customer Profile] dans [!DNL Experience Platform].

## [!DNL Profile] dans Experience Platform

La relation entre Real-time Customer Profile et les autres services dans Experience Platform est mise en évidence dans le schéma suivant :

![](images/profile-overview/profile-in-platform.png)

## Présentation des profils

[!DNL Real-time Customer Profile] fusionne les données de divers systèmes d’entreprise, puis fournit un accès à ces données sous la forme de profils client avec des événements de séries chronologiques connexes. Cette fonctionnalité permet aux spécialistes marketing d’offrir à leur audience des expériences coordonnées, cohérentes et pertinentes sur plusieurs canaux. Les sections suivantes mettent en évidence certains des concepts de base que vous devez comprendre afin de créer et de gérer efficacement des profils au sein de Plateforme.

### Banque de données de profil

Bien que [!DNL Real-time Customer Profile] traite les données imbriquées et utilise Adobe Experience Platform [!DNL Identity Service] pour fusionner les données connexes par le biais du mappage d&#39;identité, il conserve ses propres données dans le magasin de données [!DNL Profile]. Le magasin [!DNL Profile] est séparé des données du catalogue dans le lac de données et des données [!DNL Identity Service] dans le graphique d&#39;identité.

Le magasin de Profils utilise une infrastructure de base de données Microsoft Azure Cosmos et Platform Data Lake utilise l&#39;enregistrement Microsoft Azure Data Lake.

### Gardiens de profil

L’Experience Platform fournit une série de garde-fous pour vous aider à éviter de créer des [schémas de modèle de données d’expérience (XDM)](../xdm/home.md) que le Profil client en temps réel ne peut pas prendre en charge. Cela inclut des limites souples qui entraîneront une dégradation des performances, ainsi que des limites strictes qui entraîneront des erreurs et des pannes système. Pour plus d&#39;informations, y compris une liste de directives et des exemples d&#39;utilisation, veuillez lire la [documentation sur les garde-Profils](guardrails.md).

### (Bêta) tableau de bord de Profil {#profile-dashboard}

>[!IMPORTANT]
>
>La fonctionnalité de tableau de bord est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

L’interface utilisateur de l’Experience Platform fournit un tableau de bord grâce auquel vous pouvez vue des informations importantes sur vos données de Profil client en temps réel, telles qu’elles sont capturées au cours d’un instantané quotidien. Pour savoir comment accéder au tableau de bord [!DNL Profile] et l&#39;utiliser dans l&#39;interface utilisateur, ainsi que pour obtenir des informations détaillées sur les mesures affichées dans le tableau de bord, consultez le [guide de l&#39;interface utilisateur du tableau de bord de Profil](ui/profile-dashboard.md).

### Fragments de profil par rapport aux profils fusionnés {#profile-fragments-vs-merged-profiles}

Chaque profil client individuel est composé de plusieurs fragments de profil qui ont été fusionnés pour former une seule vue du client. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre entreprise aura plusieurs fragments de profil liés à ce client unique qui apparaîtront dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans la plate-forme, ils sont fusionnés ensemble afin de créer un profil unique pour ce client.

Lorsque les données provenant de plusieurs sources entrent en conflit (par exemple, un fragment liste le client comme &quot;unique&quot; tandis que les autres listes le client comme &quot;marié&quot;), la [stratégie de fusion](#merge-policies) détermine les informations à classer par priorité et à inclure dans le profil pour l&#39;individu. Par conséquent, il est probable que le nombre total de fragments de profil au sein de la plate-forme soit toujours supérieur au nombre total de profils fusionnés, chaque profil étant composé de fragments multiples.

### Enregistrer les données

Un profil est la représentation d&#39;un sujet, d&#39;une organisation ou d&#39;un individu, composé de nombreux attributs (également appelés données d&#39;enregistrement). Par exemple, le profil d’un produit peut inclure un SKU et une description, tandis que le profil d’une personne contient des informations telles que le prénom, le nom et l’adresse électronique. [!DNL Experience Platform] vous permet de personnaliser des profils afin d’utiliser des données spécifiques concernant votre entreprise. La classe standard [!DNL Experience Data Model] (XDM), [!DNL XDM Individual Profile], est la classe préférée sur laquelle construire un schéma lors de la description des données d&#39;enregistrement client, et fournit les données qui font partie intégrante de nombreuses interactions entre les services Platform. Pour plus d&#39;informations sur l&#39;utilisation des schémas dans [!DNL Experience Platform], veuillez commencer par lire l&#39;[Présentation du système XDM](../xdm/home.md).

### Événements de série temporelle

Les données de série temporelle fournissent un instantané du système au moment où une action a été entreprise, directement ou indirectement, par un sujet, ainsi que des données détaillant l’événement lui-même. Représentées par la classe de schéma standard XDM ExperienceEvent, les données de série temporelle peuvent décrire des événements tels que l’ajout d’articles à un panier, l’utilisation de liens et la lecture de vidéos. Vous pouvez utiliser les données de série temporelle pour établir des règles de segmentation et consulter les événements individuellement dans le cadre d’un profil.

### Identités

Toutes les entreprises souhaitent s’adresser à leurs clients de manière personnalisée. Cependant, l’un des défis que représente la proposition d’expériences numériques pertinentes aux clients consiste à trouver un moyen de relier leurs données déconnectées. Celles-ci sont souvent réparties sur différents canaux numériques tels que les tablettes, les téléphones mobiles et les ordinateurs portables. [!DNL Identity Service] vous permet de rassembler l&#39;image complète de votre client en liant les identités de plusieurs canaux et en créant un graphique d&#39;identité pour chaque client. Consultez la [présentation d’Identity Service](../identity-service/home.md) pour en savoir plus.

### Stratégies de fusion

Lorsque vous rassemblez des fragments de données provenant de plusieurs sources et les combinez afin d’obtenir une vue complète de chacun de vos clients, les stratégies de fusion sont les règles que [!DNL Platform] utilise pour déterminer comment les données seront hiérarchisées et quelles données seront utilisées pour créer le profil client. En cas de conflit de données provenant de plusieurs jeux de données, la stratégie de fusion détermine comment ces données doivent être traitées et quelle valeur doit être utilisée. À l’aide d’API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation dans l’interface utilisateur.

Pour plus d&#39;informations sur l&#39;utilisation des stratégies de fusion à l&#39;aide de l&#39;API [!DNL Real-time Customer Profile], consultez le [guide du point de terminaison des stratégies de fusion](api/merge-policies.md). Pour utiliser les stratégies de fusion à l&#39;aide de l&#39;[!DNL Experience Platform] interface utilisateur, consultez le [guide d&#39;interface utilisateur des stratégies de fusion](ui/merge-policies.md).

### Schémas d&#39;Union {#profile-fragments-and-union-schemas}

L&#39;une des principales fonctionnalités de [!DNL Real-time Customer Profile] est la possibilité d&#39;unifier les données à canaux multiples. Lorsque [!DNL Real-time Customer Profile] est utilisé pour accéder à une entité, il peut vous fournir une vue fusionnée de tous les fragments de profil pour cette entité dans les jeux de données, appelés &quot;vue d&#39;union&quot; et rendue possible par ce qu&#39;on appelle un schéma d&#39;union.

Pour en savoir plus sur les schémas d’union, y compris sur la façon d’accéder aux schémas d’union dans l’interface utilisateur, consultez le [guide de l’interface utilisateur des schémas d’union](ui/union-schema.md).

### (Alpha) Attributs calculés

>[!IMPORTANT]
>
>La fonctionnalité d&#39;attribut calculé est en alpha. La documentation et les fonctionnalités peuvent être modifiées.

Les attributs calculés sont des fonctions utilisées pour agrégat des données au niveau du événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées pour la segmentation, l’activation et la personnalisation. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat de durée de vie, le temps écoulé entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que ces informations sont nécessaires. Pour plus d&#39;informations sur les attributs calculés, y compris la compréhension du rôle que jouent les attributs calculés dans Adobe Experience Platform, veuillez commencer par lire l&#39;[aperçu des attributs calculés](computed-attributes/overview.md).

## Profils et segments

Adobe Experience Platform [!DNL Segmentation Service] produit les audiences nécessaires pour alimenter les expériences de vos clients individuels. Lorsqu’un segment ciblé est créé, l’identifiant de ce segment est ajouté à la liste des adhésions au segment pour tous les profils admissibles. Les règles de segmentation sont créées et appliquées aux données [!DNL Real-time Customer Profile] à l’aide des API RESTful et de l’interface utilisateur du créateur de segments. Pour en savoir plus sur la segmentation, commencez pas lire la [Présentation de Segmentation Service](../segmentation/home.md).

### Ingestion par flux et segmentation par flux

L’entrée en temps réel est possible grâce à un processus appelé ingestion par flux. À mesure que des données de profil et de série chronologique sont ingérées, [!DNL Real-time Customer Profile] décide automatiquement d&#39;inclure ou d&#39;exclure ces données des segments par le biais d&#39;un processus continu appelé segmentation en flux continu, avant de les fusionner avec les données existantes et de mettre à jour la vue d&#39;union. Par conséquent, vous pouvez instantanément effectuer des calculs et prendre des décisions pour offrir aux clients de meilleures expériences personnalisées lorsqu’ils interagissent avec votre marque. Lors de l’ingestion, les données sont également soumises à un processus de validation pour s’assurer qu’elles sont correctement ingérées et conformes au schéma sur lequel le jeu de données est basé. Pour plus d’informations sur la validation effectuée lors de l’ingestion, commencez par lire la [présentation de la qualité d’ingestion des données](../ingestion/quality/overview.md).

## Projections de périphérie

Afin d’offrir des expériences coordonnées, cohérentes et personnalisées à vos clients sur plusieurs canaux en temps réel, les données appropriées doivent être facilement disponibles et mises à jour en continu au fur et à mesure des changements. Adobe Experience Platform permet cet accès aux données en temps réel grâce à l’utilisation de ce que l’on appelle les périphéries. Une périphérie est un serveur réparti géographiquement qui stocke les données et les rend facilement accessibles aux applications. Par exemple, les applications d’Adobe telles que Adobe Target et Adobe Campaign utilisent des bords afin de fournir des expériences client personnalisées en temps réel. Les données sont acheminées vers une périphérie par projection, une destination de projection définissant la périphérie vers laquelle les données sont envoyées, et une configuration de projection définissant les informations spécifiques rendues disponibles dans la périphérie. Pour en savoir plus et commencer à utiliser les projections à l&#39;aide de l&#39;API [!DNL Real-time Customer Profile], consultez le [guide des points de terminaison de projection de périphérie](api/edge-projections.md).

## Incorporation de données dans [!DNL Profile]

[!DNL Platform] peut être configuré pour envoyer des données d’enregistrement et de série chronologique à  [!DNL Profile], en prenant en charge l’assimilation en temps réel de flux continu et l’assimilation par lot. Pour plus d’informations, consultez le tutoriel décrivant comment [ajouter des données à Real-time Customer Profile](tutorials/add-profile-data.md).

>[!NOTE]
>
>Les données collectées par l&#39;intermédiaire de solutions d&#39;Adobe, y compris [!DNL Analytics Cloud], [!DNL Marketing Cloud] et [!DNL Advertising Cloud], débordent dans [!DNL Experience Platform] et sont assimilées à [!DNL Profile].

### Mesures d&#39;assimilation de profil

Observability Insights vous permet d’afficher les mesures clés dans Adobe Experience Platform. Outre les [!DNL Experience Platform] statistiques d&#39;utilisation et les indicateurs de performances de diverses fonctionnalités [!DNL Platform], il existe des mesures spécifiques liées aux profils qui vous permettent d&#39;obtenir des informations sur les taux de demande entrants, les taux d&#39;assimilation réussis, les tailles d&#39;enregistrements assimilés, etc. Pour en savoir plus, lisez tout d&#39;abord [Présentation de l&#39;API d&#39;statistiques d&#39;observabilité](../observability/api/overview.md) et pour obtenir une liste complète des mesures du Profil client en temps réel, consultez la documentation sur [les mesures disponibles](../observability/api/metrics.md#available-metrics).

## [!DNL Data governance] et [!DNL Privacy]

[!DNL Data governance] est une série de stratégies et de technologies utilisées pour gérer les données client et assurer le respect des règlements, restrictions et politiques applicables à l&#39;utilisation des données.

En ce qui concerne l&#39;accès aux données, la gouvernance des données joue un rôle clé dans [!DNL Experience Platform] à divers niveaux :
* Application de libellés d’utilisation des données
* Stratégies d’accès aux données
* Contrôle de l’accès aux données pour les actions marketing

[!DNL Data governance] est géré à plusieurs points. Il s’agit notamment de déterminer quelles données sont assimilées à [!DNL Platform] et quelles données sont accessibles après l’assimilation pour une action marketing donnée. Pour plus d’informations, commencez par lire la [présentation de la gouvernance des données](../data-governance/home.md).

### Gestion des demandes d’exclusion et de confidentialité des données

[!DNL Experience Platform] permet à vos clients d’envoyer des demandes d’exclusion liées à l’utilisation et à l’enregistrement de leurs données dans  [!DNL Real-time Customer Profile]. Pour plus d’informations sur la gestion des demandes d’exclusion, consultez la documentation sur le [respect des demandes d’exclusion](../segmentation/honoring-opt-outs.md).

## Étapes suivantes et ressources supplémentaires

Pour en savoir plus sur l&#39;utilisation des données [!DNL Real-time Customer Profile] à l&#39;aide de l&#39;interface utilisateur Experience Platform ou de l&#39;API de Profil, consultez le [guide de l&#39;interface utilisateur du Profil](ui/user-guide.md) ou le [guide du développeur d&#39;API](api/overview.md), respectivement.
