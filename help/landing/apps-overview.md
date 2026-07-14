---
title: Fonctionnement  [!DNL Adobe Experience Platform]  applications
description: Découvrez  [!DNL Adobe Experience Platform]  et ses applications, le fonctionnement de chacune d’elles, les objectifs qu’elles prennent en charge et la manière dont elles partagent les données, les profils et la gouvernance.
solution: Experience Platform
feature: Getting Started
topic: Overview
role: User, Developer, Leader
source-git-commit: 8d7b4a77161914147004f559913ee9b2ccf888c0
workflow-type: tm+mt
source-wordcount: '5312'
ht-degree: 2%

---


# Fonctionnement des [!DNL Adobe Experience Platform] et des applications

[!DNL Adobe Experience Platform] est la base des données partagées et de la prise de décision qui alimente [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer], [!DNL Customer Journey Analytics] et [!DNL Adobe Marketing Campaign Analytics] (anciennement appelé [!DNL Adobe Mix Modeler]). Lorsque ces applications partagent un profil, un ensemble de règles de données et un modèle d’événement, vos équipes arrêtent de reconstruire les mêmes pipelines de données et commencent à atteindre les clients plus rapidement, avec une gouvernance intégrée. Cette page explique comment chaque partie s’intègre.

>[!NOTE]
>
>Cette rubrique présente un aperçu. Pour connaître les étapes pratiques, les actions de l’interface utilisateur et les détails de l’API, voir [Ressources supplémentaires](#additional-resources).

## Qui doit lire cette rubrique ? {#who-should-read}

Utilisez ce tableau pour voir si cette rubrique correspond à votre rôle.

| Votre rôle | questions Principal | Aide de cette rubrique |
| --- | --- | --- |
| Chefs d’entreprise et marketing | Quelle valeur puis-je tirer des [!DNL Experience Platform] et des applications ensemble ? | Connectez les objectifs des clients et de la marque aux fonctionnalités et applications [!DNL Experience Platform]. Utilisez les mêmes mots que vos équipes techniques. |
| Personnes impliquées dans les opérations marketing, les analyses ou l’expérience client | Comment exécutez-vous des campagnes et des parcours, et comment les données s’alignent-elles ? | Voyez où les données se rassemblent, où les choix sont faits et quelle application correspond à quelle étape. |
| Architectes, ingénieurs et développeurs | Comment faire pour que les applications fonctionnent de manière fiable à grande échelle ? | Utilisez le même modèle et les mêmes termes simples que dans le reste du [!DNL Experience League] lorsque vous concevez ou créez. |
| Analystes et spécialistes des données | Comment répondre aux questions et trouver des opportunités d’activation ? | Découvrez comment l’analyse des données [!DNL Experience Platform] se connecte aux audiences et aux parcours. |

Partagez cette rubrique avec les professionnels du marketing, les propriétaires de produits et les personnes qui créent ou exécutent la solution. Après l’avoir lu, utilisez les guides détaillés dans [!DNL Experience League] pour les tâches de produit ou les détails techniques.

>[!IMPORTANT]
>
>Les applications que vous pouvez utiliser dépendent de votre licence Adobe. Vérifiez votre contrat et la dernière documentation du produit Experience League.

## Ce que vous comprendrez après lecture {#learning-outcomes}

Après avoir lu cette rubrique, vous devriez être en mesure d’effectuer les opérations suivantes.

1. Décrire [!DNL Adobe Experience Platform] : expliquez ce que fait [!DNL Experience Platform] en tant que base partagée pour les données et les règles de données. Vous pouvez expliquer cela sans nommer d’application spécifique.
2. Décrivez chaque application principale : expliquez quel est l’objectif commercial pris en charge par chaque application et à quel type de travail elle correspond.
3. Décrivez comment les [!DNL Experience Platform] et les applications s’intègrent : expliquez comment les profils client, les identités, les formes de données (schémas) et les règles de données passent de la [!DNL Experience Platform] aux applications. Expliquez pourquoi les équipes n’ont pas besoin de créer des pipelines de données distincts et en conflit pour chaque outil.
4. Connectez un objectif à la partie droite de la solution : pour un exemple d’objectif (par exemple, « Intégration via les e-mails et les appareils mobiles »), nommez les parties de [!DNL Experience Platform] et les applications qui prennent généralement en charge cet objectif.

Dans cette rubrique, « vos objectifs » signifie ce que votre entreprise souhaite (par exemple, la croissance, l’efficacité ou la confiance des clients). « Vos clients » désigne les personnes qui interagissent avec votre marque. Des [!DNL Experience Platform] et des applications existent pour aider vos équipes à servir ces clients.

## [!DNL Adobe CX Enterprise] {#cx-enterprise}

[!DNL Adobe CX Enterprise] est l’interface unifiée et la couche de services partagés pour le portfolio d’expérience client d’Adobe. Il s’agit du point d’entrée de niveau supérieur de la pile d’expérience client : à partir des applications [!DNL Adobe CX Enterprise], [!DNL Adobe Experience Platform] ouvertes et [!DNL Experience Platform] (telles que [!DNL Real-Time CDP], [!DNL Journey Optimizer] et [!DNL Customer Journey Analytics]) avec :

- En-tête et navigation partagés
- Sélecteur d’applications à déplacer entre les produits
- Services centraux tels que [!DNL Audience Library], [!DNL Customer Attributes], ressources partagées, triggers et Marketplace

Sous [!DNL CX Enterprise] se trouve [!DNL Adobe Experience Platform] que la base de données et de prise de décision (schémas, identité, [!DNL Real-Time Customer Profile], segmentation, gouvernance, lac de données, [!DNL Edge] et services associés). Les applications sous licence telles que [!DNL Real-Time CDP], [!DNL Journey Optimizer], [!DNL Customer Journey Analytics] et [!DNL Adobe Marketing Campaign Analytics] reposent sur cette base. Les sections qui suivent effectuent un zoom avant sur la base et sur chaque application.

## Que sont [!DNL Adobe Experience Platform] et ses applications ? {#platform}

[!DNL Adobe Experience Platform] constitue la base de données et de prise de décision en temps réel pour les applications d’expérience telles que [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer], [!DNL Customer Journey Analytics] et [!DNL Adobe Marketing Campaign Analytics]. Ces applications sont créées sur [!DNL Experience Platform] et partagent les mêmes services pour les données, l’identité, les profils, les audiences et la gouvernance afin que vos équipes puissent passer d’insight à l’activation dans un système connecté au lieu d’assembler des outils distincts. Utilisez [!DNL Experience Platform] pour normaliser et unifier les données une seule fois, puis utilisez des applications pour analyser, orchestrer et activer des expériences sur plusieurs canaux à grande échelle.

Dans les workflows classiques, les équipes accèdent à [!DNL Experience Platform] et à ces applications via [Adobe CX Enterprise](#cx-enterprise), comme décrit ci-dessus.

## Où commencer avec la pile complète {#where-to-start}

Utilisez les éléments suivants comme ordre de niveau supérieur pour utiliser la pile complète. Votre entreprise peut adapter les phases à vos workflows.

| Phase | Que faire |
| --- | --- |
| Établir les bases d’Experience Platform | Définissez des cas d’utilisation et des sources prioritaires. Concevez des schémas XDM, des règles d’identité, des sandbox, ainsi que la gouvernance et le consentement de base. |
| Stand up Real-Time CDP | Configurez les audiences qui correspondent à vos cas d’utilisation. Connectez les destinations pour les canaux qui comptent en premier. |
| Ajout de parcours Adobe Journey Optimizer | Commencez par un ou deux parcours à fort impact. Utilisez les segments Real-Time CDP et les événements Experience Platform comme déclencheurs et conditions. |
| Ajout de Customer Journey Analytics pour l’apprentissage en boucle fermée | Connectez des jeux de données Experience Platform. Utilisez des visualisations par parcours pour rechercher des opportunités, puis republiez les audiences dans Experience Platform pour Real-Time CDP et Adobe Journey Optimizer. |
| Itération et mise à l’échelle | Développez les parcours, les canaux, les segments et les scores modélisés à mesure que votre programme se développe. |

## Les différences entre les fonctionnalités, les services et les applications d’Experience Platform {#feature-service-application}

[!DNL Adobe Experience Platform] comprend des fonctionnalités et des services. Il prend également en charge les applications sous licence qui conditionnent des workflows pour des tâches spécifiques.

| Terme | Signification de ce terme dans cette documentation | Exemples courants |
| --- | --- | --- |
| Fonctionnalité de Platform | Fonctionnalité disponible dans [!DNL Experience Platform] que les équipes utilisent directement à des fins spécifiques (souvent pour l’analyse, le test ou le contrôle). Il ne s’agit pas d’une application sous licence distincte. | Sandbox et fonctionnalités de gouvernance et de confidentialité des données |
| Service Platform | Service en arrière-plan qui fournit un comportement partagé sur lequel plusieurs produits reposent via [!DNL Experience Platform]. Les services sont fondamentaux et ne sont pas commercialisés en tant qu’applications autonomes quotidiennes. | [!DNL Identity Service], [!DNL Real-Time Customer Profile], [!DNL Query Service], segmentation, destinations, ingestion de données |
| Application Platform | Produit sous licence reposant sur [!DNL Adobe Experience Platform], qui ajoute sa propre expérience utilisateur, ses propres workflows et des fonctionnalités spécifiques au produit à la base partagée. | [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer], [!DNL Customer Journey Analytics], [!DNL Adobe Marketing Campaign Analytics] |

## But de chaque demande {#applications-at-a-glance}

Dans cette documentation, une application est un produit Adobe sous licence qui s’exécute sur [!DNL Adobe Experience Platform]. Les applications utilisent le même profil client, la même structure de données, les mêmes liens d’identité et les mêmes règles de données que les [!DNL Experience Platform]. Chaque application ajoute ses propres écrans et workflows pour un type de travail (par exemple, envoyer des audiences aux canaux, exécuter des parcours ou créer des rapports).

Le tableau ci-dessous répertorie chaque application. Il fournit une brève description et l’objectif principal. Elle ne répertorie pas toutes les modifications d’application. Ce à quoi vous pouvez accéder dépend de votre licence .

| Application | Signification | Objectif principal |
| --- | --- | --- |
| [Real-Time Customer Data Platform (Real-Time CDP)](https://experienceleague.adobe.com/fr/docs/experience-platform/rtcdp/home) | Application pour les données et audiences client | Rassemblez vos propres données client. Créez des audiences qui se mettent à jour fréquemment. Envoyez des audiences et des attributs aux publicités, aux e-mails, aux applications mobiles et à d’autres outils. Les règles de données sont appliquées. La même famille de produits prend en charge les entreprises grand public, les clients professionnels et les modèles mixtes. Voir l’aide de l’application pour connaître les éditions disponibles. |
| [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer) | Application pour parcours et messages | Planifiez et exécutez des parcours personnalisés (par exemple, chemins de bienvenue, conservation ou suivi après le service). Envoyez des messages sur plusieurs canaux à l’aide d’événements en direct et de données de profil. |
| [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/customer-journey-analytics) | Application pour l’analyse sur plusieurs canaux | Mesurez et analysez la façon dont les clients et clientes se déplacent sur les parcours à travers plusieurs canaux (y compris le web, les appareils mobiles, les centres d’appels et les systèmes de point de vente), et comment les performances marketing sont évaluées. Utilise les données préparées en [!DNL Adobe Experience Platform]. |
| [Adobe Marketing Campaign Analytics (anciennement Adobe Mix Modeler)](https://experienceleague.adobe.com/fr/docs/mix-modeler) | Application pour la mesure et la planification du marketing | Rassemblez les mesures (y compris la modélisation du marketing mix). Planifiez des scénarios de dépenses pour le marketing. Utilise les données connectées par le biais de [!DNL Adobe Experience Platform] afin que les équipes puissent voir ce qui génère des résultats et planifier les budgets. |

## Autres applications et éditions sur [!DNL Experience Platform] {#other-applications-and-editions}

Le tableau ci-dessus décrit quatre applications qui fonctionnent ensemble dans de nombreuses implémentations de [!DNL Experience Platform]. Votre entreprise peut également utiliser des offres sous licence associées qui reposent sur la même base (schémas, [!DNL Identity Service], [!DNL Real-Time Customer Profile], segmentation et gouvernance). Le tableau ci-dessous en fournit des exemples. Elle ne remplace pas la documentation spécifique au produit. Les éléments auxquels vous pouvez accéder dépendent de votre licence, de votre région et du portfolio Adobe.

| Rubrique | Rôle |
| --- | --- |
| [Real-Time CDP B2B edition](../rtcdp/b2b-overview.md) | Activation centrée sur le compte et le lead sur la même base [!DNL Experience Platform] que les solutions orientées vers les consommateurs ou les modèles B2B et B2C mixtes. |
| [Journey Orchestration](https://experienceleague.adobe.com/fr/docs/journeys/using/journey-orchestration-home) | Orchestration reposant sur [!DNL Experience Platform]. Vérifiez auprès de votre équipe Adobe quel produit de parcours votre organisation a acheté et mis en œuvre. |
| [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/home) | Cas d’utilisation de collaboration de partenaires (par exemple, chevauchement d’audiences avec des éditeurs ou des partenaires) dans la famille de [!DNL Real-Time CDP]. Les audiences peuvent apparaître dans [!DNL Audience Portal] avec les audiences de [!DNL Experience Platform]. |

>[!NOTE]
>
>D’autres produits Adobe CX Enterprise peuvent se connecter à Adobe Experience Platform sans être répertoriés ici ou au-dessus. Pour obtenir un mappage de haut niveau des modèles d’intégration courants (sources et destinations, par exemple Adobe Analytics en tant que source ou Adobe Target en tant que destination), consultez [Intégrations Adobe Experience Platform](integrations.md).

Les noms de produits, les éditions et les produits vendus peuvent différer selon la licence, le pays ou la région.

## Mappez vos objectifs aux [!DNL Experience Platform] et aux applications. {#goals-map}

Utilisez ce tableau pour voir ce que vous souhaitez, ce que [!DNL Experience Platform] fournit et les applications utiles.

| Votre objectif | Éléments à utiliser à partir de [!DNL Experience Platform] | Éléments à utiliser dans les applications |
| --- | --- | --- |
| Afficher une personne ou un compte sur plusieurs canaux | [!DNL Identity Service], [!DNL Real-Time Customer Profile], XDM | Toutes les applications répertoriées en bénéficient. [!DNL Real-Time CDP] et [!DNL Adobe Journey Optimizer] utilisez Profile pour envoyer des audiences et des parcours. |
| Exécuter des campagnes et des listes avec des adhésions à jour | Profil, segmentation, destinations, règles de données | [!DNL Real-Time CDP] de la manière dont les audiences sont envoyées. Les destinations transportent un contexte de politique. |
| Exécuter des expériences en plusieurs étapes qui réagissent au comportement | Profil, événements en direct, règles de données | [!DNL Adobe Journey Optimizer] pour la logique de parcours et les messages. |
| Rapport sur les parcours et les canaux avec des nombres correspondants | Événements et identités XDM partagés | [!DNL Customer Journey Analytics] pour l’analyse des mêmes données. |
| Transformer l’analyse en audiences pour activation | Audiences publiées de [!DNL Customer Journey Analytics] à [!DNL Adobe Experience Platform] | [!DNL Real-Time CDP] et [!DNL Adobe Journey Optimizer] utilisent ces audiences à partir de [!DNL Experience Platform]. |
| Découvrez comment les canaux contribuent et planifient les budgets marketing | Jeux de données unifiés, règles de données, données prêtes pour les modèles | [!DNL Adobe Marketing Campaign Analytics] pour la modélisation mix et la planification des dépenses. |
| Veiller à ce que le marketing et le service correspondent aux faits concernant les clients | Profil, règles de données, connexions facultatives à d’autres systèmes | La façon de connecter d’autres systèmes peut varier. [!DNL Experience Platform] reste la base des données client. |

## Comment [!DNL Adobe Experience Platform] apporte de la valeur {#platform-alone}

Les sous-sections qui suivent montrent comment Platform Foundation se transforme en valeur pour vos équipes.

- Les mêmes données et règles
- Chemins d’accès plus rapides aux audiences, aux analyses et aux activations
- Utilisation régie entre les outils

[!DNL Adobe Experience Platform] est la couche de base des données d’expérience client. Il ne s’agit pas d’un seul écran marketing. Il repose sur des services qui s’exécutent en arrière-plan. Vous configurez les données, l’identité et les règles une seule fois. Les applications sous licence réutilisent cette base, ce qui accélère le temps nécessaire aux audiences, aux analyses et aux activations que les équipes peuvent exécuter en toute confiance.

Avant d’ouvrir une application, [!DNL Experience Platform] pouvez effectuer les opérations suivantes.

| Que fait [!DNL Experience Platform] | Pourquoi cela vous aide |
| --- | --- |
| Importe des données à partir de sites web, d’applications ou de vos propres systèmes d’entreprise, par le biais d’API de streaming ou d’exportations par lots | Vous n’êtes pas bloqué avec un canal ou une base de données. Vous pouvez créer une vue plus complète au fil du temps. |
| Structure les données avec des schémas basés sur le [!DNL Experience Data Model] (XDM) afin que les événements et les champs partagent la même signification. | Le partage des définitions entre les équipes d’analystes, de marketing et de conformité réduit les erreurs et la duplication du travail. |
| Associe les identités de sorte que, dans vos règles, la même personne ou le même compte puisse être reconnu sur tous les appareils et systèmes | Les équipes peuvent travailler à partir d’une seule vue du client, lorsque la politique le permet. |
| Permet de [!DNL Real-Time Customer Profile] tenir à jour en tant que vue active pour les décisions et l&#39;exportation de données | Les décisions et les activations utilisent toujours de nouvelles données. |
| Crée des audiences (segmentation) à partir des données de profil, du comportement et du consentement | Vous définissez qui est inclus à un emplacement. D’autres étapes réutilisent cette logique. |
| Envoie les données vers les destinations (exportations et systèmes connectés) et applique les règles de données par le biais de libellés, de politiques et de [!DNL Privacy Service] | Les règles de gouvernance s’appliquent automatiquement à l’activation. Les équipes n’ont donc pas besoin d’un examen de conformité distinct avant chaque exportation de données. |

En résumé, [!DNL Experience Platform] regroupe les données clients, applique des règles et prépare les données à utiliser. La valeur de ce travail apparaît donc dans les applications (audiences, parcours, analyses) au lieu de rester piégée dans des projets de données ponctuels. Il ne remplace pas les écrans complets fournis par les applications pour la conception de parcours, les workflows multimédia ou les rapports cross-canal. Les applications fournissent ces expériences.

### [!DNL Experience Platform] des services en un coup d’œil {#core-platform-services}

Ce tableau répertorie les services principaux et résume les tâches de chacun d’eux.

| Zone | Rôle sur [!DNL Experience Platform] |
| --- | --- |
| Collecte de données ([!DNL Tags], [!DNL Experience Platform Web SDK], [!DNL Experience Platform Mobile SDK], flux de données) | Collectez des données à partir d’expériences digitales de manière standard. |
| Sources et importation de données | Connectez les données des systèmes de l’entreprise et des sources cloud aux [!DNL Experience Platform]. |
| XDM et schémas | Définissez la structure et la signification des données d’expérience. |
| [!DNL Identity Service] | Connecter les identifiants dans une vue au sein de la politique. |
| [!DNL Real-Time Customer Profile] | Conservez le profil actif utilisé pour les décisions et l’envoi de données. |
| Segmentation | Définissez des audiences à partir des données de profil et des événements. |
| Destinations | Envoyez des audiences et des attributs à d’autres systèmes qui exécutent le marketing ou le service. |
| Gouvernance des données, [!DNL Privacy Service], consentement | Contrôlez la manière dont les données peuvent être utilisées. |
| Sandbox | Créez des environnements isolés pour développer et tester des schémas, des flux de données, des règles d’identité et la segmentation avant de promouvoir le travail en production. |
| [!DNL Query Service] | Exécutez SQL sur les données [!DNL Experience Platform] pour l’analyse et la création de rapports. |

Ces zones prennent en charge un modèle de bout en bout :

1. Collectez des données à partir des canaux et des systèmes.
2. Rassemblez les événements et les attributs sous des schémas et des identités partagés.
3. Appliquez la gouvernance, le consentement et la segmentation pour qualifier les personnes et les actions appropriées.
4. Activez les audiences et les attributs vers les destinations sélectionnées.
5. Mesurez les résultats, les statistiques et les performances.

Ce flux permet aux données brutes sur les [!DNL Experience Platform] de devenir des insight et des activations de clients que vous pouvez utiliser dans vos applications, avec une pile régie au lieu d’un chemin de données distinct pour chaque canal ou équipe. Les règles de données s’appliquent à chaque étape.

>[!NOTE]
>
>Lorsque vous configurez des schémas, des identités, la gouvernance et l’ingestion de données sur [!DNL Experience Platform], ce travail est disponible pour les applications incluses dans votre licence. Comme vous ne répétez pas la même configuration de base dans chaque application, les équipes peuvent utiliser ces applications plus tôt et avec moins de définitions incohérentes.

## Valeur ajoutée des applications {#applications-alone}

Le tableau ci-dessous ajoute des détails. Il indique la fonction de chaque application et l’objectif qu’elle prend en charge.

- Chaque application est un workflow complet pour un type de travail (par exemple, activation, parcours, analyse cross-canal ou mesure marketing) sur la même [!DNL Real-Time Customer Profile] et les règles de données sur les [!DNL Experience Platform].
- Les applications sont les expériences utilisateur et les écrans de cette base. Chacun aide vos équipes à effectuer un type de travail principal. Tous s’appuient sur le même profil et les mêmes règles de données, de sorte que vous ne copiez pas la pile de données complète pour chaque produit.

| Application | Fonctionnement (tâche principale) | Quel objectif cela vous aide à atteindre ? |
| --- | --- | --- |
| [Real-Time Customer Data Platform (Real-Time CDP)](https://experienceleague.adobe.com/fr/docs/experience-platform/rtcdp/home) | Gérer les audiences et l’activation : créez des audiences, mettez souvent à jour l’appartenance, envoyez des audiences et des attributs aux destinations. Prend en charge les cas d’utilisation particuliers, professionnels et variés en fonction de votre licence. | Touchez les bonnes personnes et excluez les mauvaises sur les canaux payants, propriétaires et partenaires à l’aide de vos propres données client unifiées. |
| [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer) | Concevoir des parcours et envoyer des messages : réagissez aux événements, aux chemins de branche et envoyez sur plusieurs canaux à partir d’un espace de travail de parcours. | Exécutez des séquences personnalisées (par exemple, intégration, rétention ou suivi du service) qui répondent à ce que le client vient de faire. |
| [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/customer-journey-analytics) | Générez des rapports et analysez les parcours et les résultats de campagne à l’aide d’une seule base de données. | Découvrez ce qui s’est passé et pourquoi sur plusieurs canaux afin d’améliorer les dépenses et l’expérience. |
| [&#128279;](https://experienceleague.adobe.com/fr/docs/mix-modeler) | Combinez les données connectées à [!DNL Experience Platform] avec des modèles pour mesurer les canaux et exécuter des scénarios de planification. | Planifiez et ajustez les dépenses marketing avec une vue régulière de la manière dont les canaux et d’autres facteurs affectent les résultats. |

### Quand utiliser chaque application {#when-to-use-each-app}

Utilisez le tableau suivant pour trouver l’application adaptée à votre principal objectif commercial.

| Application | Utilisez-le lorsque votre objectif principal est de |
| --- | --- |
| [Real-Time CDP](https://experienceleague.adobe.com/fr/docs/experience-platform/rtcdp/home) | Définissez des audiences une fois à partir de données unifiées et activez-les de manière cohérente sur l’ensemble des canaux et outils (y compris les destinations en dehors d’Adobe). |
| [Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer) | Écoutez le comportement et orchestrez le message ou l’expérience suivant sur plusieurs canaux en temps quasi réel (parcours planifiés et pilotés par les événements). |
| [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/customer-journey-analytics) | Comprenez les parcours de bout en bout, identifiez les frictions et découvrez les audiences ou les opportunités d’action dans [!DNL Real-Time CDP] et [!DNL Adobe Journey Optimizer]. |
| [&#128279;](https://experienceleague.adobe.com/fr/docs/mix-modeler) | Mesurez la manière dont les canaux contribuent aux résultats et planifiez ou ajustez les dépenses marketing à l’aide de modèles qui utilisent des données connectées à [!DNL Experience Platform]. |

### [!DNL AI Assistant] et agents dans les applications clés {#app-ai}

L’IA dédiée aux agents et les [!DNL AI Assistant] sont disponibles dans [!DNL Adobe CX Enterprise] lorsque vous travaillez dans des applications prises en charge, dans les limites des rôles et autorisations de chaque produit. Les fonctionnalités et les noms des agents peuvent changer. Consultez toujours la documentation actuelle du produit pour votre organisation.

| Application | Comment l’IA peut vous aider (exemples) |
| --- | --- |
| [!DNL Real-Time CDP] | Les [!DNL AI Assistant] et les agents (par exemple, [!DNL Audience Agent]) peuvent vous aider à créer et à affiner des audiences à l’aide du langage naturel. Les audiences sont toujours stockées et activées dans [!DNL Real-Time CDP] en fonction de la gouvernance et des droits. |
| [!DNL Adobe Journey Optimizer] | Les [!DNL AI Assistant] et les agents peuvent vous aider à concevoir et à optimiser le parcours tout en utilisant les mêmes profils et audiences de [!DNL Experience Platform]. |
| [!DNL Customer Journey Analytics] | Les [!DNL AI Assistant] et agents peuvent vous aider à explorer et à résumer les données de parcours et les audiences de surface que vous pouvez publier sur [!DNL Experience Platform] pour activation dans [!DNL Real-Time CDP] et [!DNL Journey Optimizer]. |

En résumé, les applications représentent la manière dont les équipes effectuent leur travail quotidien (activation, parcours, analyse, mesure marketing). [!DNL Experience Platform] contient les données et les règles du client auxquelles toutes ces équipes font confiance. [!DNL Experience Platform] offre également des requêtes SQL et d’autres fonctionnalités par le biais des fonctionnalités et services ci-dessus.

## Fonctionnement conjoint d’Experience Platform et des applications {#platform-and-apps-together}

Les [!DNL Experience Platform] et les applications sont conçus pour être utilisés en tant que système unique.

- Une base de données, d’identité et de prise de décision partagée
- Applications d’activation, d’orchestration, d’analyse et de mesure
- Pour la plupart des tâches, une entrée commune et des services partagés dans [!DNL Adobe CX Enterprise]

Les sous-sections ci-dessous montrent ce système depuis quelques vues afin que vous puissiez faire correspondre la pile à votre rôle. La première vue est un tableau de pile de haut niveau couvrant les [!DNL Experience Platform], les applications et la couche d’expérience [!DNL CX Enterprise], suivi d’une vue d’ensemble de la manière dont le travail s’exécute de bout en bout.

### [!DNL Experience Platform] la pile à l’intérieur du [!DNL Adobe CX Enterprise] {#cx-enterprise-stack}

Le tableau ci-dessous présente l’architecture de haut niveau. [!DNL Adobe CX Enterprise] est la couche d’entrée d’expérience, de services partagés et d’IA. [!DNL Experience Platform] est la base. Les applications s’exécutent sur [!DNL Experience Platform].

| Calque | Ce que cela inclut | Rôle |
| --- | --- | --- |
| [!DNL CX Enterprise] d’expérience | [!DNL Adobe CX Enterprise] : interface utilisateur unifiée, navigation partagée, sélecteur d’applications, services partagés (par exemple [!DNL Audience Library], [!DNL Customer Attributes], ressources partagées, triggers, Marketplace), agents [!DNL AI Assistant] et agents intégrés au produit | Comment accéder aux [!DNL Experience Platform] et aux applications avec une expérience cohérente, des services partagés et une IA dédiée aux agents (dans les limites des autorisations de produit). |
| Applications (reposant sur [!DNL Adobe Experience Platform]) | [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer], [!DNL Customer Journey Analytics], [!DNL Adobe Marketing Campaign Analytics] et autres applications [!DNL Experience Platform] | Les audiences et l’activation, l’orchestration des parcours et la messagerie cross-canal, l’analyse et les informations omnicanal, ainsi que la mesure et la planification, le tout à l’aide des mêmes profils, audiences et gouvernance depuis la base. |
| fondation [!DNL Adobe Experience Platform] | Schémas XDM, [!DNL Identity Service], [!DNL Real-Time Customer Profile], segmentation, gouvernance, [!DNL Privacy Service], lac de données, [!DNL Query Service], [!DNL Edge] | Base de données, d’identité, de prise de décision et de conformité partagée par chaque application. |

[!DNL Experience Platform] et applications qui fonctionnent ensemble signifient trois choses.

1. Un profil client, de nombreux produits : [!DNL Real-Time Customer Profile], [!DNL Identity Service] et les règles de données sont partagés. [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer], [!DNL Customer Journey Analytics] et [!DNL Adobe Marketing Campaign Analytics] lus à partir de cette même base (et des données associées). Vous ne conservez pas une liste de clients pour Analytics ni une liste différente pour Marketing, sauf si votre processus l’exige.
2. Un ensemble de définitions d’événement et de champ et de nombreux cas d’utilisation : les données sont mises en forme avec des schémas XDM. Le même événement peut alimenter des rapports, des parcours et des règles d’audience. Les équipes passent moins de temps à se disputer sur les définitions.
3. Un emplacement pour les règles de données : vous appliquez des libellés et des politiques aux données dans [!DNL Experience Platform], et les applications utilisent ces données régies. Vous n’avez pas à redéfinir la conformité à l’intérieur de chaque produit, indépendamment des données que le produit lit à partir de la plateforme.

Le tableau [Flux de bout en bout](#end-to-end-flows) ci-dessous mappe le travail quotidien à la même pile à l’aide des étapes Connaître, Décider, Activer et Mesurer. Pour les vues de calques et de connexions basées sur des diagrammes, consultez [Adobe Experience Platform et applications (diagrammes d&#39;architecture)](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications) dans la collection de plans directeurs d&#39;architecture.

### Flux de bout en bout (comment le travail s’exécute sur les [!DNL Experience Platform] et les applications) {#end-to-end-flows}

Ce tableau associe les étapes Connaître, Décider, Activer et Mesurer au travail sur votre plateforme et décrit les applications que vous ajoutez généralement.

| Étape | Que fait [!DNL Experience Platform] | Ce que les applications ajoutent généralement |
| --- | --- | --- |
| Know | Importer les données, les structurer, lier l’identité, mettre à jour le profil | Les applications lisent le profil et les événements. Elles ne remplacent pas l’étape d’importation des données. |
| Décider | Créer des audiences et vérifier qui remplit les conditions en utilisant les données unies | [!DNL Real-Time CDP] pour créer des audiences. [!DNL Adobe Journey Optimizer] les chemins de parcours et la meilleure action à effectuer en fonction du contexte. |
| Activer | Destinations et export contrôlé des audiences et des attributs | [!DNL Real-Time CDP] prend en charge de nombreux modèles d’activation. Les parcours envoient des messages par le biais des canaux que vous avez configurés. |
| Mesure | Événements et identités suivant un modèle dans la couche de données | [!DNL Customer Journey Analytics] pour les rapports de parcours et de campagne. Les audiences que vous définissez dans [!DNL Customer Journey Analytics] peuvent être publiées dans [!DNL Adobe Experience Platform] pour activation dans [!DNL Real-Time CDP] et [!DNL Adobe Journey Optimizer]. [!DNL Adobe Marketing Campaign Analytics] pour la mesure et la planification du marketing unifié qui utilise des données connectées à [!DNL Experience Platform]. |

## Exemple : workflow full stack sur les quatre applications {#example-full-stack-workflow}

Le scénario ci-dessous présente un modèle courant. Vos équipes peuvent modifier l’ordre ou ignorer une étape. L’objectif est de montrer comment [!DNL Adobe Experience Platform] et [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer], [!DNL Customer Journey Analytics] et [!DNL Adobe Marketing Campaign Analytics] peuvent tous apparaître dans le même workflow.

### Le scénario {#example-scenario}

Une marque de vente au détail gère un programme d’acquisition et d’intégration saisonnier. La direction souhaite planifier les dépenses, atteindre les nouveaux acheteurs avec des médias achetés, accueillir les nouveaux clients avec des messages et rendre compte des résultats. La marque utilise des données client unifiées sur [!DNL Adobe Experience Platform].

### Ce qui se passe dans le workflow {#example-steps}

Les étapes ci-dessous résument un workflow type. L’ordre est donné à titre d’illustration. Les équipes chevauchent ou réorganisent souvent le travail.

1. [!DNL Adobe Experience Platform] : ingestion, identité et profil pour fournir la base de données sur laquelle reposent les autres étapes.
2. [!DNL Adobe Marketing Campaign Analytics] : Planifiez les dépenses et la combinaison de canaux pour le programme à l’aide de données de marketing et de résultats connectées.
3. [!DNL Real-Time CDP] : créez et activez des audiences, et utilisez des listes de suppression si nécessaire.
4. [!DNL Adobe Journey Optimizer] : exécutez les parcours et messages d’accueil et de cycle de vie.
5. [!DNL Customer Journey Analytics] : mesure les chemins du toucher à l’achat et montre les performances des programmes.

#### [!DNL Adobe Experience Platform]

Les équipes apportent des événements web et d’application, des commandes, des données de consentement, de coût ou de performances à partir des publicités, le cas échéant. Les données utilisent des schémas XDM partagés. Identity Service lie les clients connus. Le profil client en temps réel est mis à jour au fur et à mesure que les gens font leurs achats et s’inscrivent. Les règles de données et le consentement sont stockés dans Experience Platform.

*Sans cette étape, les applications ci-dessous n&#39;ont rien de fiable à lire.*

#### [!DNL Adobe Marketing Campaign Analytics] (anciennement appelé [!DNL Adobe Mix Modeler])

Marketing et finances examinez comment les canaux contribuent aux ventes et comment répartir le budget entre les médias pour la saison. Ils utilisent des modèles et des vues de planification qui s’appuient sur des données de marketing et de résultats harmonisées liées à Experience Platform.

*Cette étape répond à la question « comment devrions-nous investir » au niveau de la planification. Il ne s’agit pas de l’étape pour les e-mails ou pour les créations d’audiences quotidiennes.*

#### [!DNL Real-Time CDP]

Les équipes d’acquisition créent des audiences (par exemple, les acheteurs potentiels ou les personnes qui ont laissé des articles dans un panier). Ils activent ces audiences vers la publicité et d’autres destinations. Ils peuvent également créer des audiences de suppression afin que les clients actuels ne soient pas ciblés en tant que prospects.

*Cette étape répond à la question « Qui devons-nous contacter ou exclure dans les canaux achetés et détenus* ».

#### [!DNL Adobe Journey Optimizer]

Les équipes de cycle de vie exécutent un parcours de bienvenue après un achat ou une inscription. Le parcours écoute les conditions de profil ou d’événement, les branches (par exemple, premier achat vs répétition) et envoie des e-mails ou des messages mobiles.

*Cette étape répond à la question « Quel message ou chemin cette personne reçoit-elle ensuite* ? »

#### [!DNL Customer Journey Analytics]

Les équipes Analytics créent des rapports et des tableaux de bord sur le chemin complet allant de l’ad touch à l’achat et à l’intégration. Ils mesurent les entonnoirs, les canaux et les segments en utilisant les mêmes définitions d’événement et de profil que celles utilisées ailleurs par l’entreprise.

*Cette étape répond à « ce qui s’est passé dans le parcours et quelles parties ont fonctionné* ».

Les équipes exécutent souvent les applications en parallèle sur un trimestre. [!DNL Marketing Campaign Analytics] mises à jour peuvent se produire plus lentement que les audiences ou les parcours en direct. C&#39;est normal.

### Fonctionnement des applications ensemble {#example-together}

La liste suivante montre comment les applications fonctionnent les unes avec les autres pour fournir une solution complète.

- Un profil et un modèle d’événement. La même personne et les mêmes événements se propagent d’Experience Platform vers Real-Time CDP, Adobe Journey Optimizer et Customer Journey Analytics. Marketing Campaign Analytics utilise des données connectées et harmonisées d’Experience Platform. Il peut utiliser des résumés (par exemple, les dépenses hebdomadaires) ainsi que des données au niveau de l’événement, selon la configuration.
- Des boulots différents, la même vérité. Real-Time CDP détermine qui contacter. Adobe Journey Optimizer exécute ce qui se passe ensuite après une action. Customer Journey Analytics indique ce qui s’est produit entre les étapes. Adobe Marketing Campaign Analytics aide les équipes à déterminer quand et comment déplacer le budget à un niveau supérieur.
- Les règles de données se déplacent avec les données. Les libellés et le consentement sur Experience Platform affectent les profils qui peuvent être utilisés dans les segments, les parcours et les rapports.



## Exemple : workflow d’abandon de panier {#example-cart-abandonment}

Le tableau ci-dessous présente un second modèle courant. Il met insight en surbrillance pour que l’audience puisse être orchestrée sur le même profil et les mêmes événements. Il n’inclut pas les [!DNL Adobe Marketing Campaign Analytics]. Vos étapes et votre ordre peuvent différer.

| Étape | Ce qui se passe |
| --- | --- |
| Collecter et unifier ([!DNL Adobe Experience Platform]) | Les événements web et d’application sont collectés avec le [!DNL Experience Platform Web SDK] ou le [!DNL Experience Platform Mobile SDK]. Les commandes ou les données de point de vente peuvent être entrées par lot. [!DNL Identity Service] lie les identifiants dans des [!DNL Real-Time Customer Profile]. |
| Comprendre le comportement ([!DNL Customer Journey Analytics]) | Les analystes voient où les acheteurs se rendent et définissent un groupe (par exemple, les clients à forte valeur ajoutée qui ont ajouté au panier mais n’ont pas effectué d’achat dans les 24 heures) à l’aide des vues de données et des rapports. |
| Création d’une audience ([!DNL Customer Journey Analytics] pour [!DNL Experience Platform] à [!DNL Real-Time CDP]) | Les analystes enregistrent ce groupe en tant qu’audience publiée sur [!DNL Adobe Experience Platform]. [!DNL Real-Time CDP] l’expose en tant qu’audience pour l’activation et pour les parcours. |
| Orchestrer la récupération ([!DNL Adobe Journey Optimizer]) | Un parcours utilise la qualification d’audience ou les événements comme déclencheur (par exemple, entrée dans l’audience de l’abandonné de panier). Les messages peuvent se composer de plusieurs messageries : e-mail, web ou in-app, SMS ou push, selon votre configuration. |
| Activer ailleurs ([!DNL Real-Time CDP]) | La même audience peut accéder à des destinations (par exemple, des annonces) à des fins de remarketing ou de suppression, afin que vous n’envoyiez pas de messages aux personnes déjà converties. |
| Mesurer et affiner ([!DNL Customer Journey Analytics]) | Les équipes mesurent l’effet élévateur et affinent l’audience, la logique du parcours et le mix des canaux. |

## Précautions de configuration {#configuration-cautions}

Le tableau suivant répertorie les zones de problème courantes et les éléments à vérifier.

>[!IMPORTANT]
>
>Ces problèmes sèment la confusion dans les projets réels. Considérez-les comme des points de contrôle pour vos architectes et administrateurs.

| Zone | Que regarder |
| --- | --- |
| Identité | Si le Web, l’application et le CRM envoient des identifiants ou des paramètres d’espace de noms différents, le profil peut diviser une personne en deux. Les audiences, les parcours et les rapports ne correspondent pas. Alignez les règles d’identité et les identifiants principaux avant de mettre à l’échelle l’activation. |
| Règles de consentement et de données | Si les jeux de données utilisés dans [!DNL Real-Time CDP] ou [!DNL Adobe Journey Optimizer] ne sont pas correctement étiquetés ou consentis, vous pouvez activer ou envoyer un message à des personnes que vous ne devriez pas. Examinez les libellés, les politiques et les champs de consentement sur les mêmes jeux de données que ceux que vous utilisez pour les audiences et les parcours. |
| [!DNL Real-Time CDP] et [!DNL Adobe Journey Optimizer] simultanément | Une même personne peut se trouver dans une audience activée et dans un parcours. Vous pouvez envoyer un double message ou entrer en conflit avec des offres si vous n’utilisez pas de listes de suppression, de filtres d’entrée de parcours ou de règles d’effacement pour savoir qui entre dans un parcours. Coordonnez d’abord les équipes et effectuez un test dans un sandbox. |
| [!DNL Customer Journey Analytics] des définitions | Les rapports utilisent des vues de données et des règles de mesure. Si ces définitions ne correspondent pas aux événements ou attributs utilisés par vos spécialistes marketing dans [!DNL Real-Time CDP] ou [!DNL Adobe Journey Optimizer], les tableaux de bord ne seront pas d’accord avec les rapports de campagne. Alignez les définitions de dimension et de mesure avec les parties prenantes. |
| [!DNL Adobe Marketing Campaign Analytics] et forme des données | La modélisation mix utilise souvent des entrées harmonisées ou cumulées et des actualisations planifiées. Ne vous attendez pas à la même réponse en temps réel que [!DNL Real-Time Customer Profile]. Les données sur les dépenses et les résultats doivent être cartographiées et nettoyées en harmonisation. Mappages incorrects biaisant le crédit de canal et les conseils budgétaires. |
| [!DNL Marketing Campaign Analytics] comparé à [!DNL Customer Journey Analytics] | [!DNL Marketing Campaign Analytics] se concentre sur la contribution et la planification au niveau des canaux. [!DNL Customer Journey Analytics] se concentre sur les chemins et les audiences du parcours. Ils répondent à des questions connexes mais différentes. Ne forcez pas un KPI à correspondre à l’autre sans pont documenté. |
| Sandbox | La configuration dans un sandbox ne passe pas automatiquement à la production. Planifiez un processus de promotion pour les schémas, les audiences, les parcours et les connexions. |
| Fuseaux horaires | Les parcours, fenêtres de création de rapports et plateformes publicitaires peuvent utiliser différents fuseaux horaires. Les fenêtres mal alignées provoquent des décomptes « incorrects » et une entrée de parcours rompue. |

## Mécanismes de sécurisation et limitations {#guardrails-and-limitations}

Adobe publie des mécanismes de sécurisation pour [!DNL Adobe Experience Platform] et pour chaque application. Les mécanismes de sécurisation décrivent les limites, les performances attendues et les plages sécurisées pour la configuration. Ils vous aident à éviter les erreurs, les ralentissements ou les comportements instables. Les mécanismes de sécurisation ne sont pas des accords de niveau de service (SLA). Ils ne garantissent pas la vitesse ou la disponibilité au sens juridique du terme.

Votre contrat, la description du produit et la commande client peuvent définir des limites ou des droits contractuels. Ces règles peuvent différer de la documentation générale. En cas de doute, contactez votre équipe chargée du contrat et du compte Adobe, ainsi que [!DNL Experience League].

| Rubrique | Éléments à prévoir |
| --- | --- |
| Limites souples et limites strictes | Certaines limites sont indicatives. Si vous les dépassez de beaucoup, les performances peuvent baisser ou la latence peut augmenter. Les autres limites sont fixées par le système ou par votre contrat. Vous ne pouvez pas les dépasser sans modifier votre configuration ou votre achat. |
| Où des limites s’appliquent | De nombreuses limites s’appliquent au niveau de l’organisation, et non par sandbox. Les environnements Sandbox ont souvent des limites plus petites que la production. Les résultats de test dans un sandbox peuvent ne pas afficher des performances à grande échelle. |
| Ingestion et profil | Un volume d’événements, un volume d’identités ou un nombre de profils élevés affectent le coût, la vitesse et la stabilité. Appliquez des mécanismes de sécurisation pour l’ingestion de données et le profil lorsque vous concevez des pipelines. Des audiences très volumineuses ou des mises à jour très fréquentes peuvent souligner les chemins d’activation. |
| Segmentation et activation | [!DNL Real-Time CDP] dispose de mécanismes de sécurisation pour les audiences, l’activation et les destinations. Les destinations partenaires ont également leurs propres limites, tailles de fichier ou champs obligatoires. Une audience qui fonctionne dans l’interface utilisateur peut toujours échouer ou être tronquée à une destination si vous ignorez les deux côtés. |
| [!DNL Adobe Journey Optimizer] | Les parcours, les canaux et les taux de messages ont des limites de produit. Les parcours complexes ou les volumes élevés doivent être examinés par rapport aux mécanismes de sécurisation [!DNL Adobe Journey Optimizer] afin que les messages restent fiables. |
| [!DNL Customer Journey Analytics] | La création de rapports présente des limites sur les connexions, les vues de données, les lignes et la cardinalité. Les dimensions importantes ou les volumes d’événements très importants doivent être révisés afin que les rapports restent utilisables. |
| [!DNL Adobe Marketing Campaign Analytics] | La modélisation et la planification dépendent d&#39;un historique suffisant et de données harmonisées propres. Il existe des limites de produit sur les jeux de données, les modèles et le comportement d’actualisation. Les données fines ou bruyantes produisent des modèles faibles ou instables. |
| API et automatisation | Les appels programmatiques utilisent des limites de débit et des quotas. Les traitements par lots qui ignorent ces limites peuvent échouer ou ralentir. |
| Régions et disponibilité | Certaines fonctionnalités, destinations ou applications ne sont pas disponibles dans toutes les régions. Confirmez la région pour la résidence des données et la disponibilité du produit avant de concevoir le workflow complet. |

>[!NOTE]
>
>Les limites numériques et les valeurs par défaut changent au fil du temps. Utilisez les pages de mécanismes de sécurisation actuelles dans [!DNL Experience League], les vues d’utilisation de licence où se trouve votre entreprise et votre contrat.

## Où en savoir plus {#where-to-read-more}

Utilisez les rubriques d’aide suivantes pour aller au-delà de cette présentation.

- [Mécanismes de sécurisation d’Experience Platform et des applications &#x200B;](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-diagrams/architecture-overview/guardrails) : présentation du fonctionnement des mécanismes de sécurisation dans les [!DNL Experience Platform] et les applications.
- [Mécanismes de sécurisation pour l’ingestion des données](https://experienceleague.adobe.com/fr/docs/experience-platform/ingestion/guardrails) : débit d’ingestion et limites associées.
- [Mécanismes de sécurisation de Real-Time CDP &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/guardrails/overview) : audiences, activation et utilisation des [!DNL Real-Time CDP].
- [Utilisation de la licence](https://experienceleague.adobe.com/en/docs/experience-platform/landing/license-usage-and-guardrails/data-management-best-practices) : gestion des données et pratiques d’utilisation de la licence sur [!DNL Experience Platform] (le cas échéant, pour votre organisation).

Si votre workflow s’appuie fortement sur [!DNL Customer Journey Analytics], [!DNL Adobe Journey Optimizer], [!DNL Adobe Marketing Campaign Analytics] ou [!DNL Query Service], consultez également les rubriques relatives aux mécanismes de sécurisation pour ces produits dans l’aide de leur produit .

## Rôles et transferts {#roles-and-handoffs}

Ce tableau résume les rôles souvent impliqués à chaque étape et les parties de la pile qu’ils utilisent.

| Étape | Qui est souvent impliqué | Ce qu’ils utilisent principalement |
| --- | --- | --- |
| Définition de la signification et des règles pour les données | Gouvernance des données, juridique, leadership marketing | Schémas, libellés, politiques sur les [!DNL Experience Platform] |
| Configurer des pipelines de collecte et de données | Ingénieurs de données, technologie marketing | [!DNL Tags], SDK, sources, préparation des données sur [!DNL Experience Platform] |
| Création d’audiences et de parcours | Marketing, CRM, équipes de parcours | Applications ([!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer]) au-dessus du même profil |
| Activer et exécuter quotidiennement | Opérations marketing, médias, équipes chargées du cycle de vie | Destinations, rapports de parcours, alertes |
| Vérifier et améliorer | Analyses, conformité, opérations | Journaux d’audit, surveillance, tableaux de bord |

## Terminologie {#terminology}

Cette rubrique utilise les termes suivants de manière spécifique.

- [!DNL Adobe Experience Platform] : services et fonctionnalités partagés : intégration de données, modélisation des données, [!DNL Identity Service], [!DNL Real-Time Customer Profile], segmentation, destinations, gouvernance des données, confidentialité, services tels que [!DNL Query Service] et fonctionnalités telles que les sandbox. Pour connaître les différences entre ces termes, voir [En quoi les fonctionnalités, services et applications d’Experience Platform diffèrent &#x200B;](#feature-service-application).
- [!DNL Adobe CX Enterprise] : interface unifiée et couche de services partagés par laquelle vous accédez généralement aux applications [!DNL Experience Platform] et [!DNL Experience Platform]. Voir [[!DNL Adobe CX Enterprise]](#cx-enterprise).
- Applications : produits sous licence sur des [!DNL Experience Platform] (par exemple [!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer], [!DNL Customer Journey Analytics], [!DNL Adobe Marketing Campaign Analytics]) qui regroupent des workflows pour des tâches spécifiques. Ils ne sont pas les mêmes que [!DNL Experience Platform] services tels que [!DNL Query Service] et [!DNL Identity Service]. Les éditions et applications associées apparaissent dans [Autres applications et éditions sur Experience Platform](#other-applications-and-editions).
- [!DNL Adobe Marketing Campaign Analytics] (anciennement appelée [!DNL Adobe Mix Modeler]) : application sous licence pour la mesure et la planification du marketing (y compris la modélisation du marketing mix). [!DNL Experience League] aide sur les produits peut toujours utiliser les anciens chemins d’accès au nom du produit et du modéliseur de mix alors que la documentation est mise à jour après le changement de nom du produit.

Cela correspond à la manière dont la présentation de la documentation Experience Platform [&#128279;](https://experienceleague.adobe.com/en/docs/experience-platform/landing/documentation/overview) regroupe le contenu.

## Ressources supplémentaires {#additional-resources}

Les rubriques d’aide et collections suivantes développent les concepts de cette page.

- [Intégrations Adobe Experience Platform &#x200B;](integrations.md) : méthode de connexion d’autres produits [!DNL Adobe CX Enterprise] à [!DNL Experience Platform] (sources et destinations).
- [Présentation de &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/landing/home) : principaux points d’entrée pour obtenir de l’aide.
- [Présentation de la documentation Experience Platform &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/landing/documentation/overview) : organisation des rubriques d’aide.
- [Adobe Experience Platform et applications (diagrammes d&#39;architecture)](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications) : comment les [!DNL Experience Platform] et les applications s&#39;intègrent à un niveau élevé.
- [Plans directeurs d’expérience digitale](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/overview/experience-cloud) : exemples de conception par cas d’utilisation et secteur.

Pour une formation pratique, reportez-vous aux tutoriels et cours dans [!DNL Experience League] sur les [!DNL Experience Platform Web SDK], XDM et les schémas, l’identité, la segmentation et les destinations.
