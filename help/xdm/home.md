---
keywords: Experience Platform;accueil;rubriques les plus consultées;XDM;système XDM;profil individuel XDM;XDM ExperienceEvent;XDM ExperienceEvent;experienceEvent;événement d’expérience;groupes de champs;groupe de champs;groupe de champs;événement d’expérience;événement d’expérience XDM;événement d’expérience XDM;événement d’expérience;événement d’expérience;événement d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience registre des schémas;registre des schémas;bibliothèque de schémas;bibliothèque de schémas;schéma;données d’enregistrement;série temporelle;série temporelle
solution: Experience Platform
title: Présentation du système XDM
topic-legacy: overview
description: La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. Le modèle de données d’expérience (XDM), optimisé par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 9fda5dad7b7e29c88598ff299c26277a015277a6
workflow-type: tm+mt
source-wordcount: '1993'
ht-degree: 55%

---

# Présentation du système XDM

>[!NOTE]
>
>Le terme &quot;mixin&quot; a été mis à jour vers le schéma &quot;groupe de champs&quot; pour promouvoir la compréhension. Les groupes de champs sont un ensemble de champs réutilisables pour prendre en charge les cas pratiques professionnels. Cette modification est désormais répercutée dans l’API Schema Registry, l’interface utilisateur de Adobe Experience Platform et dans toute la documentation Platform.

