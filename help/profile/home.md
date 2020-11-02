---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;XDM graphs
title: Présentation de Real-time Customer Profile
topic: guide
description: Real-time Customer Profile est une banque d’entités de recherche générique qui fusionne les données de différentes ressources de données d’entreprise, puis fournit un accès à ces données sous la forme de profils client individuels et d’événements de série temporelle connexes. Cette fonctionnalité permet aux spécialistes marketing d’offrir à leur audience des expériences coordonnées, cohérentes et pertinentes sur plusieurs canaux.
translation-type: tm+mt
source-git-commit: 47c65ef5bdd083c2e57254189bb4a1f1d9c23ccc
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 42%

---


# [!DNL Real-time Customer Profile] présentation

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. With [!DNL Real-time Customer Profile], you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. [!DNL Profile] vous permet de consolider vos données client disparates en une vue unifiée offrant un compte d’activité horodaté de chaque interaction client. This overview will help you understand the role and use of [!DNL Real-time Customer Profile] in [!DNL Experience Platform].

## [!DNL Profile] dans Experience Platform

La relation entre Real-time Customer Profile et les autres services dans Experience Platform est mise en évidence dans le schéma suivant :

![Services Adobe Experience Platform.](images/profile-overview/profile-in-platform.png)

### Banque de données de profil

Although [!DNL Real-time Customer Profile] processes ingested data and uses Adobe Experience Platform [!DNL Identity Service] to merge related data through identity mapping, it maintains its own data in the [!DNL Profile] store. En d’autres termes, le [!DNL Profile] magasin est séparé des [!DNL Catalog] données ([!DNL Data Lake]) et [!DNL Identity Service] des données (graphique d’identité).

### Gardiens de profil

Experience Platform fournit une série de garde-fous pour vous aider à éviter de créer des schémas [de modèle de données d’](../xdm/home.md) expérience (XDM) que le Profil client en temps réel ne peut pas prendre en charge. Cela inclut des limites souples qui entraîneront une dégradation des performances, ainsi que des limites strictes qui entraîneront des erreurs et des pannes système. Pour plus d&#39;informations, y compris une liste de directives et des exemples de cas d&#39;utilisation, veuillez lire la documentation sur les garde-fous [](guardrails.md) Profil.

## Présentation des profils

[!DNL Real-time Customer Profile] fusionne les données de divers systèmes d’entreprise, puis fournit un accès à ces données sous la forme de profils client avec des événements de séries chronologiques connexes. Cette fonctionnalité permet aux spécialistes marketing d’offrir à leur audience des expériences coordonnées, cohérentes et pertinentes sur plusieurs canaux. Les sections suivantes mettent en évidence certains des concepts de base que vous devez comprendre afin de créer et de gérer efficacement des profils au sein de Plateforme.

### Fragments de profil par rapport aux profils fusionnés

Chaque profil client individuel est composé de plusieurs fragments de profil qui ont été fusionnés pour former une seule vue du client. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre entreprise aura plusieurs fragments de profil liés à ce client unique qui apparaîtront dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans la plate-forme, ils sont fusionnés ensemble afin de créer un profil unique pour ce client.

