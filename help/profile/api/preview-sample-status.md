---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;aperçu;exemple
title: Aperçu de l’exemple d’état (aperçu du profil), point de terminaison de l’API
description: L’aperçu de l’exemple de point de terminaison d’état de l’API Real-time Customer Profile vous permet de prévisualiser le dernier échantillon réussi de vos données de profil, de répertorier la distribution du profil par jeu de données et par identité, et de générer des rapports montrant le chevauchement des jeux de données, le chevauchement d’identités et les profils désassemblés.
role: Developer
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2906'
ht-degree: 5%

---

# Aperçu d’un exemple de point de terminaison d’état (aperçu du profil)

Adobe Experience Platform vous permet d’ingérer des données client provenant de plusieurs sources afin de créer un profil robuste et unifié pour chacun de vos clients. Lorsque des données sont ingérées dans Platform, un exemple de tâche est exécuté pour mettre à jour le nombre de profils et d’autres mesures liées aux données de Real-Time Customer Profile.

Les résultats de cet exemple de tâche peuvent être affichés à l’aide de la fonction `/previewsamplestatus` point de terminaison, qui fait partie de l’API Real-time Customer Profile. Ce point de terminaison peut également être utilisé pour répertorier les distributions de profil par jeu de données et espace de noms d’identité, ainsi que pour générer plusieurs rapports afin de mieux comprendre la composition de la banque de profils de votre entreprise. Ce guide décrit les étapes requises pour afficher ces mesures à l’aide du `/previewsamplestatus` Point d’entrée de l’API.

