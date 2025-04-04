---
title: Notes de mise à jour d’Adobe Experience Platform de novembre 2020
description: Notes de mise à jour de novembre 2020 pour Adobe Experience Platform.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2178'
ht-degree: 20%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : jeudi 11 novembre 2020**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Migration du lac de données de Adobe Experience Platform](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

Mises à jour des fonctionnalités existantes :

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [Service [!DNL Destinations]](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Migration du lac de données de Adobe Experience Platform {#migration}

Lorsqu’Adobe migre le lac de données de la génération 1 vers la génération 2, les utilisateurs pourront lire depuis le lac de données, mais toutes les fonctionnalités qui écrivent dans le lac de données seront affectées. Adobe contactera les administrateurs système pour discuter en détail de l’impact de la migration et confirmer les dates et heures de migration pour des organisations spécifiques.

Pour plus d’informations, consultez le [ Guide de migration du lac de données ](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] exploite les profils de produit [Adobe Admin Console](https://adminconsole.adobe.com) pour lier les utilisateurs à des autorisations et des sandbox. Les autorisations contrôlent l’accès à de nombreuses fonctionnalités d’Experience Platform, notamment la modélisation des données, la gestion des profils et l’administration des sandbox.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Autorisations | Dans l’[!DNL Admin Console], l’onglet d’un profil de produit [!DNL Experience Platform] vous permet de personnaliser les fonctionnalités de [!DNL Experience Platform] disponibles pour les utilisateurs associés à ce profil. Les catégories d’autorisations disponibles sont les suivantes : **[!UICONTROL Modélisation des données]**, **[!UICONTROL Gestion des données]**, **[!UICONTROL Gestion des profils]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Surveillance des données]**, **[!UICONTROL Administration des sandbox]**, **[!UICONTROL Destinations]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL Query Service]** et **[!UICONTROL Gouvernance des données]** ****. |
| Accès aux sandbox | L’onglet **[!UICONTROL Autorisations]** au sein d’un profil de produit [!DNL Experience Platform] peut accorder aux utilisateurs l’accès à des sandbox spécifiques. Consultez la section sur les [sandbox](#sandboxes) ci-dessous pour plus d’informations. |

Pour plus d’informations, consultez la [présentation du contrôle d’accès](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] est un service applicatif intégré à [!DNL Experience Platform]. Il vous permet de tirer parti de [!DNL Experience Platform] pour offrir à vos clients la meilleure offre et la meilleure expérience possible à tous les points de contact au bon moment.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Bibliothèque des offres centralisée | L’interface dans laquelle vous créez et gérez les différents éléments qui composent vos offres et définissez leurs règles et contraintes. |
| Moteur de décision d’offre | Le moteur de décision d’offre tire parti des données et des [!DNL Real-Time Customer Profiles] [!DNL Experience Platform], ainsi que de la bibliothèque des offres, pour sélectionner l’heure, les clients et les canaux pour lesquels les offres seront diffusées. |

Pour plus d’informations, consultez la documentation [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=fr).

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, [!DNL Experience Platform] fournit des sandbox qui divisent une instance de [!DNL Experience Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Sandbox de production | [!DNL Experience Platform] fournit un sandbox de production unique, qui ne peut pas être supprimé ou réinitialisé. Le nombre total de sandbox disponibles, en production et hors production, est déterminé par la licence acquise. |
| Sandbox hors production | Plusieurs sandbox hors production peuvent être créés pour une seule instance [!DNL Experience Platform], ce qui vous permet de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter votre sandbox de production. |
| Sélecteur de sandbox | Dans l’interface utilisateur [!DNL Experience Platform], le sélecteur de sandbox dans le coin supérieur gauche de l’écran vous permet de basculer entre les sandbox disponibles via un menu déroulant. Le sélecteur de sandbox fournit également une fonction de recherche qui vous permet de filtrer les sandbox disponibles. |
| En-tête `x-sandbox-name` | Tous les appels aux API [!DNL Experience Platform] doivent désormais inclure le nouvel en-tête `x-sandbox-name` , dont la valeur fait référence à l’attribut `name` du sandbox dans lequel l’opération aura lieu. |

Pour plus d’informations, consultez la [présentation des sandbox](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Opérations itératives | [!DNL Data Prep] mappeur prend désormais en charge l’exécution d’opérations itératives sur une hiérarchie. |
| Fonction du mappeur | [!DNL Data Prep] mappeur a désormais la possibilité de **pas** copier un attribut de la source vers le XDM cible. |

Pour plus d’informations, reportez-vous à la [[!DNL Data Prep] présentation](../../data-prep/home.md).

## Espace de travail de science des données {#dsw}

L’espace de travail de science des données utilise le machine learning et l’intelligence artificielle pour exploiter les informations contenues dans vos données. Intégré à Adobe Experience Platform, l’espace de travail de sciences des données vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de l’ensemble des solutions Adobe. Le Workspace de science des données accomplit cela notamment par l’utilisation de [!DNL JupyterLab]. [!DNL JupyterLab] est une interface utilisateur web pour [[!DNL Project Jupyter]](https://jupyter.org/) et est étroitement intégré à Adobe Experience Platform. Il fournit un environnement de développement interactif pour que les spécialistes des données puissent travailler avec des notebooks, du code et des données [!DNL Jupyter].

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Modèle [!DNL JupyterLab] créateur de recettes | Notebook pour la recette utilisation des exigences et versions mises à jour. [!DNL Python] image de base ML Runtime a été mise à jour afin d’utiliser [!DNL Python] 3.6.7 et un environnement [!DNL Conda] exclusivement. |

Pour plus d’informations, consultez le document sur la [création d’une recette à l’aide de notebooks Jupyter](../../data-science-workspace/jupyterlab/create-a-model.md).

## Service [!DNL Destinations] {#destinations}

Dans [Real-Time Customer Data Platform](../../rtcdp/overview.md), les destinations sont des intégrations préconfigurées à des plateformes de destination qui activent les données vers ces partenaires de manière transparente.

**Nouvelles destinations**

| Destination | Description |
| ----------- | ----------- |
| Braze | Braze est une plateforme d’engagement client complète qui alimente des expériences pertinentes et mémorables entre les clients et les marques qu’ils aiment. |
| Microsoft Bing | La destination Microsoft Bing vous permet d’exécuter des campagnes numériques de reciblage et d’audience ciblées dans Microsoft Display Advertising. |
| Le Trade Desk | Trade Desk est une plateforme en libre-service permettant aux acheteurs de publicités d’exécuter des campagnes numériques de reciblage et d’audience ciblée sur l’affichage, les vidéos et les sources d’inventaire mobile. |

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mises à jour de l’expérience utilisateur des détails de la destination | Le workflow de destination Real-Time CDP comprend désormais une surveillance intégrée afin que vous puissiez voir quels lots ont été activés. Cette fonctionnalité permet aux utilisateurs et utilisatrices de résoudre les problèmes directement dans le workflow pour les destinations par lots au moyen d’alertes et d’un tableau de bord de surveillance pour suivre les erreurs dans le pipeline de traitement. |
| Chiffrement de fichier | Pour les destinations basées sur des fichiers, les utilisateurs peuvent désormais ajouter un chiffrement à leurs fichiers exportés. |
| Planification des fichiers | Pour les destinations de stockage dans le cloud et par e-mail, les utilisateurs peuvent créer une exportation ponctuelle ou des instantanés quotidiens. |
| Champs obligatoires | Les utilisateurs peuvent marquer les champs comme obligatoires, en s’assurant que seuls les champs contenant le champ obligatoire sont exportés. |

Pour plus d’informations, reportez-vous à la [présentation des destinations](../../destinations/home.md).

## Intelligent Services {#intelligent-services}

Intelligent Services permet aux analystes et spécialistes du marketing d’exploiter la puissance de l’intelligence artificielle et du machine learning dans les cas d’utilisation de l’expérience client. Les analystes marketing peuvent obtenir des prédictions spécifiques aux besoins d’une entreprise en utilisant des configurations au niveau de l’entreprise sans avoir besoin d’expertise en sciences des données.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Jeu de données d’événements d’expérience client (CEE) | La création d’un jeu de données CEE prend désormais en charge l’ajout de champs d’identité au jeu de données avec l’éditeur de schémas. L’IA dédiée à l’attribution et l’IA dédiée aux clients utilisent l’identité principale pour combiner des événements. |

Pour plus d’informations, consultez la section sur [l’ajout de champs d’identité à un jeu de données](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) dans le guide de préparation des données des services intelligents.

### IA dédiée à l’attribution

Dans le cadre d’Intelligent Services, l’IA dédiée à l’attribution est un service d’attribution algorithmique à plusieurs canaux qui calcule l’influence et l’impact incrémentiel des interactions des clients par rapport à des résultats spécifiés.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Lien de la source de données | Le lien vers la source du jeu de données d’origine peut être affiché et accessible à partir du rail de droite d’une instance de service sélectionnée. |
| Modifier le nom de l’instance | Vous pouvez désormais modifier le nom d’une instance IA dédiée à l’attribution existante. |
| Cloner l’instance | Copie la configuration de l&#39;instance de service actuellement sélectionnée et autorise les modifications. |
| Modifier les paramètres de configuration des instances | Vous pouvez désormais modifier la configuration d’une instance IA dédiée à l’attribution existante si elle n’a pas encore commencé la notation. |
| Score unique | Vous pouvez désormais déclencher la notation de modèle ad hoc dans vos instances IA dédiée à l’attribution. |
| Transmettre à travers les colonnes | Vous pouvez désormais configurer des colonnes supplémentaires qui seront ajoutées aux fichiers de score de sortie brute pour ajouter des dimensions supplémentaires aux vues d’outils BI. |
| Activation et désactivation d’instances | Vous pouvez désormais activer et désactiver l’entraînement de modèle planifié et la notation de vos instances IA dédiée à l’attribution. |
| Suivi des droits | Vous pouvez trouver la quantité totale d’insights d’attribution consommés par votre compte dans le conteneur de création d’instances. |
| Répartition des points de contact par position | Un nouveau graphique d’informations qui fournit une analyse des points de contact par position du chemin de conversion. |
| Principaux chemins de conversion | Un nouveau graphique d’informations situé dans l’onglet Analyse des chemins . Le graphique contient une liste des cinq premiers chemins de conversion indiquant la séquence des points de contact des canaux marketing qui ont conduit au plus grand nombre de conversions. |
| Efficacité des points de contact | Fournit des informations détaillées sur les trois variables les plus importantes dont votre modèle mesure l’efficacité des points de contact. Les variables sont le rapport des chemins positifs et négatifs touchés, l’efficacité des points de contact et le volume des points de contact. |

Pour plus d’informations, consultez la [présentation de l’IA dédiée à l’attribution](../../intelligent-services/attribution-ai/overview.md).

### IA dédiée aux clients

L’IA dédiée aux clients, en tant que composant des services intelligents, permet aux marketeurs de générer des prédictions client au niveau individuel avec des explications. À l’aide de facteurs d’influence, Customer AI peut vous indiquer ce qu’un client est susceptible de faire et pourquoi. De plus, les spécialistes marketing peuvent tirer parti des prédictions et des informations de Customer AI pour personnaliser les expériences client en diffusant les offres et les messages les plus appropriés.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Lien de la source de données | Le lien vers la source du jeu de données d’origine peut être affiché et accessible à partir du rail de droite d’une instance de service sélectionnée. |
| Modifier le nom de l’instance | Vous pouvez modifier le nom d’une instance IA dédiée aux clients existante. |
| Modifier les paramètres de configuration des instances | Vous pouvez désormais modifier la configuration d’une instance IA dédiée aux clients existante si elle n’a pas encore démarré de notation. |
| Cloner l’instance | Copie la configuration de l&#39;instance de service actuellement sélectionnée et autorise les modifications. |
| Suivi des droits | Le nombre total de profils notés par l’IA dédiée aux clients pour votre compte figure dans le conteneur Créer une instance . |
| Objectif de prédiction | La flexibilité dans la création d’un objectif de prédiction a été augmentée avec de nouvelles options pour prédire si quelque chose « se produira » ou « ne se produira pas ». En outre, les options permettant de prédire si « tous » les événements se produisent ou « n’importe lequel » des événements se produit lorsque plusieurs événements sont utilisés ont été ajoutées. |
| Zoom sur les facteurs d&#39;influence | Les intervalles de facteurs d’influence supérieurs de propension contiennent désormais des analyses en profondeur. Les analyses en profondeur constituent une synthèse de niveau plus approfondie des valeurs de chacun des principaux facteurs d’influence au sein d’un intervalle de propension. |

Pour plus d’informations, veuillez lire la [présentation de l’IA dédiée aux clients](../../intelligent-services/customer-ai/overview.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le profil client en temps réel offre une vue holistique de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. [!DNL Profile] vous permet de consolider vos données client disparates en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Workflow des politiques de fusion mises à jour | Experience Platform a mis à niveau la configuration de la politique de fusion vers un nouveau workflow par étapes. Ce workflow permet aux utilisateurs de rassembler des fragments de données provenant de plusieurs jeux de données de profil et de définir la priorité de fusion des données entre ces jeux afin de créer une vue d’ensemble complète de chaque individu. Les utilisateurs peuvent fusionner les jeux de données XDM Individual Profile sélectionnés en sélectionnant la méthode de fusion appropriée (Horodatage ordonné ou Priorité du jeu de données) et en ajoutant les jeux de données ExperienceEvent aux jeux de données de profil. |
| Vue du schéma d’union | Dans l’interface utilisateur d’Experience Platform, les utilisateurs peuvent plus facilement trouver des informations concernant tous les schémas et jeux de données qui contribuent au schéma d’union, ainsi que les attributs clés de surface tels que les champs d’identité et de relation. Ces mises à jour améliorent la capacité à résoudre les problèmes et à vérifier que les profils sont correctement configurés, que les identités sont correctement assemblées et que les données ont bien été ingérées. |

Pour plus d’informations sur le profil client en temps réel, notamment les bonnes pratiques et les tutoriels relatifs à l’utilisation des données [!DNL Profile], consultez la [ présentation du profil client en temps réel](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Experience Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles sources**

| Fonctionnalité | Description |
| ------- | ----------- |
| [!DNL Shopify] | Vous pouvez désormais connecter [!DNL Shopify] à [!DNL Experience Platform] à l’aide de l’interface utilisateur ou de l’API [!DNL Flow Service]. Pour plus d’informations, consultez la présentation du connecteur [Shopify](../../sources/connectors/ecommerce/shopify.md). |

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mettre à jour les informations de connexion | Vous pouvez désormais mettre à jour les noms, descriptions et informations d’identification des connexions par lots existantes à l’aide de l’API [!DNL Flow Service] et de l’interface utilisateur. Pour plus d’informations, consultez le tutoriel sur [la mise à jour des connexions à l’aide de l’API Flow Service](../../sources/tutorials/api/update.md) et [la modification des détails du compte à l’aide de l’interface utilisateur](../../sources/tutorials/ui/monitor.md). |
| Suppression des connexions | Les connexions par lots contenant des erreurs ou devenues inutiles peuvent désormais être supprimées à l’aide de l’API [!DNL Flow Service] et de l’interface utilisateur. Pour plus d’informations, consultez le tutoriel sur [la suppression de connexions à l’aide de l’API Flow Service](../../sources/tutorials/api/delete.md) et [la suppression de comptes à l’aide de l’interface utilisateur](../../sources/tutorials/ui/delete-accounts.md). |
| Mapping hiérarchique | Vous pouvez prévisualiser un fichier source hiérarchique, tel que JSON ou Parquet, au cours du processus d’ingestion de données. Pour plus d’informations, consultez le tutoriel sur la [configuration d’un flux de données pour les connecteurs de stockage dans le cloud](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) dans l’interface utilisateur. |
| Prise en charge des API pour le mappage dans les sources en flux continu | Vous pouvez désormais utiliser des API pour exécuter des fonctions de mappage avec des sources en flux continu. |
| Prise en charge des API pour les délimiteurs personnalisés pour les sources d’espace de stockage dans le cloud | Vous pouvez désormais collecter des fichiers non délimités au format CSV à l’aide de sources d’espace de stockage. Vous pouvez utiliser n’importe quel délimiteur de colonne unique, tel qu’une tabulation, une virgule, une barre verticale, un point-virgule ou un hachage pour collecter des fichiers plats dans n’importe quel format. |
| Prise en charge des sandbox pour le connecteur Adobe Audience Manager | Le connecteur Audience Manager prend désormais en charge les sandbox. Les utilisateurs peuvent activer le connecteur pour acheminer les jeux de données Audience Manager vers le sandbox de leur choix (y compris les sandbox hors production). La configuration est limitée à un sandbox par organisation. |
| Améliorations de l’expérience utilisateur | L’ingestion basée sur des fichiers est désormais accessible via le catalogue de sources. |

Pour en savoir plus sur les sources, consultez la [vue d’ensemble des sources](../../sources/home.md).
