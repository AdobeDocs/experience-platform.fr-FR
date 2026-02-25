---
keywords: Experience Platform;activation;dépannage;mécanismes de sécurisation;instructions;limite
title: Mécanismes de sécurisation par défaut pour l’activation des données
solution: Experience Platform
product: experience platform
type: Documentation
description: En savoir plus sur l’utilisation par défaut de l’activation des données et les limites de débit.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: bdd0039249366ceabebe52694046ec01906ced3c
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 42%

---

# Mécanismes de sécurisation pour l’activation des données

>[!IMPORTANT]
>
>Vérifiez vos droits de licence dans votre commande client et la [Description du produit](https://helpx.adobe.com/fr/legal/product-descriptions.html) correspondante sur les limites d’utilisation réelles en plus de cette page de mécanismes de sécurisation.

Cette page fournit les limites d’utilisation et de débit par défaut en ce qui concerne le comportement d’activation. Lors de la révision des mécanismes de sécurisation suivants, on suppose que vous avez correctement [connecté aux destinations](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* La plupart des clients ne dépassent pas ces limites par défaut. Si vous souhaitez en savoir plus sur les limites personnalisées, contactez votre représentant de l’assistance clientèle.
>* Les limites décrites dans ce document sont constamment améliorées. Consultez régulièrement les mises à jour.
>* Selon les limites individuelles en aval, certaines destinations peuvent avoir des mécanismes de sécurisation plus stricts que ceux documentés sur cette page. Veillez également à vérifier la page du [catalogue](/help/destinations/catalog/overview.md) de la destination à laquelle vous vous connectez et activez les données.

## Types de mécanismes de sécurisation {#limit-types}

Ce document comprend deux types de limites par défaut :

| Type de mécanisme de sécurisation | Description |
|----------|---------|
| **Mécanisme de sécurisation des performances (limite soft)** | Les mécanismes de sécurisation de performances sont des limites d’utilisation liées à la portée de vos cas d’utilisation. Si vous dépassez les mécanismes de sécurisation des performances, vous pouvez rencontrer une dégradation des performances et une latence. Adobe n’est pas responsable de cette dégradation des performances. Les clients qui dépassent régulièrement un mécanisme de sécurisation des performances peuvent choisir de se procurer une licence pour une capacité supplémentaire afin d’éviter une dégradation des performances. |
| **Mécanismes de sécurisation appliqués par le système (limite Hard)** | Les mécanismes de sécurisation appliqués par le système sont appliqués par l’interface utilisateur ou l’API Real-Time CDP. Il s’agit de limites que vous ne pouvez pas dépasser, car l’interface utilisateur et l’API vous en empêcheront ou renverront une erreur. |

{style="table-layout:auto"}


## Limites d’activation {#activation-limits}

Les mécanismes de sécurisation suivants fournissent des limites recommandées lors de l’activation des données du profil client en temps réel vers les destinations.

### Mécanismes de sécurisation générales de l’activation {#general-activation-guardrails}

Les mécanismes de sécurisation ci-dessous s’appliquent généralement à l’activation par le biais de [tous les types de destination](/help/destinations/destination-types.md#destination-types).

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal d’audiences vers une seule destination | 250 | Mécanisme de sécurisation des performances | Il est recommandé de mapper un maximum de 250 audiences à une seule instance de destination. <br><br> Si vous devez activer plus de 250 audiences vers une destination, vous pouvez effectuer l’une des opérations suivantes : <ul><li> Annuler le mappage des audiences que vous ne souhaitez plus activer, ou</li><li>[Créez une instance de destination](ui/connect-destination.md) et mappez-y des audiences.</li></ul> <br> Notez que dans le cas de certaines destinations, vous pouvez être limité à moins de 250 audiences mappées à la destination. Ces destinations sont répertoriées plus bas sur la page, dans leurs sections respectives. |
| Nombre maximal d’attributs mappés vers une destination | 50 | Mécanisme de sécurisation des performances | Dans le cas de plusieurs destinations et types de destination, vous pouvez sélectionner des attributs de profil et des identités à mapper pour l’exportation. Pour des performances optimales, un maximum de 50 attributs doit être mappé à une instance de destination. |
| Nombre maximal de destinations | 100 | Mécanisme de sécurisation mis en œuvre par le système | Vous pouvez créer un maximum de 100 destinations auxquelles vous pouvez vous connecter et activer des données, *par sandbox*. Les [destinations de personnalisation Edge (personnalisation personnalisée)](#edge-destinations-activation) peuvent représenter un maximum de 10 sur les 100 destinations recommandées. |
| Type de données activées vers les destinations | Données de profil, y compris les identités et le mappage d’identités | Mécanisme de sécurisation mis en œuvre par le système | Actuellement, il n’est possible d’exporter que des *attributs d’enregistrement de profil* vers les destinations. Pour l’instant, les attributs XDM qui décrivent les données d’événement ne sont pas pris en charge pour l’exportation. |
| Type de données activées vers les destinations : prise en charge des attributs de tableau et de mappage | Partiellement disponible | Mécanisme de sécurisation mis en œuvre par le système | Vous pouvez exporter des attributs de tableau vers des [destinations basées sur des fichiers](/help/destinations/destination-types.md#file-based). [En savoir plus](/help/destinations/ui/export-arrays-maps-objects.md) à propos de la fonctionnalité. |

{style="table-layout:auto"}

### Activation de la diffusion en continu {#streaming-activation}

Les mécanismes de sécurisation ci-dessous s’appliquent à l’activation par le biais de [destinations de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre d’activations (messages HTTP avec export de profils) par seconde | S.O. | - | Il n’existe actuellement aucune limite au nombre de messages par seconde envoyés par Experience Platform aux points d’entrée de l’API des destinations partenaires. <br> Toute limite ou latence est déterminée par le point d’entrée où Experience Platform envoie des données. Veillez également à vérifier la page [catalogue](/help/destinations/catalog/overview.md) de la destination à laquelle vous vous connectez et vers laquelle vous activez les données. |

{style="table-layout:auto"}

### Activation par lot (basée sur des fichiers) {#batch-file-based-activation}

Les mécanismes de sécurisation ci-dessous s’appliquent à l’activation par le biais de [destinations par lot (basées sur des fichiers)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Fréquence d’activation | Exportation complète quotidienne ou exportation incrémentielle plus fréquente toutes les 3, 6, 8 ou 12 heures. | Mécanisme de sécurisation mis en œuvre par le système | Consultez les sections de documentation [Exporter des fichiers complets](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) et [Exporter des fichiers incrémentiels](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) pour plus d’informations sur les incréments de fréquence pour les exportations par lots. |
| Nombre maximal d’audiences pouvant être exportées à une heure donnée | 100 | Mécanisme de sécurisation des performances | Il est recommandé d’ajouter un maximum de 100 audiences aux instances de destination par lots. |
| Nombre maximum de lignes (enregistrements) par fichier à activer | 5 million | Mécanisme de sécurisation mis en œuvre par le système | Adobe Experience Platform fractionne automatiquement les fichiers exportés à raison de 5 millions d’enregistrements (lignes) par fichier. Chaque ligne représente un profil. Les noms de fichiers fractionnés sont ajoutés avec un nombre indiquant que le fichier fait partie d’une exportation plus importante, comme : `filename.csv`, `filename_2.csv`, `filename_3.csv`. Pour plus d’informations, reportez-vous à la [section de planification](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) du tutoriel d’activation des destinations par lot. |
| Nombre maximal d’audiences externes (par exemple, AEC, chargement personnalisé, composition de l’audience) pouvant être activées dans une instance de destination | 10 | Mécanisme de sécurisation mis en œuvre par le système | Lors de l’activation d’audiences externes (par exemple, [Composition d’audience fédérée](/help/segmentation/ui/audience-portal.md#fac), [chargement personnalisé](/help/segmentation/ui/audience-portal.md#import-audience), [Composition d’audience](/help/segmentation/ui/audience-portal.md#audience-composition)) vers des destinations basées sur des fichiers par lots, il existe une limite de 10 audiences de ce type que vous pouvez activer dans une instance de destination. Voir [Types et personnalisation d’audience](/help/segmentation/ui/audience-portal.md#customize) pour plus d’informations sur ces types d’audience. En savoir plus sur le workflow d’[activation des audiences externes vers des destinations basées sur des fichiers par lots](/help/destinations/ui/activate-batch-profile-destinations.md#select-audiences). |

{style="table-layout:auto"}

### Activation ad hoc {#ad-hoc-activation}

Les mécanismes de sécurisation ci-dessous s’appliquent à la méthode d’[activation ad hoc](/help/destinations/api/ad-hoc-activation-api.md).

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Audiences activées par traitement d’activation ad hoc | 80 | Mécanisme de sécurisation mis en œuvre par le système | Actuellement, chaque traitement d’activation ad hoc peut activer jusqu’à 80 audiences. Si vous tentez d’activer plus de 80 audiences par traitement, celui-ci échouera. Ce comportement peut faire l’objet de modifications dans les prochaines versions. |
| Traitements d’activation ad hoc simultanés par audience | 1 | Mécanisme de sécurisation mis en œuvre par le système | N’exécutez pas plusieurs traitements d’activation ad hoc simultanés par audience. |

{style="table-layout:auto"}

### Activation des destinations de personnalisation Edge {#edge-destinations-activation}

Les mécanismes de sécurisation ci-dessous s’appliquent à l’activation par le biais des [Destinations de personnalisation Edge](/help/destinations/destination-types.md#advanced-enterprise-destinations).

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal de destinations de [Personnalisation personnalisée](/help/destinations/catalog/personalization/custom-personalization.md) | 10 | Mécanisme de sécurisation des performances | Vous pouvez configurer un maximum de 10 instances de destination de personnalisation personnalisée par sandbox. |
| Nombre maximal d’attributs mappés à une destination de personnalisation par sandbox | 30 | Mécanisme de sécurisation des performances | Un maximum de 30 attributs peuvent être mappés à une instance de destination de personnalisation, par sandbox. |

{style="table-layout:auto"}

### Exportations de jeux de données {#dataset-exports}

Les exportations de jeux de données sont actuellement prises en charge selon un **[!UICONTROL First Full and then Incremental]** [modèle](/help/destinations/ui/export-datasets.md#scheduling). Les mécanismes de sécurisation décrits dans cette section *s’appliquent à la première exportation complète* qui se produit une fois qu’un workflow d’exportation de jeu de données est configuré.

<!--

| Guardrail | Limit | Limit Type | Description |
| --- | --- | --- | --- |
| Size of exported datasets | 5 billion records | Soft | The limit described here for dataset exports is a *soft guardrail*. For example, while the user interface will not block you from exporting datasets larger than 5 billion records, the behavior is unpredictable and exports might either fail or have very long export latency. |

{style="table-layout:auto"}

-->

#### Types de jeux de données {#dataset-types}

Les mécanismes de sécurisation de l’exportation des jeux de données s’appliquent à deux types de jeux de données exportés depuis Experience Platform, comme décrit ci-dessous :

**Jeux de données basés sur le schéma d’événements d’expérience XDM et jeux de données basés sur tout autre schéma**

Dans le cas des jeux de données basés sur le schéma d’événements d’expérience XDM, le schéma du jeu de données inclut une colonne d’horodatage de niveau supérieur. Les données sont ingérées en ajout uniquement. Dans le cas de jeux de données basés sur un autre schéma, le schéma du jeu de données peut inclure une colonne d’horodatage et les données sont ingérées en upsert.

Le mécanisme de sécurisation logiciel ci-dessous s’applique à tous les jeux de données exportés depuis Experience Platform. Examinez également les mécanismes de sécurisation stricts ci-dessous, spécifiques aux différents types de jeux de données et de compression.

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Taille des jeux de données exportés | 5 milliards d’enregistrements | Mécanisme de sécurisation des performances | La limite décrite ici pour les exportations de jeux de données est un *mécanisme de sécurisation souple*. Par exemple, bien que l’interface utilisateur ne vous empêche pas d’exporter des jeux de données de plus de 5 milliards d’enregistrements, le comportement est imprévisible et les exportations peuvent échouer ou présenter une latence d’exportation très longue. |

{style="table-layout:auto"}

#### Mécanismes de sécurisation pour les exportations de jeux de données planifiées

Pour les exportations de jeux de données planifiées ou récurrentes, les mécanismes de sécurisation ci-dessous sont identiques pour les deux formats du fichier exporté (JSON ou parquet) et sont regroupés par type de jeu de données.

>[!WARNING]
>
>Les exportations vers des fichiers JSON sont uniquement prises en charge en mode compressé.

| Type de jeu de données | Mécanisme de sécurisation | Type de mécanisme de sécurisation | Description |
|---------|----------|---------|-------|
| Jeux de données basés sur le schéma **XDM Experience Events** | 365 derniers jours de données | Mécanisme de sécurisation mis en œuvre par le système | Les données de la dernière année civile sont exportées. |
| Jeux de données basés sur **n’importe quel schéma à l’exception du schéma XDM Experience Events** | Dix milliards d’enregistrements sur tous les fichiers exportés dans une instance de destination | Mécanisme de sécurisation mis en œuvre par le système | Le nombre d’enregistrements du jeu de données doit être inférieur à dix milliards pour les fichiers JSON ou parquet compressés et à un million pour les fichiers parquet non compressés. Dans le cas contraire, l’exportation échouera. Réduisez la taille du jeu de données que vous essayez d’exporter s’il est supérieur au seuil autorisé. |

{style="table-layout:auto"}

<!--

#### Ad-hoc dataset exports

Exporting datasets in an-hoc manner is currently supported via API only. For ad-hoc dataset exports, you must use the backfill parameter in the API to limit the timeframe of exported data. 

The guardrails below are the same whether you are exporting parquet of JSON files ad-hoc. 

**Parquet and JSON output**

|Dataset type | Backfill parameter provided | Guardrail | Guardrail type | Description |
|---------|---------|-----------|-----------|------------|
| Datasets based on the **XDM Experience Events schema** |  <p><ul><li>Both start and end date provided in `backfill` parameter in API call</li><li>Incomplete `backfill` parameter provided in API call</li></ul></p> | <p><ul><li>Last 30 days</li><li>Last 365 days</li></ul></p> | Hard | <p><ul><li>The export fails if the `startDate - endDate` interval is over 30 days</li><li>Either the `startDate` or `endDate` are missing or  incorrectly formatted in the API call. Expected format: `yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`</li></ul></p> |
| Datasets based on the **XDM Individual Profile schema** |  - | Ten billion records across all files exported in a destination instance | Hard | The record count of the dataset must be less than ten billion for compressed JSON or parquet files and one million for uncompressed parquet files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold. |

{style="table-layout:auto"}

-->

En savoir plus sur l’[export de jeux de données](/help/destinations/ui/export-datasets.md).


### Mécanismes de sécurisation de Destination SDK {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) est une suite dʼAPI de configuration permettant de configurer des modèles dʼintégration de destination, afin quʼExperience Platform puisse envoyer des données dʼaudience et de profil à votre point dʼentrée, selon les formats de données et dʼauthentification choisis. Les mécanismes de sécurisation ci-dessous s’appliquent aux destinations que vous configurez à l’aide de Destination SDK.

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal de [destinations personnalisées privées](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Mécanisme de sécurisation des performances | Vous pouvez créer un maximum de 5 destinations de diffusion en continu ou par lots privées à l’aide de Destination SDK. Contactez un représentant de l’assistance clientèle si vous devez créer plus de 5 destinations de ce type. |
| Politique d’exportation de profils pour Destination SDK | <ul><li>`maxBatchAgeInSecs` (minimum 301 et maximum 3 600)</li><li>`maxNumEventsInBatch` (1 000 au minimum et 10 000 au maximum)</li></ul> | Mécanisme de sécurisation mis en œuvre par le système | Lors de l’utilisation de l’option [agrégation configurable](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) pour votre destination, gardez à l’esprit les valeurs minimale et maximale qui déterminent la fréquence d’envoi des messages HTTP vers votre destination basée sur l’API et le nombre de profils que les messages doivent inclure. |
| Durée de vie du jeton OAuth 2 pour Destination SDK | Minimum 24 heures recommandé | Mécanisme de sécurisation des performances | Pour les destinations qui utilisent l’autorisation [OAuth 2](/help/destinations/destination-sdk/functionality/destination-configuration/oauth2-authorization.md), Adobe recommande de définir les valeurs de durée de vie des jetons d’accès sur un minimum de 24 heures. Les connexions avec des jetons dont la durée de vie est inférieure à 1 heure entraînent la suppression de profils lors de l’activation. |

{style="table-layout:auto"}

### Politique de limitation et de reprise des destinations {#destination-throttling-and-retry-policy}

Détails sur les seuils de limitations ou les limites pour des destinations données. Cette section fournit également des informations sur la politique de reprise pour les destinations.

| Type de destination | Description |
| --- | --- |
| Destinations Grands comptes (API HTTP, Kinesis Amazon, Azure EventHubs) | Dans 95 % des cas, Experience Platform tente d’offrir une latence de débit inférieure à 10 minutes pour les messages envoyés avec succès, avec un taux de moins de 10 000 requêtes par seconde pour chaque instance de destination d’entreprise. <br> En cas d’échec des requêtes vers la destination de votre entreprise, Experience Platform stocke les requêtes ayant échoué et tente à deux reprises d’envoyer les requêtes à votre point d’entrée. |

{style="table-layout:auto"}

## Étapes suivantes

Consultez la documentation suivante pour plus d’informations sur les autres mécanismes de sécurisation des services Experience Platform, sur les informations de latence de bout en bout et les informations de licence dans les documents de description du produit Real-Time CDP :

* [Mécanismes de sécurisation de Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagrammes de latence de bout en bout](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) pour divers services Experience Platform.
* [Real-Time Customer Data Platform (B2C Edition - Packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Packages Prime et Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Packages Prime et Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
