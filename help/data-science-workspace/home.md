---
keywords: Experience Platform;home;Data Science Workspace;popular topics
solution: Experience Platform
title: Présentation de Data Science Workspace
topic: overview
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# Présentation de Data Science Workspace

Adobe Experience Platform Data Science Workspace utilise l’apprentissage automatique et l’intelligence artificielle pour libérer des informations de vos données. Intégrée à Adobe Experience Platform, Data Science Workspace vous permet de faire des prédictions à l’aide de vos contenus et de vos ressources de données dans les solutions Adobe.

Les chercheurs en données de tous les niveaux de compétence trouveront des outils sophistiqués et faciles à utiliser qui soutiennent le développement rapide, la formation et l&#39;ajustement des recettes d&#39;apprentissage automatique - tous les avantages de la technologie de l&#39;IA, sans la complexité.

Avec Data Science Workspace, les chercheurs en données peuvent facilement créer des API de services intelligents, optimisées par l&#39;apprentissage automatique. Ces services fonctionnent avec d’autres services Adobe, notamment Adobe Cible et Adobe Analytics Cloud, afin de vous aider à automatiser les expériences numériques ciblées et personnalisées dans les applications Web, de bureau et mobiles.

Ce guide présente un aperçu des concepts clés liés à Data Science Workspace.

## Introduction

L&#39;entreprise d&#39;aujourd&#39;hui accorde une grande priorité à l&#39;extraction de données massives pour les prédictions et les analyses qui les aideront à personnaliser les expériences client et à fournir plus de valeur aux clients - et à l&#39;entreprise.
Aussi important que cela soit, l&#39;obtention de données à des connaissances peut coûter cher. Il faut généralement des scientifiques spécialisés dans les données qui effectuent des recherches de données intensives et chronophages pour développer des modèles d&#39;apprentissage automatique, ou des recettes, qui génèrent des services intelligents. Le processus est long, la technologie est complexe et les scientifiques spécialisés en données peuvent être difficiles à trouver.

Avec Data Science Workspace, Adobe Experience Platform vous permet d’apporter une intelligence artificielle axée sur l’expérience à l’échelle de l’entreprise, en rationalisant et en accélérant les conversions de données vers des statistiques grâce à :
- Cadre d’apprentissage automatique et exécution
- Accès intégré à vos données stockées dans Adobe Experience Platform
- schéma de données unifié basé sur le modèle de données d’expérience (XDM)
- Puissance informatique essentielle à l&#39;apprentissage/à l&#39;IA des machines et à la gestion de jeux de données volumineux
- Recettes d&#39;apprentissage automatique préconçues pour accélérer le saut vers des expériences pilotées par l&#39;IA
- Création, réutilisation et modification simplifiées de recettes pour les spécialistes des données de différents niveaux de compétences
- Publication et partage de services intelligents en quelques clics - sans développeur - et surveillance et recyclage pour une optimisation continue des expériences client personnalisées

Les chercheurs en données de tous les niveaux de compétence parviendront plus rapidement à obtenir des informations plus rapides et plus efficaces sur les expériences numériques.

## Prise en main

Avant de vous plonger dans les détails de Data Science Workspace, voici un bref résumé des termes clés :

