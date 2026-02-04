---
title: Notes de mise à jour d’Adobe Experience Platform - Janvier 2026
description: Notes de mise à jour de janvier 2026 pour Adobe Experience Platform.
source-git-commit: 1761acbcab12acf1596daf5461476d5b91bb0e9b
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 22%

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
| Essai des agents Adobe Experience Platform lié à l’utilisation | **Certains clients bénéficient désormais d’un accès gratuit à titre d’essai aux agents Adobe Experience Platform**. Vous pouvez utiliser la version d&#39;évaluation pour explorer les agents et interagir avec eux par le biais de l&#39;interface de l&#39;assistant AI optimisée par Adobe Experience Platform Agent Orchestrator. L’essai offre une expérience pratique avec des agents d’IA qui fonctionnent dans le cadre des produits et environnements Experience Cloud existants des clients, ce qui permet aux équipes d’évaluer la valeur avant de s’engager à effectuer un achat complet. Les agents Adobe Experience Platform sont guidés par les entrées et la supervision des utilisateurs et respectent les contrôles d’accès existants au niveau du produit, ce qui garantit que les utilisateurs et utilisatrices ne peuvent effectuer que des actions ou afficher des données pour lesquelles ils sont autorisés dans les applications Experience Cloud sous-jacentes. Lisez la présentation de l’essai lié à l’utilisation des agents Experience Platform [&#128279;](https://experienceleague.adobe.com/en/docs/experience-cloud-ai/experience-cloud-ai/agents/trial) pour plus d’informations sur la prise en main. |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [documentation d’Agent Orchestrator](https://experienceleague.adobe.com/fr/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Destination | Description |
| --- | --- |
| Connecteur [Destination de niveau](/help/destinations/catalog/advertising/kevel.md) désormais disponible | La destination de diffusion en continu [!DNL Kevel] pour Adobe Experience Platform permet aux clients d’activer les audiences Adobe directement dans la base de données des utilisateurs d’[!DNL Kevel] et les API de gestion des segments afin de prendre en charge le ciblage en temps réel au moment de la décision de publicité. [[!DNL Kevel]](https://www.kevel.com/) fournit la technologie activée par l’IA et des conseils d’experts qui aident les leaders du commerce innovants à lancer, développer et réussir dans les médias de détail. [!DNL Kevel]’s Retail Media Cloud optimise les formats publicitaires ciblés, attribuables et personnalisables pour la publicité sur site et hors site. |
| Connecteur de destination [Index Exchange](/help/destinations/catalog/advertising/index-exchange.md) désormais disponible | Utilisez ce connecteur de destination pour exporter des segments d’audience de Adobe Experience Platform directement vers la plateforme de publicité programmatique d’[!DNL Index Exchange]. [!DNL Index] est une plateforme publicitaire mondiale axée sur l’offre qui aide les propriétaires de médias à maximiser la valeur de leur contenu sur chaque écran. Fort de plus de 20 ans de leadership dans le secteur, [!DNL Index] met en relation les plus grandes marques du monde avec des créateurs d’expériences haut de gamme afin de proposer des expériences client de haute qualité. |
| Prise en charge des points d’entrée régionaux pour les connexions Braze | Tous les points d’entrée [spécifiques à une région](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) pris en charge par [!DNL Braze] peuvent désormais être sélectionnés pendant le flux de configuration de destination. Demandez à votre représentant [!DNL Braze] quelle instance de point d’entrée vous devez utiliser. |
| Prise en charge de la planification hebdomadaire et mensuelle pour l’intégration [Liveramp](../../destinations/catalog/advertising/liveramp-onboarding.md#scheduling) | Vous pouvez désormais configurer des plannings d’exportation hebdomadaires et mensuels pour la destination d’intégration Liveramp. <br> Cette version est déployée progressivement et sera terminée d’ici le 30 janvier. |
| Expérience d’activation améliorée pour les destinations [The Trade Desk](../../destinations/catalog/advertising/tradedesk.md) et [Microsoft Bing](../../destinations/catalog/advertising/bing.md) | Les destinations Trade Desk et Microsoft Bing incluent désormais des mappages obligatoires prédéfinis pour une expérience d’activation optimisée.  <br> Cette version est déployée progressivement et sera terminée d’ici le 30 janvier. ![Image montrant les mappages prédéfinis pour The Trade Desk](assets/january/mandatory-mappings-ttd.png) {width="150" align="center" zoomable="yes"} <br> ![Image montrant les mappages prédéfinis pour Microsoft Bing](assets/january/mandatory-mappings-bing.png) {width="150" align="center" zoomable="yes"} |
| Prise en charge de l’activation des numéros de téléphone pour la connexion [&#x200B; The Trade Desk - CRM &#x200B;](../../destinations/catalog/advertising/tradedesk-emails.md#phone-hashing) | La destination Trade Desk - CRM prend désormais en charge l’activation des numéros de téléphone en plus des adresses e-mail. Vous pouvez activer les numéros de téléphone non hachés au format E.164 et les numéros de téléphone hachés (format SHA256_E.164) sur votre compte Trade Desk pour le ciblage et la suppression d’audiences en fonction des données CRM. Les numéros de téléphone doivent être normalisés au format E.164 avant activation. |
| [Mises à jour de destination par lots de Snowflake](../../destinations/catalog/warehouses/snowflake-batch.md) | La destination par lots Snowflake comprend désormais une fonctionnalité de sélection de région lors de la configuration de la destination. Vous pouvez désormais sélectionner la région Snowflake spécifique dans laquelle votre instance est configurée, ce qui garantit un transfert de données optimal et la conformité aux exigences régionales. En outre, la restriction par défaut de la politique de fusion a été supprimée, ce qui vous permet d’exporter des audiences mappées à n’importe quelle politique de fusion. <br> La destination par lots [!DNL Snowflake] est actuellement disponible uniquement pour les clients Real-Time CDP configurés dans la région Experience Platform VA7. |


<!-- |AES256 encryption support for [Amazon S3](../../destinations/catalog/cloud-storage/amazon-s3.md#destination-details) destinations | You can now configure AES256 encryption for your Amazon S3 exports. Two options are available: <ul><li>**[!UICONTROL Default]**: Data will be encrypted at rest with the default encryption algorithm set on your bucket.</li><li>**[!UICONTROL SSE-S3/AES256]**: Experience Platform adds the `s3:x-amz-server-side-encryption": "AES256` header in the export and data will be encrypted at rest with the AES256 algorithm when it lands in S3. **This option takes precedence over any default encryption algorithm configured on your S3 bucket**.</li></ul> This release is being rolled out gradually and will be complete by January 30th.| -->

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Mise à jour des limites du mécanisme de sécurisation pour les destinations [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | Le nombre maximal d’audiences pouvant être mappées à une seule destination Adobe Target est passé de 50 à 250. Cela aligne Adobe Target sur la limite d’audience standard pour d’autres destinations, offrant ainsi une plus grande flexibilité pour les workflows d’activation des audiences. Vous pouvez désormais activer davantage d’audiences vers les destinations Adobe Target sans avoir à créer plusieurs flux de données. |
| [Modifier les destinations](/help/destinations/ui/edit-destination.md) et [modifier les actions marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) disponibilité générale | L’option permettant de modifier les destinations et les actions marketing est désormais disponible pour tous les utilisateurs et utilisatrices. |
| Activez/désactivez les noms d’affichage des champs dans l’[&#x200B; Mappage &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) | Lors du mappage des champs de schéma à une destination, vous pouvez désormais basculer entre l’affichage du nom complet du champ XDM et l’affichage uniquement du nom d’affichage. <br> ![Enregistrement d’écran affichant le bouton bascule du nom d’affichage.](/help/release-notes/2026/assets/january/show-display-names.gif) |

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
| Améliorations de la visionneuse de profils (GA) | Les améliorations suivantes ont été apportées à la visionneuse de profils. <ul><li>**Vue combinée** : les attributs, événements et informations ont été combinés en une seule vue.</li><li>**Informations générées par l’IA** : la page des détails du profil affiche désormais des informations générées par l’IA, vous permettant de connaître les détails générés à partir de votre profil. Ces informations peuvent inclure des informations telles que les scores de propension et l’analyse des tendances.</li><li>**Mise à jour du style** : la page des détails du profil a été actualisée visuellement.</li><li>**Parcourir** : vous pouvez désormais explorer vos profils à l’aide d’un carrousel interactif basé sur une carte avec recherche et personnalisation.</li></ul> Pour plus d’informations, consultez le [guide de la visionneuse de profils](/help/profile/ui/user-guide.md). |

{style="table-layout:auto"}

Pour plus d’informations, consultez la [[!DNL Real-Time Customer Profile] vue d’ensemble](../../profile/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Actualisation de l’expiration des données d’audience externe | Les audiences externes (telles que les chargements de fichiers CSV) prennent désormais en charge une fonctionnalité d’actualisation forcée pour les paramètres d’expiration des données. Cette fonctionnalité permet aux utilisateurs d’actualiser manuellement l’expiration des données pour les audiences externes, offrant ainsi un meilleur contrôle sur la gestion du cycle de vie des audiences. Cela s’avère particulièrement utile pour les audiences qui doivent persister au-delà de leur période d’expiration initiale des données ou qui nécessitent une réactivation sans télécharger à nouveau les données. Pour plus d’informations sur cette fonctionnalité, consultez la [présentation d’Audience Portal](../../segmentation/ui/audience-portal.md#audience-summary). |
| Validation de l’audience | Experience Platform fournit désormais des validations intégrées pour s’assurer que vos audiences sont précises, stables et évolutives. Ces vérifications sont automatiquement exécutées en temps réel pendant que vous créez vos définitions d’audience. Pour plus d’informations, consultez la [présentation de la validation de l’audience](/help/segmentation/validation.md). |

Pour plus d’informations, consultez la [[!DNL Segmentation Service] vue d’ensemble](../../segmentation/home.md).

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Sources nouvelles ou mises à jour**

| Source | Description |
| --- | --- |
| Source [[!DNL Oracle Eloqua]](/help/sources/connectors/marketing-automation/eloqua.md) V2 | Un nouveau connecteur source [!DNL Oracle Eloqua] est désormais disponible, remplaçant le [connecteur obsolète](/help/sources/connectors/marketing-automation/oracle-eloqua.md). Ce connecteur mis à jour offre des fonctionnalités améliorées et une fiabilité améliorée pour l’ingestion de données à partir de [!DNL Oracle Eloqua] dans Experience Platform. Les clients qui utilisent le connecteur existant doivent migrer vers la nouvelle mise en œuvre, car les connexions existantes ne fonctionneront plus. Le nouveau connecteur prend en charge toutes les étapes d’installation et de configuration nécessaires pour se connecter à [!DNL Oracle Eloqua] et ingérer des données d’automatisation du marketing. |
| Source [[!DNL Salesforce Marketing Cloud]](/help/sources/connectors/marketing-automation/sfmc.md) V2 | Un nouveau connecteur source [!DNL Salesforce Marketing Cloud] est désormais disponible, remplaçant le [connecteur obsolète](/help/sources/connectors/marketing-automation/salesforce-marketing-cloud.md). Ce connecteur mis à jour offre des performances améliorées et des fonctionnalités supplémentaires pour l’ingestion de données à partir de [!DNL Salesforce Marketing Cloud] dans Experience Platform. Les clients qui utilisent le connecteur existant doivent passer à la nouvelle mise en œuvre. Le nouveau connecteur comprend des instructions de configuration complètes pour la connexion à [!DNL Salesforce Marketing Cloud] et l’ingestion de données d’automatisation du marketing. |

Pour plus d’informations, consultez la [vue d’ensemble des sources](../../sources/home.md).

