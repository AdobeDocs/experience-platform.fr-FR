---
keywords: Experience Platform ; accueil ; Espace de travail des sciences de données ; sujets populaires ; espace de travail des sciences de données ; sciences des données
solution: Experience Platform
title: Présentation de l’espace de travail Data Science
topic-legacy: overview
description: Ce guide présente un aperçu des concepts clés liés à Data Science Workspace à Adobe Experience Platform.
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 73%

---

# Présentation de Data Science Workspace

Adobe Experience Platform [!DNL Data Science Workspace] utilise l&#39;apprentissage automatique et l&#39;intelligence artificielle pour libérer des connaissances à partir de vos données. Intégré dans Adobe Experience Platform, [!DNL Data Science Workspace] vous aide à faire des prédictions à l’aide de vos contenus et de vos ressources de données dans les solutions d’Adobe.

Les spécialistes des données de tout niveau de compétence trouveront des outils sophistiqués et faciles à utiliser qui aident au développement, à la formation et au réglage rapide de recettes d’apprentissage automatique pour vous faire bénéficier de tous les avantages de la technologie IA sans sa complexité.

Avec [!DNL Data Science Workspace], les chercheurs en données peuvent facilement créer des API de services intelligents, optimisées par l&#39;apprentissage automatique. Ces services fonctionnent avec d’autres services Adobe, notamment Adobe Target et Adobe Analytics Cloud, pour vous aider à automatiser les expériences numériques ciblées et personnalisées dans les applications web, de bureau et mobiles.

Ce guide présente un aperçu des concepts clés liés à [!DNL Data Science Workspace].

## Introduction

Les entreprises d’aujourd’hui accordent une grande priorité à l’exploration du Big Data pour obtenir des prévisions et des informations qui les aideront à personnaliser les expériences client et à offrir plus de valeur aux clients et à l’entreprise.
Aussi importante qu’elle soit, la transformation des données en informations peut se révéler très coûteuse. Cela requiert généralement des spécialistes des données compétents qui effectuent des recherches de données intensives et chronophages pour développer des modèles d’apprentissage automatique ou des recettes, qui optimisent les services intelligents. Le processus est long, la technologie est complexe et les spécialistes des données compétents peuvent être difficiles à trouver.

Grâce à [!DNL Data Science Workspace], Adobe Experience Platform vous permet d’apporter une intelligence d’affaires axée sur l’expérience à l’échelle de l’entreprise, en rationalisant et en accélérant les conversions de données en données d’expérience en code avec :
- Une structure et une exécution d’apprentissage automatique
- Accès intégré à vos données stockées dans Adobe Experience Platform
- Schéma de données unifié basé sur [!DNL Experience Data Model] (XDM)
- La puissance de calcul indispensable à l’apprentissage automatique/IA et à la gestion des jeux de données volumineux
- Recettes d’apprentissage automatique prédéfinies pour accélérer la transition vers des expériences basées sur l’IA
- Création, réutilisation et modification simplifiées des recettes pour les spécialistes des données de différents niveaux de compétence
- Publication et partage de services intelligents en quelques clics seulement (sans développeur), surveillance et nouvelle formation pour une optimisation continue des expériences client personnalisées

Les spécialistes des données de tout niveau de compétence pourront obtenir plus rapidement des informations et des expériences numériques plus efficaces.

## Prise en main

Avant d&#39;entrer dans les détails de [!DNL Data Science Workspace], voici un bref résumé des termes clés :

