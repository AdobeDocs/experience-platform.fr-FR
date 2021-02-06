---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour d’Experience Platform, 11 novembre 2020
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 25%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 11 novembre 2020**

Nouvelles fonctionnalités d’Adobe Experience Platform :

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

## Migration de Adobe Experience Platform Data Lake {#migration}

Bien que l&#39;Adobe migre le lac Data de Gen1 à Gen2, les utilisateurs pourront lire à partir de Data Lake, mais toutes les capacités qui s&#39;inscrivent dans le lac Data seront affectées. L&#39;Adobe contactera les administrateurs système pour discuter en détail de l&#39;impact de la migration et confirmer les dates et heures de migration pour certaines organisations IMS.

Pour plus d&#39;informations, consultez le [Guide de migration de Data Lake](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] exploite les profils de produit [Adobe Admin Console](https://adminconsole.adobe.com) pour lier les utilisateurs à des autorisations et des environnements de test. Les autorisations contrôlent l’accès à de nombreuses fonctionnalités de Platform, notamment la modélisation des données, la gestion des profils et l’administration des environnements de test.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Autorisations | Dans le [!DNL Admin Console], l&#39;onglet d&#39;un profil de produits [!DNL Platform] vous permet de personnaliser les fonctionnalités [!DNL Platform] disponibles pour les utilisateurs associés à ce profil. Les catégories d&#39;autorisation disponibles sont les suivantes : **[!UICONTROL Modélisation des données]**, **[!UICONTROL Data Management]**, **[!UICONTROL Gestion des Profils]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Surveillance des données]**, **[!UICONTROL Administration Sandbox]**, **[!UICONTROL Destinations&lt;a**[!UICONTROL  Ingestion des données ]**,**[!UICONTROL  Data Science Workspace ]**,**[!UICONTROL  Requête Service ]**et**[!UICONTROL  Data Governance ]**.]** |
| Accès aux environnements de test | L’onglet **[!UICONTROL Autorisations]** d’un profil de produit peut accorder aux utilisateurs l’accès à des environnements de test spécifiques. [!DNL Platform] Consultez la section sur les [environnements de test](#sandboxes) ci-dessous pour plus d’informations. |

Pour plus d’informations, consultez la [présentation du contrôle d’accès](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] est un service d’applications intégré à  [!DNL Experience Platform]. Il vous permet de tirer parti de [!DNL Platform] pour offrir à vos clients la meilleure offre et la meilleure expérience sur tous les points de contact au bon moment.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Bibliothèque d’offres centralisée | Interface dans laquelle vous créez et gérez les différents éléments qui composent vos offres, et définissez leurs règles et contraintes. |
| Moteur de décision Offre | Le moteur de décision d&#39;Offre utilise [!DNL Platform] données et [!DNL Real-time Customer Profiles], ainsi que la bibliothèque d&#39;Offres, pour sélectionner le moment, les clients et les canaux appropriés pour la livraison des offres. |

Pour plus d&#39;informations, consultez la documentation [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=fr).

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] est conçu pour enrichir les applications d’expérience numérique à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience numérique en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, [!DNL Experience Platform] fournit des sandbox qui partitionnent une instance [!DNL Platform] unique en environnements virtuels distincts pour aider à développer et à développer des applications d&#39;expérience numérique.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Environnement de test de production | [!DNL Experience Platform] fournit un environnement de test de production unique, qui ne peut pas être supprimé ou réinitialisé. Le nombre total de sandbox disponibles, production et non-production, est déterminé par la licence acquise. |
| Environnement de test hors production | Vous pouvez créer plusieurs sandbox hors production pour une seule instance [!DNL Platform], ce qui vous permet de tester des fonctionnalités, d&#39;exécuter des expériences et de créer des configurations personnalisées sans affecter votre sandbox de production. |
| Sélecteur d’environnement de test | Dans l&#39;interface utilisateur [!DNL Experience Platform], le sélecteur de sandbox situé dans le coin supérieur gauche de l&#39;écran vous permet de passer d&#39;un sandbox disponible à un autre par le biais d&#39;un menu déroulant. Le sélecteur de sandbox fournit également une fonction de recherche qui vous permet de filtrer les sandbox disponibles. |
| En-tête `x-sandbox-name` | Tous les appels aux API [!DNL Experience Platform] doivent désormais inclure le nouvel en-tête `x-sandbox-name`, dont la valeur fait référence à l&#39;attribut `name` du sandbox dans lequel l&#39;opération aura lieu. |

