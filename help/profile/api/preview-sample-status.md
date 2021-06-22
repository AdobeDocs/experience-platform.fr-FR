---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;aperçu;exemple
title: Aperçu de l’exemple d’état (aperçu du profil), point de terminaison de l’API
description: À l’aide de l’exemple de point de terminaison d’état de la prévisualisation, qui fait partie de l’API Real-time Customer Profile, vous pouvez prévisualiser le dernier échantillon réussi de vos données Profile, répertorier la distribution du profil par jeu de données et par identité, et générer un rapport de chevauchement de jeux de données.
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
source-git-commit: 0c7dc02ed0bacf7e0405b836f566149a872fc31a
workflow-type: tm+mt
source-wordcount: '2450'
ht-degree: 5%

---

# Aperçu d’un exemple de point de terminaison d’état (aperçu du profil)

Adobe Experience Platform vous permet d’ingérer des données client provenant de plusieurs sources afin de créer un profil robuste et unifié pour chacun de vos clients. Lorsque des données sont ingérées dans Platform, un exemple de tâche est exécuté pour mettre à jour le nombre de profils et d’autres mesures liées aux données de Real-time Customer Profile.

Les résultats de cet exemple de tâche peuvent être visualisés à l’aide du point de terminaison `/previewsamplestatus`, qui fait partie de l’API Real-time Customer Profile. Ce point de terminaison peut également être utilisé pour répertorier les distributions de profil par jeu de données et espace de noms d’identité, ainsi que pour générer un rapport de chevauchement de jeux de données et un rapport de chevauchement d’identités afin de bénéficier d’une meilleure visibilité sur la composition de la banque de profils de votre entreprise. Ce guide décrit les étapes requises pour afficher ces mesures à l’aide du point de terminaison de l’API `/previewsamplestatus`.

>[!NOTE]
>
>Des points de terminaison d’estimation et de prévisualisation sont disponibles dans le cadre de l’API Adobe Experience Platform Segmentation Service. Ils vous permettent d’afficher des informations de niveau résumé concernant les définitions de segment afin de vous assurer que vous isolez l’audience attendue. Pour obtenir des instructions détaillées sur l’utilisation des points de terminaison de prévisualisation et d’estimation des segments, consultez le [guide de prévisualisation et d’estimation des points de terminaison](../../segmentation/api/previews-and-estimates.md), qui fait partie du guide de développement de l’API [!DNL Segmentation].

## Prise en main

