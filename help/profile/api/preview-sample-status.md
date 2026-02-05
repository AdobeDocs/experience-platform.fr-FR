---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;prévisualisation;exemple
title: Prévisualiser l’exemple de point d’entrée de l’API Statut (Aperçu du profil)
description: Le point d’entrée d’aperçu de statut d’échantillon de l’API Real-Time Customer Profile vous permet de prévisualiser le dernier exemple réussi de vos données de profil, de répertorier la distribution des profils par jeu de données et par identité et de générer des rapports présentant le chevauchement des jeux de données, le chevauchement des identités et les profils désassemblés.
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: 399b76f260732015f691fd199c977d6f7e772b01
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 6%

---

# Prévisualiser l’exemple de point d’entrée de statut (aperçu du profil)

Adobe Experience Platform vous permet d’ingérer des données client provenant de plusieurs sources afin de créer un profil robuste et unifié pour chacun de vos clients. Lorsque les données sont ingérées dans Experience Platform, un exemple de tâche est exécuté pour mettre à jour le nombre de profils et d’autres mesures liées aux données du profil client en temps réel.

Les résultats de cet exemple de tâche peuvent être affichés à l’aide du point d’entrée `/previewsamplestatus`, qui fait partie de l’API Real-Time Customer Profile. Ce point d’entrée peut également être utilisé pour répertorier les distributions de profils à la fois par jeu de données et espace de noms d’identité, ainsi que pour générer plusieurs rapports afin de bénéficier d’une meilleure visibilité sur la composition de la banque de profils de votre organisation. Ce guide décrit les étapes requises pour afficher ces mesures à l’aide du point d’entrée de l’API `/previewsamplestatus`.

