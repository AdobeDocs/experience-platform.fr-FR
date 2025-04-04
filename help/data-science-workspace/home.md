---
keywords: Experience Platform;accueil;Espace de travail de science des données;rubriques populaires;espace de travail de science des donnée;science des données
solution: Experience Platform
title: Présentation de l’espace de travail de science des données
description: Ce guide présente les concepts clés de l’espace de travail de science des données dans Adobe Experience Platform.
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 99%

---

# Présentation de l’espace de travail de science des données

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

[!DNL Data Science Workspace] dans Adobe Experience Platform utilise le machine learning et lʼintelligence artificielle pour exploiter les informations contenues dans vos données. Intégré à Adobe Experience Platform, [!DNL Data Science Workspace] vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de lʼensemble des solutions Adobe.

Les spécialistes des données de tout niveau de compétence trouveront des outils sophistiqués et faciles à utiliser qui aident au développement, à la formation et au réglage rapide de recettes de machine learning pour vous faire bénéficier de tous les avantages de la technologie IA sans sa complexité.

Avec [!DNL Data Science Workspace], les spécialistes des données peuvent facilement créer des API de services intelligents optimisés par le machine learning. Ces services fonctionnent avec d’autres services Adobe, notamment Adobe Target et Adobe Analytics Cloud, pour vous aider à automatiser les expériences digitales ciblées et personnalisées dans les applications web, de bureau et mobiles.

Ce guide présente les concepts clés liés à [!DNL Data Science Workspace].

## Introduction

Les entreprises d’aujourd’hui accordent une grande priorité à l’exploration du Big Data pour obtenir des prévisions et des informations qui les aideront à personnaliser les expériences client et à offrir plus de valeur aux clients et à l’entreprise.
Aussi importante qu’elle soit, la transformation des données en informations peut se révéler très coûteuse. Cela requiert généralement des spécialistes des données compétents qui effectuent des recherches de données intensives et chronophages pour développer des modèles d’apprentissage automatique ou des recettes, qui optimisent les services intelligents. Le processus est long, la technologie est complexe et les spécialistes des données compétents peuvent être difficiles à trouver.

Avec [!DNL Data Science Workspace], Adobe Experience Platform vous permet de mettre en place une IA axée sur lʼexpérience à lʼéchelle de lʼentreprise, en rationalisant et en accélérant les conversions des données en informations et ensuite en code à lʼaide des solutions suivantes :
- Une structure et une exécution de machine learning
- Accès intégré à vos données stockées dans Adobe Experience Platform
- Schéma de données unifié basé sur [!DNL Experience Data Model] (XDM)
- La puissance de calcul indispensable au machine learning/IA et à la gestion des jeux de données volumineux
- Recettes de machine learning prédéfinies pour accélérer la transition vers des expériences basées sur l’IA
- Création, réutilisation et modification simplifiées des recettes pour les spécialistes des données de différents niveaux de compétence
- Publication et partage de services intelligents en quelques clics seulement (sans développeur), surveillance et nouvelle formation pour une optimisation continue des expériences client personnalisées

Les spécialistes des données de tout niveau de compétence pourront obtenir plus rapidement des informations et des expériences digitales plus efficaces.

## Prise en main

Avant de rentrer dans les détails de [!DNL Data Science Workspace], voici un résumé des termes clés :