| Terme | Définition |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Espace de travail Data Science | Data Science Workspace dans Experience Platform permet aux clients de créer des modèles d’apprentissage automatique utilisant des données dans Experience Platform et les solutions Adobe afin de générer des aperçus et des prédictions intelligents pour tisser de merveilleuses expériences numériques d’utilisateur final. |
| Intelligence artificielle | L&#39;intelligence artificielle est une théorie et un développement de systèmes informatiques capables d&#39;exécuter des tâches qui nécessitent normalement l&#39;intelligence humaine, comme la perception visuelle, la reconnaissance vocale, la prise de décision et la traduction entre les langues. |
| Apprentissage automatique | L&#39;apprentissage automatique est le domaine d&#39;étude qui permet aux ordinateurs d&#39;apprendre sans être explicitement programmés. |
| Cadre de gestion de Sensei ML | Sensei ML Framework est une structure d’apprentissage automatique unifiée à l’échelle d’Adobe qui utilise les données de la plate-forme d’expérience pour permettre aux chercheurs de données de développer des services de renseignement pilotés par l’apprentissage automatique d’une manière plus rapide, évolutive et réutilisable. |
| Modèle de données d’expérience | Le modèle de données d’expérience (XDM) est l’effort de normalisation mené par Adobe pour définir des schémas standard tels que Profil et ExperienceEvent, pour la gestion de l’expérience client. |
| JupyterLab | JupyterLab est une interface web open-source pour Project Jupyter et est étroitement intégrée dans la plate-forme d’expérience. |
| Recettes | Une recette est le terme utilisé par Adobe pour désigner une spécification de modèle. Il s’agit d’un conteneur de niveau supérieur qui représente un apprentissage automatique, un algorithme d’IA ou un ensemble d’algorithmes, une logique de traitement et une configuration nécessaires à la création et à l’exécution d’un modèle formé et qui contribue ainsi à résoudre des problèmes commerciaux spécifiques. |
| Modèle | Un modèle est l&#39;instance d&#39;une recette d&#39;apprentissage automatique qui est formée à l&#39;aide de données historiques et de configurations pour résoudre un cas d&#39;utilisation commerciale. |
| Formation | La formation est le processus d’apprentissage des schémas et des connaissances à partir de données étiquetées. |
| Modèle formé | Un modèle formé représente la sortie exécutable d&#39;un processus de formation de modèle, dans lequel un ensemble de données de formation a été appliqué à l&#39;instance de modèle. Un modèle formé conserve une référence à tout service Web intelligent créé à partir de celui-ci. Le modèle formé est adapté pour le score et la création d&#39;un service web intelligent. Les modifications apportées à un modèle entraîné peuvent être suivies en tant que nouvelle version. |
| Scores | Le score est le processus de génération d’informations à partir de données à l’aide d’un modèle formé. |
| Service | Un service déployé expose les fonctionnalités d’une intelligence artificielle, d’un modèle d’apprentissage automatique ou d’un algorithme avancé par le biais d’une API afin de pouvoir être utilisé par d’autres services ou applications pour créer des applications intelligentes. |

Le graphique suivant décrit la relation hiérarchique entre les recettes, les modèles, les exécutions de formation et les exécutions de score.

![](./images/home/recipe_hiearchy_ui.png)

## Présentation de l&#39;espace de travail Data Science

Avec Data Science Workspace, vos chercheurs en données peuvent simplifier le processus encombrant de découverte d&#39;informations dans des jeux de données volumineux. Basé sur un cadre d’apprentissage automatique commun et un environnement d’exécution, Data Science Workspace offre une gestion avancée des processus, une gestion des modèles et une évolutivité. Les services intelligents prennent en charge la réutilisation des recettes d’apprentissage automatique pour alimenter diverses applications créées à l’aide des produits et solutions Adobe.

### Accès aux données à guichet unique

Les données sont la pierre angulaire de l&#39;IA et de l&#39;apprentissage automatique.

Data Science Workspace est entièrement intégré à Adobe Experience Platform, notamment à Data Lake, au Profil client en temps réel et à Unified Edge. Explorez simultanément toutes vos données d’entreprise stockées dans Adobe Experience Platform, ainsi que les données volumineuses et les bibliothèques d’apprentissage en profondeur courantes, telles que Spark ML et TensorFlow. Si vous ne trouvez pas ce dont vous avez besoin, ingérez vos propres jeux de données en utilisant le schéma standard XDM.

### Recettes d&#39;apprentissage automatique préétablies

