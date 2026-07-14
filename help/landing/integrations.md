---
title: Intégrations [!DNL Adobe Experience Platform]
description: Découvrez comment étendre votre pile  [!DNL Adobe Analytics], [!DNL Adobe Target], and other products connect to [!DNL Experience Platform] ’expérience client en tant que sources ou destinations.
solution: Experience Platform
feature: Getting Started
topic: Overview
role: User, Developer, Leader
source-git-commit: 8d7b4a77161914147004f559913ee9b2ccf888c0
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 0%

---


# Intégrations à [!DNL Adobe Experience Platform]

Si votre équipe utilise [!DNL Adobe Experience Platform] conjointement avec d’autres solutions Adobe, vous avez besoin d’une image simple de ce qui connecte et où, sans vous noyer dans les noms de produits. Cette page vous donne une idée de la manière dont les données entrent en [!DNL Experience Platform], dont les audiences et les attributs sont envoyés à des outils tels que [!DNL Adobe Target] et où lire les guides de configuration détaillés.

Commencez par [Comment Adobe Experience Platform et les applications fonctionnent ensemble](apps-overview.md) si vous souhaitez obtenir des informations complètes sur les applications [!DNL Experience Platform]-first ([!DNL Real-Time CDP], [!DNL Adobe Journey Optimizer], [!DNL Customer Journey Analytics], [!DNL Adobe Marketing Campaign Analytics] (anciennement [!DNL Adobe Mix Modeler])). Cette page d’accompagnement se concentre sur d’autres produits de la pile Adobe qui sont liés à [!DNL Experience Platform].

## Ce que couvre cette page {#what-this-page-covers}

Utilisez cette liste comme mappage. Vous pouvez accéder à n’importe quelle section à partir des en-têtes ci-dessous.

- **Deux modèles mentaux :** les applications [!DNL Experience Platform]-first par rapport aux produits qui s’intègrent aux [!DNL Experience Platform] (sources, destinations, shell de [!DNL Adobe CX Enterprise] partagé).
- **Quatre modèles d’intégration :** Ingestion, activation, services partagés et [!DNL Data Collection] (la collection fait partie d’[!DNL Experience Platform], et non d’un produit secondaire distinct).
- **Applications Adobe en tant que sources** [!DNL Analytics], [!DNL Audience Manager], [!DNL Campaign], [!DNL Marketo] et autres qui importent des données dans [!DNL Experience Platform].
- **[!DNL Adobe Target]:** Utilisation des audiences et des attributs [!DNL Experience Platform] dans la personnalisation et les tests.
- **Scénarios réels :** exemples courts de [!DNL Analytics] en tant que source et de [!DNL Target] en tant que destination.
- **Autres destinations :** où parcourir les connecteurs au-delà de la [!DNL Target].
- **Trois vérifications avant la mise à l’échelle :** identité, gouvernance, système d’enregistrement.

>[!NOTE]
>
>Il s’agit d’une présentation et non d’un tutoriel de configuration. La modification de la licence, de la région et du produit contrôle les éléments que vous pouvez activer. Pour obtenir une configuration détaillée du connecteur, des limites et des chemins d’interface utilisateur, suivez les guides des sources et des destinations de [!DNL Experience Platform] liés et l’aide propre à chaque produit.

## À qui cela s&#39;adresse-t-il {#who-should-read}

| Si vous êtes... | Tu auras... |
| --- | --- |
| Architecte ou ingénieur | Un modèle mental unique pour les pipelines : ce qui arrive en [!DNL Experience Platform], ce qui [!DNL Experience Platform] et ce qui se trouve dans le shell Adobe partagé. |
| Opérations marketing ou prospect CX | La clarté sur laquelle les outils Adobe alimentent les [!DNL Experience Platform] par rapport aux audiences et aux attributs, y compris les [!DNL Adobe Target] pour les expériences sur site et in-app. |
| Analyste ou praticien des données | Contexte expliquant comment les données d’analyse ou de campagne historiques s’adaptent aux données de profil unifiées et pourquoi les définitions doivent toujours correspondre. |

