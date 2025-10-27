---
keywords: Experience Platform;accueil;rubriques les plus consultées;ingestion par flux;ingestion;diffusion en continu de plusieurs messages;messages multiples;
solution: Experience Platform
title: Envoyer plusieurs messages dans une seule requête HTTP
type: Tutorial
description: Ce document fournit un tutoriel permettant d’envoyer plusieurs messages vers Adobe Experience Platform dans une seule requête HTTP à l’aide de l’ingestion par flux.
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 31c00e69dd92f7c3232e09f02da36c60cd8cf486
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 58%

---

# Envoyer plusieurs messages dans une seule requête HTTP

Lorsque vous diffusez des données en continu vers Adobe Experience Platform, effectuer de nombreux appels HTTP peut vous coûter cher. Par exemple, au lieu de créer 200 requêtes HTTP contenant des payloads de 1 Ko chacun, il est plus efficace de créer une requête HTTP contenant 200 messages de 1 Ko chacun avec un payload unique de 200 Ko. Lorsque cette fonctionnalité est utilisée correctement, regrouper plusieurs messages au sein d’une requête unique est une excellente manière d’optimiser les données envoyées à [!DNL Experience Platform].

Ce document fournit un tutoriel permettant d’envoyer plusieurs messages à [!DNL Experience Platform] dans une seule requête HTTP à l’aide de l’ingestion par flux.

## Commencer

Ce tutoriel nécessite une compréhension pratique de Adobe Experience Platform [!DNL Data Ingestion]. Avant de commencer ce tutoriel, consultez la documentation suivante :

- [Présentation de Data Ingestion](../home.md) : couvre les concepts de base de la [!DNL Experience Platform Data Ingestion], notamment les méthodes d’ingestion et les connecteurs de données.
- [Présentation de l’ingestion par flux](../streaming-ingestion/overview.md) : processus et blocs de création de l’ingestion par flux, tels que les connexions par flux, les jeux de données, les [!DNL XDM Individual Profile] et les [!DNL XDM ExperienceEvent].

Pour passer à ce tutoriel, vous devez également avoir terminé le tutoriel [Authentification à Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) afin d’effectuer avec succès des appels vers les API [!DNL Experience Platform]. Terminer le tutoriel d’authentification fournit la valeur de l’en-tête d’autorisation requise par tous les appels API de ce tutoriel. L’en-tête est affiché dans les appels d’échantillon de la manière suivante :

- Authorization: Bearer `{ACCESS_TOKEN}`

Toutes les requêtes POST nécessitent un en-tête supplémentaire :

- Content-Type: application/json

## Création d’une connexion en continu

Vous devez d’abord créer une connexion en continu avant de pouvoir commencer à diffuser des données en continu vers [!DNL Experience Platform]. Lisez le guide [Création d’une connexion en continu](./create-streaming-connection.md) pour savoir comment créer une connexion en continu.

Après l’enregistrement d’une connexion en continu, vous, en tant que producteur de données, disposerez d’une URL unique qui peut être utilisée pour diffuser des données vers Experience Platform.

## Diffusion en continu vers un jeu de données

L’exemple suivant vous montre comment envoyer plusieurs messages vers un jeu de données spécifique au sein d’une requête HTTP unique. Insérez l’identifiant du jeu de données dans l’en-tête du message pour que ce message soit directement ingéré.

