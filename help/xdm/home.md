---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Système XDM (Experience Data Model)
topic: overview
translation-type: tm+mt
source-git-commit: c07f926a71447e840c692ed15e85c9e02f1106ab

---


# Présentation du système XDM

La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. Le modèle de données d’expérience (XDM), piloté par Adobe, vise à normaliser les données d’expérience client et à définir des  pour la gestion de l’expérience client.

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences numériques. Il fournit des structures et des définitions communes pour toute application à utiliser pour communiquer avec les services de Plateforme. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune qui peut fournir des informations d’une manière plus rapide et plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des  de clients  par le biais de segments et exprimer les attributs du client à des fins de personnalisation.

XDM est la structure de base qui permet à Adobe Experience Cloud, optimisé par Experience Platform, de transmettre le message approprié à la bonne personne, sur le bon , exactement au bon moment. La méthodologie sur laquelle est construite la plateforme d’expérience, **XDM System**, rend opérationnel le de modèles de données d’expérience pour l’utilisation par les services de plateforme.

Ce donne une vue d’ensemble du rôle du système XDM dans Experience Platform.

##  XDM

Experience Platform utilise des  pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il devient plus facile de conserver une signification et, par conséquent, de tirer profit des données.

Avant que les données ne puissent être assimilées dans la plateforme, un  de doit être composé pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenues dans chaque champ. Les  de se composent d’une classe de base et de zéro ou plusieurs mixins.

Pour plus d&#39;informations sur le modèle de composition , y compris les principes de conception et les meilleures pratiques, voir les [bases de la composition](schema/composition.md).

### Registre  et bibliothèque de

Le Registre **des** fournit une interface utilisateur et une API RESTful à partir de laquelle vous pouvez et gérer toutes les ressources liées aux **dans la bibliothèque** dedede la plateforme Adobe Experience Platform. La bibliothèque de  contient des ressources standard du secteur que vous avez mises à votre disposition par Adobe, ainsi que des ressources des partenaires d’Experience Platform et des fournisseurs dont vous utilisez les applications. L’interface utilisateur et l’API du Registre des  peuvent également être utilisées pour créer et gérer de nouveaux et ressources propres à votre organisation.

Pour obtenir un guide détaillé des principales opérations disponibles dans le Registre des , consultez le guide [de développement du Registre des](api/getting-started.md).

## Comportements de données dans le système XDM {#data-behaviors}

Les données destinées à être utilisées dans la plate-forme d’expérience sont regroupées en deux types de comportement :

* **Enregistrer les données**: Fournit des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu.
* **Données** de la série chronologique : Fournit un instantané du système au moment où une action a été effectuée directement ou indirectement par un sujet d&#39;enregistrement.

Tous les XDM décrivent des données pouvant être classées comme enregistrements ou séries chronologiques. Le comportement des données d’un  de est défini par la **classe** de  de, qui est affectée à un  lors de sa création. Les classes XDM décrivent le plus petit nombre de propriétés qu’un doit contenir pour représenter un comportement de données particulier.

Bien que vous puissiez définir vos propres classes dans le Registre des  de, il est recommandé d&#39;utiliser les classes préférées **XDM Individuel** et **XDM ExperienceEvent** pour les données d&#39;enregistrement et de série chronologique, respectivement. Ces classes sont décrites plus en détail ci-dessous.

###  de XDM individuel

XDM Les  individuels sont une classe basée sur les enregistrements qui forme une représentation singulière des attributs des sujets identifiés et partiellement identifiés. Les  hautement identifiés peuvent être utilisés pour des communications personnelles ou des engagements ciblés et peuvent contenir des renseignements personnels détaillés tels que le nom, le sexe, la date de naissance, le lieu et les coordonnées, y compris les numéros de téléphone et les adresses électroniques.

Les  moins identifiés peuvent être constitués uniquement de signaux comportementaux anonymes, tels que des cookies de navigateur. Dans ce cas, les données  éparses sont utilisées pour constituer une base d&#39;informations dans laquelle les intérêts et les préférences du anonyme sont rassemblés et stockés. Ces identifiants peuvent devenir plus détaillés au fil du temps lorsque le sujet s’inscrit pour recevoir des notifications,  des , des achats, etc. Cette augmentation des attributs de  de peut éventuellement donner lieu à un sujet identifié et permettre un degré d’engagement ciblé plus élevé.

