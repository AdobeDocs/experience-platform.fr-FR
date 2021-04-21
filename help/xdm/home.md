---
keywords: Experience Platform ; accueil ; rubriques populaires ; XDM ; système XDM ; profil individuel XDM ; XDM ExperienceEvent ; XDM Experience Événement ; experienceEvent ; experience événement ; mixins ; mixins ; mixin ; Mixin ; Experience événement ; XDM Experience Événement ; XDM ExperienceEvent ; experienceEvent ; experience;XDM ExperienceEvent;XDM Experienceevenet;Experience data model ; Experience data model;modèle de données;modèle de données;registre de schémas;registre de Schémas;bibliothèque de ;bibliothèque de Schéma;schéma bibliothèque de ;schéma ; enregistrement de données;série de temps;série de temps
solution: Experience Platform
title: Présentation du système XDM
topic-legacy: overview
description: La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. Le modèle de données d’expérience (XDM), optimisé par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 57%

---

# Présentation du système XDM

La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. [!DNL Experience Data Model] (XDM), piloté par l’Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Il fournit des structures et des définitions communes pour toute application à utiliser pour communiquer avec les services [!DNL Platform]. L’adhésion aux normes XDM permet d’intégrer toutes les données d’expérience client dans une représentation commune afin de fournir des informations de manière plus rapide et intégrée. Vous pouvez obtenir des insights précieux à partir des actions des clients, définir des audiences de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

XDM est le cadre fondateur qui permet à Adobe Experience Cloud, propulsé par [!DNL Experience Platform], de transmettre le bon message à la bonne personne, sur le bon canal, exactement au bon moment. La méthodologie sur laquelle [!DNL Experience Platform] est construit, XDM System, rend opérationnels [!DNL Experience Data Model] schémas pour les services [!DNL Platform].

Ce document offre une vue d’ensemble du rôle du système XDM dans [!DNL Experience Platform].

## Schémas XDM

[!DNL Experience Platform] utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit.

Avant que les données puissent être ingérées dans [!DNL Platform], un schéma doit être composé pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenu dans chaque champ. Les schémas se composent d’une classe de base et de zéro ou plusieurs mixins.

Pour plus d’informations sur le modèle de composition de schémas, y compris sur les principes de conception et les bonnes pratiques, consultez les [bases de la composition de schémas](schema/composition.md).

### [!DNL Schema Registry] et [!DNL Schema Library]

**[!DNL Schema Registry]** fournit une interface utilisateur et une API RESTful à partir de laquelle vous pouvez vue et gérer toutes les ressources liées au schéma dans le Adobe Experience Platform **[!DNL Schema Library]**. [!DNL Schema Library] contient des ressources standard mises à votre disposition par Adobe, ainsi que des ressources provenant de [!DNL Experience Platform] partenaires et fournisseurs dont vous utilisez les applications. L’interface utilisateur et l’API du registre des schémas peuvent aussi être utilisées pour créer et gérer de nouveaux schémas et ressources propres à votre organisation.

Pour un guide complet des principales opérations disponibles dans le [!DNL Schema Registry], consultez le [Schéma Registry developer guide](api/getting-started.md).

## Comportements de données dans le système XDM {#data-behaviors}

Les données destinées à être utilisées dans [!DNL Experience Platform] sont regroupées en deux types de comportement :

* **Enregistrer les données** : fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **Données de série temporelle** : fournissent un instantané du système au moment où une action a été entreprise directement ou indirectement par un sujet enregistré.

Tous les schémas XDM décrivent des données pouvant être catégorisées en tant qu’enregistrement ou série temporelle. Le comportement des données d’un schéma est défini par la classe du schéma attribuée à celui-ci lorsqu’il est créé pour la première fois. Les classes XDM décrivent le plus petit nombre de propriétés qu’un schéma doit contenir pour représenter un comportement de données spécifique.

Bien que vous puissiez définir vos propres classes dans [!DNL Schema Registry], il est recommandé d&#39;utiliser les classes préférées **[!DNL XDM Individual Profile]** et **[!DNL XDM ExperienceEvent]** pour les données d&#39;enregistrement et de série chronologique, respectivement. Ces classes sont décrites plus en détail ci-dessous.

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] est une classe basée sur les enregistrements qui forme une représentation singulière des attributs des sujets identifiés et partiellement identifiés. Les profils hautement identifiés peuvent être utilisés pour des communications personnelles ou des engagements ciblés et peuvent contenir des informations personnelles détaillées telles que le nom, le genre, la date de naissance, l’adresse et les coordonnées, y compris les numéros de téléphone et les adresses électroniques.

