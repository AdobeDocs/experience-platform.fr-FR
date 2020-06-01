---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Présentation du profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: 86fe1f407afb24d7222cff51cf9937a42571fd54
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 2%

---


# Présentation du profil client en temps réel

Adobe Experience Platform vous permet de proposer à vos clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Grâce au Profil client en temps réel, vous pouvez voir une vue holistique de chaque client qui combine les données de plusieurs canaux, y compris les données en ligne, hors ligne, CRM et tierces. Le profil vous permet de consolider vos diverses données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client. Cette présentation vous aidera à comprendre le rôle et l’utilisation du Profil client en temps réel dans la plate-forme d’expérience.

## Comprendre le Profil client en temps réel

Le Profil client en temps réel est un magasin d’entités de recherche générique qui fusionne les données de divers actifs de données d’entreprise, puis fournit l’accès à ces données sous la forme de profils clients individuels et de événements de séries chronologiques connexes. Cette fonctionnalité permet aux spécialistes du marketing de proposer des expériences coordonnées, cohérentes et pertinentes avec leurs audiences sur plusieurs canaux.

### Stockage de données de Profil

Bien que le Profil client en temps réel traite les données imbriquées et utilise Adobe Experience Platform Identity Service pour fusionner les données associées par le biais du mappage d’identité, il conserve ses propres données dans le magasin de Profils. En d’autres termes, le magasin de Profils est distinct des données du catalogue (Data Lake) et des données du service d’identité (graphique d’identité).

### Services de Profil et de plate-forme

La relation entre le Profil client en temps réel et d’autres services dans la plate-forme d’expérience est mise en évidence dans le diagramme suivant :

![Relation entre le Profil et d’autres services Experience Platform.](images/profile-overview/profile-in-platform.png)

### Profils et enregistrements de données

Un profil est la représentation d&#39;un sujet, d&#39;une organisation ou d&#39;un individu, également appelé données d&#39;enregistrement. Par exemple, le profil d’un produit peut inclure un SKU et une description, tandis que le profil d’une personne contient des informations telles que le prénom, le nom et l’adresse électronique. Avec Experience Platform, vous pouvez personnaliser des profils pour utiliser des types de données pertinentes pour votre entreprise. La classe de Profil de modèle de données d’expérience standard (XDM) est la classe privilégiée sur laquelle construire un schéma pour décrire les données d’enregistrement client et fournit les données qui font partie intégrante de nombreuses interactions entre les services de plateforme. Pour plus d’informations sur l’utilisation des schémas dans Experience Platform, veuillez commencer par lire la présentation [du système](../xdm/home.md)XDM.

### événements de séries chronologiques

Les données de séries chronologiques fournissent un instantané du système au moment où une action a été entreprise, directement ou indirectement, par un sujet, ainsi que des données détaillant le événement lui-même. Représentées par la classe de schéma standard XDM ExperienceEvent, les données de série chronologique peuvent décrire des événements tels que des éléments ajoutés à un panier, des liens sur lesquels l’utilisateur clique et des vidéos visionnées. Les données de séries chronologiques peuvent être utilisées pour baser les règles de segmentation sur et les événements peuvent être accessibles individuellement dans le contexte d’un profil.

### Identités

Chaque entreprise veut communiquer avec ses clients d&#39;une manière qui lui semble personnelle. Cependant, l&#39;un des défis à relever pour fournir aux clients des expériences numériques pertinentes est de comprendre comment lier leurs données déconnectées, qui sont souvent réparties sur différents canaux numériques tels que tablettes, téléphones portables et ordinateurs portables. Identity Service vous permet de rassembler l&#39;image complète de votre client en liant les identités de plusieurs canaux, en créant un graphique d&#39;identité pour chaque client, ce qui vous permet de mieux les comprendre. Pour plus d&#39;informations, consultez la présentation [du service](../identity-service/home.md) d&#39;identité.

### Segmentation

Adobe Experience Platform Segmentation Service produit les audiences nécessaires à l’alimentation de vos clients individuels. Lorsqu’un segment d’audience est créé, l’ID de ce segment est ajouté à la liste des adhésions de segment pour tous les profils admissibles. Les règles de segmentation sont créées et appliquées aux données du Profil client en temps réel à l’aide des API RESTful et de l’interface utilisateur du créateur de segments. Pour en savoir plus sur la segmentation, lisez tout d’abord la présentation [du service de](../segmentation/home.md)segmentation.

