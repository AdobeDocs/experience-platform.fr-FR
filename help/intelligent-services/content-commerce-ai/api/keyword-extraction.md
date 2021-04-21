---
keywords: Experience Platform ; prise en main ; contenu ai ; commerce ai ; contenu et commerce ai ; extraction de mots-clés ; extraction de mots-clés
solution: Experience Platform, Intelligent Services
title: Extraction de mots-clés dans l’API d’API Content and Commerce
topic-legacy: Developer guide
description: Le service d'extraction de mots-clés, lorsqu'il reçoit un document de texte, extrait automatiquement les mots-clés ou les expressions-clés qui décrivent le mieux le sujet du document. Afin d'extraire des mots-clés, une combinaison d'algorithmes de reconnaissance d'entité nommée (NER) et d'extraction de mot-clé non supervisée est utilisée.
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 4%

---

# Extraction des mots-clés

>[!NOTE]
>
>[!DNL Content and Commerce AI] est en version bêta. La documentation peut être modifiée.

Le service d&#39;extraction de mots-clés, lorsqu&#39;il reçoit un document de texte, extrait automatiquement les mots-clés ou les expressions-clés qui décrivent le mieux le sujet du document. Afin d&#39;extraire des mots-clés, une combinaison d&#39;algorithmes de reconnaissance d&#39;entité nommée (NER) et d&#39;extraction de mot-clé non supervisée est utilisée.

Les entités nommées reconnues par [!DNL Content and Commerce AI] sont répertoriées dans le tableau suivant :

| Nom de l’entité | Description |
| --- | --- |
| PERSONNE | Les gens, y compris les fictions. |
| NORP | Nationalités ou groupes religieux ou politiques. |
| GPE | Pays, villes et états. |
| LOC | Emplacements non-GPE, chaînes de montagnes, étendues d&#39;eau. |
| FAC | Bâtiments, aéroports, autoroutes, ponts, etc. |
| ORG | Sociétés, agences, institutions, etc. |
| PRODUIT | Objets, véhicules, aliments, etc. (Pas les services.) |
| ÉVÉNEMENT | ouragans, batailles, guerres, événements sportifs, etc. |
| WORK_OF_ART | Des titres de livres, de chansons, etc. |
| DROIT | Les documents nommés sont des lois. |
| LANGUE | Toute langue nommée. |

>[!NOTE]
>
>Si vous prévoyez de traiter des fichiers PDF, passez aux instructions relatives à l&#39;[extraction de mot-clé PDF](#pdf-extraction) dans ce document. En outre, la prise en charge d’autres types de fichiers, tels que docx, ppt et amd xml, est définie pour être publiée ultérieurement.

**Format d’API**

```http
POST /services/v1/predict
```

**Requête**

La requête suivante extrait les mots-clés d’un document en fonction des paramètres d’entrée fournis dans la charge utile.

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

Consultez le tableau ci-dessous pour plus d’informations sur les paramètres d’entrée affichés.

>[!CAUTION]
>
>`analyzer_id` détermine lequel  [!DNL Sensei Content Framework] est utilisé. Veuillez vérifier que vous disposez du `analyzer_id` approprié avant de faire votre demande. Pour le service d&#39;extraction de mots-clés, l&#39;ID `analyzer_id` est :
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
| `analyzer_id` | ID de service [!DNL Sensei] sous lequel votre requête est déployée. Cet identifiant détermine lequel des [!DNL Sensei Content Frameworks] est utilisé. Pour les services personnalisés, contactez l’équipe d’API Content and Commerce pour configurer un identifiant personnalisé. | Oui |
| `application-id` | ID de l’application créée. | Oui |
| `data` | Tableau contenant un objet JSON avec chaque objet du tableau représentant un document. Tout paramètre transmis dans le cadre de ce tableau remplace les paramètres globaux spécifiés en dehors du tableau `data`. Toutes les autres propriétés décrites ci-dessous dans ce tableau peuvent être remplacées à partir de `data`. | Oui |
| `language` | Langue du texte de saisie. La valeur par défaut est `en`. | Non |
| `content-type` | Permet d’indiquer si l’entrée fait partie du corps de la requête ou si une URL signée est associée à un compartiment S3. La valeur par défaut de cette propriété est `inline`. | Oui |
| `encoding` | Format de codage du texte d’entrée. Il peut s’agir de `utf-8` ou `utf-16`. La valeur par défaut de cette propriété est `utf-8`. | Non |
| `threshold` | Seuil de score (0 à 1) au-dessus duquel les résultats doivent être renvoyés. Utilisez la valeur `0` pour renvoyer tous les résultats. La valeur par défaut de cette propriété est `0`. | Non |
| `top-N` | Nombre de résultats à renvoyer (ne peut pas être un entier négatif). Utilisez la valeur `0` pour renvoyer tous les résultats. Lorsqu&#39;il est utilisé conjointement avec `threshold`, le nombre de résultats renvoyés est le moins élevé des deux limites définies. La valeur par défaut de cette propriété est `0`. | Non |
| `custom` | Tout paramètre personnalisé à transmettre. Cette propriété requiert un objet JSON valide pour fonctionner. Pour plus d&#39;informations sur les paramètres personnalisés, consultez l&#39;[annexe](#appendix). | Non |
| `content-id` | ID unique de l’élément de données renvoyé dans la réponse. Si elle n’est pas transmise, un identifiant généré automatiquement est attribué. | Non |
| `content` | Contenu utilisé par le service d&#39;extraction de mots-clés. Le contenu peut être du texte brut (type de contenu &quot;intégré&quot;). <br> Si le contenu est un fichier sur S3 (&#39;s3-bucket&#39; content-type), transmettez l’URL signée. Lorsque le contenu fait partie du corps de la requête, la liste des éléments de données ne doit comporter qu’un seul objet. Si plusieurs objets sont transmis, seul le premier objet est traité. | Oui |