Lorsque les données provenant de plusieurs sources entrent en conflit (par exemple, un fragment liste le client comme &quot;unique&quot; tandis que les autres listes le client comme &quot;marié&quot;), la stratégie [de](#merge-policies) fusion détermine les informations à classer par priorité et à inclure dans le profil de la personne. Par conséquent, il est probable que le nombre total de fragments de profil au sein de la plate-forme soit toujours supérieur au nombre total de profils fusionnés, chaque profil étant composé de fragments multiples.

### Enregistrer les données

Un profil est la représentation d&#39;un sujet, d&#39;une organisation ou d&#39;un individu, composé de nombreux attributs (également appelés données d&#39;enregistrement). Par exemple, le profil d’un produit peut inclure un SKU et une description, tandis que le profil d’une personne contient des informations telles que le prénom, le nom et l’adresse électronique. Using [!DNL Experience Platform], you can customize profiles to use specific data relevant to your business. The standard [!DNL Experience Data Model] (XDM) class, [!DNL XDM Individual Profile], is the preferred class upon which to build a schema when describing customer record data, and supplies the data integral to many interactions between Platform services. For more information on working with schemas in [!DNL Experience Platform], please begin by reading the [XDM System overview](../xdm/home.md).

### Événements de série temporelle

Les données de série temporelle fournissent un instantané du système au moment où une action a été entreprise, directement ou indirectement, par un sujet, ainsi que des données détaillant l’événement lui-même. Représentées par la classe de schéma standard XDM ExperienceEvent, les données de série temporelle peuvent décrire des événements tels que l’ajout d’articles à un panier, l’utilisation de liens et la lecture de vidéos. Vous pouvez utiliser les données de série temporelle pour établir des règles de segmentation et consulter les événements individuellement dans le cadre d’un profil.

### Identités

Toutes les entreprises souhaitent s’adresser à leurs clients de manière personnalisée. Cependant, l’un des défis que représente la proposition d’expériences numériques pertinentes aux clients consiste à trouver un moyen de relier leurs données déconnectées. Celles-ci sont souvent réparties sur différents canaux numériques tels que les tablettes, les téléphones mobiles et les ordinateurs portables. [!DNL Identity Service] vous permet de rassembler l&#39;image complète de votre client en liant les identités de plusieurs canaux et en créant un graphique d&#39;identité pour chaque client. Consultez la [présentation d’Identity Service](../identity-service/home.md) pour en savoir plus.

### Stratégies de fusion

When bringing data fragments together from multiple sources and combining them in order to see a complete view of each of your individual customers, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be used to create the customer profile. En cas de conflit de données provenant de plusieurs jeux de données, la stratégie de fusion détermine comment ces données doivent être traitées et quelle valeur doit être utilisée. À l’aide d’API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation dans l’interface utilisateur. Pour plus d’informations sur l’utilisation des stratégies de fusion à l’aide de l’ [!DNL Real-time Customer Profile] API, consultez le guide [des points de terminaison des stratégies de](api/merge-policies.md)fusion. To work with merge policies using the [!DNL Experience Platform] UI, refer to the [merge policies user guide](ui/merge-policies.md).

### Schémas Unions {#profile-fragments-and-union-schemas}

One of the key features of [!DNL Real-time Customer Profile] is the ability to unify multi-channel data. When [!DNL Real-time Customer Profile] is used to access an entity, it can supply you with a merged view of all profile fragments for that entity across datasets, referred to as the union view and made possible through what is known as a union schema. [!DNL Real-time Customer Profile]Les données sont fusionnées entre les sources lorsqu’une entité ou un profil est consulté à l’aide de son identifiant ou exporté sous forme de segment. Pour en savoir plus sur l’accès aux profils et aux vues d’union à l’aide de l’ [!DNL Real-time Customer Profile] API, consultez le guide [des points de terminaison](api/entities.md)entités.

### Segmentation

Adobe Experience Platform [!DNL Segmentation Service] produces the audiences needed to power experiences for your individual customers. Lorsqu’un segment ciblé est créé, l’identifiant de ce segment est ajouté à la liste des adhésions au segment pour tous les profils admissibles. Segment rules are built and applied to [!DNL Real-time Customer Profile] data using RESTful APIs and the Segment Builder user interface. Pour en savoir plus sur la segmentation, commencez pas lire la [Présentation de Segmentation Service](../segmentation/home.md).

### (Alpha) Configuration des attributs calculés

>[!IMPORTANT]
>
>La fonctionnalité d’attribut calculée est en alpha. La documentation et les fonctionnalités peuvent changer.

Les attributs calculés vous permettent de calculer automatiquement la valeur des champs en fonction d’autres valeurs, calculs et expressions. Les attributs calculés fonctionnent au niveau du profil, ce qui signifie que vous pouvez agréger des valeurs sur tous les enregistrements et tous les événements. Chaque attribut calculé contient une expression, ou « règle », qui évalue les données entrantes et stocke la valeur obtenue dans un attribut de profil ou dans un événement. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat de durée de vie, le temps écoulé entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que ces informations sont nécessaires. Pour plus d’informations sur les attributs calculés et des instructions détaillées sur leur utilisation à l’aide de l’ [!DNL Real-time Customer Profile] API, consultez le guide [des points de terminaison des attributs](api/computed-attributes.md)calculés. Ce guide vous aidera à mieux comprendre le rôle que jouent les attributs calculés dans Adobe Experience Platform et comprend des exemples d’appels d’API pour effectuer des opérations CRUD de base.

## Composants en temps réel

This section introduces the components that allow [!DNL Real-time Customer Profile] to update and monitor record and time series data in real-time.

### Ingestion par flux et segmentation par flux

L’entrée en temps réel est possible grâce à un processus appelé ingestion par flux. As profile and time series data is ingested, [!DNL Real-time Customer Profile] automatically decides to include or exclude that data from segments through an ongoing process called streaming segmentation, before merging it with existing data and updating the union view. Par conséquent, vous pouvez instantanément effectuer des calculs et prendre des décisions pour offrir aux clients de meilleures expériences personnalisées lorsqu’ils interagissent avec votre marque. Lors de l’ingestion, les données sont également soumises à un processus de validation pour s’assurer qu’elles sont correctement ingérées et conformes au schéma sur lequel le jeu de données est basé. Pour plus d’informations sur la validation effectuée lors de l’ingestion, commencez par lire la [présentation de la qualité d’ingestion des données](../ingestion/quality/overview.md).

### Configurations et destinations de projection Edge

Afin d’offrir à vos clients des expériences coordonnées, cohérentes et personnalisées sur plusieurs canaux en temps réel, les bonnes données doivent être facilement disponibles et mises à jour en continu, au fur et à mesure des changements. Adobe Experience Platform permet cet accès aux données en temps réel grâce à l’utilisation de ce que l’on appelle les périphéries. Une périphérie est un serveur réparti géographiquement qui stocke les données et les rend facilement accessibles aux applications. Par exemple, les applications Adobe telles qu’Adobe Target et Adobe Campaign utilisent des périphéries afin d’offrir des expériences client personnalisées en temps réel. Les données sont acheminées vers une périphérie par projection, une destination de projection définissant la périphérie vers laquelle les données sont envoyées, et une configuration de projection définissant les informations spécifiques rendues disponibles dans la périphérie. Pour en savoir plus et commencer à utiliser les projections à l&#39;aide de l&#39; [!DNL Real-time Customer Profile] API, consultez le guide [des points de terminaison de projection](api/edge-projections.md)de périphérie.

## Ingest data into [!DNL Profile]

[!DNL Platform] peut être configuré pour envoyer des données d’enregistrement et de série chronologique à [!DNL Profile], en prenant en charge l’assimilation en temps réel de flux continu et l’assimilation par lot. Pour plus d’informations, consultez le tutoriel décrivant comment [ajouter des données à Real-time Customer Profile](tutorials/add-profile-data.md).

>[!NOTE]
>
>Les données collectées par le biais de solutions d&#39;Adobe, y compris [!DNL Analytics Cloud], [!DNL Marketing Cloud]et [!DNL Advertising Cloud], se déversent dans [!DNL Experience Platform] et sont ingérées dans [!DNL Profile].

### [!DNL Profile] mesures d’assimilation

Observability Insights vous permet d’afficher les mesures clés dans Adobe Experience Platform. In addition to [!DNL Platform] usage statistics and performance indicators for various [!DNL Platform] functionalities, there are specific [!DNL Profile]-related metrics that allow you to gain insight into incoming request rates, successful ingestion rates, ingested record sizes, and more. To learn more, begin by reading the [Observability Insights API overview](../observability/api/overview.md), and for a complete list of [!DNL Profile] metrics, see the documentation on [available metrics](../observability/api/metrics.md#available-metrics).

## [!DNL Data governance] et [!DNL Privacy]

[!DNL Data governance] est une série de stratégies et de technologies utilisées pour gérer les données client et assurer le respect des règlements, restrictions et politiques applicables à l&#39;utilisation des données.

As it relates to accessing data, data governance plays a key role within [!DNL Experience Platform] at various levels:
* Application de libellés d’utilisation des données
* Stratégies d’accès aux données
* Contrôle de l’accès aux données pour les actions marketing

[!DNL Data governance] est géré à plusieurs points. These include deciding what data is ingested into [!DNL Platform] and what data is accessible after ingestion for a given marketing action. Pour plus d’informations, commencez par lire la [présentation de la gouvernance des données](../data-governance/home.md).

### Gestion des demandes d’exclusion et de confidentialité des données

[!DNL Experience Platform] permet à vos clients d’envoyer des demandes d’exclusion liées à l’utilisation et à l’enregistrement de leurs données dans [!DNL Real-time Customer Profile]. Pour plus d’informations sur la gestion des demandes d’exclusion, consultez la documentation sur le [respect des demandes d’exclusion](../segmentation/honoring-opt-outs.md).

## Étapes suivantes et ressources supplémentaires

Pour en savoir plus sur l&#39;utilisation [!DNL Real-time Customer Profile]de l&#39;interface utilisateur de [Profil ou du guide](ui/user-guide.md) du développeur d&#39; [](api/overview.md)API, consultez la section

>[!WARNING]
>
>L&#39;interface utilisateur de l&#39;Experience Platform est fréquemment mise à jour et peut avoir changé depuis l&#39;enregistrement de cette vidéo. Consultez le guide [d&#39;utilisation du Profil client en temps](ui/user-guide.md) réel pour obtenir les dernières captures d&#39;écran et fonctionnalités de l&#39;interface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)