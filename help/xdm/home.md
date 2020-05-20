---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Système de modèle de données d’expérience (XDM)
topic: overview
translation-type: tm+mt
source-git-commit: c07f926a71447e840c692ed15e85c9e02f1106ab
workflow-type: tm+mt
source-wordcount: '1744'
ht-degree: 0%

---


# Présentation du système XDM

La normalisation et l’interopérabilité sont des concepts clés d’Adobe Experience Platform. Le modèle de données d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Il fournit des structures et des définitions communes pour toute application à utiliser pour communiquer avec les services de la plate-forme. En respectant les normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune qui peut fournir des informations d’une manière plus rapide et plus intégrée. Vous pouvez obtenir des informations précieuses sur les actions client, définir des audiences client par le biais de segments et exprimer des attributs client à des fins de personnalisation.

XDM est le cadre fondamental qui permet à Adobe Experience Cloud, optimisé par Experience Platform, de transmettre le message approprié à la bonne personne, au bon canal, exactement au bon moment. La méthodologie sur laquelle la plate-forme d’expérience est créée, **XDM System**, rend opérationnels les schémas de modèles de données d’expérience pour les utiliser par les services de plateforme.

Ce document présente un aperçu du rôle de XDM System dans Experience Platform.

## schémas XDM

Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente entre les systèmes, il devient plus facile de conserver une signification et, par conséquent, de tirer profit des données.

Avant que les données puissent être ingérées dans la plate-forme, un schéma doit être composé pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenu dans chaque champ. Les Schémas se composent d&#39;une classe de base et de mixins nuls ou plus.

Pour plus d&#39;informations sur le modèle de composition des schémas, y compris les principes de conception et les meilleures pratiques, voir les [bases de la composition](schema/composition.md)des schémas.

### Registre des Schémas et bibliothèque de Schémas

Le Registre **des** Schémas fournit une interface utilisateur et une API RESTful à partir de laquelle vous pouvez vue et gérer toutes les ressources liées aux schémas dans la bibliothèque **de** Schémas Adobe Experience Platform. La bibliothèque de Schémas contient des ressources standard mises à votre disposition par Adobe, ainsi que des ressources provenant de partenaires d’Experience Platform et de fournisseurs dont vous utilisez les applications. L’interface utilisateur et l’API du registre de Schémas peuvent également être utilisées pour créer et gérer de nouveaux schémas et ressources propres à votre entreprise.

Pour un guide complet sur les principales opérations disponibles dans le registre des Schémas, consultez le guide [de développement du registre des](api/getting-started.md)Schémas.

## Comportements de données dans le système XDM {#data-behaviors}

Les données destinées à être utilisées dans la plate-forme d’expérience sont regroupées en deux types de comportement :

* **Enregistrer les données**: Fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **Données** de série chronologique : Fournit un instantané du système au moment où une action a été entreprise directement ou indirectement par un sujet d&#39;enregistrement.

Tous les schémas XDM décrivent des données pouvant être classées comme enregistrements ou séries chronologiques. Le comportement des données d&#39;un schéma est défini par la **classe** de schéma, qui est affectée à un schéma lors de sa création. Les classes XDM décrivent le plus petit nombre de propriétés qu&#39;un schéma doit contenir pour représenter un comportement de données particulier.

Bien que vous puissiez définir vos propres classes dans le registre des Schémas, il est recommandé d&#39;utiliser les classes préférées **XDM Individuel Profil** et **XDM ExperienceEvent** pour les données d&#39;enregistrement et de série chronologique, respectivement. Ces classes sont décrites plus en détail ci-dessous.

### Profil XDM individuel

Le Profil individuel XDM est une classe basée sur des enregistrements qui forme une représentation singulière des attributs des sujets identifiés et partiellement identifiés. Les Profils hautement identifiés peuvent être utilisés pour des communications personnelles ou des engagements ciblés et peuvent contenir des renseignements personnels détaillés tels que le nom, le sexe, la date de naissance, le lieu et les coordonnées, y compris les numéros de téléphone et les adresses électroniques.

