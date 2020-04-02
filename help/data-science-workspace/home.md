---
keywords: Experience Platform;home;Data Science Workspace;popular topics
solution: Experience Platform
title: Présentation de l’espace de travail Data Science
topic: overview
translation-type: tm+mt
source-git-commit: 9f3fc3ec3ce560534b057185e3fef2cc2bc1234d

---


# Présentation de l’espace de travail Data Science

Adobe Experience Platform Data Science Workspace utilise l’apprentissage automatique et l’intelligence artificielle pour libérer des informations à partir de vos données. Intégrée à Adobe Experience Platform, Data Science Workspace vous aide à faire des prédictions à l’aide de votre contenu et de vos ressources de données dans les solutions Adobe.

Les chercheurs en données de tous les niveaux de compétence trouveront des outils sophistiqués et faciles à utiliser qui soutiennent le développement rapide, la formation et l&#39;ajustement des recettes d&#39;apprentissage automatique - tous les avantages de la technologie de l&#39;IA, sans la complexité.

Avec Data Science Workspace, les chercheurs en données peuvent facilement créer des API de services intelligents, optimisées par l’apprentissage automatique. Ces services fonctionnent avec d’autres services Adobe, notamment Adobe  et Adobe Analytics Cloud, pour vous aider à automatiser les expériences numériques ciblées et personnalisées dans les applications Web, de bureau et mobiles.

Ce guide présente un aperçu des concepts clés liés à Data Science Workspace.

## Introduction

L&#39;entreprise d&#39;aujourd&#39;hui accorde une grande priorité à l&#39;extraction des données massives pour les prédictions et les analyses qui les aideront à personnaliser les expériences client et à offrir plus de valeur aux clients - et à l&#39;entreprise.
Aussi important que cela soit, l&#39;obtention de données pour obtenir des informations peut coûter cher. Cela nécessite généralement des scientifiques compétents qui mènent des recherches de données intensives et fastidieuses pour développer des modèles d&#39;apprentissage automatique, ou des recettes, qui génèrent des services intelligents. Le processus est long, la technologie est complexe et les scientifiques spécialisés en données peuvent être difficiles à trouver.

Avec Data Science Workspace, Adobe Experience Platform vous permet d’apporter une IA ciblée sur l’expérience à l’échelle de l’entreprise, en rationalisant et en accélérant les conversions de données vers des informations à code à l’aide des outils suivants :
- Un cadre d’apprentissage automatique et un environnement d’exécution
- Accès intégré à vos données stockées dans Adobe Experience Platform
- Un de données unifié basé sur le modèle de données d’expérience (XDM)
- Puissance informatique essentielle pour l&#39;apprentissage/l&#39;IA des machines et la gestion des grands ensembles de données
- Recettes d’apprentissage automatique prédéfinies pour accélérer le saut vers les expériences pilotées par l’IA
- Création, réutilisation et modification simplifiées des recettes pour les spécialistes des données de différents niveaux de compétence
- Publication et partage de services intelligents en quelques clics - sans développeur - et surveillance et recyclage pour une optimisation continue des expériences client personnalisées

Les spécialistes des données de tous les niveaux de compétence pourront obtenir des informations plus rapidement et plus rapidement sur les expériences numériques.

## Prise en main

Avant de vous plonger dans les détails de Data Science Workspace, voici un bref résumé des termes clés :

