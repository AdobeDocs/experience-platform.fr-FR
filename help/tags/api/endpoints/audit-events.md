---
title: Point d’entrée des événements d’audit
description: Découvrez comment effectuer des appels au point d’entrée /audit_events dans l’API Reactor.
exl-id: 59cd58dc-4085-47b7-846f-d3937740dd9b
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 100%

---

# Point d’entrée des événements d’audit

>[!WARNING]
>
>L’implémentation du point d’entrée `/audit_events` se fait en flux continu à mesure que des fonctionnalités sont ajoutées, supprimées et retravaillées.

Un événement d’audit est un enregistrement d’une modification spécifique apportée à une autre ressource de l’API Reactor; il est généré au moment de la modification. Il s’agit d’événements système auxquels vous pouvez vous abonner en utilisant un [rappel](./callbacks.md). Le point d’entrée `/audit_events` de l’API Reactor vous permet de gérer par programmation les événements d’audit dans votre application d’expérience.

Les événements d’audit sont structurés sous la forme `{RESOURCE_TYPE}.{EVENT}`, par exemple `build.created` ou `rule.updated`.

Le type de ressource peut être l’un des types suivants :

* `property`
* `extension`
* `data_element`
* `rule`
* `rule_component`
* `library`
* `build`
* `environment`
* `host`

Les événements suivants sont pris en charge pour chaque type de ressource :

* `created`
* `updated`
* `deleted`

## Prise en main

