---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Présentation du profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: 24380653fdae561d294453eaec753a863993dfaf

---


# Présentation du profil client en temps réel

Adobe Experience Platform vous permet d’offrir à vos clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Avec le  Client en temps réel, vous pouvez voir un holistique de chaque client qui combine les données de plusieurs , y compris les données en ligne, hors ligne, CRM et tierces. Le profil vous permet de consolider vos diverses données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client. Cette présentation vous aidera à comprendre le rôle et l’utilisation des  de clients en temps réel dans la plateforme d’expérience.

## Comprendre les  des clients en temps réel

Le de clients en temps réel est un magasin d’entités de recherche générique qui fusionne les données de divers actifs de données d’entreprise, puis fournit un accès à ces données sous la forme d’un de clients individuels et d’une série deséries chronologiques connexes.

Cette fonctionnalité permet aux spécialistes du marketing de générer des expériences coordonnées, cohérentes et pertinentes avec leurs   sur plusieurs, comme le montre la vidéo ci-dessous :

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12&enable10seconds=on&speedcontrol=on)

###  de données

Bien que le du client en temps réel traite les données imbriquées et utilise le service d’identité Adobe Experience Platform pour fusionner les données associées par le biais du mappage d’identité, il conserve ses propres données dans le magasin de  de. En d’autres termes, le magasin de  est distinct des données du catalogue (Data Lake) et du service d’identité (graphe d’identité).

### Services de  et de plateformes

La relation entre les  de clients en temps réel et d’autres services dans la plateforme d’expérience est mise en évidence dans le diagramme suivant :

![La relation entre  de et d’autres services Experience Platform.](images/profile-overview/profile-in-platform.png)

###  et enregistrement de données

Un  est une représentation d’un sujet, d’une organisation ou d’un individu, également appelé données d’enregistrement. Par exemple, le  d’un produit peut inclure un SKU et une description, tandis que le d’une personne contient des informations telles que son prénom, son nom et son adresse électronique.

Avec Experience Platform, vous pouvez personnaliser les  de pour utiliser des types de données pertinentes pour votre entreprise. La classe de  de modèle de données d’expérience standard (XDM) est la classe préférée sur laquelle construire un  pour décrire les données d’enregistrement des clients et fournit les données intégrées à de nombreuses interactions entre les services de plateforme. Pour plus d’informations sur l’utilisation des  dans Experience Platform, lisez d’abord la présentation [du système](../xdm/home.md)XDM.

### de séries chronologiques

Les données de série chronologique fournissent un instantané du système au moment où une action a été entreprise, directement ou indirectement, par un sujet, ainsi que des données détaillant le  lui-même. Représentées par la classe de  standard XDM ExperienceEvent, les données de série chronologique peuvent décrire des  tels que les éléments ajoutés à un panier, les liens sur lesquels l’utilisateur clique et les vidéos affichées.

Les données de série chronologique peuvent être utilisées pour baser les règles de segmentation sur et les  de peuvent être accessibles individuellement dans le contexte d’un  de segmentation.

### Identités

Chaque entreprise veut communiquer avec ses clients d&#39;une manière qui lui semble personnelle. Toutefois, l’un des défis de la diffusion d’expériences numériques pertinentes aux clients consiste à comprendre comment lier leurs données déconnectées, qui sont souvent réparties sur différents numériques, tels que les tablettes, les téléphones mobiles et les ordinateurs portables.

Identity Service vous permet de rassembler l&#39;image complète de votre client en liant les identités de plusieurs , en créant un graphique d&#39;identité pour chaque client, ce qui vous permet de mieux les comprendre. Consultez la présentation [du service](../identity-service/home.md) d’identité pour en savoir plus.

### Segmentation

Les règles de segmentation sont créées et appliquées aux données du client en temps réel à l’aide des API RESTful et de l’interface utilisateur du créateur de segments. Comme expliqué dans la vidéo suivante, le service de segmentation de plateforme d’expérience ADobe produit le   nécessaire pour alimenter les expériences client :

