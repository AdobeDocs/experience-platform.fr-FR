---
keywords: Experience Platform ; accueil ; rubriques populaires ; XDM ; système XDM ; profil individuel XDM ; XDM ExperienceEvent ; XDM ExperienceEvent ; experienceEvent ; experience event ; Field groups ; field groups ; field group ; field group ; Field event ; Expérience event ; XDM ExperienceEvent ; XDM ExperienceEvent ; experienceEvent ; experienceEvent ; XDM ExperienceEvent ; experience data model ; Experience data model ; Experience data model ; Experience data model registre de schémas ; Registre de schémas ; bibliothèque de schémas ; bibliothèque de schémas ; schéma ; schéma ; enregistrement de données ; série chronologique ; série chronologique
solution: Experience Platform
title: Présentation du système XDM
topic-legacy: overview
description: La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. Le modèle de données d’expérience (XDM), optimisé par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 196147e7691010707953561c110a3934fec8ba1b
workflow-type: tm+mt
source-wordcount: '1947'
ht-degree: 56%

---

# Présentation du système XDM

La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. Le [!DNL Experience Data Model] (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Il fournit des structures et des définitions communes qui permettent à toute application de communiquer avec les services Plateforme. L’adhésion aux normes XDM permet d’intégrer toutes les données d’expérience client dans une représentation commune afin de fournir des informations de manière plus rapide et intégrée. Vous pouvez obtenir des insights précieux à partir des actions des clients, définir des audiences de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

XDM est le cadre de base qui permet à Adobe Experience Cloud, optimisé par Experience Platform, de transmettre le message approprié à la bonne personne, sur le bon canal et exactement au bon moment. La méthodologie sur laquelle l&#39;Experience Platform est construit, XDM System, opérationnalise [!DNL Experience Data Model] schémas à utiliser par les services Platform.

Ce document offre une vue d’ensemble du rôle du système XDM dans Experience Platform.

## Schémas XDM

Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit.

Avant que les données puissent être ingérées dans Platform, il est nécessaire de composer un schéma pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenues dans chaque champ. Les schémas se composent d&#39;une classe de base et de groupes de champs de schéma nuls ou supérieurs.

Pour plus d’informations sur le modèle de composition de schémas, y compris sur les principes de conception et les bonnes pratiques, consultez les [bases de la composition de schémas](schema/composition.md).

### Composants XDM standard

XDM fournit une collection robuste de groupes de champs et de types de données standard, destinés à capturer des concepts communs et des cas d’utilisation dans différents secteurs d’activité. Experience Platform vous permet de filtrer ces composants par secteur, ce qui vous permet de construire rapidement et en toute confiance des schémas qui répondent le mieux à vos besoins spécifiques.

Lors de la construction de schémas dans l’interface utilisateur de l’Experience Platform, les groupes de champs répertoriés sont affichés avec une mesure de popularité. Cette mesure est déterminée par la fréquence à laquelle les autres utilisateurs de la plate-forme utilisent le groupe de champs dans leurs schémas. Plus le nombre est élevé, plus le groupe de champs est populaire. Par défaut, les résultats sont affichés du plus populaire au moins populaire, ce qui vous informe des tendances de modélisation des données dans votre secteur.

![Popularité du groupe de champs](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform fournit une interface utilisateur et une API RESTful à partir de laquelle vous pouvez afficher et gérer toutes les ressources associées au schéma dans l’Experience Platform **[!DNL Schema Library]**. Le [!DNL Schema Library] contient des composants XDM standard mis à votre disposition par Adobe, ainsi que des ressources provenant de partenaires Experience Platform et de fournisseurs dont vous utilisez les applications.

Utilisation de la propriété [!DNL Schema Registry API] ou [!UICONTROL Schémas] dans l’interface utilisateur de la plate-forme, vous pouvez également créer et gérer de nouveaux schémas et ressources propres à votre entreprise.

Pour plus d&#39;informations sur la gestion et l&#39;interaction avec les schémas dans la plate-forme, consultez la documentation suivante :

* [Guide de l’interface utilisateur XDM](./ui/overview.md)
* [Guide de l&#39;API du registre de schémas](./api/overview.md)

## Comportements de données dans le système XDM {#data-behaviors}

Les données pouvant être utilisées dans Experience Platform sont regroupées selon deux types de comportements :

* **Enregistrer les données** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **Données de séries chronologiques**: Fournit un instantané du système au moment où une action a été effectuée directement ou indirectement par un sujet d&#39;enregistrement.

Tous les schémas XDM décrivent des données pouvant être catégorisées en tant qu’enregistrement ou série temporelle. Le comportement des données d’un schéma est défini par la classe du schéma attribuée à celui-ci lorsqu’il est créé pour la première fois. Les classes XDM décrivent le plus petit nombre de propriétés qu’un schéma doit contenir pour représenter un comportement de données spécifique.

Bien que vous puissiez définir vos propres classes au sein de la [!DNL Schema Registry], il est recommandé d’utiliser les classes préférées **[!UICONTROL Profil individuel XDM]** et **[!UICONTROL XDM ExperienceEvent]** pour les données d&#39;enregistrement et de série chronologique, respectivement. Ces classes sont décrites plus en détail ci-dessous.

### [!UICONTROL XDM Individual Profile] {#xdm-individual-profile}

[!UICONTROL XDM Individual Profile est une classe basée sur les enregistrements qui forme une représentation singulière des attributs des sujets identifiés et partiellement identifiés. ] Les profils hautement identifiés peuvent être utilisés pour des communications personnelles ou des engagements ciblés et peuvent contenir des informations personnelles détaillées telles que le nom, le genre, la date de naissance, l’adresse et les coordonnées, y compris les numéros de téléphone et les adresses électroniques.

Les profils moins identifiés peuvent n’être constitués que de signaux comportementaux anonymes tels que les cookies de navigateur. Dans ce cas, les données de profil éparses sont utilisées pour constituer une base d’informations dans laquelle les intérêts et les préférences du profil anonyme sont rassemblés et stockés. Ces identifiants peuvent devenir plus détaillés avec le temps si le sujet s’inscrit pour recevoir des notifications, souscrit à des abonnements, effectue des achats, etc. Ce développement des attributs de profil peut permettre d’obtenir un sujet identifié et un degré plus élevé d’engagement ciblé.

À mesure qu&#39;un profil se développe, il devient un solide référentiel des renseignements personnels, des renseignements d&#39;identification, des coordonnées et des préférences de communication d&#39;une personne.

Voir la section [[!UICONTROL Profil individuel XDM] guide de référence](./classes/individual-profile.md) pour plus d&#39;informations sur la structure et le cas d&#39;utilisation des champs fournis par la classe.

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent est une classe basée sur une série temporelle utilisée pour capturer l’état du système lorsqu’un événement (ou un ensemble d’événements) se produit, y compris le moment et l’identité du sujet concerné. Expérience Les événements sont des enregistrements factuels immuables de ce qui s&#39;est passé à ce moment-là, représentant ce qui s&#39;est passé sans agrégation ni interprétation. Ils sont essentiels à l’analyse du domaine temporel, puisqu’ils peuvent être utilisés pour analyser les modifications survenant au cours d’une période donnée et pour comparer plusieurs périodes afin de suivre les tendances.

Les événements d’expérience peuvent être explicites ou implicites. Les événements explicites sont des actions humaines directement observables qui ont lieu à un moment donné d’un parcours. Les événements implicites se produisent sans action humaine directe, mais restent liés à un individu. Les événements implicites incluent, par exemple, l’envoi planifié de newsletters par e-mail ou l’arrivée d’une batterie à un certain seuil de tension.

Bien qu’il ne soit pas facile de classer tous les événements de toutes les sources de données, il est extrêmement utile d’harmoniser les événements similaires en les groupant par types similaires quand cela est possible pour le traitement.

![Parcours client ExperienceEvent](images/overview/experience-event-journey.png)

Voir la section [[!UICONTROL XDM ExperienceEvent] guide de référence](./classes/experienceevent.md) pour plus d&#39;informations sur la structure et le cas d&#39;utilisation des champs fournis par la classe.

## Schémas XDM et services Experience Platform

L’Experience Platform est indépendant du schéma, ce qui signifie que tout schéma conforme à la norme XDM est mis à la disposition des services de plate-forme. Les modalités d’utilisation des schémas par les différents services Platform sont décrites plus en détail ci-dessous.

### Service de catalogue, gestion des données et Data Lake

Le service de catalogue est le système d’enregistrement des ressources d’Experience Platform et des schémas qui lui sont associés. Le catalogue ne contient pas les fichiers de données ou les répertoires réels, mais contient les métadonnées et les descriptions de ces fichiers et répertoires.

Les données du catalogue sont stockées dans le lac de données, une banque de données hautement granulaire contenant toutes les données gérées par Platform, quels qu’en soient l’origine ou le format.

Pour commencer à assimiler des données dans l’Experience Platform, vous pouvez utiliser le service de catalogue pour créer un ensemble de données. Le jeu de données fait référence à un schéma XDM qui décrit la structure des données à assimiler. Si un ensemble de données est créé sans schéma, l&#39;Experience Platform obtient un &quot;schéma observé&quot; en inspectant le type et le contenu des champs de données assimilées. Les ensembles de données sont ensuite suivis dans le catalogue et stockés dans le lac de données avec les schémas et les schémas observés sur lesquels ils sont basés.

Pour plus d’informations sur le catalogue, consultez la [présentation du service de catalogue](../catalog/home.md). Pour plus d’informations sur Adobe Experience Platform Data Ingestion, consultez la [présentation de Data Ingestion](../ingestion/home.md).

### Query Service

Adobe Experience Platform Query Service vous permet d’utiliser le langage SQL standard pour interroger les données d’Experience Platform afin de prendre en charge de nombreux cas d’utilisation différents.

Une fois qu’un schéma a été composé et qu’un jeu de données faisant référence à ce schéma a été créé, les données sont ingérées et stockées dans le lac de données. Grâce à Query Service, vous pouvez joindre n’importe quel jeu de données du lac de données et capturer les résultats de la requête sous forme de nouveau jeu de données à utiliser dans un compte rendu des performances, dans le cadre de l’apprentissage automatique ou pour une ingestion dans Real-time Customer Profile.

Reportez-vous à la section [Présentation du service de requête](../query-service/home.md) pour plus d’informations sur le service.

### Real-time Customer Profile

Real-time Customer Profile fournit un profil de consommateur centralisé pour une gestion d’expérience ciblée et personnalisée. Chaque profil contient des données agrégées sur tous les systèmes ainsi que des comptes horodatés exploitables d’événements impliquant les personnes concernées par l’un des systèmes que vous utilisez avec Experience Platform.

Le profil de client en temps réel utilise des données au format schéma en fonction de la [!UICONTROL Profil individuel XDM] et [!UICONTROL XDM ExperienceEvent] et répond aux requêtes en fonction de ces données. Profile ne prend pas en charge l’utilisation de schémas basés sur d’autres classes.

Le système conserve une instance de chaque profil de client, fusionnant les données pour former une &quot;source unique de vérité&quot; pour l&#39;individu. Ces données unifiées sont représentées à l&#39;aide de ce qu&#39;on appelle un &quot;schéma d&#39;union&quot; (parfois appelé &quot;vue d&#39;union&quot;). Un schéma d&#39;union regroupe les champs de tous les schémas qui implémentent la même classe dans un schéma unique.  Lors de la composition d’un schéma à l’aide de l’interface utilisateur ou de l’API, vous pouvez activer le schéma pour l’utiliser avec le profil client en temps réel et le baliser pour l’inclure dans l’union. Le schéma balisé participe alors à la définition de schéma transmise à Profile.

Comme [!UICONTROL Profil individuel XDM] et [!UICONTROL XDM ExperienceEvent] Les données sont assimilées dans Data Lake, le profil client en temps réel ingère toutes les données qui ont été activées pour son utilisation. Plus la quantité d’interactions et de détails ingérés est élevée, plus les profils deviennent robustes.

[!UICONTROL Profil individuel XDM] les données permettent d’informer et d’activer les actions sur n’importe quel canal ou Adobe d’intégration de produit. Associées à une riche histoire de données comportementales et d’interactions, ces données peuvent être utilisées pour alimenter l’apprentissage automatique. L’API Real-time Customer Profile peut aussi être utilisée pour enrichir les fonctionnalités des solutions tierces, des solutions CRM et des solutions propriétaires.

Pour plus d’informations, consultez la [présentation de Real-time Customer Profile](../profile/home.md).

### Data Science Workspace

Adobe Experience Platform Data Science Workspace utilise l’apprentissage automatique et l’intelligence artificielle pour obtenir des informations à partir des données stockées dans Experience Platform. Data Science Workspace permet aux chercheurs en données de créer des recettes basées sur [!UICONTROL Profil individuel XDM] et [!UICONTROL XDM ExperienceEvent] les données sur les clients et leurs activités, facilitant les prédictions telles que la propension à acheter et les offres recommandées que l&#39;individu est susceptible d&#39;apprécier et d&#39;utiliser.

Avec Data Science Workspace, les scientifiques de données peuvent facilement créer des API de service intelligentes alimentées par l’apprentissage automatique. Ces services fonctionnent avec d’autres solutions Adobe, y compris Adobe Target et Adobe Analytics Cloud, pour vous aider à automatiser les expériences numériques ciblées et personnalisées.

Pour plus d’informations sur l’utilisation des données d’Experience Platform pour alimenter les insights, consultez la [présentation de Data Science Workspace](../data-science-workspace/home.md).

## Étapes suivantes et ressources supplémentaires

Maintenant que vous comprenez mieux le rôle des schémas dans Experience Platform, vous êtes prêt à commencer à composer le vôtre.

Pour en savoir plus sur les principes de conception et les bonnes pratiques pour composer des schémas à utiliser avec Experience Platform, commencez par lire les [bases de la composition des schémas](schema/composition.md). Pour obtenir des instructions étape par étape sur la création d’un schéma, consultez les tutoriels sur la création d’un schéma [à l’aide de l’API](tutorials/create-schema-api.md) ou [de l’interface utilisateur](tutorials/create-schema-ui.md).

Pour renforcer votre compréhension de la [!DNL XDM System] en Experience Platform, regardez la vidéo suivante :

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