Data Science Workspace inclut des recettes d&#39;apprentissage automatique préconçues pour les besoins courants de l&#39;entreprise, comme la prédiction des ventes au détail et la détection des anomalies, de sorte que les scientifiques et les développeurs de données n&#39;ont pas à début de rien. Actuellement, trois recettes sont proposées, la prédiction [des achats de](./pre-built-recipes/product-purchase-prediction.md)produits, les recommandations [de](./pre-built-recipes/product-recommendations.md)produits et les ventes [](./pre-built-recipes/retail-sales.md)au détail.

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Si vous préférez, vous pouvez adapter une recette préconçue à vos besoins, importer une recette ou un début de zéro pour créer une recette personnalisée. Cependant, dès que vous commencez à former et à ajuster une recette, la création d&#39;un service intelligent personnalisé n&#39;a pas besoin d&#39;un développeur - juste quelques clics et vous êtes prêt à construire une expérience numérique ciblée et personnalisée.

### Processus axé sur le chercheur en données

Quel que soit votre niveau d’expertise en sciences des données, Data Science Workspace permet de simplifier et d’accélérer le processus de recherche d’informations sur les données et de les appliquer aux expériences numériques.

### Exploration des données

Trouver les données appropriées et les préparer est la partie la plus exigeante en main-d&#39;oeuvre de la construction d&#39;une recette efficace. Data Science Workspace et Adobe Experience Platform vous aideront à obtenir plus rapidement des données vers des statistiques.

Sur Adobe Experience Platform, vos données entre canaux sont centralisées et stockées dans le schéma standard XDM. Les données sont donc plus faciles à trouver, à comprendre et à nettoyer. Un seul magasin de données basé sur un schéma commun peut vous faire économiser d&#39;innombrables heures d&#39;exploration et de préparation de données.

Lorsque vous naviguez, utilisez R, Python ou Scala avec le Jupyter Notebook intégré et hébergé pour parcourir le catalogue de données sur la plate-forme. En utilisant l&#39;une de ces langues, vous pouvez également profiter de Spark ML et TensorFlow. Début à partir de zéro, ou utilisez l&#39;un des modèles d&#39;ordinateurs portables fournis pour résoudre des problèmes commerciaux spécifiques.

Dans le cadre du processus d’exploration des données, vous pouvez également assimiler de nouvelles données ou utiliser les fonctionnalités existantes pour faciliter la préparation des données.

### Création  

Avec Data Science Workspace, vous décidez comment créer des recettes.

- Gagnez du temps en recherchant une recette préconçue qui répond aux besoins de votre entreprise, que vous pouvez utiliser en l&#39;état ou configurer pour répondre à vos besoins spécifiques.
- Créez une recette à partir de zéro, en utilisant le runtime de création dans Jupyter Notebook pour développer et enregistrer la recette.
- Téléchargez une recette créée en dehors d’Adobe Experience Platform dans Data Science Workspace ou importez le code de recette d’un référentiel, tel que Git, à l’aide de l’authentification et de l’intégration disponibles entre Git et Data Science Workspace.

### Expérimentation

Data Science Workspace apporte une flexibilité considérable au processus d’expérimentation. Début avec ta recette. Créez ensuite une instance distincte, en utilisant le même algorithme principal associé à des caractéristiques uniques, telles que des paramètres d’hyperréglage. Vous pouvez créer autant d’instances que vous le souhaitez, former et marquer chaque instance autant de fois que vous le souhaitez. Lorsque vous les formez, Data Science Workspace suit les recettes, les instances de recette et les instances de formation, ainsi que les mesures d’évaluation, ce qui vous évite d’avoir à le faire.

### Opérationalisation

Quand vous êtes satisfait de votre recette, ce ne sont que quelques clics pour créer un service intelligent. Aucun code requis - vous pouvez le faire vous-même, sans avoir à recruter un développeur ou un ingénieur. Enfin, publiez le service intelligent sur Adobe IO et il est prêt à être utilisé par votre équipe d’expérience numérique.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Amélioration continue