Le point d’entrée dʼAPI utilisé dans ce guide fait partie de lʼAPI [[!DNL Real-time Customer Profile] ](https://www.adobe.com/go/profile-apis-en). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples dʼappels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels à nʼimporte quel API dʼ[!DNL Experience Platform].

## Fragments de profil contre profils fusionnés

Ce guide fait référence à la fois aux &quot;fragments de profil&quot; et aux &quot;profils fusionnés&quot;. Il est important de comprendre la différence entre ces termes avant de poursuivre.

Chaque profil client est composé de plusieurs fragments de profil qui ont été fusionnés dans le but de former une vue unique pour ce client. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, il est probable que votre entreprise dispose de plusieurs fragments de profil associés à ce client unique apparaissant dans plusieurs jeux de données.

Lorsque des fragments de profil sont ingérés dans Platform, ils sont fusionnés (en fonction d’une stratégie de fusion) afin de créer un profil unique pour ce client. Par conséquent, le nombre total de fragments de profil est susceptible d’être toujours supérieur au nombre total de profils fusionnés, car chaque profil est composé de plusieurs fragments.

Pour en savoir plus sur les profils et leur rôle dans Experience Platform, commencez par lire la [présentation de Real-time Customer Profile](../home.md).

## Déclenchement de l’exemple de tâche

Les données activées pour Real-time Customer Profile étant ingérées dans [!DNL Platform], elles sont stockées dans la banque de données Profile. Lorsque l’ingestion d’enregistrements dans la banque de profils augmente ou diminue le nombre total de profils de plus de 5 %, une tâche d’échantillonnage est déclenchée pour mettre à jour le nombre. La manière dont l’échantillon est déclenché dépend du type d’ingestion utilisé :

* Pour les **workflows de données en flux continu**, une vérification est effectuée toutes les heures pour déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si tel est le cas, un exemple de tâche est automatiquement déclenché pour mettre à jour le décompte.
* Pour **l’ingestion par lots**, dans les 15 minutes suivant l’ingestion réussie d’un lot dans la banque de profils, si le seuil de 5 % d’augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour le nombre. À l’aide de l’API Profile, vous pouvez prévisualiser le dernier exemple de tâche réussi, ainsi que répertorier la distribution du profil par jeu de données et par espace de noms d’identité.

Le nombre de profils et les profils par mesures d’espace de noms sont également disponibles dans la section [!UICONTROL Profils] de l’interface utilisateur de l’Experience Platform. Pour plus d’informations sur l’accès aux données de profil à l’aide de l’interface utilisateur, consultez le [[!DNL Profile] guide de l’interface utilisateur](../ui/user-guide.md).

## Afficher le dernier état d’exemple {#view-last-sample-status}

Vous pouvez effectuer une requête de GET sur le point de terminaison `/previewsamplestatus` pour afficher les détails du dernier exemple de tâche réussi qui a été exécuté pour votre organisation IMS. Cela inclut le nombre total de profils dans l’exemple, ainsi que la mesure du nombre de profils ou le nombre total de profils de votre organisation dans Experience Platform.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

La réponse inclut les détails du dernier exemple de tâche réussi qui a été exécuté pour l’organisation.

>[!NOTE]
>
>Dans cet exemple de réponse, `numRowsToRead` et `totalRows` sont égaux les uns aux autres. Selon le nombre de profils de votre entreprise en Experience Platform, cela peut être le cas. Toutefois, ces deux nombres sont généralement différents, `numRowsToRead` étant le nombre le plus petit, car il représente l’échantillon comme sous-ensemble du nombre total de profils (`totalRows`).

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
| `sampleJobRunning` | Valeur boolean qui renvoie `true` lorsqu’un exemple de tâche est en cours. Fournit une transparence quant à la latence qui survient lorsqu’un fichier de lot est chargé dans lorsqu’il est réellement ajouté à la banque de profils. |
| `cosmosDocCount` | Nombre total de documents dans Cosmos. |
| `totalFragmentCount` | Nombre total de fragments de profil dans la banque de profils. |
| `lastSuccessfulBatchTimestamp` | Dernier horodatage d’ingestion par lots réussi. |
| `streamingDriven` | *Ce champ est obsolète et ne contient aucune signification pour la réponse.* |
| `totalRows` | Nombre total de profils fusionnés en Experience Platform, également appelé &quot;nombre de profils&quot;. |
| `lastBatchId` | Dernier identifiant d’ingestion par lots. |
| `status` | État du dernier exemple. |
| `samplingRatio` | Ratio des profils fusionnés échantillonnés (`numRowsToRead`) par rapport au total des profils fusionnés (`totalRows`), exprimé en pourcentage au format décimal. |
| `mergeStrategy` | Stratégie de fusion utilisée dans l’exemple. |
| `lastSampledTimestamp` | Dernier exemple d’horodatage réussi. |

## Liste de la distribution des profils par jeu de données

Pour afficher la distribution des profils par jeu de données, vous pouvez exécuter une requête de GET sur le point de terminaison `/previewsamplestatus/report/dataset` .

**Format d&#39;API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à la date, le rapport le plus récent pour cette date est renvoyé. Si un rapport n’existe pas pour la date spécifiée, une erreur 404 (Introuvable) est renvoyée. Si aucune date n’est spécifiée, le rapport le plus récent est renvoyé. Format : AAAA-MM-JJ. Exemple : `date=2024-12-31` |

**Requête**

La requête suivante utilise le paramètre `date` pour renvoyer le rapport le plus récent pour la date spécifiée.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset?date=2020-08-01 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

La réponse comprend un tableau `data` contenant une liste d’objets de jeu de données. La réponse affichée a été tronquée pour afficher trois jeux de données.

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
| `samplePercentage` | La valeur `sampleCount` en pourcentage du nombre total de profils fusionnés échantillonnés (la valeur `numRowsToRead` renvoyée dans le [dernier état d’échantillonnage](#view-last-sample-status)), exprimée au format décimal. |
| `fullIDsCount` | Le nombre total de profils fusionnés avec cet identifiant de jeu de données. |
| `fullIDsPercentage` | La valeur `fullIDsCount` en pourcentage du nombre total de profils fusionnés (la valeur `totalRows` renvoyée dans le [dernier état d’échantillon](#view-last-sample-status)), exprimée au format décimal. |
| `name` | Nom du jeu de données, tel qu’il est fourni lors de la création du jeu de données. |
| `description` | Description du jeu de données, tel qu’il est fourni lors de la création du jeu de données. |
| `value` | L’identifiant du jeu de données. |
| `streamingIngestionEnabled` | Si le jeu de données est activé pour l’ingestion par flux. |
| `createdUser` | Identifiant utilisateur de l’utilisateur qui a créé le jeu de données. |
| `reportTimestamp` | Horodatage du rapport. Si un paramètre `date` a été fourni pendant la demande, le rapport renvoyé correspond à la date fournie. Si aucun paramètre `date` n’est fourni, le rapport le plus récent est renvoyé. |

## Liste de la distribution des profils par espace de noms d’identité

Vous pouvez exécuter une requête de GET sur le point de terminaison `/previewsamplestatus/report/namespace` pour afficher la ventilation par espace de noms d’identité pour tous les profils fusionnés de votre banque de profils. Cela inclut les identités standard fournies par Adobe, ainsi que les identités personnalisées définies par votre organisation.

Les espaces de noms d’identité sont un composant important de Adobe Experience Platform Identity Service qui sert d’indicateurs du contexte auquel les données client se rapportent. Pour en savoir plus, commencez par lire la [présentation de l’espace de noms d’identité](../../identity-service/namespaces.md).

>[!NOTE]
>
>Le nombre total de profils par espace de noms (additionnant les valeurs affichées pour chaque espace de noms) peut être supérieur à la mesure du nombre de profils, car un profil peut être associé à plusieurs espaces de noms. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de noms seront associés à ce client individuel.

**Format d&#39;API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à la date, le rapport le plus récent pour cette date est renvoyé. Si un rapport n’existe pas pour la date spécifiée, une erreur 404 (Introuvable) est renvoyée. Si aucune date n’est spécifiée, le rapport le plus récent est renvoyé. Format : AAAA-MM-JJ. Exemple : `date=2024-12-31` |

**Requête**

La requête suivante ne spécifie pas de paramètre `date` et renverra donc le rapport le plus récent.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

La réponse comprend un tableau `data`, avec des objets individuels contenant les détails de chaque espace de noms. La réponse affichée a été tronquée pour afficher quatre espaces de noms.

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
| `samplePercentage` | La valeur `sampleCount` en pourcentage des profils fusionnés échantillonnés (la valeur `numRowsToRead` renvoyée dans le [dernier état d’échantillon](#view-last-sample-status)), exprimée au format décimal. |
| `reportTimestamp` | Horodatage du rapport. Si un paramètre `date` a été fourni pendant la demande, le rapport renvoyé correspond à la date fournie. Si aucun paramètre `date` n’est fourni, le rapport le plus récent est renvoyé. |
| `fullIDsFragmentCount` | Nombre total de fragments de profil dans l’espace de noms. |
| `fullIDsCount` | Le nombre total de profils fusionnés dans l’espace de noms. |
| `fullIDsPercentage` | La valeur `fullIDsCount` en pourcentage du total des profils fusionnés (la valeur `totalRows` renvoyée dans le [dernier état d’échantillon](#view-last-sample-status)), exprimée au format décimal. |
| `code` | `code` pour l’espace de noms. Vous pouvez le trouver lorsque vous utilisez des espaces de noms à l’aide de l’[API Adobe Experience Platform Identity Service](../../identity-service/api/list-namespaces.md) et vous pouvez également y faire référence en tant que [!UICONTROL symbole d’identité] dans l’interface utilisateur de l’Experience Platform. Pour en savoir plus, consultez la [présentation des espaces de noms d’identité](../../identity-service/namespaces.md). |
| `value` | La valeur `id` de l’espace de noms. Vous pouvez le trouver lorsque vous utilisez des espaces de noms à l’aide de l’[API Identity Service](../../identity-service/api/list-namespaces.md). |

## Génération du rapport de chevauchement de jeux de données

Le rapport de chevauchement de jeux de données offre une visibilité sur la composition de la banque de profils de votre entreprise en exposant les jeux de données qui contribuent le plus à votre audience adressable (profils fusionnés). En plus de fournir des informations sur vos données, ce rapport peut vous aider à prendre des mesures pour optimiser l’utilisation des licences, comme la définition d’un délai d’activation pour certains jeux de données.

Vous pouvez générer le rapport de chevauchement de jeux de données en exécutant une requête de GET sur le point de terminaison `/previewsamplestatus/report/dataset/overlap` .

Pour obtenir des instructions détaillées sur la génération du rapport de chevauchement de jeux de données à l’aide de la ligne de commande ou de l’interface utilisateur Postman, reportez-vous au [tutoriel sur la génération du rapport de chevauchement de jeux de données](../tutorials/dataset-overlap-report.md).

**Format d&#39;API**

```http
GET /previewsamplestatus/report/dataset/overlap
GET /previewsamplestatus/report/dataset/overlap?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à la même date, le rapport le plus récent pour cette date est renvoyé. Si un rapport n’existe pas pour la date spécifiée, une erreur 404 (Introuvable) est renvoyée. Si aucune date n’est spécifiée, le rapport le plus récent est renvoyé. Format : AAAA-MM-JJ. Exemple : `date=2024-12-31` |

**Requête**

La requête suivante utilise le paramètre `date` pour renvoyer le rapport le plus récent pour la date spécifiée.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `data` | L’objet `data` contient des listes de jeux de données séparées par des virgules et leurs nombres de profils respectifs. |
| `reportTimestamp` | Horodatage du rapport. Si un paramètre `date` a été fourni pendant la demande, le rapport renvoyé correspond à la date fournie. Si aucun paramètre `date` n’est fourni, le rapport le plus récent est renvoyé. |

### Interprétation du rapport de chevauchement de jeux de données

Les résultats du rapport peuvent être interprétés à partir des jeux de données et du nombre de profils dans la réponse. Examinez l’exemple d’objet de rapport `data` suivant :

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Ce rapport fournit les informations suivantes :
* Il existe 123 profils composés de données provenant des jeux de données suivants : `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Il existe 454 412 profils composés de données provenant de ces deux jeux de données : `5d92921872831c163452edc8` et `5eb2cdc6fa3f9a18a7592a98`.
* 107 profils se composent uniquement de données provenant du jeu de données `5eeda0032af7bb19162172a7`.
* Il y a un total de 454 642 profils dans l’organisation.

## Génération du rapport de chevauchement d’identités

Le rapport sur le chevauchement d’identités offre une visibilité sur la composition de la banque de profils de votre entreprise en exposant les identités qui contribuent le plus à votre audience adressable (profils fusionnés). Cela inclut les identités standard fournies par Adobe, ainsi que les identités personnalisées définies par votre organisation.

Vous pouvez générer le rapport de chevauchement d’identités en effectuant une requête de GET sur le point de terminaison `/previewsamplestatus/report/identity/overlap` .

**Format d&#39;API**

```http
GET /previewsamplestatus/report/identity/overlap
GET /previewsamplestatus/report/identity/overlap?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à la même date, le rapport le plus récent pour cette date est renvoyé. Si un rapport n’existe pas pour la date spécifiée, une erreur 404 (Introuvable) est renvoyée. Si aucune date n’est spécifiée, le rapport le plus récent est renvoyé. Format : AAAA-MM-JJ. Exemple : `date=2024-12-31` |

**Requête**

La requête suivante utilise le paramètre `date` pour renvoyer le rapport le plus récent pour la date spécifiée.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/identity/overlap?date=2021-12-29 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Réponse**

Une requête réussie renvoie un état HTTP 200 (OK) et le rapport de chevauchement d’identités.

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
| `data` | L’objet `data` contient des listes séparées par des virgules avec des combinaisons uniques de codes d’espace de noms d’identité et leurs nombres de profils respectifs. |
| Codes d’espace de noms | `code` est un formulaire court pour chaque nom d’espace de noms d’identité. Vous trouverez un mappage de chaque `code` à sa `name` à l’aide de l’[API Adobe Experience Platform Identity Service](../../identity-service/api/list-namespaces.md). `code` est également appelé [!UICONTROL Symbole d’identité] dans l’interface utilisateur de l’Experience Platform. Pour en savoir plus, consultez la [présentation des espaces de noms d’identité](../../identity-service/namespaces.md). |
| `reportTimestamp` | Horodatage du rapport. Si un paramètre `date` a été fourni pendant la demande, le rapport renvoyé correspond à la date fournie. Si aucun paramètre `date` n’est fourni, le rapport le plus récent est renvoyé. |

### Interprétation du rapport de chevauchement d’identités

Les résultats du rapport peuvent être interprétés à partir des identités et du nombre de profils dans la réponse. La valeur numérique de chaque ligne indique le nombre de profils composés de cette combinaison exacte d’espaces de noms d’identité standard et personnalisés.

Examinez l’extrait suivant de l’objet `data` :

```json
  "AAID,ECID,Email,crmid": 142,
  "AVID,ECID": 24,
  "ECID": 6565
```

Ce rapport fournit les informations suivantes :
* Il existe 142 profils composés d’identités standard `AAID`, `ECID` et `Email`, ainsi que d’un espace de noms d’identité `crmid` personnalisé.
* Il existe 24 profils composés d’espaces de noms d’identité `AAID` et `ECID`.
* 6 565 profils incluent uniquement une identité `ECID`.

## Étapes suivantes

Maintenant que vous savez comment prévisualiser des données d’exemple dans la banque de profils et exécuter plusieurs rapports de chevauchement, vous pouvez également utiliser les points de terminaison d’estimation et de prévisualisation de l’API Segmentation Service pour afficher des informations sommaires sur vos définitions de segment. Ces informations vous permettent de vous assurer que vous isolez l’audience attendue dans votre segment. Pour en savoir plus sur l’utilisation des prévisualisations et des estimations de segments à l’aide de l’API Segmentation, consultez le [guide de prévisualisation et d’estimation des points de terminaison](../../segmentation/api/previews-and-estimates.md).

