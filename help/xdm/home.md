---
keywords: Experience Platform;accueil;rubriques les plus consultées;XDM;système XDM;XDM individual profile;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience event;groupes de Champs;groupe de champs;groupe de Champs;Experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevenet;modèle de données d’expérience;modèle de données d’Expérience;Modèle de Données d’Expérience;modèle de données; Modèle de Données;registre des schémas;Registre des Schémas;bibliothèque de schémas;Bibliothèque de Schémas;schéma;données d’enregistrement;série temporelle;série temporelle
solution: Experience Platform
title: Présentation du système XDM
description: La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. Le modèle de données d’expérience (XDM), optimisé par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 48caa318f0e951979db4fd2c94624a73311422d6
workflow-type: tm+mt
source-wordcount: '2101'
ht-degree: 74%

---

# Présentation du système XDM

La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. Le modèle de données d’expérience (XDM), optimisé par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences digitales. Elle fournit des structures et des définitions communes qui permettent à chaque application de communiquer avec les services Platform. L’adhésion aux normes XDM permet d’intégrer toutes les données d’expérience client dans une représentation commune afin de fournir des informations de manière plus rapide et intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des audiences de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

XDM est le cadre de base qui permet à Adobe Experience Cloud, optimisé par Experience Platform, de transmettre le message approprié à la bonne personne, sur le bon canal et exactement au bon moment. La méthodologie sur laquelle Experience Platform repose, à savoir le système XDM, rend les schémas de modèles de données d’expérience opérationnels pour qu’ils soient utilisés par les services de Platform.

Découvrez le rôle du système XDM dans Experience Platform.

## Schémas XDM {#xdm-schemas}

Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit.

Avant que les données puissent être ingérées dans Platform, il est nécessaire de composer un schéma pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenues dans chaque champ. Les schémas se composent d’une classe de base et de zéro ou plusieurs groupes de champs.

Pour plus d’informations sur le modèle de composition de schémas, y compris les principes de conception et les bonnes pratiques, voir la section [principes de base de la composition des schémas](schema/composition.md).

### Composants XDM standard {#Standard-xdm-components}

XDM fournit une solide collection de groupes de champs et de types de données standard, destinés à capturer des concepts et des cas d’utilisation courants dans différents secteurs d’activité. Experience Platform vous permet de filtrer ces composants par secteur d’activité afin de créer rapidement et en toute confiance des schémas qui répondent au mieux à vos besoins.

Lors de la création de schémas dans l’interface utilisateur d’Experience Platform, les groupes de champs répertoriés s’affichent avec une mesure de popularité. Cette mesure est déterminée par la fréquence à laquelle les autres utilisateurs de Platform utilisent le groupe de champs dans leurs schémas. Plus le nombre est élevé, plus le groupe de champs est populaire. Par défaut, les résultats s’affichent du plus populaire au moins populaire, vous renseignant sur les tendances de modélisation des données dans votre secteur d’activité.

![La colonne de popularité de la variable [!UICONTROL Ajouter un groupe de champs] boîte de dialogue.](./images/overview/popularity.png)

### [!DNL Schema Library] {#schema-library}

Experience Platform fournit une interface utilisateur et une API RESTful à partir desquelles vous pouvez afficher et gérer toutes les ressources liées aux schémas de **[!DNL Schema Library]** d’Experience Platform. La [!DNL Schema Library] possède des composants XDM standard mis à votre disposition par Adobe, ainsi que des ressources de partenaires Experience Platform et de fournisseurs dont vous utilisez les applications.

Vous pouvez également créer et gérer de nouveaux schémas et ressources propres à votre organisation à l’aide de la variable [!DNL Schema Registry API], ou la variable [!UICONTROL Schémas] dans l’interface utilisateur de Platform.

Pour plus d’informations sur la gestion et l’interaction avec les schémas dans Platform, consultez la documentation suivante :

* [Guide de l’interface utilisateur XDM](./ui/overview.md)
* [Guide du registre des schémas API](./api/overview.md)

## Comportements de données dans le système XDM {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="Comportements des données"
>abstract="Les données destinées à Experience Platform sont regroupées en trois types de comportements : enregistrement, série temporelle et ad hoc. Les schémas d’enregistrement fournissent des informations sur les attributs d’un objet, tandis que les schémas de série temporelle capturent un instantané du système au moment où une action a été effectuée. Les schémas ad hoc capturent les champs dont l’espace de noms peut être utilisé uniquement par un seul jeu de données. Pour plus d’informations sur le comportement des données dans Platform, consultez la documentation."

Les données pouvant être utilisées dans Experience Platform sont regroupées selon trois types de comportements :

* **Enregistrement** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **Série temporelle**: fournit un instantané du système au moment où une action a été entreprise directement ou indirectement par un sujet enregistré.
* **Ad hoc** : capture les champs dont l’espace de noms n’est utilisable que par un seul jeu de données. Les schémas ad hoc sont utilisés dans plusieurs workflows d’ingestion de données pour Experience Platform, notamment dans l’ingestion de fichiers CSV et dans la création de certains types de connexions sources.