| Terme | Définition |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] dans [!DNL Experience Platform] permet aux clients de créer des modèles de machine learning à lʼaide de données dans [!DNL Experience Platform] et les solutions Adobe afin de générer des informations et des prévisions intelligentes pour proposer des expériences digitales exceptionnelles à lʼutilisateur final. |
| Intelligence artificielle | L’intelligence artificielle correspond à une théorie et au développement de systèmes informatiques capables d’exécuter des tâches qui nécessitent normalement l’intelligence humaine, comme la perception visuelle, la reconnaissance vocale, la prise de décision et la traduction des différents langages. |
| Machine learning | Le machine learning est le domaine d’étude qui permet aux ordinateurs d’apprendre sans programmation explicite. |
| [!DNL Sensei] ML Framework | [!DNL Sensei] ML Framework est une structure de machine learning unifiée au sein dʼAdobe qui utilise les données dʼ[!DNL Experience Platform] pour permettre aux spécialistes des données de développer des services intelligents basés sur le machine learning de manière plus rapide, évolutive et réutilisable. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM) correspond à la démarche de normalisation menée par Adobe pour définir des schémas standard, tels que [!DNL Profile] et [!DNL ExperienceEvent], pour la gestion de lʼexpérience client. |
| [!DNL JupyterLab] | [!DNL JupyterLab] est une interface web Open Source pour Project Jupyter, étroitement intégrée à [!DNL Experience Platform]. |
| Recettes | Une recette est le terme utilisé par Adobe pour désigner une spécification de modèle. Il s’agit d’un conteneur de niveau supérieur qui représente un machine learning spécifique, un algorithme d’intelligence artificielle ou un ensemble d’algorithmes, une logique de traitement et la configuration nécessaires pour créer et exécuter un modèle entraîné et ainsi aider à résoudre des problèmes d’entreprise spécifiques. |
| Modèle | Un modèle est une instance d’une recette de machine learning entraînée à l’aide de données historiques et de configurations dans le but de résoudre un cas d’usage commercial. |
| Formation | La formation est le processus de formation de modèles et d’informations à partir de données étiquetées. |
| Modèle formé | Un modèle formé représente la sortie exécutable d’un processus de formation de modèle, dans lequel un ensemble de données d’apprentissage a été appliqué à l’instance de modèle. Un modèle formé conserve une référence au service web intelligent qui est créé à partir de celui-ci. Le modèle formé est adapté à la notation et à la création d’un service web intelligent. Les modifications apportées à un modèle formé peuvent être suivies comme une nouvelle version. |
| Notation | La notation est le processus de génération d’informations à partir de données en utilisant un modèle formé. |
| Service | Un service déployé affiche la fonctionnalité d’une intelligence artificielle, d’un modèle de machine learning ou d’un algorithme avancé au moyen d’une API afin qu’elle puisse être utilisée par d’autres services ou applications pour créer des applications intelligentes. |

Le graphique suivant décrit la relation hiérarchique entre les recettes, les modèles, les opérations de formation et les opérations de notation.

![](./images/home/recipe_hiearchy_ui.png)

## Comprendre [!DNL Data Science Workspace]

[!DNL Data Science Workspace] permet à vos spécialistes des données de rationaliser le processus laborieux qui consiste à découvrir des informations dans des jeux de données volumineux. Basé sur une structure et une exécution de machine learning courantes, [!DNL Data Science Workspace] offre une gestion avancée des processus, une gestion des modèles et l’évolutivité. Les services intelligents permettent de réutiliser des recettes de machine learning pour optimiser diverses applications créées à l’aide des produits et solutions Adobe.

### Accès unique aux données

Les données sont la pierre angulaire de l’IA et du machine learning.

[!DNL Data Science Workspace] est entièrement intégré à Adobe Experience Platform, notamment au lac de données, à [!DNL Real-Time Customer Profile], et à [!DNL Unified Edge]. Consultez toutes les données de votre organisation stockées dans Adobe Experience Platform en même temps, ainsi que le Big Data courant et les bibliothèques de Deep Learning, telles que [!DNL Spark] ML et [!DNL TensorFlow]. Si vous ne trouvez pas ce dont vous avez besoin, ingérez vos propres jeux de données à l’aide du schéma XDM normalisé.

### Recettes de machine learning prédéfinies

