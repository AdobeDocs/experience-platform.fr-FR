---
title: Notes de mise à jour d’Adobe Experience Platform - Juin 2025
description: Les notes de mise à jour de juin 2025 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b39de456b40acda77c67d25ebeba2c8a41c5d3f6
workflow-type: tm+mt
source-wordcount: '1632'
ht-degree: 35%

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

**Date de publication : jeudi 18 juin 2025**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Contrôle d’accès](#access-control)
- [Gestion avancée du cycle de vie des données](#advanced-data-lifecycle-management)
- [Service de catalogue](#catalog-service)
- [Tableaux de bord](#dashboards)
- [Gouvernance des données](#data-governance)
- [Destinations](#destinations)
- [Composition d’audiences fédérées](#fac)
- [Privacy Service](#privacy-service)
- [Sandbox](#sandboxes)
- [Segmentation](#segmentation-service)
- [Sources](#sources)

## Contrôle d’accès {#access-control}

Experience Platform exploite les profils de produit [Adobe Admin Console](https://adminconsole.adobe.com) pour lier les utilisateurs à des autorisations et des sandbox. Les autorisations contrôlent l’accès à de nombreuses fonctionnalités d’Experience Platform, notamment la modélisation des données, la gestion des profils et l’administration des sandbox.

**Fonctionnalités clés**

| Fonctionnalité | Description |
| ------- | ----------- |
| Autorisation Exporter les données du tableau de bord | Les options **[!UICONTROL Télécharger CSV]** et **[!UICONTROL Envoyer par e-mail]** des tableaux de bord nécessitent désormais l’autorisation **[!UICONTROL Exporter les données du tableau de bord]**. Cette autorisation permet de s’assurer que seuls les utilisateurs autorisés peuvent exporter des données insight tabulées, ce qui permet de renforcer les politiques de gouvernance et de contrôle d’accès aux données. Pour plus d’informations, consultez la section [autorisations](../../access-control/home.md#permissions) du guide de contrôle d’accès. |

Pour plus d’informations, consultez la [présentation du contrôle d’accès](../../access-control/home.md).

## Gestion avancée du cycle de vie des données {#advanced-data-lifecycle-management}

Experience Platform fournit un ensemble de fonctionnalités d’hygiène des données qui vous permettent de gérer vos données stockées par le biais de suppressions programmées d’enregistrements et de jeux de données de clients. En utilisant l’espace de travail Cycle de vie des données dans l’interface utilisateur ou par le biais d’appels à l’API Data Hygiene, vous pouvez gérer efficacement vos entrepôts de données. Utilisez ces fonctionnalités pour vous assurer que les informations sont utilisées comme prévu, qu’elles sont mises à jour lorsque des données incorrectes doivent être corrigées et qu’elles sont supprimées lorsque les politiques d’entreprise le jugent nécessaire.

**Nouvelle documentation**

| Nouvelle documentation | Description |
| --- | --- |
| Disponibilité générale de la suppression des enregistrements | Vous pouvez désormais supprimer des enregistrements individuels en fonction de champs d’identité à l’aide de l’interface utilisateur ou de l’API. Cette fonctionnalité permet de réduire le stockage, d’appliquer la gouvernance et d’améliorer l’hygiène des données en autorisant les suppressions d’un seul jeu de données ou de tous les jeux de données. Des limites de volume et des exigences de droits s’appliquent. Pour plus d’informations, consultez le guide [suppression d’enregistrements](../../hygiene/ui/record-delete.md) . |

Pour plus d’informations, consultez la [présentation de la gestion avancée du cycle de vie des données](../../hygiene/home.md).

## Catalog Service {#catalog-service}

Catalog Service est le système d’enregistrement pour l’emplacement et la parenté des données au sein d’Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, Catalog conserve les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Amélioration de la prévisualisation des jeux de données : navigation plus rapide et informations plus claires | Prévisualisez rapidement les données des jeux de données, affichez les requêtes SQL sous-jacentes et explorez jusqu’à 100 lignes avec un filtrage amélioré et une visibilité de structure plus claire, le tout dans l’expérience familière d’aperçu de jeu de données. Lisez le [guide d’utilisation des jeux de données](../../catalog/datasets/user-guide.md#preview) pour plus d’informations. |

{style="table-layout:auto"}

## Tableaux de bord {#dashboards}

Experience Platform propose de nombreux tableaux de bord qui vous permettent d’afficher des informations importantes sur les données de votre organisation, telles quʼelles ont été capturées lors dʼinstantanés quotidiens.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Option Envoyer en tant qu’e-mail pour l’exportation | Vous pouvez désormais exporter jusqu’à 10 000 enregistrements des tableaux de bord du mode Query Pro en sélectionnant **[!UICONTROL Envoyer par e-mail]** dans le menu **[!UICONTROL En savoir plus]**. Cette option envoie en toute sécurité un lien de téléchargement à votre e-mail associé à Adobe pour des exportations plus importantes. Lisez le guide [Afficher plus](../../dashboards/sql-insights-query-pro-mode/view-more.md#export) pour plus d’informations. |

Pour plus dʼinformations sur les tableaux de bord, notamment sur la manière dʼoctroyer des autorisations dʼaccès et de créer des widgets personnalisés, commencez par lire la [présentation des tableaux de bord](../../dashboards/home.md).

## Gouvernance des données {#data-governance}

Dans Adobe Experience Platform, la gouvernance des données désigne un ensemble de politiques et de technologies permettant de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Elle joue un rôle clé dans [!DNL Experience Platform] à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les politiques d’accès aux données et le contrôle d’accès aux données pour les actions marketing.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Alertes et configuration des Places sur la liste autorisée IP Azure CMK | Vous pouvez désormais placer sur la liste autorisée l’adresse IP statique d’Adobe dans Azure Key Vault pour garantir un accès continu lorsque les restrictions réseau sont activées. Cela permet d’éviter les perturbations des services Platform dues à un accès aux clés restreint. |
| Alertes et résolutions de configuration CMK | Experience Platform déclenche désormais des alertes lorsque les services Adobe perdent l’accès à votre coffre de clés Azure (par exemple, en raison d’entrées de place sur la liste autorisée IP supprimées ou de clés désactivées). Un nouveau guide vous aide à comprendre chaque alerte et à prendre des mesures correctives. |

Pour plus d’informations, consultez la [présentation de la gouvernance des données](../../data-governance/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations**

| Destination | Description |
| --- | --- |
| Connexion [[!DNL Algolia]](../../destinations/catalog/personalization/algolia.md) | Utilisez la destination [!DNL Algolia] pour offrir une personnalisation cohérente sur tous les sites, de la page d’accueil à la recherche. Créez des audiences enrichies à partir de plusieurs sources de données et partagez-les sur différents canaux pour améliorer les stratégies de ciblage et la personnalisation des campagnes. |

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| [Surveillance au niveau de l’audience](../../dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) pour les destinations de diffusion en streaming | La surveillance au niveau de l’audience est désormais disponible pour les destinations suivantes : <ul><li>[[!DNL (API) Oracle Eloqua] Connexion](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)</li><li>[[!DNL (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)</li><li>[[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md)</li><li>[[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)</li><li>[[!DNL Google Customer Match + Display & Video 360]](../../destinations/catalog/advertising/google-customer-match-dv360.md)</li><li>[[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)</li><li>[[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md)</li><li>[[!DNL Magnite: Real-time]](../../destinations/catalog/advertising/magnite-streaming.md)</li><li>[[!DNL Marketo Engage Person Sync]](../../destinations/catalog/adobe/marketo-engage-person-sync.md)</li><li>[[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md)</li><li>[[!DNL Moengage]](../../destinations/catalog/mobile-engagement/moengage.md)</li><li>[[!DNL Outreach]](../../destinations/catalog/crm/outreach.md)</li><li>[[!DNL PubMatic Connect]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL PubMatic Connect (Custom Audience ID Mapping)]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL Qualtrics Automations]](../../destinations/catalog/survey/qualtrics-automations.md)</li><li>[[!DNL RainFocus Attendee Profiles]](../../destinations/catalog/marketing-automation/rainfocus.md)</li><li>[[!DNL SAP Commerce]](../../destinations/catalog/ecommerce/sap-commerce.md)</li><li>[[!DNL Snowflake]](../../destinations/catalog/cloud-storage/snowflake.md)</li><li>[[!DNL Yahoo DataX]](../../destinations/catalog/advertising/datax.md)</li><li>[[!DNL Zendesk]](../../destinations/catalog/crm/zendesk.md)</li></ul> |
| Prise en charge des identifiants supplémentaires pour les destinations [Facebook](../../destinations/catalog/social/facebook.md#supported-identities) | La destination [!DNL Facebook] prend désormais en charge le mappage de nouveaux champs liés aux adresses pour un ciblage amélioré et une correspondance avec les profils sur les propriétés Facebook. Pour plus d’informations sur les nouveaux champs liés à l’adresse, consultez la section [identités prises en charge](../../destinations/catalog/social/facebook.md#supported-identities). <br> ![Image de l’interface utilisateur de Platform montrant les champs supplémentaires pour Facebook.](../2025/assets/june/facebook-destination-fields.png "Image de l’interface utilisateur de Platform montrant les champs supplémentaires pour Facebook."){width="200" align="center" zoomable="yes"} |
| Mise à niveau de la destination [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | À compter du 19 juin 2025, vous pourrez voir deux cartes **[!DNL Braze]** côte à côte dans le catalogue des destinations. Cela est dû à une mise à niveau interne vers le service de destinations. Le connecteur de destination [!DNL Braze] existant a été renommé **[!UICONTROL (obsolète) Braze]** et une nouvelle carte portant le nom **[!UICONTROL Braze]** est désormais disponible. <br> Utiliser la connexion **[!UICONTROL Braze]** dans le catalogue pour les nouveaux flux de données d’activation. Si vous disposez de flux de données actifs vers la destination **[!UICONTROL (obsolète) Braze]** , ils seront mis à jour automatiquement. Aucune action n’est donc requise de votre part. <br> Si vous créez des flux de données par le biais de l’[API Flow Service](https://developer.adobe.com/experience-platform-apis/references/destinations/), vous devez mettre à jour vos [!DNL flow spec ID] et [!DNL connection spec ID] avec les valeurs suivantes : <ul><li>ID de spécification de flux : `cb7919bd-69aa-462d-bcc0-db7cdc7fdf51`</li><li>ID de spécification de connexion : `ab957205-5a78-4393-b901-b930ed548220`</li></ul> |

{style="table-layout:auto"}

<!-- | [Google Customer Match + DV360](../../destinations/catalog/advertising/google-customer-match-dv360.md) general availability | The Google Customer Match + DV360 destination is now available for all Experience Platform users. The documentation now includes detailed guidance for [account linking](../../destinations/catalog/advertising/google-customer-match-dv360.md#linking) between [!DNL Adobe] and [!DNL Google] advertising accounts. | -->

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../../destinations/home.md).

## Composition d’audiences fédérées {#fac}

La composition de l’audience fédérée permet aux entreprises de composer des données pour une meilleure application dans divers cas d’utilisation. Grâce à cette nouvelle approche, en tant qu’utilisateur Adobe Real-Time Customer Data Platform et/ou Adobe Journey Optimizer, vous pouvez fédérer des jeux de données directement à partir de votre entrepôt de données existant afin de créer et d’enrichir des audiences et des attributs Adobe Experience Platform dans un seul système.

| Nouvelle fonctionnalité | Description |
| ----------- | ----------- |
| Disponibilité générale pour les clients Adobe Healthcare Shield | La composition de l’audience fédérée sera disponible pour les clients d’Adobe Healthcare Shield pour la création d’audiences, l’enrichissement et l’enrichissement des profils d’ici la fin juin. Pour plus d’informations sur les mesures de confidentialité et de sécurité de la composition d’audiences fédérées, consultez la [présentation de la confidentialité et de la sécurité dans la composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/start/privacy-security). Pour plus d’informations sur la conformité HIPAA des produits Experience Platform en général, consultez la [ Présentation des produits et services HIPAA et Adobe ](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

Pour plus d’informations, consultez la [documentation sur la composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/home).

## [!DNL Privacy Service] {#privacy}

Plusieurs réglementations légales et organisationnelles donnent aux utilisateurs le droit d’accéder à leurs données personnelles ou de les supprimer de vos banques de données sur demande. Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface utilisateur pour vous aider à gérer ces requêtes de données de vos clients. Avec [!DNL Privacy Service], vous pouvez envoyer des demandes d’accès et de suppression de données clients privées ou personnelles des applications Adobe Experience Cloud, ce qui facilite l’automatisation de la conformité aux réglementations de confidentialité légales et au sein de l’organisation.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | ---|
| Prise en charge des lois sur la protection de la vie privée du Tennessee et du Minnesota | Privacy Service prend désormais en charge le Tennessee Information Protection Act (`tipa_tn_usa`) et le Minnesota Consumer Data Privacy Act (`mcdpa_mn_usa`). Vous pouvez traiter les demandes d’accès et de suppression conformément à ces nouvelles réglementations au niveau de l’État. Pour plus d’informations, consultez la [présentation de la réglementation](https://experienceleague.adobe.com/fr/docs/experience-platform/privacy/regulations/overview). |

Voir la présentation de [Privacy Service](../../privacy-service/home.md) pour plus d’informations sur le service.

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Migration des mises à jour de la configuration des objets | Vous pouvez désormais migrer les mises à jour de configuration d’objet itératif dans les sandbox après la réplication initiale. Cette amélioration prend en charge les workflows de développement pour lesquels les configurations doivent être mises à jour et propagées dans les environnements sans recréer l’ensemble de la configuration du sandbox. Pour plus d’informations, consultez le guide sur le [transfert des mises à jour de configuration entre les sandbox](../../sandboxes/ui/sandbox-tooling.md#move-configs). |

{style="table-layout:auto"}

Pour plus d’informations sur les sandbox, consultez la [vue d’ensemble des sandbox](../../sandboxes/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions des clientes et clients avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mise à jour de la disponibilité des informations semblables | Les informations semblables et les audiences semblables sont automatiquement désactivées pour les environnements qui affichent une faible utilisation. Une faible utilisation est définie comme le fait de ne pas afficher d’informations semblables au cours des trois derniers mois ou de ne pas créer d’audience semblable au cours des six derniers mois. Vous trouverez plus d’informations sur cette modification dans le [guide des audiences semblables](../../segmentation/types/lookalike-audiences.md). |

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de l’interface utilisateur de [!BADGE Beta]{type=Informative} pour [!DNL Azure Databricks] | Vous pouvez désormais connecter votre compte [!DNL Azure Databricks] à Experience Platform à l’aide de l’espace de travail des sources dans l’interface utilisateur. Pour plus d’informations, consultez le guide sur la [connexion  [!DNL Databricks]  Experience Platform dans l’interface utilisateur](../../sources/connectors/databases/databricks.md). |
| Prise en charge d’un nouveau type d’authentification pour [!DNL Azure Synapse Analytics] | Désormais, le [!DNL Azure Synapse Analytics] prend également en charge l’authentification du principal de service, en plus de l’authentification de chaîne de connexion existante. Pour plus d’informations, consultez la [[!DNL Azure Synapse Analytics] présentation de l’authentification](../../sources/connectors/databases/synapse-analytics.md) |
| [!DNL Salesforce] l’obsolescence de l’authentification de base | L’authentification de base pour [Salesforce CRM](../../sources/connectors/crm/salesforce.md) et [Salesforce Service Cloud](../../sources/connectors/customer-success/salesforce-service-cloud.md) sera abandonnée d’ici janvier 2026. Les clients doivent migrer vers l’authentification OAuth 2.0 pour maintenir la connectivité. Cette modification affecte les deux connecteurs source et améliore la sécurité et la conformité aux normes d’authentification Salesforce. |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des sources](../../sources/home.md).
