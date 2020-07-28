---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Présentation de Real-time Customer Profile
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 52%

---


# [!DNL Real-time Customer Profile] aperçu

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. With [!DNL Real-time Customer Profile], you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. [!DNL Profile] vous permet de consolider vos données client disparates en une vue unifiée offrant un compte d’activité horodaté de chaque interaction client. This overview will help you understand the role and use of [!DNL Real-time Customer Profile] in [!DNL Experience Platform].

## Understanding [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] est une banque d’entités de recherche générique qui fusionne les données de différentes ressources de données d’entreprise, puis fournit un accès à ces données sous la forme de profils client individuels et d’événements de série temporelle connexes. Cette fonctionnalité permet aux spécialistes marketing d’offrir à leur audience des expériences coordonnées, cohérentes et pertinentes sur plusieurs canaux.

### [!DNL Profile] banque de données

Although [!DNL Real-time Customer Profile] processes ingested data and uses Adobe Experience Platform [!DNL Identity Service] to merge related data through identity mapping, it maintains its own data in the [!DNL Profile] store. En d’autres termes, le [!DNL Profile] magasin est séparé des [!DNL Catalog] données ([!DNL Data Lake]) et [!DNL Identity Service] des données (graphique d’identité).

### [!DNL Profile] et [!DNL Platform] services

The relationship between [!DNL Real-time Customer Profile] and other services within [!DNL Experience Platform] is highlighted in the following diagram:

![La relation entre Profile et les autres services Experience Platform.](images/profile-overview/profile-in-platform.png)

### Profils et données d’enregistrement

Un profil est une représentation d’un sujet, d’une organisation ou d’un individu, également appelé données d’enregistrement. Par exemple, le profil d’un produit peut inclure un SKU et une description, tandis que le profil d’une personne contient des informations telles que le prénom, le nom et l’adresse électronique. Using [!DNL Experience Platform], you can customize profiles to use types of data relevant to your business. The standard [!DNL Experience Data Model] (XDM) [!DNL Individual Profile] class is the preferred class upon which to build a schema when describing customer record data, and supplies the data integral to many interactions between Platform services. For more information on working with schemas in [!DNL Experience Platform], please begin by reading the [XDM System overview](../xdm/home.md).

### Événements de série temporelle

Les données de série temporelle fournissent un instantané du système au moment où une action a été entreprise, directement ou indirectement, par un sujet, ainsi que des données détaillant l’événement lui-même. Représentées par la classe de schéma standard XDM ExperienceEvent, les données de série temporelle peuvent décrire des événements tels que l’ajout d’articles à un panier, l’utilisation de liens et la lecture de vidéos. Vous pouvez utiliser les données de série temporelle pour établir des règles de segmentation et consulter les événements individuellement dans le cadre d’un profil.

### Identités

Toutes les entreprises souhaitent s’adresser à leurs clients de manière personnalisée. Cependant, l’un des défis que représente la proposition d’expériences numériques pertinentes aux clients consiste à trouver un moyen de relier leurs données déconnectées. Celles-ci sont souvent réparties sur différents canaux numériques tels que les tablettes, les téléphones mobiles et les ordinateurs portables. [!DNL Identity Service] vous permet de dresser le portrait complet de votre client en reliant les identités de plusieurs canaux et en créant un graphique d’identités pour chaque client, ce qui vous permet de mieux les connaître. Consultez la [présentation d’Identity Service](../identity-service/home.md) pour en savoir plus.

### Segmentation

Adobe Experience Platform [!DNL Segmentation Service] produces the audiences needed to power experiences for your individual customers. Lorsqu’un segment ciblé est créé, l’identifiant de ce segment est ajouté à la liste des adhésions au segment pour tous les profils admissibles. Segment rules are built and applied to [!DNL Real-time Customer Profile] data using RESTful APIs and the Segment Builder user interface. Pour en savoir plus sur la segmentation, commencez pas lire la [Présentation de Segmentation Service](../segmentation/home.md).

### Fragments de profil et schémas d’union {#profile-fragments-and-union-schemas}

One of the key features of [!DNL Real-time Customer Profile] is the ability to unify multi-channel data. When [!DNL Real-time Customer Profile] is used to access an entity, it can supply you with a merged view of all profile fragments for that entity across datasets, referred to as the union view and made possible through what is known as a union schema. [!DNL Real-time Customer Profile]Les données sont fusionnées entre les sources lorsqu’une entité ou un profil est consulté à l’aide de son identifiant ou exporté sous forme de segment. Pour en savoir plus sur l’accès aux profils et aux vues d’union à l’aide de l’ [!DNL Real-time Customer Profile] API, consultez le guide [des points de terminaison](api/entities.md)entités.

### Stratégies de fusion