Pour plus d’informations, consultez la [présentation des environnements de test](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, de transformer et de valider des données à partir du modèle de données d’expérience (XDM).

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Opérations itératives | [!DNL Data Prep] Mapper prend désormais en charge les opérations itératives sur une hiérarchie. |
| Mapper, fonction | [!DNL Data Prep] Le mappeur peut désormais  **** ne pas copier un attribut de la source vers la cible XDM. |

Pour plus d’informations, reportez-vous à la [[!DNL Data Prep] présentation des ](../../data-prep/home.md).

## Data Science Workspace {#dsw}

Data Science Workspace utilise l’apprentissage automatique et l’intelligence artificielle pour créer des informations à partir de vos données. Intégré à Adobe Experience Platform, Data Science Workspace vous aide à obtenir des prévisions en utilisant votre contenu et des ressources de données de l’ensemble des solutions Adobe. L&#39;une des façons d&#39;atteindre cet objectif est d&#39;utiliser [!DNL JupyterLab]. [!DNL JupyterLab] est une interface utilisateur web pour [[!DNL Project Jupyter]](https://jupyter.org/) et est étroitement intégré à Adobe Experience Platform. Il fournit un environnement de développement interactif pour que les chercheurs en données puissent travailler avec des blocs-notes, du code et des données [!DNL Jupyter].

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| [!DNL JupyterLab] Modèle Créateur de recettes | Mise à jour de l&#39;utilisation et des versions du bloc-notes pour déterminer les exigences de la recette. [!DNL Python] L&#39;image de base d&#39;exécution ML a été mise à jour pour utiliser  [!DNL Python] 3.6.7 et un  [!DNL Conda] environnement exclusivement. |

Pour plus d&#39;informations, veuillez lire le document sur [la création d&#39;une recette à l&#39;aide de Jupyter Notebooks](../../data-science-workspace/jupyterlab/create-a-recipe.md).

## [!DNL Destinations] Service {#destinations}

Dans [Plate-forme de données client en temps réel](../../rtcdp/overview.md), les destinations sont des intégrations préétablies avec les plateformes de destination qui activent les données à ces partenaires de manière transparente.

**Nouvelles destinations**

| Destination | Description |
| ----------- | ----------- |
| Braquer | Braze est une plate-forme d&#39;engagement client complète qui permet d&#39;offrir des expériences pertinentes et mémorables entre les clients et les marques qu&#39;ils aiment. |
| Microsoft Bing | La destination Microsoft Bing vous permet d’exécuter des campagnes numériques ciblées de reciblage et d’audience dans Microsoft Display Advertising. |
| Le bureau de commerce | Le Trade Desk est une plate-forme en libre-service permettant aux acheteurs d’annonces publicitaires d’exécuter des reciblages et d’audience de campagnes numériques ciblées à l’échelle de l’affichage, de la vidéo et des sources d’inventaire mobiles. |

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mises à jour de l&#39;UX des détails de destination | Le flux de travaux de destination du CDP en temps réel comprend désormais une surveillance intégrée afin que vous puissiez identifier les activations de lot qui ont réussi. Cette fonctionnalité permet aux utilisateurs de résoudre directement les problèmes dans le flux de travaux pour les destinations par lots au moyen d’alertes et d’un tableau de bord de surveillance afin de suivre les erreurs dans le pipeline de traitement. |
| Chiffrement de fichier | Pour les destinations basées sur des fichiers, les utilisateurs peuvent désormais ajouter un chiffrement à leurs fichiers exportés. |
| Planification des fichiers | Pour les destinations d’enregistrement basées sur le courrier électronique et le cloud, les utilisateurs peuvent créer une exportation unique ou créer des instantanés quotidiens. |
| Champs obligatoires | Les utilisateurs peuvent marquer les champs comme obligatoires, en s’assurant que seuls les champs qui contiennent le champ obligatoire sont exportés. |

Pour plus d’informations, reportez-vous à la [présentation des destinations](../../destinations/home.md).

## Intelligent Services {#intelligent-services}

Intelligent Services permet aux analystes et spécialistes du marketing d’exploiter la puissance de l’intelligence artificielle et de l’apprentissage automatique dans les cas d’utilisation de l’expérience client. Les analystes marketing peuvent obtenir des prédictions spécifiques aux besoins d’une entreprise en utilisant des configurations au niveau de l’entreprise sans avoir besoin d’expertise en sciences des données.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Jeu de données des Événements d’expérience client (CEE) | La création d’un jeu de données CEE prend désormais en charge l’ajout de champs d’identité au jeu de données avec l’éditeur de Schéma. Attribution AI et l’API client utilisent l’identité Principale pour combiner des événements. |

Pour plus d&#39;informations, consultez la section [Ajout de champs d&#39;identité à un jeu de données](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) dans le guide de préparation des données Intelligent Services.

### Attribution AI

Dans le cadre d’Intelligent Services, Attribution AI est un service d’attribution algorithmique à plusieurs canaux qui calcule l’influence et l’impact incrémentiel des interactions des clients par rapport à des résultats spécifiés.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Lien de source de données | Le lien vers la source du jeu de données d’origine peut être affiché et parcouru à partir du rail droit d’une instance de service sélectionnée. |
| Modifier le nom d’instance | Vous pouvez désormais modifier le nom d’une instance d’Attribution AI existante. |
| Instance de clonage | Copie la configuration de l’instance de service actuellement sélectionnée et autorise les modifications. |
| Modification des paramètres de configuration d’instance | Vous pouvez désormais modifier la configuration d’une instance d’Attribution AI existante si elle n’a pas encore commencé à obtenir un score. |
| Un score unique | Vous pouvez désormais déclencher un score de modèle ad hoc dans vos instances Attribution AI. |
| Transférer les colonnes | Vous pouvez maintenant configurer d&#39;autres colonnes qui seront ajoutées aux fichiers de note de sortie brute pour ajouter des dimensions supplémentaires aux vues d&#39;outils BI. |
| Activation et désactivation des instances | Vous pouvez désormais activer et désactiver la formation planifiée sur les modèles et le score de vos instances Attribution AI. |
| Suivi des droits | Vous pouvez trouver la quantité totale d’informations d’attribution utilisées par votre compte dans le conteneur d’instance de création. |
| Ventilation des points de contact par position | Un nouveau graphique d’informations qui fournit une analyse des points de contact par position de chemin de conversion. |
| Principaux chemins de conversion | Un nouveau graphique d’informations situé dans l’onglet Analyse de chemin. Le graphique contient une liste des cinq principaux chemins de conversion montrant la séquence des points de contact du canal marketing qui ont généré le plus de conversions. |
| Efficacité des points de contact | Fournit des informations détaillées sur les trois variables les plus importantes par lesquelles votre modèle mesure l’efficacité des points de contact. Les variables sont le ratio des chemins positifs et négatifs touchés, l’efficacité du point de contact et le volume du point de contact. |

Pour plus d&#39;informations, veuillez lire [Attribution AI overview](../../intelligent-services/attribution-ai/overview.md).

### Customer AI

En tant que composant des services intelligents, Customer AI permet aux professionnel du marketing de générer des prédictions client au niveau individuel avec des explications. À l’aide de facteurs d’influence, Customer AI peut vous indiquer ce qu’un client est susceptible de faire et pourquoi. De plus, les professionnels du marketing peuvent tirer parti des prédictions et des informations de Customer AI pour personnaliser les expériences client en diffusant les offres et les messages les plus appropriés.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Lien de source de données | Le lien vers la source du jeu de données d’origine peut être affiché et parcouru à partir du rail droit d’une instance de service sélectionnée. |
| Modifier le nom d’instance | Vous pouvez modifier le nom d’une instance d’API cliente existante. |
| Modification des paramètres de configuration d’instance | Vous pouvez désormais modifier la configuration d’une instance d’IA de client existante si elle n’a pas encore démarré une notation. |
| Instance de clonage | Copie la configuration de l’instance de service actuellement sélectionnée et autorise les modifications. |
| Suivi des droits | Vous pouvez trouver le nombre total de profils marqués par l’IA du client pour votre compte dans le conteneur d’instance de création. |
| Objectif de prévision | La souplesse de création d&#39;un objectif de prédiction a été augmentée avec de nouvelles options pour prévoir si quelque chose &quot;se produira&quot; ou &quot;ne se produira pas&quot;. En outre, les options permettant de prévoir si &quot;tous&quot; les événements se produisent ou si &quot;n’importe lequel&quot; des événements se produit lorsque plusieurs événements sont utilisés ont été ajoutées. |
| Effet d&#39;entraînement des facteurs influents | Les groupes de facteurs influents les plus importants de propension contiennent maintenant des forages. Les listes déroulantes constituent un récapitulatif plus détaillé des valeurs pour chacun des principaux facteurs influents d’une catégorie de propension. |

Pour plus d&#39;informations, veuillez lire [Présentation de l&#39;IA client](../../intelligent-services/customer-ai/overview.md).

## Real-time Customer Profile {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Real-time Customer Profile offre une vue d’ensemble de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. [!DNL Profile] vous permet de consolider vos données client disparates en une vue unifiée offrant un compte d’activité horodaté de chaque interaction client.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Processus des stratégies de fusion mis à jour | La plate-forme a mis à niveau la configuration de la stratégie de fusion vers un nouveau processus par étapes. Ce processus permet aux utilisateurs de rassembler des fragments de données provenant de plusieurs jeux de données de Profil et de définir la priorité de la fusion des données entre ces jeux de données afin de créer une vue complète de chaque individu. Les utilisateurs peuvent fusionner des jeux de données de Profil individuels XDM sélectionnés en sélectionnant la méthode de fusion appropriée (horodatage ordonné ou ordre de priorité des jeux de données) et en ajoutant des jeux de données ExperienceEvent aux jeux de données de Profil. |
| Vue schéma Union | Dans l’interface utilisateur de l’Experience Platform, les utilisateurs peuvent plus facilement trouver des informations concernant tous les schémas et jeux de données contribuant au schéma d’union, ainsi que des attributs de surface clés tels que les champs d’identité et de relation. Ces mises à jour permettent de résoudre les problèmes et de vérifier que les profils sont correctement configurés, que les identités sont correctement assemblées et que les données ont été correctement ingérées. |

Pour plus d&#39;informations sur le Profil client en temps réel, y compris des didacticiels et les meilleures pratiques pour utiliser les données [!DNL Profile], consultez la [Présentation du Profil client en temps réel](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services [!DNL Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les logiciels tiers et le système de gestion de la relation client.

[!DNL Experience Platform] fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Nouvelles sources**

| Fonctionnalité | Description |
| ------- | ----------- |
| [!DNL Shopify] | Vous pouvez désormais vous connecter à [!DNL Shopify] à [!DNL Experience Platform] à l&#39;aide de l&#39;API [!DNL Flow Service] ou de l&#39;interface utilisateur. Pour plus d&#39;informations, consultez la section [Présentation du connecteur Shopify](../../sources/connectors/ecommerce/shopify.md). |

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mettre à jour les informations de connexion | Vous pouvez désormais mettre à jour les noms, descriptions et informations d’identification des connexions par lot existantes à l’aide de l’API [!DNL Flow Service] et de l’interface utilisateur. Pour plus d&#39;informations, consultez le didacticiel sur la [mise à jour des connexions à l&#39;aide de l&#39;API Flow Service](../../sources/tutorials/api/update.md) et [modification des détails du compte à l&#39;aide de l&#39;interface utilisateur](../../sources/tutorials/ui/monitor.md). |
| Suppression des connexions | Les connexions par lots contenant des erreurs ou devenues inutiles peuvent maintenant être supprimées à l&#39;aide de l&#39;API [!DNL Flow Service] et de l&#39;interface utilisateur. Pour plus d&#39;informations, consultez le didacticiel sur la suppression de connexions à l&#39;aide de l&#39;API Flow Service](../../sources/tutorials/api/delete.md) et [suppression de comptes à l&#39;aide de l&#39;interface utilisateur](../../sources/tutorials/ui/delete-accounts.md).[ |
| Mappage hiérarchique | Vous pouvez prévisualisation un fichier source hiérarchique, tel que JSON ou Parquet, pendant le processus d’assimilation des données. Pour plus d’informations, consultez le didacticiel sur la [configuration d’un flux de données pour les connecteurs d’enregistrement cloud dans l’interface utilisateur](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |
| Prise en charge des API pour le mappage dans les sources de diffusion en continu | Vous pouvez désormais utiliser des API pour exécuter des fonctions de mappage avec des sources de diffusion en continu. |
| Prise en charge des API pour les délimiteurs personnalisés pour les sources d’enregistrement cloud | Vous pouvez désormais collecter des fichiers délimités par des CSV à l’aide de sources d’enregistrement cloud. Vous pouvez utiliser n’importe quel délimiteur de colonne unique, tel qu’une tabulation, une virgule, une barre verticale, un point-virgule ou un hachage, pour collecter des fichiers plats dans n’importe quel format. |
| Prise en charge de sandbox pour Adobe Audience Manager Connector | Le connecteur d&#39;Audience Manager est maintenant compatible avec le sandbox. Les utilisateurs peuvent activer le connecteur pour acheminer les jeux de données d’Audience Manager vers le sandbox de leur choix (y compris les sandbox hors production). La configuration est limitée à un sandbox par organisation IMS. |
| Améliorations de l&#39;environnement | L’assimilation basée sur des fichiers est désormais accessible via le catalogue des sources. |

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).