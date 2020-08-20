---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;keyword extraction;Keyword extraction
solution: Experience Platform
title: Extraction des couleurs
topic: Developer guide
description: Le service d'extraction de mots-clés, lorsqu'il reçoit un document de texte, extrait automatiquement les mots-clés ou les expressions-clés qui décrivent le mieux le sujet du document. Afin d'extraire des mots-clés, une combinaison d'algorithmes de reconnaissance d'entité nommée (NER) et d'extraction de mot-clé non supervisée est utilisée.
translation-type: tm+mt
source-git-commit: e69f4e8ddc0fe5f7be2b2b2bd89c09efdfca8e75
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 4%

---


# Extraction des mots-clés

>[!NOTE]
>
>[!DNL Content and Commerce AI] est en version bêta. La documentation peut être modifiée.

Le service d&#39;extraction de mots-clés, lorsqu&#39;il reçoit un document de texte, extrait automatiquement les mots-clés ou les expressions-clés qui décrivent le mieux le sujet du document. Afin d&#39;extraire des mots-clés, une combinaison d&#39;algorithmes de reconnaissance d&#39;entité nommée (NER) et d&#39;extraction de mot-clé non supervisée est utilisée.

**Extraction de mots-clés non surveillée**

Pour l&#39;extraction non supervisée du mot-clé, [[ !DNL YAKE]](http://yake.inesctec.pt/) est utilisé. [!DNL YAKE] est une méthode d&#39;extraction automatique des mots-clés rapide et précise, non supervisée, utilisée pour sélectionner les mots-clés les plus importants d&#39;un document. Les extraits de mots-clés [!DNL YAKE] sont ensuite filtrés afin de ne sélectionner que des phrases de nom.

**Reconnaissance d&#39;entité nommée**

Pour la reconnaissance d’entité nommée, le modèle OntoNotes de [[ !DNL spaCy]](https://spacy.io/)est utilisé. Ce modèle affecte des vecteurs de jeton spécifiques au contexte, des balises POS (partie de parole), l’analyse des dépendances et des entités nommées. Le modèle OntoNotes est l’un des modèles principaux [!DNL spaCy] . Vous trouverez plus d&#39;informations sur le modèle OntoNotes [ici](https://spacy.io/models/en).

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

Les résultats de [!DNL OntoNotes] sont combinés aux mots-clés de [!DNL YAKE]et sont ensuite renvoyés par ordre de classement en fonction de leur importance.

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
>`analyzer_id` détermine lequel [!DNL Sensei Content Framework] est utilisé. Veuillez vérifier que vous en avez le bon `analyzer_id` avant de faire votre demande.

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
| `analyzer_id` | ID [!DNL Sensei] de service sous lequel votre demande est déployée. Cet identifiant détermine lequel des [!DNL Sensei Content Frameworks] est utilisé. | Oui |
| `application-id` | ID de l’application créée. | Oui |
| `data` | Tableau contenant un objet JSON avec chaque objet du tableau représentant un document. Tous les paramètres transmis dans le cadre de ce tableau remplacent les paramètres globaux spécifiés en dehors du `data` tableau. Toutes les autres propriétés décrites ci-dessous dans ce tableau peuvent être remplacées de l’intérieur `data`. | Oui |
| `language` | Langue du texte de saisie. La valeur par défaut est `en`. | Non |
| `content-type` | Permet d’indiquer si l’entrée fait partie du corps de la requête ou si une URL signée est associée à un compartiment S3. La valeur par défaut de cette propriété est `inline`. | Oui |
| `encoding` | Format de codage du texte d’entrée. Cela peut être `utf-8` ou `utf-16`. La valeur par défaut de cette propriété est `utf-8`. | Non |
| `threshold` | Seuil de score (0 à 1) au-dessus duquel les résultats doivent être renvoyés. Utilisez la valeur `0` pour renvoyer tous les résultats. La valeur par défaut de cette propriété est `0`. | Non |
| `top-N` | Nombre de résultats à renvoyer (ne peut pas être un entier négatif). Utilisez la valeur `0` pour renvoyer tous les résultats. Lorsqu&#39;elle est utilisée conjointement avec `threshold`, le nombre de résultats renvoyés est le plus faible des deux limites définies. La valeur par défaut de cette propriété est `0`. | Non |
| `custom` | Tout paramètre personnalisé à transmettre. Cette propriété requiert un objet JSON valide pour fonctionner. Consultez l’ [annexe](#appendix) pour plus d’informations sur les paramètres personnalisés. | Non |
| `content-id` | ID unique de l’élément de données renvoyé dans la réponse. Si ce n’est pas le cas, un identifiant généré automatiquement est attribué. | Non |
| `content` | Contenu utilisé par le service d&#39;extraction de mots-clés. Le contenu peut être du texte brut (type de contenu &quot;intégré&quot;). <br> Si le contenu est un fichier sur S3 (type de contenu du compartiment 3), transmettez l’URL signée. Lorsque le contenu fait partie du corps de la requête, la liste des éléments de données ne doit comporter qu’un seul objet. Si plusieurs objets sont transmis, seul le premier objet est traité. | Oui |

**Réponse**

Une réponse réussie renvoie un objet JSON contenant des mots-clés extraits dans le `response` tableau.

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

## Annexe {#appendix}

Le tableau suivant contient les paramètres disponibles qui peuvent être utilisés dans `custom`.

| Nom | Description | Obligatoire |
| --- | --- | --- |
| `min-n` | Nombre minimum de mots requis dans les mots-clés. | Non |
| `entity-types` | Types d&#39;entités à renvoyer. Consultez le tableau de reconnaissance des entités nommées au début de ce document. | Non |