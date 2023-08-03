---
keywords: Experience Platform;activation;dépannage;mécanismes de sécurisation;instructions;limite
title: Mécanismes de sécurisation par défaut pour les données d’activation
solution: Experience Platform
product: experience platform
type: Documentation
description: En savoir plus sur l’utilisation par défaut de l’activation des données et les limites de débit.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: f360df6273986be35340432c72d8f8620f339b67
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 77%

---

# Mécanismes de sécurisation pour les données d’activation

Cette page fournit les limites d’utilisation et de débit par défaut en ce qui concerne le comportement d’activation. Lors de la révision des mécanismes de sécurisation suivants, on suppose que vous avez correctement [connecté aux destinations](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* La plupart des clients ne dépassent pas ces limites par défaut. Si vous souhaitez en savoir plus sur les limites personnalisées, contactez votre représentant de l’assistance clientèle.
>* Les limites décrites dans ce document sont constamment améliorées. Consultez régulièrement les mises à jour.
>* Selon les limites individuelles en aval, certaines destinations peuvent avoir des mécanismes de sécurisation plus stricts que ceux documentés sur cette page. Veillez également à vérifier la page du [catalogue](/help/destinations/catalog/overview.md) de la destination à laquelle vous vous connectez et activez les données.

## Types de limite {#limit-types}

Ce document comprend deux types de limites par défaut :

* **Limite soft :** il est possible d’aller au-delà d’une limite soft, cependant ces limites fournissent une orientation recommandée pour les performances du système.
* **Limite Hard :** une limite Hard fournit un maximum absolu. L’interface utilisateur ou l’API d’Experience Platform ne vous permet pas de franchir cette limite. Une erreur sera renvoyée si vous la dépassez.


## Limites d’activation {#activation-limits}

Les barrières de sécurité suivantes fournissent des limites recommandées lors de l’activation des données Real-Time Customer Profile vers les destinations.

### Mécanismes de sécurisation générales de l’activation {#general-activation-guardrails}

Les mécanismes de sécurisation ci-dessous s’appliquent généralement à l’activation par le biais de [tous les types de destination](/help/destinations/destination-types.md#destination-types).

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal d’audiences vers une seule destination | 250 | Soft | Il est recommandé de mapper un maximum de 250 audiences à une seule destination dans un flux de données. <br><br> Si vous devez activer plus de 250 audiences vers une destination, vous pouvez effectuer l’une des opérations suivantes : <ul><li> Dissociez les audiences que vous ne souhaitez plus activer, ou</li><li>Créez un nouveau flux de données vers la destination souhaitée et mappez les audiences à ce nouveau flux de données.</li></ul> <br> Notez que dans le cas de certaines destinations, vous pouvez être limité à moins de 250 audiences mappées à la destination. Ces destinations sont répertoriées plus bas sur la page, dans leurs sections respectives. |
| Nombre maximal de destinations | 100 | Soft | Il est recommandé de créer un maximum de 100 destinations auxquelles vous pouvez connecter et activer des données *par sandbox*. Les [destinations de personnalisation Edge (personnalisation personnalisée)](#edge-destinations-activation) peuvent représenter un maximum de 10 sur les 100 destinations recommandées. |
| Nombre maximal d’attributs mappés vers une destination | 50 | Soft | Dans le cas de plusieurs destinations et types de destination, vous pouvez sélectionner des attributs de profil et des identités à mapper pour l’exportation. Pour des performances optimales, un maximum de 50 attributs doit être mappé dans un flux de données vers une destination. |
| Type de données activées vers les destinations | Données de profil, y compris les identités et le mappage d’identités | Hard | Actuellement, il n’est possible d’exporter que des *attributs d’enregistrement de profil* vers les destinations. Pour l’instant, les attributs XDM qui décrivent les données d’événement ne sont pas pris en charge pour l’exportation. |
| Type de données activées vers les destinations : prise en charge des attributs de tableau et de mappage | Non disponible | Hard | À l’heure actuelle, il n’est **pas** possible d’exporter des *attributs de tableau ou de mappage* vers des destinations. L’exception à cette règle est le [mappage d’identités](/help/xdm/field-groups/profile/identitymap.md), qui est exporté à la fois dans les activations par flux et basées sur des fichiers. |

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
| Fréquence d’activation | Exportation complète quotidienne ou exportation incrémentielle plus fréquente toutes les 3, 6, 8 ou 12 heures. | Hard | Consultez les sections de documentation [Exporter des fichiers complets](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) et [Exporter des fichiers incrémentiels](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) pour plus d’informations sur les incréments de fréquence pour les exportations par lots. |
| Nombre maximal d’audiences pouvant être exportées à une heure donnée | 100 | Soft | Il est recommandé d’ajouter un maximum de 100 audiences aux flux de données de destination des lots. |
| Nombre maximum de lignes (enregistrements) par fichier à activer | 5 million | Hard | Adobe Experience Platform fractionne automatiquement les fichiers exportés à raison de 5 millions d’enregistrements (lignes) par fichier. Chaque ligne représente un profil. Les noms de fichiers fractionnés sont ajoutés avec un nombre indiquant que le fichier fait partie d’une exportation plus importante, comme : `filename.csv`, `filename_2.csv`, `filename_3.csv`. Pour plus d’informations, reportez-vous à la [section de planification](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) du tutoriel d’activation des destinations par lot. |

{style="table-layout:auto"}

### Activation ad hoc {#ad-hoc-activation}

Les mécanismes de sécurisation ci-dessous s’appliquent à la méthode d’[activation ad hoc](/help/destinations/api/ad-hoc-activation-api.md).

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Audiences activées par tâche d’activation ad hoc | 80 | Hard | Actuellement, chaque tâche d’activation ad hoc peut activer jusqu’à 80 audiences. Si vous tentez d’activer plus de 80 audiences par tâche, la tâche échouera. Ce comportement peut faire l’objet de modifications dans les prochaines versions. |
| Tâches d’activation ad hoc simultanées par audience | 1 | Hard | N’exécutez pas plusieurs tâches d’activation ad hoc simultanées par audience. |

{style="table-layout:auto"}

### Activation des destinations de personnalisation Edge {#edge-destinations-activation}

Les mécanismes de sécurisation ci-dessous s’appliquent à l’activation par le biais des [Destinations de personnalisation Edge](/help/destinations/destination-types.md#streaming-profile-export).

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal de destinations de [Personnalisation personnalisée](/help/destinations/catalog/personalization/custom-personalization.md) | 10 | Soft | Vous pouvez configurer des flux de données vers 10 destinations de personnalisation personnalisée par sandbox. |
| Nombre maximal d’attributs mappés à une destination de personnalisation par sandbox | 30 | Hard | Un maximum de 30 attributs peuvent être mappés dans un flux de données à une destination de personnalisation, par sandbox. |
| Nombre maximal d’audiences mappées à une seule [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) destination | 50 | Soft | Vous pouvez activer un maximum de 50 audiences dans un flux d’activation vers une seule destination Adobe Target. |

{style="table-layout:auto"}

## [!BADGE Beta]Exports de jeux de données {type=Informative} {#dataset-exports}

Les exportations de jeux de données sont actuellement prises en charge dans une **[!UICONTROL Premier Complet puis Incrémentiel]** [pattern](/help/destinations/ui/export-datasets.md#scheduling). Les barrières de sécurité décrites dans cette section s’appliquent au premier export complet qui se produit après la configuration d’un workflow d’exportation de jeux de données.

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Taille des jeux de données exportés | 5 milliards d’enregistrements | Soft | La limite décrite ici pour les exportations de jeux de données est une *garde-fou souple*. Par exemple, bien que l’interface utilisateur ne vous empêche pas d’exporter des jeux de données de plus de 5 milliards d’enregistrements, le comportement est imprévisible et les exportations peuvent échouer ou présenter une latence d’exportation très longue. |

{style="table-layout:auto"}

<!--

### Dataset Types {#dataset-types}

Datasets exported from Experience Platform can be of two types, as described below:

**Timeseries**
Timeseries datasets are also known as *XDM Experience Events* datasets in Experience Platform terminology.
The dataset schema includes a top level *timestamp* column. Data is ingested in an append-only fashion.

**Record** 
Record datasets are also known as *XDM Individual Profile* datasets in Experience Platform terminology.
The dataset schema does not include a top level *timestamp* column. Data is ingested in upsert fashion.

The guardrails below are grouped by the format of the exported file, and then further by dataset type.

**Parquet output**

|Dataset type | Compression | Guardrail | Description |
|---------|----------|---------|-----------|
| Timeseries | N/A | Last seven days per file | The data from the last seven days only is exported. |
| Record | N/A | Five billion records per file | Only the data from the last seven days is exported. |

{style="table-layout:auto"}

**JSON output**

|Dataset type | Compression | Guardrail | Description |
|---------|----------|---------|-----------|
| Timeseries | N/A | Last seven days per file | The data from the last seven days only is exported. |
| <p>Record</p> | <p><ul><li>Yes</li><li>No</li></ul></p> | <p><ul><li>Five billion records per compressed file</li><li>One million records per uncompressed file</li></ul></p> | <p>The record count of the dataset must be less than five billion for compressed files and one million for uncompressed files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</p> |

{style="table-layout:auto"}

-->

<!--

<table>
<thead>
  <tr>
    <th>Output format</th>
    <th>Dataset type</th>
    <th>Compression</th>
    <th>Guardrail</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Parquet</td>
    <td>Timeseries</td>
    <td>-</td>
    <td>Last seven days per file</td>
    <td>Only the data from the last seven days is exported.</td>
  </tr>
  <tr>
    <td>Record</td>
    <td>-</td>
    <td>Five billion records per file</td>
    <td>The record count of the dataset must be less than five billion, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
  <tr>
    <td rowspan="3">JSON</td>
    <td>Timeseries</td>
    <td>-</td>
    <td>Last seven days per file</td>
    <td>Only the data from the last seven days is exported.</td>
  </tr>
  <tr>
    <td rowspan="2">Record</td>
    <td>Yes</td>
    <td>Five billion records per file</td>
    <td>The record count of the dataset must be less than five billion, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
  <tr>
    <td>No</td>
    <td>One million records per file</td>
    <td>The record count of the dataset must be less than one million, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
</tbody>
</table>

-->

### Mécanismes de sécurisation de Destination SDK {#destination-sdk-guardrails}

[Destination SDK](/help/destinations/destination-sdk/overview.md) est une suite dʼAPI de configuration permettant de configurer des modèles dʼintégration de destination, afin quʼExperience Platform puisse envoyer des données dʼaudience et de profil à votre point dʼentrée, selon les formats de données et dʼauthentification choisis. Les mécanismes de sécurisation ci-dessous s’appliquent aux destinations que vous configurez à l’aide de Destination SDK.

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --- | --- | --- | --- |
| Nombre maximal de [destinations personnalisées privées](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Soft | Vous pouvez créer un maximum de 5 destinations de diffusion en continu ou par lots privées à l’aide de Destination SDK. Contactez un représentant de l’assistance clientèle si vous devez créer plus de 5 destinations de ce type. |
| Politique d’exportation de profils pour Destination SDK | <ul><li>`maxBatchAgeInSecs` (1 800 au minimum et 3 600 au maximum)</li><li>`maxNumEventsInBatch` (1 000 au minimum, 10 000 au maximum)</li></ul> | Hard | Lors de l’utilisation de l’option [agrégation configurable](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) pour votre destination, gardez à l’esprit les valeurs minimale et maximale qui déterminent la fréquence d’envoi des messages HTTP vers votre destination basée sur l’API et le nombre de profils que les messages doivent inclure. |

{style="table-layout:auto"}

### Politique de limitation et de reprise des destinations {#destination-throttling-and-retry-policy}

Détails sur les seuils de limitations ou les limites pour des destinations données. Cette section fournit également des informations sur la politique de reprise pour les destinations.

| Type de destination | Description |
| --- | --- |
| Destinations Grands comptes (API HTTP, Kinesis Amazon, Azure EventHubs) | Dans 95 % des cas, Experience Platform tente d’offrir une latence de débit inférieure à 10 minutes pour les messages envoyés avec succès, avec un taux de moins de 10 000 demandes par seconde pour chaque flux de données vers une destination Grands comptes. <br> En cas d’échec des requêtes vers la destination de votre entreprise, Experience Platform stocke les requêtes ayant échoué et tente à deux reprises d’envoyer les requêtes à votre point d’entrée. |

{style="table-layout:auto"}

## Mécanismes de sécurisation pour les autres services Experience Platform {#guardrails-other-services}

Consultez les informations sur les mécanismes de sécurisation pour d’autres services Experience Platform :

* Mécanismes de sécurisation pour l’[ingestion des données](/help/ingestion/guardrails.md)
* Mécanismes de sécurisation pour les [[!DNL Identity Service] données](/help/identity-service/guardrails.md)
* Mécanismes de sécurisation pour les [[!DNL Real-Time Customer Profile] données](/help/profile/guardrails.md)
* Mécanismes de sécurisation pour les [[!DNL Query Service] données](/help/query-service/guardrails.md)