La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. Le [!DNL Experience Data Model] (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Il fournit des structures et des définitions communes qui permettent à toute application de communiquer avec les services Platform. L’adhésion aux normes XDM permet d’intégrer toutes les données d’expérience client dans une représentation commune afin de fournir des informations de manière plus rapide et intégrée. Vous pouvez obtenir des insights précieux à partir des actions des clients, définir des audiences de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

XDM est le cadre de base qui permet à Adobe Experience Cloud, optimisé par Experience Platform, de transmettre le message approprié à la bonne personne, sur le bon canal et exactement au bon moment. La méthodologie sur laquelle l’Experience Platform est construit, le système XDM, rend les schémas [!DNL Experience Data Model] opérationnels pour qu’ils soient utilisés par les services Platform.

Ce document offre une vue d’ensemble du rôle du système XDM dans Experience Platform.

## Schémas XDM

Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit.

Avant que les données puissent être ingérées dans Platform, il est nécessaire de composer un schéma pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenues dans chaque champ. Les schémas se composent d’une classe de base et de zéro ou plusieurs groupes de champs de schéma.

Pour plus d’informations sur le modèle de composition de schémas, y compris sur les principes de conception et les bonnes pratiques, consultez les [bases de la composition de schémas](schema/composition.md).

### Composants XDM standard

XDM fournit une solide collection de groupes de champs et de types de données standard, destinés à capturer des concepts et des cas d’utilisation courants dans différents secteurs d’activité. Experience Platform vous permet de filtrer ces composants par secteur d’activité, ce qui vous permet de créer rapidement et en toute confiance des schémas qui répondent le mieux à vos besoins.

Lors de la création de schémas dans l’interface utilisateur de l’Experience Platform, les groupes de champs répertoriés s’affichent avec une mesure de popularité. Cette mesure est déterminée par la fréquence à laquelle les autres utilisateurs de Platform utilisent le groupe de champs dans leurs schémas. Plus le nombre est élevé, plus le groupe de champs est populaire. Par défaut, les résultats s’affichent du plus populaire au moins populaire, ce qui vous permet de vous tenir informé des tendances de modélisation des données dans votre secteur d’activité.

![Popularité du groupe de champs](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform fournit une interface utilisateur et une API RESTful à partir desquelles vous pouvez afficher et gérer toutes les ressources liées aux schémas dans l’Experience Platform **[!DNL Schema Library]**. [!DNL Schema Library] contient des composants XDM standard mis à votre disposition par Adobe, ainsi que des ressources provenant de partenaires et de fournisseurs Experience Platform dont vous utilisez les applications.

À l’aide de l’espace de travail [!DNL Schema Registry API] ou [!UICONTROL Schémas] dans l’interface utilisateur de Platform, vous pouvez également créer et gérer de nouveaux schémas et ressources propres à votre organisation.

Pour plus d&#39;informations sur la gestion et l&#39;interaction avec les schémas dans Platform, consultez la documentation suivante :

* [Guide de l’interface utilisateur XDM](./ui/overview.md)
* [Guide de l’API Schema Registry](./api/overview.md)

## Comportements de données dans le système XDM {#data-behaviors}

Les données pouvant être utilisées dans Experience Platform sont regroupées selon deux types de comportements :

* **Enregistrer les données** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **Données de série temporelle** : Fournit un instantané du système au moment où une action a été entreprise directement ou indirectement par un sujet enregistré.

Tous les schémas XDM décrivent des données pouvant être catégorisées en tant qu’enregistrement ou série temporelle. Le comportement des données d’un schéma est défini par la classe du schéma attribuée à celui-ci lorsqu’il est créé pour la première fois. Les classes XDM décrivent le plus petit nombre de propriétés qu’un schéma doit contenir pour représenter un comportement de données spécifique.

Bien que vous puissiez définir vos propres classes dans [!DNL Schema Registry], il est recommandé d’utiliser les classes préférées **[!UICONTROL XDM Individual Profile]** et **[!UICONTROL XDM ExperienceEvent]** pour les données d’enregistrement et de série temporelle, respectivement. Ces classes sont décrites plus en détail ci-dessous.

### [!UICONTROL XDM Individual Profile] {#xdm-individual-profile}

[!UICONTROL XDM Individual Profile est une classe basée sur les enregistrements qui forme une représentation singulière des attributs des sujets identifiés et partiellement identifiés. ] Les profils hautement identifiés peuvent être utilisés pour des communications personnelles ou des engagements ciblés et peuvent contenir des informations personnelles détaillées telles que le nom, le genre, la date de naissance, l’adresse et les coordonnées, y compris les numéros de téléphone et les adresses électroniques.

Les profils moins identifiés peuvent n’être constitués que de signaux comportementaux anonymes tels que les cookies de navigateur. Dans ce cas, les données de profil éparses sont utilisées pour constituer une base d’informations dans laquelle les intérêts et les préférences du profil anonyme sont rassemblés et stockés. Ces identifiants peuvent devenir plus détaillés avec le temps si le sujet s’inscrit pour recevoir des notifications, souscrit à des abonnements, effectue des achats, etc. Ce développement des attributs de profil peut permettre d’obtenir un sujet identifié et un degré plus élevé d’engagement ciblé.

À mesure qu’un profil se développe, il devient un solide référentiel des informations personnelles, des informations d’identification, des coordonnées et des préférences de communication d’un individu.

Pour plus d’informations sur la structure et le cas d’utilisation des champs fournis par la classe, consultez le [[!UICONTROL Guide de référence XDM Individual Profile] ](./classes/individual-profile.md) .

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent est une classe basée sur une série temporelle utilisée pour capturer l’état du système lorsqu’un événement (ou un ensemble d’événements) se produit, y compris le moment et l’identité du sujet concerné. Les événements d’expérience sont des enregistrements factuels non modifiables de ce qui s’est produit à ce moment-là, représentant ce qui s’est produit sans agrégation ni interprétation. Ils sont essentiels à l’analyse du domaine temporel, puisqu’ils peuvent être utilisés pour analyser les modifications survenant au cours d’une période donnée et pour comparer plusieurs périodes afin de suivre les tendances.

Les événements d’expérience peuvent être explicites ou implicites. Les événements explicites sont des actions humaines directement observables qui ont lieu à un moment donné d’un parcours. Les événements implicites se produisent sans action humaine directe, mais restent liés à un individu. Les événements implicites incluent, par exemple, l’envoi planifié de newsletters par e-mail ou l’arrivée d’une batterie à un certain seuil de tension.

Bien qu’il ne soit pas facile de classer tous les événements de toutes les sources de données, il est extrêmement utile d’harmoniser les événements similaires en les groupant par types similaires quand cela est possible pour le traitement.

![Parcours client ExperienceEvent](images/overview/experience-event-journey.png)

Pour plus d’informations sur la structure et le cas d’utilisation des champs fournis par la classe, consultez le [[!UICONTROL guide de référence XDM ExperienceEvent]](./classes/experienceevent.md) .

## Schémas XDM et services Experience Platform

L’Experience Platform est indépendant des schémas, ce qui signifie que tout schéma conforme à la norme XDM est mis à la disposition des services Platform. Les modalités d’utilisation des schémas par les différents services Platform sont décrites plus en détail ci-dessous.

### Service de catalogue, ingestion de données et lac de données

Le service de catalogue est le système d’enregistrement des ressources d’Experience Platform et des schémas qui lui sont associés. Le catalogue ne contient pas les fichiers de données ou les répertoires réels, mais il contient plutôt les métadonnées et les descriptions de ces fichiers et répertoires.

Les données du catalogue sont stockées dans le lac de données, une banque de données hautement granulaire contenant toutes les données gérées par Platform, quels qu’en soient l’origine ou le format.

Pour commencer à ingérer des données dans Experience Platform, vous pouvez utiliser le service de catalogue pour créer un jeu de données. Le jeu de données fait référence à un schéma XDM qui décrit la structure des données à ingérer. Si un jeu de données est créé sans schéma, l’Experience Platform génère un &quot;schéma observé&quot; en examinant le type et le contenu des champs de données ingérés. Les ensembles de données sont ensuite suivis dans le catalogue et stockés dans le lac de données avec les schémas et les schémas observés sur lesquels ils sont basés.

Pour plus d’informations sur le catalogue, consultez la [présentation du service de catalogue](../catalog/home.md). Pour plus d’informations sur Adobe Experience Platform Data Ingestion, consultez la [présentation de Data Ingestion](../ingestion/home.md).

### Query Service

Adobe Experience Platform Query Service vous permet d’utiliser le langage SQL standard pour interroger les données d’Experience Platform afin de prendre en charge de nombreux cas d’utilisation différents.

Une fois qu’un schéma a été composé et qu’un jeu de données faisant référence à ce schéma a été créé, les données sont ingérées et stockées dans le lac de données. Grâce à Query Service, vous pouvez joindre n’importe quel jeu de données du lac de données et capturer les résultats de la requête sous forme de nouveau jeu de données à utiliser dans un compte rendu des performances, dans le cadre de l’apprentissage automatique ou pour une ingestion dans Real-time Customer Profile.

Pour plus d’informations sur le service, consultez la [Présentation de Query Service](../query-service/home.md) .

### Real-time Customer Profile

Real-time Customer Profile fournit un profil de consommateur centralisé pour une gestion d’expérience ciblée et personnalisée. Chaque profil contient des données agrégées sur tous les systèmes ainsi que des comptes horodatés exploitables d’événements impliquant les personnes concernées par l’un des systèmes que vous utilisez avec Experience Platform.

Real-time Customer Profile utilise des données au format schéma basées sur les classes [!UICONTROL XDM Individual Profile] et [!UICONTROL XDM ExperienceEvent] et répond aux requêtes basées sur ces données. Profile ne prend pas en charge l’utilisation de schémas basés sur d’autres classes.

Le système conserve une instance de chaque profil client, fusionnant les données pour former une &quot;source unique de vérité&quot; pour l’individu. Ces données unifiées sont représentées à l’aide d’un &quot;schéma d’union&quot; (parfois appelé &quot;vue d’union&quot;). Un schéma d’union agrège les champs de tous les schémas qui mettent en oeuvre la même classe dans un seul schéma.  Lors de la composition d’un schéma à l’aide de l’interface utilisateur ou de l’API, vous pouvez activer le schéma à utiliser avec Real-time Customer Profile et le marquer pour l’inclure dans l’union. Le schéma balisé participe alors à la définition de schéma transmise à Profile.

Comme les données [!UICONTROL XDM Individual Profile] et [!UICONTROL XDM ExperienceEvent] sont ingérées dans le lac de données, Real-time Customer Profile ingère toutes les données qui ont été activées pour son utilisation. Plus la quantité d’interactions et de détails ingérés est élevée, plus les profils deviennent robustes.

[!UICONTROL XDM Individual ] Profiledata permet d’informer et d’autonomiser les actions sur n’importe quel canal ou intégration de produit d’Adobe. Associées à un riche historique de données comportementales et interactives, ces données peuvent être utilisées pour alimenter l’apprentissage automatique. L’API Real-time Customer Profile peut aussi être utilisée pour enrichir les fonctionnalités des solutions tierces, des solutions CRM et des solutions propriétaires.

Pour plus d’informations, consultez la [présentation de Real-time Customer Profile](../profile/home.md).

### Data Science Workspace

Adobe Experience Platform Data Science Workspace utilise l’apprentissage automatique et l’intelligence artificielle pour obtenir des informations à partir des données stockées dans Experience Platform. Data Science Workspace permet aux spécialistes des données de créer des recettes basées sur [!UICONTROL XDM Individual Profile] et [!UICONTROL XDM ExperienceEvent] données sur les clients et leurs activités, ce qui facilite les prédictions telles que la propension d’achat et les offres recommandées que l’individu est susceptible d’apprécier et d’utiliser.

Data Science Workspace permet aux spécialistes des données de créer facilement des API de service intelligent optimisées par l’apprentissage automatique. Ces services fonctionnent avec d’autres solutions Adobe, y compris Adobe Target et Adobe Analytics Cloud, pour vous aider à automatiser les expériences numériques ciblées et personnalisées.

Pour plus d’informations sur l’utilisation des données d’Experience Platform pour alimenter les insights, consultez la [présentation de Data Science Workspace](../data-science-workspace/home.md).

## Étapes suivantes et ressources supplémentaires

Maintenant que vous comprenez mieux le rôle des schémas dans Experience Platform, vous êtes prêt à commencer à composer le vôtre.

Pour en savoir plus sur les principes de conception et les bonnes pratiques pour composer des schémas à utiliser avec Experience Platform, commencez par lire les [bases de la composition des schémas](schema/composition.md). Pour obtenir des instructions étape par étape sur la création d’un schéma, consultez les tutoriels sur la création d’un schéma [à l’aide de l’API](tutorials/create-schema-api.md) ou [de l’interface utilisateur](tutorials/create-schema-ui.md).

Pour mieux comprendre [!DNL XDM System] en Experience Platform, regardez la vidéo suivante :

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