When bringing data together from multiple sources and combining it in order to see a complete view of each of your individual customers, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create that unified view. À l’aide d’API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre organisation dans l’interface utilisateur. Pour plus d’informations sur l’utilisation des stratégies de fusion à l’aide de l’ [!DNL Real-time Customer Profile] API, consultez le guide [des points de terminaison des stratégies de](api/merge-policies.md)fusion. To work with merge policies using the [!DNL Experience Platform] UI, refer to the [merge policies user guide](ui/merge-policies.md).

### (Alpha) Configuration des attributs calculés

>[!IMPORTANT]
>Ce document décrit la version alpha de la fonctionnalité des attributs calculés. La documentation et les fonctionnalités peuvent changer.

Les attributs calculés vous permettent de calculer automatiquement la valeur des champs en fonction d’autres valeurs, calculs et expressions. Les attributs calculés fonctionnent au niveau du profil, ce qui signifie que vous pouvez agréger des valeurs sur tous les enregistrements et tous les événements. Chaque attribut calculé contient une expression, ou « règle », qui évalue les données entrantes et stocke la valeur obtenue dans un attribut de profil ou dans un événement. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat de durée de vie, le temps écoulé entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que ces informations sont nécessaires. Pour plus d’informations sur les attributs calculés et des instructions détaillées sur leur utilisation à l’aide de l’ [!DNL Real-time Customer Profile] API, consultez le guide [des points de terminaison des attributs](api/computed-attributes.md)calculés. Ce guide vous aidera à mieux comprendre le rôle que jouent les attributs calculés dans l’Adobe Experience Platform et il inclut des exemples d’appels d’API pour effectuer des opérations CRUD de base.

## Composants en temps réel

This section introduces the components that allow [!DNL Real-time Customer Profile] to update and monitor record and time series data in real-time.

### Ingestion par flux et segmentation par flux

L’entrée en temps réel est possible grâce à un processus appelé ingestion par flux. As profile and time series data is ingested, [!DNL Real-time Customer Profile] automatically decides to include or exclude that data from segments through an ongoing process called streaming segmentation, before merging it with existing data and updating the union view. Par conséquent, vous pouvez instantanément effectuer des calculs et prendre des décisions pour offrir aux clients de meilleures expériences personnalisées lorsqu’ils interagissent avec votre marque. Lors de l’ingestion, les données sont également soumises à un processus de validation pour s’assurer qu’elles sont correctement ingérées et conformes au schéma sur lequel le jeu de données est basé. Pour plus d’informations sur la validation effectuée lors de l’ingestion, commencez par lire la [présentation de la qualité d’ingestion des données](../ingestion/quality/overview.md).

### Configurations et destinations de projection Edge

Afin d’offrir à vos clients des expériences coordonnées, cohérentes et personnalisées sur plusieurs canaux en temps réel, les bonnes données doivent être facilement disponibles et mises à jour en continu, au fur et à mesure des changements. Adobe Experience Platform permet cet accès aux données en temps réel grâce à l’utilisation de ce que l’on appelle les périphéries. Une périphérie est un serveur réparti géographiquement qui stocke les données et les rend facilement accessibles aux applications. Par exemple, les applications Adobe telles qu’Adobe Target et Adobe Campaign utilisent des périphéries afin d’offrir des expériences client personnalisées en temps réel. Les données sont acheminées vers une périphérie par projection, une destination de projection définissant la périphérie vers laquelle les données sont envoyées, et une configuration de projection définissant les informations spécifiques rendues disponibles dans la périphérie. Pour en savoir plus et commencer à utiliser les projections à l&#39;aide de l&#39; [!DNL Real-time Customer Profile] API, consultez le guide [des points de terminaison de projection](api/edge-projections.md)de périphérie.

## Add data to [!DNL Real-time Customer Profile]

[!DNL Platform]Vous pouvez configurer pour envoyer vos données d’enregistrement et de série temporelle à , compatible avec l’ingestion par flux et l’ingestion par lots en temps réel. [!DNL Profile] Pour plus d’informations, consultez le tutoriel décrivant comment [ajouter des données à Real-time Customer Profile](tutorials/add-profile-data.md).

>[!NRemarque]
>Les données collectées par le biais de solutions d&#39;Adobe, y compris [!DNL Analytics Cloud], [!DNL Marketing Cloud]et [!DNL Advertising Cloud], se déversent dans [!DNL Experience Platform] et sont ingérées dans [!DNL Profile].

### [!DNL Profile] mesures d’assimilation

Observability Insights vous permet d’afficher les mesures clés dans Adobe Experience Platform. In addition to [!DNL Platform] usage statistics and performance indicators for various [!DNL Platform] functionalities, there are specific [!DNL Profile]-related metrics that allow you to gain insight into incoming request rates, successful ingestion rates, ingested record sizes, and more. Pour en savoir plus, commencez par lire la [présentation d’Observability Insights](../observability/home.md)[!DNL Profile] et pour obtenir une liste complète des mesures de , consultez la documentation sur les [mesures disponibles](../observability/metrics.md).