Tous les schémas XDM décrivent des données pouvant être catégorisées en tant qu’enregistrement ou série temporelle. Le comportement des données d’un schéma est défini par la classe du schéma attribuée à celui-ci lorsqu’il est créé pour la première fois. Les classes XDM décrivent le plus petit nombre de propriétés qu’un schéma doit contenir pour représenter un comportement de données spécifique.

Bien que vous puissiez définir vos propres classes dans la variable [!DNL Schema Registry], il est recommandé d’utiliser les classes standard **[!UICONTROL XDM Individual Profile]** et **[!UICONTROL XDM ExperienceEvent]** pour les données d’enregistrement et de série temporelle, respectivement. Ces classes sont décrites plus en détail ci-dessous.

>[!NOTE]
>
>Il n’existe aucune classe standard basée sur le comportement ad hoc. Les schémas ad hoc sont générés automatiquement par les processus Platform qui les utilisent, mais ils peuvent également être [créé manuellement à l’aide de l’API Schema Registry](./tutorials/ad-hoc.md).

### [!UICONTROL XDM Individual Profile] {#xdm-individual-profile}

[!UICONTROL XDM Individual Profile] est une classe basée sur des enregistrements qui forme une représentation singulière des attributs des sujets identifiés et partiellement identifiés. Les profils hautement identifiés peuvent être utilisés pour des communications personnelles ou des engagements ciblés. Les profils hautement identifiés peuvent contenir des informations personnelles détaillées telles que le nom, le sexe, la date de naissance, l’emplacement et les coordonnées, y compris les numéros de téléphone et les adresses électroniques.

Les profils moins identifiés peuvent n’être constitués que de signaux comportementaux anonymes tels que les cookies de navigateur. Dans ce cas, les données de profil éparses sont utilisées pour constituer une base d’informations dans laquelle les intérêts et les préférences du profil anonyme sont rassemblés et stockés. Ces identifiants peuvent devenir plus détaillés avec le temps si l’objet s’inscrit pour recevoir des notifications, souscrit à des abonnements, effectue des achats, etc. Ce développement des attributs de profil peut permettre d’obtenir un objet identifié et un degré plus élevé d’engagement ciblé.

Au fur et à mesure qu’un profil croît, il devient un solide référentiel des informations personnelles, des informations d’identification, des coordonnées et des préférences de communication d’une personne.

Pour plus d’informations sur la structure et le cas d’utilisation des champs fournis par la classe, consultez le [[!UICONTROL guide de référence XDM Individual Profile]](./classes/individual-profile.md).

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent est une classe basée sur une série temporelle utilisée pour capturer l’état du système lorsqu’un événement (ou un ensemble d’événements) se produit, y compris le moment et l’identité du titulaire concerné. Les événements d’expérience sont des enregistrements factuels non modifiables de ce qui s’est produit à un moment précis, reprenant les faits sans aucune agrégation ni interprétation. Ils sont essentiels à l’analyse du domaine temporel, puisqu’ils peuvent être utilisés pour analyser les modifications survenant au cours d’une période donnée et pour comparer plusieurs périodes afin de suivre les tendances.

Les événements d’expérience peuvent être explicites ou implicites. Les événements explicites sont des actions humaines directement observables qui ont lieu à un moment donné d’un parcours. Les événements implicites se produisent sans action humaine directe, mais restent liés à un individu. Les événements implicites incluent, par exemple, l’envoi planifié de newsletters par e-mail ou l’arrivée d’une batterie à un certain seuil de tension.

Bien qu’il ne soit pas facile de classer tous les événements de toutes les sources de données, il est extrêmement utile d’harmoniser les événements similaires en les groupant par types similaires quand cela est possible pour le traitement.

![Infographie du Parcours client visualisée avec les événements d’expérience au fil du temps.](images/overview/experience-event-journey.png)

Pour plus d’informations sur la structure et le cas d’utilisation des champs fournis par la classe, consultez le [[!UICONTROL guide de référence XDM ExperienceEvent]](./classes/experienceevent.md).

## Schémas XDM et services Experience Platform {#schemas-and-platform-services}

Experience Platform est compatible avec les schémas, ce qui signifie que tout schéma conforme au standard XDM est mis à disposition des services Platform. Les modalités d’utilisation des schémas par les différents services Platform sont décrites plus en détail ci-dessous.

### Service de catalogue, ingestion de données et lac de données {#ingestion-catalog-and-storage}

Le service de catalogue est le système d’enregistrement des fichiers d’Experience Platform et des schémas qui lui sont associés. Le catalogue ne contient pas les fichiers ou les répertoires de données, mais plutôt les métadonnées et les descriptions de ces fichiers et répertoires.

Les données du catalogue sont stockées dans le lac de données, un entrepôt de données hautement granulaire contenant toutes les données gérées par Platform, indépendamment de leur origine ou de leur format.

