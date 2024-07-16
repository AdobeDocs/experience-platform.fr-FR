---
keywords: OCR;présence de texte;reconnaissance optique de caractères
solution: Experience Platform
title: Présence de texte et reconnaissance optique des caractères
description: Dans l’API Content Tagging, le service Text Presence/Optical Character Reconnaissance (OCR) peut indiquer si du texte est présent dans une image donnée. Si du texte est présent, la reconnaissance optique des caractères peut renvoyer le texte.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: 82722ddf7ff543361177b555fffea730a7879886
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 4%

---

# Présence de texte et reconnaissance optique des caractères

Lorsqu’une image est fournie, le service de reconnaissance de caractères optique/présence de texte peut indiquer si du texte est présent dans l’image. Si du texte est présent, la reconnaissance optique des caractères peut renvoyer le texte.

L’image suivante a été utilisée dans l’exemple de requête illustré dans ce document :

![Exemple d’image](../images/sample_image.png)

**Format d’API**

```http
POST /services/v2/predict
```

**Requête**

La requête suivante vérifie si du texte est présent en fonction de l’image d’entrée fournie dans le payload. Pour plus d’informations sur les paramètres d’entrée affichés, reportez-vous au tableau ci-dessous de l’exemple de payload.

Exécution avec image intégrée :

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F file=@sample_image.png \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "sensei:multipart_field_name": "file",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true,
        "min_probability": 0.2,
        "min_relevance": 0.01,
        "filter_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

**Réponse**

Une réponse réussie renvoie le texte qui a été détecté dans la liste `tags` pour chaque image qui a été transmise dans la requête. S’il n’y a pas de texte dans une certaine image, `is_text_present` a 0 et `tags` est une liste vide.

[result0, result1, ...] : liste des réponses pour chaque document d’entrée. Chaque résultat est un dict avec des clés :

1. request_element_id : index correspondant au fichier d’entrée pour cette réponse, 0 pour la première image de la liste de documents de la requête, 1 pour la suivante, etc.
2. balises : liste des dictionnaires, chaque dictionnaire comporte deux clés : le texte, qui est un mot reconnu de l’image, et la pertinence, qui est calculé comme la fraction de la zone du cadre de sélection du texte extrait par rapport à l’image complète. 0,01 correspond à un texte occupant au moins 1 % de l’image.
3. is_text_present : 0 ou 1 selon si du texte est présent dans l’image. Si la valeur des balises est 0, la liste est vide.

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "dttklFR7DPtMtEmjlRSx5BYP5WGg3tTx"
  },
  "result": [
    {
      "is_text_present": 1,
      "tags": [
        {
          "text": "yosemite",
          "relevance": 0.06
        }
      ],
      "request_element_id": 0
    }
  ]
}
```

**Requête**

La requête suivante vérifie si du texte est présent en fonction de l’image d’entrée fournie dans le payload. Pour plus d’informations sur les paramètres d’entrée affichés, reportez-vous au tableau ci-dessous de l’exemple de payload.

Exécution avec URL :

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
  "sensei:invocation_mode": "asynchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690"
      },
      "sensei:inputs": {
        "documents": [
        {
          "repo:path": <IMG_URL_PATH>,
          "sensei:repoType": "HTTP",
          "dc:format": "image/jpg"
        }
        ]
      },
      "sensei:params": {
        "correct_with_dictionary": true
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}'
```

```json
{
  "contentAnalyzerResponse": {
    "statuses": [
      {
        "sensei:engine": "Feature:cintel-object-detection:Service-b9ace8b348b6433e9e7d82371aa16690",
        "invocations": [
          {
            "sensei:outputs": {
              "result": {
                "sensei:multipart_field_name": "result",
                "dc:format": "application/json"
              }
            },
            "message": null,
            "status": "200"
          }
        ]
      }
    ],
    "request_id": "ZbdhcK0JqS4Wg1wGdlEHGR3JOm530YNn"
  },
  "result": [
    {
      "is_text_present": 0,
      "tags": [],
      "request_element_id": 0
    }
  ]
}
```

| Propriété | Description | Obligatoire |
| --- | --- | --- |
| `documents` | Liste des éléments JSON dont chaque élément de la liste représente une image. Tous les paramètres transmis dans le cadre de cette liste remplacent le paramètre global spécifié en dehors de la liste, pour l’élément de liste correspondant. | Oui |
| `sensei:multipart_field_name` | field_name pour lire le chemin du fichier d’entrée. | Oui |
| `repo:path` | URL présignée à la ressource image. | Oui |
| `sensei:repoType` | &quot;HTTP&quot; (pour presigned-url). | Non |
| `dc:format` | Format codé de l’image d’entrée. Seuls les formats d’image tels que jpeg, jpg, png et tiff sont autorisés pour le codage d’image. Le format dc:format est comparé aux formats autorisés. | Non |
| `correct_with_dictionary` | Est-il possible de corriger les mots avec un dictionnaire d&#39;anglais ? Si cette option n’est pas activée, il est possible que des mots non anglais soient reconnus. La valeur par défaut est True : activée.) Notez que lorsque le dictionnaire est activé, il n’est pas nécessaire d’obtenir toujours un mot anglais. Nous essayons de le corriger, mais si ce n&#39;est pas possible dans un certain délai d&#39;édition, nous retournons le mot d&#39;origine. | Non |
| `filter_with_dictionary` | Est-il possible de filtrer les mots pour ne contenir que les mots du dictionnaire anglais ? Si cette option est activée, les mots renvoyés appartiennent toujours au grand anglais , qui comprend 470 000 mots. | Non |
| `min_probability` | Quelle est la probabilité minimale pour les mots reconnus ? Seuls les mots extraits de l’image et ayant une probabilité supérieure à min_probabilité sont renvoyés par le service. La valeur par défaut est 0,2. | Non |
| `min_relevance` | Quelle est la pertinence minimale pour les mots reconnus ? Seuls les mots extraits de l’image et ayant une plus grande pertinence que min_relevant sont renvoyés par le service. La valeur par défaut est 0,01. La pertinence correspond à la fraction de la zone du cadre de sélection du texte extrait par rapport à l’image complète. 0,01 correspond à un texte occupant au moins 1 % de l’image. | Non |

| Nom | Type de données | Obligatoire | Par défaut | Valeurs | Description |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | chaîne | - | - | - | URL présignée de l’image à partir de laquelle le texte doit être extrait. |
| `sensei:repoType` | Chaîne | - | - | HTTPS | Type de référentiel dans lequel l’image est stockée. |
| `sensei:multipart_field_name` | Chaîne | - | - | - | Utilisez-le lorsque vous transmettez l’image en tant qu’argument en plusieurs parties au lieu d’utiliser des URL présignées. |
| `dc:format` | Chaîne | Oui | - | &quot;image/jpg&quot;, <br>&quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | Le codage des images est comparé aux types de codage d’entrée autorisés avant d’être traité. |