**Réponse**

Une réponse réussie renvoie un objet JSON contenant des mots-clés extraits dans le tableau `response`.

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

## EXTRACTION du mot-clé PDF {#pdf-extraction}

Le service d’extraction de mots-clés prend en charge les fichiers PDF. Toutefois, vous devez utiliser un nouvel AnalyzerID pour les fichiers PDF et modifier le type de document en PDF. Consultez l’exemple ci-dessous pour plus d’informations.

**Format d’API**

```http
POST /services/v1/predict
```

**Requête**

La requête suivante extrait les mots-clés d’un document PDF en fonction des paramètres d’entrée fournis dans la charge utile.

>[!CAUTION]
>
>`analyzer_id` détermine lequel  [!DNL Sensei Content Framework] est utilisé. Veuillez vérifier que vous disposez du `analyzer_id` approprié avant de faire votre demande. Pour l’extraction du mot-clé PDF, l’ID `analyzer_id` est :
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
| `analyzer_id` | ID de service [!DNL Sensei] sous lequel votre requête est déployée. Cet identifiant détermine lequel des [!DNL Sensei Content Frameworks] est utilisé. Pour les services personnalisés, contactez l’équipe d’API Content and Commerce pour configurer un identifiant personnalisé. | Oui |
| `application-id` | ID de l’application créée. | Oui |
| `data` | Tableau contenant un objet JSON avec chaque objet du tableau représentant un document. Tout paramètre transmis dans le cadre de ce tableau remplace les paramètres globaux spécifiés en dehors du tableau `data`. Toutes les autres propriétés décrites ci-dessous dans ce tableau peuvent être remplacées à partir de `data`. | Oui |
| `language` | Langue de saisie. La valeur par défaut est `en` (anglais). | Non |
| `content-type` | Permet d’indiquer le type de contenu d’entrée. Il doit être défini sur `file`. | Oui |
| `encoding` | Format de codage de l’entrée. Il doit être défini sur `pdf`. D’autres types de codage sont définis pour être pris en charge ultérieurement. | Oui |
| `threshold` | Seuil de score (0 à 1) au-dessus duquel les résultats doivent être renvoyés. Utilisez la valeur `0` pour renvoyer tous les résultats. La valeur par défaut de cette propriété est `0`. | Non |
| `top-N` | Nombre de résultats à renvoyer (ne peut pas être un entier négatif). Utilisez la valeur `0` pour renvoyer tous les résultats. Lorsqu&#39;il est utilisé conjointement avec `threshold`, le nombre de résultats renvoyés est le moins élevé des deux limites définies. La valeur par défaut de cette propriété est `0`. | Non |
| `custom` | Tout paramètre personnalisé à transmettre. Cette propriété requiert un objet JSON valide pour fonctionner. Pour plus d&#39;informations sur les paramètres personnalisés, consultez l&#39;[annexe](#appendix). | Non |
| `content-id` | ID unique de l’élément de données renvoyé dans la réponse. Si elle n’est pas transmise, un identifiant généré automatiquement est attribué. | Non |
| `content` | Il doit être défini sur `file`. | Oui |

**Réponse**

Une réponse réussie renvoie un objet JSON contenant des mots-clés extraits dans le tableau `response`.

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

Pour plus d’informations et un exemple sur l’utilisation de l’extraction PDF contenant des instructions sur la configuration, le déploiement et l’intégration avec le service AEM cloud. Visitez le [référentiel github de l’extraction PDF CCAI](https://github.com/adobe/asset-compute-example-workers/tree/master/projects/worker-ccai-pdfextract).

## Annexe {#appendix}

Le tableau suivant contient les paramètres disponibles qui peuvent être utilisés à partir de `custom`.

| Nom | Description | Obligatoire |
| --- | --- | --- |
| `min-n` | Nombre minimum de mots requis dans les mots-clés. | Non |
| `entity-types` | Types d&#39;entités à renvoyer. Consultez le tableau de reconnaissance des entités nommées au début de ce document. | Non |
