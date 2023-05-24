---
keywords: Experience Platform;accueil;rubriques les plus consultées;XDM;système XDM;XDM individual profile;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience event;groupes de Champs;groupe de champs;groupe de Champs;Experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevenet;modèle de données d’expérience;modèle de données d’Expérience;Modèle de Données d’Expérience;modèle de données; Modèle de Données;registre des schémas;Registre des Schémas;bibliothèque de schémas;Bibliothèque de Schémas;schéma;données d’enregistrement;série temporelle;série temporelle
solution: Experience Platform
title: Présentation du système XDM
description: La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. Le modèle de données d’expérience (XDM), optimisé par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 100%

---

# Présentation du système XDM

La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. Le modèle de données [!DNL Experience Data Model] d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences digitales. Elle fournit des structures et des définitions communes qui permettent à chaque application de communiquer avec les services Platform. L’adhésion aux normes XDM permet d’intégrer toutes les données d’expérience client dans une représentation commune afin de fournir des informations de manière plus rapide et intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des audiences de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

XDM est le cadre de base qui permet à Adobe Experience Cloud, optimisé par Experience Platform, de transmettre le message approprié à la bonne personne, sur le bon canal et exactement au bon moment. La méthodologie sur laquelle Experience Platform repose, à savoir le système XDM, rend les schémas [!DNL Experience Data Model] opérationnels pour qu’ils soient utilisés par les services de Platform.

Ce document offre une vue d’ensemble du rôle du système XDM dans Experience Platform.

## Schémas XDM

Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit.

Avant que les données puissent être ingérées dans Platform, il est nécessaire de composer un schéma pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenues dans chaque champ. Les schémas se composent d’une classe de base et de zéro ou plusieurs groupes de champs.

Pour plus d’informations sur le modèle de composition de schémas, y compris sur les principes de conception et les bonnes pratiques, consultez les [bases de la composition de schémas](schema/composition.md).

### Composants XDM standard

XDM fournit une solide collection de groupes de champs et de types de données standard, destinés à capturer des concepts et des cas d’utilisation courants dans différents secteurs d’activité. Experience Platform vous permet de filtrer ces composants par secteur d’activité afin de créer rapidement et en toute confiance des schémas qui répondent au mieux à vos besoins.

Lors de la création de schémas dans l’interface utilisateur d’Experience Platform, les groupes de champs répertoriés s’affichent avec une mesure de popularité. Cette mesure est déterminée par la fréquence à laquelle les autres utilisateurs de Platform utilisent le groupe de champs dans leurs schémas. Plus le nombre est élevé, plus le groupe de champs est populaire. Par défaut, les résultats s’affichent du plus populaire au moins populaire, vous renseignant sur les tendances de modélisation des données dans votre secteur d’activité.

