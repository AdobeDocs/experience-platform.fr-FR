---
keywords: Experience Platform;prise en main;contenu;commerce ai;contenu et commerce ai;extraction de mots-clés;extraction de mots-clés
solution: Experience Platform
title: Extraction de mots-clés dans l’API Content and Commerce AI
description: Le service d’extraction de mots-clés, lorsqu’il reçoit un document texte, extrait automatiquement les mots-clés ou les expressions-clés qui décrivent le mieux l’objet du document. Pour extraire des mots-clés, une combinaison d’algorithmes NER (nom de l’entité) et d’extraction de mots-clés non surveillés est utilisée.
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 4%

---

# Extraction des mots-clés

>[!NOTE]
>
>[!DNL Content and Commerce AI] est en version bêta. La documentation peut être modifiée.

Le service d’extraction de mots-clés, lorsqu’il reçoit un document texte, extrait automatiquement les mots-clés ou les expressions-clés qui décrivent le mieux l’objet du document. Pour extraire des mots-clés, une combinaison d’algorithmes NER (nom de l’entité) et d’extraction de mots-clés non surveillés est utilisée.

Les entités nommées reconnues par [!DNL Content and Commerce AI] sont répertoriés dans le tableau suivant :

| Nom de l’entité | Description |
| --- | --- |
| PERSONNE | Des gens, y compris de la fiction. |
| NORP | Nationalités ou groupes religieux ou politiques. |
| GPE | Pays, villes et états. |
| LOC | Emplacements non-GPE, étendues de montagne, étendues d&#39;eau. |
| FAC | Bâtiments, aéroports, autoroutes, ponts, etc. |
| ORG | Entreprises, agences, institutions, etc. |
| PRODUIT | Objets, véhicules, aliments, etc. (Pas les services.) |
| ÉVÉNEMENT | ouragans, batailles, guerres, événements sportifs, etc. |
| WORK_OF_ART | Des titres de livres, de chansons, etc. |
| LOI | Les documents nommés deviennent des lois. |
| LANGUE | Toute langue nommée. |