### Fragments de Profil et schémas d’union {#profile-fragments-and-union-schemas}

L’une des principales caractéristiques du Profil client en temps réel est la possibilité d’unifier les données à canaux multiples. Lorsque le Profil client en temps réel est utilisé pour accéder à une entité, il peut vous fournir une vue fusionnée de tous les fragments de profil pour cette entité entre les jeux de données, appelés vue d&#39;union, et rendue possible par ce qu&#39;on appelle un schéma d&#39;union. Les données du Profil client en temps réel sont fusionnées entre les sources lorsqu’une entité ou un profil est accessible par son identifiant ou exporté en tant que segment. Pour en savoir plus sur l’accès aux profils et aux vues d’union, consultez le sous-guide du développeur API Profil client en temps réel sur les [entités, également appelé &quot;Accès au Profil&quot;](api/entities.md).

### Stratégies de fusion

Lorsque vous rassemblez des données provenant de plusieurs sources et les combinez afin d’obtenir une vue complète de chacun de vos clients, les stratégies de fusion sont les règles utilisées par Plateforme pour déterminer comment les données seront hiérarchisées et quelles données seront combinées pour créer cette vue unifiée. A l’aide des API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre entreprise. Pour plus d’informations sur l’utilisation des stratégies de fusion à l’aide des API, consultez le sous-guide [Stratégies de](api/merge-policies.md) fusion de l’API du Profil client en temps réel ou le guide [d’utilisateur des stratégies de](ui/merge-policies.md) fusion pour savoir comment utiliser les stratégies de fusion à l’aide de l’interface utilisateur de la plate-forme.

## (Alpha) Configurer des attributs calculés

>[!IMPORTANT]
>La fonctionnalité d&#39;attribut calculée décrite dans ce document est en alpha. La documentation et les fonctionnalités peuvent changer.

Les attributs calculés vous permettent de calculer automatiquement la valeur des champs en fonction d’autres valeurs, calculs et expressions. Les attributs calculés fonctionnent au niveau du profil, ce qui signifie que vous pouvez agrégat des valeurs sur tous les enregistrements et événements. Chaque attribut calculé contient une expression, ou &quot;règle&quot;, qui évalue les données entrantes et stocke la valeur résultante dans un attribut de profil ou dans un événement. Ces calculs vous permettent de répondre facilement aux questions relatives à des éléments tels que la valeur d’achat sur toute la durée de vie, le délai entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que les informations sont nécessaires. Pour plus d’informations sur les attributs calculés et des instructions détaillées sur leur utilisation, consultez le [sous-guide API Profil client en temps réel sur les attributs](api/computed-attributes.md)calculés. Ce guide vous aidera à mieux comprendre le rôle que jouent les attributs calculés dans la plateforme d’expérience Adobe et comprend des exemples d’appels d’API pour effectuer des opérations CRUD de base à l’aide de l’API Profil client en temps réel.

## Composants en temps réel

Cette section présente les composants qui permettent au Profil client en temps réel de mettre à jour et de surveiller les données d’enregistrement et de série chronologique en temps réel.

### Intégration en flux continu et segmentation en flux continu

L’entrée en temps réel est rendue possible par un processus appelé assimilation en flux continu. À mesure que les données de profil et de série chronologique sont ingérées, le Profil client en temps réel décide automatiquement d’inclure ou d’exclure ces données des segments par le biais d’un processus continu appelé segmentation en flux continu, avant de les fusionner avec les données existantes et de mettre à jour la vue d’union. En conséquence, vous pouvez instantanément effectuer des calculs et prendre des décisions pour fournir aux clients des expériences améliorées et individualisées lorsqu’ils interagissent avec votre marque. Lors de l’assimilation, les données sont également validées pour s’assurer qu’elles sont correctement ingérées et conformes au schéma sur lequel le jeu de données est basé. Pour plus d&#39;informations sur la validation effectuée lors de l&#39;assimilation, veuillez commencer par lire l&#39;aperçu [de la qualité d&#39;assimilation des](../ingestion/quality/overview.md)données.

### Projections Edge

