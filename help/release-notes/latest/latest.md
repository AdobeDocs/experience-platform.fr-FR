---
title: Notes de mise à jour d’Adobe Experience Platform
description: Dernières notes de mise à jour pour Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 8e1f4d8cef1a962a056328417a1dbdff1aed2078
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 34%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de mise à jour : 25 mai 2022**

<!-- New features in Adobe Experience Platform: -->

<!-- - [Attribute-based access control](#abac) -->
<!-- - [Data hygiene](#hygiene) -->

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Alertes](#alerts)
- [Journaux d’audit](#audit-logs)
- [Tableaux de bord](#dashbaords)
- [Collecte de données](#data-collection)
<!-- - [Data Governance](#data-governance) -->
- [Préparation de données](#data-prep)
- [Destinations](#destinations)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Query Service](#query-service)
- [Sources](#sources)

## Alertes {#alerts}

Experience Platform vous permet de vous abonner à des alertes basées sur des événements pour diverses activités de Platform. Vous pouvez vous abonner à différentes règles d’alerte à l’aide de l’onglet [!UICONTROL Alertes] dans l’interface utilisateur de Platform. Vous pouvez aussi choisir de recevoir les messages d’alerte dans l’interface utilisateur elle-même ou par le biais de notifications par e-mail.

**Fonctionnalités mises à jour**

| Fonctionnalité | Règle d’alerte | Description |
| --- | --- | --- |
| Nouvelle règle d’alerte | Le taux de saut de page dépasse le seuil | Vous pouvez désormais utiliser l’alerte pour recevoir des notifications lorsque le flux de données de vos sources dépasse le seuil des identités. Consultez la présentation des [règles d’alerte](../../observability/alerts/rules.md) pour obtenir la liste mise à jour des types d’alerte. |

{style=&quot;table-layout:auto&quot;}


<!-- ## Attribute-based access control {#abac}

>[!IMPORTANT]
>
>Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released.

Attribute-based access control is a capability of Adobe Experience Platform that enables administrators to control access to specific objects and/or capabilities based on attributes. Attributes can be metadata added to an object, such as a label added to a schema field or segment. An administrator defines access policies that include attributes to manage user access permissions.

Through attribute-based access control, administrators of your organization can control users’ access to both sensitive personal data (SPD) and personally identifiable information (PII) across all Platform workflows and resources. Administrators can define user roles that have access only to specific fields and data that correspond to those fields.

| Feature | Description |
| --- | --- |
| Attribute-based access control | Attribute-based access control allows you to label Experience Data Model (XDM) schema fields with labels that define organizational or data usage scopes. In parallel, administrators can use the user and role administration interface to define access policies covering XDM schema fields and better manage the access given to users or groups of users (internal, external, or third-party users). Additionally, attribute-based access control allows administrators to manage access to specific segments. |
| Permissions | Permissions is the area of Experience Cloud where administrators can define user roles and access policies to manage access permissions for features and objects within a product application. Through Permissions, you can create and manage roles, as well as assign the desired resource permissions for these roles. Permissions also allow you to manage the labels, sandboxes, and users associated with a specific role. For more information, see the [Permissions UI guide](../../access-control/abac/ui/browse.md). |

For more information on attribute-based access control, see the [attribute-based access control overview](../../access-control/abac/overview.md). -->

<!-- ## Data hygiene {#hygiene}

Experience Platform provides a suite of data hygiene capabilities that allow you manage your stored data through programmatic deletions of consumer records and datasets. Using either the [!UICONTROL Data Hygiene] workspace in the UI or through calls to the Data Hygiene API, you can manage your data stores to ensure that information is used as expected, is updated when incorrect data needs fixing, and is deleted when organizational policies deem it necessary.

>[!IMPORTANT]
>
>Data hygiene capabilities are currently only available for organizations that have purchased the Adobe Shield for Healthcare add-on offering.

**New features**

| Feature | Description |
| --- | --- |
| Consumer deletion | [Delete consumer records](../../hygiene/ui/delete-consumer.md) from the data lake and Profile store based on primary identity data. |
| Time to live (TTL) for datasets | [Schedule TTLs](../../hygiene/ui/ttl.md) for Platform datasets.  |

For more information on audit logs in Platform, refer to the [data hygiene overview](../../hygiene/home.md). -->

## Journaux d’audit {#audit-logs}

Experience Platform vous permet d’auditer l’activité des utilisateurs pour plusieurs services et fonctionnalités. Les journaux d’audit fournissent des informations sur ce qui a été fait, par qui et à quel moment.

**Fonctionnalités mises à jour**

| Fonctionnalité | Nom | Description |
| --- | --- | --- |
| Ressources ajoutées | <ul><li> Stratégie de contrôle d’accès </li><li> Rôle </li><li> Journaux d’audit </li><li> Ordre de travail </li><li> Espace de noms d’identité </li><li> Graphique d’identités </li><li> Requête </li><li> Jeu de données </li><li> Flux de données source </li></ul> | Les ressources du journal d’audit sont automatiquement enregistrées au fur et à mesure que l’activité se produit. Si la fonction est activée, vous n’avez pas besoin d’activer manuellement la collecte des journaux. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur les journaux d’audit dans Platform, consultez la [présentation des journaux d’audit](../../landing/governance-privacy-security/audit-logs/overview.md).

## Tableaux de bord {#dashboards}

Adobe Experience Platform propose de nombreux tableaux de bord qui vous permettent d’afficher des informations importantes concernant les données de votre entreprise. Celles-ci sont présentées telles qu’elles sont capturées lors d’aperçus quotidiens.

### Tableaux de bord des profils

Le tableau de bord des profils affiche un instantané des données d’attribut (enregistrement) dont votre organisation dispose dans la banque de profils en Experience Platform.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Superposition des audiences par widget de stratégie de fusion | Ce widget affiche le croisement visuel des définitions de segment et vous permet d’optimiser la stratégie de segmentation en étudiant les similarités entre vos définitions de segment. |
| Les profils comptabilisent la tendance de changement par widget d’identité | Ces widgets vous aident à gérer vos besoins d’activation de destination en présentant le modèle de croissance des profils filtrés selon l’identité requise. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur les profils, voir [documentation du tableau de bord des profils](../../dashboards/guides/profiles.md).

### Tableaux de bord des destinations

Le tableau de bord des destinations affiche un instantané des destinations que votre entreprise a activées dans Experience Platform.

| Fonctionnalité | Description |
| --- | --- |
| Audiences activées par widget de destination | Ce widget vous aide à comprendre en un coup d’oeil la valeur de vos destinations en fonction du nombre d’audiences activées. Il permet également d’accéder facilement à des informations plus détaillées sur vos segments qui ont été mappés à la destination. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur les destinations, voir [documentation du tableau de bord des destinations](../../dashboards/guides/destinations.md).

### Tableaux de bord des segments

Le tableau de bord des segments fournit une interface utilisateur dans laquelle vous pouvez afficher des informations importantes sur vos segments, telles qu’elles sont capturées lors d’un instantané quotidien.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Widget de chevauchement d’audiences | Ce widget vous permet d’optimiser votre stratégie de segmentation en visualisant les similitudes dans les résultats de vos définitions de segment. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur les segments, reportez-vous à la section [documentation du tableau de bord des segments](../../dashboards/guides/segments.md).

## Collecte de données {#data-collection}

Experience Platform fournit une suite de technologies qui vous permet de collecter des données d’expérience client côté client et de les envoyer au réseau Adobe Experience Platform Edge où elles peuvent être enrichies, transformées et distribuées vers des destinations d’Adobe ou non Adobe.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| Copie de flux de données | [Création d’une copie d’un flux de données existant](../../edge/datastreams/overview.md#copy) et ajustez sa configuration selon les besoins, en évitant la nécessité de partir de zéro. |
| Importation des règles de mappage des jeux de données | Lors de la configuration de la préparation des données pour la collecte de données, vous pouvez [importer les règles de mappage d’un flux de données existant ;](../../edge/datastreams/data-prep.md#import-mapping) au lieu de configurer manuellement chaque mappage de champ. |
| Prise en charge du mappage de l’équipe de données pour le SDK Mobile | Vous pouvez désormais configurer la préparation des données pour la collecte de données dans les flux de données destinés à être utilisés avec le SDK Mobile Experience Platform. |
| Prise en charge du mappage de l’équipe de données pour les objets XDM | Mappage d’objets XDM en plus des objets de couche de données lors de [configuration de la préparation des données pour la collecte de données](../../edge/datastreams/data-prep.md#select-data). |
| Intégration aux flux de données | Utilisez le catalogue de sources dans Platform pour accéder à vos données sur Platform Edge Network, y compris la préparation des données pour la collecte de données et la prise en charge améliorée des avertissements relatifs à la préparation des données. Voir [Présentation de la source de collecte de données Adobe](../../sources/connectors/adobe-applications/data-collection.md) pour plus d’informations. |

Pour plus d’informations sur la collecte de données dans Platform, consultez la [Présentation de la collecte de données](../../collection/home.md).

<!-- ## Data Governance {#governance}

Adobe Experience Platform Data Governance is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**New features**

| Feature | Description | 
| ------- | ----------- |
| Consent policy enforcement (limited availability) | If your organization has purchased the Adobe Shield for Healthcare add-on offering, you can now [create consent policies](../../data-governance/policies/user-guide.md#consent-policy) to automatically [enforce customer consents and preferences in segment participation](../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation). |

{style="table-layout:auto"}

See the [Data Governance overview](../../data-governance/home.md) for more information on the service. -->

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| ------- | ----------- |
| Erreurs de données localisées | [!DNL Data Prep] localise désormais toutes les erreurs de transformation au niveau de l’attribut (précédemment au niveau de la ligne). Les flux de données ingèrent désormais des lignes partielles remplies de colonnes qui ne comportent aucune erreur de transformation, au lieu d’ignorer les lignes complètes. |
| Diffusion en continu des upserts vers [!DNL Profile Service] | Diffusion en continu de upserts avec [!DNL Data Prep] pour envoyer des mises à jour de lignes partielles au service de profil à l’aide de la variable [[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md), [[!DNL Azure Event Hubs]](../../sources/connectors/cloud-storage/eventhub.md)ou [[!DNL HTTP API]](../../sources/connectors/streaming/http.md) source. Consultez le guide sur la [upserts de diffusion en continu](../../data-prep/upserts.md) pour plus d’informations. |

{style=&quot;table-layout:auto&quot;}

<!-- | Attribute-based access control in [!DNL Data Prep] | You will now only be able to map attributes that you have access to. Attributes that you do not have access to can not be used in pass-through mappings and calculated fields. For more information, see [attribute-based access control in [!DNL Data Prep]](../../data-prep/home.md). **Note**: Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released. | -->

Pour plus d’informations sur la [!DNL Data Prep], consultez [[!DNL Data Prep] la présentation](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| ----------- | ----------- |
| Exporter les dernières qualifications de profil [après l’évaluation quotidienne des segments](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) | Vous pouvez désormais planifier une exportation de fichier complète, une fois ou quotidiennement, avec les dernières qualifications de profil, une fois l’évaluation quotidienne du segment terminée. |
| Identifiant de suivi de données facultatif pour [Destinations Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) | Pour activer la personnalisation Adobe Target pour les utilisateurs qui ne peuvent pas mettre en oeuvre le SDK Web Experience Platform, la sélection de l’identifiant de la banque de données est désormais facultative lors de la configuration des destinations Adobe Target. Lorsque vous n’utilisez pas de flux de données, les segments exportés d’Experience Platform vers Target ne prennent en charge que la personnalisation de session suivante, tandis que la segmentation Edge est désactivée, ainsi que toutes les [cas d’utilisation](../../destinations/ui/configure-personalization-destinations.md) qui dépendent de la segmentation edge. |

{style=&quot;table-layout:auto&quot;}

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types de clients par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Nouveaux composants XDM**

| Type de composant | Nom | Description |
| --- | --- | --- |
| Groupe de champs | [[!UICONTROL Modifier le jeu]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/changeset.schema.json) | Capture les modifications au niveau de la ligne des jeux de données et des jeux de données. Ce groupe de champs peut être utilisé par n’importe quelle classe. |
| Groupe de champs | [[!UICONTROL Clés de référence]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-reference-keys.schema.json) | Capture les clés de référence des schémas ExperienceEvent, ce qui vous permet de créer des relations avec des schémas basés sur d’autres classes. |

{style=&quot;table-layout:auto&quot;}

**Composants XDM mis à jour**

| Type de composant | Nom | Description de la mise à jour |
| --- | --- | --- |
| Comportement | [[!UICONTROL Schéma de série temporelle]](https://github.com/surbhi114/xdm/blob/master/components/behaviors/time-series.schema.json) | Mise à jour `eventType` pour inclure plusieurs nouveaux types d’événements liés aux médias et un cas d’utilisation entrant d’un canal web pour Adobe Journey Optimizer. |
| Schéma global | [[!UICONTROL Destination]](https://github.com/tumulurik/xdm/blob/master/schemas/destinations/destination.schema.json) | Valeurs d’énumération supprimées de `xdm:destinationCategory`. |
| Groupe de champs | [[!UICONTROL État d’enregistrement]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/record-status.schema.json) | Mise à jour de l’état du groupe de champs depuis `experimental` to `stable`. |
| Groupe de champs | (Plusieurs) | Plusieurs groupes de champs B2B ont été mis à jour afin que certains champs d’ID soient abandonnés au profit de champs de type clé qui utilisent la variable [[!UICONTROL Source B2B]](../../xdm/data-types/b2b-source.md) type de données. Les champs d’identifiant précédents seront abandonnés lors d’une prochaine mise à jour. Reportez-vous aux [requête d’extraction](https://github.com/adobe/xdm/pull/1533/files#diff-720c0bb1d1cbaf622f5656c2a4b62d35830c75f6563794da72a280a6a520fbc1) pour obtenir la liste complète des modifications apportées aux groupes de champs concernés. |
| Type de données | [[!UICONTROL Informations sur le navigateur]](https://github.com/liljenback/xdm/blob/master/components/datatypes/browserdetails.schema.json) | Ajout d’un nouveau champ `xdm:userAgentClientHints` qui capture les informations contextuelles sur l’agent utilisateur interagissant avec le navigateur. |
| Type de données | [[!UICONTROL Informations sur les médias]](https://github.com/lidiaist/xdm/blob/master/components/datatypes/media.schema.json) | Ajout d’une `xdm:playhead` pour capturer l’heure du curseur de lecture d’un contenu multimédia. Correction de la validation du modèle pour `xdm:videoSegment`. |
| Type de données | [[!UICONTROL Évaluation]](https://github.com/lidiaist/xdm/blob/master/components/datatypes/external/iptc/rating.schema.json) | `iptc4xmpExt:RatingSourceLink` n’est plus un champ obligatoire. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur XDM dans Platform, consultez la [présentation du système XDM](../../xdm/home.md).

## Query Service {#query-service}

Query Service vous permet d’utiliser le langage SQL standard pour interroger des données dans Adobe Experience Platform. [!DNL data lake]. Vous pouvez joindre n’importe quel jeu de données à partir du [!DNL data lake] et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, dans Data Science Workspace ou pour l’ingestion dans Real-time Customer Profile.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Intégration du journal d’audit de Query Service | L’intégration du journal d’audit de Query Service fournit des enregistrements des actions utilisateur liées aux requêtes dans le but de résoudre les problèmes ou de respecter les politiques de gestion des données d’entreprise et les exigences réglementaires. Voir [documentation sur l’intégration du journal d’audit](../../query-service/data-governance/audit-log-guide.md) pour obtenir des informations complètes |
| Conception SQL ALTER TABLE | Utilisez SQL pour définir des identités Principales dans un jeu de données ad hoc. Query Service vous permet de marquer les colonnes de jeux de données comme identités Principales ou secondaires directement via SQL à l’aide de la fonction `ALTER TABLE` . |

{style=&quot;table-layout:auto&quot;}

<!-- For more information on data governance in Query Service, see the [data governance overview](../../query-service/data-governance/overview.md). -->

Pour plus d’informations sur les fonctionnalités de Query Service, voir [Présentation de Query Service](../../query-service/home.md)

## Sources {#sources}

Adobe Experience Platform peut ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer ces données à l’aide des services de Platform. Vous pouvez ingérer des données à partir de diverses sources telles que les applications Adobe, le stockage dans le cloud, des logiciels tiers et votre système de gestion de la relation client.

Experience Platform fournit une API RESTful et une interface utilisateur interactive qui vous permet de configurer facilement des connexions source à différents fournisseurs de données. Ces connexions source vous permettent de vous authentifier et de vous connecter à des services de gestion de la relation client et à des systèmes de stockage externes, de définir des heures d’ingestion et de gérer le débit d’ingestion des données.

| Fonctionnalité | Description |
| --- | --- |
| Version bêta de [!DNL Zendesk] source | Utilisez la variable [!DNL Zendesk] source pour ingérer des données d’utilisateur, d’agent et d’organisation à partir de votre [!DNL Zendesk] instance pour [!DNL Profile] enrichissement. Voir [[!DNL Zendesk] présentation de la source](../../sources/connectors/customer-success/zendesk.md) pour plus d’informations. |
| Prise en charge de la collecte de données d’Adobe | Utilisez le catalogue de sources dans Platform pour accéder à vos données sur Platform Edge Network, y compris la préparation des données pour la collecte de données et la prise en charge améliorée des avertissements relatifs à la préparation des données. Voir [Présentation de la source de collecte de données Adobe](../../sources/connectors/adobe-applications/data-collection.md) pour plus d’informations. |
| Prise en charge de l’ingestion de fichiers avec `ISO-8859-1` encoding | Utilisez la variable `encoding` paramètre à ingérer `ISO-8859-1` fichiers codés avec une source de stockage dans le cloud vers Platform à l’aide de la méthode [!DNL Flow Service] API. Consultez le guide sur la [création d’une connexion source de stockage dans le cloud](../../sources/tutorials/api/collect/cloud-storage.md) pour plus d’informations. |

{style=&quot;table-layout:auto&quot;}

<!-- | Attribute-based access control in sources | You can now manage and control access to individual source fields and attributes during ingestion. **Note**: Attribute-based access control is currently available in a limited release for US-based healthcare customers. This capability will be available to all Real-time Customer Data Platform customers once it is fully released.  | -->

Pour en savoir plus sur les sources, consultez la [présentation des sources](../../sources/home.md).