Pour commencer l’ingestion de données dans Experience Platform, vous pouvez utiliser le service de catalogue pour créer un jeu de données. Le jeu de données fait référence à un schéma XDM qui décrit la structure des données à ingérer. Si un jeu de données est créé sans schéma, Experience Platform crée alors un « schéma observé » en examinant le type et le contenu des champs de données ingérés. Les jeux de données sont ensuite suivis dans le service de catalogue et stockés dans le lac de données aux côtés des schémas et des schémas observés sur lesquels ils sont basés.

Voir [Présentation du service de catalogue](../catalog/home.md) pour plus d’informations. Voir [Présentation de Data Ingestion](../ingestion/home.md) pour plus d’informations sur Adobe Experience Platform Data Ingestion.

### Query Service {#query-service}

Vous pouvez utiliser SQL standard pour interroger les données Experience Platform afin de prendre en charge de nombreux cas d’utilisation différents avec Adobe Experience Platform Query Service.

Une fois qu’un schéma a été composé et qu’un jeu de données qui référence ce schéma a été créé, les données sont ensuite ingérées et stockées dans le lac de données. Vous pouvez ensuite utiliser Query Service pour joindre n’importe quel jeu de données dans le lac de données et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, l’apprentissage automatique ou l’ingestion dans Real-time Customer Profile.

Pour plus d’informations sur le service, consultez la [présentation de Query Service](../query-service/home.md).

### Profil client en temps réel {#real-time-customer-profile}

Le profil client en temps réel fournit un profil de consommateur centralisé pour une gestion d’expérience ciblée et personnalisée. Chaque profil contient des données agrégées sur tous les systèmes et inclut des comptes horodatés exploitables d’événements qui impliquent l’objet du profil. Ces événements peuvent avoir eu lieu dans n’importe quel système que vous utilisez avec Experience Platform.

Real-Time Customer Profile utilise des données au format schéma basées sur la variable [!UICONTROL XDM Individual Profile] et [!UICONTROL XDM ExperienceEvent] et répond aux requêtes en fonction de ces données.

Le système conserve une instance de chaque profil client, fusionnant les données pour former une « source unique de vérité » pour l’individu. Ces données unifiées sont représentées par un « schéma d’union »; (parfois appelé « vue d’union »;). Un schéma d’union agrège les champs de tous les schémas qui mettent en oeuvre la même classe dans un seul schéma. Lors de la composition d’un schéma à l’aide de l’interface utilisateur ou d’une API, vous pouvez l’activer pour une utilisation avec le profil client en temps réel et l’étiqueter pour l’inclure à l’union. Le schéma balisé participe alors à la définition de schéma transmise à Profil.

As [!UICONTROL XDM Individual Profile] et [!UICONTROL XDM ExperienceEvent] Les données sont ingérées dans le lac de données. Real-time Customer Profile ingère toutes les données qui ont été activées pour son utilisation. Plus la quantité d’interactions et de détails ingérés est élevée, plus les profils deviennent robustes.

Les données [!UICONTROL XDM Individual Profile] permettent de guider et d’exécuter les actions sur n’importe quel canal ou intégration de produit Adobe. Associées à un riche historique de données sur les comportements et les interactions, ces données peuvent être utilisées pour alimenter le machine learning. L’API Real-Time Customer Profile peut aussi être utilisée pour enrichir les fonctionnalités des solutions tierces, des solutions CRM et des solutions propriétaires.

Pour plus d’informations, consultez la [vue d’ensemble du profil client en temps réel](../profile/home.md).

### Espace de travail de science des données {#data-science-workspace}

L’espace de travail de science des données d’Adobe Experience Platform utilise le machine learning et l’intelligence artificielle pour obtenir des informations à partir des données stockées dans Experience Platform. Data Science Workspace permet aux spécialistes des données de créer des recettes basées sur [!UICONTROL XDM Individual Profile] et [!UICONTROL XDM ExperienceEvent] des données sur les clients et leurs activités. Ces recettes facilitent les prédictions telles que la propension à acheter et les offres recommandées que l’individu est susceptible d’apprécier et d’utiliser.

Avec l’espace de travail de science des données, les spécialistes des données peuvent facilement créer des API de service intelligents optimisés par le machine learning. Ces services fonctionnent avec d’autres solutions Adobe, y compris Adobe Target et Adobe Analytics Cloud, pour vous aider à automatiser les expériences digitales ciblées et personnalisées.

Pour plus d’informations sur l’utilisation des données d’Experience Platform pour alimenter les insights, consultez la [présentation de l’espace de travail de science des données](../data-science-workspace/home.md).

## Étapes suivantes et ressources supplémentaires

Maintenant que vous comprenez mieux le rôle des schémas dans Experience Platform, vous êtes prêt à commencer à composer le vôtre.

Pour en savoir plus sur les principes de conception et les bonnes pratiques pour composer des schémas à utiliser avec Experience Platform, commencez par lire les [bases de la composition des schémas](schema/composition.md). Pour obtenir des instructions étape par étape sur la création d’un schéma, consultez les tutoriels sur la création d’un schéma [à l’aide de l’API](tutorials/create-schema-api.md) ou [de l’interface utilisateur](tutorials/create-schema-ui.md).

Pour mieux comprendre le [!DNL XDM System] dans Experience Platform, regardez la vidéo suivante :

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