| Terme | Définition |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Espace de travail Data Science | Data Science Workspace dans Experience Platform permet aux clients de créer des modèles d’apprentissage automatique à l’aide de données dans Experience Platform et les solutions Adobe afin de générer des aperçus et des prédictions intelligents pour tisser de superbes expériences numériques d’utilisateur final. |
| Intelligence artificielle | L&#39;intelligence artificielle est une théorie et un développement de systèmes informatiques capables de réaliser des  qui nécessitent normalement l&#39;intelligence humaine, comme la perception visuelle, la reconnaissance vocale, la prise de décision et la traduction entre les langues. |
| Apprentissage automatique | L&#39;apprentissage automatique est le domaine d&#39;étude qui permet aux ordinateurs d&#39;apprendre sans être explicitement programmés. |
| Cadre LML Sensei | Sensei ML Framework est une structure d’apprentissage automatique unifiée à travers Adobe qui utilise les données de la plateforme Experience Platform pour permettre aux chercheurs de données de développer des services de renseignement pilotés par l’apprentissage automatique d’une manière plus rapide, évolutive et réutilisable. |
| Modèle de données d’expérience | Le modèle de données d’expérience (XDM) est l’effort de normalisation mené par Adobe pour définir des  standard, telles que  et ExperienceEvent, pour la gestion de l’expérience client. |
| JupyterLab | JupyterLab est une interface Web open-source pour Project Jupyter et est étroitement intégrée à Experience Platform. |
| Recettes | Une recette est le terme utilisé par Adobe pour désigner une spécification de modèle. Il s’agit d’un de niveau supérieur qui représente un apprentissage automatique spécifique, un algorithme AI ou un ensemble d’algorithmes, une logique de traitement et une configuration nécessaires pour créer et exécuter un modèle formé et aider ainsi à résoudre des problèmes commerciaux spécifiques. |
| Modèle | Un modèle est l’instance d’une recette d’apprentissage automatique qui est formée à l’aide de données historiques et de configurations pour résoudre un cas d’utilisation commerciale. |
| Formation | La formation est le processus d’apprentissage des modèles et des connaissances à partir des données étiquetées. |
| Modèle formé | Un modèle formé représente la sortie exécutable d’un processus de formation de modèle, dans lequel un ensemble de données d’identification a été appliqué à l’instance de modèle. Un modèle formé conserve une référence à tout service Web intelligent créé à partir de ce service. Le modèle formé est adapté pour marquer et créer un service Web intelligent. Les modifications apportées à un modèle entraîné peuvent être suivies comme une nouvelle version. |
| Score | Le score est le processus de génération d’informations à partir de données à l’aide d’un modèle formé. |
| Service | Un service déployé expose la fonctionnalité d’une intelligence artificielle, d’un modèle d’apprentissage automatique ou d’un algorithme avancé au moyen d’une API afin qu’elle puisse être utilisée par d’autres services ou applications pour créer des applications intelligentes. |

Le graphique suivant décrit la relation hiérarchique entre les recettes, les modèles, les exécutions de formation et les exécutions de score.

![](./images/home/recipe_hiearchy_ui.png)

## Présentation de Data Science Workspace

Avec Data Science Workspace, vos chercheurs en données peuvent simplifier le processus encombrant de découverte d’informations dans des jeux de données volumineux. Basé sur un cadre d’apprentissage automatique et un environnement d’exécution courants, Data Science Workspace offre une gestion avancée des processus, une gestion des modèles et une évolutivité. Les services intelligents prennent en charge la réutilisation des recettes d’apprentissage automatique pour alimenter diverses applications créées à l’aide des produits et solutions Adobe.

### Accès unique aux données

Les données sont la pierre angulaire de l&#39;IA et de l&#39;apprentissage automatique.

Data Science Workspace est entièrement intégré à Adobe Experience Platform, notamment à Data Lake, au de clients en temps réel et à Unified Edge. Explorez toutes vos données d’entreprise stockées en même temps dans Adobe Experience Platform, ainsi que les Big Data courantes et les bibliothèques d’apprentissage en profondeur, telles que Spark ML et TensorFlow. Si vous ne trouvez pas ce dont vous avez besoin, ingérez vos propres jeux de données à l&#39;aide du  standard XDM.

### Recettes d&#39;apprentissage automatique prédéfinies

Data Science Workspace inclut des recettes d’apprentissage automatique préconçues pour répondre aux besoins courants de l’entreprise, comme la prédiction des ventes au détail et la détection des anomalies, de sorte que les chercheurs et les développeurs de données n’ont pas à  de toutes pièces. Actuellement, trois recettes sont proposées, la prédiction [des achats de](./pre-built-recipes/product-purchase-prediction.md)produits, les recommandations [de](./pre-built-recipes/product-recommendations.md)produits et les ventes [au](./pre-built-recipes/retail-sales.md)détail.

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Si vous préférez, vous pouvez adapter une recette préconçue à vos besoins, importer une recette ou  de toutes pièces pour créer une recette personnalisée. Cependant, dès que vous commencez à former et à optimiser une recette, la création d&#39;un service intelligent personnalisé ne nécessite pas de développeur - juste quelques clics et vous êtes prêt à construire une expérience numérique ciblée et personnalisée.

### Flux de travaux axé sur le chercheur en données

Quel que soit votre niveau d’expertise en sciences des données, Data Science Workspace permet de simplifier et d’accélérer le processus de recherche d’informations dans les données et de les appliquer aux expériences numériques.