Les profils moins identifiés peuvent n’être constitués que de signaux comportementaux anonymes tels que les cookies de navigateur. Dans ce cas, les données de profil éparses sont utilisées pour constituer une base d’informations dans laquelle les intérêts et les préférences du profil anonyme sont rassemblés et stockés. Ces identifiants peuvent devenir plus détaillés avec le temps si le sujet s’inscrit pour recevoir des notifications, souscrit à des abonnements, effectue des achats, etc. Ce développement des attributs de profil peut permettre d’obtenir un sujet identifié et un degré plus élevé d’engagement ciblé.

Au fur et à mesure qu’un profil client croît, il devient un solide référentiel des informations personnelles, des informations d’identification, des coordonnées et des préférences de communication d’une personne.

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent est une classe basée sur une série temporelle utilisée pour capturer l’état du système lorsqu’un événement (ou un ensemble d’événements) se produit, y compris le moment et l’identité du sujet concerné. Les événements d’expérience sont des enregistrements factuels de ce qui s’est passé. Par conséquent, ces événements sont inaltérables et représentent ce qui s’est passé sans agrégation ni interprétation. Ils sont essentiels à l’analyse du domaine temporel, puisqu’ils peuvent être utilisés pour analyser les modifications survenant au cours d’une période donnée et pour comparer plusieurs périodes afin de suivre les tendances.

Les événements d’expérience peuvent être explicites ou implicites. Les événements explicites sont des actions humaines directement observables qui ont lieu à un moment donné d’un parcours. Les événements implicites se produisent sans action humaine directe, mais restent liés à un individu. Les événements implicites incluent, par exemple, l’envoi planifié de newsletters par e-mail ou l’arrivée d’une batterie à un certain seuil de tension.

Bien qu’il ne soit pas facile de classer tous les événements de toutes les sources de données, il est extrêmement utile d’harmoniser les événements similaires en les groupant par types similaires quand cela est possible pour le traitement.

![Parcours client ExperienceEvent](images/overview/experience-event-journey.png)

## Schémas XDM et services [!DNL Experience Platform]

[!DNL Experience Platform] est indépendante du schéma, ce qui signifie que tout schéma conforme à la norme XDM est disponible pour être utilisé par  [!DNL Platform] les services. Les modalités d&#39;utilisation des schémas des différents services [!DNL Platform] sont décrites plus en détail ci-dessous.

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] est le système d&#39;enregistrement des  [!DNL Experience Platform] actifs et de leurs schémas connexes. [!DNL Catalog] ne correspond pas aux fichiers ou répertoires contenant des données, mais aux métadonnées et descriptions de ces fichiers et répertoires.

[!DNL Catalog] les données sont stockées dans le  [!DNL Data Lake], un magasin de données très granulaire contenant toutes les données gérées par  [!DNL Platform], quel que soit l’origine ou le format de fichier.

Pour commencer à ingérer des données dans [!DNL Experience Platform], un jeu de données est créé à l&#39;aide de [!DNL Catalog Service]. Le jeu de données fait référence à un schéma XDM décrivant la structure des données à ingérer. Si un jeu de données est créé sans schéma, [!DNL Experience Platform] obtient un &quot;schéma observé&quot; en examinant le type et le contenu des champs de données assimilés. Les jeux de données sont ensuite suivis dans [!DNL Catalog] et stockés dans [!DNL Data Lake] à côté des schémas et des schémas observés sur lesquels ils sont basés.

Pour plus d&#39;informations sur [!DNL Catalog], consultez la [Présentation du service de catalogue](../catalog/home.md). Pour plus d’informations sur Adobe Experience Platform Data Ingestion, consultez la [présentation de Data Ingestion](../ingestion/home.md).

### [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] vous permet d&#39;utiliser des données SQL standard pour la requête [!DNL Experience Platform] afin de prendre en charge de nombreux cas d&#39;utilisation différents.

Une fois qu&#39;un schéma a été composé et qu&#39;un jeu de données a été créé qui fait référence à ce schéma, les données sont ensuite assimilées et stockées dans le [!DNL Data Lake]. [!DNL Query Service] vous permet de joindre n&#39;importe quel jeu de données dans [!DNL Data Lake] et de capturer les résultats de la requête sous la forme d&#39;un nouveau jeu de données à utiliser dans le rapports, l&#39;apprentissage automatique ou pour l&#39;assimilation dans [!DNL Real-time Customer Profile].