Vous pouvez obtenir l’identifiant d’un jeu de données existant à l’aide de l’interface utilisateur de [!DNL Experience Platform] ou d’une opération de liste dans l’API . L’ID du jeu de données se trouve sur [Experience Platform](https://platform.adobe.com) en accédant à l’onglet **[!UICONTROL Datasets]** , en cliquant sur le jeu de données dont vous souhaitez récupérer l’ID et en copiant la chaîne depuis le champ ID du jeu de données de l’onglet **[!UICONTROL Info]** . Consultez la [présentation du service de catalogue](../../catalog/home.md) pour obtenir des informations sur la manière dont vous pouvez récupérer les jeux de données à l’aide de l’API.

Au lieu d’utiliser un jeu de données existant, vous pouvez créer un nouveau jeu de données. Pour plus d’informations sur la création d’un jeu de données à l’aide d’API, lisez le tutoriel [Création d’un jeu de données à l’aide d’API](../../catalog/api/create-dataset.md).

**Format d’API**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{CONNECTION_ID}` | L’identifiant de la connexion en continu créée. |

**Requête**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Fernie Snow",
              "quantity": 30,
              "priceTotal": 7.8
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "gregdorcey@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "7af6adcc-dc9e-4692-b826-55d2abe68c11",
          "timestamp": "2019-02-23T22:07:31Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "emilyong@example.com"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 207 (état multiple). En examinant le corps de la réponse, vous pouvez récupérer davantage d’informations sur la réussite ou l’échec de chaque méthode exécutée dans la requête. Une réponse est renvoyée pour chaque élément du tableau de messages de requête. Vous trouverez ci-dessous un exemple de réponse réussie sans échecs de message :

```json
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565628583792:1485:153",
    "receivedTimeMs": 1565628583854,
    "responses": [
        {
            "xactionId": "1565628583792:1485:153:0"
        },
        {
            "xactionId": "1565628583792:1485:153:1"
        }
    ]
}
```

Pour plus d’informations sur les codes d’état, consultez le tableau [Codes de réponse](#response-codes) dans l’annexe de ce tutoriel.

## Identification des messages en échec

Par rapport à l’envoi d’une requête avec un message unique, il y a plusieurs facteurs supplémentaires à prendre en compte lorsque vous envoyez une requête HTTP contenant plusieurs messages, notamment : la manière dont identifier le moment où l’envoi des données a échoué, les messages spécifiques n’ayant pas été envoyés et la manière dont vous pouvez les récupérer, et ce qu’il advient des données qui réussissent alors que d’autres messages de la même requête échouent.

Avant de poursuivre ce tutoriel, nous vous recommandons de consulter dans un premier temps le guide [Récupération des lots rejetés](../quality/retrieve-failed-batches.md).

### Envoi du payload de la requête avec des messages valides et invalides

L’exemple suivant montre ce qui se produit lorsque le lot contient des messages valides et invalides.

Le payload de la requête est un tableau d’objets JSON représentant l’événement dans le schéma XDM. Notez que vous devez remplir les conditions suivantes pour valider le message avec succès :
- Le champ `imsOrgId` de l’en-tête du message doit correspondre à la définition de l’inlet. Si la payload de la requête n’inclut pas de champ `imsOrgId`, le [!DNL Data Collection Core Service] (DCCS) ajoute automatiquement le champ.
- L’en-tête du message doit référencer un schéma XDM existant créé dans l’interface utilisateur de [!DNL Experience Platform].
- Le champ `datasetId` doit référencer un jeu de données existant dans [!DNL Experience Platform] et son schéma doit correspondre au schéma fourni dans l’objet `header` dans chaque message inclus dans le corps de la requête.

**Format d’API**

```http
POST /collection/batch/{CONNECTION_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{CONNECTION_ID}` | L’identifiant de l’inlet de données créé. |

**Requête**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "rogerkanagawa@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "invalidIMSOrg@AdobeOrg",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "mohandeewar@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
   {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          }
        }
      }
    },
    {
      "header": {
        "msgType": "xdmEntityCreate",
        "msgId": "79d2e715-f25f-4c36",
        "xdmSchema": {
          "name": "_xdm.context.experienceevent"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "xdmSchema": {
            "name": "_xdm.context.experienceevent"
          }
        },
        "xdmEntity": {
          "_id": "abc",
          "dataSource": {
            "_id": "http://abc.com/abc"
          },
          "timestamp": "2018-05-18T15:28:25Z",
          "endUserIDs": {
            "_vendor": {
              "adobe": {
                "experience": {
                  "mcId": {
                    "id": "http://abc.com/abc"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**Réponse**

Le payload de réponse inclut un état pour chaque message avec un GUID dans le `xactionId` pouvant être utilisé pour le traçage.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        }
    ]
}
```

L’exemple de réponse ci-dessus affiche les messages d’erreur de la requête précédente. En comparant cette réponse à la réponse valide précédente, vous pouvez observer que la requête a entraîné une réussite partielle, un message ayant été ingéré avec succès et trois messages ayant entraîné un échec. Notez que les deux types de réponses renvoient un code d’état « 207 ». Pour plus d’informations sur les codes d’état, consultez le tableau [Codes de réponse](#response-codes) dans l’annexe de ce tutoriel.

Le premier message a été envoyé avec succès à [!DNL Experience Platform] et n’est pas affecté par les résultats des autres messages. Par conséquent, lorsque vous tentez d’envoyer à nouveau les messages échoués, vous n’avez pas besoin d’inclure à nouveau ce message.

Le deuxième message a échoué parce qu’il manquait un corps de message. Pour que la requête de collecte soit valide, des éléments de message possédant un en-tête et des sections corps valides sont nécessaires. L’ajout du code suivant après l’en-tête du deuxième message réparera la requête, permettant au deuxième message de passer la validation :

```JSON
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version={SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
        }
    },
```

Le troisième message a échoué en raison d’un ID d’organisation non valide utilisé dans l’en-tête . L’organisation doit correspondre au {CONNECTION_ID} vers lequel vous essayez de publier. Pour déterminer l’ID d’organisation correspondant à la connexion en continu que vous utilisez, vous pouvez effectuer une requête `GET inlet` à l’aide de l’[[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) . Consultez la section [Récupération d’une connexion en continu](./create-streaming-connection.md#get-data-collection-url) pour obtenir un exemple de la manière dont vous pouvez récupérer les connexions en continu créées précédemment.

Le quatrième message a échoué, car il ne suivait pas le schéma XDM attendu. Les éléments `xdmSchema` inclus dans l’en-tête et dans le corps de la requête ne correspondent pas au schéma XDM de `{DATASET_ID}`. La correction du schéma dans l’en-tête et le corps du message lui permet de réussir la validation DCCS et d’être envoyé avec succès à [!DNL Experience Platform]. Le corps du message doit également être mis à jour pour correspondre au schéma XDM du `{DATASET_ID}` afin qu’il transmette la validation de diffusion en continu sur [!DNL Experience Platform]. Pour plus d’informations sur le sort des messages qui diffusent avec succès vers Experience Platform, consultez la section [confirmer les messages ingérés](#confirm-messages-ingested) de ce tutoriel.

### Récupérer les messages ayant échoué depuis [!DNL Experience Platform]

Les messages en échec sont identifiés par un code d’état d’erreur dans le tableau de réponse.
Les messages invalides sont collectés et stockés dans un lot « erreur » au sein du jeu de données spécifié par `{DATASET_ID}`.

Pour plus d’informations sur la récupération des messages par lots en échec, lisez le guide [Récupération des messages en échec](../quality/retrieve-failed-batches.md).

## Confirmation des messages ingérés

Les messages qui réussissent la validation DCCS sont diffusés en continu vers [!DNL Experience Platform]. Sur [!DNL Experience Platform], les messages par lot sont testés par validation de diffusion en continu avant d’être ingérés dans le [!DNL Data Lake]. L’état des lots, qu’ils soient réussis ou non apparaissent au sein du jeu de données spécifié par `{DATASET_ID}`.

Vous pouvez afficher l’état de messages par lots qui diffusent avec succès vers [!DNL Experience Platform] à l’aide de l’[interface utilisateur d’Experience Platform](https://platform.adobe.com) en vous rendant dans l’onglet **[!UICONTROL Datasets]** , en cliquant sur le jeu de données sur lequel vous diffusez, et en vérifiant l’onglet **[!UICONTROL Dataset Activity]** .

Les messages par lots qui réussissent la validation de diffusion en continu sur [!DNL Experience Platform] sont ingérés dans le [!DNL Data Lake]. Les messages sont ensuite disponibles à des fins d’analyse ou d’exportation.

## Étapes suivantes

Maintenant que vous savez comment envoyer plusieurs messages dans une seule requête et vérifier quand les messages sont correctement ingérés dans le jeu de données cible, vous pouvez commencer à diffuser vos propres données vers [!DNL Experience Platform]. Pour obtenir un aperçu sur la requête et la récupération de données ingérées à partir de [!DNL Experience Platform], consultez le guide [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md).

## Annexe

Cette section contient des informations supplémentaires pour le tutoriel.

### Codes de réponse

Le tableau suivant affiche les codes d’état renvoyés par les messages de réponse en réussite et en échec.

| Code d’état | Description |
| :---: | --- |
| 207 | Bien que « 207 » soit utilisé comme code d’état de réponse global, le destinataire doit consulter le contenu du corps de réponse à plusieurs états pour plus d’informations sur le succès ou l’échec de l’exécution de la méthode. Le code de réponse est utilisé en cas de réussite, de réussite partielle, mais aussi dans les situations d’échec. |
| 400 | Un problème s’est produit avec la requête. Consultez le corps de la réponse pour obtenir un message plus spécifique à l’erreur (par exemple, des champs obligatoires manquaient dans le payload du message ou le message était à un format xdm inconnu). |
| 401 | Non autorisé : un en-tête d’autorisation valide manque dans la requête. Ce message n’est renvoyé que pour les inlets dont l’authentification est activée. |
| 403 | Non autorisé : le jeton d’autorisation fourni est non valide ou a expiré. Ce message n’est renvoyé que pour les inlets dont l’authentification est activée. |
| 413 | Payload trop grand : apparaît lorsque la requête de payload totale est supérieure à 1 Mo. |
| 429 | Trop de requêtes au cours d’une période précise. |
| 500 | Erreur lors du traitement du payload. Voir le corps de la réponse pour un message d’erreur plus spécifique (par exemple, le schéma Payload du message n’est pas spécifié ou ne correspond pas à la définition XDM dans [!DNL Experience Platform]). |
| 503 | Le service n’est pas disponible pour le moment. Nous conseillons aux clients de réessayer au moins 3 fois en utilisant une stratégie de backoff exponentiel. |