| Terme | Définition |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] permet  [!DNL Experience Platform] aux clients de créer des modèles d’apprentissage automatique utilisant des données entre  [!DNL Experience Platform] et des solutions d’Adobe pour générer des aperçus et des prédictions intelligents afin de tisser de merveilleuses expériences numériques d’utilisateur final. |
| Intelligence artificielle | L’intelligence artificielle correspond à une théorie et au développement de systèmes informatiques capables d’exécuter des tâches qui nécessitent normalement l’intelligence humaine, comme la perception visuelle, la reconnaissance vocale, la prise de décision et la traduction des différents langages. |
| Apprentissage automatique | L’apprentissage automatique est le domaine d’étude qui permet aux ordinateurs d’apprendre sans programmation explicite. |
| [!DNL Sensei] ML Framework | [!DNL Sensei] ML Framework est un cadre unifié d&#39;apprentissage automatique à l&#39;échelle de l&#39;Adobe qui utilise les données  [!DNL Experience Platform] pour donner aux scientifiques des données les moyens de développer des services de renseignement pilotés par l&#39;apprentissage automatique d&#39;une manière plus rapide, évolutive et réutilisable. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM) est l’effort de normalisation mené par l’Adobe pour définir des schémas standard, tels que  [!DNL Profile] et  [!DNL ExperienceEvent], pour la gestion de l’expérience client. |
| [!DNL JupyterLab] | [!DNL JupyterLab] est une interface web Open Source pour Project Jupyter, étroitement intégrée à [!DNL Experience Platform]. |
| Recettes | Une recette est le terme utilisé par Adobe pour désigner une spécification de modèle. Il s’agit d’un conteneur de niveau supérieur qui représente un apprentissage automatique spécifique, un algorithme d’intelligence artificielle ou un ensemble d’algorithmes, une logique de traitement et la configuration nécessaires pour créer et exécuter un modèle formé et ainsi aider à résoudre des problèmes d’entreprise spécifiques. |
| Modèle | Un modèle est une instance d’une recette d’apprentissage automatique formée à l’aide de données historiques et de configurations dans le but de résoudre un cas d’usage commercial. |
| Formation | La formation est le processus de formation de modèles et de connaissances à partir de données étiquetées. |
| Modèle formé | Un modèle formé représente la sortie exécutable d’un processus de formation de modèle, dans lequel un ensemble de données d’apprentissage a été appliqué à l’instance de modèle. Un modèle formé conserve une référence à tout service Web intelligent qui est créé à partir de celui-ci. Le modèle formé est adapté à la notation et à la création d’un service web intelligent. Les modifications apportées à un modèle formé peuvent être suivies comme une nouvelle version. |
| Notation | La notation est le processus de génération d’informations à partir de données en utilisant un modèle formé. |
| Service | Un service déployé affiche la fonctionnalité d’une intelligence artificielle, d’un modèle d’apprentissage automatique ou d’un algorithme avancé au moyen d’une API afin qu’elle puisse être utilisée par d’autres services ou applications pour créer des applications intelligentes. |

Le graphique suivant décrit la relation hiérarchique entre les recettes, les modèles, les opérations de formation et les opérations de notation.

![](./images/home/recipe_hiearchy_ui.png)

## Présentation de [!DNL Data Science Workspace]

Avec [!DNL Data Science Workspace], vos spécialistes des données peuvent simplifier le processus encombrant de découverte d&#39;informations dans des jeux de données volumineux. Basé sur un cadre d&#39;apprentissage automatique et un environnement d&#39;exécution communs, [!DNL Data Science Workspace] offre une gestion avancée des processus, une gestion des modèles et une évolutivité. Les services intelligents permettent de réutiliser des recettes d’apprentissage automatique pour optimiser diverses applications créées à l’aide des produits et solutions Adobe.

### Accès unique aux données

Les données sont la pierre angulaire de l’IA et de l’apprentissage automatique.

[!DNL Data Science Workspace] est entièrement intégrée à Adobe Experience Platform, y compris le lac Data,  [!DNL Real-time Customer Profile]et  [!DNL Unified Edge]. Explorez toutes vos données d&#39;entreprise stockées en même temps dans Adobe Experience Platform, ainsi que les big data courantes et les bibliothèques d&#39;apprentissage profond, telles que [!DNL Spark] ML et [!DNL TensorFlow]. Si vous ne trouvez pas ce dont vous avez besoin, ingérez vos propres jeux de données à l’aide du schéma XDM normalisé.

### Recettes d’apprentissage automatique prédéfinies