### Exploration des données

Trouver les bonnes données et les préparer est la partie la plus exigeante en main d&#39;oeuvre de la construction d&#39;une recette efficace. Data Science Workspace et Adobe Experience Platform vous aident à obtenir plus rapidement des données vers des informations.

Sur Adobe Experience Platform, vos données  inter-sont centralisées et stockées dans le standard XDM. Les données sont donc plus faciles à trouver, à comprendre et à nettoyer. Un seul magasin de données basé sur un commun peut vous faire économiser d’innombrables heures d’exploration et de préparation de données.

Lorsque vous naviguez, utilisez R, Python ou Scala avec le Jupyter Notebook intégré et hébergé pour parcourir le catalogue de données sur la plate-forme. En utilisant l’une de ces langues, vous pouvez également tirer parti de Spark ML et de TensorFlow.  de toutes pièces ou utilisez l&#39;un des modèles d&#39;ordinateurs portables fournis pour des problèmes spécifiques de l&#39;entreprise.

Dans le cadre du processus d’exploration des données, vous pouvez également assimiler de nouvelles données ou utiliser les fonctionnalités existantes pour faciliter la préparation des données.

### Création  

Avec Data Science Workspace, vous décidez de la manière dont vous souhaitez créer des recettes.

- Gagnez du temps en recherchant une recette préconçue qui répond aux besoins de votre entreprise, que vous pouvez utiliser en l&#39;état ou configurer pour répondre à vos besoins spécifiques.
- Créez une recette à partir de zéro, en utilisant le runtime de création dans Jupyter Notebook pour développer et enregistrer la recette.
- Téléchargez une recette créée en dehors d’Adobe Experience Platform dans Data Science Workspace ou importez le code de recette depuis un référentiel, tel que Git, à l’aide de l’authentification et de l’intégration disponibles entre Git et Data Science Workspace.

### Expérience

Data Science Workspace offre une flexibilité exceptionnelle au processus d’expérimentation.  avec ta recette. Créez ensuite une instance distincte, en utilisant le même algorithme principal associé à des caractéristiques uniques, telles que des paramètres d’hyperréglage. Vous pouvez créer autant d’instances que vous le souhaitez, former et marquer chaque instance autant de fois que vous le souhaitez. Lorsque vous les formez, Data Science Workspace suit les recettes, les instances de recette et les instances de formation, ainsi que les mesures d’évaluation, afin que vous n’ayez pas à le faire.

### Opérationalisation

Quand vous êtes satisfait de votre recette, ce ne sont que quelques clics pour créer un service intelligent. Pas besoin de codage - vous pouvez le faire vous-même, sans avoir besoin d&#39;un développeur ou d&#39;un ingénieur. Enfin, publiez le service intelligent sur les E/S Adobe et il est prêt à être consommé par votre équipe d’expérience numérique.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Amélioration continue

L’espace de travail des sciences de données effectue le suivi de l’endroit où les services intelligents sont appelés et de leurs performances. Au fur et à mesure que les données s’enchaînent, vous pouvez évaluer la précision des services intelligents afin de fermer la boucle et de recycler les recettes en fonction des besoins pour améliorer les performances. Le résultat est un raffinement continu dans la précision de la personnalisation client.

### Accès aux nouvelles fonctionnalités et aux nouveaux jeux de données

Les chercheurs en données peuvent tirer parti des nouvelles technologies et des nouveaux jeux de données dès qu’ils sont disponibles via les services Adobe. Grâce à des mises à jour fréquentes, nous faisons le travail d&#39;intégration des jeux de données et des technologies dans la plate-forme, donc vous n&#39;avez pas à le faire.

###  dans Data Science Workspace