>[!NOTE]
>
>Si vous prévoyez d’utiliser des PDF de traitement, passez aux instructions pour [Extraction de mots-clés PDF](#pdf-extraction) dans ce document. En outre, la prise en charge d’autres types de fichiers, tels que docx, ppt et amd xml, doit être publiée ultérieurement.

**Format d’API**

```http
POST /services/v1/predict
```

**Requête**

La requête suivante extrait les mots-clés d’un document en fonction des paramètres d’entrée fournis dans le payload.

JSON simplifié du fichier d’entrée :

```json
{
  "application-id": "1234",
  "language": "en",
  "content-type": "inline",
  "encoding": "utf-8",
  "threshold": 0.01,
  "top-N": 10,
  "custom": {
    "min-n": 2,
    "entity-types": ["PERSON"]
  },
  "data": [
    {
      "content-id": "abc123",
      "content": "But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31"
    }
  ]
}
```

Pour plus d’informations sur les paramètres d’entrée affichés, reportez-vous au tableau ci-dessous de l’exemple de payload.

>[!CAUTION]
>
>`analyzer_id` détermine [!DNL Sensei Content Framework] est utilisée. Vérifiez que vous disposez des `analyzer_id` avant d’effectuer votre requête. Pour le service d&#39;extraction de mots-clés, la variable `analyzer_id` L’ID est :
>`Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file="{
    \"application-id\": \"1234\", 
    \"language\": \"en\", 
    \"content-type\": \"inline\", 
    \"encoding\": \"utf-8\",
    \"threshold\": 0.01,
    \"top-N\": 10,
    \"custom\": {
        \"min-n\": 2,
        \"entity-types\": [\"PERSON\"]
      },
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"But an influential faction on the ATP player council, which is chaired by Novak Djokovic, staged a rebellion against Kermodes regime in the spring, and he will leave the post on Dec 31\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
         "parameters": {}
    }]
}'
```

| Propriété | Description | Obligatoire |
| --- | --- | --- |
| `analyzer_id` | Le [!DNL Sensei] ID de service sous lequel votre requête est déployée. Cet identifiant détermine laquelle de la variable [!DNL Sensei Content Frameworks] sont utilisées. Pour les services personnalisés, contactez l’équipe Content and Commerce AI pour configurer un identifiant personnalisé. | Oui |
| `application-id` | L’identifiant de l’application créée. | Oui |
| `data` | Tableau contenant un objet JSON dont chaque objet du tableau représente un document. Tous les paramètres transmis dans le cadre de ce tableau remplacent les paramètres globaux spécifiés en dehors de la variable `data` tableau. Toutes les propriétés restantes décrites ci-dessous dans ce tableau peuvent être remplacées dans . `data`. | Oui |
| `language` | Langue du texte de saisie. La valeur par défaut est `en`. | Non |
| `content-type` | Utilisé pour indiquer si l’entrée fait partie du corps de la requête ou une URL signée pour un compartiment S3. La valeur par défaut de cette propriété est `inline`. | Oui |
| `encoding` | Format de codage du texte d’entrée. Cela peut être `utf-8` ou `utf-16`. La valeur par défaut de cette propriété est `utf-8`. | Non |
| `threshold` | Seuil de score (0 à 1) au-dessus duquel les résultats doivent être renvoyés. Utiliser la valeur `0` pour renvoyer tous les résultats. La valeur par défaut de cette propriété est `0`. | Non |
| `top-N` | Nombre de résultats à renvoyer (ne peut pas être un entier négatif). Utiliser la valeur `0` pour renvoyer tous les résultats. Utilisé conjointement avec `threshold`, le nombre de résultats renvoyés est le plus petit des jeux de limites. La valeur par défaut de cette propriété est `0`. | Non |
| `custom` | Tous les paramètres personnalisés à transmettre. Cette propriété requiert un objet JSON valide pour fonctionner. Voir [annexe](#appendix) pour plus d’informations sur les paramètres personnalisés. | Non |
| `content-id` | Identifiant unique de l’élément de données renvoyé dans la réponse. Si cette variable n’est pas transmise, un identifiant généré automatiquement est attribué. | Non |
| `content` | Contenu utilisé par le service d’extraction de mots-clés. Le contenu peut être du texte brut (type de contenu &quot;intégré&quot;). <br> Si le contenu est un fichier sur S3 (type de contenu &quot;s3-bucket&quot;), transmettez l’URL signée. Lorsque le contenu fait partie de request-body, la liste des éléments de données ne doit comporter qu’un seul objet. Si plusieurs objets sont transmis, seul le premier objet est traité. | Oui |

**Réponse**

Une réponse réussie renvoie un objet JSON contenant des mots-clés extraits dans la variable `response` tableau.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-ner:Service-1a35aefb0f0f4dc0a3b5262370ebc709",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "success",
                "feature_name": "status"
              },
              {
                "feature_name": "labels",
                "feature_value": [
                  {
                    "feature_name": "atp player",
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ]
                  },
                  {
                    "feature_name": "Novak Djokovic",
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "PERSON"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0
                      }
                    ]
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_value": 0.00899321792126428,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "player council"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_value": "KEYWORD",
                        "feature_name": "type"
                      },
                      {
                        "feature_value": 0.007743432063478832,
                        "feature_name": "score"
                      }
                    ],
                    "feature_name": "kermodes regime"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "type",
                        "feature_value": "KEYWORD"
                      },
                      {
                        "feature_name": "score",
                        "feature_value": 0.0006052376660884209
                      }
                    ],
                    "feature_name": "atp player council"
                  }
                ]
              }
            ],
            "feature_name": "abc123"
          }
        ]
      }
    }
  ],
  "error": []
}
```

## Extraction de mots-clés PDF {#pdf-extraction}

Le service d’extraction de mots-clés prend en charge les PDF. Cependant, vous devez utiliser un nouvel AnalyzerID pour les fichiers de PDF et définir le type de document sur PDF. Voir l’exemple ci-dessous pour plus d’informations.

**Format d’API**

```http
POST /services/v1/predict
```

**Requête**

La requête suivante extrait les mots-clés d’un document de PDF en fonction des paramètres d’entrée fournis dans le payload.

>[!CAUTION]
>
>`analyzer_id` détermine [!DNL Sensei Content Framework] est utilisée. Vérifiez que vous disposez des `analyzer_id` avant d’effectuer votre requête. Pour l’extraction de mots-clés PDF, la variable `analyzer_id` L’ID est :
>`Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5`

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestPDF.pdf \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
    "parameters": {
      "application-id": "1234",
      "content-type": "file",
      "encoding": "pdf",
      "threshold": "0.01",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "abc123",
        "content": "file",
        }]
      }
    }]
  }'
```

