---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;Segmentation;Segmentation Service;segmentation par flux;segmentation par flux;Segmentation par flux;Évaluation continue;
solution: Experience Platform
title: Évaluation des événements en temps quasi réel avec la segmentation par flux
topic-legacy: developer guide
description: Ce document contient des exemples d’utilisation de la segmentation par flux avec l’API Adobe Experience Platform Segmentation Service.
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: 30a12fee487609b4c85ba342963bb915e8152195
workflow-type: tm+mt
source-wordcount: '1938'
ht-degree: 33%

---

# Évaluer les événements en temps quasi réel grâce à la segmentation par flux

>[!NOTE]
>
>Le document suivant indique comment utiliser la segmentation par flux à l’aide de l’API. Pour plus d’informations sur l’utilisation de la segmentation par flux à l’aide de l’interface utilisateur, veuillez lire le [guide de l’interface utilisateur de segmentation par flux](../ui/streaming-segmentation.md).

Segmentation par flux sur [!DNL Adobe Experience Platform] permet aux clients d’effectuer une segmentation en temps quasi réel tout en se concentrant sur la richesse des données. Avec la segmentation par flux, la qualification de segment se produit maintenant lorsque les données en continu entrent dans [!DNL Platform], ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation. Grâce à cette fonctionnalité, la plupart des règles de segmentation peuvent désormais être évaluées au fur et à mesure de la transmission des données. [!DNL Platform], ce qui signifie que l’adhésion au segment sera maintenue à jour sans exécuter les tâches de segmentation planifiées.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>La segmentation par flux fonctionne sur toutes les données ingérées à l’aide d’une source de diffusion en continu. Les segments ingérés à l’aide d’une source par lots seront évalués de nuit, même s’ils sont qualifiés pour la segmentation par flux.
>
>En outre, les segments évalués avec la segmentation par flux peuvent dériver entre l’adhésion idéale et l’adhésion réelle si le segment est basé sur un autre segment évalué à l’aide de la segmentation par lots. Si, par exemple, le segment A est basé sur le segment B et le segment B est évalué à l’aide de la segmentation par lots, puisque le segment B n’est mis à jour que toutes les 24 heures, le segment A s’éloigne davantage des données réelles jusqu’à ce qu’il se resynchronise avec la mise à jour du segment B.

## Prise en main

Ce guide de développement nécessite une compréhension pratique des différentes [!DNL Adobe Experience Platform] services impliqués dans la segmentation par flux. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fournit un profil client unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [[!DNL Segmentation]](../home.md): Permet de créer des segments et des audiences à partir de vos [!DNL Real-time Customer Profile] data.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à [!DNL Platform] API.

### Lecture d’exemples d’appels API

Ce guide de développement fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les environnements de test dans [!DNL Platform], consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

Des en-têtes supplémentaires peuvent être nécessaires pour effectuer des requêtes spécifiques. Les en-têtes corrects sont présentés dans chacun des exemples de ce document. Accordez une attention particulière aux exemples de requêtes afin de vous assurer que tous les en-têtes requis sont inclus.

### Types de requête permettant la segmentation par flux {#query-types}