Les profils moins identifiés peuvent être constitués uniquement de signaux comportementaux anonymes tels que les cookies de navigateur. Dans ce cas, les données de profil peu nombreuses sont utilisées pour constituer une base d&#39;informations dans laquelle les intérêts et les préférences du profil anonyme sont rassemblés et stockés. Ces identifiants peuvent devenir plus détaillés au fil du temps lorsque le sujet s’inscrit pour recevoir des notifications, des abonnements, des achats, etc. Cette augmentation des attributs de profil peut éventuellement donner lieu à un sujet identifié et permettre un plus haut degré d&#39;engagement ciblé.

À mesure que le profil des consommateurs continue de croître, il devient un solide référentiel des renseignements personnels, des renseignements d&#39;identification, des coordonnées et des préférences de communication d&#39;une personne.

### XDM ExperienceEvent

XDM ExperienceEvent est une classe basée sur des séries chronologiques utilisée pour capturer l&#39;état du système lorsqu&#39;un événement (ou un ensemble de événements) s&#39;est produit, y compris le moment et l&#39;identité du sujet concerné. Les Événements d&#39;expérience sont des données factuelles de ce qui s&#39;est passé, donc ils sont immuables et représentent ce qui s&#39;est passé sans agrégation ni interprétation. Ils sont essentiels pour les analyses du domaine temporel, car ils peuvent être utilisés pour analyser les modifications qui surviennent dans une période donnée et pour comparer entre plusieurs périodes afin de suivre les tendances.

Les Événements d’expérience peuvent être explicites ou implicites. Les événements explicites sont des actions humaines directement observables qui se déroulent à un moment d&#39;un voyage. Les événements implicites sont des événements qui sont élevés sans action humaine directe, mais qui sont toujours liés à un individu. Parmi les exemples de événements implicites, citons l’envoi planifié de bulletins d’information par courriel ou la tension de batterie atteignant un certain seuil.

Bien que tous les événements ne soient pas facilement classés dans toutes les sources de données, il est extrêmement utile d&#39;harmoniser des événements similaires en types similaires lorsque cela est possible pour le traitement.

![Voyage du client ExperienceEvent](images/overview/experience-event-journey.png)

## schémas XDM et services Experience Platform

Experience Platform est indépendante du schéma, ce qui signifie que tout schéma conforme à la norme XDM peut être utilisé par les services Platform. Les modalités d’utilisation des schémas par les différents services de la plate-forme sont décrites plus en détail ci-dessous.

### Service de catalogue, Ingestion des données et Data Lake

Catalog Service est le système d’enregistrement des ressources de la plateforme d’expérience et de leurs schémas associés. Le catalogue ne correspond pas aux fichiers ou répertoires contenant des données, mais aux métadonnées et descriptions de ces fichiers et répertoires.

Les données du catalogue sont stockées dans Data Lake, un magasin de données très granulaire contenant toutes les données gérées par la plateforme, quel que soit l’origine ou le format de fichier.

Pour commencer à importer des données dans la plate-forme d’expérience, un jeu de données est créé à l’aide de Catalog Service. Le jeu de données fait référence à un schéma XDM décrivant la structure des données à ingérer. Si un jeu de données est créé sans schéma, la plateforme d’expérience dérive un &quot;schéma observé&quot; en examinant le type et le contenu des champs de données assimilées. Les ensembles de données sont ensuite suivis dans le catalogue et stockés dans le lac Data le long des schémas et des schémas observés sur lesquels ils sont basés.

Pour plus d’informations sur le catalogue, voir la présentation [du service de](../catalog/home.md)catalogue. Pour plus d’informations sur l’administration des données de la plate-forme Adobe Experience, consultez l’aperçu [de l’administration des](../ingestion/home.md)données.

### Requête Service

Adobe Experience Platform Requête Service vous permet d’utiliser des données SQL standard pour requête Experience Platform afin de prendre en charge de nombreux cas d’utilisation différents.

Après la composition d&#39;un schéma et la création d&#39;un jeu de données faisant référence à ce schéma, les données sont ensuite ingérées et stockées dans le lac Data. Requête Service vous permet de joindre n’importe quel jeu de données dans Data Lake et de capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans le rapports, l’apprentissage automatique ou pour l’assimilation dans le Profil client en temps réel.

Pour en savoir plus sur Requête Service, consultez l&#39;introduction [de](../query-service/home.md)Requête Service.

### Profil client en temps réel