>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&enable10seconds=on&speedcontrol=on)

Lorsqu’un segment   est créé, l’ID de ce segment est ajouté au des abonnements de segments pour tous lesadmissibles. Pour en savoir plus sur la segmentation, lisez d’abord l’aperçu [du service de](../segmentation/home.md)segmentation.

###  fragments et   de

L’une des principales fonctionnalités du de clients en temps réel est la capacité d’unifier les données de  multi. Lorsque le du client en temps réel est utilisé pour accéder à une entité, il peut vous fournir un fusionné de tous les fragments de  de l’entité pour l’ensemble des jeux de données, appelé lede l’analyse de l’.

Les données  du client en temps réel sont fusionnées entre les sources lorsqu’une entité ou un  est accédé par son ID ou exporté en tant que segment. Pour en savoir plus sur l’accès aux  de et aux  de l’ [API d’, consultez le sous-guide en temps réel du développeur de l’API d’analyse des clients sur les](api/entities.md)entités, également appelé &quot;Accès aux&quot;.

### Stratégies de fusion

Lorsque vous rassemblez des données provenant de plusieurs sources et les combinez afin de voir un complet de chacun de vos clients, les stratégies de fusion sont les règles utilisées par Plateforme pour déterminer comment les données seront classées par priorité et quelles données seront combinées pour créer ce  de unifié.

A l’aide des API RESTful ou de l’interface utilisateur, vous pouvez créer des stratégies de fusion, gérer des stratégies existantes et définir une stratégie de fusion par défaut pour votre entreprise. Pour plus d’informations sur l’utilisation de stratégies de fusion à l’aide d’API, consultez le sous-guide [Stratégies de](api/merge-policies.md) fusion des API  client en temps réel ou le guide [utilisateur des stratégies de](ui/merge-policies.md) fusion pour savoir comment utiliser les stratégies de fusion à l’aide de l’interface utilisateur de la plateforme.

## Composants en temps réel

Cette section présente les composants qui permettent aux clients en temps réel de mettre à jour et de surveiller les données d’enregistrement et de série chronologique en temps réel.

### Exportation en flux continu et segmentation en flux continu

L’entrée en temps réel est rendue possible par un processus appelé ingestion en flux continu. À mesure que les données de  et de séries chronologiques sont ingérées, le client en temps réel décide automatiquement d’inclure ou d’exclure ces données des segments par le biais d’un processus continu appelé segmentation en flux continu, avant de les fusionner avec les données existantes et de mettre à jour ledela solution de base de données. Par conséquent, vous pouvez instantanément effectuer des calculs et prendre des décisions pour offrir aux clients des expériences personnalisées améliorées lorsqu’ils interagissent avec votre marque.

Lors de l’assimilation, les données sont également validées pour s’assurer qu’elles sont correctement ingérées et conformes au  sur lequel le jeu de données est basé. Pour plus d&#39;informations sur la validation effectuée lors de l&#39;ingestion, veuillez commencer par lire l&#39;aperçu [de la qualité d&#39;ingestion des](../ingestion/quality/overview.md)données.

### Projections Edge

Afin d’offrir des expériences coordonnées, cohérentes et personnalisées à vos clients sur plusieurs  en temps réel, les données appropriées doivent être facilement disponibles et mises à jour en permanence au fur et à mesure des changements. Adobe Experience Platform permet cet accès en temps réel aux données grâce à l’utilisation de ce que l’on appelle les contours.

Un bord est un serveur géographiquement placé qui stocke les données et les rend facilement accessibles aux applications. Par exemple, les applications Adobe telles qu’Adobe  et  Adobe Campaign utilisent des bords afin de fournir des expériences client personnalisées en temps réel. Les données sont acheminées vers un bord par une projection, avec une destination de projection définissant le bord auquel les données seront envoyées et une configuration de projection définissant les informations spécifiques qui seront rendues disponibles sur le bord.