Le point d’entrée utilisé dans ce guide fait partie de lʼ[API Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes sur la marche à suivre pour s’authentifier auprès de l’API.

## Récupération d’une liste d’événements d’audit {#list}

Vous pouvez récupérer une liste d’événements d’audit pour toutes les propriétés détenues par votre organisation en envoyant une requête GET au point d’entrée `/audit_events`.

**Format d’API**

```http
GET /audit_events
```

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/audit_events \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie une liste d’événements d’audit. La réponse ci-dessous a été réduite pour gagner de l’espace.

```json
{
  "data": [
    {
      "id": "AEa98742de8ef044d8b86767aa6a15a674",
      "type": "audit_events",
      "attributes": {
        "attributed_to_display_name": "John Smith",
        "attributed_to_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:31:21.836Z",
        "display_name": "Kessel Apns App",
        "type_of": "app_configuration.updated",
        "updated_at": "2020-12-14T17:31:21.836Z",
        "entity": "{\"data\":{\"id\":\"AC40c339ab80d24c958b90d67b698602eb\",\"type\":\"app_configurations\",\"links\":{\"self\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb\",\"company\":\"https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1\"},\"attributes\":{\"name\":\"Kessel Apns App\",\"app_id\":\"com.adobe.test_app_2\",\"key_type\":\"p8_file\",\"platform\":\"mobile\",\"created_at\":\"2020-12-14T17:31:10.626Z\",\"updated_at\":\"2020-12-14T17:31:21.787Z\",\"messaging_service\":\"apns\"},\"relationships\":{\"company\":{\"data\":{\"id\":\"CO2bf094214ffd4785bb4bcf88c952a7c1\",\"type\":\"companies\"},\"links\":{\"related\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company\"}}}}}"
      },
      "relationships": {
        "property": {
          "links": {
            "related": null
          },
          "data": null
        },
        "entity": {
          "links": {
            "related": null
          },
          "data": {
            "type": "app_configurations",
            "id": "AC40c339ab80d24c958b90d67b698602eb"
          }
        }
      },
      "links": {
        "entity": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb",
        "property": null,
        "self": "https://reactor.adobe.io/audit_events/AEa98742de8ef044d8b86767aa6a15a674"
      }
    },
    {
      "id": "AE7320b6c1c3f84bb69405fcfe9cb58189",
      "type": "audit_events",
      "attributes": {
        "attributed_to_display_name": "John Smith",
        "attributed_to_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:31:10.672Z",
        "display_name": "Kessel Apns App",
        "type_of": "app_configuration.created",
        "updated_at": "2020-12-14T17:31:10.672Z",
        "entity": "{\"data\":{\"id\":\"AC40c339ab80d24c958b90d67b698602eb\",\"type\":\"app_configurations\",\"links\":{\"self\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb\",\"company\":\"https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1\"},\"attributes\":{\"name\":\"Kessel Apns App\",\"app_id\":\"com.adobe.test_app\",\"key_type\":\"p8_file\",\"platform\":\"mobile\",\"created_at\":\"2020-12-14T17:31:10.626Z\",\"updated_at\":\"2020-12-14T17:31:10.626Z\",\"messaging_service\":\"apns\"},\"relationships\":{\"company\":{\"data\":{\"id\":\"CO2bf094214ffd4785bb4bcf88c952a7c1\",\"type\":\"companies\"},\"links\":{\"related\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company\"}}}}}"
      },
      "relationships": {
        "property": {
          "links": {
            "related": null
          },
          "data": null
        },
        "entity": {
          "links": {
            "related": null
          },
          "data": {
            "type": "app_configurations",
            "id": "AC40c339ab80d24c958b90d67b698602eb"
          }
        }
      },
      "links": {
        "entity": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb",
        "property": null,
        "self": "https://reactor.adobe.io/audit_events/AE7320b6c1c3f84bb69405fcfe9cb58189"
      }
    }
  ],
  "links": {
    "self": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=1&page%5Bsize%5D=25",
    "next": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=2&page%5Bsize%5D=25",
    "last": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=129&page%5Bsize%5D=25"
  },
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 2
    }
  }
}
```

## Recherche d’un événement d’audit {#lookup}

Vous pouvez rechercher un événement d’audit en fournissant son identifiant dans le chemin d’accès d’une requête GET.

**Format d’API**

```http
GET /audit_events/{AUDIT_EVENT_ID}
```

| Paramètre | Description |
| --- | --- |
| `AUDIT_EVENT_ID` | Le `id` de l’événement d’audit que vous souhaitez rechercher. |

{style="table-layout:auto"}

**Requête**

```shell
curl -X GET \
  https://reactor.adobe.io/audit_events/AEa98742de8ef044d8b86767aa6a15a674 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Réponse**

Une réponse réussie renvoie les détails de l’événement d’audit.

```json
{
  "data": {
    "id": "AEd6a3b381fb8241818d7520001f8bd459",
    "type": "audit_events",
    "attributes": {
      "attributed_to_display_name": "John Smith",
      "attributed_to_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:31:46.956Z",
      "display_name": "Example Rule",
      "type_of": "rule.created",
      "updated_at": "2020-12-14T17:31:46.956Z",
      "entity": "{\"data\":{\"id\":\"RL52d156a9074844b89ca20c987dbafd3b\",\"meta\":{\"latest_revision_number\":0},\"type\":\"rules\",\"links\":{\"self\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b\",\"origin\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b\",\"property\":\"https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7\",\"rule_components\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components\"},\"attributes\":{\"name\":\"Example Rule\",\"dirty\":true,\"enabled\":true,\"published\":false,\"created_at\":\"2020-12-14T17:31:46.883Z\",\"deleted_at\":null,\"updated_at\":\"2020-12-14T17:31:46.883Z\",\"published_at\":null,\"review_status\":\"unsubmitted\",\"revision_number\":0},\"relationships\":{\"notes\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/notes\"}},\"origin\":{\"data\":{\"id\":\"RL52d156a9074844b89ca20c987dbafd3b\",\"type\":\"rules\"},\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/origin\"}},\"property\":{\"data\":{\"id\":\"PR03cc61073ef74fd2af21e4cfb6ed97a7\",\"type\":\"properties\"},\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/property\"}},\"libraries\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/libraries\"}},\"revisions\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/revisions\"}},\"rule_components\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components\"}}}}}"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459/property"
        },
        "data": {
          "id": "PR03cc61073ef74fd2af21e4cfb6ed97a7",
          "type": "properties"
        }
      },
      "entity": {
        "links": {
          "related": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459/rule"
        },
        "data": {
          "type": "rules",
          "id": "RL52d156a9074844b89ca20c987dbafd3b"
        }
      }
    },
    "links": {
      "entity": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b",
      "property": "https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7",
      "self": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459"
    },
    "meta": {
      "property_name": "Kessel Example Property"
    }
  }
}
```