[!DNL Data Science Workspace] inclut des recettes d’apprentissage automatique prédéfinies pour répondre aux besoins courants de l’entreprise, comme la prévision des ventes au détail et la détection des anomalies, afin que les spécialistes des données et les développeurs n’aient pas à partir de zéro. Actuellement, trois recettes sont proposées : [la prévision d’achat de produits](./pre-built-recipes/product-purchase-prediction.md), [les recommandations de produits](./pre-built-recipes/product-recommendations.md) et [les ventes au détail](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Si vous préférez, vous pouvez adapter une recette prédéfinie à vos besoins, importer une recette ou partir de zéro pour créer une recette personnalisée. Quel que soit votre choix, lorsque vous formez et optimisez une recette, la création d’un service intelligent personnalisé ne nécessite pas de développeur. Il suffit de quelques clics et vous êtes prêt à créer une expérience numérique ciblée et personnalisée.

### Processus axé sur le spécialiste des données

Quel que soit votre niveau d&#39;expertise en sciences des données, [!DNL Data Science Workspace] contribue à simplifier et à accélérer le processus de recherche d&#39;informations dans les données et de les appliquer aux expériences numériques.

### Exploration des données

Trouver les données adéquates et les préparer représente la partie la plus laborieuse de la création d’une recette efficace. [!DNL Data Science Workspace] et Adobe Experience Platform vous permettent de passer plus rapidement des données aux informations.

Sur Adobe Experience Platform, vos données des différents canaux sont centralisées et stockées dans le schéma XDM normalisé. Les données sont donc plus faciles à trouver, à comprendre et à nettoyer. Une seule banque de données basée sur un schéma commun peut vous faire économiser d’innombrables heures d’exploration et de préparation de données.

Lorsque vous naviguez, utilisez R, [!DNL Python] ou Scala avec l’élément intégré hébergé [!DNL Jupyter Notebook] pour parcourir le catalogue de données sur [!DNL Platform]. En utilisant l&#39;une de ces langues, vous pouvez également tirer parti de [!DNL Spark] ML et de TensorFlow. Partez de zéro ou utilisez l’un des modèles de notebook fournis pour des problèmes d’entreprise spécifiques.

Dans le cadre du processus d’exploration des données, vous pouvez également ingérer de nouvelles données ou utiliser des fonctionnalités existantes pour faciliter la préparation des données.

### Création

Avec [!DNL Data Science Workspace], vous décidez de la manière dont vous souhaitez créer des recettes.

- Gagnez du temps en recherchant une recette prédéfinie qui répond aux besoins de votre entreprise, que vous pouvez utiliser en l’état ou configurer pour répondre à vos besoins spécifiques.
- Créez une recette à partir de zéro, en utilisant l’exécution de création du notebook Jupyter pour développer et enregistrer la recette.
- Téléchargez une recette créée en dehors de Adobe Experience Platform dans [!DNL Data Science Workspace] ou importez le code de recette d&#39;un référentiel, tel que [!DNL Git], en utilisant l&#39;authentification et l&#39;intégration disponibles entre [!DNL Git] et [!DNL Data Science Workspace].

### Expérimentation

Data Science Workspace offre une flexibilité exceptionnelle au processus d’expérimentation. Commencez par votre recette. Créez ensuite une instance distincte, en utilisant le même algorithme principal associé à des caractéristiques uniques, telles que des paramètres d’optimisation. Vous pouvez créer autant d’instances que vous le souhaitez, en formant et en notant chaque instance autant de fois que vous le souhaitez. Lorsque vous les formez, [!DNL Data Science Workspace] suit les recettes, les instances de recette et les instances de formation, ainsi que les mesures d&#39;évaluation, afin que vous n&#39;ayez pas à le faire.

### Mise en œuvre

Lorsque vous êtes satisfait de votre recette, il suffit de quelques clics pour créer un service intelligent. Aucun codage n’est nécessaire, vous pouvez le faire vous-même, sans faire appel à un développeur ou à un ingénieur. Enfin, publiez le service intelligent sur Adobe IO et il est prêt à être utilisé par votre équipe d’expérience numérique.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Amélioration continue

[!DNL Data Science Workspace] effectue le suivi de l’endroit où les services intelligents sont appelés et de leur fonctionnement. À mesure que les données arrivent, vous pouvez évaluer la précision des services intelligents afin de fermer la boucle et de reformer les recettes en fonction des besoins pour améliorer les performances. La précision de la personnalisation des clients est ainsi sans cesse améliorée.

### Accès aux nouvelles fonctionnalités et aux nouveaux jeux de données

Les spécialistes des données peuvent tirer parti des nouvelles technologies et des nouveaux jeux de données dès qu’ils sont disponibles via les services Adobe. Grâce à des mises à jour fréquentes, nous nous chargeons d’intégrer les jeux de données et les technologies dans la plateforme, afin que vous n’ayez pas à le faire.

### Sécurité et tranquillité d’esprit

La protection de vos données est une priorité absolue pour Adobe. Adobe protège vos données à l’aide de processus et de contrôles de sécurité développés pour vous aider à vous conformer aux normes, réglementations et certifications reconnues par le secteur.

La sécurité est intégrée aux logiciels et services dans le cadre d’Adobe SPLC (Secure Product Lifecycle).
Pour en savoir plus sur la sécurité des données et des logiciels Adobe, la conformité, etc., consultez la page de sécurité à l’adresse https://www.adobe.com/fr/security.html.

## [!DNL Data Science Workspace] en action

Les prévisions et les insights fournissent les informations dont vous avez besoin pour offrir une expérience hautement personnalisée à chaque client qui visite votre site web, contacte votre centre d’appel ou participe à d’autres expériences numériques. Voici comment se déroule votre travail quotidien avec [!DNL Data Science Workspace].

### Définition du problème

Tout commence par un problème d’entreprise. Par exemple, un centre d’appel en ligne a besoin de contexte pour l’aider à transformer une opinion négative d’un client en une opinion positive.

Les données sur le client sont nombreuses. Il a consulté le site, placé des articles dans son panier et même passé des commandes. Il a peut-être déjà reçu des courriers électroniques, utilisé des bons de réduction ou contacté le centre d’appel. La recette doit donc utiliser les données disponibles sur le client et ses activités pour déterminer la propension à acheter et recommander une offre que le client est susceptible d’apprécier et d’utiliser.

![](./images/home/example_problem.png)

Lorsqu’il contacte le centre d’appel, le client dispose encore de deux paires de chaussures dans le panier, mais a retiré une chemise. Sur la base de ces informations, le service intelligent peut recommander à l’agent du centre d’appel d’offrir un bon de réduction de 20 % sur les chaussures pendant l’appel. Si le client utilise le bon de réduction, ces informations sont ajoutées au jeu de données et les prévisions s’améliorent davantage lors du prochain appel du client.

### Exploration et préparation des données

En fonction du problème d’entreprise défini, vous savez que la recette doit tenir compte de toutes les transactions web du client, y compris les visites sur le site, les recherches, les pages vues, les liens utilisés, les actions liées au panier, les offres reçues, les courriers électroniques reçus, les interactions avec le centre d’appel, etc.

En règle générale, un spécialiste des données passe jusqu’à 75 % du temps nécessaire à la création d’une recette à explorer et à transformer les données. Les données proviennent souvent de plusieurs référentiels et sont enregistrées dans différents schémas. Elles doivent être combinées et mappées avant de pouvoir être utilisées pour créer une recette.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Si vous partez de zéro ou configurez une recette existante, vous commencez votre recherche de données dans un catalogue de données centralisé et normalisé pour votre organisation, ce qui simplifie considérablement la recherche. Vous pourriez même découvrir qu’un autre spécialiste des données de votre organisation a déjà identifié un jeu de données similaire, et choisir d’optimiser ce jeu de données plutôt que de partir de zéro.
Toutes les données d’Adobe Experience Platform sont conformes au schéma XDM normalisé, ce qui élimine la nécessité de créer un modèle complexe pour associer les données ou d’obtenir de l’aide d’un ingénieur en données.

Si vous ne trouvez pas immédiatement les données dont vous avez besoin, mais qu’elles existent en dehors d’Adobe Experience Platform, il est relativement simple d’ingérer des jeux de données supplémentaires, qui se transformeront également en schéma XDM normalisé.\
Vous pouvez utiliser [!DNL Jupyter Notebook] pour simplifier le prétraitement des données, en commençant éventuellement par un modèle de bloc-notes ou un bloc-notes que vous avez utilisé précédemment pour la propension à acheter.

![](./images/home/notebook_templates.png)

### Création de la recette

Si vous avez déjà trouvé une recette qui répond à tous vos besoins, vous pouvez passer à l’expérimentation. Vous pouvez également modifier un peu la recette ou en créer une à partir de zéro - en profitant de l&#39;exécution de création de [!DNL Data Science Workspace] dans [!DNL Jupyter Notebook]. L&#39;utilisation du runtime de création vous permet d&#39;utiliser à la fois le workflow de formation et de notation [!DNL Data Science Workspace] et de convertir la recette ultérieurement afin qu&#39;elle puisse être stockée et réutilisée par d&#39;autres membres de votre organisation.

Vous pouvez également importer une recette dans [!DNL Data Science Workspace] et tirer parti des workflows d&#39;expérimentation lorsque vous créez votre service intelligent.

### Expérience avec la recette

Une recette qui intègre vos principaux algorithmes d’apprentissage automatique permet de créer de nombreuses instances de recette à l’aide d’une seule recette. Ces instances de recette sont appelées modèles. Un modèle nécessite une formation et une évaluation pour optimiser son fonctionnement et son efficacité, un processus généralement constitué d’essais et d’erreurs.

![](./images/home/recipe_hiearchy_ui.png)

Lorsque vous formez vos modèles, des opérations et des évaluations de formation sont générées. [!DNL Data Science Workspace] effectue le suivi des mesures d’évaluation pour chaque modèle unique et de leurs opérations de formation. Les mesures d’évaluation générées par l’expérimentation vous permettent de déterminer l’opération de formation la plus performante.

![](./images/home/evaluation_metrics.png)

Consultez le [didacticiel API](./models-recipes/train-evaluate-model-api.md) ou [UI](./models-recipes/train-evaluate-model-ui.md) sur la façon de former et d&#39;évaluer les modèles dans [!DNL Data Science Workspace].

### Mise en œuvre du modèle

Lorsque vous avez sélectionné la recette la mieux formée pour répondre à vos besoins commerciaux, vous pouvez créer un service intelligent dans [!DNL Data Science Workspace] sans l&#39;aide des développeurs. Il suffit de quelques clics et aucun codage n’est nécessaire. Les autres membres de votre organisation peuvent accéder à un service intelligent publié sans devoir en recréer le modèle.

Un service intelligent publié peut être configuré pour se former automatiquement de temps en temps à l’aide de nouvelles données dès qu’elles sont disponibles. Vous garantissez ainsi l’efficacité de votre service au fil du temps.

## Étapes suivantes

[!DNL Data Science Workspace] permet de rationaliser et de simplifier le flux de données scientifiques, de la collecte de données aux algorithmes en passant par les services intelligents pour les spécialistes des données de tous les niveaux de compétences. Grâce aux outils sophistiqués [!DNL Data Science Workspace] proposés, vous pouvez considérablement réduire le temps passé des données aux informations.

Plus important encore, [!DNL Data Science Workspace] place les capacités de science des données et d&#39;optimisation algorithmique de la plateforme marketing de pointe du Adobe entre les mains des spécialistes des données d&#39;entreprise. Pour la première fois, les entreprises peuvent intégrer des algorithmes propriétaires à la plateforme, en tirant parti des puissantes fonctionnalités d’apprentissage machine et d’IA d’Adobe pour offrir des expériences client hautement personnalisées à grande échelle.

L’alliance de l’expertise en matière de marques et des prouesses d’Adobe en matière d’apprentissage automatique et d’IA permet aux entreprises de développer la valeur de l’entreprise et la fidélité à la marque en donnant aux clients ce qu’ils veulent, avant qu’ils ne le demandent.

Pour plus d’informations, comme un processus quotidien complet, commencez par lire la documentation de [présentation de Data Science Workspace](./walkthrough.md).

## Ressources supplémentaires

La vidéo suivante est conçue pour vous aider à comprendre [!DNL Data Science Workspace].

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)
