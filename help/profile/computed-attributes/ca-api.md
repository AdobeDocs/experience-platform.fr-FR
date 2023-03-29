---
keywords: Experience Platform;profil;real-time customer profile;dépannage;API
title: Point de terminaison de l’API Attributs calculés
type: Documentation
description: Dans Adobe Experience Platform, les attributs calculés sont des fonctions utilisées pour agréger les données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées au niveau de la segmentation, de l’activation et de la personnalisation. Ce guide explique comment créer, afficher, mettre à jour et supprimer des attributs calculés à l’aide de l’API Real-time Customer Profile.
exl-id: 6b35ff63-590b-4ef5-ab39-c36c39ab1d58
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '2275'
ht-degree: 65%

---

# (Alpha) Point d’entrée de l’API des attributs calculés

>[!IMPORTANT]
>
>La fonctionnalité d’attribut calculé décrite dans ce document est actuellement en version alpha et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Les attributs calculés sont des fonctions utilisées pour regrouper des données au niveau de l’événement en attributs au niveau du profil. Ces fonctions sont automatiquement calculées afin de pouvoir être utilisées au niveau de la segmentation, de l’activation et de la personnalisation. Ce guide comprend des exemples d’appels API pour effectuer des opérations CRUD de base à l’aide de `/computedAttributes` point de terminaison .

Pour en savoir plus sur les attributs calculés, commencez par lire le [présentation des attributs calculés](overview.md).

## Prise en main