[!DNL Data Science Workspace] inclut des recettes de machine learning prédéfinies pour répondre aux besoins courants de l’entreprise, comme la prévision des ventes au détail et la détection des anomalies, afin que les spécialistes des données et les développeurs n’aient pas à partir de zéro. Actuellement, trois recettes sont proposées : [la prévision d’achat de produits](./pre-built-recipes/product-purchase-prediction.md), [les recommandations de produits](./pre-built-recipes/product-recommendations.md) et [les ventes au détail](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Si vous préférez, vous pouvez adapter une recette prédéfinie à vos besoins, importer une recette ou partir de zéro pour créer une recette personnalisée. Quel que soit votre choix, lorsque vous formez et optimisez une recette, la création d’un service intelligent personnalisé ne nécessite pas de développeur. Il suffit de quelques clics et vous êtes prêt à créer une expérience digitale ciblée et personnalisée.

### Processus axé sur le spécialiste des données

Quel que soit votre niveau de compétence en matière de science des données, [!DNL Data Science Workspace] permet de simplifier et dʼaccélérer le processus de recherche dʼinformations dans les données et leur application à des expériences digitales.

### Exploration des données

Trouver les données adéquates et les préparer représente la partie la plus laborieuse de la création d’une recette efficace. [!DNL Data Science Workspace] et Adobe Experience Platform vous permettent de passer plus rapidement des données aux informations.

Sur Adobe Experience Platform, vos données des différents canaux sont centralisées et stockées dans le schéma XDM normalisé. Les données sont donc plus faciles à trouver, à comprendre et à nettoyer. Une seule banque de données basée sur un schéma commun peut vous faire économiser d’innombrables heures d’exploration et de préparation de données.

Pendant votre navigation, utilisez R, [!DNL Python], ou Scala avec [!DNL Jupyter Notebook] intégré et hébergé pour parcourir le catalogue de données de [!DNL Experience Platform]. Vous pouvez également profiter de [!DNL Spark] ML et TensorFlow en utilisant lʼun de ces langages. Partez de zéro ou utilisez l’un des modèles de notebook fournis pour des problèmes d’entreprise spécifiques.

Dans le cadre du processus d’exploration des données, vous pouvez également ingérer de nouvelles données ou utiliser des fonctionnalités existantes pour faciliter la préparation des données.

### Création

[!DNL Data Science Workspace] vous permet de choisir la méthode de création des recettes.

- Gagnez du temps en recherchant une recette prédéfinie qui répond aux besoins de votre entreprise, que vous pouvez utiliser en l’état ou configurer pour répondre à vos besoins spécifiques.
- Créez une recette à partir de zéro, en utilisant l’exécution de création du notebook Jupyter pour développer et enregistrer la recette.
- Chargez une recette créée en dehors dʼAdobe Experience Platform dans [!DNL Data Science Workspace] ou importez le code de recette dʼun référentiel, comme [!DNL Git], à lʼaide de lʼauthentification et de lʼintégration disponibles entre [!DNL Git] et [!DNL Data Science Workspace].

### Expérimentation

L’espace de travail de science des données offre une flexibilité exceptionnelle au processus d’expérimentation. Commencez par votre recette. Créez ensuite une instance distincte, en utilisant le même algorithme principal associé à des caractéristiques uniques, telles que des paramètres d’optimisation. Vous pouvez créer autant d’instances que vous le souhaitez, en formant et en notant chaque instance autant de fois que vous le souhaitez. Lorsque vous les formez, [!DNL Data Science Workspace] suit les recettes, les instances de recette et les instances formées, ainsi que les mesures dʼévaluation, afin que vous nʼayez pas à le faire.

### Mise en œuvre

Lorsque vous êtes satisfait de votre recette, il suffit de quelques clics pour créer un service intelligent. Aucun codage n’est nécessaire, vous pouvez le faire vous-même, sans faire appel à un développeur ou à un ingénieur. Enfin, publiez le service intelligent sur Adobe IO et il est prêt à être utilisé par votre équipe d’expérience digitale.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Amélioration continue

[!DNL Data Science Workspace] permet de suivre les endroits où sont invoqués les services intelligents et leurs performances. À mesure que les données arrivent, vous pouvez évaluer la précision des services intelligents afin de fermer la boucle et de reformer les recettes en fonction des besoins pour améliorer les performances. La précision de la personnalisation des clients est ainsi sans cesse améliorée.

### Accès aux nouvelles fonctionnalités et aux nouveaux jeux de données

Les spécialistes des données peuvent tirer parti des nouvelles technologies et des nouveaux jeux de données dès qu’ils sont disponibles via les services Adobe. Grâce à des mises à jour fréquentes, nous nous chargeons d’intégrer les jeux de données et les technologies dans la plateforme, afin que vous n’ayez pas à le faire.

### Sécurité et tranquillité d’esprit

La protection de vos données est une priorité absolue pour Adobe. Adobe protège vos données à l’aide de processus et de contrôles de sécurité développés pour vous aider à vous conformer aux normes, réglementations et certifications reconnues par le secteur.

La sécurité est intégrée aux logiciels et services dans le cadre d’Adobe SPLC (Secure Product Lifecycle).
Pour en savoir plus sur la sécurité des données et des logiciels Adobe, la conformité, etc., consultez la page de sécurité à l’adresse https://www.adobe.com/fr/security.html.

## [!DNL Data Science Workspace] en action

Les prévisions et les insights fournissent les informations dont vous avez besoin pour offrir une expérience hautement personnalisée à chaque client qui visite votre site web, contacte votre centre d’appel ou participe à d’autres expériences digitales. Découvrez le déroulement de votre travail quotidien avec [!DNL Data Science Workspace].

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
Toutes les données d’Adobe Experience Platform sont conformes au schéma XDM normalisé, ce qui élimine la nécessité de créer un modèle complexe pour associer les données ou d’obtenir de l’aide d’un ingénieur en données.

Si vous ne trouvez pas immédiatement les données dont vous avez besoin, mais qu’elles existent en dehors d’Adobe Experience Platform, il est relativement simple d’ingérer des jeux de données supplémentaires, qui se transformeront également en schéma XDM normalisé.\
Vous pouvez utiliser [!DNL Jupyter Notebook] pour simplifier le prétraitement des données, en commençant éventuellement par un modèle de notebook ou un notebook que vous avez déjà utilisé pour la propension à acheter.

![](./images/home/notebook_templates-new.png)

### Création de la recette

Si vous avez déjà trouvé une recette qui répond à tous vos besoins, vous pouvez passer à l’expérimentation. Vous pouvez aussi légèrement modifier la recette ou en créer une à partir de zéro, en profitant de lʼexécution de création de [!DNL Data Science Workspace] dans [!DNL Jupyter Notebook]. Lʼutilisation de lʼexécution de création vous permet dʼutiliser le processus de formation et de notation de [!DNL Data Science Workspace] et de convertir la recette ultérieurement afin que dʼautres membres de votre organisation puissent la stocker et la réutiliser.

Vous pouvez également importer une recette dans [!DNL Data Science Workspace] et tirer parti du processus dʼexpérimentation lors de la création de votre service intelligent.

### Expérience avec la recette

Une recette qui intègre vos principaux algorithmes de machine learning permet de créer de nombreuses instances de recette à l’aide d’une seule recette. Ces instances de recette sont appelées modèles. Un modèle nécessite une formation et une évaluation pour optimiser son fonctionnement et son efficacité, un processus généralement constitué d’essais et d’erreurs.

![](./images/home/recipe_hiearchy_ui.png)

Lorsque vous formez vos modèles, des opérations et des évaluations de formation sont générées. [!DNL Data Science Workspace] effectue le suivi des mesures d’évaluation pour chaque modèle unique et de leurs opérations de formation. Les mesures d’évaluation générées par l’expérimentation vous permettent de déterminer l’opération de formation la plus performante.

![](./images/home/evaluation_metrics.png)

Consultez le tutoriel sur lʼ[API](./models-recipes/train-evaluate-model-api.md) ou sur lʼ[UI](./models-recipes/train-evaluate-model-ui.md) sur la manière de former et dʼévaluer les modèles dans [!DNL Data Science Workspace].

### Mise en œuvre du modèle

Lorsque vous avez sélectionné la recette la mieux formée pour répondre aux besoins de votre entreprise, vous pouvez créer un service intelligent dans [!DNL Data Science Workspace] sans lʼaide dʼun développeur. Il suffit de quelques clics et aucun codage n’est nécessaire. Les autres membres de votre organisation peuvent accéder à un service intelligent publié sans devoir en recréer le modèle.

Un service intelligent publié peut être configuré pour se former automatiquement de temps en temps à l’aide de nouvelles données dès qu’elles sont disponibles. Vous garantissez ainsi l’efficacité de votre service au fil du temps.

## Étapes suivantes

[!DNL Data Science Workspace] permet de rationaliser et de simplifier le processus de science des données, de la collecte de données aux algorithmes en passant par les services intelligents pour les spécialistes des données de tout niveau de compétence. Les outils sophistiqués de [!DNL Data Science Workspace] vous permettent de réduire considérablement le temps nécessaire pour convertir les données en informations.

Plus important encore, [!DNL Data Science Workspace] place les fonctionnalités de science des données et dʼoptimisation algorithmique de la principale plateforme marketing dʼAdobe entre les mains des spécialistes des données dʼentreprise. Pour la première fois, les entreprises peuvent intégrer des algorithmes propriétaires à la plateforme, en tirant parti des puissantes fonctionnalités de machine learning et d’IA d’Adobe pour offrir des expériences client hautement personnalisées à grande échelle.

L’alliance de l’expertise en matière de marques et des prouesses d’Adobe en matière de machine learning et d’IA permet aux entreprises de développer la valeur de l’entreprise et la fidélité à la marque en donnant aux clients ce qu’ils veulent, avant qu’ils ne le demandent.

Pour plus d’informations, comme un processus quotidien complet, commencez par lire la documentation de [présentation de l’espace de travail de science des données](./walkthrough.md).

## Ressources supplémentaires

La vidéo suivante est conçue pour vous aider à comprendre [!DNL Data Science Workspace].

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)