---
keywords: Experience Platform;prise en main;contenu;ia dédiée au balisage de contenu;balisage des mots-clés;balisage des mots-clés
solution: Experience Platform
title: Balisage de mots-clés dans l’API de balisage de contenu
description: Lorsqu’il reçoit un document texte, le service Balisage des mots-clés extrait automatiquement les mots-clés ou les expressions-clés qui décrivent le mieux l’objet du document. Pour extraire des mots-clés, on utilise une combinaison d'algorithmes de reconnaissance d'entités nommées (NER) et de balisage de mots-clés non supervisé.
exl-id: 56a2da96-5056-4702-9110-a1dfec56f0dc
TQID: https://experienceleague.adobe.com/iOmCfCfAhDGqiiRHDs9qjI6fD41yfDl9SBaf6a-JdSM
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 448
ht-degree: 6%

---

# Balisage des mots-clés

Lorsqu’il reçoit un document texte, le service de balisage des mots-clés extrait automatiquement les mots-clés ou les expressions clés qui décrivent le mieux l’objet du document. Pour extraire des mots-clés, on utilise une combinaison d&#39;algorithmes de reconnaissance d&#39;entités nommées (NER) et de balisage de mots-clés non supervisé.

Le tableau suivant répertorie les entités nommées que [!DNL Content Tagging] pouvez identifier :

| Nom de l’entité | Description |
| --- | --- |
| PERSONNE | Des gens, y compris des fictifs. |
| GPE | Pays, villes et états. |
| LOC | Emplacements non conformes au GPE, chaînes de montagnes et masses d&#39;eau. |
| AAAA | Bâtiments, aéroports, autoroutes, ponts, etc. |
| ORG | Entreprises, agences, institutions, etc. |
| PRODUIT | Objets, véhicules, aliments, etc. (Pas les services.) |
| ÉVÉNEMENT | Ouragans nommés, batailles, guerres, événements sportifs, etc. |
| WORK_OF_ART | Titres de livres, de chansons, etc. |
| DROIT | Documents nommés transformés en lois. |
| LANGUE | Toute langue nommée. |

**Format d’API**

```http
POST /services/v2/predict
```

**Requête**

La requête suivante extrait des mots-clés d’un document en fonction des paramètres d’entrée fournis dans la payload.

Pour plus d’informations sur les paramètres d’entrée affichés, consultez le tableau ci-dessous l’exemple de payload.