>[!NOTE]
>
>Vous devez activer la segmentation planifiée pour l’organisation afin que la segmentation par flux fonctionne. Vous trouverez des informations sur l’activation de la segmentation planifiée dans la section [Activation de la section de segmentation planifiée](#enable-scheduled-segmentation)

Pour qu’un segment soit évalué à l’aide de la segmentation par flux, la requête doit respecter les instructions suivantes.

| Type de requête | Détails |
| ---------- | ------- |
| Événement unique | Toute définition de segment qui fait référence à un seul événement entrant sans restriction temporelle. |
| Événement unique dans une fenêtre temporelle relative | Toute définition de segment qui fait référence à un seul événement entrant. |
| Un seul événement avec une fenêtre temporelle | Toute définition de segment qui fait référence à un seul événement entrant avec une fenêtre temporelle. |
| Profil uniquement | Toute définition de segment qui ne fait référence qu’à un attribut de profil. |
| Événement unique avec un attribut de profil | Toute définition de segment qui fait référence à un seul événement entrant, sans restriction temporelle, et à un ou plusieurs attributs de profil. **Remarque :** La requête est immédiatement évaluée lorsque l’événement arrive. Toutefois, dans le cas d’un événement de profil, il doit attendre 24 heures pour être incorporé. |
| Événement unique avec un attribut de profil dans une fenêtre de temps relative | Toute définition de segment qui fait référence à un seul événement entrant et à un ou plusieurs attributs de profil. |
| Segment de segments | Toute définition de segment contenant un ou plusieurs segments par lot ou en flux continu. **Remarque :** Si un segment est utilisé, la disqualification du profil se produit. **toutes les 24 heures**. |
| Plusieurs événements avec un attribut de profil | Toute définition de segment qui fait référence à plusieurs événements **au cours des dernières 24 heures** et (éventuellement) comporte un ou plusieurs attributs de profil. |

Une définition de segment sera **not** être activé pour la segmentation par flux dans les scénarios suivants :

- La définition de segment inclut des segments ou des caractéristiques Adobe Audience Manager (AAM).
- La définition de segment comprend plusieurs entités (requêtes d’entités multiples).

Veuillez noter que les instructions suivantes s’appliquent lors de la segmentation par flux :

| Type de requête | Instruction |
| ---------- | -------- |
| Requête d’événement unique | Il n’existe aucune limite à l’intervalle de recherche en amont. |
| Requête avec historique des événements | <ul><li>L’intervalle de recherche en amont est limité à **un jour**.</li><li>Condition d’ordre du temps stricte **must** existent entre les événements.</li><li>Les requêtes comportant au moins un événement annulé sont prises en charge. Cependant, l’événement entier **cannot** être une négation.</li></ul> |

Si une définition de segment est modifiée de sorte qu’elle ne répond plus aux critères de la segmentation par flux, elle passe automatiquement de &quot;Diffusion en continu&quot; à &quot;Lot&quot;.

De plus, l’exclusion du segment, tout comme la qualification du segment, se produit en temps réel. Par conséquent, si une audience n’est plus admissible pour un segment, elle sera immédiatement non qualifiée. Par exemple, si la définition de segment demande &quot;Tous les utilisateurs qui ont acheté des chaussures rouges au cours des trois dernières heures&quot;, au bout de trois heures, tous les profils initialement qualifiés pour la définition de segment ne seront pas qualifiés.

## Récupération de tous les segments activés pour la segmentation par flux

Vous pouvez récupérer une liste de tous vos segments qui sont activés pour la segmentation par flux dans votre organisation IMS en adressant une demande de GET à la fonction `/segment/definitions` point de terminaison .

**Format d’API**

Pour récupérer les segments activés dans le flux, vous devez inclure le paramètre de requête `evaluationInfo.continuous.enabled=true` dans le chemin de requête.

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**Requête**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de segments de votre organisation IMS permettant une segmentation par flux.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Création d’un segment activé dans le flux

Un segment est automatiquement activé en continu s’il correspond à l’un des segments [types de segmentation par flux répertoriés ci-dessus](#query-types).

**Format d’API**

```http
POST /segment/definitions
```

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    }
}'
```

>[!NOTE]
>
>Il s’agit d’une requête &quot;créer un segment&quot; standard. Pour plus d’informations sur la création d’une définition de segment, consultez le tutoriel sur [création d’un segment](../tutorials/create-a-segment.md).

**Réponse**

Une réponse réussie renvoie les détails de la nouvelle définition de segment activée dans le flux.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true,
                   },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## Activation de l’évaluation planifiée {#enable-scheduled-segmentation}

Une fois l’évaluation par flux activée, une ligne de base doit être créée (ensuite le segment sera toujours à jour). L’évaluation planifiée (également appelée segmentation planifiée) doit d’abord être activée pour que le système effectue automatiquement la mise en base. Avec la segmentation planifiée, votre organisation IMS peut se conformer à un planning récurrent pour exécuter automatiquement les tâches d’exportation afin d’évaluer les segments.

>[!NOTE]
>
>L’évaluation planifiée peut être activée pour les environnements de test avec un maximum de cinq (5) stratégies de fusion pour [!DNL XDM Individual Profile]. Si votre organisation dispose de plus de cinq stratégies de fusion pour [!DNL XDM Individual Profile] dans un seul environnement de test, vous ne pourrez pas utiliser l’évaluation planifiée.

### Création d’un planning

En effectuant une requête POST sur le point de terminaison `/config/schedules`, vous pouvez créer un planning et inclure l’heure spécifique à laquelle le planning doit être déclenché.

**Format d’API**

```http
POST /config/schedules
```

**Requête**

La requête suivante crée un planning en fonction des spécifications fournies dans le payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | **(Obligatoire)** Le nom du planning. Doit être une chaîne. |
| `type` | **(Obligatoire)** Le type de tâche au format chaîne. Les types `batch_segmentation` et `export` sont pris en charge. |
| `properties` | **(Obligatoire)** Un objet contenant des propriétés supplémentaires liées au planning. |
| `properties.segments` | **(Obligatoire lorsque `type` est égal à `batch_segmentation`)** L’utilisation de `["*"]` permet de s’assurer que tous les segments sont inclus. |
| `schedule` | **(Obligatoire)** Une chaîne contenant le planning de la tâche. Vous ne pouvez planifier qu’une seule exécution de tâche par jour, ce qui signifie que vous ne pouvez pas planifier l’exécution d’une tâche plus d’une fois au cours d’une période de 24 heures. L’exemple illustré (`0 0 1 * * ?`) signifie que la tâche est déclenchée tous les jours à 1:00:00 UTC. Pour plus d’informations, veuillez consulter l’ annexe de la section [format d’expression cron](./schedules.md#appendix) dans la documentation sur les plannings dans la segmentation. |
| `state` | *(Facultatif)* Chaîne contenant l’état du planning. Valeurs disponibles : `active` et `inactive`. La valeur par défaut est `inactive`. Une organisation IMS ne peut créer qu’un seul planning. Les étapes de mise à jour du planning sont disponibles plus loin dans ce tutoriel. |

**Réponse**

Une réponse réussie renvoie les détails du planning créé.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

### Activation d’un planning

Par défaut, un planning est inactif lors de la création, sauf si la propriété `state` est définie sur `active` dans le corps de la requête de création (POST). Vous pouvez activer un planning (définissez `state` sur `active`) en effectuant une requête PATCH sur le point de terminaison `/config/schedules` et en incluant l’identifiant du planning dans le chemin.

**Format d’API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Requête**

La requête suivante utilise le [format du correctif JSON](https://datatracker.ietf.org/doc/html/rfc6902) pour mettre à jour l’état `state` du planning sur `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**Réponse**

