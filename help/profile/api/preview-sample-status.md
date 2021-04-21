---
keywords: Experience Platform ; profil ; profil client en temps réel ; résolution des problèmes ; API ; prévisualisation ; exemple
title: Point de terminaison de l’API de l’exemple de statut de prévisualisation (Prévisualisation de Profil)
description: À l’aide de l’exemple de point de terminaison d’état de la prévisualisation, qui fait partie de l’API Profil client en temps réel, vous pouvez prévisualisation le dernier échantillon réussi de vos données de Profil, ainsi que la distribution des profils de liste par jeu de données et par espace de nommage d’identité dans Adobe Experience Platform.
topic-legacy: guide
exl-id: a90a601e-629e-417b-ac27-3d69379bb274
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1655'
ht-degree: 4%

---

# Point de terminaison d’état de l’exemple de prévisualisation (prévisualisation de Profil)

Adobe Experience Platform vous permet d&#39;assimiler des données client provenant de plusieurs sources afin de créer des profils unifiés robustes pour chaque client. Les données activées pour le Profil client en temps réel étant ingérées dans [!DNL Platform], elles sont stockées dans le magasin de données du Profil.

Lorsque l&#39;ingestion d&#39;enregistrements dans le magasin de Profils augmente ou diminue le nombre total de profils de plus de 5 %, une tâche d&#39;échantillonnage est déclenchée pour mettre à jour le nombre. La façon dont l’échantillon est déclenché dépend du type d’ingestion utilisé :

* Pour **les workflows de données en flux continu**, une vérification est effectuée sur une base horaire afin de déterminer si le seuil de 5 % d&#39;augmentation ou de diminution a été atteint. Si tel est le cas, un exemple de tâche est automatiquement déclenché pour mettre à jour le décompte.
* Pour **l&#39;assimilation par lot**, dans les 15 minutes suivant l&#39;assimilation réussie d&#39;un lot dans le magasin de Profils, si le seuil de 5 % d&#39;augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour le décompte. L&#39;API Profil vous permet de prévisualisation de la dernière tâche d&#39;exemple réussie, ainsi que de la distribution de profil de liste par jeu de données et par espace de nommage d&#39;identité.

Ces mesures sont également disponibles dans la section [!UICONTROL Profils] de l’interface utilisateur Experience Platform. Pour plus d&#39;informations sur la façon d&#39;accéder aux données de Profil à l&#39;aide de l&#39;interface utilisateur, consultez le [[!DNL Profile] guide de l&#39;utilisateur](../ui/user-guide.md).

>[!NOTE]
>
>Il existe des points de terminaison d’estimation et de prévisualisation disponibles dans le cadre de l’API Adobe Experience Platform Segmentation Service qui vous permettent de vue des informations de niveau récapitulatif concernant les définitions de segment afin de vous assurer que vous isolez l’audience attendue. Pour obtenir des instructions détaillées sur l&#39;utilisation de la prévisualisation de segments et des points de terminaison d&#39;estimation, consultez le [guide des points de terminaison des prévisualisations et des estimations](../../segmentation/api/previews-and-estimates.md), qui fait partie du guide du développeur d&#39;API [!DNL Segmentation].

## Prise en main

Le point de terminaison API utilisé dans ce guide fait partie de l&#39;[[!DNL Real-time Customer Profile] API](https://www.adobe.com/go/profile-apis-en). Avant de continuer, consultez le [guide de prise en main](getting-started.md) pour obtenir des liens vers la documentation connexe, un guide de lecture des exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API [!DNL Experience Platform].

## Fragments de profil par rapport aux profils fusionnés

Ce guide fait référence à la fois aux &quot;fragments de profil&quot; et aux &quot;profils fusionnés&quot;. Il est important de comprendre la différence entre ces termes avant de procéder.

Chaque profil client individuel est composé de plusieurs fragments de profil qui ont été fusionnés pour former une seule vue du client. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, votre entreprise aura plusieurs fragments de profil liés à ce client unique qui apparaîtront dans plusieurs jeux de données. Lorsque ces fragments sont ingérés dans la plate-forme, ils sont fusionnés ensemble (en fonction de la stratégie de fusion) afin de créer un profil unique pour ce client. Par conséquent, il est probable que le nombre total de fragments de profil soit toujours supérieur au nombre total de profils fusionnés, chaque profil étant composé de fragments multiples.

## Etat du dernier exemple de vue {#view-last-sample-status}

