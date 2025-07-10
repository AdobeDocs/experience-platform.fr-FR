---
title: Notes de mise à jour d’Adobe Experience Platform - Juin 2025
description: Les notes de mise à jour de juin 2025 pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c78dc0e83976499403e066b314a0889df803c976
workflow-type: ht
source-wordcount: '1665'
ht-degree: 100%

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

**Date de publication : 18 juin 2025**

Nouvelles fonctionnalités et mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

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
| Autorisation Exporter les données du tableau de bord | Les options **[!UICONTROL Télécharger le CSV]** et **[!UICONTROL Envoyer en tant qu’e-mail]** des tableaux de bord nécessitent désormais l’autorisation **[!UICONTROL Exporter les données du tableau de bord]**. Cette autorisation permet de s’assurer que seules les personnes autorisées peuvent exporter des données d’informations tabulées, ce qui permet de renforcer les politiques de gouvernance et de contrôle d’accès aux données. Pour plus d’informations, consultez la section [Autorisations du guide de contrôle d’accès](../../access-control/home.md#permissions). |

Pour plus d’informations, consultez la [vue d’ensemble du contrôle d’accès](../../access-control/home.md).

## Gestion avancée du cycle de vie des données {#advanced-data-lifecycle-management}

Experience Platform offre toute une gamme de fonctionnalités de nettoyage des données. Celles-ci vous permettent de gérer vos données stockées à l’aide de suppressions programmées des enregistrements et des jeux de données des personnes. Depuis l’espace de travail Cycle de vie des données de l’interface d’utilisation ou par le biais d’appels à l’API Data Hygiene, vous pouvez gérer efficacement vos banques de données. Utilisez ces fonctionnalités pour vous assurer que les informations sont utilisées comme prévu, qu’elles sont mises à jour lorsque des données incorrectes doivent être corrigées et qu’elles sont supprimées lorsque les politiques d’entreprise le jugent nécessaire.

**Nouvelle documentation**

| Nouvelle documentation | Description |
| --- | --- |
| Disponibilité générale de la suppression des enregistrements | Vous pouvez désormais supprimer des enregistrements individuels en fonction de champs d’identité à l’aide de l’interface d’utilisation ou de l’API. Cette fonctionnalité permet de réduire le stockage, d’appliquer la gouvernance et d’améliorer l’hygiène des données en autorisant les suppressions d’un ou plusieurs jeux de données. Des limites de volume et des exigences de droits s’appliquent. Pour plus d’informations, consultez le [guide de suppression des enregistrements](../../hygiene/ui/record-delete.md). |

Pour plus d’informations, consultez la [vue d’ensemble de la gestion avancée du cycle de vie des données](../../hygiene/home.md).

## Catalog Service {#catalog-service}

Catalog Service est le système d’enregistrement pour l’emplacement et la parenté des données au sein d’Adobe Experience Platform. Bien que toutes les données ingérées dans Experience Platform soient stockées dans le lac de données sous forme de fichiers et de répertoires, Catalog conserve les métadonnées et la description de ces fichiers et répertoires à des fins de recherche et de surveillance.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Amélioration de la prévisualisation des jeux de données : navigation plus rapide et informations plus claires | Prévisualisez rapidement les données des jeux de données, affichez les requêtes SQL sous-jacentes et explorez jusqu’à 100 lignes avec un filtrage amélioré et une visibilité de structure plus claire, le tout dans l’expérience familière des aperçus de jeu de données. Pour plus d’informations, consultez le [guide d’utilisation des jeux de données](../../catalog/datasets/user-guide.md#preview). |

{style="table-layout:auto"}

## Tableaux de bord {#dashboards}

Experience Platform propose de nombreux tableaux de bord qui vous permettent d’afficher des informations importantes sur les données de votre organisation, telles quʼelles ont été capturées lors dʼinstantanés quotidiens.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Option d’export Envoyer en tant qu’e-mail | Vous pouvez désormais exporter jusqu’à 10 000 enregistrements depuis les tableaux de bord du mode Query Pro en sélectionnant **[!UICONTROL Envoyer en tant qu’e-mail]** dans le menu **[!UICONTROL Afficher plus]**. Cette option envoie en toute sécurité un lien de téléchargement à votre e-mail associé à Adobe pour des exports plus importants. Pour plus d’informations, consultez le [guide Afficher plus](../../dashboards/sql-insights-query-pro-mode/view-more.md#export). |

Pour plus dʼinformations sur les tableaux de bord, notamment sur la manière dʼoctroyer des autorisations dʼaccès et de créer des widgets personnalisés, commencez par lire la [vue dʼensemble des tableaux de bord](../../dashboards/home.md).

## Gouvernance des données {#data-governance}

Dans Adobe Experience Platform, la gouvernance des données désigne un ensemble de politiques et de technologies permettant de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Elle joue un rôle clé dans [!DNL Experience Platform] à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage de l’utilisation des données, les politiques d’accès aux données et le contrôle d’accès aux données pour les actions marketing.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Alertes CMK Azure et configuration de la liste autorisée d’adresses IP | Vous pouvez désormais ajouter l’adresse IP statique d’Adobe à la liste des adresses autorisées dans le coffre Azure Key Vault, afin de garantir un accès continu lorsque des restrictions réseau sont activées. Cela permet d’éviter les perturbations des services Platform dues à un accès aux clés restreint. |
| Alertes de configuration CMK et résolutions | Experience Platform déclenche désormais des alertes lorsque les services Adobe perdent l’accès à votre coffre Azure Key Vault (par exemple, en raison de la suppression d’adresses IP de la liste autorisée ou de clés désactivées). Un nouveau guide vous aide à comprendre chaque alerte et à prendre des mesures correctives. |

Pour plus d’informations, consultez la [vue d’ensemble de la gouvernance des données](../../data-governance/home.md).

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Nouvelles destinations**

| Destination | Description |
| --- | --- |
| Connexion [[!DNL Algolia]](../../destinations/catalog/personalization/algolia.md) | Utilisez la destination [!DNL Algolia] pour offrir une personnalisation cohérente sur tous les sites, de la page d’accueil à la recherche. Créez des audiences enrichies à partir de plusieurs sources de données et partagez-les sur différents canaux pour améliorer les stratégies de ciblage et la personnalisation des campagnes. |

**Fonctionnalité nouvelle ou mise à jour**

| Fonctionnalité | Description |
| --- | --- |
| Disponibilité générale du [Ciblage par liste de clientes et clients de Google + DV360](../../destinations/catalog/advertising/google-customer-match-dv360.md) | La destination Ciblage par liste de clientes et clients de Google + DV360 est désormais disponible pour toutes les personnes utilisant Experience Platform. La documentation comprend désormais des conseils détaillés sur la [liaison de comptes](../../destinations/catalog/advertising/google-customer-match-dv360.md#linking) entre les comptes publicitaires [!DNL Adobe] et [!DNL Google]. |
| [Surveillance au niveau de l’audience](../../dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) pour les destinations de diffusion en streaming | La surveillance au niveau de l’audience est désormais disponible pour les destinations suivantes : <ul><li>[[!DNL (API) Oracle Eloqua] Connexion](../../destinations/catalog/email-marketing/oracle-eloqua-api.md)</li><li>[[!DNL (V2) Marketo Engage]](../../destinations/catalog/adobe/marketo-engage.md)</li><li>[[!DNL Airship Attributes]](../../destinations/catalog/mobile-engagement/airship-attributes.md)</li><li>[[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)</li><li>[[!DNL Google Customer Match + Display & Video 360]](../../destinations/catalog/advertising/google-customer-match-dv360.md)</li><li>[[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)</li><li>[[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md)</li><li>[[!DNL Magnite: Real-time]](../../destinations/catalog/advertising/magnite-streaming.md)</li><li>[[!DNL Marketo Engage Person Sync]](../../destinations/catalog/adobe/marketo-engage-person-sync.md)</li><li>[[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md)</li><li>[[!DNL Moengage]](../../destinations/catalog/mobile-engagement/moengage.md)</li><li>[[!DNL Outreach]](../../destinations/catalog/crm/outreach.md)</li><li>[[!DNL PubMatic Connect]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL PubMatic Connect (Custom Audience ID Mapping)]](../../destinations/catalog/advertising/pubmatic.md)</li><li>[[!DNL Qualtrics Automations]](../../destinations/catalog/survey/qualtrics-automations.md)</li><li>[[!DNL RainFocus Attendee Profiles]](../../destinations/catalog/marketing-automation/rainfocus.md)</li><li>[[!DNL SAP Commerce]](../../destinations/catalog/ecommerce/sap-commerce.md)</li><li>[[!DNL Snowflake]](../../destinations/catalog/cloud-storage/snowflake.md)</li><li>[[!DNL Yahoo DataX]](../../destinations/catalog/advertising/datax.md)</li><li>[[!DNL Zendesk]](../../destinations/catalog/crm/zendesk.md)</li></ul> |
| Prise en charge des identifiants supplémentaires pour les destinations [Facebook](../../destinations/catalog/social/facebook.md#supported-identities) | La destination [!DNL Facebook] prend désormais en charge le mappage de nouveaux champs liés aux adresses pour un ciblage amélioré et une correspondance avec les profils sur les propriétés Facebook. Pour plus d’informations sur les nouveaux champs liés à l’adresse, consultez la section [identités prises en charge](../../destinations/catalog/social/facebook.md#supported-identities). <br> ![Image de l’interface d’utilisation de Platform montrant les champs supplémentaires de Facebook.](../2025/assets/june/facebook-destination-fields.png "Image de l’interface d’utilisation de Platform montrant les champs supplémentaires de Facebook."){width="200" align="center" zoomable="yes"} |
| Mise à niveau de la destination [[!DNL Braze]](../../destinations/catalog/mobile-engagement/braze.md) | À compter du 19 juin 2025, vous pourrez voir deux cartes **[!DNL Braze]** côte à côte dans le catalogue des destinations. Cela est dû à une mise à niveau interne vers le service de destinations. Le connecteur de destination [!DNL Braze] existant a été renommé **[!UICONTROL (obsolète) Braze]** et une nouvelle carte portant le nom **[!UICONTROL Braze]** est désormais disponible. <br> Utilisez la connexion **[!UICONTROL Braze]** dans le catalogue pour les nouveaux flux de données d’activation. Si vous avez des flux de données actifs vers la destination **[!UICONTROL (obsolète) Braze]**, ils seront automatiquement mis à jour. Aucune action n’est donc requise de votre part. <br> Si vous créez des flux de données par le biais de l’[API Flow Service](https://developer.adobe.com/experience-platform-apis/references/destinations/), vous devez mettre à jour vos [!DNL flow spec ID] et [!DNL connection spec ID] avec les valeurs suivantes : <ul><li>ID de spécification de flux : `cb7919bd-69aa-462d-bcc0-db7cdc7fdf51`</li><li>ID de spécification de connexion : `ab957205-5a78-4393-b901-b930ed548220`</li></ul> |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../../destinations/home.md).

## Composition d’audiences fédérées {#fac}

La composition d’audiences fédérées permet aux entreprises de composer des données pour une meilleure application dans divers cas d’utilisation. Grâce à cette nouvelle approche, en tant qu’utilisateur ou utilisatrice d’Adobe Real-Time Customer Data Platform et/ou d’Adobe Journey Optimizer, vous pouvez fédérer les jeux de données directement à partir de votre entrepôt de données existant pour créer et enrichir les audiences et les attributs Adobe Experience Platform dans un seul système.

| Nouvelle fonctionnalité | Description |
| ----------- | ----------- |
| Disponibilité générale pour la clientèle Adobe Healthcare Shield | La composition d’audiences fédérées sera disponible pour la clientèle d’Adobe Healthcare Shield pour la création d’audiences, l’enrichissement et l’enrichissement des profils d’ici la fin juin. Pour plus d’informations sur les mesures de confidentialité et de sécurité de la composition d’audiences fédérées, consultez la [vue d’ensemble de la confidentialité et de la sécurité dans la composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/start/privacy-security). Pour plus d’informations sur la conformité HIPAA des produits Experience Platform en général, consultez la [vue d’ensemble des produits et services HIPAA et Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

Pour plus d’informations, consultez la [documentation de la composition d’audiences fédérées](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/home).

## [!DNL Privacy Service] {#privacy}

Diverses réglementations légales et organisationnelles donnent le droit d’accéder aux données personnelles et de les supprimer des banques de données sur demande. Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface d’utilisation pour vous aider à gérer ces requêtes de données de votre clientèle. Grâce à [!DNL Privacy Service], vous pouvez envoyer des demandes d’accès et de suppression de données clientèle personnelles depuis les applications Adobe Experience Cloud. Cela facilite l’automatisation de la mise en conformité concernant les réglementations légales et organisationnelles liées à la confidentialité.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | ---|
| Prise en charge des lois de confidentialité du Tennessee et du Minnesota | Privacy Service prend désormais en charge le Tennessee Information Protection Act (`tipa_tn_usa`) et le Minnesota Consumer Data Privacy Act (`mcdpa_mn_usa`). Vous pouvez traiter les demandes d’accès et de suppression conformément à ces nouvelles réglementations au niveau de l’État. Pour plus dʼinformations, voir la [vue d’ensemble des réglementations](https://experienceleague.adobe.com/fr/docs/experience-platform/privacy/regulations/overview). |

Pour plus dʼinformations sur ce service, voir la [vue d’ensemble de Privacy Service](../../privacy-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Migration des mises à jour de la configuration des objets | Vous pouvez désormais migrer les mises à jour de configuration d’objet itératif dans les sandbox après la réplication initiale. Cette amélioration prend en charge les workflows de développement pour lesquels les configurations doivent être mises à jour et propagées dans les environnements sans recréer l’ensemble de la configuration du sandbox. Pour plus d’informations, consultez le guide sur le [transfert des mises à jour de configuration des sandbox](../../sandboxes/ui/sandbox-tooling.md#move-configs). |

{style="table-layout:auto"}

Pour plus d’informations sur les sandbox, consultez la [vue d’ensemble des sandbox](../../sandboxes/home.md).

## Service de segmentation {#segmentation-service}

[!DNL Segmentation Service] définit un sous-ensemble particulier de profils en décrivant les critères qui identifient un groupe de clients potentiels de votre base. Les audiences peuvent être basées sur des données d’enregistrement (telles que des informations démographiques) ou des événements de séries temporelles représentant les interactions de la clientèle avec votre marque.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Mise à jour de la disponibilité des informations semblables | Les informations semblables et les audiences semblables sont automatiquement désactivées pour les environnements qui affichent une faible utilisation. Une faible utilisation est définie comme le fait de ne pas afficher d’informations semblables au cours des trois derniers mois ou de ne pas créer d’audience semblable au cours des six derniers mois. Vous trouverez plus d’informations sur cette modification dans le [guide des audiences semblables](../../segmentation/types/lookalike-audiences.md). |

## Sources {#sources}

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de l’IU [!BADGE Beta]{type=Informative} pour [!DNL Azure Databricks] | Vous pouvez désormais connecter votre compte [!DNL Azure Databricks] à Experience Platform à lʼaide de l’espace de travail Sources dans l’IU. Veuillez consulter le guide sur la [connexion [!DNL Databricks]  à Experience Platform dans l’IU](../../sources/connectors/databases/databricks.md) pour plus d’informations. |
| Prise en charge d’un nouveau type d’authentification pour [!DNL Azure Synapse Analytics] | Désormais, [!DNL Azure Synapse Analytics] prend également en charge l’authentification du principal de service, en plus de l’authentification de chaîne de connexion existante. Pour plus d’informations, consultez la [[!DNL Azure Synapse Analytics] vue d’ensemble des authentifications](../../sources/connectors/databases/synapse-analytics.md). |
| Obsolescence de l’authentification de base [!DNL Salesforce] | L’authentification de base pour [Salesforce CRM](../../sources/connectors/crm/salesforce.md) et [Salesforce Service Cloud](../../sources/connectors/customer-success/salesforce-service-cloud.md) sera abandonnée d’ici janvier 2026. La clientèle doit migrer vers l’authentification OAuth 2.0 pour maintenir la connectivité. Cette modification affecte les deux connecteurs source et améliore la sécurité et la conformité aux normes d’authentification Salesforce. |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des sources](../../sources/home.md).
