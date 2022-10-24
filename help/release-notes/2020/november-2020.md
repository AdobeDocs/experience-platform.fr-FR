---
title: Notes de mise à jour de Adobe Experience Platform, novembre 2020
description: Les notes de mise à jour de novembre 2020 pour Adobe Experience Platform.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '2184'
ht-degree: 27%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 11 novembre 2020**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Migration du lac de données Adobe Experience Platform](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

Mises à jour des fonctionnalités existantes :

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] Service](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Migration du lac de données Adobe Experience Platform {#migration}

Pendant que Adobe migre le lac de données de Gen1 vers Gen2, les utilisateurs pourront lire depuis le lac de données, mais toutes les fonctionnalités qui écrivent dans le lac de données seront affectées. Adobe contactera les administrateurs système pour discuter en détail de l’impact de la migration et confirmer les dates et heures de migration pour certaines organisations IMS.

Pour plus d’informations, veuillez lire la [Guide de migration du lac de données](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] exploite les profils de produit [Adobe Admin Console](https://adminconsole.adobe.com) pour lier les utilisateurs à des autorisations et des environnements de test. Les autorisations contrôlent l’accès à de nombreuses fonctionnalités de Platform, notamment la modélisation des données, la gestion des profils et l’administration des environnements de test.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Autorisations | Dans le [!DNL Admin Console], l’onglet dans un [!DNL Platform] le profil de produit vous permet de personnaliser ce qui [!DNL Platform] Les fonctionnalités sont disponibles pour les utilisateurs associés à ce profil. Les catégories d’autorisations disponibles sont les suivantes : **[!UICONTROL Modélisation des données]**, **[!UICONTROL Data Management]**, **[!UICONTROL Gestion des profils]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Surveillance des données]**, **[!UICONTROL Sandbox Administration]**, **[!UICONTROL Destinations]**, **[!UICONTROL Ingestion des données]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL Query Service]**, et **[!UICONTROL Gouvernance des données]**. |
| Accès aux environnements de test | L’onglet **[!UICONTROL Autorisations]** d’un profil de produit peut accorder aux utilisateurs l’accès à des environnements de test spécifiques. [!DNL Platform] Consultez la section sur les [environnements de test](#sandboxes) ci-dessous pour plus d’informations. |

Pour plus d’informations, consultez la [présentation du contrôle d’accès](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] est un service d’application intégré à [!DNL Experience Platform]. Il vous permet d’exploiter [!DNL Platform] pour offrir la meilleure offre et la meilleure expérience à vos clients sur tous les points de contact au bon moment.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Bibliothèque d’offres centralisée | Interface dans laquelle vous créez et gérez les différents éléments qui composent vos offres, et définissez leurs règles et contraintes. |
| Moteur de décision d’offre | Le moteur de décision d’offre tire parti de [!DNL Platform] data et [!DNL Real-time Customer Profiles], ainsi que la bibliothèque des offres, afin de sélectionner l’heure, les clients et les canaux auxquels les offres seront diffusées. |

Pour plus d’informations, reportez-vous à la section [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=fr) documentation.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] est conçu pour enrichir les applications d’expérience numérique à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience numérique en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, [!DNL Experience Platform] fournit des environnements de test qui divisent une seule [!DNL Platform] dans des environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Environnement de test de production  | [!DNL Experience Platform] fournit un environnement de test de production unique, qui ne peut pas être supprimé ou réinitialisé. Le nombre total d’environnements de test disponibles, production et hors production, est déterminé par la licence acquise. |
| Environnement de test hors production | Plusieurs environnements de test hors production peuvent être créés pour une seule [!DNL Platform] vous permettant de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter votre environnement de test de production. |
| Sélecteur d’environnement de test | Dans le [!DNL Experience Platform] l’interface utilisateur, le sélecteur d’environnements de test dans le coin supérieur gauche de l’écran vous permet de basculer entre les environnements de test disponibles via un menu déroulant. Le sélecteur d’environnements de test fournit également une fonction de recherche qui vous permet de filtrer les environnements de test disponibles. |
| En-tête `x-sandbox-name` | Tous les appels à [!DNL Experience Platform] Les API doivent désormais inclure la nouvelle `x-sandbox-name` dont la valeur fait référence à la propriété `name` de l’environnement de test dans lequel l’opération aura lieu. |

Pour plus d’informations, consultez la [présentation des environnements de test](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Opérations itératives | [!DNL Data Prep] Mapper prend désormais en charge les opérations itératives sur une hiérarchie. |
| Fonction Mapper | [!DNL Data Prep] Le mappeur peut désormais **not** Copiez un attribut de la source vers le XDM cible. |

Pour plus d’informations, reportez-vous à la [[!DNL Data Prep] présentation](../../data-prep/home.md).

## Data Science Workspace {#dsw}

Data Science Workspace utilise le machine learning et l’intelligence artificielle pour exploiter les informations contenues dans vos données. Intégré à Adobe Experience Platform, Data Science Workspace vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de l’ensemble des solutions Adobe. Data Science Workspace accomplit cela notamment par l’utilisation de [!DNL JupyterLab]. [!DNL JupyterLab] est une interface utilisateur web pour [[!DNL Project Jupyter]](https://jupyter.org/) et est étroitement intégré à Adobe Experience Platform. Il fournit un environnement de développement interactif avec lequel les spécialistes des données peuvent travailler. [!DNL Jupyter] notebooks, code et données.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| [!DNL JupyterLab] Modèle Recipe Builder | Mise à jour de l’utilisation et des versions du notebook vers les exigences de recette. [!DNL Python] Mise à jour de l’image de base de l’exécution ML pour l’utilisation [!DNL Python] 3.6.7 et a [!DNL Conda] environnement exclusivement. |

Pour plus d’informations, veuillez lire le document sur [création d’une recette à l’aide de notebooks Jupyter](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] Service {#destinations}

Dans [Real-time Customer Data Platform](../../rtcdp/overview.md), les destinations sont des intégrations prédéfinies avec des plateformes de destination qui activent les données vers ces partenaires de manière transparente.

**Nouvelles destinations**

| Destination | Description |
| ----------- | ----------- |
| Braze | Braze est une plateforme d’engagement client complète qui optimise les expériences pertinentes et mémorables entre les clients et les marques qu’ils aiment. |
| Microsoft Bing | La destination Microsoft Bing vous aide à exécuter le reciblage et l’audience des campagnes numériques ciblées dans Microsoft Display Advertising. |
| Le bureau de commerce | Le bureau commercial est une plateforme en libre-service permettant aux acheteurs de publicités d’exécuter le reciblage et d’exécuter des campagnes numériques ciblées sur l’affichage, la vidéo et les sources d’inventaire mobiles. |

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mises à jour de l’UX des détails de la destination | Le workflow de destination Real-Time CDP comprend désormais une surveillance en ligne afin que vous puissiez voir quelles activations par lots ont réussi. Cette fonctionnalité permet aux utilisateurs de résoudre les problèmes directement dans le workflow pour les destinations par lots au moyen d’alertes et d’un tableau de bord de surveillance afin de suivre les erreurs dans le pipeline de traitement. |
| Chiffrement de fichier | Pour les destinations basées sur des fichiers, les utilisateurs peuvent désormais ajouter un chiffrement à leurs fichiers exportés. |
| Planification des fichiers | Pour les destinations de stockage dans le cloud et par courrier électronique, les utilisateurs peuvent créer une exportation unique ou créer des instantanés quotidiens. |
| Champs obligatoires | Les utilisateurs peuvent marquer les champs comme obligatoires, en s’assurant que seuls les champs contenant le champ obligatoire sont exportés. |

Pour plus d’informations, reportez-vous à la [présentation des destinations](../../destinations/home.md).

## Intelligent Services {#intelligent-services}

Intelligent Services permet aux analystes et spécialistes du marketing d’exploiter la puissance de l’intelligence artificielle et de l’apprentissage automatique dans les cas d’utilisation de l’expérience client. Les analystes marketing peuvent obtenir des prédictions spécifiques aux besoins d&#39;une entreprise en utilisant des configurations au niveau de l&#39;entreprise sans avoir besoin d&#39;expertise en sciences des données.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Jeu de données d’événements d’expérience client (CEE) | La création d’un jeu de données CEE prend désormais en charge l’ajout de champs d’identité au jeu de données à l’aide de l’éditeur de schémas. Attribution AI et Customer AI utilisent l’identité Principale pour combiner des événements. |

Pour plus d’informations, veuillez lire la section sur [ajout de champs d’identité à un jeu de données](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) dans le guide de préparation des données d’Intelligent Services.

### IA dédiée à l’attribution

Dans le cadre d’Intelligent Services, Attribution AI est un service d’attribution algorithmique à plusieurs canaux qui calcule l’influence et l’impact incrémentiel des interactions des clients par rapport à des résultats spécifiés.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Lien de source de données | Le lien vers la source du jeu de données d’origine peut être affiché et accédé à partir du rail droit d’une instance de service sélectionnée. |
| Modifier le nom de l’instance | Vous pouvez désormais modifier le nom d’une instance Attribution AI existante. |
| Clonage d’instance | Copie la configuration de l’instance de service actuellement sélectionnée et autorise les modifications. |
| Modification des paramètres de configuration de l’instance | Vous pouvez désormais modifier la configuration d’une instance Attribution AI existante si elle n’a pas encore commencé la notation. |
| Une notation ponctuelle | Vous pouvez désormais déclencher une notation de modèle ad hoc dans vos instances Attribution AI. |
| Transmission de colonnes | Vous pouvez maintenant configurer des colonnes supplémentaires qui seront ajoutées aux fichiers de score de sortie bruts pour ajouter des dimensions supplémentaires aux vues de l’outil de BI. |
| Activation et désactivation des instances | Vous pouvez désormais activer et désactiver la formation et la notation de modèle planifiées de vos instances Attribution AI. |
| Suivi des droits | Vous trouverez la quantité totale d’informations d’attribution consommées par votre compte dans le conteneur de création d’instance. |
| Ventilation des points de contact par position | Un nouveau graphique d’insights qui fournit une analyse des points de contact par position de chemin de conversion. |
| Meilleurs chemins de conversion | Un nouveau graphique d’informations situé dans l’onglet Analyse de chemin d’accès. Le graphique contient une liste des cinq principaux chemins de conversion qui indiquent la séquence des points de contact des canaux marketing qui ont généré le plus de conversions. |
| Efficacité des points de contact | Fournit des informations détaillées sur les trois variables les plus importantes selon lesquelles votre modèle mesure l’efficacité des points de contact. Les variables sont le rapport entre les chemins positifs et négatifs touchés, l’efficacité du point de contact et le volume du point de contact. |

Pour plus d’informations, veuillez lire la [Présentation d’Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### IA dédiée aux clients

En tant que composant des services intelligents, Customer AI permet aux professionnel du marketing de générer des prédictions client au niveau individuel avec des explications. À l’aide de facteurs d’influence, Customer AI peut vous indiquer ce qu’un client est susceptible de faire et pourquoi. De plus, les professionnels du marketing peuvent tirer parti des prédictions et des informations de Customer AI pour personnaliser les expériences client en diffusant les offres et les messages les plus appropriés.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Lien de source de données | Le lien vers la source du jeu de données d’origine peut être affiché et accédé à partir du rail droit d’une instance de service sélectionnée. |
| Modifier le nom de l’instance | Vous pouvez modifier le nom d’une instance de Customer AI existante. |
| Modification des paramètres de configuration de l’instance | Vous pouvez désormais modifier la configuration d’une instance de Customer AI existante si elle n’a pas encore commencé une notation. |
| Clonage d’instance | Copie la configuration de l’instance de service actuellement sélectionnée et autorise les modifications. |
| Suivi des droits | Vous pouvez trouver le nombre total de profils notés par Customer AI pour votre compte dans le conteneur d’instances de création. |
| Objectif de prédiction | La flexibilité de création d’un objectif de prédiction a été augmentée avec de nouvelles options pour prédire si quelque chose &quot;va se produire&quot; ou &quot;ne va pas se produire&quot;. En outre, les options permettant de prédire si &quot;tous&quot; les événements se produisent ou &quot;l’un&quot; des événements se produit lorsque plusieurs événements sont utilisés ont été ajoutées. |
| Effet déroulant des facteurs d’influence | Les compartiments de facteurs d’influence supérieurs de propension contiennent désormais des explorations. Les listes déroulantes constituent un résumé plus détaillé des valeurs pour chacun des principaux facteurs d’influence au sein d’un intervalle de propension. |

Pour plus d’informations, veuillez lire la [Présentation de Customer AI](../../intelligent-services/customer-ai/overview.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Profil client en temps réel offre une vue d’ensemble de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. [!DNL Profile] vous permet de consolider vos données client disparates en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Workflow des stratégies de fusion mis à jour | Platform a mis à niveau la configuration de la stratégie de fusion vers un nouveau workflow par étapes. Ce workflow permet aux utilisateurs de rassembler des fragments de données provenant de plusieurs jeux de données Profile et de définir la priorité de la manière dont les données sont fusionnées dans ces jeux de données afin de créer une vue d’ensemble exhaustive de chaque individu. Les utilisateurs peuvent fusionner des jeux de données XDM Individual Profile sélectionnés en sélectionnant la méthode de fusion appropriée (ordre d’horodatage ou priorité du jeu de données) et en ajoutant des jeux de données ExperienceEvent aux jeux de données Profile. |
| Vue du schéma d’union | Dans l’interface utilisateur de l’Experience Platform, les utilisateurs peuvent trouver plus facilement des informations concernant tous les schémas et jeux de données contribuant au schéma d’union, ainsi que des attributs de clé de surface tels que les champs d’identité et de relation. Ces mises à jour améliorent la possibilité de dépanner et de valider que les profils sont correctement configurés, que les identités sont correctement regroupées et que les données ont été ingérées avec succès. |

Pour plus d’informations sur Real-time Customer Profile, notamment des tutoriels et des bonnes pratiques pour travailler avec [!DNL Profile] data, veuillez lire la [Présentation de Real-time Customer Profile](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide de [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles sources**

| Fonctionnalité | Description |
| ------- | ----------- |
| [!DNL Shopify] | Vous pouvez désormais connecter [!DNL Shopify] à [!DNL Experience Platform] à l’aide de l’interface utilisateur ou de l’API [!DNL Flow Service]. Voir [Présentation du connecteur Shopify](../../sources/connectors/ecommerce/shopify.md) pour plus d’informations. |

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mise à jour des informations de connexion | Vous pouvez désormais mettre à jour les noms, descriptions et informations d’identification des connexions par lots existantes à l’aide de la variable [!DNL Flow Service] API et interface utilisateur. Pour plus d’informations, consultez le tutoriel sur [mise à jour des connexions à l’aide de l’API Flow Service](../../sources/tutorials/api/update.md) et [modification des détails d’un compte à l’aide de l’interface utilisateur](../../sources/tutorials/ui/monitor.md). |
| Suppression des connexions | Les connexions par lots contenant des erreurs ou devenues inutiles peuvent désormais être supprimées à l’aide de la variable [!DNL Flow Service] API et interface utilisateur. Pour plus d’informations, consultez le tutoriel sur [suppression des connexions à l’aide de l’API Flow Service](../../sources/tutorials/api/delete.md) et [suppression de comptes à l’aide de l’interface utilisateur](../../sources/tutorials/ui/delete-accounts.md). |
| Mappage hiérarchique | Vous pouvez prévisualiser un fichier source hiérarchique, tel que JSON ou Parquet, pendant le processus d’ingestion des données. Voir le tutoriel sur [configuration d’un flux de données pour les connecteurs de stockage dans le cloud dans l’interface utilisateur](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) pour plus d’informations. |
| Prise en charge des API pour le mappage dans les sources de diffusion en continu | Vous pouvez désormais utiliser des API pour exécuter des fonctions de mappage avec des sources en continu. |
| Prise en charge des API pour les délimiteurs personnalisés pour les sources de stockage dans le cloud | Vous pouvez désormais collecter des fichiers non délimités par un fichier CSV à l’aide de sources de stockage dans le cloud. Vous pouvez utiliser n’importe quel délimiteur de colonne, tel qu’une tabulation, une virgule, une barre verticale, un point-virgule ou un hachage, pour collecter des fichiers plats dans n’importe quel format. |
| Prise en charge des environnements de test pour le connecteur Adobe Audience Manager | Le connecteur d’Audience Manager est désormais compatible avec les environnements de test. Les utilisateurs peuvent activer le connecteur pour acheminer les jeux de données d’Audience Manager vers l’environnement de test de leur choix (y compris les environnements de test hors production). La configuration est limitée à un environnement de test par organisation IMS. |
| Améliorations de l’expérience utilisateur | L’ingestion basée sur des fichiers est désormais accessible par le biais du catalogue de sources. |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
