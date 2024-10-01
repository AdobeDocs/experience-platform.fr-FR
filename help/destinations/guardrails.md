---
keywords: Experience Platform;activation;dépannage;mécanismes de sécurisation;instructions;limite
title: Barrières de sécurité par défaut pour l’activation des données
solution: Experience Platform
product: experience platform
type: Documentation
description: En savoir plus sur l’utilisation par défaut de l’activation des données et les limites de débit.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 3ff20e51458cb9cccafb6da92414def9eeaaf821
workflow-type: tm+mt
source-wordcount: '1686'
ht-degree: 50%

---

# Barrières de sécurité pour l’activation des données

>[!IMPORTANT]
>
>Vérifiez vos droits de licence dans votre commande de ventes et la [description du produit](https://helpx.adobe.com/fr/legal/product-descriptions.html) correspondante sur les limites d’utilisation réelles en plus de cette page de garde-fous.

Cette page fournit les limites d’utilisation et de débit par défaut en ce qui concerne le comportement d’activation. Lors de la révision des mécanismes de sécurisation suivants, on suppose que vous avez correctement [connecté aux destinations](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* La plupart des clients ne dépassent pas ces limites par défaut. Si vous souhaitez en savoir plus sur les limites personnalisées, contactez votre représentant de l’assistance clientèle.
>* Les limites décrites dans ce document sont constamment améliorées. Consultez régulièrement les mises à jour.
>* Selon les limites individuelles en aval, certaines destinations peuvent avoir des mécanismes de sécurisation plus stricts que ceux documentés sur cette page. Veillez également à vérifier la page du [catalogue](/help/destinations/catalog/overview.md) de la destination à laquelle vous vous connectez et activez les données.

## Types de protection {#limit-types}

Ce document comprend deux types de limites par défaut :

| Type de protection | Description |
|----------|---------|
| **Barrière de sécurité des performances (limite de soft)** | Les barrières de performance sont des limites d’utilisation liées à la portée de vos cas d’utilisation. Lorsque vous dépassez les barrières de performance, vous pouvez rencontrer une dégradation des performances et une latence. Adobe n’est pas responsable d’une telle dégradation des performances. Les clients qui dépassent systématiquement une barrière de performance peuvent choisir d’acquérir une capacité supplémentaire afin d’éviter une dégradation des performances. |
| **Barrières de sécurité système (limite stricte)** | Les barrières de sécurité appliquées par le système sont appliquées par l’interface utilisateur ou l’API de Real-Time CDP. Il s’agit de limites que vous ne pouvez pas dépasser, car l’interface utilisateur et l’API vous empêcheront de le faire ou renverront une erreur. |

{style="table-layout:auto"}


## Limites d’activation {#activation-limits}

Les barrières de sécurité suivantes fournissent des limites recommandées lors de l’activation des données Real-Time Customer Profile vers les destinations.

### Mécanismes de sécurisation générales de l’activation {#general-activation-guardrails}

Les mécanismes de sécurisation ci-dessous s’appliquent généralement à l’activation par le biais de [tous les types de destination](/help/destinations/destination-types.md#destination-types).

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal d’audiences vers une seule destination | 250 | Protecteur des performances | Il est recommandé de mapper un maximum de 250 audiences à une seule destination dans un flux de données. <br><br> Si vous devez activer plus de 250 audiences vers une destination, vous pouvez effectuer l’une des opérations suivantes : <ul><li> Dissociez les audiences que vous ne souhaitez plus activer, ou</li><li>Créez un nouveau flux de données vers la destination souhaitée et mappez les audiences à ce nouveau flux de données.</li></ul> <br> Notez que dans le cas de certaines destinations, vous pouvez être limité à moins de 250 audiences mappées à la destination. Ces destinations sont répertoriées plus bas sur la page, dans leurs sections respectives. |
| Nombre maximal d’attributs mappés vers une destination | 50 | Protecteur des performances | Dans le cas de plusieurs destinations et types de destination, vous pouvez sélectionner des attributs de profil et des identités à mapper pour l’exportation. Pour des performances optimales, un maximum de 50 attributs doit être mappé dans un flux de données vers une destination. |
| Nombre maximal de destinations | 100 | Barrière de sécurité mise en place par le système | Vous pouvez créer un maximum de 100 destinations auxquelles vous pouvez vous connecter et activer des données, *par sandbox*. Les [destinations de personnalisation Edge (personnalisation personnalisée)](#edge-destinations-activation) peuvent représenter un maximum de 10 sur les 100 destinations recommandées. |
| Type de données activées vers les destinations | Données de profil, y compris les identités et le mappage d’identités | Barrière de sécurité mise en place par le système | Actuellement, il n’est possible d’exporter que des *attributs d’enregistrement de profil* vers les destinations. Pour l’instant, les attributs XDM qui décrivent les données d’événement ne sont pas pris en charge pour l’exportation. |
| Type de données activées vers les destinations : prise en charge des attributs de tableau et de mappage | Non disponible | Barrière de sécurité mise en place par le système | À l’heure actuelle, il n’est **pas** possible d’exporter des *attributs de tableau ou de mappage* vers des destinations. L’exception à cette règle est le [mappage d’identités](/help/xdm/field-groups/profile/identitymap.md), qui est exporté à la fois dans les activations par flux et basées sur des fichiers. |

{style="table-layout:auto"}

### Activation de la diffusion en continu {#streaming-activation}

Les mécanismes de sécurisation ci-dessous s’appliquent à l’activation par le biais de [destinations de diffusion en continu](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre d’activations (messages HTTP avec export de profils) par seconde | S/O | - | Il n’existe actuellement aucune limite au nombre de messages par seconde envoyés par Experience Platform aux points d’entrée de l’API des destinations partenaires. <br> Toute limite ou latence est déterminée par le point d’entrée où Experience Platform envoie des données. Veillez également à vérifier la page [catalogue](/help/destinations/catalog/overview.md) de la destination à laquelle vous vous connectez et vers laquelle vous activez les données. |

{style="table-layout:auto"}

### Activation par lot (basée sur des fichiers) {#batch-file-based-activation}

Les mécanismes de sécurisation ci-dessous s’appliquent à l’activation par le biais de [destinations par lot (basées sur des fichiers)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Fréquence d’activation | Exportation complète quotidienne ou exportation incrémentielle plus fréquente toutes les 3, 6, 8 ou 12 heures. | Barrière de sécurité mise en place par le système | Consultez les sections de documentation [Exporter des fichiers complets](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) et [Exporter des fichiers incrémentiels](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) pour plus d’informations sur les incréments de fréquence pour les exportations par lots. |
| Nombre maximal d’audiences pouvant être exportées à une heure donnée | 100 | Protecteur des performances | Il est recommandé d’ajouter un maximum de 100 audiences aux flux de données de destination des lots. |
| Nombre maximum de lignes (enregistrements) par fichier à activer | 5 million | Barrière de sécurité mise en place par le système | Adobe Experience Platform fractionne automatiquement les fichiers exportés à raison de 5 millions d’enregistrements (lignes) par fichier. Chaque ligne représente un profil. Les noms de fichiers fractionnés sont ajoutés avec un nombre indiquant que le fichier fait partie d’une exportation plus importante, comme : `filename.csv`, `filename_2.csv`, `filename_3.csv`. Pour plus d’informations, reportez-vous à la [section de planification](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) du tutoriel d’activation des destinations par lot. |

{style="table-layout:auto"}

### Activation ad hoc {#ad-hoc-activation}

Les mécanismes de sécurisation ci-dessous s’appliquent à la méthode d’[activation ad hoc](/help/destinations/api/ad-hoc-activation-api.md).

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Audiences activées par tâche d’activation ad hoc | 80 | Barrière de sécurité mise en place par le système | Actuellement, chaque tâche d’activation ad hoc peut activer jusqu’à 80 audiences. Si vous tentez d’activer plus de 80 audiences par tâche, la tâche échouera. Ce comportement peut faire l’objet de modifications dans les prochaines versions. |
| Tâches d’activation ad hoc simultanées par audience | 1 | Barrière de sécurité mise en place par le système | N’exécutez pas plusieurs tâches d’activation ad hoc simultanées par audience. |

{style="table-layout:auto"}

### Activation des destinations de personnalisation Edge {#edge-destinations-activation}

Les mécanismes de sécurisation ci-dessous s’appliquent à l’activation par le biais des [Destinations de personnalisation Edge](/help/destinations/destination-types.md#advanced-enterprise-destinations).

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal de destinations de [Personnalisation personnalisée](/help/destinations/catalog/personalization/custom-personalization.md) | 10 | Protecteur des performances | Vous pouvez configurer des flux de données vers 10 destinations de personnalisation personnalisée par sandbox. |
| Nombre maximal d’attributs mappés à une destination de personnalisation par sandbox | 30 | Barrière de sécurité mise en place par le système | Un maximum de 30 attributs peuvent être mappés dans un flux de données à une destination de personnalisation, par sandbox. |
| Nombre maximal d’audiences mappées à une seule destination [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) | 50 | Protecteur des performances | Vous pouvez activer un maximum de 50 audiences dans un flux d’activation vers une seule destination Adobe Target. |

{style="table-layout:auto"}

### Exports de jeux de données {#dataset-exports}

Les exportations de jeux de données sont actuellement prises en charge dans un **[!UICONTROL premier complet, puis incrémentiel]** [modèle](/help/destinations/ui/export-datasets.md#scheduling). Les barrières de sécurité décrites dans cette section *s’appliquent à la première exportation complète* qui se produit après la configuration d’un workflow d’exportation de jeux de données.

<!--

| Guardrail | Limit | Limit Type | Description |
| --- | --- | --- | --- |
| Size of exported datasets | 5 billion records | Soft | The limit described here for dataset exports is a *soft guardrail*. For example, while the user interface will not block you from exporting datasets larger than 5 billion records, the behavior is unpredictable and exports might either fail or have very long export latency. |

{style="table-layout:auto"}

-->

#### Types de jeux de données {#dataset-types}

Les barrières de sécurité à l’exportation des jeux de données s’appliquent à deux types de jeux de données exportés depuis un Experience Platform, comme décrit ci-dessous :

**Jeux de données basés sur le schéma des événements d’expérience XDM**
Dans le cas de jeux de données basés sur le schéma d’événements d’expérience XDM, le schéma de jeu de données comprend une colonne de niveau supérieur *horodatage* . Les données sont ingérées de manière à ajouter uniquement.

**Jeux de données basés sur le schéma XDM Individual Profile**
Dans le cas de jeux de données basés sur le schéma XDM Individual Profile, le schéma de jeu de données n’inclut pas une colonne de niveau supérieur *horodatage*. Les données sont ingérées de manière positive.

La barrière de sécurité logicielle ci-dessous s’applique à tous les jeux de données exportés hors d’Experience Platform. Examinez également les garde-fous durs plus loin ci-dessous, spécifiques à différents types de jeux de données et de compression.

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Taille des jeux de données exportés | 5 milliards d’enregistrements | Protecteur des performances | La limite décrite ici pour les exportations de jeux de données est un *garde-fous souple*. Par exemple, bien que l’interface utilisateur ne vous empêche pas d’exporter des jeux de données de plus de 5 milliards d’enregistrements, le comportement est imprévisible et les exportations peuvent échouer ou présenter une latence d’exportation très longue. |

{style="table-layout:auto"}

#### Barrières de sécurité pour les exportations planifiées de jeux de données

Pour les exportations planifiées ou récurrentes de jeux de données, les barrières de sécurité ci-dessous sont identiques pour les deux formats du fichier exporté (JSON ou parquet) et sont regroupées par type de jeu de données.

>[!WARNING]
>
>Les exportations vers les fichiers JSON sont prises en charge en mode compressé uniquement.

| Type de jeu de données | Mécanisme de sécurisation | Type de protection | Description |
---------|----------|---------|-------|
| Jeux de données basés sur le **schéma des événements d’expérience XDM** | 365 derniers jours de données | Barrière de sécurité mise en place par le système | Les données de la dernière année civile sont exportées. |
| Jeux de données basés sur le **schéma XDM Individual Profile** | Dix milliards d’enregistrements sur tous les fichiers exportés dans un flux de données | Barrière de sécurité mise en place par le système | Le nombre d’enregistrements du jeu de données doit être inférieur à dix milliards pour les fichiers JSON ou parquet compressés et à un million pour les fichiers parquet non compressés. Dans le cas contraire, l’exportation échoue. Réduisez la taille du jeu de données que vous essayez d’exporter s’il est supérieur au seuil autorisé. |

{style="table-layout:auto"}

<!--

#### Ad-hoc dataset exports

Exporting datasets in an-hoc manner is currently supported via API only. For ad-hoc dataset exports, you must use the backfill parameter in the API to limit the timeframe of exported data. 

The guardrails below are the same whether you are exporting parquet of JSON files ad-hoc. 

**Parquet and JSON output**

|Dataset type | Backfill parameter provided | Guardrail | Guardrail type | Description |
|---------|---------|-----------|-----------|------------|
| Datasets based on the **XDM Experience Events schema** |  <p><ul><li>Both start and end date provided in `backfill` parameter in API call</li><li>Incomplete `backfill` parameter provided in API call</li></ul></p> | <p><ul><li>Last 30 days</li><li>Last 365 days</li></ul></p> | Hard | <p><ul><li>The export fails if the `startDate - endDate` interval is over 30 days</li><li>Either the `startDate` or `endDate` are missing or  incorrectly formatted in the API call. Expected format: `yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`</li></ul></p> |
| Datasets based on the **XDM Individual Profile schema** |  - | Ten billion records across all files exported in a dataflow | Hard | The record count of the dataset must be less than ten billion for compressed JSON or parquet files and one million for uncompressed parquet files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold. |

{style="table-layout:auto"}

-->

En savoir plus sur l’ [exportation de jeux de données](/help/destinations/ui/export-datasets.md).


### Mécanismes de sécurisation de Destination SDK {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) est une suite dʼAPI de configuration permettant de configurer des modèles dʼintégration de destination, afin quʼExperience Platform puisse envoyer des données dʼaudience et de profil à votre point dʼentrée, selon les formats de données et dʼauthentification choisis. Les mécanismes de sécurisation ci-dessous s’appliquent aux destinations que vous configurez à l’aide de Destination SDK.

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal de [destinations personnalisées privées](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Protecteur des performances | Vous pouvez créer un maximum de 5 destinations de diffusion en continu ou par lots privées à l’aide de Destination SDK. Contactez un représentant de l’assistance clientèle si vous devez créer plus de 5 destinations de ce type. |
| Politique d’exportation de profils pour Destination SDK | <ul><li>`maxBatchAgeInSecs` (1 800 minimum et 3 600 maximum)</li><li>`maxNumEventsInBatch` (1 000 minimum et 10 000 maximum)</li></ul> | Barrière de sécurité mise en place par le système | Lors de l’utilisation de l’option [agrégation configurable](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) pour votre destination, gardez à l’esprit les valeurs minimale et maximale qui déterminent la fréquence d’envoi des messages HTTP vers votre destination basée sur l’API et le nombre de profils que les messages doivent inclure. |

{style="table-layout:auto"}

### Politique de limitation et de reprise des destinations {#destination-throttling-and-retry-policy}

Détails sur les seuils de limitations ou les limites pour des destinations données. Cette section fournit également des informations sur la politique de reprise pour les destinations.

| Type de destination | Description |
| --- | --- |
| Destinations Grands comptes (API HTTP, Kinesis Amazon, Azure EventHubs) | Dans 95 % des cas, Experience Platform tente d’offrir une latence de débit inférieure à 10 minutes pour les messages envoyés avec succès, avec un taux de moins de 10 000 demandes par seconde pour chaque flux de données vers une destination Grands comptes. <br> En cas d’échec des requêtes vers la destination de votre entreprise, Experience Platform stocke les requêtes ayant échoué et tente à deux reprises d’envoyer les requêtes à votre point d’entrée. |

{style="table-layout:auto"}

## Étapes suivantes

Pour plus d’informations sur les barrières de sécurité des autres services Experience Platform, sur les informations de latence de bout en bout et les informations de licence des documents Description du produit Real-Time CDP, consultez la documentation suivante :

* [Barrières de sécurité Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagrammes de latence de bout en bout](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) pour divers services Experience Platform.
* [Real-Time Customer Data Platform (Édition B2C - Packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Packages Prime et Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Packages Prime et Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