| Propriété | Description | Obligatoire |
| --- | --- | --- |
| `analyzer_id` | Le [!DNL Sensei] ID de service sous lequel votre requête est déployée. Cet identifiant détermine laquelle de la variable [!DNL Sensei Content Frameworks] sont utilisées. Pour les services personnalisés, contactez l’équipe Content and Commerce AI pour configurer un identifiant personnalisé. | Oui |
| `application-id` | L’identifiant de l’application créée. | Oui |
| `data` | Tableau contenant un objet JSON dont chaque objet du tableau représente un document. Tous les paramètres transmis dans le cadre de ce tableau remplacent les paramètres globaux spécifiés en dehors de la variable `data` tableau. Toutes les propriétés restantes décrites ci-dessous dans ce tableau peuvent être remplacées dans . `data`. | Oui |
| `language` | Langue de saisie. La valeur par défaut est `en` (en anglais). | Non |
| `content-type` | Utilisé pour indiquer le type de contenu des entrées. Cette variable doit être définie sur `file`. | Oui |
| `encoding` | Format de codage de l’entrée. Cette variable doit être définie sur `pdf`. D’autres types de codage doivent être pris en charge ultérieurement. | Oui |
| `threshold` | Seuil de score (0 à 1) au-dessus duquel les résultats doivent être renvoyés. Utiliser la valeur `0` pour renvoyer tous les résultats. La valeur par défaut de cette propriété est `0`. | Non |
| `top-N` | Nombre de résultats à renvoyer (ne peut pas être un entier négatif). Utiliser la valeur `0` pour renvoyer tous les résultats. Utilisé conjointement avec `threshold`, le nombre de résultats renvoyés est le plus petit des jeux de limites. La valeur par défaut de cette propriété est `0`. | Non |
| `custom` | Tous les paramètres personnalisés à transmettre. Cette propriété requiert un objet JSON valide pour fonctionner. Voir [annexe](#appendix) pour plus d’informations sur les paramètres personnalisés. | Non |
| `content-id` | Identifiant unique de l’élément de données renvoyé dans la réponse. Si cette variable n’est pas transmise, un identifiant généré automatiquement est attribué. | Non |
| `content` | Cette variable doit être définie sur `file`. | Oui |

**Réponse**

Une réponse réussie renvoie un objet JSON contenant des mots-clés extraits dans la variable `response` tableau.

```json
{
  "statusCode": 200,
  "body": {
    "type": "JSON",
    "matchType": "strict",
    "json": {
      "status": 200,
      "content_id": "161hw2.pdf",
      "cas_responses": [
        {
          "status": 200,
          "analyzer_id": "Feature:cintel-ner:Service-7a87cb57461345c280b62470920bcdc5",
          "content_id": "161hw2.pdf",
          "result": {
            "response_type": "feature",
            "response": [
              {
                "feature_value": [
                  {
                    "feature_name": "status",
                    "feature_value": "success"
                  },
                  {
                    "feature_value": [
                      {
                        "feature_name": "delbick",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0.03673855028832046
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "KEYWORD"
                          }
                        ]
                      },
                      {
                        "feature_name": "Ci",
                        "feature_value": [
                          {
                            "feature_name": "score",
                            "feature_value": 0
                          },
                          {
                            "feature_name": "type",
                            "feature_value": "PERSON"
                          }
                        ]
                      }
                    ],
                    "feature_name": "labels"
                  }
                ],
                "feature_name": "abc123"
              }
            ]
          }
        }
      ],
      "error": []
    }
  }
}
```

Pour plus d’informations et un exemple sur l’utilisation de l’extraction de PDF contenant des instructions sur la configuration, le déploiement et l’intégration avec le service cloud AEM. Visitez le [Référentiel github du programme de travail d’extraction de PDF CCAI](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract).

## Annexe {#appendix}

Le tableau suivant contient les paramètres disponibles qui peuvent être utilisés dans `custom`.

| Nom | Description | Obligatoire |
| --- | --- | --- |
| `min-n` | Nombre minimum de mots requis dans les mots-clés. | Non |
| `entity-types` | Types d’entités à renvoyer. Consultez le tableau de reconnaissance des entités nommées au début de ce document. | Non |
