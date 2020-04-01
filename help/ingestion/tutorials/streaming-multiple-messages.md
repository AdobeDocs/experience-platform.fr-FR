---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Diffusion en flux continu de plusieurs messages dans une seule requête HTTP
topic: tutorial
translation-type: tm+mt
source-git-commit: 79466c78fd78c0f99f198b11a9117c946736f47a

---


# Envoi de plusieurs messages dans une seule requête HTTP

Lors de la diffusion en flux continu de données vers Adobe Experience Platform, il peut s’avérer coûteux d’effectuer de nombreux appels HTTP. Par exemple, au lieu de créer 200 requêtes HTTP avec des charges de 1 Ko, il est beaucoup plus efficace de créer 1 requête HTTP avec 200 messages de 1 Ko chacun, avec une charge utile unique de 200 Ko. Lorsqu’il est utilisé correctement, le regroupement de plusieurs messages au sein d’une même requête constitue un excellent moyen d’optimiser les données envoyées à la plateforme d’expérience.

Ce fournit un didacticiel pour l’envoi de plusieurs messages vers la plateforme Experience Platform au sein d’une seule requête HTTP à l’aide de l’assimilation en flux continu.

## Prise en main

Ce didacticiel nécessite une compréhension pratique de l’administration des données d’Adobe Experience Platform. Avant de commencer ce didacticiel, consultez la documentation suivante :

- [Présentation](../home.md)de l&#39;assimilation des données : Couvre les concepts de base de la gestion des données de plateforme d’expérience, y compris les méthodes d’assimilation et les connecteurs de données.
- [Présentation](../streaming-ingestion/overview.md)de l&#39;assimilation en flux continu : Flux de travaux et blocs de création de l’assimilation en flux continu, tels que les connexions en flux continu, les jeux de données, les  individuels XDM et XDM ExperienceEvent.

Ce didacticiel nécessite également que vous ayez suivi le didacticiel [Authentication to Adobe Experience Platform](../../tutorials/authentication.md) afin d’effectuer des appels aux API de plateforme. Le didacticiel sur l’authentification fournit la valeur de l’en-tête d’autorisation requis par tous les appels d’API dans ce didacticiel. L’en-tête s’affiche dans les exemples d’appels comme suit :

- Autorisation : Porteur `{ACCESS_TOKEN}`

Toutes les requêtes POST nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Création d’une connexion de flux continu

Vous devez d’abord créer une connexion de flux continu avant de pouvoir des données de flux continu à la plateforme d’expérience. Lisez le guide [Création d’une connexion](./create-streaming-connection.md) en flux continu pour savoir comment créer une connexion en flux continu.

Après avoir enregistré une connexion de flux continu, vous, en tant que producteur de données, disposez d’une URL unique qui peut être utilisée pour diffuser des données vers la plateforme.

## Flux vers un jeu de données

L’exemple suivant montre comment envoyer plusieurs messages à un jeu de données spécifique au sein d’une requête HTTP unique. Insérez l’ID du jeu de données dans l’en-tête du message pour que ce message soit directement assimilé.