Pour en savoir plus sur [!DNL Query Service], consultez l&#39;introduction [Requête Service](../query-service/home.md).

### [!DNL Real-time Customer Profile]

Real-time Customer Profile fournit un profil de consommateur centralisé pour une gestion d’expérience ciblée et personnalisée. Chaque profil contient des données agrégées sur tous les systèmes ainsi que des comptes horodatés exploitables d’événements impliquant les personnes concernées par l’un des systèmes que vous utilisez avec [!DNL Experience Platform].

[!DNL Real-time Customer Profile] utilise des données au format schéma basées sur les  [!DNL XDM Individual Profile] ou  [!DNL XDM ExperienceEvent] classes et répond aux requêtes basées sur ces données. [!DNL Profile] ne prend pas en charge l’utilisation de schémas basés sur d’autres classes.

[!DNL Profile] conserve une instance de chaque profil client, fusionnant les données pour former une « source unique de vérité » pour l’individu. Ces données unifiées sont représentées à l’aide d’une « vue d’union ». Une vue d’union agrège les champs de tous les schémas qui mettent en œuvre la même classe dans un seul et même schéma.  Lors de la composition d’un schéma à l’aide de l’interface utilisateur ou de l’API, vous pouvez activer le schéma pour l’utiliser avec [!DNL Real-time Customer Profile] et le marquer pour l’inclure dans la vue d’union. Le schéma balisé participe alors à la définition de schéma transmise à [!DNL Profile].

Comme les données [!DNL XDM Individual Profile] et [!DNL XDM ExperienceEvent] sont ingérées et gérées par [!DNL Catalog], [!DNL Real-time Customer Profile] commence à ingérer les données qui ont été activées pour leur utilisation. Plus la quantité d’interactions et de détails ingérés est élevée, plus les profils deviennent robustes.

[!DNL XDM Individual Profile]Les données permettent d’informer et d’autonomiser les actions sur les canaux ou sur les intégrations de solutions Adobe. Associées à un riche historique de données sur les comportements et les interactions, ces données sont utilisées pour alimenter l’apprentissage automatique. L&#39;API [!DNL Real-time Customer Profile] peut également être utilisée pour enrichir les fonctionnalités des solutions tierces, des solutions de gestion de la relation client et des solutions propriétaires.

Pour plus d’informations, consultez la [présentation de Real-time Customer Profile](../profile/home.md).

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utilise l&#39;apprentissage automatique et l&#39;intelligence artificielle pour obtenir des informations sur les données stockées dans [!DNL Experience Platform]. [!DNL Data Science Workspace] permet aux spécialistes des données de créer des recettes basées sur des données XDM Individual et concernant les clients et leurs activités, ce qui facilite les prédictions telles que la propension d’achat et les offres recommandées que l’individu est susceptible d’apprécier et de saisir.[!DNL Profile][!DNL XDM ExperienceEvent]

Avec [!DNL Data Science Workspace], les chercheurs en données peuvent facilement créer des API de services intelligents alimentées par l&#39;apprentissage automatique. Ces services fonctionnent avec d’autres solutions Adobe, y compris Adobe Target et Adobe Analytics Cloud, pour vous aider à automatiser les expériences numériques ciblées et personnalisées.

Pour plus d&#39;informations sur l&#39;utilisation des données [!DNL Experience Platform] pour obtenir des informations sur la puissance, consultez l&#39;[Présentation de Data Science Workspace](../data-science-workspace/home.md).

## Étapes suivantes et ressources supplémentaires

Maintenant que vous comprenez mieux le rôle des schémas tout au long de [!DNL Experience Platform], vous êtes prêt à vous début à composer les vôtres. Pour continuer à compléter votre apprentissage, début en lisant la documentation suggérée et regardez la vidéo ci-dessous.

Pour découvrir les principes de conception et les meilleures pratiques de composition des schémas à utiliser avec [!DNL Experience Platform], commencez par lire les [bases de la composition des schémas](schema/composition.md). Pour obtenir des instructions étape par étape sur la création d’un schéma, consultez les tutoriels sur la création d’un schéma [à l’aide de l’API](tutorials/create-schema-api.md) ou [de l’interface utilisateur](tutorials/create-schema-ui.md).

Pour mieux comprendre [!DNL XDM System] dans [!DNL Experience Platform], regardez la vidéo suivante :

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