Le Profil client en temps réel fournit un profil client centralisé pour une gestion d’expérience ciblée et personnalisée. Chaque profil contient des données qui sont agrégées sur tous les systèmes, ainsi que des comptes horodatés exploitables des événements impliquant les individus qui se sont produits sur l’un des systèmes que vous utilisez avec Experience Platform.

Le Profil client en temps réel utilise des données au format schéma basées sur les classes XDM Individuel Profil ou XDM ExperienceEvent et répond aux requêtes basées sur ces données. Le Profil ne prend pas en charge l&#39;utilisation de schémas basés sur d&#39;autres classes.

Profil conserve une instance de chaque profil client, fusionnant les données pour former une &quot;source unique de vérité&quot; pour l&#39;individu. Ces données unifiées sont représentées à l’aide de ce qu’on appelle une &quot;vue d’union&quot;. Une vue d’union agrégat les champs de tous les schémas qui implémentent la même classe dans un seul schéma.  Lors de la composition d’un schéma à l’aide de l’interface utilisateur ou de l’API, vous pouvez activer le schéma pour l’utiliser avec le Profil client en temps réel et le marquer pour l’inclusion dans la vue d’union. Le schéma balisé participera alors à la définition du schéma alimentée au Profil.

Comme les données de Profil individuel XDM et XDM ExperienceEvent sont ingérées et gérées par le catalogue, le Profil client en temps réel est déclenché pour commencer à ingérer les données qui ont été activées pour leur utilisation. Plus les interactions et les détails sont ingérés, plus les profils individuels deviennent robustes.

Les données des Profils individuels XDM permettent d’informer et d’activer les actions dans n’importe quel canal ou intégration de solution Adobe. Lorsqu’elles sont associées à un riche historique de données comportementales et d’interaction, ces données sont utilisées pour alimenter l’apprentissage automatique. L’API Profil client en temps réel peut également être utilisée pour enrichir les fonctionnalités des solutions tierces, des solutions de gestion de la relation client et des solutions propriétaires.

Pour plus d’informations, consultez la présentation [du Profil client en temps](../profile/home.md) réel.

### Espace de travail Data Science

Adobe Experience Platform Data Science Workspace utilise l’apprentissage automatique et l’intelligence artificielle pour obtenir des informations à partir des données stockées dans Experience Platform. Data Science Workspace permet aux chercheurs de données de créer des recettes basées sur les données de Profil individuel XDM et XDM ExperienceEvent relatives aux clients et à leurs activités, ce qui facilite les prédictions telles que la propension à acheter et les offres recommandées que l&#39;individu est susceptible d&#39;apprécier et d&#39;utiliser.

Avec Data Science Workspace, les chercheurs en données peuvent facilement créer des API de services intelligents alimentées par l&#39;apprentissage automatique. Ces services fonctionnent avec d’autres solutions Adobe, notamment Adobe Cible et Adobe Analytics Cloud, afin de vous aider à automatiser les expériences numériques ciblées et personnalisées.

Pour plus d’informations sur l’utilisation des données de la plate-forme d’expérience pour alimenter les statistiques, voir l’aperçu [de](../data-science-workspace/home.md)Data Science Workspace.

### Service de prise de décision

Le service de prise de décision permet de configurer la prise de décision personnalisée par offre dans les applications intégrées à la plate-forme. Les Offres peuvent être des recommandations de produit, des composants de contenu pour une expérience Web, des scripts de conversation et des actions à entreprendre.

Le service de prise de décision utilise les données du Profil client en temps réel et n&#39;est donc compatible qu&#39;avec les jeux de données basés sur les schémas d&#39;implémentation de la classe de Profil individuel XDM ou XDM ExperienceEvent.

See the [Decisioning Service overview](../decisioning-service/home.md) for more information.

## Étapes suivantes

Maintenant que vous comprenez mieux le rôle des schémas dans la plate-forme d’expérience, vous êtes prêt à début à composer les vôtres.

Pour découvrir les principes de conception et les meilleures pratiques de composition des schémas à utiliser avec Experience Platform, commencez par lire les [bases de la composition](schema/composition.md)des schémas. Pour obtenir des instructions détaillées sur la création d’un schéma, consultez les didacticiels sur la création d’un schéma à l’ [aide de l’API](tutorials/create-schema-api.md) ou [à l’aide de l’interface](tutorials/create-schema-ui.md)utilisateur.