Vous pouvez exécuter une demande de GET au point de terminaison `/previewsamplestatus` pour vue les détails du dernier exemple de travail réussi qui a été exécuté pour votre organisation IMS. Cela inclut le nombre total de profils dans l’exemple, ainsi que la mesure Nombre de profils ou le nombre total de profils de votre organisation dans l’Experience Platform. Le nombre de profils est généré après la fusion de fragments de profil afin de former un seul profil pour chaque client. En d’autres termes, votre organisation peut disposer de plusieurs fragments de profil liés à un seul client qui interagit avec votre marque sur différents canaux, mais ces fragments sont fusionnés (selon la stratégie de fusion par défaut) et renvoient le nombre de profils « 1 », car ils sont tous liés à la même personne.

Le nombre de profils inclut également les profils avec des attributs (données d’enregistrement) ainsi que les profils contenant uniquement des données de séries chronologiques (événement), telles que les profils de Adobe Analytics. L’exemple de tâche est régulièrement actualisé lorsque des données de Profil sont ingérées afin de fournir un nombre total de profils actualisé dans la plateforme.

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

La réponse comprend les détails de la dernière tâche exemple réussie qui a été exécutée pour l&#39;organisation IMS.

>[!NOTE]
>
>Dans cet exemple de réponse, `numRowsToRead` et `totalRows` sont égaux les uns aux autres. Cela peut être le cas en fonction du nombre de profils de votre organisation en Experience Platform. Cependant, en règle générale, ces deux nombres sont différents, `numRowsToRead` étant le nombre le plus petit, car il représente l’échantillon sous la forme d’un sous-ensemble du nombre total de profils (`totalRows`).

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
| `numRowsToRead` | Nombre total de profils fusionnés dans l’échantillon. |
| `sampleJobRunning` | Valeur booléenne qui renvoie `true` lorsqu&#39;un exemple de travail est en cours. Fournit de la transparence dans la latence qui survient lorsqu’un fichier de commandes est téléchargé lorsqu’il est effectivement ajouté au magasin de Profils. |
| `cosmosDocCount` | Nombre total de documents dans Cosmos. |
| `totalFragmentCount` | Nombre total de fragments de profil dans le magasin de Profils. |
| `lastSuccessfulBatchTimestamp` | Dernier horodatage d&#39;assimilation par lot réussi. |
| `streamingDriven` | *Ce champ est obsolète et ne contient aucune signification pour la réponse.* |
| `totalRows` | Nombre total de profils fusionnés en Experience Platform, également appelé &quot;nombre de profils&quot;. |
| `lastBatchId` | Dernier identifiant d&#39;assimilation par lot. |
| `status` | État du dernier échantillon. |
| `samplingRatio` | Ratio des profils fusionnés échantillonnés (`numRowsToRead`) par rapport au total des profils fusionnés (`totalRows`), exprimé en pourcentage au format décimal. |
| `mergeStrategy` | Stratégie de fusion utilisée dans l’exemple. |
| `lastSampledTimestamp` | Dernier exemple d’horodatage réussi. |

## Profil de liste par jeu de données

Pour voir la distribution des profils par jeu de données, vous pouvez exécuter une requête de GET au point de terminaison `/previewsamplestatus/report/dataset`.

**Format d’API**