![Popularité du groupe de champs](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform fournit une interface utilisateur et une API RESTful à partir desquelles vous pouvez afficher et gérer toutes les ressources liées aux schémas de **[!DNL Schema Library]** d’Experience Platform. La [!DNL Schema Library] possède des composants XDM standard mis à votre disposition par Adobe, ainsi que des ressources de partenaires Experience Platform et de fournisseurs dont vous utilisez les applications.

En utilisant le [!DNL Schema Registry API] ou l’espace de travail [!UICONTROL Schémas] dans l’interface utilisateur de Platform, vous pouvez également créer et gérer de nouveaux schémas et de nouvelles ressources propres à votre entreprise.

Pour plus d’informations sur la gestion et l’interaction avec les schémas dans Platform, consultez la documentation suivante :

* [Guide de l’interface utilisateur XDM](./ui/overview.md)
* [Guide du registre des schémas API](./api/overview.md)

## Comportements de données dans le système XDM {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="Comportements des données"
>abstract="Les données destinées à Experience Platform sont regroupées en trois types de comportements : enregistrement, série temporelle et ad hoc. Les schémas d’enregistrement fournissent des informations sur les attributs d’un objet, tandis que les schémas de série temporelle capturent un instantané du système au moment où une action a été effectuée. Les schémas ad hoc capturent les champs qui sont des espaces de noms, à des fins d’utilisation par un jeu de données unique. Pour plus d’informations sur le comportement des données dans Platform, consultez la documentation."

Les données pouvant être utilisées dans Experience Platform sont regroupées selon trois types de comportements :

* **Enregistrement** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **Série temporelle** : fournit un instantané du système au moment où une action a été entreprise directement ou indirectement par un sujet enregistré.
* **Ad hoc** : capture les champs dont l’espace de noms n’est utilisable que par un seul jeu de données. Les schémas ad hoc sont utilisés dans plusieurs workflows d’ingestion de données pour Experience Platform, notamment dans l’ingestion de fichiers CSV et dans la création de certains types de connexions sources.

Tous les schémas XDM décrivent des données pouvant être catégorisées en tant qu’enregistrement ou série temporelle. Le comportement des données d’un schéma est défini par la classe du schéma attribuée à celui-ci lorsqu’il est créé pour la première fois. Les classes XDM décrivent le plus petit nombre de propriétés qu’un schéma doit contenir pour représenter un comportement de données spécifique.

Bien que vous puissiez définir vos propres classes dans le [!DNL Schema Registry], il est recommandé d’utiliser les classes standard **[!UICONTROL XDM Individual Profile]** et **[!UICONTROL XDM ExperienceEvent]** pour les données d’enregistrement et de série temporelle, respectivement. Ces classes sont décrites plus en détail ci-dessous.

>[!NOTE]
>
>Il n’existe aucune classe standard basée sur le comportement ad hoc. Les schémas ad hoc sont générés automatiquement par les processus Platform qui les utilisent, mais ils peuvent également être [créés manuellement à l’aide du registre des schémas API](./tutorials/ad-hoc.md).

### [!UICONTROL XDM Individual Profile] {#xdm-individual-profile}

[!UICONTROL XDM Individual Profile] est une classe basée sur les enregistrements qui forme une représentation singulière des attributs des sujets identifiés et partiellement identifiés.  Les profils hautement identifiés peuvent être utilisés pour des communications personnelles ou des engagements ciblés et peuvent contenir des informations personnelles détaillées telles que le nom, le genre, la date de naissance, l’adresse et les coordonnées, y compris les numéros de téléphone et les adresses e-mail.

Les profils moins identifiés peuvent n’être constitués que de signaux comportementaux anonymes tels que les cookies de navigateur. Dans ce cas, les données de profil éparses sont utilisées pour constituer une base d’informations dans laquelle les intérêts et les préférences du profil anonyme sont rassemblés et stockés. Ces identifiants peuvent devenir plus détaillés avec le temps si le sujet s’inscrit pour recevoir des notifications, souscrit à des abonnements, effectue des achats, etc. Ce développement des attributs de profil peut permettre d’obtenir un sujet identifié et un degré plus élevé d’engagement ciblé.

Au fur et à mesure qu’un profil croît, il devient un solide référentiel des informations personnelles, des informations d’identification, des coordonnées et des préférences de communication d’une personne.

Pour plus d’informations sur la structure et le cas d’utilisation des champs fournis par la classe, consultez le [[!UICONTROL guide de référence XDM Individual Profile]](./classes/individual-profile.md).

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent est une classe basée sur une série temporelle utilisée pour capturer l’état du système lorsqu’un événement (ou un ensemble d’événements) se produit, y compris le moment et l’identité du sujet concerné. Les événements d’expérience sont des enregistrements factuels non modifiables de ce qui s’est produit à un moment précis, reprenant les faits sans aucune agrégation ni interprétation. Ils sont essentiels à l’analyse du domaine temporel, puisqu’ils peuvent être utilisés pour analyser les modifications survenant au cours d’une période donnée et pour comparer plusieurs périodes afin de suivre les tendances.

Les événements d’expérience peuvent être explicites ou implicites. Les événements explicites sont des actions humaines directement observables qui ont lieu à un moment donné d’un parcours. Les événements implicites se produisent sans action humaine directe, mais restent liés à un individu. Les événements implicites incluent, par exemple, l’envoi planifié de newsletters par e-mail ou l’arrivée d’une batterie à un certain seuil de tension.

Bien qu’il ne soit pas facile de classer tous les événements de toutes les sources de données, il est extrêmement utile d’harmoniser les événements similaires en les groupant par types similaires quand cela est possible pour le traitement.

![Parcours client ExperienceEvent](images/overview/experience-event-journey.png)

Pour plus d’informations sur la structure et le cas d’utilisation des champs fournis par la classe, consultez le [[!UICONTROL guide de référence XDM ExperienceEvent]](./classes/experienceevent.md).

## Schémas XDM et services Experience Platform

Experience Platform est compatible avec les schémas, ce qui signifie que tout schéma conforme au standard XDM est mis à disposition des services Platform. Les modalités d’utilisation des schémas par les différents services Platform sont décrites plus en détail ci-dessous.

### Service de catalogue, ingestion de données et lac de données

Le service de catalogue est le système d’enregistrement des fichiers d’Experience Platform et des schémas qui lui sont associés. Le catalogue ne contient pas les fichiers ou les répertoires de données, mais plutôt les métadonnées et les descriptions de ces fichiers et répertoires.

Les données du catalogue sont stockées dans le lac de données, une banque de données hautement granulaire contenant toutes les données gérées par Platform, quels qu’en soient l’origine ou le format.

Pour commencer l’ingestion de données dans Experience Platform, vous pouvez utiliser le service de catalogue pour créer un jeu de données. Le jeu de données fait référence à un schéma XDM qui décrit la structure des données à ingérer. Si un jeu de données est créé sans schéma, Experience Platform crée alors un « schéma observé » en examinant le type et le contenu des champs de données ingérés. Les jeux de données sont ensuite suivis dans le catalogue et stockés dans le lac de données avec les schémas et les schémas observés sur lesquels ils sont basés.

Pour plus d’informations sur le catalogue, consultez la [présentation du service de catalogue](../catalog/home.md). Pour plus d’informations sur Adobe Experience Platform Data Ingestion, consultez la [présentation de Data Ingestion](../ingestion/home.md).

### Query Service

Adobe Experience Platform Query Service vous permet d’utiliser le langage SQL standard pour interroger les données d’Experience Platform afin de prendre en charge de nombreux cas d’utilisation différents.

Une fois qu’un schéma a été composé et qu’un jeu de données faisant référence à ce schéma a été créé, les données sont ingérées et stockées dans le lac de données. Grâce à Query Service, vous pouvez joindre n’importe quel jeu de données du lac de données et capturer les résultats de la requête sous forme de nouveau jeu de données à utiliser dans la création de rapports, dans le cadre du machine learning ou pour une ingestion dans le profil client en temps réel.

Pour plus d’informations sur le service, consultez la [présentation de Query Service](../query-service/home.md).

### Profil client en temps réel

Le profil client en temps réel fournit un profil de consommateur centralisé pour une gestion d’expérience ciblée et personnalisée. Chaque profil contient des données agrégées sur tous les systèmes ainsi que des comptes horodatés exploitables d’événements impliquant les personnes concernées par l’un des systèmes que vous utilisez avec Experience Platform.

Le profil client en temps réel utilise des données sous forme de schémas basées sur les classes [!UICONTROL XDM Individual Profile] ou [!UICONTROL XDM ExperienceEvent], et répond aux requêtes en fonction de ces données. Le profil ne prend pas en charge l’utilisation de schémas basés sur d’autres classes.

Le système conserve une instance de chaque profil client, fusionnant les données pour former une « source unique de vérité » pour l’individu. Ces données unifiées sont représentées par un « schéma d’union »; (parfois appelé « vue d’union »;). Un schéma d’union agrège les champs de tous les schémas qui mettent en œuvre la même classe dans un seul et même schéma.  Lors de la composition d’un schéma à l’aide de l’interface utilisateur ou d’une API, vous pouvez l’activer pour une utilisation avec le profil client en temps réel et l’étiqueter pour l’inclure à l’union. Le schéma balisé participe alors à la définition de schéma transmise à Profil.

Alors que les données [!UICONTROL XDM Individual Profile] et [!UICONTROL XDM ExperienceEvent] sont ingérées dans le lac de données, le profil client en temps réel ingère quant à lui toutes les données qui ont été activées pour son utilisation. Plus la quantité d’interactions et de détails ingérés est élevée, plus les profils deviennent robustes.

Les données [!UICONTROL XDM Individual Profile] permettent de guider et d’exécuter les actions sur n’importe quel canal ou intégration de produit Adobe. Associées à un riche historique de données sur les comportements et les interactions, ces données peuvent être utilisées pour alimenter le machine learning. L’API Real-Time Customer Profile peut aussi être utilisée pour enrichir les fonctionnalités des solutions tierces, des solutions CRM et des solutions propriétaires.

Pour plus d’informations, consultez la [vue d’ensemble du profil client en temps réel](../profile/home.md).

### Espace de travail de science des données

L’espace de travail de science des données d’Adobe Experience Platform utilise le machine learning et l’intelligence artificielle pour obtenir des informations à partir des données stockées dans Experience Platform. L’espace de travail de science des données permet aux spécialistes des données de créer des recettes basées sur des données [!UICONTROL XDM Individual Profile] et [!UICONTROL XDM ExperienceEvent] concernant les clients et leurs activités, ce qui facilite les prédictions telles que la propension d’achat et les offres recommandées que l’individu est susceptible d’apprécier et de saisir.

Avec l’espace de travail de science des données, les spécialistes des données peuvent facilement créer des API de service intelligents optimisés par le machine learning. Ces services fonctionnent avec d’autres solutions Adobe, y compris Adobe Target et Adobe Analytics Cloud, pour vous aider à automatiser les expériences digitales ciblées et personnalisées.

Pour plus d’informations sur l’utilisation des données d’Experience Platform pour alimenter les insights, consultez la [présentation de l’espace de travail de science des données](../data-science-workspace/home.md).

## Étapes suivantes et ressources supplémentaires

Maintenant que vous comprenez mieux le rôle des schémas dans Experience Platform, vous êtes prêt à commencer à composer le vôtre.

Pour en savoir plus sur les principes de conception et les bonnes pratiques pour composer des schémas à utiliser avec Experience Platform, commencez par lire les [bases de la composition des schémas](schema/composition.md). Pour obtenir des instructions étape par étape sur la création d’un schéma, consultez les tutoriels sur la création d’un schéma [à l’aide de l’API](tutorials/create-schema-api.md) ou [de l’interface utilisateur](tutorials/create-schema-ui.md).

Pour mieux comprendre le [!DNL XDM System] dans Experience Platform, regardez la vidéo suivante :

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
