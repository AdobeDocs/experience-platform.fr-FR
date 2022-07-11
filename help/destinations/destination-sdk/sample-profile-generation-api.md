---
description: Cette page répertorie et décrit toutes les opérations d’API que vous pouvez effectuer à l’aide du point de terminaison API `/authoring/sample-profiles`, afin de générer des exemples de profils à utiliser dans les tests de destination.
title: Opérations de l’API pour la génération d’un profil type
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 789a3928379d200af292c722806f7ca72441d9f3
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 15%

---

# Opérations de l’API pour la génération d’un profil type {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

Cette page répertorie et décrit toutes les opérations de l’API que vous pouvez effectuer à l’aide du point d’entrée de l’API `/authoring/sample-profiles`.

## Génération de différents types de profils pour différentes API {#different-profiles-different-apis}

>[!IMPORTANT]
>
>Utilisez ce point de terminaison API pour générer des exemples de profils pour deux cas d’utilisation distincts. Vous pouvez effectuer l’une des actions suivantes :
>* générer des profils à utiliser lors de [conception et test d&#39;un modèle de transformation des messages](./create-template.md) - en utilisant *ID de destination* comme paramètre de requête.
>* générer des profils à utiliser lors d’appels à [tester si votre destination est correctement configurée ;](./test-destination.md) - en utilisant *ID d’instance de destination* comme paramètre de requête.


Vous pouvez générer des exemples de profils en fonction du schéma source XDM Adobe (à utiliser lors du test de votre destination) ou du schéma cible pris en charge par votre destination (à utiliser lors de la conception de votre modèle). Pour comprendre la différence entre le schéma source XDM d’Adobe et le schéma cible, consultez la section de présentation de la section [Format du message](./message-format.md) article.

Notez que les finalités pour lesquelles les exemples de profils peuvent être utilisés ne sont pas interchangeables. Profils générés à partir de *ID de destination* ne peut être utilisé que pour concevoir vos modèles et profils de transformation de messages générés en fonction des *ID d’instance de destination* ne peut être utilisé que pour tester votre point de terminaison de destination.

## Prise en main d’exemples d’opérations de l’API de génération de profil {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes requis.

## Générer des exemples de profils en fonction du schéma source à utiliser lors du test de votre destination {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>Ajoutez les exemples de profils générés ici aux appels HTTP lorsque [test de votre destination](./test-destination.md).

Vous pouvez générer des exemples de profils en fonction du schéma source en adressant une requête de GET à la variable `authoring/sample-profiles/` point d’entrée et fournissant l’identifiant d’une instance de destination que vous avez créée en fonction de la configuration de destination que vous souhaitez tester.

Pour obtenir l’identifiant d’une instance de destination, vous devez d’abord créer une connexion dans l’interface utilisateur de l’Experience Platform à votre destination avant de tenter de tester votre destination. Lisez le [Tutoriel sur l’activation de la destination](/help/destinations/ui/activation-overview.md) et consultez l’astuce ci-dessous pour savoir comment obtenir l’ID d’instance de destination à utiliser pour cette API.

>[!TIP]
>
>* Obtenez l’ID d’instance de destination que vous devez utiliser ici à partir de l’URL lorsque vous parcourez une connexion avec votre destination.
   >![Image de l’interface utilisateur comment obtenir l’ID d’instance de destination](./assets/get-destination-instance-id.png)


**Format d’API**


```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Paramètre de requête | Description |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | L’identifiant de l’instance de destination sur laquelle vous générez des exemples de profils. |
| `{COUNT}` | *Facultatif*. Le nombre d’exemples de profils que vous générez. Le paramètre peut prendre des valeurs entre les variables `1 - 1000`. <br> Si le paramètre count n’est pas spécifié, le nombre de profils générés par défaut est déterminé par la variable `maxUsersPerRequest` dans la variable [configuration du serveur de destination](./destination-server-api.md#create). Si cette propriété n’est pas définie, Adobe génère un exemple de profil. |

{style=&quot;table-layout:auto&quot;}


**Requête**

La requête suivante génère des exemples de profils, configurés par la variable `{DESTINATION_INSTANCE_ID}` et `{COUNT}` paramètres de requête.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec le nombre spécifié de profils d’exemple, avec l’appartenance au segment, les identités et les attributs de profil qui correspondent au schéma XDM source.

>[!TIP]
>
> La réponse renvoie uniquement les attributs d’appartenance, d’identité et de profil utilisés dans l’instance de destination. Même si votre schéma source comporte d’autres champs, ceux-ci sont ignorés.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-7VEsJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Y55JJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Nd9GK"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    }
]
```

| Propriété | Description |
| -------- | ----------- |
| `segmentMembership` | Objet map qui décrit les appartenances aux segments de l’individu. Pour plus d’informations sur `segmentMembership`, lire [Détails de l’adhésion au segment](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | Horodatage de la dernière fois que ce profil s’est qualifié pour le segment. |
| `xdm:status` | Un champ de chaîne qui indique si l’appartenance au segment a été réalisée dans le cadre de la requête actuelle. Les valeurs suivantes sont acceptées : <ul><li>`existing`: Le profil faisait déjà partie du segment avant la demande et continue de conserver son adhésion.</li><li>`realized`: Le profil entre dans le segment dans le cadre de la requête actuelle.</li><li>`exited`: Le profil quitte le segment dans le cadre de la requête actuelle.</li></ul> |
| `identityMap` | Champ de type map qui décrit les différentes valeurs d’identité d’un individu, ainsi que les espaces de noms qui lui sont associés. Pour plus d’informations sur `identityMap`, lire [Base de la composition des schémas](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |

{style=&quot;table-layout:auto&quot;}

## Générer des exemples de profils en fonction du schéma cible à utiliser lors de la conception d&#39;un modèle de transformation des messages {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>Utilisez les exemples de profils générés ici lors de la conception de votre modèle, dans la variable [étape du modèle de rendu](./render-template-api.md#multiple-profiles-with-body).

Vous pouvez générer des exemples de profils en fonction du schéma cible en adressant une requête GET à la variable `authoring/sample-profiles/` point de terminaison et fournissant l’identifiant de destination de la configuration de destination selon laquelle vous créez votre modèle.

>[!TIP]
>
>* L’identifiant de destination que vous devez utiliser ici est `instanceId`, qui correspond à une configuration de destination, créée à l’aide du point d’entrée `/destinations`. Reportez-vous à la section [référence de l’API de configuration de destination](./destination-configuration-api.md#retrieve-list).


**Format d’API**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Paramètre de requête | Description |
| -------- | ----------- |
| `{DESTINATION_ID}` | L’identifiant de la configuration de destination sur laquelle vous générez des exemples de profils. |
| `{COUNT}` | *Facultatif*. Le nombre d’exemples de profils que vous générez. Le paramètre peut prendre des valeurs entre les variables `1 - 1000`. <br> Si le paramètre count n’est pas spécifié, le nombre de profils générés par défaut est déterminé par la variable `maxUsersPerRequest` dans la variable [configuration du serveur de destination](./destination-server-api.md#create). Si cette propriété n’est pas définie, Adobe génère un exemple de profil. |

{style=&quot;table-layout:auto&quot;}

**Requête**

La requête suivante génère des exemples de profils, configurés par la variable `{DESTINATION_ID}` et `{COUNT}` paramètres de requête.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec le nombre spécifié de profils d’exemple, avec l’appartenance au segment, les identités et les attributs de profil qui correspondent au schéma XDM cible.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-vizii"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-adKYs"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-t4sKv"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-C3enB"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-bfnbs"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609626Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-6YjGc"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-SfJ21"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-eQMWS"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-d3WzP"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-eWfFn"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609823Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-2PMjZ"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-3aLez"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-D2H1J"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-i6PsF"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-VPUtZ"
                }
            ]
        }
    }
]
```

## Gestion des erreurs d’API {#api-error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant comment générer des profils d’exemple à utiliser lors de la [test d&#39;un modèle de transformation de message](./create-template.md) ou [test si votre destination est correctement configurée](./test-destination.md).