À mesure qu&#39;un de consommateurs continue de croître, il devient un solide référentiel de renseignements personnels, d&#39;informations d&#39;identification, de coordonnées et de préférences de communication d&#39;une personne.

### XDM ExperienceEvent

XDM ExperienceEvent est une classe basée sur des séries chronologiques utilisée pour capturer l’état du système lorsqu’un (ou un ensemble de ) s’est produit, y compris le moment et l’identité du sujet concerné. Les  d&#39;expérience sont des données factuelles de ce qui s&#39;est passé, elles sont donc immuables et représentent ce qui s&#39;est passé sans agrégation ni interprétation. Elles sont essentielles pour l’analyse du domaine temporel, car elles peuvent être utilisées pour analyser les modifications qui surviennent dans une période donnée et pour comparer plusieurs périodes afin de suivre les tendances.

Les  d’expérience peuvent être explicites ou implicites. Les  explicites sont des actions humaines directement observables qui se déroulent à un moment du voyage. Les  implicites sont des  qui sont élevés sans action humaine directe, mais qui sont toujours liés à un individu. Les exemples de  implicites peuvent inclure l’envoi planifié de bulletins d’information par courrier électronique ou la tension de batterie atteignant un certain seuil.

Bien que tous les ne soient pas facilement classés dans toutes les sources de données, il est extrêmement utile d&#39;harmoniser des similaires dans des types similaires lorsque cela est possible pour le traitement.

![Voyage du client ExperienceEvent](images/overview/experience-event-journey.png)

##  XDM et services Experience Platform

Experience Platform est  agnostique, ce qui signifie que tout  conforme à la norme XDM peut être utilisé par les services Platform. Les modalités d’utilisation des  par les différents services de plateforme sont décrites plus en détail ci-dessous.

### Service Catalogue, Ingestion des données et Data Lake

Le service de catalogue est le système d’enregistrement des ressources de la plateforme d’expérience et de leurs  connexes. Le catalogue ne correspond pas aux fichiers ou répertoires contenant des données, mais aux métadonnées et descriptions de ces fichiers et répertoires.

Les données du catalogue sont stockées dans Data Lake, une banque de données très granulaire contenant toutes les données gérées par Platform, quel que soit le format de fichier ou le  .

Pour commencer à importer des données dans la plateforme d’expérience, un jeu de données est créé à l’aide du service de catalogue. Le jeu de données fait référence à un XDM décrivant la structure des données à assimiler. Si un jeu de données est créé sans  de, la plateforme d’expérience dérive un &quot;observé&quot; en examinant le type et le contenu des champs de données assimilées. Les ensembles de données sont ensuite suivis dans le catalogue et stockés dans le lac Data, le long du  et du observé sur lequel ils sont basés.

Pour plus d’informations sur le catalogue, voir la présentation [du service de](../catalog/home.md)catalogue. Pour plus d’informations sur l’administration des données d’Adobe Experience Platform, reportez-vous à la section Présentation [de l’administration des](../ingestion/home.md)données.

### Service 

Le service de Adobe Experience Platform vous permet d’utiliser le langage SQL standard pour  les données de la plateforme Experience Platform afin de prendre en charge de nombreux cas d’utilisation différents.

Une fois qu’un a été composé et qu’un jeu de données a été créé qui fait référence à ce, les données sont alors ingérées et stockées dans le lac Data. Grâce au service de , vous pouvez joindre n’importe quel jeu de données dans le lac Data et capturer les résultats  du sous forme d’un nouveau jeu de données à utiliser dans les , l’apprentissage automatique ou pour l’assimilation dans le client en temps réel.

Pour en savoir plus sur le service , veuillez consulter l&#39;introduction [du service ](../query-service/home.md).

### Profil client en temps réel