Vous pouvez obtenir l’ID d’un jeu de données existant à l’aide de l’interface utilisateur de la plate-forme ou à l’aide d’une opération de liste dans l’API. L’ID du jeu de données se trouve sur la plate-forme [](https://platform.adobe.com) d’expérience en accédant à l’onglet **Jeu de données** , en cliquant sur le jeu de données pour lequel vous souhaitez obtenir l’ID, puis en copiant la chaîne à partir du champ ID **du jeu de** données dans l’onglet **Info.** Consultez la présentation [du service de](../../catalog/home.md) catalogue pour savoir comment récupérer des jeux de données à l’aide de l’API.

Au lieu d’utiliser un jeu de données existant, vous pouvez créer un jeu de données. Pour plus d&#39;informations sur la création d&#39;un jeu de données à l&#39;aide d&#39;API [, consultez le didacticiel](../../catalog/api/create-dataset.md) Création d&#39;un jeu de données à l&#39;aide d&#39;API.

**Format API**

```http
POST /collection/{CONNECTION_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID de la connexion de flux continu créée. |

**Requête**

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
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
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
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

Une réponse réussie renvoie un état HTTP 207 (multi-état). L’examen du corps de la réponse fournit plus de détails sur la réussite ou l’échec de chaque méthode exécutée dans la requête. Une réponse est renvoyée pour chaque élément du tableau des messages de requête. Voici un exemple de réponse réussie sans échec de message :

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

Pour plus d&#39;informations sur les codes d&#39;état, consultez le tableau des codes [de](#response-codes) réponse dans l&#39;annexe de ce didacticiel.

## Identifier les messages ayant échoué

Par rapport à l’envoi d’une requête avec un seul message, lors de l’envoi d’une requête HTTP avec plusieurs messages, d’autres facteurs peuvent être pris en compte, tels que : comment identifier le moment où les données n’ont pas été envoyées, quels messages spécifiques n’ont pas été envoyés et comment ils peuvent être récupérés, et ce qui arrive aux données qui réussissent lorsque d’autres messages de la même requête échouent.

Avant de poursuivre avec ce didacticiel, il est recommandé de consulter d’abord le guide de [récupération des lots](../quality/retrieve-failed-batches.md) ayant échoué.

### Envoyer la charge utile de requête avec des messages valides et non valides

L’exemple suivant montre ce qui se produit lorsque le lot inclut des messages valides et non valides.

La charge utile de la requête est un tableau d’objets JSON représentant le  dans le XDM . Notez que les conditions suivantes doivent être remplies pour une validation réussie du message :
- Le `imsOrgId` champ de l’en-tête du message doit correspondre à la définition d’entrée. Si la charge utile de la demande n’inclut pas de `imsOrgId` champ, le service principal de collecte de données (DCCS) ajoute le champ automatiquement.
- L’en-tête du message doit faire référence à un XDM existant créé dans l’interface utilisateur de la plateforme.
- Le `datasetId` champ doit faire référence à un jeu de données existant dans Platform et son  de doit correspondre au  fourni dans l’ `header` objet dans chaque message inclus dans le corps de la requête.

**Format API**

```http
POST /collection/{CONNECTION_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{CONNECTION_ID}` | ID de l’entrée de données créée. |

**Requête**

```shell
curl -X POST https://dcs.adobedc.net/collection/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
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
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "invalidIMSOrg@AdobeOrg",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
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
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
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
        "imsOrgId": "{IMS_ORG}",
        "source": {
          "name": "GettingStarted"
        },
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

La charge utile de réponse inclut un état pour chaque message, ainsi qu’un GUID dans le `xactionId` qui peut être utilisé pour le suivi.

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
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        }
    ]
}
```

L’exemple de réponse ci-dessus affiche des messages d’erreur pour la requête précédente. En comparant cette réponse à la réponse valide précédente, vous pouvez constater que la requête a abouti à un succès partiel, avec un message correctement ingéré et trois messages qui ont abouti à un échec. Notez que les deux réponses renvoient un code d’état &quot;207&quot;. Pour plus d&#39;informations sur les codes d&#39;état, consultez le tableau des codes [de](#response-codes) réponse dans l&#39;annexe de ce didacticiel.

Le premier message a bien été envoyé à Platform et n’est pas affecté par les résultats des autres messages. Par conséquent, lorsque vous tentez de renvoyer les messages ayant échoué, vous n’avez pas besoin de réinclure ce message.

Le second message a échoué car il manquait un corps de message. La demande de collection attend des éléments de message qu’ils possèdent des sections d’en-tête et de contenu valides. L’ajout du code suivant après l’en-tête du second message corrigera la requête, permettant au second message de transmettre la validation :

```JSON
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
        }
    },