Le point de terminaison API utilisé dans ce guide fait partie de la variable [API Real-Time Customer Profile](https://www.adobe.com/go/profile-apis-en).

Avant de poursuivre, veuillez consulter la section [Guide de prise en main de l’API Profile](../api/getting-started.md) pour obtenir des liens vers la documentation recommandée, un guide de lecture des exemples d’appels API qui apparaissent dans ce document, ainsi que des informations importantes concernant les en-têtes requis pour réussir les appels à une API Experience Platform.

## Configuration d’un champ d’attribut calculé

Pour créer un attribut calculé, vous devez d’abord identifier le champ dans un schéma qui contiendra la valeur de l’attribut calculé.

Reportez-vous à la documentation relative à la [configuration d’un attribut calculé](configure-api.md) pour obtenir un guide complet de bout en bout sur la création d’un champ d’attribut calculé dans un schéma.

>[!WARNING]
>
>Pour pouvoir continuer avec le guide d’API, un champ d’attribut calculé doit être configuré.

## Création d’un attribut calculé {#create-a-computed-attribute}

Avec votre champ d’attribut calculé défini dans votre schéma activé pour Profile, vous pouvez maintenant configurer un attribut calculé. Si vous ne l’avez pas déjà fait, suivez le workflow décrit dans la section [configuration d’un attribut calculé](configure-api.md) documentation.

Pour créer un attribut calculé, commencez par envoyer une requête de POST à la variable `/config/computedAttributes` point de terminaison avec un corps de requête contenant les détails de l’attribut calculé que vous souhaitez créer.

**Format d’API**

```http
POST /config/computedAttributes
```

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "birthdayCurrentMonth",
        "path": "_{TENANT_ID}",
        "description": "Computed attribute to capture if the customer birthday is in the current month.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Propriété | Description |
|---|---|
| `name` | Le nom du champ attribut calculé, sous forme de chaîne. |
| `path` | Le chemin d’accès au champ contenant l’attribut calculé. Ce chemin d’accès se trouve dans l’attribut `properties` du schéma et ne doit PAS inclure le nom du champ. Lors de l’écriture du chemin d’accès, omettez les multiples niveaux des attributs `properties`. |
| `{TENANT_ID}` | Si vous ne connaissez pas votre identifiant de client, veuillez vous reporter à la procédure de recherche de votre identifiant de client dans le [guide de développement du registre des schémas](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Une description de l’attribut calculé. Celle-ci s’avère particulièrement utile si vous avez défini plusieurs attributs calculés, car elle aidera les autres membres de votre organisation IMS à déterminer l’attribut calculé correct à utiliser. |
| `expression.value` | Un valide [!DNL Profile Query Language] (PQL). Les attributs calculés prennent actuellement en charge les fonctions suivantes : sum, count, min, max et boolean. Pour obtenir une liste d’exemples d’expressions, reportez-vous à la section [exemple d’expressions PQL](expressions.md) documentation. |
| `schema.name` | La classe sur laquelle le schéma contenant le champ attribut calculé est basé. Par exemple : `_xdm.context.experienceevent` pour un schéma basé sur la classe XDM ExperienceEvent. |

**Réponse**

Un attribut calculé créé avec succès renvoie un état HTTP 200 (OK) et un corps de réponse contenant les détails de l’attribut calculé que vous venez de créer. Ces détails incluent un `id` unique, en lecture seule, généré par le système que vous pouvez utiliser pour faire référence à l’attribut calculé pendant les autres opérations API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| Propriété | Description |
|---|---|
| `id` | Un identifiant unique, en lecture seule, généré par le système que vous pouvez utiliser pour faire référence à l’attribut calculé pendant les autres opérations API. |
| `imsOrgId` | L’organisation IMS associée à l’attribut calculé doit correspondre à la valeur envoyée dans la requête. |
| `sandbox` | L’objet Sandbox contient des détails sur le sandbox sur lequel l’attribut calculé a été configuré. Ces informations sont tirées de l’en-tête du sandbox envoyé dans la requête. Pour plus d’informations, consultez la [présentation des sandbox](../../sandboxes/home.md). |
| `positionPath` | Un tableau contenant le `path` déconstruit vers le champ envoyé dans la requête. |
| `returnSchema.meta:xdmType` | Le type du champ dans lequel l’attribut calculé sera stocké. |
| `definedOn` | Un tableau affichant les schémas d’union sur lesquels l’attribut calculé a été défini. Contient un objet par schéma d’union, ce qui signifie qu’il peut y avoir plusieurs objets dans le tableau si l’attribut calculé a été ajouté à plusieurs schémas selon différentes classes. |
| `active` | Une valeur booléenne affichant si l’attribut calculé est actuellement actif ou non. Par défaut, la valeur est `true`. |
| `type` | Le type de ressource créé, dans la case « ComputedAttribute » est la valeur par défaut. |
| `createEpoch` et `updateEpoch` | L’heure à laquelle l’attribut calculé a été respectivement créé et mis à jour pour la dernière fois. |

## Création d’un attribut calculé qui référence des attributs calculés existants

Il est également possible de créer un attribut calculé qui référence des attributs calculés existants. Pour ce faire, commencez par envoyer une requête de POST à la fonction `/config/computedAttributes` point de terminaison . Le corps de la requête contiendra des références aux attributs calculés dans la variable `expression.value` comme illustré dans l’exemple ci-dessous.

**Format d’API**

```http
POST /config/computedAttributes
```

**Requête**

Dans cet exemple, deux attributs calculés ont déjà été créés et seront utilisés pour définir un troisième. Les attributs calculés existants sont les suivants :

* **`totalSpend`:** Capture le montant total en dollars qu’un client a dépensé.
* **`countPurchases`:** Compte le nombre d’achats effectués par un client.

La requête ci-dessous fait référence aux deux attributs calculés existants, en utilisant un PQL valide à diviser pour calculer le nouveau `averageSpend` attribut calculé.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "averageSpend",
        "path": "_{TENANT_ID}.purchaseSummary",
        "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Propriété | Description |
|---|---|
| `name` | Le nom du champ attribut calculé, sous forme de chaîne. |
| `path` | Le chemin d’accès au champ contenant l’attribut calculé. Ce chemin d’accès se trouve dans l’attribut `properties` du schéma et ne doit PAS inclure le nom du champ. Lors de l’écriture du chemin d’accès, omettez les multiples niveaux des attributs `properties`. |
| `{TENANT_ID}` | Si vous ne connaissez pas votre identifiant de client, veuillez vous reporter à la procédure de recherche de votre identifiant de client dans le [guide de développement du registre des schémas](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Une description de l’attribut calculé. Celle-ci s’avère particulièrement utile si vous avez défini plusieurs attributs calculés, car elle aidera les autres membres de votre organisation IMS à déterminer l’attribut calculé correct à utiliser. |
| `expression.value` | Une expression PQL valide. Les attributs calculés prennent actuellement en charge les fonctions suivantes : sum, count, min, max et boolean. Pour obtenir une liste d’exemples d’expressions, reportez-vous à la section [exemple d’expressions PQL](expressions.md) documentation.<br/><br/>Dans cet exemple, l’expression fait référence à deux attributs calculés existants. Les attributs sont référencés à l’aide de la fonction `path` et le `name` de l’attribut calculé tel qu’il apparaît dans le schéma dans lequel les attributs calculés ont été définis. Par exemple, la variable `path` du premier attribut calculé référencé est `_{TENANT_ID}.purchaseSummary` et le `name` is `totalSpend`. |
| `schema.name` | La classe sur laquelle le schéma contenant le champ attribut calculé est basé. Par exemple : `_xdm.context.experienceevent` pour un schéma basé sur la classe XDM ExperienceEvent. |

**Réponse**

Un attribut calculé créé avec succès renvoie un état HTTP 200 (OK) et un corps de réponse contenant les détails de l’attribut calculé que vous venez de créer. Ces détails incluent un `id` unique, en lecture seule, généré par le système que vous pouvez utiliser pour faire référence à l’attribut calculé pendant les autres opérations API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "averageSpend",
    "path": "_{TENANT_ID}.purchaseSummary",
    "positionPath": [
        "_{TENANT_ID}",
        "purchaseSummary"
    ],
    "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
    "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "number"
    },
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"\bVR)JMSR())(+KLOJKկHO+I(/(OI/S8{E:",
    "dependencies": [
        "c08a92f3-2418-4a3d-89d0-96f15fda3e5d",
        "4ed9e3aa-57ae-4705-9e8a-7fba9a6a7010"
    ],
    "dependents": [],
    "active": true,
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
    "type": "ComputedAttribute",
    "createEpoch": 1613696592,
    "updateEpoch": 1613696593
}
```

| Propriété | Description |
|---|---|
| `id` | Un identifiant unique, en lecture seule, généré par le système que vous pouvez utiliser pour faire référence à l’attribut calculé pendant les autres opérations API. |
| `imsOrgId` | L’organisation IMS associée à l’attribut calculé doit correspondre à la valeur envoyée dans la requête. |
| `sandbox` | L’objet Sandbox contient des détails sur le sandbox sur lequel l’attribut calculé a été configuré. Ces informations sont tirées de l’en-tête du sandbox envoyé dans la requête. Pour plus d’informations, consultez la [présentation des sandbox](../../sandboxes/home.md). |
| `positionPath` | Un tableau contenant le `path` déconstruit vers le champ envoyé dans la requête. |
| `returnSchema.meta:xdmType` | Le type du champ dans lequel l’attribut calculé sera stocké. |
| `definedOn` | Un tableau affichant les schémas d’union sur lesquels l’attribut calculé a été défini. Contient un objet par schéma d’union, ce qui signifie qu’il peut y avoir plusieurs objets dans le tableau si l’attribut calculé a été ajouté à plusieurs schémas selon différentes classes. |
| `active` | Une valeur booléenne affichant si l’attribut calculé est actuellement actif ou non. Par défaut, la valeur est `true`. |
| `type` | Le type de ressource créé, dans la case « ComputedAttribute » est la valeur par défaut. |
| `createEpoch` et `updateEpoch` | L’heure à laquelle l’attribut calculé a été respectivement créé et mis à jour pour la dernière fois. |

## Accès aux attributs calculés

Lorsque vous travaillez avec des attributs calculés en utilisant l’API, vous avez deux options pour accéder aux attributs calculés définis par votre organisation. La première consiste à répertorier tous les attributs calculés, la seconde à afficher un attribut calculé spécifique selon son `id` unique.

Les étapes des deux modèles d’accès sont décrites dans ce document. Sélectionnez l’une des options suivantes pour commencer :

* **[Liste de tous les attributs calculés existants](#list-all-computed-attributes):** Renvoie une liste de tous les attributs calculés existants créés par votre organisation.
* **[Affichage d’un attribut calculé spécifique](#view-a-computed-attribute):** Renvoie les détails d’un attribut calculé unique en spécifiant son identifiant lors de la requête.

### Liste de tous les attributs calculés {#list-all-computed-attributes}

Votre organisation IMS peut créer plusieurs attributs calculés et réaliser une requête GET sur le point de terminaison `/config/computedAttributes` vous permet de répertorier tous les attributs calculés existant pour votre organisation.

**Format d’API**

```http
GET /config/computedAttributes
```

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie inclut un attribut `_page` qui fournit le nombre total d’attributs calculés (`totalCount`) et le nombre d’attributs calculés sur la page (`pageSize`).

La réponse inclut également un tableau `children` composé d’un ou de plusieurs objets qui contiennent chacun les détails d’un attribut calculé. Si votre organisation ne dispose d’aucun attribut calculé, la variable `totalCount` et `pageSize` sera 0 (zéro) et la variable `children` est vide.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type": "PQL", 
                "format": "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Propriété | Description |
|---|---|
| `_page.totalCount` | Le nombre total d’attributs calculés définis par votre organisation IMS. |
| `_page.pageSize` | Le nombre d’attributs calculés renvoyés sur cette page de résultats. Si `pageSize` est égal à `totalCount`, cela signifie qu’il n’y a qu’une seule page de résultats et que tous les attributs calculés ont été renvoyés. Si ces valeurs ne sont pas égales, cela signifie que vous pouvez accéder à des pages de résultats supplémentaires. Consultez `_links.next` pour plus d’informations. |
| `children` | Un tableau composé d’un ou plusieurs objets, contenant chacun les détails d’un attribut calculé unique. Si aucun attribut calculé n’a été défini, le tableau `children` est vide. |
| `id` | Une valeur unique, en lecture seule, générée par le système attribuée automatiquement à un attribut calculé à sa création. Pour plus d’informations sur les composants d’un objet attribut calculé, veuillez consulter la section [Création d’un attribut calculé](#create-a-computed-attribute) qui apparaît plus tôt dans ce tutoriel. |
| `_links.next` | Si une page unique d’attributs calculés est renvoyée, `_links.next` est un objet vide, comme illustré dans l’exemple de réponse ci-dessus. Si votre organisation dispose de nombreux attributs calculés, ils seront renvoyés sur plusieurs pages auxquelles vous pourrez accéder en effectuant une requête GET sur la valeur `_links.next`. |

### Affichage d’un attribut calculé {#view-a-computed-attribute}

Vous pouvez afficher un attribut calculé spécifique en envoyant une requête GET au `/config/computedAttributes` point de terminaison et inclusion de l’identifiant d’attribut calculé dans le chemin d’accès de la requête.

**Format d’API**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Paramètre | Description |
|---|---|
| `{ATTRIBUTE_ID}` | L’identifiant de l’attribut calculé que vous souhaitez afficher. |

**Requête**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## Mise à jour d’un attribut calculé

Si vous estimez que vous avez besoin de mettre à jour un attribut calculé, vous pouvez effectuer une requête PATCH sur le point de terminaison `/config/computedAttributes` et inclure l’identifiant de l’attribut calculé que vous souhaitez mettre à jour dans le chemin d’accès de la requête.

**Format d’API**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Paramètre | Description |
|---|---|
| `{ATTRIBUTE_ID}` | L’identifiant de l’attribut calculé que vous souhaitez mettre à jour. |

**Requête**

Cette requête utilise le [format du correctif JSON](https://datatracker.ietf.org/doc/html/rfc6902) pour mettre à jour la « valeur » du champ « expression ».

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type": "PQL", 
            "format": "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Propriété | Description |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Un valide [!DNL Profile Query Language] (PQL). Les attributs calculés prennent actuellement en charge les fonctions suivantes : sum, count, min, max et boolean. Pour obtenir une liste d’exemples d’expressions, reportez-vous à la section [exemple d’expressions PQL](expressions.md) documentation. |

**Réponse**

Une mise à jour réussie renvoie un état HTTP 204 (No Content) et un corps de réponse vide. Si vous souhaitez confirmer que la mise à jour a réussi, vous pouvez réaliser une requête GET pour afficher l’attribut complété en fonction de son identifiant.

## Suppression d’un attribut calculé

Il est également possible de supprimer un attribut calculé à l’aide de l’API. Vous pouvez effectuer ceci à l’aide d’une requête DELETE sur le point de terminaison `/config/computedAttributes` et inclure l’identifiant de l’attribut calculé que vous souhaitez supprimer dans le chemin d’accès de la requête.

>[!NOTE]
>
>Soyez prudent lorsque vous supprimez un attribut calculé, car celui-ci peut être utilisé sur plusieurs schémas. Par ailleurs, l’opération DELETE ne peut pas être annulée.

**Format d’API**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Paramètre | Description |
|---|---|
| `{ATTRIBUTE_ID}` | L’identifiant de l’attribut calculé que vous souhaitez supprimer. |

**Requête**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Réponse**

Une requête de suppression réussie renvoie un état HTTP 200 (OK) et un corps de réponse vide. Pour confirmer que la suppression a réussi, vous pouvez effectuer une requête GET pour rechercher l’attribut calculé à l’aide de son identifiant. Si l’attribut a été supprimé, vous recevrez un état HTTP 404 (Not Found).

## Création d’une définition de segment référençant un attribut calculé

Adobe Experience Platform vous permet de créer des segments définissant un groupe d’attributs ou de comportements spécifiques à partir d’un groupe de profils. Une définition de segment inclut une expression qui encapsule une requête écrite dans PQL. Ces expressions peuvent également faire référence à des attributs calculés.

L’exemple suivant crée une définition de segment qui fait référence à un attribut calculé existant. Pour en savoir plus sur les définitions de segment et sur leur utilisation dans l’API Segmentation Service, reportez-vous à la section [guide d’entrée de l’API des définitions de segment](../../segmentation/api/segment-definitions.md).

Pour commencer, envoyez une requête de POST au `/segment/definitions` point de terminaison , fournissant l’attribut calculé dans le corps de la requête.

**Format d’API**

```http
POST /segment/definitions
```

**Requête**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "downloadedInLast7Days",
        "description": "Has product been downloaded in last 7 days?",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "ttlInDays": 30,
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "_{TENANT_ID}.downloadsLast7Days > 0",
            "meta": "m"
        },
        "dataGovernancePolicy": {
            "excludeOptOut": true
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
        }
    }'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Nom unique du segment, sous forme de chaîne. |
| `description` | Description lisible par l’utilisateur de la définition. |
| `schema.name` | Le schéma associé aux entités du segment. Se compose d’un champ `id` ou `name`. |
| `expression` | Objet contenant des champs contenant des informations sur la définition de segment. |
| `expression.type` | Indique le type d’expression. Actuellement, seul « PQL » est pris en charge. |
| `expression.format` | Indique la structure de l’expression en valeur. Actuellement, seul `pql/text` est pris en charge. |
| `expression.value` | Une expression PQL valide, dans cet exemple, inclut une référence à un attribut calculé existant. |

Pour plus d’informations sur les attributs de définition de schéma, reportez-vous aux exemples fournis dans la section [guide d’entrée de l’API des définitions de segment](../../segmentation/api/segment-definitions.md).

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la définition de segment que vous venez de créer. Pour en savoir plus sur les objets de réponse de définition de segment, reportez-vous à la section [guide d’entrée de l’API des définitions de segment](../../segmentation/api/segment-definitions.md).

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "segment-downloadedInLast7Days",
    "description": "Has product been downloaded in last 7 days?",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "_{TENANT_ID}.downloadsLast7Days > 0",
        "meta": "m"
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
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1602016581000,
    "updateEpoch": 1610609459,
    "updateTime": 1610609459000,
    "createEpoch": 1602016554,
    "_etag": "\"8b01611a-0000-0200-0000-5ffff3330000\"",
    "dependents": [
        "023d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [
    "103d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "type": "SegmentDefinition"
}
```

## Étapes suivantes

Maintenant que vous avez appris les bases des attributs calculés, vous êtes prêt à commencer à les définir pour votre organisation.
