---
title: Notes de mise à jour d’Adobe Experience Platform - Janvier 2026
description: Notes de mise à jour de janvier 2026 pour Adobe Experience Platform.
source-git-commit: 436e65f22b8866fb9922afcf51811f537c05fc9f
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 21%

---


# Notes de mise à jour d’Adobe Experience Platform

>[!TIP]
>
>Reportez-vous à la documentation suivante pour les notes de mise à jour des autres applications Adobe Experience Platform :
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/fr/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/fr/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/fr/docs/analytics-platform/using/releases/pre-release-notes)
>- [Composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/e-release-notes)
>- [Collaboration dans Real-Time CDP](https://experienceleague.adobe.com/fr/docs/real-time-cdp-collaboration/using/latest)

**Date de publication : mercredi 27 janvier 2026**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

<!-- - [Agent Orchestrator](#agent-orchestrator) -->

- [Destinations](#destinations)
- [Profil client en temps réel](#real-time-customer-profile)
- [Schémas](#schemas)
- [Service de segmentation](#segmentation-service)
- [Sources](#sources)

<!-- ## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator enables you to build and deploy AI-powered agents that can automate workflows and interact with customers across multiple channels.

**New or updated features**

| Feature | Description |
| --- | --- |
| Trial motion for Adobe Experience Platform Agents | **Select customers now have access to Adobe Experience Platform Agents for a complimentary trial**, enabling them to explore and interact with these Agents through the AI Assistant interface powered by Adobe Experience Platform Agent Orchestrator. The trial offers hands-on experience with AI Agents that operate within the context of customers' existing Experience Cloud products and environments, allowing teams to evaluate value before committing to a full purchase. Adobe Experience Platform Agents are guided by user input and oversight and respect existing product-level access controls, ensuring users can only perform actions or view data for which they are authorized within the underlying Experience Cloud applications.|

{style="table-layout:auto"}

For more information, see the [Agent Orchestrator documentation](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator). -->

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Destination | Description |
| --- | --- |
| Connecteur [Destination de niveau](/help/destinations/catalog/advertising/kevel.md) désormais disponible | La destination de diffusion en continu [!DNL Kevel] pour Adobe Experience Platform permet aux clients d’activer les audiences Adobe directement dans la base de données des utilisateurs d’[!DNL Kevel] et les API de gestion des segments afin de prendre en charge le ciblage en temps réel au moment de la décision de publicité. [[!DNL Kevel]](https://www.kevel.com/) fournit la technologie activée par l’IA et des conseils d’experts qui aident les leaders du commerce innovants à lancer, développer et réussir dans les médias de détail. [!DNL Kevel]’s Retail Media Cloud optimise les formats publicitaires ciblés, attribuables et personnalisables pour la publicité sur site et hors site. |
| Connecteur [Destination Exchange d’index](/help/destinations/catalog/advertising/index-exchange.md) désormais disponible | Utilisez ce connecteur de destination pour exporter des segments d’audience de Adobe Experience Platform directement vers la plateforme de publicité programmatique d’[!DNL Index Exchange]. [!DNL Index] est une plateforme publicitaire mondiale axée sur l’offre qui aide les propriétaires de médias à maximiser la valeur de leur contenu sur chaque écran. Fort de plus de 20 ans de leadership dans le secteur, [!DNL Index] met en relation les plus grandes marques du monde avec des créateurs d’expériences haut de gamme afin de proposer des expériences client de haute qualité. |
| Prise en charge des points d’entrée régionaux pour les connexions Braze | Tous les points d’entrée [spécifiques à une région](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) pris en charge par [!DNL Braze] peuvent désormais être sélectionnés pendant le flux de configuration de destination. Demandez à votre représentant [!DNL Braze] quelle instance de point d’entrée vous devez utiliser. |
| Prise en charge de la planification hebdomadaire et mensuelle pour l’intégration [Liveramp](../../destinations/catalog/advertising/liveramp-onboarding.md#scheduling) | Vous pouvez désormais configurer des plannings d’exportation hebdomadaires et mensuels pour la destination d’intégration Liveramp. <br> Cette version est déployée progressivement et sera terminée d’ici le 30 janvier. |
| Expérience d’activation améliorée pour les destinations [The Trade Desk](../../destinations/catalog/advertising/tradedesk.md) et [Microsoft Bing](../../destinations/catalog/advertising/bing.md) | Les destinations Trade Desk et Microsoft Bing incluent désormais des mappages obligatoires prédéfinis pour une expérience d’activation optimisée.  <br> Cette version est déployée progressivement et sera terminée d’ici le 30 janvier. |
| Prise en charge du chiffrement AES256 pour les destinations [Amazon S3](../../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) | Vous pouvez désormais configurer le chiffrement AES256 pour vos exportations Amazon S3. Deux options sont disponibles : <ul><li>**[!UICONTROL Default]** : les données seront chiffrées au repos avec l’algorithme de chiffrement par défaut défini sur votre compartiment.</li><li>**[!UICONTROL SSE-S3/AES256]** : Experience Platform ajoute l’en-tête `s3:x-amz-server-side-encryption": "AES256` dans l’exportation et les données seront chiffrées au repos avec l’algorithme AES256 lorsqu’elles arrivent dans S3. **Cette option est prioritaire sur tout algorithme de chiffrement par défaut configuré sur votre compartiment S3**.</li></ul> Cette version est déployée progressivement et sera terminée d’ici le 30 janvier. |
| Prise en charge de l’activation des numéros de téléphone pour la connexion [ The Trade Desk - CRM ](../../destinations/catalog/advertising/tradedesk-emails.md#phone-hashing) | La destination Trade Desk - CRM prend désormais en charge l’activation des numéros de téléphone en plus des adresses e-mail. Vous pouvez activer les numéros de téléphone non hachés au format E.164 et les numéros de téléphone hachés (format SHA256_E.164) sur votre compte Trade Desk pour le ciblage et la suppression d’audiences en fonction des données CRM. Les numéros de téléphone doivent être normalisés au format E.164 avant activation. |

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mise à jour des limites du mécanisme de sécurisation pour les destinations [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | Le nombre maximal d’audiences pouvant être mappées à une seule destination Adobe Target est passé de 50 à 250. Cela aligne Adobe Target sur la limite d’audience standard pour d’autres destinations, offrant ainsi une plus grande flexibilité pour les workflows d’activation des audiences. Vous pouvez désormais activer davantage d’audiences vers les destinations Adobe Target sans avoir à créer plusieurs flux de données. |
| [Modifier les destinations](/help/destinations/ui/edit-destination.md) et [modifier les actions marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) disponibilité générale | L’option permettant de modifier les destinations et les actions marketing est désormais disponible pour tous les utilisateurs et utilisatrices. |
| Activez/désactivez les noms d’affichage des champs dans l’[ Mappage ](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) | Lors du mappage des champs de schéma à une destination, vous pouvez désormais basculer entre l’affichage du nom complet du champ XDM et l’affichage uniquement du nom d’affichage. <br> ![Enregistrement d’écran affichant le bouton bascule du nom d’affichage.](/help/release-notes/2026/assets/january/show-display-names.gif) |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [vue d’ensemble des destinations](../../destinations/home.md).

## Profil client en temps réel {#real-time-customer-profile}

Le profil client en temps réel offre une vue d’ensemble de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| [Capacité de diffusion en continu](/help/landing/license-usage-and-guardrails/capacity.md) application | Experience Platform applique désormais les capacités de débit en flux continu pour le profil client en temps réel et le service d’identités. Lorsque les clients dépassent leur capacité de diffusion en continu convenue, les données sont placées en file d’attente et traitées selon le principe du premier entré, premier sorti. Cela garantit des performances système prévisibles et empêche les violations de capacité d’avoir un impact sur la qualité de l’ingestion des données. Remarques importantes : <ul><li>Les upserts en flux continu ne seront pas disponibles sur le lac de données lorsque la capacité est dépassée</li><li>Cette application ne s’applique pas aux clients disposant de licences Adobe Journey Optimizer</li><li>Les données placées en file d’attente seront traitées de manière séquentielle une fois que la capacité sera disponible.</li></ul> Pour plus d’informations, consultez la [présentation de la capacité](/help/landing/license-usage-and-guardrails/capacity.md). |
| Obsolescence de la recherche d’entité | L’utilisation de l’API de recherche d’entité pour les événements d’expérience est désormais obsolète pour tous les clients Real-Time CDP Prime. Cette obsolescence permet d’aligner Real-Time CDP sur les fonctionnalités de licence. Les clients Real-Time CDP Ultimate qui ont l’intention d’utiliser cette fonctionnalité peuvent contacter l’assistance clientèle d’Adobe pour réactiver cette fonctionnalité.  Pour plus d’informations, consultez le guide de l’API [entities](/help/profile/api/entities.md). |
| Surveiller le statut de la tâche d’ingestion de profil | Vous pouvez désormais surveiller le pourcentage de progression au niveau de la tâche pour les exécutions de flux de données d’ingestion de profils par lots. Cette fonctionnalité offre une visibilité en temps réel sur la progression actuelle des traitements d’ingestion par lots, y compris des points de contrôle critiques qui indiquent si l’ingestion est prête pour la segmentation client et les recherches Adobe Journey Optimizer. Pour les ingestions volumineuses dont le traitement peut prendre plusieurs heures, cette transparence de progression vous aide à comprendre si le traitement progresse normalement ou rencontre des problèmes, ce qui réduit l’incertitude pendant le traitement des données. Pour plus d’informations, consultez le guide [surveiller les profils](/help/dataflows/ui/monitor-profiles.md). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [[!DNL Real-Time Customer Profile] vue d’ensemble](../../profile/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Actualisation de l’expiration des données d’audience externe | Les audiences externes (telles que les chargements de fichiers CSV) prennent désormais en charge une fonctionnalité d’actualisation forcée pour les paramètres d’expiration des données. Cette fonctionnalité permet aux utilisateurs d’actualiser manuellement l’expiration des données pour les audiences externes, offrant ainsi un meilleur contrôle sur la gestion du cycle de vie des audiences. Cela s’avère particulièrement utile pour les audiences qui doivent persister au-delà de leur période d’expiration initiale des données ou qui nécessitent une réactivation sans télécharger à nouveau les données. Pour plus d’informations sur cette fonctionnalité, consultez la [présentation d’Audience Portal](../../segmentation/ui/audience-portal.md#audience-summary). |

Pour plus d’informations, consultez la [[!DNL Segmentation Service] vue d’ensemble](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Sources nouvelles ou mises à jour**

| Source | Description |
| --- | --- |
| Source [[!DNL Oracle Eloqua]](/help/sources/connectors/marketing-automation/eloqua.md) V2 | Un nouveau connecteur source [!DNL Oracle Eloqua] est désormais disponible, remplaçant le [connecteur obsolète](/help/sources/connectors/marketing-automation/oracle-eloqua.md). Ce connecteur mis à jour offre des fonctionnalités améliorées et une fiabilité améliorée pour l’ingestion de données à partir de [!DNL Oracle Eloqua] dans Experience Platform. Les clients qui utilisent le connecteur existant doivent migrer vers la nouvelle mise en œuvre, car les connexions existantes ne fonctionneront plus. Le nouveau connecteur prend en charge toutes les étapes d’installation et de configuration nécessaires pour se connecter à [!DNL Oracle Eloqua] et ingérer des données d’automatisation du marketing. |
| Source [[!DNL Salesforce Marketing Cloud]](/help/sources/connectors/marketing-automation/sfmc.md) V2 | Un nouveau connecteur source [!DNL Salesforce Marketing Cloud] est désormais disponible, remplaçant le [connecteur obsolète](/help/sources/connectors/marketing-automation/salesforce-marketing-cloud.md). Ce connecteur mis à jour offre des performances améliorées et des fonctionnalités supplémentaires pour l’ingestion de données à partir de [!DNL Salesforce Marketing Cloud] dans Experience Platform. Les clients qui utilisent le connecteur existant doivent passer à la nouvelle mise en œuvre. Le nouveau connecteur comprend des instructions de configuration complètes pour la connexion à [!DNL Salesforce Marketing Cloud] et l’ingestion de données d’automatisation du marketing. |

Pour plus d’informations, consultez la [vue d’ensemble des sources](../../sources/home.md).