Data Science Workspace suit l’endroit où les services intelligents sont appelés et leurs performances. Au fur et à mesure que les données se déploient, vous pouvez évaluer la précision des services intelligents pour fermer la boucle et recycler les recettes en fonction des besoins afin d&#39;améliorer les performances. Le résultat est un raffinement continu de la précision de la personnalisation client.

### Accès aux nouvelles fonctionnalités et aux nouveaux jeux de données

Les chercheurs en données peuvent tirer parti des nouvelles technologies et des nouveaux jeux de données dès qu’ils sont disponibles via les services Adobe. Grâce à des mises à jour fréquentes, nous faisons le travail d&#39;intégration des jeux de données et des technologies dans la plate-forme, pour que vous n&#39;ayez pas à le faire.

### Contrôle d&#39;accès dans Data Science Workspace

Access control for Experience Platform is administered through the [Adobe Admin Console](https://auth.services.adobe.com/fr_FR/index.html?callback=https%3A%2F%2Fims-na1.adobelogin.com%2Fims%2Fadobeid%2FONESIE1%2FAdobeID%2Ftoken%3Fredirect_uri%3Dhttps%253A%252F%252Fadminconsole.adobe.com%252Fredirect.html%253Ftarget%253D%25252Foverview%2523from_ims%253Dtrue%2526old_hash%253D%2526api%253Dauthorize&amp;client_id=ONESIE1&amp;scope=openid%2CAdobeID%2Cadditional_info.projectedProductContext%2Cread_organizations%2Cread_members%2Cread_countries_regions%2Cadditional_info.roles%2Cadobeio_api%2Cread_auth_src_domains%2CauthSources.rwd&amp;denied_callback=https%3A%2F%2Fims-na1.adobelogin.com%2Fims%2Fdenied%2FONESIE1%3Fredirect_uri%3Dhttps%253A%252F%252Fadminconsole.adobe.com%252Fredirect.html%253Ftarget%253D%25252Foverview%2523from_ims%253Dtrue%2526old_hash%253D%2526api%253Dauthorize%26response_type%3Dtoken&amp;relay=6e938255-62f5-42c8-8176-178f6f1ab5bc&amp;locale=fr_FR&amp;flow_type=token&amp;ctx_id=admin_console_logo&amp;idp_flow_type=login#/). Cette fonctionnalité exploite les profils de produits de la Console d’administration, qui relient les utilisateurs avec des autorisations et des sandbox. See the [access control overview](../access-control/home.md) for more information.

>[!IMPORTANT] Pour utiliser Data Science Workspace, l’autorisation &quot;Gérer Data Science Workspace&quot; doit être activée.

Le tableau suivant décrit les effets de l’activation ou de la désactivation de cette autorisation :

| Autorisation | Activé | Désactivé |
|---|---|---|
| Gérer l’espace de travail Data Science | Permet d’accéder à tous les services de l’espace de travail Data Science. | L’accès à l’API et à l’interface utilisateur à tous les services de l’espace de travail Data Science est désactivé. Bien que désactivé, le routage aux *modèles* d’espace de travail Data Science Workspace et aux pages *Services* est évité. |

### Sécurité et tranquillité d&#39;esprit

La sécurisation de vos données est une priorité pour Adobe. Adobe protège vos données à l’aide de processus et de contrôles de sécurité élaborés pour vous aider à vous conformer aux normes, réglementations et certifications reconnues par le secteur.

La sécurité est intégrée aux logiciels et services dans le cadre du cycle de vie des produits Adobe Secure.
Pour en savoir plus sur la sécurité des données et des logiciels Adobe, la conformité, etc., consultez la page Sécurité à l’adresse https://www.adobe.com/security.html.

### Prise en charge de sandbox

Les sandbox sont des partitions virtuelles au sein d’une seule instance de la plateforme d’expérience. Chaque instance de plate-forme prend en charge un sandbox de production et plusieurs sandbox hors production, chacun conservant sa propre bibliothèque de ressources de plate-forme. Les sandbox hors production vous permettent de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter votre sandbox de production. Pour plus d’informations sur les sandbox, voir l’aperçu [des](../sandboxes/home.md)sandbox.

Actuellement, Data Science Workspace présente quelques limitations de sandbox :

- Les ressources de calcul sont partagées dans le sandbox de production et les sandbox hors production. L&#39;isolation des sandbox de production est prévue pour l&#39;avenir.
- Actuellement, les charges de travail Scala/Spark et PySpark pour les cahiers de travail et les recettes ne sont prises en charge que dans le sandbox de production. La prise en charge des sandbox hors production est prévue pour l’avenir.

## Espace de travail des sciences de données en action

Les prédictions et les statistiques fournissent les informations dont vous avez besoin pour offrir une expérience hautement personnalisée à chaque client qui visite votre site Web, contacte votre centre d’appels ou participe à d’autres expériences numériques. Voici comment votre travail quotidien se déroule avec Data Science Workspace.

### Définir le problème

Tous les débuts ont un problème commercial. Par exemple, un centre d’appels en ligne a besoin de contexte pour les aider à exprimer une opinion négative des clients.

Il y a beaucoup de données sur le client. Ils ont parcouru le site, mis des articles dans leur panier, et même passé des commandes. Ils ont peut-être reçu des courriels, utilisé des bons ou contacté le centre d’appels précédemment. La recette doit donc utiliser les données disponibles sur le client et ses activités pour déterminer la propension à acheter et recommander une offre que le client est susceptible d&#39;apprécier et d&#39;utiliser.

![](./images/home/example_problem.png)

Au moment du contact du centre d&#39;appel, le client a toujours deux paires de chaussures dans le panier, mais a retiré une chemise. Grâce à ces informations, le service intelligent peut recommander que l&#39;agent du centre d&#39;appels offre un coupon de 20 % sur les chaussures pendant l&#39;appel. Si le client utilise le bon, ces informations sont ajoutées au jeu de données et les prévisions s’améliorent encore la prochaine fois que le client appelle.

### Explorer et préparer les données

En fonction du problème d&#39;entreprise défini, vous savez que la recette doit examiner toutes les transactions Web du client, y compris les visites sur le site, les recherches, les vues de page, les liens sur lesquels l&#39;utilisateur a cliqué, les actions de panier, les offres reçues, les courriels reçus, les interactions du centre d&#39;appels, etc.

En règle générale, un chercheur en données consacre jusqu&#39;à 75 % du temps nécessaire à la création d&#39;une recette qui explore et transforme les données. Les données proviennent souvent de plusieurs référentiels et sont enregistrées dans différents schémas. Elles doivent être combinées et mises en correspondance avant de pouvoir être utilisées pour créer une recette.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Si vous commencez à zéro ou configurez une recette existante, vous commencez votre recherche de données dans un catalogue de données centralisé et standardisé pour votre entreprise, ce qui simplifie considérablement la recherche. Il se peut même qu’un autre chercheur de données de votre organisation ait déjà identifié un jeu de données similaire et ait choisi de le raffiner plutôt que de le début de zéro.
Toutes les données d’Adobe Experience Platform sont conformes à un schéma XDM standard, ce qui évite d’avoir à créer un modèle complexe pour l’association de données ou d’obtenir de l’aide d’un ingénieur des données.

Si vous ne trouvez pas immédiatement les données dont vous avez besoin, mais qu’elles existent en dehors d’Adobe Experience Platform, il s’agit d’une tâche relativement simple d’assimiler des jeux de données supplémentaires, qui se transformeront également en schéma XDM standard.\
Vous pouvez utiliser Jupyter Notebook pour simplifier le prétraitement des données - en commençant par un modèle de bloc-notes ou un bloc-notes que vous avez utilisé précédemment pour la propension à acheter.

![](./images/home/notebook_templates.png)

### Créer la recette

Si vous avez déjà trouvé une recette qui répond à tous vos besoins, vous pouvez passer à l&#39;expérimentation. Vous pouvez également modifier un peu la recette ou en créer une à partir de zéro, en profitant de l&#39;environnement d&#39;exécution de création Data Science Workspace dans Jupyter Notebook. L’utilisation de l’exécution de création vous permet d’utiliser à la fois la formation sur l’espace de travail des sciences de données et le processus de notation et de convertir ultérieurement la recette afin qu’elle puisse être stockée et réutilisée par d’autres personnes de votre organisation.

Vous pouvez également importer une recette dans Data Science Workspace et tirer parti des workflows d’expérimentation lors de la création de votre service intelligent.

### Testez la recette

Avec une recette qui intègre vos algorithmes d&#39;apprentissage automatique de base, de nombreuses instances de recette peuvent être créées avec une seule recette. Ces instances de recette sont appelées modèles. Un modèle nécessite de la formation et de l&#39;évaluation pour optimiser son efficacité et son efficacité opérationnelles, un processus généralement constitué d&#39;essais et d&#39;erreurs.

![](./images/home/recipe_hiearchy_ui.png)

Lorsque vous formez vos modèles, des sessions de formation et des évaluations sont générées. Data Science Workspace conserve le suivi des mesures d’évaluation pour chaque modèle unique et leurs exécutions de formation. Les mesures d’évaluation générées par l’expérimentation vous permettent de déterminer la période de formation la plus performante.

![](./images/home/evaluation_metrics.png)

Consultez [cette section](https://www.adobe.io/apis/experienceplatform/home/tutorials/data-science-workspace/dsw-tutorials/trainmodel.html) pour obtenir des didacticiels sur la formation et l’évaluation des modèles dans Data Science Workspace.

### Opérationnaliser le modèle

Lorsque vous avez sélectionné la recette la mieux formée pour répondre aux besoins de votre entreprise, vous pouvez créer un service intelligent dans Data Science Workspace sans l’aide des développeurs. Il ne s&#39;agit que de quelques clics - aucun codage n&#39;est requis. Un service intelligent publié est accessible aux autres membres de votre organisation sans avoir à recréer le modèle.

Un service intelligent publié est configurable pour s&#39;entraîner automatiquement de temps en temps à l&#39;utilisation de nouvelles données au fur et à mesure de leur disponibilité. Ainsi, votre service conserve son efficacité et son efficience au fil du temps.

## Étapes suivantes

Data Science Workspace permet de rationaliser et de simplifier le flux de données scientifiques, de la collecte de données aux algorithmes en passant par les services intelligents, pour les chercheurs en données de tous les niveaux de compétence. Grâce aux outils sophistiqués fournis par Data Science Workspace, vous pouvez réduire considérablement le temps passé des données aux informations.

Plus important encore, Data Science Workspace met les capacités de science des données et d’optimisation algorithmique de la principale plate-forme marketing d’Adobe entre les mains des spécialistes des données d’entreprise. Pour la première fois, les entreprises peuvent apporter des algorithmes propriétaires à la plate-forme, en tirant parti des puissantes capacités d’apprentissage automatique et d’IA d’Adobe pour offrir des expériences client hautement personnalisées à grande échelle.

Grâce à l’alliance de l’expertise de la marque et des prouesses d’Adobe en matière d’apprentissage automatique et d’IA, les entreprises ont le pouvoir d’augmenter la valeur commerciale et la fidélité de la marque en donnant aux clients ce qu’ils veulent avant de le demander.

Pour plus d’informations, par exemple un flux de travail complet au quotidien, lisez la documentation de présentation [de](./walkthrough.md) Data Science Workspace.

## Ressources supplémentaires

La vidéo suivante est conçue pour vous aider à mieux comprendre Data Science Workspace.

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)