>[!NOTE]
>
>Des points de terminaison d’estimation et de prévisualisation sont disponibles dans le cadre de l’API Adobe Experience Platform Segmentation Service. Ils vous permettent d’afficher des informations de niveau résumé concernant les définitions de segment afin de vous assurer que vous isolez l’audience attendue. Pour obtenir des instructions détaillées sur l’utilisation des points de terminaison de prévisualisation et d’estimation, consultez la [guide des prévisualisations et des points de fin d’estimation](../../segmentation/api/previews-and-estimates.md), partie de la fonction [!DNL Segmentation] Guide de développement d’API.

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de lʼ [[!DNL Real-Time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Fragments de profil contre profils fusionnés

Ce guide fait référence aux &quot;fragments de profil&quot; et aux &quot;profils fusionnés&quot;. Il est important de comprendre la différence entre ces termes avant de poursuivre.

Chaque profil client est composé de plusieurs fragments de profil qui ont été fusionnés dans le but de former une vue unique pour ce client. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, il est probable que votre entreprise dispose de plusieurs fragments de profil associés à ce client unique apparaissant dans plusieurs jeux de données.

Lorsque des fragments de profil sont ingérés dans Platform, ils sont fusionnés (en fonction d’une stratégie de fusion) afin de créer un profil unique pour ce client. Par conséquent, le nombre total de fragments de profil est susceptible d’être toujours supérieur au nombre total de profils fusionnés, car chaque profil est composé de plusieurs fragments.

Pour en savoir plus sur les profils et leur rôle dans Experience Platform, veuillez commencer par lire la [Présentation de Real-Time Customer Profile](../home.md).

## Déclenchement de l’exemple de tâche

Lorsque les données activées pour Real-time Customer Profile sont ingérées dans [!DNL Platform], il est stocké dans la banque de données Profile. Lorsque l’ingestion d’enregistrements dans la banque de profils augmente ou diminue le nombre total de profils de plus de 5 %, une tâche d’échantillonnage est déclenchée pour mettre à jour le nombre. La manière dont l’échantillon est déclenché dépend du type d’ingestion utilisé :

* Pour **flux de travaux de données**, une vérification est effectuée toutes les heures pour déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si tel est le cas, un exemple de tâche est automatiquement déclenché pour mettre à jour le décompte.
* Pour **ingestion par lots**, dans les 15 minutes suivant l’ingestion réussie d’un lot dans la banque de profils, si le seuil de 5 % d’augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour le nombre. À l’aide de l’API Profile, vous pouvez prévisualiser le dernier exemple de tâche réussi, ainsi que répertorier la distribution du profil par jeu de données et par espace de noms d’identité.

Le nombre de profils et les profils par mesures d’espace de noms sont également disponibles dans la variable [!UICONTROL Profils] de l’interface utilisateur de l’Experience Platform. Pour plus d’informations sur l’accès aux données de profil à l’aide de l’interface utilisateur, consultez la page [[!DNL Profile] Guide de l’interface utilisateur](../ui/user-guide.md).

## Afficher le dernier état d’exemple {#view-last-sample-status}

Vous pouvez exécuter une requête de GET sur la variable `/previewsamplestatus` point de terminaison pour afficher les détails du dernier exemple de tâche réussi qui a été exécuté pour votre organisation. Cela inclut le nombre total de profils dans l’exemple, ainsi que la mesure du nombre de profils ou le nombre total de profils de votre organisation dans Experience Platform.

Le nombre de profils est généré après la fusion de fragments de profil afin de former un seul profil pour chaque client. En d’autres termes, lorsque des fragments de profil sont fusionnés, ils renvoient le nombre de profils &quot;1&quot;, car ils sont tous liés à la même personne.

Le nombre de profils inclut également les profils avec des attributs (données d’enregistrement) ainsi que les profils contenant uniquement des données de série temporelle (événement), tels que les profils Adobe Analytics. L’exemple de tâche est régulièrement actualisé lorsque des données de profil sont ingérées afin de fournir un nombre total de profils à jour dans Platform.

**Format d’API**

```http
GET /previewsamplestatus
```

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

La réponse inclut les détails du dernier exemple de tâche réussi qui a été exécuté pour l’organisation.

>[!NOTE]
>
>Dans cet exemple de réponse, `numRowsToRead` et `totalRows` sont égaux les uns aux autres. Selon le nombre de profils de votre entreprise en Experience Platform, cela peut être le cas. Toutefois, ces deux nombres sont généralement différents, `numRowsToRead` étant le nombre le plus petit, car il représente l’échantillon sous forme de sous-ensemble du nombre total de profils (`totalRows`).

```json
{
  "numRowsToRead": "41003",
  "sampleJobRunning": {
    "status": true,
    "submissionTimestamp": "2020-08-01 17:57:57.0"
  },
  "cosmosDocCount": "\"300803\"",
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
|---|---|
| `numRowsToRead` | Le nombre total de profils fusionnés dans l’exemple. |
| `sampleJobRunning` | Une valeur booléenne qui renvoie `true` lorsqu’un exemple de tâche est en cours. Fournit une transparence quant à la latence qui survient lorsqu’un fichier de lot est chargé dans lorsqu’il est réellement ajouté à la banque de profils. |
| `cosmosDocCount` | Nombre total de documents dans Cosmos. |
| `totalFragmentCount` | Nombre total de fragments de profil dans la banque de profils. |
| `lastSuccessfulBatchTimestamp` | Dernier horodatage d’ingestion par lots réussi. |
| `streamingDriven` | *Ce champ est obsolète et ne contient aucune signification pour la réponse.* |
| `totalRows` | Nombre total de profils fusionnés en Experience Platform, également appelé &quot;nombre de profils&quot;. |
| `lastBatchId` | Dernier identifiant d’ingestion par lots. |
| `status` | État du dernier exemple. |
| `samplingRatio` | Ratio des profils fusionnés échantillonnés (`numRowsToRead`) au total des profils fusionnés (`totalRows`), exprimé sous la forme d’un pourcentage au format décimal. |
| `mergeStrategy` | Stratégie de fusion utilisée dans l’exemple. |
| `lastSampledTimestamp` | Dernier exemple d’horodatage réussi. |

## Liste de la distribution des profils par jeu de données

Pour afficher la distribution des profils par jeu de données, vous pouvez exécuter une requête de GET sur la variable `/previewsamplestatus/report/dataset` point de terminaison .

**Format d’API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à la date, le rapport le plus récent pour cette date est renvoyé. Si un rapport n’existe pas pour la date spécifiée, une erreur 404 (Introuvable) est renvoyée. Si aucune date n’est spécifiée, le rapport le plus récent est renvoyé. Format : AAAA-MM-JJ. Exemple : `date=2024-12-31` |

**Requête**

La requête suivante utilise la variable `date` pour renvoyer le rapport le plus récent pour la date spécifiée.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

La réponse comprend une `data` contenant une liste d’objets de jeu de données. La réponse affichée a été tronquée pour afficher trois jeux de données.

>[!NOTE]
>
>S’il existe plusieurs rapports pour la date, seul le dernier rapport est renvoyé. Si un rapport de jeu de données n’existe pas pour la date fournie, l’état HTTP 404 (Introuvable) est renvoyé.

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
|---|---|
| `sampleCount` | Le nombre total de profils fusionnés échantillonnés avec cet identifiant de jeu de données. |
| `samplePercentage` | La variable `sampleCount` en pourcentage du nombre total de profils fusionnés échantillonnés (le `numRowsToRead` comme indiqué dans la variable [dernier exemple d’état](#view-last-sample-status)), exprimé au format décimal. |
| `fullIDsCount` | Le nombre total de profils fusionnés avec cet identifiant de jeu de données. |
| `fullIDsPercentage` | La variable `fullIDsCount` en pourcentage du nombre total de profils fusionnés (le `totalRows` comme indiqué dans la variable [dernier exemple d’état](#view-last-sample-status)), exprimé au format décimal. |
| `name` | Nom du jeu de données, tel qu’il est fourni lors de la création du jeu de données. |
| `description` | Description du jeu de données, tel qu’il est fourni lors de la création du jeu de données. |
| `value` | L’identifiant du jeu de données. |
| `streamingIngestionEnabled` | Si le jeu de données est activé pour l’ingestion par flux. |
| `createdUser` | Identifiant utilisateur de l’utilisateur qui a créé le jeu de données. |
| `reportTimestamp` | Horodatage du rapport. Si une `date` a été fourni pendant la requête, le rapport renvoyé correspond à la date fournie. Si non `date` est fourni, le rapport le plus récent est renvoyé. |

## Liste de la distribution des profils par espace de noms d’identité

Vous pouvez exécuter une requête de GET sur la variable `/previewsamplestatus/report/namespace` point de terminaison pour afficher la ventilation par espace de noms d’identité pour tous les profils fusionnés dans votre banque de profils. Cela inclut les identités standard fournies par Adobe, ainsi que les identités personnalisées définies par votre organisation.

Les espaces de noms d’identité sont un composant important de Adobe Experience Platform Identity Service qui sert d’indicateurs du contexte auquel les données client se rapportent. Pour en savoir plus, commencez par lire le [présentation de l’espace de noms d’identité](../../identity-service/features/namespaces.md).

>[!NOTE]
>
>Le nombre total de profils par espace de noms (additionnant les valeurs affichées pour chaque espace de noms) peut être supérieur à la mesure du nombre de profils, car un profil peut être associé à plusieurs espaces de noms. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à ce client individuel.

**Format d’API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à la date, le rapport le plus récent pour cette date est renvoyé. Si un rapport n’existe pas pour la date spécifiée, une erreur 404 (Introuvable) est renvoyée. Si aucune date n’est spécifiée, le rapport le plus récent est renvoyé. Format : AAAA-MM-JJ. Exemple : `date=2024-12-31` |

**Requête**

La requête suivante ne spécifie pas un `date` et renverra donc le rapport le plus récent.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

La réponse comprend une `data` avec des objets individuels contenant les détails de chaque espace de noms. La réponse affichée a été tronquée pour afficher quatre espaces de noms.

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
|---|---|
| `sampleCount` | Nombre total de profils fusionnés échantillonnés dans l’espace de noms. |
| `samplePercentage` | La variable `sampleCount` en tant que pourcentage des profils fusionnés échantillonnés (le `numRowsToRead` comme indiqué dans la variable [dernier exemple d’état](#view-last-sample-status)), exprimé au format décimal. |
| `reportTimestamp` | Horodatage du rapport. Si une `date` a été fourni pendant la requête, le rapport renvoyé correspond à la date fournie. Si non `date` est fourni, le rapport le plus récent est renvoyé. |
| `fullIDsFragmentCount` | Nombre total de fragments de profil dans l’espace de noms. |
| `fullIDsCount` | Le nombre total de profils fusionnés dans l’espace de noms. |
| `fullIDsPercentage` | La variable `fullIDsCount` en tant que pourcentage du total des profils fusionnés (le `totalRows` comme indiqué dans la variable [dernier exemple d’état](#view-last-sample-status)), exprimé au format décimal. |
| `code` | La variable `code` pour l’espace de noms. Vous pouvez le trouver lorsque vous utilisez des espaces de noms à l’aide de la variable [API Adobe Experience Platform Identity Service](../../identity-service/api/list-namespaces.md) et est également appelé [!UICONTROL Symbole d’identité] dans l’interface utilisateur de l’Experience Platform. Pour en savoir plus, consultez la [présentation de l’espace de noms d’identité](../../identity-service/features/namespaces.md). |
| `value` | La variable `id` pour l’espace de noms. Vous pouvez le trouver lorsque vous utilisez des espaces de noms à l’aide de la variable [API Identity Service](../../identity-service/api/list-namespaces.md). |

## Génération du rapport de chevauchement de jeux de données

Le rapport de chevauchement de jeux de données offre une visibilité sur la composition de la banque de profils de votre entreprise en exposant les jeux de données qui contribuent le plus à votre audience adressable (profils fusionnés). En plus de fournir des informations sur vos données, ce rapport peut vous aider à prendre des mesures pour optimiser l’utilisation des licences, comme la définition d’expirations pour certains jeux de données.

Vous pouvez générer le rapport de chevauchement de jeux de données en adressant une requête GET à la variable `/previewsamplestatus/report/dataset/overlap` point de terminaison .

Pour obtenir des instructions détaillées sur la génération du rapport de chevauchement de jeux de données à l’aide de la ligne de commande ou de l’interface utilisateur de Postman, reportez-vous à la section [génération du tutoriel sur le rapport de chevauchement de jeux de données](../tutorials/dataset-overlap-report.md).

**Format d’API**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à la même date, le rapport le plus récent pour cette date est renvoyé. Si un rapport n’existe pas pour la date spécifiée, une erreur 404 (Introuvable) est renvoyée. Si aucune date n’est spécifiée, le rapport le plus récent est renvoyé. Format : AAAA-MM-JJ. Exemple : `date=2024-12-31` |

**Requête**

La requête suivante utilise la variable `date` pour renvoyer le rapport le plus récent pour la date spécifiée.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Réponse**

Une requête réussie renvoie un état HTTP 200 (OK) et le rapport de chevauchement de jeux de données.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-12-29T19:55:31.147"
}
```

| Propriété | Description |
|---|---|
| `data` | La variable `data` contient des listes de jeux de données séparées par des virgules et leurs nombres de profils respectifs. |
| `reportTimestamp` | Horodatage du rapport. Si une `date` a été fourni pendant la requête, le rapport renvoyé correspond à la date fournie. Si non `date` est fourni, le rapport le plus récent est renvoyé. |

### Interprétation du rapport de chevauchement de jeux de données

Les résultats du rapport peuvent être interprétés à partir des jeux de données et du nombre de profils dans la réponse. Examinez l’exemple de rapport suivant : `data` objet :

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Ce rapport fournit les informations suivantes :

* Il existe 123 profils composés de données provenant des jeux de données suivants : `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Il existe 454 412 profils composés de données provenant de ces deux jeux de données : `5d92921872831c163452edc8` et `5eb2cdc6fa3f9a18a7592a98`.
* 107 profils sont constitués uniquement de données issues d’un jeu de données. `5eeda0032af7bb19162172a7`.
* Il y a un total de 454 642 profils dans l’organisation.

## Génération du rapport de chevauchement des espaces de noms d’identité {#identity-overlap-report}

Le rapport sur le chevauchement des espaces de noms d’identité offre une visibilité sur la composition de la banque de profils de votre organisation en exposant les espaces de noms d’identité qui contribuent le plus à votre audience adressable (profils fusionnés). Cela inclut les espaces de noms d’identité standard fournis par Adobe, ainsi que les espaces de noms d’identité personnalisés définis par votre organisation.

Vous pouvez générer le rapport de chevauchement d’espaces de noms d’identité en adressant une requête de GET à la variable `/previewsamplestatus/report/namespace/overlap` point de terminaison .

**Format d’API**

```http
GET /previewsamplestatus/report/namespace/overlap
GET /previewsamplestatus/report/namespace/overlap?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à la même date, le rapport le plus récent pour cette date est renvoyé. Si un rapport n’existe pas pour la date spécifiée, une erreur 404 (Introuvable) est renvoyée. Si aucune date n’est spécifiée, le rapport le plus récent est renvoyé. Format : AAAA-MM-JJ. Exemple : `date=2024-12-31` |

**Requête**

La requête suivante utilise la variable `date` pour renvoyer le rapport le plus récent pour la date spécifiée.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Réponse**

Une requête réussie renvoie un état HTTP 200 (OK) et le rapport de chevauchement des espaces de noms d’identité.

```json
{
    "data": {
        "Email,crmid,loyal": 2,
        "ECID,Email,crmid": 7,
        "ECID,Email,mobilenr": 12,
        "AAID,ECID,loyal": 1,
        "mobilenr": 25,
        "AAID,ECID": 1508,
        "ECID,crmid": 1,
        "AAID,ECID,crmid": 2,
        "Email,crmid": 328,
        "CORE": 49,
        "AAID": 446,
        "crmid,loyal": 20988,
        "Email": 10904,
        "crmid": 249,
        "ECID,Email": 74,
        "Phone": 40,
        "Email,Phone,loyal": 48,
        "AAID,AVID,ECID": 85,
        "Email,loyal": 1002,
        "AAID,ECID,Email,Phone,crmid": 5,
        "AAID,ECID,Email,crmid,loyal": 23,
        "AAID,AVID,ECID,Email,crmid": 2,
        "AVID": 3,
        "AAID,ECID,Phone": 1,
        "loyal": 43,
        "ECID,Email,crmid,loyal": 6,
        "AAID,ECID,Email,Phone,crmid,loyal": 1,
        "AAID,ECID,Email": 2,
        "AAID,ECID,Email,crmid": 142,
        "AVID,ECID": 24,
        "ECID": 6565
    },
    "reportTimestamp": "2021-12-29T16:55:03.624"
}
```

| Propriété | Description |
|---|---|
| `data` | La variable `data` contient des listes séparées par des virgules avec des combinaisons uniques de codes d’espace de noms d’identité et leurs nombres de profils respectifs. |
| Codes d’espace de noms | La variable `code` est un formulaire court pour chaque nom d’espace de noms d’identité. Mappage de chaque `code` à `name` se trouve à l’aide de la méthode [API Adobe Experience Platform Identity Service](../../identity-service/api/list-namespaces.md). La variable `code` est également appelé [!UICONTROL Symbole d’identité] dans l’interface utilisateur de l’Experience Platform. Pour en savoir plus, consultez la [présentation de l’espace de noms d’identité](../../identity-service/features/namespaces.md). |
| `reportTimestamp` | Horodatage du rapport. Si une `date` a été fourni pendant la requête, le rapport renvoyé correspond à la date fournie. Si non `date` est fourni, le rapport le plus récent est renvoyé. |

### Interprétation du rapport de chevauchement des espaces de noms d’identité

Les résultats du rapport peuvent être interprétés à partir des identités et du nombre de profils dans la réponse. La valeur numérique de chaque ligne indique le nombre de profils composés de cette combinaison exacte d’espaces de noms d’identité standard et personnalisés.

Examinez l’extrait suivant de la `data` objet :

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

Ce rapport fournit les informations suivantes :

* Il y a 142 profils composés de `AAID`, `ECID`, et `Email` identités standard, ainsi que depuis une `crmid` espace de noms d’identité.
* Il y a 24 profils composés de `AAID` et `ECID` espaces de noms d’identité.
* Il existe 6 565 profils qui incluent uniquement une `ECID` identité.

## Générer le rapport des profils désassemblés

Vous pouvez mieux comprendre la composition de la banque de profils de votre entreprise grâce au rapport Profils désassemblés. Un profil &quot;désassemblé&quot; est un profil qui ne contient qu’un fragment de profil. Un profil &quot;inconnu&quot; est un profil associé à des espaces de noms d’identité pseudonymes tels que `ECID` et `AAID`. Les profils inconnus sont inactifs, ce qui signifie qu’ils n’ont pas ajouté de nouveaux événements pour la période spécifiée. Le rapport Profils désassemblés fournit une ventilation des profils pour une période de 7, 30, 60, 90 et 120 jours.

Vous pouvez générer le rapport des profils désassemblés en adressant une requête de GET au `/previewsamplestatus/report/unstitchedProfiles` point de terminaison .

**Format d’API**

```http
GET /previewsamplestatus/report/unstitchedProfiles
```

**Requête**

La requête suivante renvoie le rapport des profils désassemblés.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/unstitchedProfiles \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Réponse**

Une requête réussie renvoie un état HTTP 200 (OK) et le rapport des profils désassemblés.

>[!NOTE]
>
>Pour les besoins de ce guide, le rapport a été tronqué afin d’inclure uniquement `"120days"` et`7days`&quot; des périodes. Le rapport Profils désassemblés complet fournit une ventilation des profils pour une période de 7, 30, 60, 90 et 120 jours.

```json
{
  "data": {
      "totalNumberOfProfiles": 63606,
      "totalNumberOfEvents": 130977,
      "unstitchedProfiles": {
          "120days": {
              "countOfProfiles": 1644,
              "eventsAssociated": 26824,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 18,
                      "eventsAssociated": 95
                  },
                  "loyal": {
                      "countOfProfiles": 26,
                      "eventsAssociated": 71
                  },
                  "ECID": {
                      "countOfProfiles": 1600,
                      "eventsAssociated": 26658
                  }
              }
          },
          "7days": {
              "countOfProfiles": 1782,
              "eventsAssociated": 29151,
              "nsDistribution": {
                  "Email": {
                      "countOfProfiles": 19,
                      "eventsAssociated": 97
                  },
                  "ECID": {
                      "countOfProfiles": 1734,
                      "eventsAssociated": 28591
                  },
                  "loyal": {
                      "countOfProfiles": 29,
                      "eventsAssociated": 463
                  }
              }
          }
      }
  },
  "reportTimestamp": "2025-08-25T22:14:55.186"
}
```

| Propriété | Description |
|---|---|
| `data` | La variable `data` contient les informations renvoyées pour le rapport des profils désassemblés. |
| `totalNumberOfProfiles` | Comptage total des profils uniques dans la banque de profils. Cela équivaut au nombre d’audiences adressables. Il comprend les profils connus et désassemblés. |
| `totalNumberOfEvents` | Nombre total d’ExperienceEvents dans la banque de profils. |
| `unstitchedProfiles` | Objet contenant une ventilation des profils désassemblés par période. Le rapport Profils désassemblés fournit une ventilation des profils pour des périodes de 7, 30, 60, 90 et 120 jours. |
| `countOfProfiles` | Le nombre de profils désassemblés pour la période ou le nombre de profils désassemblés pour l’espace de noms. |
| `eventsAssociated` | Nombre d’ExperienceEvents pour la période ou nombre d’événements pour l’espace de noms. |
| `nsDistribution` | Objet contenant des espaces de noms d’identité individuels avec la distribution de profils et d’événements désassemblés pour chaque espace de noms. Remarque : Si vous additionnez le total `countOfProfiles` pour chaque espace de noms d’identité dans la variable `nsDistribution` est égal à `countOfProfiles` pour la période. Il en va de même pour `eventsAssociated` par espace de noms et le total `eventsAssociated` par période. |
| `reportTimestamp` | Horodatage du rapport. |

### Interprétation du rapport des profils désassemblés

Les résultats du rapport peuvent fournir des informations sur le nombre de profils désassemblés et inactifs de votre organisation dans sa banque de profils.

Examinez l’extrait suivant de la `data` objet :

```json
  "7days": {
    "countOfProfiles": 1782,
    "eventsAssociated": 29151,
    "nsDistribution": {
      "Email": {
        "countOfProfiles": 19,
        "eventsAssociated": 97
      },
      "ECID": {
        "countOfProfiles": 1734,
        "eventsAssociated": 28591
      },
      "loyal": {
        "countOfProfiles": 29,
        "eventsAssociated": 463
      }
    }
  }
```

Ce rapport fournit les informations suivantes :

* Il existe 1 782 profils qui ne contiennent qu’un fragment de profil et n’ont aucun nouvel événement au cours des sept derniers jours.
* 29 151 ExperienceEvents sont associés aux 1 782 profils désassemblés.
* Il existe 1 734 profils désassemblés contenant un fragment de profil unique de l’espace de noms d’identité d’ECID.
* 28 591 événements sont associés aux 1 734 profils désassemblés qui contiennent un fragment de profil unique de l’espace de noms d’identité d’ECID.

## Étapes suivantes

Maintenant que vous savez comment prévisualiser des données d’exemple dans la banque de profils et exécuter plusieurs rapports sur les données, vous pouvez également utiliser les points de terminaison d’estimation et de prévisualisation de l’API Segmentation Service pour afficher des informations sommaires sur vos définitions de segment. Ces informations vous permettent de vous assurer que vous isolez l’audience attendue. Pour en savoir plus sur l’utilisation des prévisualisations et des estimations à l’aide de l’API Segmentation, consultez le [guide de prévisualisation et d’estimation des points de fin](../../segmentation/api/previews-and-estimates.md).