Access control for Experience Platform is administered through the [Adobe Admin Console](https://adminconsole.adobe.com). Cette fonctionnalité tire parti des  de produits dans la Console d’administration, qui relient les utilisateurs à des autorisations et des sandbox. See the [access control overview](../access-control/home.md) for more information.

>[!IMPORTANT] Pour utiliser Data Science Workspace, l’autorisation &quot;Gérer Data Science Workspace&quot; doit être activée.

Le tableau suivant décrit les effets de l’activation ou de la désactivation de cette autorisation :

| Autorisation | Activé | Désactivé |
|---|---|---|
| Gestion de l’espace de travail Data Science | Permet d’accéder à tous les services de Data Science Workspace. | L’accès à l’API et à l’interface utilisateur à tous les services de l’espace de travail Data Science est désactivé. Bien que désactivé, les  aux pages *Modèles* et *Services* de l’espace de travail Data Science ne sont pas. |

### Sécurité et tranquillité d&#39;esprit

La sécurisation de vos données est une priorité absolue pour Adobe. Adobe protège vos données à l’aide de processus et de contrôles de sécurité développés pour vous aider à vous conformer aux normes, réglementations et certifications reconnues par le secteur.

La sécurité est intégrée aux logiciels et services dans le cadre du cycle de vie des produits Adobe Secure.
Pour en savoir plus sur la sécurité des données et des logiciels Adobe, la conformité, etc., consultez la page de sécurité à l’adresse https://www.adobe.com/security.html.

### Prise en charge de sandbox

Les sandbox sont des partitions virtuelles au sein d’une seule instance de la plateforme d’expérience. Chaque instance de plateforme prend en charge un sandbox de production et plusieurs sandbox hors production, chacun conservant sa propre bibliothèque de ressources de plateforme. Les sandbox hors production vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter votre sandbox de production. Pour plus d’informations sur les sandbox, voir l’aperçu [des](../sandboxes/home.md)sandbox.

Actuellement, Data Science Workspace présente quelques limitations de sandbox :

- Les ressources de calcul sont partagées dans le sandbox de production et les sandbox hors production. L’isolation des sandbox de production doit être fournie à l’avenir.
- Les charges de travail Scala/Spark et PySpark pour les ordinateurs portables et les recettes ne sont actuellement prises en charge que dans le sandbox de production. La prise en charge des sandbox autres que la production est prévue pour l’avenir.

## Espace de travail des sciences de données en action

Les prédictions et les statistiques fournissent les informations dont vous avez besoin pour offrir une expérience hautement personnalisée à chaque client qui visite votre site Web, contacte votre centre d’appels ou participe à d’autres expériences numériques. Voici comment se passe votre travail quotidien avec Data Science Workspace.

### Définir le problème

Tout  avec un problème d&#39;entreprise. Par exemple, un centre d’appels en ligne a besoin de contexte pour les aider à rendre l’opinion négative des clients positive.

Il y a plein de données sur le client. Ils ont parcouru le site, mis des objets dans leur panier, et même passé des commandes. Ils ont peut-être reçu des courriers électroniques, utilisé des bons ou contacté le centre d’appels précédemment. La recette doit donc utiliser les données disponibles sur le client et son   pour déterminer la propension à acheter et recommander un  que le client est susceptible d&#39;apprécier et d&#39;utiliser.

![](./images/home/example_problem.png)

Au moment du contact du centre d’appels, le client a toujours deux paires de chaussures dans le panier, mais a retiré une chemise. Grâce à ces informations, le service intelligent peut recommander que l’agent du centre d’appels  un coupon pour 20 % de remise sur les chaussures pendant l’appel. Si le client utilise le bon, ces informations sont ajoutées au jeu de données et les prévisions s’améliorent encore la prochaine fois que le client appelle.

### Explorer et préparer les données

En fonction du problème d&#39;entreprise défini, vous savez que la recette doit examiner toutes les transactions Web du client, y compris les visites sur le site, les recherches, les  de page, les liens sur lesquels l&#39;utilisateur a cliqué, les actions de panier, les  de reçues, les courriers électroniques reçus, les interactions du centre d&#39;appels, etc.

En règle générale, un chercheur en données passe jusqu’à 75 % du temps nécessaire à la création d’une recette explorant et transformant les données. Les données proviennent souvent de plusieurs référentiels et sont enregistrées dans différents  de. Elles doivent être combinées et mappées avant de pouvoir être utilisées pour créer une recette.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Si vous commencez à zéro ou configurez une recette existante, vous commencez votre recherche de données dans un catalogue de données centralisé et standardisé pour votre entreprise, ce qui simplifie considérablement la recherche. Vous pouvez même constater qu’un autre chercheur de données de votre organisation a déjà identifié un jeu de données similaire et choisir d’affiner ce jeu de données plutôt que de le  de toutes pièces.
Toutes les données d’Adobe Experience Platform sont conformes à un  XDM standard, ce qui évite d’avoir à créer un modèle complexe de jonction de données ou d’obtenir de l’aide d’un ingénieur des données.

Si vous ne trouvez pas immédiatement les données dont vous avez besoin, mais qu’elles existent en dehors d’Adobe Experience Platform, il s’agit d’un relativement simple d’assimiler des jeux de données supplémentaires, qui se transformeront également en XDM standard.\
Vous pouvez utiliser Jupyter Notebook pour simplifier le prétraitement des données - en commençant par un modèle de portable ou un ordinateur portable que vous avez utilisé précédemment pour la propension à acheter.

<!-- databricks update-->
![](./images/home/notebook_templates.png)

### Créer la recette

Si vous avez déjà trouvé une recette qui répond à tous vos besoins, vous pouvez passer à l&#39;expérimentation. Vous pouvez également modifier un peu la recette ou en créer une à partir de zéro, en profitant du runtime de création de Data Science Workspace dans Jupyter Notebook. L’utilisation de l’environnement d’exécution de création vous permet d’utiliser à la fois la formation à l’espace de travail des sciences de données et le processus de notation et de convertir la recette ultérieurement afin qu’elle puisse être stockée et réutilisée par d’autres personnes de votre entreprise.

Vous pouvez également importer une recette dans Data Science Workspace et tirer parti du d’expérimentation lors de la création de votre service intelligent.

### Testez la recette

Avec une recette qui intègre vos algorithmes d’apprentissage automatique principaux, de nombreuses instances de recette peuvent être créées avec une seule recette. Ces instances de recette sont appelées modèles. Un modèle exige de la formation et de l&#39;évaluation pour optimiser son efficacité et son efficacité opérationnelle, un processus généralement constitué d&#39;essais et d&#39;erreurs.

![](./images/home/recipe_hiearchy_ui.png)

Lorsque vous formez vos modèles, des sessions de formation et des évaluations sont générées. L’espace de travail des sciences de données effectue le suivi des mesures d’évaluation pour chaque modèle unique et de leurs exécutions de formation. Les mesures d’évaluation générées par l’expérimentation vous permettent de déterminer la période de formation la plus performante.

![](./images/home/evaluation_metrics.png)

Consultez [cette section](https://www.adobe.io/apis/experienceplatform/home/tutorials/data-science-workspace/dsw-tutorials/trainmodel.html) pour obtenir des didacticiels sur la formation et l’évaluation des modèles dans Data Science Workspace.

### Opérationnaliser le modèle

Lorsque vous avez sélectionné la recette la mieux formée pour répondre aux besoins de votre entreprise, vous pouvez créer un service intelligent dans Data Science Workspace sans l’aide des développeurs. Ce ne sont que quelques clics - aucun code requis. Un service intelligent publié est accessible aux autres membres de votre organisation sans avoir à recréer le modèle.

Un service intelligent publié peut être configuré pour s’entraîner automatiquement de temps à autre à l’aide de nouvelles données dès qu’elles deviennent disponibles. Vous garantissez ainsi l’efficacité et l’efficience de votre service au fil du temps.

## Étapes suivantes

Data Science Workspace permet de rationaliser et de simplifier le flux de travaux des sciences de données, de la collecte de données aux algorithmes en passant par les services intelligents, pour les spécialistes des données de tous les niveaux de compétence. Grâce aux outils sophistiqués fournis par Data Science Workspace, vous pouvez réduire considérablement le temps passé des données aux informations.

Plus important encore, Data Science Workspace met les fonctionnalités de science des données et d’optimisation algorithmique de la principale plate-forme marketing d’Adobe entre les mains des spécialistes des données d’entreprise. Pour la première fois, les entreprises peuvent apporter des algorithmes propriétaires à la plate-forme, en tirant parti des puissantes capacités d’apprentissage automatique et d’IA d’Adobe pour offrir des expériences client hautement personnalisées à grande échelle.

Grâce à l’alliance de l’expertise de la marque et des prouesses d’Adobe en matière d’apprentissage automatique et d’IA, les entreprises ont le pouvoir d’accroître la valeur commerciale et la fidélité de la marque en donnant aux clients ce qu’ils veulent avant de le demander.

Pour plus d’informations, comme un flux de travail quotidien complet, lisez d’abord la documentation de présentation [de](./walkthrough.md) Data Science Workspace.

## Ressources supplémentaires   

La vidéo suivante est conçue pour vous aider à comprendre l’espace de travail des sciences de données.

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)