## Applications [!DNL Experience Platform] et intégrations {#built-on-vs-connects}

Voici la distinction qui réduit la confusion :

- **Basé sur [!DNL Experience Platform] :** des produits comme [!DNL Real-Time CDP] et [!DNL Journey Optimizer] exécutent leurs workflows principaux sur les mêmes profils, audiences et gouvernance que ceux que vous configurez dans [!DNL Experience Platform]. Voir [Objectif de chaque application]apps-overview.md#applications-at-a-glance).
- **S’intègre à [!DNL Experience Platform] :** un autre produit Adobe envoie des données aux [!DNL Experience Platform] (sources), reçoit des audiences ou des attributs de [!DNL Experience Platform] (destinations) ou s’affiche avec des [!DNL Experience Platform] dans [!DNL Adobe CX Enterprise] (navigation partagée, [!DNL Audience Library] et services similaires). Pour plus de contexte, consultez [Adobe CX Enterprise](apps-overview.md#cx-enterprise).

La plupart des équipes du monde réel utilisent les deux. Vous unifiez les données client sur [!DNL Experience Platform] et vous connectez toujours l’historique d’analyse, les outils multimédias ou les produits de personnalisation à l’emplacement approprié selon votre feuille de route.

## Modèles d’intégration (référence rapide) {#integration-types}

| Motif | En termes simples | Commencer ici |
| --- | --- | --- |
| Sources | Vous importez des données dans [!DNL Experience Platform] jeux de données (souvent vers [!DNL Real-Time Customer Profile]). | [Présentation des sources](../sources/home.md) |
| Destinations | Vous envoyez des audiences, des attributs ou des exportations vers des canaux, des annonces, de la personnalisation, du stockage ou des partenaires. | [Vue d’ensemble des destinations](../destinations/home.md) |
| Shared [!DNL CX Enterprise] services | Vous passez d’une application Adobe à l’autre à l’aide d’un seul shell qui inclut la navigation et des services partagés tels que [!DNL Audience Library] ou [!DNL Customer Attributes], et non d’un canal de données distinct en soi. | [Adobe CX Entreprise](apps-overview.md#cx-enterprise) |
| [!DNL Data Collection] | Vous collectez le comportement des sites et des applications ([!DNL Tags], [!DNL Web SDK], [!DNL Mobile SDK], flux de données) dans [!DNL Experience Platform] et [!DNL Edge Network]. Il s’agit d’une partie d’[!DNL Experience Platform], et non d’un ajout facultatif à un autre cloud. | [&#x200B; Présentation de la collecte de données &#x200B;](../collection/home.md) |

## [!DNL Data Collection] : fait partie de votre [!DNL Experience Platform] foundation {#data-collection}

Utilisez des [!DNL Adobe Experience Platform Data Collection] ([!DNL Tags], [!DNL Experience Platform Web SDK], [!DNL Experience Platform Mobile SDK] et [flux de données](../datastreams/overview.md)) pour implémenter la collecte dans [!DNL Experience Platform] et le [!DNL Edge Network]. Considérez-le comme une infrastructure qui se trouve avec l’ingestion et la [!DNL Identity Service], et non pas aux côtés de clouds marketing indépendants.

Si vous déployez déjà des [!DNL Web SDK] ou des [!DNL Mobile SDK] pour [!DNL Real-Time CDP], [!DNL Journey Optimizer] ou [!DNL Customer Journey Analytics], vous utilisez la même couche décrite sous [Services Experience Platform en un coup d’œil](apps-overview.md#core-platform-services).

## Importation de données d’application Adobe dans [!DNL Experience Platform] (sources) {#adobe-sources}

Vous disposez peut-être déjà de données enrichies dans d’autres produits Adobe. [!DNL Experience Platform] pouvez effectuer une ingestion à partir de plusieurs d’entre eux afin que les champs d’historique et spécialisés se trouvent à côté de votre modèle unifié, toujours avec des schémas, un mappage et une gouvernance appliqués.

Voici quelques exemples répertoriés dans [!DNL Experience Platform] documentation :

- [!DNL Adobe Analytics] (données et classifications de suite de rapports)
- [!DNL Adobe Audience Manager]
- [!DNL Adobe Campaign Managed Cloud Services]
- [!DNL Marketo Engage]

Étape suivante : ouvrez la [Présentation des sources](../sources/home.md), puis utilisez la catégorie Applications Adobe du catalogue pour rechercher le connecteur dont vous avez besoin.

## [!DNL Adobe Target] {#adobe-target}

[!DNL Adobe Target] est l’endroit où de nombreuses équipes exécutent des opérations de personnalisation et d’expérimentation sur des sites web, des applications mobiles et des points de contact similaires. Elle ne figure pas parmi les quatre [!DNL Experience Platform] premières applications de la [présentation complémentaire](apps-overview.md#applications-at-a-glance). Au lieu de cela, [!DNL Target] agit généralement sur ce que vous avez déjà décidé dans [!DNL Experience Platform] (qui se qualifie pour quoi, quels attributs comptent).

Comment cela fonctionne-t-il généralement pour vous :

1. **Activer à partir de [!DNL Experience Platform] :** vous partagez des audiences créées à partir de [!DNL Real-Time Customer Profile] (et de vos workflows de segmentation) dans [!DNL Target] à l’aide de la [connexion Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) dans le catalogue des destinations. Lorsque le produit le prend en charge, vous envoyez également des attributs de profil pour la personnalisation, et pas seulement l’appartenance à une liste.
2. **Faire correspondre l’implémentation à votre pile :** ce que vous pouvez faire dépend de la manière dont [!DNL Target] est déployé : [!DNL Experience Platform Web SDK] avec [flux de données](../datastreams/overview.md) ou d’autres chemins décrits dans le guide de destination. Certains scénarios utilisent [segmentation Edge](../segmentation/home.md#edge) et [personnalisation Edge](../destinations/ui/activate-edge-personalization-destinations.md). Les audiences par lots et en flux continu se comportent différemment selon la configuration. La documentation de destination décrit la matrice.

Où lire la suite : Commencez par la connexion [&#128279;](../destinations/catalog/personalization/adobe-target-connection.md) (cas d’utilisation, sandbox, espaces de travail, mappage). Pour le contexte de [!DNL Edge Network] et de collecte, voir [Présentation de la collecte de données](../collection/home.md).

## Scénarios réels {#real-world-scenarios}

Ces histoires sont simplifiées à titre d’illustration. Vos sources, votre configuration d’identité et vos licences seront différentes. Utilisez-les comme amorces de conversation avec votre équipe d’implémentation et non comme scripts de déploiement.

### Marque de vente au détail : [!DNL Adobe Analytics] historique rejoint les profils unifiés {#scenario-analytics}

Un retailer s’appuie déjà sur des [!DNL Adobe Analytics] pour le comportement numérique et l’attribution des campagnes. Ils activent le connecteur source [&#128279;](../sources/connectors/adobe-applications/analytics.md) de sorte que les données de la suite de rapports arrivent dans des jeux de données [!DNL Experience Platform] avec des mappages de champs convenus. Les règles d’identité lient les identifiants [!DNL Analytics] aux identifiants d’espace de noms utilisés ailleurs (par exemple, dans les systèmes CRM ou de fidélité lorsque la politique le permet). Une fois que ces données se trouvent aux côtés d’événements web et d’applications plus récents collectés par l’intermédiaire de [!DNL Data Collection], les professionnels du marketing créent des audiences dans [!DNL Real-Time CDP] à partir d’une image plus complète, non seulement « qui a cliqué hier » de manière isolée, mais qui elles sont sur l’ensemble des canaux. Ces audiences peuvent être activées pour les e-mails, les médias achetés ou les parcours [!DNL Adobe Journey Optimizer] en utilisant les mêmes libellés de gouvernance que l’équipe a définis sur [!DNL Experience Platform].

À retenir : [!DNL Analytics] fait partie de l’enregistrement client unifié sur [!DNL Experience Platform] au lieu d’un silo distinct, tant que l’identité et les définitions restent alignées.

### Même retailer : les audiences optimisent la personnalisation dans [!DNL Adobe Target] {#scenario-target}

L’équipe de personnalisation souhaite que les grilles de héros et de produits de la page d’accueil reflètent le niveau de fidélité et la navigation récente à forte intention, et non un site à taille unique. Les audiences créées sur [!DNL Experience Platform] (par exemple, les membres qui ont parcouru l’équipement de course mais n’ont pas effectué d’achat en sept jours) sont activées pour [!DNL Adobe Target] via la connexion [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md). [!DNL Target] activités et expériences lisent ces audiences afin que les visiteurs voient des offres ou des mises en page personnalisées dans les tests que l’équipe y exécute. En fonction de l’implémentation, les attributs de profil peuvent également s’écouler pour une personnalisation plus riche. Les configurations orientées Edge peuvent utiliser des [!DNL Web SDK] et des flux de données comme décrit dans ce guide de destination.

À retenir : [!DNL Experience Platform] décide qui est admissible. [!DNL Adobe Target] décide de la manière de présenter l’expérience à ces visiteurs dans le cadre de vos tests et activités.

## Autres destinations Adobe et partenaires {#adobe-destinations}

En plus de [!DNL Target], vous pouvez activer de nombreux autres points d’entrée Adobe et non Adobe (e-mail, publicités, stockage, etc.) en fonction des droits.

Parcourez tous les éléments du [catalogue des destinations](../destinations/catalog/overview.md). Confirmez toujours votre contrat et la disponibilité régionale d’un connecteur donné avant de le contourner.

Pour [!DNL Real-Time CDP B2B Edition], [!DNL Journey Orchestration], [!DNL Real-Time CDP Collaboration] et d&#39;autres applications sur [!DNL Experience Platform] qui ne sont pas les quatre dans le tableau compagnon principal, voir [Autres applications et éditions sur Experience Platform](apps-overview.md#other-applications-and-editions).

## Trois vérifications avant la mise à l&#39;échelle {#checkpoints}

Lorsque vous transférez des [!DNL Experience Platform] à d’autres produits Adobe, les équipes réservent moins de surprises si vous êtes d’accord dès le départ sur les points suivants :

- **Identité :** les espaces de noms et les identifiants sont-ils alignés de sorte que le profil, les destinations et les rapports fassent tous référence à la même personne ou au même compte, là où la politique le permet ? Sinon, les audiences et les tableaux de bord ne correspondront pas et vos clients obtiendront des expériences incohérentes.
- **Gouvernance :** les libellés et le consentement sur [!DNL Experience Platform] suivent vos audiences dans l’activation. Les outils en aval doivent respecter ces choix, et non les contourner.
- **Système d’enregistrement :** est-[!DNL Experience Platform] la source de vérité pour un attribut donné de ce parcours ou un autre système le possède-t-il toujours ? L’ambiguïté ici entraîne des messages et des rapports contradictoires.

## Ressources supplémentaires {#additional-resources}

- [Comment Adobe Experience Platform et les applications fonctionnent ensemble &#x200B;](apps-overview.md) : applications [!DNL Experience Platform] et comment elles partagent des données.
- [Présentation de Adobe Experience Platform &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/landing/home) : principaux points d&#39;entrée de l&#39;aide.
- [Plans directeurs d’expérience digitale](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/overview/experience-cloud) : architectures de référence pour les solutions Adobe.
- [Adobe Experience Platform et applications (diagrammes d&#39;architecture)](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications) : diagrammes de pile visuelle.