Pour en savoir plus et commencer à utiliser les bords et les projections, consultez le sous-guide [Projections](api/edge-projections.md)Edge en temps réel du client  API.

## Gouvernance des données et confidentialité

La gouvernance des données est une série de stratégies et de technologies utilisées pour gérer les données des clients et assurer la conformité aux réglementations, restrictions et politiques applicables à l’utilisation des données.

En ce qui concerne l’accès aux données, la gouvernance des données joue un rôle clé au sein de la plateforme d’expérience à divers niveaux :
* Étiquetage de l’utilisation des données
* Stratégies d’accès aux données
*  sur les données pour les actions marketing

La gouvernance des données est gérée à plusieurs points. Il s’agit notamment de décider quelles données sont assimilées à une plateforme et quelles données sont accessibles après l’assimilation pour une action marketing donnée.

Pour plus d’informations, commencez par lire la présentation [de la gouvernance des](../data-governance/home.md)données.

### Gestion des demandes d’exclusion et de confidentialité des données

Experience Platform permet à vos clients d’envoyer des demandes d’exclusion liées à l’utilisation et   de leurs données dans le client en temps réel. Pour plus d’informations sur le traitement des demandes d’exclusion, consultez la documentation sur le [traitement des demandes](../segmentation/honoring-opt-outs.md)d’exclusion.

## Ajouter les données au client en temps réel 

La plateforme peut être configurée pour envoyer vos données d’enregistrement et de série chronologique aux , prenant en charge l’assimilation en temps réel de flux continu et l’assimilation par lots. Pour plus d’informations, reportez-vous au didacticiel décrivant comment [ajouter des données à la clientèle en temps réel](tutorials/add-profile-data.md).

>[!Note] :
>Les données collectées par le biais des solutions Adobe, notamment Analytics Cloud, Marketing Cloud et Advertising Cloud, s’enchaînent dans la plateforme d’expérience et sont assimilées à des  de.

## Création de segments  

La pierre angulaire de votre campagne marketing est votre  . Le de clients en temps réel fournit les outils pour segmenter votre base de clients en  composé de membres répondant aux critères précis dont vous avez besoin. Avec la segmentation, vous pouvez isoler  membres  à l’aide de critères tels que :

* Clients pour lesquels une semaine s’est écoulée depuis le dernier achat.
* Clients pour lesquels la somme des achats est supérieure à 10 000 euros.
* Clients qui ont vu un nombre défini de campagnes marketing uniques à partir d’un  prédéfini, spécifié par leur Campaign ID, et les ont explorées en 30 minutes.

Pour commencer avec la segmentation, reportez-vous à la présentation [de la](../segmentation/home.md)segmentation.

## (Alpha) Configuration des attributs calculés

>[!IMPORTANT]
>La fonctionnalité d’attribut calculé décrite dans ce est en alpha. La documentation et la fonctionnalité peuvent changer.

Les attributs calculés vous permettent de calculer automatiquement la valeur des champs en fonction d’autres valeurs, calculs et  de . Les attributs calculés fonctionnent au niveau  du, ce qui signifie que vous pouvez  des valeurs de sur tous les enregistrements et tous les.

Chaque attribut calculé contient un  de , ou &quot;règle&quot;, qui évalue les données entrantes et stocke la valeur résultante dans un attribut de ou dans un. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat sur la durée de vie, le délai entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que les informations sont nécessaires.

Pour plus d’informations sur les attributs calculés et pour obtenir des instructions détaillées sur leur utilisation, reportez-vous au [sous-guide en temps réel sur les attributs](api/computed-attributes.md)calculés de l’API  client. Ce guide vous aidera à mieux comprendre le rôle que jouent les attributs calculés dans Adobe Experience Platform. Il inclut des exemples d’appels d’API pour effectuer des opérations CRUD de base à l’aide de l’API  client en temps réel.