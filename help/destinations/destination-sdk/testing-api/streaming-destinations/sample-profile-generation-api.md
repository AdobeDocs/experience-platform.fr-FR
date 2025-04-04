---
description: Découvrez comment utiliser l’API de test de destination pour générer des profils types pour la destination de diffusion en streaming, que vous pouvez utiliser dans les tests de destination.
title: Génération de profils types en fonction d’un schéma source
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 98%

---


# Génération de profils types en fonction d’un schéma source {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

Cette page répertorie et décrit toutes les opérations de l’API que vous pouvez effectuer à l’aide du point d’entrée de l’API `/authoring/sample-profiles`.

## Génération de différents types de profils pour différentes interfaces API {#different-profiles-different-apis}

>[!IMPORTANT]
>
>Utilisez ce point d’entrée de l’API pour générer des profils types pour deux cas d’utilisation distincts. Vous pouvez effectuer l’une des actions suivantes :
>* Générer des profils à utiliser au moment de la [conception et du test d’un modèle de transformation des messages](create-template.md), à l’aide de l’*identifiant de destination* comme paramètre de requête.
>* Générer des profils à utiliser lors d’appels pour [tester si la destination est correctement configurée](streaming-destination-testing-overview.md), à l’aide de l’*identifiant d’instance de destination* comme paramètre de requête.

Vous pouvez générer des profils types en fonction du schéma source XDM d’Adobe (à utiliser au moment du test de la destination) ou du schéma cible pris en charge par la destination (à utiliser lors de la conception de votre modèle). Pour comprendre la différence entre le schéma source XDM d’Adobe et le schéma cible, consultez la section de présentation de l’article [Format de message](../../functionality/destination-server/message-format.md).

Notez que les profils types ne peuvent pas être utilisés à d’autres fins. Les profils générés à partir de l’*identifiant de destination* peuvent uniquement être utilisés pour concevoir des modèles et les profils de transformation de messages générés en fonction des *identifiants d’instance de destination* peuvent uniquement être utilisés pour tester le point d’entrée de destination.

## Prise en main des opérations de l’API de génération de profils types {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Génération de profils types en fonction du schéma source à utiliser lors du test de la destination {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>Ajoutez les profils types générés ici aux appels HTTP lors du [test de la destination](streaming-destination-testing-overview.md).

Vous pouvez générer des profils types en fonction du schéma source en adressant une requête GET au point d’entrée `authoring/sample-profiles/` avec l’identifiant de l’instance de destination que vous avez créé en fonction de la configuration de destination que vous souhaitez tester.

Pour obtenir l’identifiant d’une instance de destination, vous devez d’abord créer une connexion dans l’interface utilisateur d’Experience Platform vers la destination avant d’essayer de tester la destination. Pour découvrir comment obtenir l’identifiant d’instance de destination à utiliser pour cette API, consultez le [tutoriel sur l’activation de la destination](../../../ui/activation-overview.md) et l’astuce ci-dessous.

>[!IMPORTANT]
>
>* Pour utiliser cette API, vous devez disposer d’une connexion existante vers la destination dans l’interface utilisateur d’Experience Platform. Pour plus d’informations, consultez la documentation [Se connecter à la destination](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=fr) et [Activer des profils et des audiences vers cette destination](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html).
> * Après avoir établi la connexion à la destination, obtenez l’identifiant d’instance de destination que vous devez utiliser dans les appels API vers ce point d’entrée pendant la [recherche d’une connexion avec la destination ](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html).
>![Image de l’interface utilisateur illustrant comment obtenir l’identifiant d’instance de destination](../../assets/testing-api/get-destination-instance-id.png)

**Format d’API**