```

Le troisième message a échoué en raison d’un ID d’organisation IMS non valide utilisé dans l’en-tête. L’organisation IMS doit correspondre à {CONNECTION_ID} à laquelle vous tentez de publier du contenu. Pour déterminer l’ID d’organisation IMS correspondant à la connexion de flux continu que vous utilisez, vous pouvez effectuer une `GET inlet` requête à l’aide de l’API [d’administration des](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)données. Voir [récupération d’une connexion](./create-streaming-connection.md#get-data-collection-url) de flux continu pour obtenir un exemple de récupération des connexions de flux continu précédemment créées.

Le quatrième message a échoué car il ne suivait pas le  XDM attendu. Les `xdmSchema` éléments inclus dans l’en-tête et le corps de la requête ne correspondent pas au XDM du `{DATASET_ID}`. La correction du  dans l’en-tête et le corps du message lui permet de transmettre la validation DCCS et d’être envoyé avec succès à la plateforme. Le corps du message doit également être mis à jour pour correspondre au  XDM du `{DATASET_ID}` pour qu’il transfère la validation en flux continu sur la plateforme. Pour plus d&#39;informations sur ce qui arrive aux messages qui arrivent en continu sur Plateforme, consultez la section [Confirmer les messages assimilés](#confirm-messages-ingested) de ce didacticiel.

### Récupérer les messages ayant échoué à partir de la plateforme

Les messages d’échec sont identifiés par un code d’état d’erreur dans le tableau de réponses.
Les messages non valides sont collectés et stockés dans un lot &quot;erreur&quot; dans le jeu de données spécifié par `{DATASET_ID}`.

Pour plus d&#39;informations sur la récupération des messages de lot ayant échoué, consultez le guide [de récupération des lots](../quality/retrieve-failed-batches.md) ayant échoué.

## Confirmer les messages assimilés

Les messages qui réussissent la validation DCCS sont diffusés en continu sur la plateforme. Sur Plate-forme, les messages par lot sont testés par validation en flux continu avant d’être assimilés dans le lac de données. L’état des lots, qu’ils soient réussis ou non, s’affiche dans le jeu de données spécifié par `{DATASET_ID}`.

Vous pouvez l’état des messages par lot qui sont diffusés en continu sur la plateforme à l’aide de l’interface utilisateur [de la plateforme](https://platform.adobe.com) d’expérience en accédant à l’onglet **Jeu de données** , en cliquant sur le jeu de données auquel vous effectuez la diffusion en continu et en vérifiant l’onglet **Jeu de** données  l’onglet .

Les messages par lots qui passent la validation en flux continu sur la plateforme sont assimilés dans le lac de données. Les messages sont alors disponibles pour   ou exportation.

## Étapes suivantes

Maintenant que vous savez comment envoyer plusieurs messages dans une seule requête et vérifier quand les messages sont correctement assimilés dans le jeu de données , vous pouvez  la diffusion de vos propres données sur la plateforme. Pour une présentation sur la manière de  et de récupérer les données assimilées à partir de la plateforme, reportez-vous au guide [Data Access](../../data-access/tutorials/dataset-data.md) (accès auxdonnées).

## Annexe

Cette section contient des informations supplémentaires pour le didacticiel.

### Codes de réponse :

Le tableau suivant présente les codes d’état renvoyés par les messages de réponse réussis et ayant échoué.

| Code d’état | Description |
| :---: | --- |
| 207 | Bien que &#39;207&#39; soit utilisé comme code d&#39;état global de la réponse, le doit consulter le contenu de l&#39;organisme de réponse à plusieurs états pour obtenir des informations supplémentaires sur la réussite ou l&#39;échec de l&#39;exécution de la méthode. Le code de réponse est utilisé en cas de succès, de succès partiel et aussi en cas d’échec. |
| 400 | Il y a eu un problème avec la demande. Voir le corps de la réponse pour obtenir un message d’erreur plus spécifique (par exemple, les champs obligatoires de la charge utile du message étaient absents ou le format xdm du message était inconnu). |
| 401 | Non autorisé : en-tête d&#39;autorisation valide manquante pour la requête. Ceci est renvoyé uniquement pour les entrées pour lesquelles l’authentification est activée. |
| 403 | Non autorisé :  Le jeton d’autorisation fourni n’est pas valide ou a expiré. Ceci est renvoyé uniquement pour les entrées pour lesquelles l’authentification est activée. |
| 413 | Charge utile trop importante - générée lorsque la demande de charge totale est supérieure à 1 Mo. |
| 429 | Trop de requêtes dans une durée spécifiée. |
| 500 | Erreur lors du traitement de la charge utile. Voir le corps de la réponse pour obtenir un message d’erreur plus spécifique (par exemple, le de charge utile de message n’a pas été spécifié, ou ne correspondait pas à la définition XDM dans Platform). |
| 503 | Le service n’est actuellement pas disponible. Les clients doivent réessayer au moins 3 fois en utilisant une stratégie de sauvegarde exponentielle. |