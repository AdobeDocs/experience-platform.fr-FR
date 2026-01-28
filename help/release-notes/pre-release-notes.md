---
title: Notes de mise à jour préliminaires d’Experience Platform
description: Aperçu des dernières notes de mise à jour de Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: 6fa71c48151e937f2e18d8b9761aad94eca85ade
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 23%

---

# Notes de mise à jour préliminaires de Adobe Experience Platform

>[!IMPORTANT]
>
>Ce document est conçu comme un **aperçu** des notes de mise à jour du mois en cours. Les éléments de version peuvent faire l’objet de modifications et peuvent être ajoutés ou supprimés dans la version finale.

>[!TIP]
>
>Reportez-vous à la documentation suivante pour les notes de mise à jour des autres applications Adobe Experience Platform :
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/fr/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/e-release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de publication : janvier 2026**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Agent Orchestrator](#agent-orchestrator)
- [Destinations](#destinations)
- [Profil client en temps réel](#real-time-customer-profile)
- [Schémas](#schemas)
- [Service de segmentation](#segmentation-service)
- [Sources](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator vous permet de créer et de déployer des agents optimisés par l’IA qui peuvent automatiser les workflows et interagir avec les clients sur plusieurs canaux.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Requête d’essai pour Agent Orchestrator | Agent Orchestrator propose désormais une version d’essai, qui permet aux clients d’explorer et de tester le service avant de s’engager à effectuer un achat complet. Cette option d’essai avant achat permet aux entreprises d’évaluer les fonctionnalités d’Agent Orchestrator, y compris les compétences et les fonctionnalités d’orchestration, dans leur propre environnement. L’essai offre une expérience pratique dans la création d’agents optimisés par l’IA et la compréhension de la manière dont ils peuvent être intégrés dans les workflows existants. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [documentation d’Agent Orchestrator](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Destination | Description |
| --- | --- |
| Connecteur de destination de niveau désormais disponible | [[!DNL Kevel]](https://www.kevel.com/) fournit la technologie activée par l’IA et des conseils d’experts qui aident les leaders du commerce innovants à lancer, développer et réussir dans les médias de détail. [!DNL Kevel]’s Retail Media Cloud optimise les formats publicitaires ciblés, attribuables et personnalisables pour la publicité sur site et hors site. |
| Connecteur de destination Exchange d’index désormais disponible | [!DNL Index] est une plateforme publicitaire mondiale axée sur l’offre qui aide les propriétaires de médias à maximiser la valeur de leur contenu sur chaque écran. Fort de plus de 20 ans de leadership dans le secteur, [!DNL Index] met en relation les plus grandes marques du monde avec des créateurs d’expériences haut de gamme afin de proposer des expériences client de haute qualité. |
| Prise en charge des points d’entrée régionaux pour les connexions Braze | Tous les points d’entrée [spécifiques à une région](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) pris en charge par [!DNL Braze] peuvent désormais être sélectionnés pendant le flux de configuration de destination. Demandez à votre représentant [!DNL Braze] quelle instance de point d’entrée vous devez utiliser. |
| Prise en charge de la planification hebdomadaire et mensuelle pour l’intégration Liveramp | Vous pouvez désormais configurer des plannings d’exportation hebdomadaires et mensuels pour la destination d’intégration Liveramp. |
| Prise en charge du chiffrement AES256 pour les destinations Amazon S3 | Vous pouvez désormais configurer le chiffrement AES256 pour vos exportations Amazon S3. |
| Expérience d’activation améliorée pour les destinations The Trade Desk et Microsoft Bing | Les destinations Trade Desk et Microsoft Bing incluent désormais des mappages obligatoires prédéfinis pour une expérience d’activation optimisée. |

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mise à jour des limites du mécanisme de sécurisation pour la destination Adobe Target | Le nombre maximal d’audiences pouvant être mappées à une seule destination Adobe Target est passé de 50 à 250. Cela aligne Adobe Target sur la limite d’audience standard pour d’autres destinations, offrant ainsi une plus grande flexibilité pour les workflows d’activation des audiences. Vous pouvez désormais activer davantage d’audiences vers les destinations Adobe Target sans avoir à créer plusieurs flux de données. |
| [Modifier les destinations](/help/destinations/ui/edit-destination.md) et [modifier les actions marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) disponibilité générale | L’option permettant de modifier les destinations et les actions marketing est désormais disponible pour tous les utilisateurs et utilisatrices. |
| Activer/désactiver le nom d’affichage des champs à l’étape Mappage | Lors du mappage des champs de schéma à une destination, vous pouvez désormais basculer entre l’affichage du nom complet du champ XDM et l’affichage uniquement du nom d’affichage. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des destinations](../destinations/home.md).

## Profil client en temps réel {#real-time-customer-profile}

Le profil client en temps réel offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Application de la capacité de diffusion en continu | Experience Platform applique désormais les capacités de débit en flux continu pour le profil client en temps réel et le service d’identités. Lorsque les clients dépassent leur capacité de diffusion en continu convenue, les données sont placées en file d’attente et traitées selon le principe du premier entré, premier sorti. Cela garantit des performances système prévisibles et empêche les violations de capacité d’avoir un impact sur la qualité de l’ingestion des données. Remarques importantes : les upserts en flux continu ne seront pas disponibles sur le lac de données lorsque la capacité est dépassée. Cette application ne s’applique pas aux clients disposant de licences Adobe Journey Optimizer et les données placées en file d’attente seront traitées de manière séquentielle une fois que la capacité sera disponible. |
| Obsolescence de l’accès à l’API pour Real-Time CDP Prime | L’accès aux API pour les événements d’expérience est désormais obsolète pour tous les clients Real-Time CDP Prime. Cette modification affecte la possibilité d’interroger les événements d’expérience directement via l’API. Les clients Real-Time CDP Ultimate peuvent demander une exception par le biais d’un processus d’exception formel pour activer l’accès à l’API des événements d’expérience, si nécessaire, pour leurs cas d’utilisation. Cette obsolescence permet d’aligner Real-Time CDP sur les fonctionnalités de licence. |
| Surveillance de l’exécution du flux de données | Vous pouvez désormais surveiller la progression et la préparation des exécutions de flux de données dans Profile. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [[!DNL Real-Time Customer Profile] vue d’ensemble](../profile/home.md).

## Schémas {#schemas}

Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit. Les schémas sont composés d’une classe de base et de zéro ou plusieurs groupes de champs de schéma.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Modernisation de l’inventaire des schémas avec la recherche, le filtre, les balises et les dossiers | Modernisation de la page de navigation des schémas afin d’améliorer les fonctionnalités d’organisation et de découverte. Les nouvelles fonctionnalités comprennent des options de recherche et de filtrage avancées, la prise en charge de balises et de dossiers générés par l’utilisateur pour organiser les schémas, ainsi que des actions intégrées pour rationaliser les workflows. Les principales améliorations incluent : des colonnes mises à jour (nom, classe, jeux de données, identités, relations, activer pour le profil, comportement, type de schéma, balises, date de création, dernière modification), des filtres avancés (afficher les profils, type de schéma, classe, a une balise, créé par, date de création, date de modification, a une identité principale, a une relation, espace de noms d’identité de Principal), des actions intégrées (modifier, supprimer, appliquer des libellés, créer un jeu de données pour les schémas non relationnels, gérer les balises, déplacer vers un dossier, ajouter au package, copier la structure JSON, télécharger un fichier d’exemple) et la possibilité d’organiser les schémas à l’aide de balises et de dossiers. Ces améliorations offrent une visibilité complète sur les ressources de schéma et permettent une gestion plus efficace des schémas au niveau du sandbox. |

Pour plus d’informations, consultez la [[!DNL Schemas] vue d’ensemble](../xdm/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Actualisation de la TTL de l’audience externe | Les audiences externes (telles que les chargements de fichiers CSV) prennent désormais en charge une fonctionnalité d’actualisation forcée pour les paramètres de durée de vie (TTL). Cette fonctionnalité permet aux utilisateurs d’actualiser manuellement l’expiration de la TTL pour les audiences externes, offrant ainsi un meilleur contrôle sur la gestion du cycle de vie des audiences. Cela s’avère particulièrement utile pour les audiences qui doivent persister au-delà de leur période de TTL initiale ou qui nécessitent une réactivation sans charger à nouveau les données. |

Pour plus d’informations, consultez la [[!DNL Segmentation Service] vue d’ensemble](../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Sources nouvelles ou mises à jour**

| Source | Description |
| --- | --- |
| Source [!DNL Oracle Eloqua] V2 | Un nouveau connecteur source [!DNL Oracle Eloqua] est désormais disponible, remplaçant le connecteur obsolète. Ce connecteur mis à jour offre des fonctionnalités améliorées et une fiabilité améliorée pour l’ingestion de données à partir de [!DNL Oracle Eloqua] dans Experience Platform. Les clients qui utilisent le connecteur existant doivent migrer vers la nouvelle mise en œuvre, car les connexions existantes ne fonctionneront plus. Le nouveau connecteur prend en charge toutes les étapes d’installation et de configuration nécessaires pour se connecter à [!DNL Oracle Eloqua] et ingérer des données d’automatisation du marketing. |
| Source [!DNL Salesforce Marketing Cloud] V2 | Un nouveau connecteur source [!DNL Salesforce Marketing Cloud] est désormais disponible, remplaçant le connecteur obsolète. Ce connecteur mis à jour offre des performances améliorées et des fonctionnalités supplémentaires pour l’ingestion de données à partir de [!DNL Salesforce Marketing Cloud] dans Experience Platform. Les clients qui utilisent le connecteur existant doivent passer à la nouvelle mise en œuvre. Le nouveau connecteur comprend des instructions de configuration complètes pour la connexion à [!DNL Salesforce Marketing Cloud] et l’ingestion de données d’automatisation du marketing. |

Pour plus d’informations, consultez la [vue d’ensemble des sources](../sources/home.md).