Afin d’offrir des expériences coordonnées, cohérentes et personnalisées à vos clients sur plusieurs canaux en temps réel, les données appropriées doivent être facilement disponibles et mises à jour en continu au fur et à mesure des changements. La plate-forme Adobe Experience Platform permet cet accès en temps réel aux données à l’aide de ce que l’on appelle les arêtes. Un bord est un serveur géographiquement placé qui stocke les données et les rend facilement accessibles aux applications. Par exemple, les applications Adobe telles que Adobe Cible et Adobe Campaign utilisent des arêtes afin de fournir des expériences client personnalisées en temps réel. Les données sont acheminées vers un bord par une projection, avec une destination de projection qui définit le bord auquel les données seront envoyées et une configuration de projection qui définit les informations spécifiques qui seront rendues disponibles sur le bord. Pour en savoir plus et commencer à utiliser les arêtes et les projections, consultez le sous-guide [Projections](api/edge-projections.md)Edge de l&#39;API Profil client en temps réel.

## Ajouter les données au Profil client en temps réel

La plate-forme peut être configurée pour envoyer vos données d&#39;enregistrement et de série chronologique au Profil, en prenant en charge l&#39;assimilation en temps réel de flux continu et l&#39;assimilation par lot. Pour plus d’informations, voir le didacticiel qui décrit comment [ajouter des données au Profil](tutorials/add-profile-data.md)client en temps réel.

>[!Note] :
>Les données collectées par le biais des solutions Adobe, y compris Analytics Cloud, Marketing Cloud et Advertising Cloud, s’enchaînent dans la plate-forme d’expérience et sont ingérées dans le Profil.

### Mesures d’assimilation en flux continu Profil

Observability Insights vous permet d’exposer les mesures clés dans Adobe Experience Platform. Outre les statistiques d&#39;utilisation de la plate-forme et les indicateurs de performances de diverses fonctionnalités de la plate-forme, il existe des mesures spécifiques liées au Profil qui vous permettent d&#39;obtenir des informations sur les taux de demande entrants, les taux d&#39;assimilation réussis, les tailles d&#39;enregistrements assimilés, etc. Pour en savoir plus, lisez tout d’abord l’aperçu [des statistiques d’](../observability/home.md)observabilité et pour obtenir une liste complète des mesures de Profil, consultez la documentation sur les mesures [](../observability/metrics.md)disponibles.

## Gouvernance des données et confidentialité

La gouvernance des données est une série de stratégies et de technologies utilisées pour gérer les données des clients et assurer le respect des réglementations, restrictions et politiques applicables à l&#39;utilisation des données.

En ce qui concerne l’accès aux données, la gouvernance des données joue un rôle clé au sein de la plate-forme d’expérience à divers niveaux :
* Étiquetage de l’utilisation des données
* Stratégies d’accès aux données
* Contrôle d&#39;accès sur les données pour les actions marketing

La gouvernance des données est gérée à plusieurs points. Il s’agit notamment de décider quelles données sont incorporées dans la plate-forme et quelles données sont accessibles après l’assimilation pour une action marketing donnée. Pour plus d’informations, commencez par lire la présentation [de la gouvernance des](../data-governance/home.md)données.

### Gestion des demandes d’exclusion et de confidentialité des données

Experience Platform permet à vos clients d’envoyer des demandes d’exclusion liées à l’utilisation et à l’enregistrement de leurs données dans le Profil client en temps réel. Pour plus d’informations sur la façon dont les demandes d’exclusion sont traitées, consultez la documentation sur le [traitement des demandes](../segmentation/honoring-opt-outs.md)d’exclusion.

## Directives Profils

Experience Platform a une série de directives à suivre pour utiliser efficacement le Profil.

| Section | Limite |
| ------- | -------- |
| schéma union Profil | Un maximum de **20** jeux de données peut contribuer au schéma d&#39;union de Profil. |
| Relations multientités | Il est possible de créer un maximum de **5** relations multientités. |
| Profondeur JSON pour l’association à plusieurs entités | La profondeur maximale de JSON est de **4**. |
| Données de la série chronologique | Les données de séries chronologiques **ne sont pas** autorisées dans le Profil pour les entités non-personnes. |
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

>!![NOTE] Une entité non-personne fait référence à toute classe XDM qui **ne fait pas** partie du Profil.

## Étapes suivantes et ressources supplémentaires

Pour en savoir plus sur le Profil client en temps réel, veuillez continuer à lire la documentation fournie dans ce guide et compléter votre apprentissage en regardant la vidéo ci-dessous ou en explorant d’autres didacticiels [vidéo de la plateforme](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html)d’expérience.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)