Ce fichier [exemple pdf](../pdf-files/simple-text.pdf) a été utilisé dans l’exemple illustré dans ce document.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "test",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-ner:Service-1e9081c865214d1e8bace51dd918b5c0"
      },
      "sensei:inputs": {
        "documents": [
          {
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "application/pdf"
          }
        ]
      },
      "sensei:params": {
        "application-id": "1234",
        "min_key_phrase_length": 1,
        "max_key_phrase_length": 3,
        "top_n": 5,
        "last_semantic_unit_type": "concept"
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}' \
-F 'infile_1=@simple-text.pdf'
```

**Paramètres d’entrée**

| Propriété | Description | Obligatoire |
| --- | --- | --- |
| `top_n` | Nombre de résultats à retourner. 0, pour renvoyer tous les résultats. Utilisé conjointement avec le seuil, le nombre de résultats renvoyés sera inférieur à l’une des limites. | Non |
| `min_relevance` | Seuil de score en dessous duquel les résultats doivent être renvoyés. Excluez le paramètre pour renvoyer tous les résultats. | Non |
| `min_key_phrase_length` | Nombre minimum de mots requis dans les expressions clés. | Non |
| `max_key_phrase_length` | Nombre maximal de mots requis dans les expressions clés. | Non |
| `last_semantic_unit_type` | Renvoie uniquement les unités sémantiques jusqu’au niveau donné dans la réponse hiérarchique. « key_phrase » renvoie uniquement les phrases clés, « linked_entity » renvoie uniquement les phrases clés et leurs entités liées correspondantes, et « concept » renvoie les phrases clés, les entités liées et les concepts. | Non |
| `entity_types` | Types d’entités à renvoyer sous forme d’expressions clés. | Non |

**Objet document**

| Nom | Type de données | Obligatoire | Par défaut | Valeurs | Description |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | chaîne | - | - | - | URL prédéfinie du document à partir duquel les expressions clés doivent être extraites. |
| `sensei:repoType` | chaîne | - | - | HTTPS | Type de référentiel dans lequel le document est stocké. |
| `sensei:multipart_field_name` | chaîne | - | - | - | Utilisez ceci lors de la transmission du document en tant qu’argument multipartie au lieu d’utiliser des URL présignées. |
| `dc:format` | chaîne | Oui | - | « text/plain »,<br>« application/pdf »,<br>« text/pdf »,<br>« text/html »,<br>« text/rtf »,<br>« application/rtf »,<br>« application/msword »,<br>« application/vnd.openxmlformats-officedocument.wordprocessingml.document »,<br>« application/mspowerpoint »,<br>« application/vnd.ms-powerpoint »,<br>« application/vnd.openxmlformats-officedocument.presentationml.presentation » | Le codage du document est vérifié par rapport aux types de codage d’entrée autorisés avant d’être traité. |

**Réponse**

Une réponse réussie renvoie un objet JSON contenant les mots-clés extraits dans le tableau `response`.

```json
{
  [
  {
    "key_phrases": [
      {
        "name": "Canada",
        "type": "GPE",
        "relevance": 0.9525035277863068,
        "confidence": 1.0,
        "linked_entity": {
          "name": "Canada",
          "id": "b27a82e6-e963-45de-add8-dc4f3f0dd399",
          "confidence": 1.0,
          "relevance": 0.9706433035237365,
          "concepts": [
            {
              "name": "Commonwealth realm",
              "relationship": "instance_of",
              "id": "f5354ab6-ad25-406a-b289-9209db0db8ea",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "sovereign state",
              "relationship": "instance_of",
              "id": "10c24191-beef-43cc-a823-c170f217fe12",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "dominion of the British Empire",
              "relationship": "instance_of",
              "id": "4ffabaee-e6ab-422d-b121-145dcdbcf427",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "country",
              "relationship": "instance_of",
              "id": "6e8f43cb-7e64-41fc-93b4-119adfe87926",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            },
            {
              "name": "North America",
              "relationship": "part_of",
              "id": "0f4b1f78-9681-414a-91c6-576ed643941a",
              "confidence": 1.0,
              "relevance": 0.9525035277863066
            }
          ]
        }
      },
      {
        "name": "Sherlock Homles",
        "type": "ENTITY_UNKNOWN_TYPE",
        "relevance": 0.9516463011782174,
        "confidence": 1.0,
        "linked_entity": null
      },
      {
        "name": "Albert Einstein",
        "type": "PERSON",
        "relevance": 0.95080732382989,
        "confidence": 1.0,
        "linked_entity": {
          "name": "Albert Einstein",
          "id": "0fdb37f6-f575-4b4d-91e9-fbff57eae0ab",
          "confidence": 1.0,
          "relevance": 0.9695742180192723,
          "concepts": [
            {
              "name": "pedagogue",
              "relationship": "occupation",
              "id": "1439eb14-2988-43cc-865d-ad5a60d3ea62",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "philosopher of science",
              "relationship": "occupation",
              "id": "eefb9bbf-e617-4434-abb2-56b5853abd3a",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "university teacher",
              "relationship": "occupation",
              "id": "bb2c4745-4116-46ef-a122-c28c2f902026",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "science writer",
              "relationship": "occupation",
              "id": "5084431d-9073-45cb-be82-4a6898becd5b",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "non-fiction writer",
              "relationship": "occupation",
              "id": "57cc1f7b-5391-458b-9303-ec35b3ba01a4",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "patent examiner",
              "relationship": "occupation",
              "id": "d3f10fc5-ca81-4049-8c48-3d935552d9e7",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "philosopher",
              "relationship": "occupation",
              "id": "04d3cd32-68ad-4b71-9231-bdf3acfb09b2",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "scientist",
              "relationship": "occupation",
              "id": "dc8c068b-aa75-4ece-acd7-06fa304964fb",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "physicist",
              "relationship": "occupation",
              "id": "56ac942c-12a2-42c1-b10c-d1394a7971af",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "teacher",
              "relationship": "occupation",
              "id": "c70301bd-bcf4-47ab-b958-b983f0b0a6bd",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "human",
              "relationship": "instance_of",
              "id": "ead8a1d7-f901-44e6-b80f-63ebbbca4ffe",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "professor",
              "relationship": "occupation",
              "id": "c6d691f2-1e26-49fd-8481-58cb2d64d3e9",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "mathematician",
              "relationship": "occupation",
              "id": "23bf46db-a69a-4546-b18a-690a41144caa",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "theoretical physics",
              "relationship": "field_of_work",
              "id": "d6c03027-4efd-49d6-a7e5-ac4994c9143e",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "theoretical physicist",
              "relationship": "occupation",
              "id": "eedb6531-c2bf-4d05-af92-6f21751bc894",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "inventor",
              "relationship": "occupation",
              "id": "7baf322e-5913-4e2a-997a-90a039b0ff5c",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            },
            {
              "name": "writer",
              "relationship": "occupation",
              "id": "4c4c287c-0d83-4da3-b8c7-26df5adc9b33",
              "confidence": 1.0,
              "relevance": 0.9508073238298899
            }
          ]
        }
      },
      {
        "name": "Toronto",
        "type": "GPE",
        "relevance": 0.9370046727951885,
        "confidence": 1.0,
        "linked_entity": {
          "name": "Toronto",
          "id": "762db630-b272-4828-b1af-e7c65334e1d3",
          "confidence": 1.0,
          "relevance": 0.9608202651283239,
          "concepts": [
            {
              "name": "provincial or territorial capital city in Canada",
              "relationship": "instance_of",
              "id": "d7447629-e940-43b1-a726-4ac3f675410c",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "city",
              "relationship": "instance_of",
              "id": "d9d95c34-a2ce-4098-bd9d-3616b85620a8",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "big city",
              "relationship": "instance_of",
              "id": "68275742-3451-40af-8f5a-84211953a438",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "single-tier municipality",
              "relationship": "instance_of",
              "id": "a0f67ef3-52bb-44d9-bc52-9059d37c6d0c",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            },
            {
              "name": "city with millions of inhabitants",
              "relationship": "instance_of",
              "id": "b08def76-4b71-4545-9efb-f4858aaf253d",
              "confidence": 1.0,
              "relevance": 0.9370046727951883
            }
          ]
        }
      },
      {
        "name": "vacation",
        "type": "KEY_PHRASE",
        "relevance": 0.933964522339908,
        "confidence": 1.0,
        "linked_entity": null
      }
    ],
    "detected_languages": [
      {
        "language": "en",
        "confidence": 0.9999951616458576
      }
    ],
    "word_count": 183
  }
]   
}
```