```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Paramètre de requête | Description |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | Identifiant de l’instance de destination en fonction de laquelle vous générez des profils types. |
| `{COUNT}` | *Facultatif*. Nombre de profils types que vous générez. Le paramètre peut prendre des valeurs entre `1 - 1000`. <br> Si le paramètre de nombre n’est pas spécifié, le nombre de profils générés par défaut est déterminé par la valeur `maxUsersPerRequest` dans la [configuration du serveur de destination](../../authoring-api/destination-server/create-destination-server.md). Si cette propriété n’est pas définie, Adobe génère alors un profil type. |

{style="table-layout:auto"}


**Requête**

La requête suivante génère des profils types, configurés par les paramètres de requête `{DESTINATION_INSTANCE_ID}` et `{COUNT}`.

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

Une réponse réussie renvoie le statut HTTP 200 avec le nombre spécifié d’échantillons de profils, les appartenances à l’audience, les identités et les attributs de profil qui correspondent au schéma XDM source.

>[!TIP]
>
> La réponse ne renvoie que les appartenances à l’audience, les identités et les attributs de profil utilisés dans l’instance de destination. Même si votre schéma source comporte d’autres champs, ceux-ci sont ignorés.

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
| `segmentMembership` | Objet de mappage décrivant les appartenances à des audiences d’un individu. Pour plus d’informations sur `segmentMembership`, consultez [Détails de l’appartenance à une audience](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html?lang=fr). |
| `lastQualificationTime` | Date et heure de la dernière qualification de ce profil pour le segment. |
| `xdm:status` | Champ de type chaîne indiquant si l’appartenance à l’audience a été établie dans le cadre de la requête actuelle. Les valeurs suivantes sont acceptées : <ul><li>`realized` : le profil fait partie du segment.</li><li>`exited` : le profil quitte l’audience dans le cadre de la requête actuelle.</li></ul> |
| `identityMap` | Champ de type map qui décrit les différentes valeurs d’identité d’un individu, ainsi que les espaces de noms qui lui sont associés. Pour plus d’informations sur `identityMap`, consultez [Base de la composition des schémas](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#identityMap). |

{style="table-layout:auto"}

## Génération de profils types en fonction du schéma cible à utiliser au moment de la création de votre modèle de transformation de message {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>Utilisez les profils types générés ici au moment de la conception de votre modèle, dans l’[étape du modèle de rendu](render-template-api.md#multiple-profiles-with-body).

Vous pouvez générer des profils types en fonction du schéma cible en adressant une requête GET au point d’entrée `authoring/sample-profiles/` et en fournissant l’identifiant de destination de la configuration de destination à partir de laquelle vous créez votre modèle.

>[!TIP]
>
>* L’identifiant de destination que vous devez utiliser ici est `instanceId`, qui correspond à une configuration de destination, créée à l’aide du point d’entrée `/destinations`. Pour plus d’informations, consultez la [récupération d’une configuration de destination](../../authoring-api/destination-configuration/retrieve-destination-configuration.md).

**Format d’API**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Paramètre de requête | Description |
| -------- | ----------- |
| `{DESTINATION_ID}` | Identifiant de la configuration de destination en fonction de laquelle vous générez des profils types. |
| `{COUNT}` | *Facultatif*. Nombre de profils types que vous générez. Le paramètre peut prendre des valeurs entre `1 - 1000`. <br> Si le paramètre de nombre n’est pas spécifié, le nombre de profils générés par défaut est déterminé par la valeur `maxUsersPerRequest` dans la [configuration du serveur de destination](../../authoring-api/destination-server/create-destination-server.md). Si cette propriété n’est pas définie, Adobe génère alors un profil type. |

{style="table-layout:auto"}

**Requête**

La requête suivante génère des profils types, configurés par les paramètres de requête `{DESTINATION_ID}` et `{COUNT}`.

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

Une réponse réussie renvoie le statut HTTP 200 avec le nombre spécifié d’échantillons de profils, les appartenances à l’audience, les identités et les attributs de profil qui correspondent au schéma XDM source.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "realized"
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
                    "status": "realized"
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
                    "status": "realized"
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

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes d’état API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs d’en-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment générer des profils types à utiliser lors du [test d’un modèle de transformation de message](create-template.md) ou un [test de vérification de la configuration de la destination](streaming-destination-testing-overview.md).