## [!DNL Data governance] et [!DNL Privacy]

[!DNL Data governance] est une série de stratégies et de technologies utilisées pour gérer les données client et assurer le respect des règlements, restrictions et politiques applicables à l&#39;utilisation des données.

As it relates to accessing data, data governance plays a key role within [!DNL Experience Platform] at various levels:
* Application de libellés d’utilisation des données
* Stratégies d’accès aux données
* Contrôle de l’accès aux données pour les actions marketing

[!DNL Data governance] est géré à plusieurs points. These include deciding what data is ingested into [!DNL Platform] and what data is accessible after ingestion for a given marketing action. Pour plus d’informations, commencez par lire la [présentation de la gouvernance des données](../data-governance/home.md).

### Gestion des demandes d’exclusion et de confidentialité des données

[!DNL Experience Platform] permet à vos clients d’envoyer des demandes d’exclusion liées à l’utilisation et à l’enregistrement de leurs données dans [!DNL Real-time Customer Profile]. Pour plus d’informations sur la gestion des demandes d’exclusion, consultez la documentation sur le [respect des demandes d’exclusion](../segmentation/honoring-opt-outs.md).

## [!DNL Profile] directives

[!DNL Experience Platform] a une série de lignes directrices à suivre afin d&#39;utiliser efficacement [!DNL Profile].

| Section | Limite |
| ------- | -------- |
| [!DNL Profile] schéma union | Un maximum de **20** jeux de données peut contribuer au schéma [!DNL Profile] d’union. |
| Relations multientités | Il est possible de créer un maximum de **5** relations multientités. |
| Profondeur JSON pour l’association à plusieurs entités | La profondeur maximale de JSON est de **4**. |
| Données de la série chronologique | Les données de séries chronologiques **ne sont pas** autorisées dans [!DNL Profile] les entités autres que les personnes. |
| Relations de schéma avec des non-personnes | Les relations de schéma avec des non-personnes **ne sont pas** autorisées. |
| Fragment de Profil | La taille maximale recommandée d’un fragment de profil est de **10 ko**.<br><br> La taille maximale absolue d’un fragment de profil est de **1 Mo**. |
| Entité non-personne | La taille totale maximale pour une seule entité non-personne est de **200 Mo**. |
| Jeu de données par entité non-personne | Un maximum de **1** jeux de données peut être associé à une entité non-personne. |

<!--
| Section | Boundary | Enforcement |
| ------- | -------- | ----------- |
| Profile union schema | A maximum of **20** datasets can contribute to the Profile union schema. | A message stating you've reached the maximum number of datasets appears. You must either disable or clean up other obsolete datasets in order to create a new dataset. |
| Multi-entity relationships | A maximum of **5** multi-entity relationship can be created. | A message stating all available mappings have been used appears when the fifth relationship is mapped. An error message letting you know you have exceeded the number of available mappings appears when attempting to map a sixth relationship. | 
| JSON depth for multi-entity association | The maximum JSON depth is **4**. | When trying to use the relationship selector with a field that is more than four levels deep, an error message appears, stating it is ineligible for multi-entity association. |
| Time series data | Time-series data is **not** permitted in Profile for non-people entities. | A message stating that this data cannot be enabled for Profile because it is of an unsupported type appears. |
| Non-people schema relationships | Non-people schema relationships are **not** permitted. | Relationships between two non-people schemas cannot be created. The relationships checkbox will be disabled. |
| Profile fragment | The recommended maximum size of a profile fragment is **10kB**.<br><br> The absolute maximum size of a profile fragment is **1MB**. | If you upload a fragment that is larger than 10kB, a warning appears, stating that performance may be degraded since the fragment exceeds the recommended maximum working size.<br><br> If you upload a fragment that is larger than 1MB, ingestion will fail, and an alert letting you know that records have failed will be sent. |
| Non-person entity | The maximum total size for a single non-person entity is **200MB**. | If you load an object as a non-person entity that is larger than 200MB, an alert will appear, stating that the entity has exceeded the maximum allowable size and will not be useable for segmentation. |
| Datasets per non-person entity | A maximum of **1** dataset can be associated to a non-person entity. | If you try to create a second dataset that is associated to the same non-person entity, an error appears, stating that only one dataset can be active per non-person entity. |

--->

>[!NOTE]
>
>
>Une entité non-personne fait référence à toute classe XDM qui **ne fait pas** partie de [!DNL Profile].

## Étapes suivantes et ressources supplémentaires

To learn more about [!DNL Real-time Customer Profile], please continue reading the documentation and supplement your learning by watching the video below or exploring other [Experience Platform video tutorials](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html).

>[!WARNING]
>L’ [!DNL Platform] interface utilisateur affichée dans la vidéo suivante est obsolète. Consultez le guide [d&#39;utilisation du Profil client en temps](ui/user-guide.md) réel pour obtenir les dernières captures d&#39;écran et fonctionnalités de l&#39;interface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)