Une mise à jour réussie renvoie un corps de réponse vide et un état HTTP 204 (No Content).

La même opération peut être utilisée pour désactiver un planning en remplaçant la « valeur » de la requête précédente par « inactif ».

## Étapes suivantes

Maintenant que vous avez activé la segmentation par flux pour les segments nouveaux et existants, ainsi que la segmentation planifiée pour développer une ligne de base et effectuer des évaluations récurrentes, vous pouvez commencer à créer des segments activés par flux pour votre organisation.

Pour savoir comment effectuer des actions similaires et utiliser des segments à l’aide de l’interface utilisateur d’Adobe Experience Platform, consultez le [guide d’utilisation du créateur de segments](../ui/segment-builder.md).

## Annexe

La section suivante répertorie les questions fréquentes sur la segmentation par flux :

### La segmentation par flux &quot;non-qualification&quot; se produit-elle également en temps réel ?

Pour la plupart des instances, l’inqualification de la segmentation par flux se produit en temps réel. Toutefois, les segments en flux continu qui utilisent des segments le font **not** non admissible en temps réel, mais non admissible après 24 heures.

### Sur quelles données la segmentation par flux fonctionne-t-elle ?

La segmentation par flux fonctionne sur toutes les données ingérées à l’aide d’une source de diffusion en continu. Les segments ingérés à l’aide d’une source par lots seront évalués de nuit, même s’ils sont qualifiés pour la segmentation par flux. Les événements diffusés dans le système avec un horodatage de plus de 24 heures seront traités dans la tâche par lots suivante.

### Comment les segments sont-ils définis comme segmentation par lots ou par flux ?

Un segment est défini comme une segmentation par lot ou par flux basée sur une combinaison de type de requête et de durée d’historique des événements. Vous trouverez une liste des segments qui seront évalués en tant que segment en continu dans la variable [section types de requête de segmentation par flux](#query-types).

Notez que si un segment contient **both** an `inSegment` et une chaîne d’événement unique directe, elle ne peut pas être admissible pour la segmentation par flux. Si vous souhaitez que ce segment soit admissible pour la segmentation par flux, vous devez faire de la chaîne d’événement unique directe son propre segment.

### Pourquoi le nombre de segments &quot;total qualifié&quot; continue-t-il à augmenter alors que le nombre sous &quot;X derniers jours&quot; reste à zéro dans la section de détails du segment ?

Le nombre total de segments qualifiés est tiré de la tâche de segmentation quotidienne, qui inclut les audiences qui remplissent les critères des segments par lot et par flux. Cette valeur s’affiche pour les segments par lot et en flux continu.

Nombre sous &quot;X derniers jours&quot; **only** inclut les audiences qualifiées en segmentation par flux, et **only** augmente si vous avez diffusé des données en flux continu dans le système et qu’elles sont prises en compte dans cette définition de flux continu. Cette valeur est **only** s’affiche pour les segments en continu. Par conséquent, cette valeur **may** s’affiche comme 0 pour les segments par lot.

Par conséquent, si vous constatez que le nombre sous &quot;X derniers jours&quot; est nul et que le graphique linéaire signale également zéro, vous avez la valeur **not** diffusion en continu de tous les profils dans le système qui répondent aux critères de ce segment.

### Combien de temps faut-il pour qu’un segment soit disponible ?

La disponibilité d’un segment peut prendre jusqu’à une heure.