>[!NOTE]
>
>Des points d’entrée d’estimation et de prévisualisation sont disponibles dans le cadre de l’API Segmentation Service de Adobe Experience Platform. Ils vous permettent d’afficher des informations de niveau résumé concernant les définitions de segment afin de vous assurer que vous isolez l’audience prévue. Pour obtenir des instructions détaillées sur l’utilisation des points d’entrée de prévisualisation et d’estimation, consultez le guide de [prévisualisations et points d’entrée des estimations](../../segmentation/api/previews-and-estimates.md), qui fait partie du guide de développement de l’API [!DNL Segmentation].

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de lʼ [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Fragments de profil contre profils fusionnés

Ce guide fait référence à la fois aux « fragments de profil » et aux « profils fusionnés ». Il est important de comprendre la différence entre ces termes avant de continuer.

Chaque profil client est composé de plusieurs fragments de profil qui ont été fusionnés dans le but de former une vue unique de ce client ou cette cliente. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre organisation dispose probablement de plusieurs fragments de profil associés à ce client unique apparaissant dans plusieurs jeux de données.

Lorsque des fragments de profil sont ingérés dans Experience Platform, ils sont fusionnés (en fonction d’une politique de fusion) afin de créer un profil unique pour ce client. Par conséquent, il est probable que le nombre total de fragments de profil soit toujours supérieur au nombre total de profils fusionnés, chaque profil étant composé de fragments multiples.

Pour en savoir plus sur les profils et leur rôle dans Experience Platform, commencez par lire la [présentation du profil client en temps réel](../home.md).

## Déclenchement de l’exemple de traitement

Lorsque les données activées pour le profil client en temps réel sont ingérées dans [!DNL Experience Platform], elles sont stockées dans la banque de données Profile. Lorsque l’ingestion d’enregistrements dans la banque de profils augmente ou réduit le nombre total de profils de plus de 3 %, une tâche d’échantillonnage est déclenchée pour mettre à jour le nombre. Le déclenchement de l’échantillon dépend du type d’ingestion utilisé :

* Pour les **workflows de données en flux continu**, une vérification est effectuée toutes les heures pour déterminer si le seuil d’augmentation ou de diminution de 3 % a été atteint. Si c’est le cas, un exemple de tâche est automatiquement déclenché pour mettre à jour le décompte.
* Pour l’**ingestion par lots**, dans les 15 minutes suivant l’ingestion réussie d’un lot dans la banque de profils, si le seuil d’augmentation ou de diminution de 3 % est atteint, une tâche est exécutée pour mettre à jour le nombre. À l’aide de l’API Profile, vous pouvez prévisualiser le dernier exemple de tâche réussie, ainsi que répertorier la distribution des profils par jeu de données et par espace de noms d’identité.

Les mesures nombre de profils et profils par espace de noms sont également disponibles dans la section [!UICONTROL Profiles] de l’interface utilisateur d’Experience Platform. Pour plus d’informations sur l’accès aux données de profil à l’aide de l’interface utilisateur, consultez le [[!DNL Profile] guide de l’interface utilisateur](../ui/user-guide.md).

## Afficher le dernier statut d’échantillon {#view-last-sample-status}

Vous pouvez afficher les détails du dernier exemple de tâche réussie exécuté pour votre organisation en envoyant une requête GET au point d’entrée `/previewsamplestatus`. Ce rapport inclut le nombre total de profils dans l’exemple, ainsi que la mesure du nombre de profils ou le nombre total de profils de votre organisation dans Experience Platform.

Le nombre de profils est généré après la fusion de fragments de profil afin de former un seul profil pour chaque client individuel. En d’autres termes, lorsque des fragments de profil sont fusionnés, ils renvoient un nombre de « 1 » profil, car ils sont tous liés à la même personne.

Le nombre de profils inclut également les profils avec attributs (données d’enregistrement) ainsi que les profils contenant uniquement des données de série temporelle (événement), tels que les profils Adobe Analytics. L’exemple de tâche est actualisé régulièrement au fur et à mesure de l’ingestion des données de profil afin de fournir un nombre total de profils à jour dans Experience Platform.

**Format d’API**

```http
GET /previewsamplestatus
```

**Requête**

+++ Exemple de requête pour afficher le dernier statut d’échantillon.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 et inclut les détails du dernier exemple de traitement réussi exécuté pour l’organisation.

+++ Exemple de réponse contenant le dernier statut d’échantillon.

>[!NOTE]
>
>Dans cet exemple de réponse, `numRowsToRead` et `totalRows` sont égales l’une à l’autre. Cela peut être le cas selon le nombre de profils de votre entreprise dans Experience Platform. Cependant, ces deux nombres sont généralement différents, `numRowsToRead` étant le plus petit car il représente l’échantillon comme un sous-ensemble du nombre total de profils (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "docCount": "\"300803\"",
  "totalFragmentCount": 47429,
  "lastSuccessfulBatchTimestamp": "\"null\"",
  "streamingDriven": "\"false\"",
  "totalRows": "41003",
  "lastBatchId": "\"null\"",
  "status": "TASK_FINISHED",
  "samplingRatio": 1.0,
  "mergeStrategy": "timestampOrdered_auto",
  "lastSampledTimestamp": "2020-08-01 17:57:57.0"
}
```

| Propriété | Description |
| -------- | ----------- |
| `numRowsToRead` | Nombre total de profils fusionnés dans l’échantillon. |
| `sampleJobRunning` | Valeur booléenne qui renvoie un `true` lorsqu’un exemple de tâche est en cours. Fournit une transparence sur la latence qui se produit lorsqu’un fichier de commandes est chargé vers lorsqu’il est réellement ajouté à la banque de profils. |
| `docCount` | Nombre total de documents dans la base de données. |
| `totalFragmentCount` | Nombre total de fragments de profil dans la banque de profils. |
| `lastSuccessfulBatchTimestamp` | Date et heure de la dernière ingestion par lots réussie. |
| `streamingDriven` | *Ce champ est obsolète et n’a aucune importance pour la réponse.* |
| `totalRows` | Nombre total de profils fusionnés dans Experience Platform, également appelé nombre de profils. |
| `lastBatchId` | ID de la dernière ingestion par lots. |
| `status` | Statut du dernier échantillon. |
| `samplingRatio` | Rapport entre les profils fusionnés échantillonnés (`numRowsToRead`) et le total des profils fusionnés (`totalRows`), exprimé en pourcentage au format décimal. |
| `mergeStrategy` | Stratégie de fusion utilisée dans l’exemple. |
| `lastSampledTimestamp` | Dernier exemple d’horodatage réussi. |

+++

## Répertorier la distribution des profils par jeu de données

Vous pouvez voir la répartition des profils par jeu de données en adressant une requête GET au point d’entrée `/previewsamplestatus/report/dataset`.

**Format d’API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Paramètre de requête | Description | Exemple |
| --------------- | ----------- | ------- |
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à cette date, le rapport le plus récent pour cette date est renvoyé. Si aucun rapport n’existe pour la date spécifiée, une erreur 404 (Introuvable) est renvoyée. Si aucune date n’est spécifiée, le rapport le plus récent est renvoyé. Format : AAAA-MM-JJ. | `date=2024-12-31` |

**Requête**

La requête suivante utilise le paramètre `date` pour renvoyer le rapport le plus récent pour la date spécifiée.

+++ Exemple de requête pour récupérer la distribution des profils par jeu de données.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Réponse**

>[!NOTE]
>
>S’il existe plusieurs rapports pour la date, seul le dernier rapport est renvoyé. Si aucun rapport de jeu de données n’existe pour la date fournie, le statut HTTP 404 (Not Found) est renvoyé.

Une réponse réussie renvoie un état HTTP 200 et inclut un tableau `data`, contenant une liste d’objets de jeu de données.

+++ Exemple de réponse contenant les derniers objets de jeu de données.

>[!NOTE]
>
>La réponse suivante affichée a été tronquée pour afficher trois jeux de données.

```json
{
  "data": [
    {
      "sampleCount": 12577,
      "samplePercentage": 0.306734,
      "fullIDsCount": 20988,
      "fullIDsPercentage": 0.511865,
      "name": "CRM Profiles",
      "description": "Profiles from the CRM.",
      "value": "5f160106be34361915754b9c",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697",
    },
    {
      "sampleCount": 12938,
      "samplePercentage": 0.315538,
      "fullIDsCount": 21796,
      "fullIDsPercentage": 0.531571,
      "name": "AAM Authenticated Profiles",
      "description": "This data set contains AAM authenticated profiles.",
      "value": "5dc77ec6eed47f18a796ca90",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    },
    {
      "sampleCount": 22725,
      "samplePercentage": 0.554228,
      "fullIDsCount": 41003,
      "fullIDsPercentage": 1.0,
      "name": "Loyalty Program Members",
      "description": "Members of the loyalty program at all levels.",
      "value": "5d0fda92274e55144d4de620",
      "streamingIngestionEnabled": "",
      "createdUser": "{CREATED_USER}",
      "reportTimestamp": "2020-08-01T17:57:58.697"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Propriété | Description |
| -------- | ----------- |
| `sampleCount` | Nombre total de profils fusionnés échantillonnés avec cet identifiant de jeu de données. |
| `samplePercentage` | Le `sampleCount` en tant que pourcentage du nombre total de profils fusionnés échantillonnés (la valeur de `numRowsToRead` telle qu’elle est renvoyée dans le [dernier statut d’échantillon](#view-last-sample-status)), exprimé au format décimal. |
| `fullIDsCount` | Nombre total de profils fusionnés avec cet identifiant de jeu de données. |
| `fullIDsPercentage` | Le `fullIDsCount` en tant que pourcentage du nombre total de profils fusionnés (la valeur `totalRows` telle qu’elle est renvoyée dans le [dernier statut d’échantillon](#view-last-sample-status)), exprimé au format décimal. |
| `name` | Nom du jeu de données, tel qu’il est fourni lors de la création du jeu de données. |
| `description` | Description du jeu de données fournie lors de la création du jeu de données. |
| `value` | Identifiant du jeu de données. |
| `streamingIngestionEnabled` | Indique si le jeu de données est activé pour l’ingestion en flux continu. |
| `createdUser` | ID de l’utilisateur qui a créé le jeu de données. |
| `reportTimestamp` | Date et heure du rapport. Si un paramètre de `date` a été fourni pendant la requête, le rapport renvoyé porte sur la date fournie. Si aucun paramètre `date` n’est fourni, le rapport le plus récent est renvoyé. |

+++

## Répartition des profils de liste par espace de noms d’identité

Vous pouvez envoyer une requête GET au point d’entrée `/previewsamplestatus/report/namespace` pour afficher la répartition par espace de noms d’identité pour tous les profils fusionnés de votre banque de profils. Cela inclut les identités standard fournies par Adobe, ainsi que les identités personnalisées définies par votre organisation.

Les espaces de noms d’identité sont des composants importants du Adobe Experience Platform Identity Service qui servent d’indicateurs du contexte auquel les données client se rapportent. Pour en savoir plus, commencez par lire la [présentation des espaces de noms d’identité](../../identity-service/features/namespaces.md).

>[!NOTE]
>
>Le nombre total de profils par espace de noms (en additionnant les valeurs affichées pour chaque espace de noms) peut être supérieur à la mesure du nombre de profils, car un profil peut être associé à plusieurs espaces de noms. Par exemple, si un client ou une cliente interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à cette personne.

**Format d’API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Paramètre de requête | Description | Exemple |
| --------------- | ----------- | ------- |
| `date` | Spécifie la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à cette date, le rapport le plus récent pour cette date est renvoyé. Si aucun rapport n’existe pour la date spécifiée, une erreur 404 (Introuvable) est renvoyée. Si aucune date n’est spécifiée, le rapport le plus récent est renvoyé. Format : `YYYY-MM-DD`. | `date=2025-6-20` |

**Requête**

La requête suivante ne spécifie aucun paramètre `date` et renvoie le rapport le plus récent.

+++ Exemple de requête pour renvoyer le rapport le plus récent pour la distribution de profils par espace de noms. 

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 et inclut un tableau `data`, avec des objets individuels contenant les détails de chaque espace de noms. La réponse affichée a été tronquée afin d’afficher quatre espaces de noms.

+++ Un exemple de réponse contient des informations sur la distribution des profils par espace de noms.

```json
{
  "data": [
    {
      "sampleCount": 12148,
      "samplePercentage": 0.296271,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 13141,
      "fullIDsCount": 12631,
      "fullIDsPercentage": 0.308051,
      "code": "Email",
      "value": "6"
    },
    {
      "sampleCount": 6989,
      "samplePercentage": 0.170451,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 7543,
      "fullIDsCount": 7042,
      "fullIDsPercentage": 0.171744,
      "code": "ECID",
      "value": "4"
    },
    {
      "sampleCount": 888,
      "samplePercentage": 0.021657,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 3801,
      "fullIDsCount": 3206,
      "fullIDsPercentage": 0.078189,
      "code": "AAID",
      "value": "10"
    },
    {
      "sampleCount": 21809,
      "samplePercentage": 0.531888,
      "reportTimestamp": "2020-08-01T17:57:58.697",
      "fullIDsFragmentCount": 27023,
      "fullIDsCount": 21936,
      "fullIDsPercentage": 0.534985,
      "code": "Phone",
      "value": "7"
    }
  ],
  "reportTimestamp": "2020-08-01T17:57:58.697"
}
```

| Propriété | Description |
| -------- | ----------- |
| `sampleCount` | Nombre total de profils fusionnés échantillonnés dans l’espace de noms. |
| `samplePercentage` | Le `sampleCount` sous la forme d’un pourcentage de profils fusionnés échantillonnés (la valeur de `numRowsToRead` telle qu’elle est renvoyée dans le [dernier état d’échantillon](#view-last-sample-status)), exprimé au format décimal. |
| `reportTimestamp` | Date et heure du rapport. Si un paramètre de `date` a été fourni pendant la requête, le rapport renvoyé porte sur la date fournie. Si aucun paramètre `date` n’est fourni, le rapport le plus récent est renvoyé. |
| `fullIDsFragmentCount` | Nombre total de fragments de profil dans l’espace de noms. |
| `fullIDsCount` | Nombre total de profils fusionnés dans l’espace de noms. |
| `fullIDsPercentage` | Le `fullIDsCount` en pourcentage du total des profils fusionnés (la valeur `totalRows` telle qu’elle est renvoyée dans le [dernier état d’échantillon](#view-last-sample-status)), exprimé au format décimal. |
| `code` | `code` de l’espace de noms. Vous pouvez le trouver lors de l’utilisation d’espaces de noms à l’aide de l’API Adobe Experience Platform Identity Service [&#128279;](../../identity-service/api/list-namespaces.md). Il est également appelé [!UICONTROL Identity symbol] dans l’interface utilisateur d’Experience Platform. Pour en savoir plus, consultez la [présentation des espaces de noms d’identité](../../identity-service/features/namespaces.md). |
| `value` | Valeur `id` pour l’espace de noms . Vous pouvez le trouver lorsque vous utilisez des espaces de noms à l’aide de l’[API Identity Service](../../identity-service/api/list-namespaces.md). |

+++

## Liste des statistiques des jeux de données {#dataset-stats}

Vous pouvez générer un rapport qui fournit des statistiques sur le jeu de données en envoyant une requête GET au point d’entrée `/previewsamplestatus/report/dataset_stats`.

**Format d’API**

```http
GET /previewsamplestatus/report/dataset_stats
```

**Requête**

+++ Exemple de requête pour générer le rapport de statistiques de jeux de données.

```shell
curl -X GET https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset_stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations sur les statistiques du jeu de données.

+++ Exemple de réponse contenant des informations sur les statistiques du jeu de données.

>[!NOTE]
>
>La réponse suivante a été tronquée pour afficher trois jeux de données.

```json
{
    "data": [
        {
            "120days": 4,
            "14days": 4,
            "30days": 4,
            "365days": 4,
            "60days": 4,
            "7days": 4,
            "90days": 4,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 1,
            "records": 4,
            "totalProfiles": 1
        },
        {
            "120days": 155435837,
            "14days": 32888631,
            "30days": 66496282,
            "365days": 155435837,
            "60days": 116433804,
            "7days": 18202004,
            "90days": 155435837,
            "datasetId": "{DATASET_ID}",
            "datasetType": "ExperienceEvents",
            "percentEvents": 16.0,
            "percentProfiles": 0.0,
            "profileFragments": 5410745,
            "records": 155435837,
            "totalProfiles": 4524723
        },
        {
            "120days": 0,
            "14days": 0,
            "30days": 0,
            "365days": 0,
            "60days": 0,
            "7days": 0,
            "90days": 0,
            "datasetId": "{DATASET_ID}",
            "datasetType": "Profiles",
            "percentEvents": 0.0,
            "percentProfiles": 0.0,
            "profileFragments": 3589,
            "records": 3589,
            "totalProfiles": 3589
        }
    ],
    "reportTimestamp": "2025-10-29T16:20:18.956"
}
```

| Propriété | Description |
| -------- | ----------- |
| `120days` | Le nombre d’enregistrements qui resteront dans le jeu de données après une expiration de données de 120 jours. |
| `14days` | Le nombre d’enregistrements qui resteront dans le jeu de données après une expiration de données de 14 jours. |
| `30days` | Le nombre d’enregistrements qui resteront dans le jeu de données après une expiration de données de 30 jours. |
| `365days` | Le nombre d’enregistrements qui resteront dans le jeu de données après une expiration de données de 365 jours. |
| `60days` | Le nombre d’enregistrements qui resteront dans le jeu de données après une expiration de données de 60 jours. |
| `7days` | Le nombre d’enregistrements qui resteront dans le jeu de données après une expiration de données de 7 jours. |
| `90days` | Le nombre d’enregistrements qui resteront dans le jeu de données après une expiration de données de 90 jours. |
| `datasetId` | Identifiant du jeu de données. |
| `datasetType` | Type de jeu de données. Cette valeur peut être `Profiles` ou `ExperienceEvents`. |
| `percentEvents` | Pourcentage d’enregistrements d’événements d’expérience qui se trouvent dans le jeu de données. |
| `percentProfiles` | Pourcentage d’enregistrements de profil qui se trouvent dans le jeu de données. |
| `profileFragments` | Nombre total de fragments de profil qui existent dans le jeu de données. |
| `records` | Nombre total d’enregistrements de profil ingérés dans le jeu de données. |
| `totalProfiles` | Nombre total de profils ingérés dans le jeu de données. |

+++

## Étapes suivantes

Maintenant que vous savez comment prévisualiser des données d’exemple dans la banque de profils et exécuter plusieurs rapports sur les données, vous pouvez également utiliser les points d’entrée d’estimation et de prévisualisation de l’API Segmentation Service pour afficher des informations de niveau résumé concernant vos définitions de segment. Ces informations vous permettent de vous assurer que vous isolez l’audience attendue. Pour en savoir plus sur l’utilisation des aperçus et des estimations à l’aide de l’API Segmentation, consultez le guide des points d’entrée [aperçu et estimation](../../segmentation/api/previews-and-estimates.md).