Le de clients en temps réel fournit un de consommateurs centralisé pour une gestion d’expérience ciblée et personnalisée. Chaque  contient des données qui sont agrégées sur tous les systèmes, ainsi que des comptes horodatés exploitables de  de impliquant les personnes qui ont eu lieu sur l’un des systèmes que vous utilisez avec Experience Platform.

Le de clients en temps réel  utilise des données au format  basées sur les classes XDM Individuelle ou XDM ExperienceEvent et répond aux en fonction de ces données.  ne prend pas en charge l’utilisation de  de en fonction d’autres classes.

conserve une instance de chaque client , fusionnant les données pour former une &quot;source unique de vérité&quot; pour l’individu. Ces données unifiées sont représentées à l’aide de ce qu’on appelle un &quot;  &quot;. Un      les champs de tous les qui implémentent la même classe dans un seul et même.  Lors de la composition d’un à l’aide de l’interface utilisateur ou de l’API, vous pouvez activer le pour l’utilisation avec l’ Client en temps réel et le marquer pour l’inclusion dans lede. Le balisé  alors à participer à la définition de  être alimenté à l’ de l’utilisateur.

Comme les données XDM Individuel  et XDM ExperienceEvent sont assimilées et gérées par le catalogue, cela déclenche l’assimilation en temps réel des données qui ont été activées pour son utilisation par le client. Plus les interactions et les détails sont ingérés, plus le individuel devient robuste.

Les données de  de XDM individuels permettent d’informer et d’autonomiser les actions dans toute  de ou intégration de solution Adobe. Lorsqu’elles sont associées à une riche histoire de données comportementales et d’interactions, ces données sont utilisées pour alimenter l’apprentissage automatique. L’API  client en temps réel peut également être utilisée pour enrichir les fonctionnalités des solutions tierces, des solutions de gestion de la relation client et des solutions propriétaires.

Pour plus d’informations, reportez-vous à l’aperçu [du de clients en temps](../profile/home.md) réel.

### Espace de travail Data Science

Adobe Experience Platform Data Science Workspace utilise l’apprentissage automatique et l’intelligence artificielle pour obtenir des informations à partir des données stockées dans Experience Platform. Data Science Workspace permet aux chercheurs de données de créer des recettes basées sur les données XDM Individuel  et XDM ExperienceEvent relatives aux clients et à leur -, ce qui facilite les prédictions, telles que la propension à acheter et lesrecommandations d’que l’individu est susceptible d’apprécier et d’utiliser.

Avec Data Science Workspace, les chercheurs en données peuvent facilement créer des API de services intelligents optimisées par l’apprentissage automatique. Ces services fonctionnent avec d’autres solutions Adobe, notamment Adobe  et Adobe Analytics Cloud, pour vous aider à automatiser les expériences numériques ciblées et personnalisées.

Pour plus d’informations sur l’utilisation des données de plateforme d’expérience pour alimenter les statistiques, voir la présentation [de](../data-science-workspace/home.md)Data Science Workspace.

### Service de prise de décision

Le service de prise de décision offre la possibilité de configurer la prise de décision   personnalisée dans les applications intégrées à la plateforme.   peut être des recommandations de produits, des composants de contenu pour une expérience Web, des scripts de conversation et des actions à entreprendre.

Le service de prise de décision utilise les données de de clients en temps réel et est donc uniquement compatible avec les jeux de données basés sur l’implémentation de la classe XDM Individuel ou XDM ExperienceEvent .

See the [Decisioning Service overview](../decisioning-service/home.md) for more information.

## Étapes suivantes

Maintenant que vous comprenez mieux le rôle de l’dans Experience Platform, vous êtes prêt à vous  à composer le vôtre.

Pour apprendre les principes de conception et les bonnes pratiques pour composer des à utiliser avec Experience Platform, commencez par lire les [bases de la composition](schema/composition.md)de . Pour obtenir des instructions détaillées sur la création d’un  de, reportez-vous aux didacticiels sur la création d’un à l’aide de l’API [ou](tutorials/create-schema-api.md) de l’interface [](tutorials/create-schema-ui.md)utilisateur.