```http
GET /previewsamplestatus/report/dataset
GET /previewsamplestatus/report/dataset?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à la date, le rapport le plus récent pour cette date est renvoyé. Si un rapport n&#39;existe pas pour la date spécifiée, une erreur 404 est renvoyée. Si aucune date n&#39;est spécifiée, le rapport le plus récent est renvoyé. Format : AAAA-MM-JJ. Exemple : `date=2024-12-31` |

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

La réponse comprend un tableau `data` contenant une liste d&#39;objets de jeu de données. La réponse affichée a été tronquée pour afficher trois jeux de données.

>[!NOTE]
>
>Si plusieurs rapports existaient pour la date, seuls les derniers rapports sont renvoyés. Si un rapport de jeu de données n’existait pas pour la date fournie, l’état HTTP 404 (introuvable) est renvoyé.

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
| `sampleCount` | Nombre total de profils fusionnés échantillonnés avec cet ID de jeu de données. |
| `samplePercentage` | `sampleCount` en pourcentage du nombre total de profils fusionnés échantillonnés (valeur `numRowsToRead` renvoyée dans le [dernier état d’échantillonnage](#view-last-sample-status)), exprimée au format décimal. |
| `fullIDsCount` | Nombre total de profils fusionnés avec cet ID de jeu de données. |
| `fullIDsPercentage` | Le `fullIDsCount` en pourcentage du nombre total de profils fusionnés (la valeur `totalRows` renvoyée dans le [dernier état d’échantillonnage](#view-last-sample-status)), exprimé au format décimal. |
| `name` | Nom du jeu de données, tel qu’il est fourni lors de la création du jeu de données. |
| `description` | Description du jeu de données, telle qu’elle est fournie lors de la création du jeu de données. |
| `value` | ID du jeu de données. |
| `streamingIngestionEnabled` | Indique si le jeu de données est activé pour l’assimilation en flux continu. |
| `createdUser` | ID utilisateur de l’utilisateur qui a créé le jeu de données. |
| `reportTimestamp` | Horodatage du rapport. Si un paramètre `date` a été fourni pendant la demande, le rapport renvoyé correspond à la date fournie. Si aucun paramètre `date` n&#39;est fourni, le rapport le plus récent est renvoyé. |

## Répartition des profils listes par espace de nommage

Vous pouvez exécuter une demande de GET au point de terminaison `/previewsamplestatus/report/namespace` pour vue la ventilation par espace de nommage d&#39;identité sur tous les profils fusionnés de votre magasin de Profils. Les espaces de nommage d&#39;identité sont un composant important du service d&#39;identité Adobe Experience Platform qui sert d&#39;indicateur du contexte auquel se rapportent les données client. Pour en savoir plus, consultez la [présentation de l&#39;espace de nommage d&#39;identité](../../identity-service/namespaces.md).

>[!NOTE]
>
>Le nombre total de profils par espace de nommage (additionnant les valeurs affichées pour chaque espace de nommage) sera toujours supérieur à la mesure Nombre de profils car un profil peut être associé à plusieurs espaces de nommage. Par exemple, si un client interagit avec votre marque sur plusieurs canaux, plusieurs espaces de nommage sont associés à ce client individuel.

**Format d’API**

```http
GET /previewsamplestatus/report/namespace
GET /previewsamplestatus/report/namespace?{QUERY_PARAMETERS}
```

| Paramètre | Description |
|---|---|
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à la date, le rapport le plus récent pour cette date est renvoyé. Si un rapport n&#39;existe pas pour la date spécifiée, une erreur 404 est renvoyée. Si aucune date n&#39;est spécifiée, le rapport le plus récent est renvoyé. Format : AAAA-MM-JJ. Exemple : `date=2024-12-31` |

**Requête**

La requête suivante ne spécifie pas de paramètre `date` et renvoie donc le rapport le plus récent.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/namespace \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

La réponse comprend un tableau `data`, avec des objets individuels contenant les détails de chaque espace de nommage. La réponse affichée a été tronquée pour afficher quatre espaces de nommage.

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
| `sampleCount` | Nombre total de profils fusionnés échantillonnés dans l’espace de nommage. |
| `samplePercentage` | Le `sampleCount` en pourcentage des profils fusionnés échantillonnés (valeur `numRowsToRead` renvoyée dans le [dernier état d&#39;échantillonnage](#view-last-sample-status)), exprimé au format décimal. |
| `reportTimestamp` | Horodatage du rapport. Si un paramètre `date` a été fourni pendant la demande, le rapport renvoyé correspond à la date fournie. Si aucun paramètre `date` n&#39;est fourni, le rapport le plus récent est renvoyé. |
| `fullIDsFragmentCount` | Nombre total de fragments de profil dans l’espace de nommage. |
| `fullIDsCount` | Nombre total de profils fusionnés dans l’espace de nommage. |
| `fullIDsPercentage` | Le `fullIDsCount` en pourcentage du total des profils fusionnés (la valeur `totalRows` renvoyée dans le [dernier état de l’échantillon](#view-last-sample-status)), exprimé au format décimal. |
| `code` | `code` pour l&#39;espace de nommage. Vous pouvez le trouver lorsque vous travaillez avec des espaces de nommage à l&#39;aide de l&#39;[API Service d&#39;identité de Adobe Experience Platform](../../identity-service/api/list-namespaces.md) et il est également appelé [!UICONTROL symbole d&#39;identité] dans l&#39;interface utilisateur Experience Platform. Pour en savoir plus, consultez la [présentation de l&#39;espace de nommage d&#39;identité](../../identity-service/namespaces.md). |
| `value` | Valeur `id` de l’espace de nommage. Vous pouvez le trouver lorsque vous travaillez avec des espaces de nommage à l&#39;aide de l&#39;[API Identity Service](../../identity-service/api/list-namespaces.md). |

## Étapes suivantes

Maintenant que vous savez comment prévisualisation des données d’exemple dans le magasin de Profils, vous pouvez également utiliser les points de terminaison d’estimation et de prévisualisation de l’API du service de segmentation pour vue des informations de niveau récapitulatif concernant vos définitions de segment. Ces informations vous permettent de vous assurer que vous isolez l’audience attendue dans votre segment. Pour en savoir plus sur l’utilisation des prévisualisations de segments et des estimations à l’aide de l’API de segmentation, consultez le [guide des points de terminaison de la prévisualisation et de l’estimation](../../segmentation/api/previews-and-estimates.md).
