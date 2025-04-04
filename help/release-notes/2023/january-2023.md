---
title: Notes de mise à jour d’Adobe Experience Platform - Janvier 2023
description: Notes de mise à jour de janvier 2023 pour Adobe Experience Platform.
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2227'
ht-degree: 97%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 25 janvier 2023**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [Assurance](#assurance)
- [Collecte de données](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Profil client en temps réel](#profile)
- [Segmentation Service](#segmentation)
- [Sources](#sources)

## Services d’intelligence artificielle/de machine learning {#ai-ml}

Les services d’intelligence artificielle et de machine learning permettent aux analystes et aux spécialistes du marketing d’exploiter la puissance de l’IA/ML dans les cas d’utilisation de l’expérience client. Cela permet aux analystes marketing de configurer des prédictions, sans avoir besoin d’expertise en science des données, spécifiques aux besoins d’une entreprise utilisant des configurations au niveau de l’entreprise.

### IA dédiée à l’attribution

Le service IA dédiée à l’attribution est utilisé pour attribuer des crédits aux points de contact qui mènent à des événements de conversion. Il peut aider les spécialistes du marketing à quantifier l’impact publicitaire de chaque point de contact marketing sur le parcours client.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Conformité HIPAA | Les clients de Healthcare Shield peuvent désormais recevoir, utiliser, gérer ou transmettre des informations de santé protégées dans le service IA dédiée à l’attribution et dans certaines autres applications basées sur Experience Platform. Healthcare Shield est destiné aux clients du secteur de la santé qui sont soit une entité couverte, soit un partenaire commercial soumis à la loi américaine HIPAA. Pour plus d’informations, consultez la documentation sur la loi [HIPAA et les produits et services Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |
| Modifier des colonnes de jeux de données de score supplémentaires | Il est désormais possible d’ajouter ou supprimer des colonnes de jeux de données de score supplémentaires (colonnes de rapports) lorsque des modèles existants sont modifiés. Cela permet d’étendre la flexibilité des scores d’attribution afin d’obtenir des insights sur les dimensions supplémentaires une fois qu’un modèle a déjà été créé. Consultez le [Guide de l’interface utilisateur du service Attribution](../../intelligent-services/attribution-ai/user-guide.md) pour en savoir plus. |

{style="table-layout:auto"}

Consultez la présentation générale des [Services AI/ML](../../intelligent-services/attribution-ai/overview.md) pour plus d’informations.

### IA dédiée aux clients

L’application IA dédiée aux clients pour Real-time Customer Data Platform est utilisée pour générer des scores de propension personnalisés tels que l’attrition et la conversion pour des profils individuels à grande échelle. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en un problème de machine learning ou d’avoir recours à un algorithme, à une formation ou à un déploiement.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Conformité HIPAA | Les clients de Healthcare Shield peuvent désormais recevoir, utiliser, gérer ou transmettre des informations de santé protégées dans IA dédiée aux clients pour Real-time Customer Data Platform et certaines autres applications basées sur Experience Platform. Healthcare Shield est destiné aux clients du secteur de la santé qui sont soit une entité couverte, soit un partenaire commercial soumis à la loi américaine HIPAA. Pour plus d’informations, consultez la documentation sur la loi [HIPAA et les produits et services Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

{style="table-layout:auto"}

Consultez la présentation générale des [Services IA/ML](../../intelligent-services/customer-ai/overview.md) pour plus d’informations.

## Assurance {#assurance}

Adobe Assurance permet de contrôler, de tester, de simuler et de valider la manière dont vous collectez les données ou dont les expériences sont accomplies dans l’application mobile.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Éditeur de validation | De nouvelles améliorations ont été apportées à l’éditeur de validation. Ces améliorations incluent des colonnes de validation, de nouveaux outils de création de code et des vues améliorées. |

{style="table-layout:auto"}

Pour plus d’informations sur l’assurance, consultez la [documentation sur l’assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Nouvel écran d’accueil | La page d’accueil de l’interface utilisateur de collecte de données a été mise à jour afin d’inclure des informations d’intégration et des liens utiles pour favoriser la productivité. Cela inclut :<ol><li>Documentation et workflows recommandés pour commencer</li><li>Propriétés, règles et éléments de données récents</li><li>Extensions populaires</li><li>Nouvelles mises à jour des extensions avec une fonction d’installation rapide</li></ol> |
| Envoyer des données à [!DNL Google Ads] en utilisant le transfert d’événement | Vous pouvez désormais utiliser l’[[!DNL Google Ads Enhanced Conversions] extension API](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) pour le transfert d’événement, combiné avec [Google Oauth 2 secrets](../../tags/ui/event-forwarding/secrets.md#google-oauth2), pour envoyer en toute sécurité des données côté serveur à [!DNL Google Ads] en temps réel. |

{style="table-layout:auto"}

## Destinations (mises à jour le 2 février) {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations**

| Destination | Description |
| ----------- | ----------- |
| [Connexion à Adobe Experience Cloud Audiences (bêta)](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Utilisez la connexion [!UICONTROL à Audiences Adobe Experience Cloud (bêta)] pour partager des segments d’Experience Platform vers différentes solutions d’Experience Platform, telles qu’Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target ou Marketo. |
| [Connexion à un profil Pega](../../destinations/catalog/personalization/pega-profile.md) | Utilisez le [!DNL Pega Profile Connector] dans Adobe Experience Platform pour créer une connexion sortante active à votre stockage S3 [!DNL Amazon] afin d’exporter périodiquement des données de profil vers des fichiers CSV à partir d’Adobe Experience Platform dans vos propres compartiments S3. Dans [!DNL Pega Customer Decision Hub], vous pouvez planifier des tâches de données pour importer ces données de profil à partir du stockage S3 afin de mettre à jour le profil [!DNL Pega Customer Decision Hub]. |
| [Connexion UE à The Trade Desk CRM (bêta)](../../destinations/catalog/advertising/tradedesk-emails.md) | Avec la publication de l’EUID (European Unified ID), deux destinations [!DNL The Trade Desk - CRM] dans le [catalogue de destinations](/help/destinations/catalog/overview.md) sont maintenant affichées. <ul><li> Si vos données proviennent de l’UE, utilisez la destination **[!DNL The Trade Desk - CRM (EU)]**.</li><li> Si vos données proviennent des régions APAC ou NAMER, utilisez la destination **[!DNL The Trade Desk - CRM (NAMER & APAC)]**. </li></ul> |

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonction | Description |
| ----------- | ----------- |
| Amélioration de la politique de consentement des médias payants pour les intégrations aux destinations de streaming | Une [amélioration de l’application des politiques de consentement](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) sur les [destinations de streaming](/help/destinations/destination-types.md#streaming-destinations) pour les cas d’utilisation de l’activation de médias payants. Lorsque les profils ne sont plus qualifiés pour une politique de consentement, Experience Platform communique désormais de manière proactive sa sortie de politique aux destinations de streaming. <br> <b>Remarque</b> : cette fonctionnalité est disponible uniquement pour les clients et clientes de **[!UICONTROL Privacy and Security Shield]** et celles et ceux de **[!UICONTROL Healthcare Shield]**. |
| Nouvelles options de délimiteur pour les connecteurs de destination d’espace de stockage dans le cloud beta | Trois nouvelles options de délimiteur (deux points `:`, barre verticale, point-virgule `;`) sont désormais disponibles pour les nouvelles destinations d’espace de stockage dans le cloud bêta - [(Bêta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Bêta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Bêta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Bêta) Zone d’atterrissage des données](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Bêta) Espace de stockage dans le cloud Google](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Bêta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> En savoir plus sur la prise en charge des [options de formatage de fichier](/help/destinations/ui/batch-destinations-file-formatting-options.md) pour les destinations basées sur des fichiers. |
| Nouveau paramètre facultatif disponible dans les configurations de [champs de données client](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md) dans [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique` : utilisez ce paramètre lorsque vous devez créer un champ de données client dont la valeur doit être unique pour tous les flux de données de destination configurés par l’organisation d’un utilisateur ou d’une utilisatrice. <br> Par exemple, le champ **[!UICONTROL Alias d’intégration]** dans la destination [[!UICONTROL Personnalisation sur mesure]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) doit être unique, ce qui signifie que deux flux de données distincts vers cette destination ne peuvent pas avoir la même valeur pour ce champ. |

**Correctifs et améliorations** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Correctif ou amélioration</b></td>
        <td><b>Description</b></td>
    </tr>
    <tr>
        <td>Mise à jour du comportement d’exportation vers des destinations basées sur des fichiers (PLAT-123316)</td>
        <td>Nous avons corrigé un problème dans le comportement des <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mandatory-attributes">attributs obligatoires</a> lors de l’exportation de fichiers de données vers des destinations groupées. <br> Auparavant, chaque enregistrement des fichiers de sortie était vérifié pour contenir à la fois : <ol><li>Une valeur non nulle de la colonne <code>mandatoryField</code> et</li><li>Une valeur non nulle sur au moins un des autres champs non obligatoires.</li></ol> La deuxième condition a été supprimée. Par conséquent, il se peut que davantage de lignes de sortie s’affichent dans vos fichiers de données exportés, comme illustré dans l’exemple ci-dessous :<br> <b> Exemple de comportement avant la version de janvier 2023 </b> <br> Champ obligatoire : <code>emailAddress</code> <br> <b>Données de saisie à activer</b> <br><table><thead><tr><th>Prénom</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jennifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Sortie d’activation</b> <br><table><thead><tr><th>Prénom</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jennifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Exemple de comportement après la version de janvier 2023 </b> <br> <b>Sortie d’activation</b> <br> <table><thead><tr><th>Prénom</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jennifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>Validation de l’interface utilisateur et de l’API pour les mappages requis et les mappages en double (PLAT-123316)</td>
        <td>La validation est désormais appliquée comme suit dans l’interface utilisateur et l’API lors du <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mapping">mappage des champs</a> dans le workflow d’activation des destinations :<ul><li><b>Mappings requis</b> : si la destination a été configurée par le développeur ou la développeuse de destination avec les mappages requis (par exemple, la destination <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html">Google Ad Manager 360</a>), ces mappages requis doivent être ajoutés par l’utilisateur ou l’utilisatrice lors de l’activation des données vers la destination. </li><li><b>Duplication des mappages</b> : dans l’étape de mapping du workflow d’activation, vous pouvez dupliquer des valeurs dans les champs sources, mais pas dans les champs cibles. Consultez le tableau ci-dessous pour obtenir un exemple de combinaisons de mappage autorisées et interdites. <br><table><thead><tr><th>Autorisé/interdit</th><th>Champ source</th><th>Champ cible</th></tr></thead><tbody><tr><td>Autorisé</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>email alias2</li></ul></td></tr><tr><td>Interdit</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

Pour des informations plus générales sur les destinations, consultez la [présentation des destinations](../../destinations/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Améliorations du nom d’affichage de l’arborescence des schémas | Auparavant, les noms de champ s’affichaient dans l’interface utilisateur, mais désormais, les noms d’affichage des champs de schéma sur la zone de travail de schéma sont plus facile à lire. |

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Classe | [[!UICONTROL Conversion]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Une classe permettant d’effectuer le suivi des données de conversion telles que les conversions de devise. |
| Groupe de champs | [[!UICONTROL Détails sur le taux de conversion de devise]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Un groupe de champs pour la classe [!UICONTROL Conversion], capturant des détails supplémentaires liés à la conversion de devise. |
| Groupe de champs | [[!UICONTROL Mappage des résultats d’évaluation des politiques de consentement avec métadonnées]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.json) | Capture les détails du résultat de l’évaluation de plusieurs politiques de consentement, y compris les informations de métadonnées sur les entrées et sorties des politiques de consentement. |

**Composants XDM mis à jour**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Type de données | [[!UICONTROL Informations détaillées sur la publicité]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | Le champ `ID` a été renommé `name` et le champ `name` précédent est maintenant `friendlyName`. |
| Type de données | [[!UICONTROL Détails de la proposition de décision]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Ajout d’un champ `selectionStrategy` qui capture les détails d’une stratégie de sélection. |
| Groupe de champs | [[!UICONTROL Événement d’expérience - Interactions de propositions]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | Le groupe de champs est désormais compatible avec la classe [!UICONTROL Événement d’étape de parcours]. |
| Type de données | [[!UICONTROL Informations détaillés sur les erreurs]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | Le champ `ID` a été renommé `name`. |
| Type de données | [[!UICONTROL Informations sur les médias]](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/media.schema.json) | Annulation d’une modification du modèle de la propriété de segment vidéo. |
| Type de données | [[!UICONTROL Informations détaillées sur les données de la QoE]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Le champ `droppedFrameCount` a été supprimé. |
| Type de données | [[!UICONTROL Informations détaillées sur la session]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Le champ `isAuthorized` a été renommé `authorized`, et son `type`  a été mis à jour en tant que chaîne plutôt qu’en tant que booléen. |
| Type de données | [[!UICONTROL Expédition]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Plusieurs nouveaux champs ajoutés : `shipDate`, `trackingNumber`, et `trackingURL`. |
| Groupe de champs | [[!UICONTROL Champs d’entité AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Plusieurs nouveaux champs ajoutés : `journeyNodeID`, `journeyNodeName`, et `journeyModeType`. |
| Groupe de champs | [[!UICONTROL Événement d’expérience client]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | Le groupe de champs est désormais également compatible avec la classe [!UICONTROL Mesures récapitulatives]. |
| Groupe de champs | [[!UICONTROL Déclencheurs de produits]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | Le champ `productTriggers` est maintenant imbriqué sous un objet `weather`. |
| Groupe de champs | [[!UICONTROL Déclencheurs relatifs]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | Le champ `relativeTriggers` est maintenant imbriqué sous un objet `weather`. |
| Groupe de champs | [[!UICONTROL Déclencheurs Conditions extrêmes]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Le champ `severeTriggers` est maintenant imbriqué sous un objet `weather`. |
| Groupe de champs | [[!UICONTROL Déclencheurs météo]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Le champ `weatherTriggers` est maintenant imbriqué sous un objet `weather`. |
| Groupe de champs | [[!UICONTROL Comptes professionnels associés à XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | Le groupe de champs est maintenant stable. |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Experience Platform, consultez la [ Présentation du système XDM ](../../xdm/home.md).

## Profil client en temps réel {#profile}

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque. Le profil client en temps réel offre une vue holistique de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le Profil vous permet de consolider vos données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

**Obsolescence à venir** {#deprecation}

Pour supprimer la redondance dans le cycle de vie de l’adhésion au segment, le statut `Existing` sera supprimé de le [mappage d’appartenance aux segments](../../xdm/field-groups/profile/segmentation.md) fin mars 2023. Une annonce ultérieure contiendra la date exacte de l’obsolescence.

Après l’obsolescence, les profils qualifiés dans un segment seront représentés comme `Realized` et les profils disqualifiés continueront à être représentés comme `Exited`. Cela permettra d’obtenir la parité avec les destinations basées sur des fichiers avec les statuts de segment `Active` et `Expired`.

Cette modification peut vous impacter si vous utilisez des [destinations d’entreprise](../../destinations/destination-types.md#advanced-enterprise-destinations) (Amazon Kinesis, Azure Event Hubs, API HTTP) et avez mis en place en aval des processus automatisés, en fonction des statuts `Existing`. Vérifiez vos intégrations en aval si c’est votre cas. Si vous souhaitez identifier les profils nouvellement qualifiés au-delà d’un certain temps, envisagez d’utiliser une combinaison du statut `Realized` et du `lastQualificationTime` dans votre mappage d’appartenance aux segments. Pour plus d’informations, contactez votre représentant ou représentante Adobe.

Pour en savoir plus sur le profil client en temps réel, notamment les bonnes pratiques et les tutoriels relatifs à lʼutilisation des données de profil, consultez la [présentation du profil client en temps réel](../../profile/home.md).

## Service de segmentation {#segmentation}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les segments peuvent être basés sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clients avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Importer des valeurs groupées dans le créateur de segments | Le créateur de segments prend désormais en charge l’importation de plusieurs valeurs, soit en chargeant un fichier CSV ou TSV, soit en insérant manuellement des valeurs séparées par des virgules. Vous trouverez plus d’informations dans le [Guide du créateur de segments](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| Expiration de l’appartenance à une audience externe | Par défaut, les appartenances aux audiences externes sont conservées pendant 30 jours. Pour les conserver plus longtemps, utilisez le champ `validUntil` lors de l’ingestion des données d’audience. |
| Expiration de l’appartenance à un segment généré par Experience Platform | Toute appartenance à un segment avec l’état `Exited` pendant plus de 30 jours sera sujette à suppression, en fonction du champ `lastQualificationTime`. |

{style="table-layout:auto"}

Pour plus d’informations sur [!DNL Segmentation Service], consultez la [présentation de la segmentation](../../segmentation/home.md).

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes et vous permet de structurer, d’étiqueter et d’améliorer ces données à l’aide des services d’Experience Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| --- | --- |
| Autoriser l’accès des utilisateurs et utilisatrices aux sous-dossiers des sources d’espaces de stockage dans le cloud | Vous pouvez désormais définir l’accès à un sous-dossier spécifique de votre source d’espace de stockage dans le cloud lors de la création d’un compte. Une fois cet accès créé, les utilisateurs ne pourront accéder qu’aux données du sous-dossier autorisé. Cette fonctionnalité est disponible pour les sources d’espaces de stockage dans le cloud suivantes : [Stockage Azure Blob](../../sources/connectors/cloud-storage/blob.md), [Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md), et [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilité bêta de [!DNL SugarCRM] | Les sources [!DNL SugarCRM] sont désormais disponibles en version bêta. Utilisez les [!DNL SugarCRM Accounts & Contacts] et les sources [!DNL SugarCRM Events] pour importer des données à partir de votre compte [!DNL SugarCRM] dans Experience Platform. Pour plus d’informations, consultez la [[!DNL SugarCRM] vue d’ensemble](../../sources/connectors/crm/sugarcrm.md). |
