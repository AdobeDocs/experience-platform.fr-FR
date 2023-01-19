---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre des schémas;schéma;schéma;schémas;schémas;schémas;créer
solution: Experience Platform
title: Création d’un schéma à l’aide de l’API Schema Registry
type: Tutorial
description: Ce tutoriel utilise l’API Schema Registry pour vous guider tout au long des étapes de composition d’un schéma à l’aide d’une classe standard.
exl-id: fa487a5f-d914-48f6-8d1b-001a60303f3d
source-git-commit: 3dffa9687f3429b970e8fceebd6864a5b61ead21
workflow-type: tm+mt
source-wordcount: '2588'
ht-degree: 40%

---

# Créez un schéma à l’aide du [!DNL Schema Registry] API

Le [!DNL Schema Registry] est utilisé pour accéder à la variable [!DNL Schema Library] dans Adobe Experience Platform. Le [!DNL Schema Library] contient les ressources mises à votre disposition par Adobe, [!DNL Experience Platform] partenaires et fournisseurs dont vous utilisez les applications. Le registre fournit une interface utilisateur et une API RESTful à partir de laquelle toutes les ressources disponibles de la bibliothèque sont accessibles.

Ce tutoriel utilise la méthode [!DNL Schema Registry] API pour vous guider dans les étapes de composition d’un schéma à l’aide d’une classe standard. Si vous préférez utiliser l’interface utilisateur dans [!DNL Experience Platform], la variable [Tutoriel de l’éditeur de schémas](create-schema-ui.md) fournit des instructions détaillées pour exécuter des actions similaires dans l’éditeur de schémas.

>[!NOTE]
>
>Si vous ingérez des données CSV dans Platform, vous pouvez [mapper ces données à un schéma XDM créé par des recommandations générées par l’IA](../../ingestion/tutorials/map-csv/recommendations.md) (actuellement en version bêta) sans avoir à créer manuellement le schéma.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM) System]](../home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
   * [Principes de base de la composition des schémas](../schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
* [[!DNL Sandboxes]](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des sandbox virtuelles qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Avant de commencer ce tutoriel, veuillez consulter le [guide de développement](../api/getting-started.md) pour trouver les informations importantes à connaître afin d’effectuer avec succès des appels vers l’API [!DNL Schema Registry] Cela inclut votre `{TENANT_ID}`, le concept de « conteneurs » et les en-têtes requis pour effectuer des requêtes (avec une attention particulière à l’en-tête et à ses valeurs possibles).`Accept`

Ce tutoriel passe en revue les étapes de la composition d’un schéma Loyalty Members qui décrit les données relatives aux membres d’un programme de fidélité dans la vente au détail. Avant de commencer, vous pouvez consulter avoir un aperçu de [l’intégralité du schéma Loyalty Members](#complete-schema) dans l’annexe.

## Composition d’un schéma avec une classe standard

Un schéma peut être considéré comme le plan directeur des données que vous souhaitez ingérer dans [!DNL Experience Platform]. Chaque schéma est composé d’une classe et de zéro ou plusieurs groupes de champs de schéma. En d’autres termes, il n’est pas nécessaire d’ajouter un groupe de champs pour définir un schéma, mais dans la plupart des cas, au moins un groupe de champs est utilisé.

### Attribution d’une classe

Le processus de composition du schéma commence par la sélection d’une classe. La classe définit les principaux aspects comportementaux des données (enregistrement ou série temporelle), ainsi que les champs minimaux requis pour décrire les données qui seront ingérées.

Le schéma que vous créez dans ce tutoriel utilise la variable [!DNL XDM Individual Profile] classe . [!DNL XDM Individual Profile] est une classe standard fournie par Adobe pour définir le comportement des enregistrements. Vous trouverez plus d’informations sur le comportement dans les [principes de base de la composition des schémas](../schema/composition.md).

Pour attribuer une classe, un appel API est effectué pour créer (POST) un nouveau schéma dans le conteneur du client. Cet appel inclut la classe que le schéma va implémenter. Chaque schéma ne peut mettre en œuvre qu’une seule classe.

**Format d’API**

```http
POST /tenant/schemas
```

**Requête**

La requête doit inclure un attribut `allOf` qui fait référence à la clé `$id` d’une classe. Cet attribut définit la « classe de base » que le schéma va mettre en œuvre. Dans cet exemple, la classe de base est la suivante : [!DNL XDM Individual Profile] classe . La clé `$id`[!DNL XDM Individual Profile] de la classe est utilisée comme valeur du champ `$ref` dans le tableau `allOf` ci-dessous.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "type": "object",
        "title": "Loyalty Members",
        "description": "Information for all members of the loyalty program",
        "allOf": [
            {
              "$ref": "https://ns.adobe.com/xdm/context/profile"
            }
        ]
      }'
```

**Réponse**

Une requête réussie renvoie un état de réponse HTTP 201 (Created) avec un corps de réponse qui contient les détails du nouveau schéma, y compris les clés `$id`, `meta:altIt`, et `version`. Ces valeurs sont en lecture seule et sont affectées par la variable [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/tenantId/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_tenantId.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673310304048,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "6d2ed8acd9c3b768a44de29e069fc6f71329d2550f708381d22fa8bf8c192366",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_tenantId"
}
```

### Recherche d’un schéma

Pour afficher votre nouveau schéma, effectuez une requête de recherche (GET) en utilisant la clé `meta:altId` ou l’URI `$id` encodé par URL pour le schéma.

**Format d’API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | Le `meta:altId` ou encodé URL `$id` du schéma que vous souhaitez rechercher. |

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F533ca5da28087c44344810891b0f03d9\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

**Réponse**

Le format de réponse dépend de la variable `Accept` en-tête envoyé avec la requête. Tentative d’expérimentation avec différentes `Accept` pour identifier celle qui répond le mieux à vos besoins.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.0",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673310304048,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "6d2ed8acd9c3b768a44de29e069fc6f71329d2550f708381d22fa8bf8c192366",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:allFieldAccess": true
}
```

### Ajouter un groupe de champs {#add-a-field-group}

Maintenant que le schéma Loyalty Members a été créé et confirmé, des groupes de champs peuvent y être ajoutés.

Différents groupes de champs standard sont disponibles, selon la classe de schéma sélectionnée. Chaque groupe de champs contient une `intendedToExtend` champ qui définit la ou les classes avec lesquelles ce groupe de champs est compatible.

Les groupes de champs définissent des concepts, tels que &quot;name&quot; ou &quot;address&quot;, qui peuvent être réutilisés dans n’importe quel schéma qui doit capturer les mêmes informations.

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | Le `meta:altId` ou encodé URL `$id` du schéma auquel vous ajoutez le groupe de champs. |

**Requête**

Cette requête met à jour le schéma Loyalty Members pour inclure les champs dans la variable [[!UICONTROL Détails démographiques] groupe de champs](../field-groups/profile/demographic-details.md) (`profile-person-details`).

En ajoutant la variable `profile-person-details` groupe de champs, le schéma Loyalty Members capture désormais des informations démographiques pour les membres du programme de fidélité, telles que leur prénom, leur nom et leur anniversaire.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-person-details"}}
      ]'
```

**Réponse**

La réponse affiche le nouveau groupe de champs ajouté dans la variable `meta:extends` et contient un `$ref` au groupe de champs de la `allOf` attribut.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.1",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673310912096,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "b480f28a35f356b237fc129e796074a3f33a7a67df273f6a8beaee1ec6465540",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:descriptorStatus": {
    "result": []
  }
}
```

### Ajouter d’autres groupes de champs

Les schémas Loyalty Members nécessitent deux autres groupes de champs standard, que vous pouvez ajouter en répétant les étapes à l’aide d’un autre groupe de champs.

>[!TIP]
>
>Il est utile de passer en revue tous les groupes de champs disponibles pour mieux connaître les champs inclus dans chacun d’eux. Vous pouvez répertorier (par GET) tous les groupes de champs disponibles pour une classe particulière en exécutant une requête sur chacun des conteneurs &quot;global&quot; et &quot;client&quot;, en ne renvoyant que les groupes de champs dont le champ &quot;meta:intendedToExtend&quot; correspond à la classe que vous utilisez. Dans ce cas, il s’agit de la variable [!DNL XDM Individual Profile] , donc la variable [!DNL XDM Individual Profile] `$id` est utilisé :
>
>
```http
>GET /global/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
>GET /tenant/fieldgroups?property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile
>```

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | Le `meta:altId` ou encodé URL `$id` du schéma que vous mettez à jour. |

**Requête**

Cette requête met à jour le schéma Loyalty Members pour inclure les champs dans les groupes de champs standard suivants :

* [[!UICONTROL Détails du contact personnel]](../field-groups/profile/personal-contact-details.md) (`profile-personal-details`) : Ajoute des informations de contact telles que l’adresse du domicile, l’adresse électronique et le téléphone personnel.
* [[!UICONTROL Détails de fidélité]](../field-groups/profile/loyalty-details.md) (`profile-loyalty-details`) : Ajoute des informations de contact telles que l’adresse du domicile, l’adresse électronique et le téléphone personnel.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"}},
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"}}
      ]'  
```

**Réponse**

La réponse affiche les groupes de champs nouvellement ajoutés dans la variable `meta:extends` et contient un `$ref` au groupe de champs de la `allOf` attribut.

Le schéma Loyalty Members doit maintenant contenir quatre `$ref` dans la variable `allOf` tableau : `profile`, `profile-person-details`, `profile-personal-details`, et `profile-loyalty-details` comme illustré ci-dessous.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.2",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673311559934,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "1de5ed1a07e3478719952f0a8c94d5e5390d5a9a998761adb4cf1989137fd6ea",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:descriptorStatus": {
    "result": []
  }
}
```

### Définir un nouveau groupe de champs

Lors de la [!UICONTROL Détails de fidélité] Le groupe de champs fournit des champs utiles liés à la fidélité au schéma. Il existe des champs de fidélité supplémentaires qui ne sont inclus dans aucun groupe de champs standard.

Pour ajouter ces champs, vous pouvez définir vos propres groupes de champs personnalisés au sein du `tenant` conteneur. Ces groupes de champs sont propres à votre organisation et ne sont ni visibles ni modifiables par quiconque en dehors de votre organisation.

Pour créer (POST) un groupe de champs, votre requête doit inclure une `meta:intendedToExtend` contenant le champ `$id` pour la ou les classes de base avec lesquelles le groupe de champs est compatible, ainsi que les propriétés que le groupe de champs va inclure.

Toutes les propriétés personnalisées doivent être imbriquées sous votre `TENANT_ID` pour éviter les collisions avec d’autres groupes de champs ou champs.

**Format d’API**

```http
POST /tenant/fieldgroups
```

**Requête**

Cette requête crée un groupe de champs doté d’un `loyaltyTier` contenant quatre champs spécifiques au programme de fidélité d’une entreprise : `id`, `effectiveDate`, `currentThreshold`, et `nextThreshold`.

```SHELL
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Loyalty Tier",
        "meta:intendedToExtend": [
          "https://ns.adobe.com/xdm/context/profile"
        ],
        "description": "Captures info about the current loyalty tier of a customer.",
        "definitions": {
          "loyaltyTier": {
            "properties": {
              "_{TENANT_ID}": {
                "type": "object",
                "properties": {
                  "loyaltyTier": {
                    "type": "object",
                    "properties": {
                      "id": {
                        "title": "Loyalty Tier Identifier",
                        "type": "string",
                        "description": "Loyalty Tier Identifier."
                      },
                      "effectiveDate": {
                        "title": "Effective Date",
                        "type": "string",
                        "format": "date-time",
                        "description": "Date the member joined their current loyalty tier."
                      },
                      "currentThreshold": {
                        "title": "Current Point Threshold",
                        "type": "integer",
                        "description": "The minimum number of loyalty points the member must maintain to remain in the current tier."
                      },
                      "nextThreshold": {
                        "title": "Next Point Threshold",
                        "type": "integer",
                        "description": "The number of loyalty points the member must accrue to graduate to the next tier."
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/loyaltyTier"
          }
        ]
      }'
```

**Réponse**

Une requête réussie renvoie un état de réponse HTTP 201 (Created) avec un corps de réponse contenant les détails du nouveau groupe de champs, y compris le `$id`, `meta:altIt`, et `version`. Ces valeurs sont en lecture seule et sont affectées par la variable [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Captures info about the current loyalty tier of a customer.",
  "definitions": {
    "loyaltyTier": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "loyaltyTier": {
              "type": "object",
              "properties": {
                "id": {
                  "title": "Loyalty Tier Identifier",
                  "type": "string",
                  "description": "Loyalty Tier Identifier.",
                  "meta:xdmType": "string"
                },
                "effectiveDate": {
                  "title": "Effective Date",
                  "type": "string",
                  "format": "date-time",
                  "description": "Date the member joined their current loyalty tier.",
                  "meta:xdmType": "date-time"
                },
                "currentThreshold": {
                  "title": "Current Point Threshold",
                  "type": "integer",
                  "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                  "meta:xdmType": "int"
                },
                "nextThreshold": {
                  "title": "Next Point Threshold",
                  "type": "integer",
                  "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                  "meta:xdmType": "int"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673313004645,
    "repo:lastModifiedDate": 1673313004645,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "98e5d48808f5a4d9655493777389568a2581cfce013351ab9e1595d82f698dd6",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

### Ajout du groupe de champs personnalisé au schéma

Vous pouvez maintenant suivre les mêmes étapes que pour [ajout d’un groupe de champs standard](#add-a-field-group) pour ajouter ce nouveau groupe de champs à votre schéma.

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | Le `meta:altId` ou encodé URL `$id` du schéma. |

**Requête**

Cette requête met à jour (PATCH) le schéma Loyalty Members pour inclure les champs dans le nouveau groupe de champs &quot;Loyalty Level&quot;.

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/allOf/-", "value":  {"$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"}}
      ]'
```

**Réponse**

Vous pouvez constater que le groupe de champs a bien été ajouté, car la réponse affiche maintenant le nouveau groupe de champs ajouté dans la variable `meta:extends` tableau et contenir un `$ref` au groupe de champs de la `allOf` attribut.

```JSON
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
    "meta:resourceType": "schemas",
    "version": "1.3",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Information for all members of the loyalty program",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "refs": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "imsOrg": "{ORG_ID}",
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1673310304048,
        "repo:lastModifiedDate": 1673313118938,
        "xdm:createdClientId": "{CLIENT_ID}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "xdm:createdUserId": "{USER_ID}",
        "xdm:lastModifiedUserId": "{USER_ID}",
        "eTag": "6559b197a04bb3fda5bc80bf383a260cfbe32539d528f0139c5750711eebfba2",
        "meta:globalLibVersion": "1.38.2"
    },
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:descriptorStatus": {
        "result": []
    }
}
```

### Affichage du schéma actuel

Vous pouvez désormais effectuer une requête de GET pour afficher le schéma actuel et voir comment les groupes de champs ajoutés ont contribué à la structure globale du schéma.

**Format d’API**

```http
GET /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | Le `meta:altId` ou encodé URL `$id` du schéma. |

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1'
```

**Réponse**

En utilisant l’en-tête `application/vnd.adobe.xed-full+json; version=1`, vous pouvez voir le schéma complet indiquant toutes les propriétés. `Accept` Ces propriétés sont les champs fournis par la classe et les groupes de champs qui ont été utilisés pour composer le schéma. Dans l’exemple de réponse ci-dessous, seuls les champs récemment ajoutés sont affichés pour l’espace. Vous pouvez consulter le schéma dans son intégralité, y compris toutes les propriétés et leurs attributs, dans l’[annexe](#appendix) à la fin de ce document.

Sous `"properties"`, vous pouvez voir la variable `_{TENANT_ID}` espace de noms créé lors de l’ajout du groupe de champs personnalisé. Dans cet espace de noms se trouve la variable `loyaltyTier` et les champs définis lors de la création du groupe de champs.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:resourceType": "mixins",
  "version": "1.0",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Captures info about the current loyalty tier of a customer.",
  "definitions": {
    "loyaltyTier": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "loyaltyTier": {
              "type": "object",
              "properties": {
                "id": {
                  "title": "Loyalty Tier Identifier",
                  "type": "string",
                  "description": "Loyalty Tier Identifier.",
                  "meta:xdmType": "string"
                },
                "effectiveDate": {
                  "title": "Effective Date",
                  "type": "string",
                  "format": "date-time",
                  "description": "Date the member joined their current loyalty tier.",
                  "meta:xdmType": "date-time"
                },
                "currentThreshold": {
                  "title": "Current Point Threshold",
                  "type": "integer",
                  "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
                  "meta:xdmType": "int"
                },
                "nextThreshold": {
                  "title": "Next Point Threshold",
                  "type": "integer",
                  "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
                  "meta:xdmType": "int"
                }
              },
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673313004645,
    "repo:lastModifiedDate": 1673313004645,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "98e5d48808f5a4d9655493777389568a2581cfce013351ab9e1595d82f698dd6",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

### Création d’un type de données

Le groupe de champs Niveau de fidélité que vous avez créé contient des propriétés spécifiques qui peuvent s’avérer utiles dans d’autres schémas. Par exemple, les données peuvent être ingérées dans le cadre d’un événement d’expérience ou utilisées par un schéma qui met en œuvre une autre classe. Dans ce cas, il est logique d’enregistrer la hiérarchie d’objets en tant que type de données afin de faciliter la réutilisation de la définition ailleurs.

Les types de données vous permettent de définir une hiérarchie d’objets une seule fois, et d’y faire référence dans un champ comme vous le feriez pour tout autre type scalaire.

En d’autres termes, les types de données permettent l’utilisation cohérente de structures à champs multiples, avec plus de flexibilité que les groupes de champs, car ils peuvent être inclus n’importe où dans un schéma en les ajoutant comme &quot;type&quot; d’un champ.

**Format d’API**

```http
POST /tenant/datatypes
```

**Requête**

La définition d’un type de données ne nécessite pas `meta:extends` ou `meta:intendedToExtend` Les champs et ne doivent pas être imbriqués sous votre ID de client pour éviter les collisions.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "title": "Loyalty Tier",
        "type": "object",
        "description": "Loyalty Tier data type",
        "definitions": {
          "loyaltyTier": {
            "type": "object",
            "properties": {
              "id": {
                "title": "Loyalty Tier Identifier",
                "type": "string",
                "description": "Loyalty Tier Identifier."
              },
              "effectiveDate": {
                "title": "Effective Date",
                "type": "string",
                "format": "date-time",
                "description": "Date the member joined their current loyalty tier."
              },
              "currentThreshold": {
                "title": "Current Point Threshold",
                "type": "integer",
                "description": "The minimum number of loyalty points the member must maintain to remain in the       current tier."
              },
              "nextThreshold": {
                "title": "Next Point Threshold",
                "type": "integer",
                "description": "The number of loyalty points the member must accrue to graduate to the next tier."
              }
            }
          }
        },
        "allOf": [
          {
            "$ref": "#/definitions/loyaltyTier"
          }
        ]
      }'
```

**Réponse**

Une requête réussie renvoie un état de réponse HTTP 201 (Created) avec un corps de réponse qui contient les détails du nouveau type de données, y compris les clés `$id`, `meta:altIt`, et `version`. Ces valeurs sont en lecture seule et sont affectées par la variable [!DNL Schema Registry].

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
  "meta:altId": "_{TENANT_ID}.datatypes.c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
  "meta:resourceType": "datatypes",
  "version": "1.0",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Loyalty Tier data type",
  "definitions": {
    "loyaltyTier": {
      "type": "object",
      "properties": {
        "id": {
          "title": "Loyalty Tier Identifier",
          "type": "string",
          "description": "Loyalty Tier Identifier.",
          "meta:xdmType": "string"
        },
        "effectiveDate": {
          "title": "Effective Date",
          "type": "string",
          "format": "date-time",
          "description": "Date the member joined their current loyalty tier.",
          "meta:xdmType": "date-time"
        },
        "currentThreshold": {
          "title": "Current Point Threshold",
          "type": "integer",
          "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
          "meta:xdmType": "int"
        },
        "nextThreshold": {
          "title": "Next Point Threshold",
          "type": "integer",
          "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
          "meta:xdmType": "int"
        }
      },
      "meta:xdmType": "object"
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673378256699,
    "repo:lastModifiedDate": 1673378256699,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "8afba84c0c9a68126a7a1389f8523a1112bdf4405badc6dcddbbb4a0e18f5cdb",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

Vous pouvez effectuer une requête de recherche (GET) à l’aide de l’URI `$id` encodé par URL pour afficher directement le nouveau type de données. Veillez à inclure `version` dans l’en-tête pour une requête de recherche.`Accept`

### Utilisation du type de données dans le schéma

Maintenant que le type de données Loyalty Level a été créé, vous pouvez mettre à jour (PATCH) la variable `loyaltyTier` dans le groupe de champs que vous avez créé pour référencer le type de données à la place des champs qui existaient auparavant.

**Format d’API**

```http
PATCH /tenant/fieldgroups/{FIELD_GROUP_ID}
```

| Paramètre | Description |
| --- | --- |
| `{FIELD_GROUP_ID}` | Le `meta:altId` ou encodé URL `$id` du groupe de champs à mettre à jour. |

**Requête**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups/_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "replace",
          "path": "/definitions/loyaltyTier/properties/_{TENANT_ID}/properties",
          "value": {
            "loyaltyTier": {
              "title": "Loyalty Tier",
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
              "description": "Loyalty tier info"
            }
          }
        }
      ]'
```

**Réponse**

La réponse comprend désormais une référence (`$ref`) au type de données dans la variable `loyaltyTier` au lieu des champs précédemment définis.

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:altId": "_{TENANT_ID}.mixins.9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
  "meta:resourceType": "mixins",
  "version": "1.1",
  "title": "Loyalty Tier",
  "type": "object",
  "description": "Captures info about the current loyalty tier of a customer.",
  "definitions": {
    "loyaltyTier": {
      "properties": {
        "_{TENANT_ID}": {
          "type": "object",
          "properties": {
            "loyaltyTier": {
              "title": "Loyalty Tier",
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb",
              "description": "Loyalty tier info",
              "type": "object",
              "meta:xdmType": "object"
            }
          },
          "meta:xdmType": "object"
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/loyaltyTier",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673313004645,
    "repo:lastModifiedDate": 1673378970276,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "4df8fa56d00991590364606bb2e219e1ea8f5717a51c0e6ae57ca956830b6a27",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:descriptorStatus": {
    "result": []
  }
}
```

Si vous effectuez une requête de GET pour rechercher le schéma maintenant, la variable `loyaltyTier` affiche la référence au type de données sous `meta:referencedFrom`:

```JSON
"_{TENANT_ID}": {
  "type": "object",
  "meta:xdmType": "object",
  "properties": {
    "loyaltyTier": {
      "title": "Loyalty Tier",
      "description": "Loyalty tier info",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "id": {
          "title": "Loyalty Tier Identifier",
          "type": "string",
          "description": "Loyalty Tier Identifier.",
          "meta:xdmType": "string"
        },
        "effectiveDate": {
          "title": "Effective Date",
          "type": "string",
          "format": "date-time",
          "description": "Date the member joined their current loyalty tier.",
          "meta:xdmType": "date-time"
        },
        "currentThreshold": {
          "title": "Current Point Threshold",
          "type": "integer",
          "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
          "meta:xdmType": "int"
        },
        "nextThreshold": {
          "title": "Next Point Threshold",
          "type": "integer",
          "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
          "meta:xdmType": "int"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
    }
  }
}
```

### Définition d’un descripteur d’identité

Les schémas sont utilisés pour ingérer des données dans [!DNL Experience Platform]. Ces données sont finalement utilisées par plusieurs services pour créer une vue unique et unifiée d’un individu. Pour faciliter ce processus, les champs clés peuvent être désignés comme champs « Identity » et, lors de l’ingestion de données, les données de ces champs sont intégrées au « Graphique d’identité » pour cette personne. Les données du graphique peuvent ensuite être consultées par [[!DNL Real-Time Customer Profile]](../../profile/home.md)[!DNL Experience Platform] et d’autres services afin de fournir une vue d’ensemble de chaque client individuel.

Les champs généralement désignés comme champs &quot;Identité&quot; sont les suivants : adresse email, numéro de téléphone, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr), ID de gestion de la relation client ou d’autres champs d’identifiant uniques. Tenez compte des identifiants uniques propres à votre organisation, dans la mesure où ils peuvent aussi représenter de bons champs d’identité.

Les descripteurs d’identité signalent que la variable `sourceProperty` de `sourceSchema` est un identifiant unique qui doit être considéré comme une identité.

Pour plus d’informations sur l’utilisation des descripteurs, consultez le [guide de développement du registre des schémas](../api/getting-started.md).

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante définit un descripteur d’identité sur la variable `personalEmail.address` pour le schéma Loyalty Members. Ceci indique : [!DNL Experience Platform] pour utiliser l’adresse électronique du membre du programme de fidélité comme identifiant afin de faciliter la collecte d’informations sur l’individu. Cet appel définit également ce champ comme identité Principale du schéma en définissant `xdm:isPrimary` to `true`, qui est une exigence de [activation du schéma à utiliser dans Real-time Customer Profile](#profile).

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_{TENANT_ID}/loyalty/loyaltyId",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

>[!NOTE]
>
>Vous pouvez répertorier les valeurs &quot;xdm:namespace&quot; disponibles ou en créer de nouvelles, à l’aide de la fonction [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service). La valeur de « xdm:property » peut être soit « xdm:code », soit « xdm:id », selon la clé « xdm:namespace » utilisée.

**Réponse**

Une réponse réussie renvoie un état de réponse HTTP 201 (Created) avec un corps de réponse qui contient les détails du nouveau descripteur, y compris la clé `@id`. Le `@id` est un champ en lecture seule attribué par la variable [!DNL Schema Registry] et sert à référencer le descripteur dans l’API.

```JSON
{
  "@id": "719a4391897c097786efbaa6d4262bb928a1cd88540344c6",
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "imsOrg": "{ORG_ID}",
  "version": "1",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": true,
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production"
}
```

## Activer le schéma à utiliser dans [!DNL Real-Time Customer Profile] {#profile}

Une fois qu’un descripteur d’identité Principal est appliqué au schéma, vous pouvez activer le schéma Loyalty Members pour l’utiliser par [!DNL Real-Time Customer Profile] en ajoutant une `union` vers la balise `meta:immutableTags` attribut.

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation des vues d’union, consultez la section sur [syndicats](../api/unions.md) dans le [!DNL Schema Registry] guide de développement.

### Ajouter un `union` tag

Pour qu’un schéma soit inclus dans la vue d’union fusionnée, la variable `union` doit être ajoutée à la balise `meta:immutableTags` du schéma. Pour ce faire, vous devez envoyer une requête de PATCH pour mettre à jour le schéma et ajouter une `meta:immutableTags` tableau avec la valeur de `union`.

**Format d’API**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Paramètre | Description |
| --- | --- |
| `{SCHEMA_ID}` | Le `meta:altId` ou encodé URL `$id` du schéma que vous activez pour Profile. |

**Requête**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**Réponse**

La réponse indique que l’opération a été effectuée correctement, et que le schéma contient maintenant un attribut de niveau supérieur, `meta:immutableTags`, qui est un tableau contenant la valeur « union ».

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.4",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "allOf": [
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
      "type": "object",
      "meta:xdmType": "object"
    },
    {
      "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "refs": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673380280074,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "c590ccc7a293040d85c2b7d93276480ef4b4aa9a4fcd6991f50fbb47f58bced2",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:immutableTags": [
    "union"
  ],
  "meta:descriptorStatus": {
    "result": []
  }
}
```

### Liste des schémas dans une union

Vous avez maintenant ajouté votre schéma à l’événement [!DNL XDM Individual Profile] union. Afin d’obtenir une liste de tous les schémas qui font partie d’une même union, vous pouvez effectuer une requête GET en utilisant les paramètres de requête pour filtrer la réponse.

En utilisant le paramètre de requête `property`, vous pouvez spécifier que seuls les schémas contenant un champ `meta:immutableTags` qui a une `meta:class` égale à la clé `$id` de la classe doivent être renvoyés.[!DNL XDM Individual Profile]

**Format d’API**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

**Requête**

L’exemple de requête ci-dessous renvoie tous les schémas qui font partie du [!DNL XDM Individual Profile] union.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse est une liste filtrée de schémas, contenant uniquement ceux qui répondent aux deux exigences. N’oubliez pas que lorsque vous utilisez plusieurs paramètres de requête, une relation ET est présumée. Le format de la réponse de liste dépend de la variable `Accept` en-tête envoyé dans la requête.

```JSON
{
  "results": [
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d29a200b5deb6cfb55d3b865ef627f33",
      "meta:altId": "_{TENANT_ID}.schemas.d29a200b5deb6cfb55d3b865ef627f33",
      "version": "1.2",
      "title": "Profile Schema"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/5d70026f5522fc60b3c81f6523b83c86",
      "meta:altId": "_{TENANT_ID}.schemas.5d70026f5522fc60b3c81f6523b83c86",
      "version": "1.3",
      "title": "CRM Onboarding"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/653e53eb04341d09453c9b6a5fb43d1b4ca9526ec274856d",
      "meta:altId": "_{TENANT_ID}.schemas.653e53eb04341d09453c9b6a5fb43d1b4ca9526ec274856d",
      "version": "1.1",
      "title": "Profile consents"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
      "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
      "version": "1.4",
      "title": "Loyalty Members"
    }
  ],
  "_page": {
    "orderby": "updated",
    "next": null,
    "count": 4
  },
  "_links": {
    "next": null,
    "global_schemas": {
      "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
    }
  }
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez réussi à composer un schéma à l’aide des groupes de champs standard et d’un groupe de champs que vous avez défini. Vous pouvez maintenant utiliser ce schéma pour créer un ensemble de données et ingérer des données d’enregistrement dans Adobe Experience Platform.

L’intégralité du schéma Loyalty Members, tel que créé tout au long de ce tutoriel, est disponible dans l’annexe suivante. En examinant le schéma, vous pouvez voir comment les groupes de champs contribuent à la structure globale et quels champs sont disponibles pour l’ingestion des données.

Une fois que vous avez créé plusieurs schémas, vous pouvez définir leurs relations en utilisant des descripteurs de relations. Pour plus d’informations, consultez le tutoriel sur [la définition d’une relation entre deux schémas](relationship-api.md). Pour obtenir des exemples détaillés sur la manière d’effectuer toutes les opérations (GET, POST, PUT, PATCH et DELETE) dans le registre, veuillez vous référer au [guide de développement du registre des schémas](../api/getting-started.md) lorsque vous utilisez l’API.

## Annexe {#appendix}

Les informations suivantes complètent le tutoriel sur l’API.

## Intégralité du schéma Loyalty Members {#complete-schema}

Dans ce tutoriel, un schéma est composé pour décrire les membres d’un programme de fidélité dans la vente au détail.

Le schéma met en oeuvre le [!DNL XDM Individual Profile] et combine plusieurs groupes de champs. Il capture des informations sur les membres du programme de fidélité à l’aide de la norme [!DNL Demographic Details], [!UICONTROL Détails du contact personnel], et [!UICONTROL Détails de fidélité] groupes de champs, ainsi que par le biais d’un groupe de champs Niveau de fidélité personnalisé défini pendant le tutoriel.

Vous trouverez ci-dessous le schéma Loyalty Members au format JSON :

+++Affichage du schéma complet

```JSON
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:altId": "_{TENANT_ID}.schemas.ee56b80adc7e03b8214e135a28538fe83c7f85bf87f565b3",
  "meta:resourceType": "schemas",
  "version": "1.4",
  "title": "Loyalty Members",
  "type": "object",
  "description": "Information for all members of the loyalty program",
  "properties": {
    "_{TENANT_ID}": {
      "type": "object",
      "properties": {
        "loyaltyTier": {
          "title": "Loyalty Tier",
          "description": "Loyalty tier info",
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "id": {
              "title": "Loyalty Tier Identifier",
              "type": "string",
              "description": "Loyalty Tier Identifier.",
              "meta:xdmType": "string"
            },
            "effectiveDate": {
              "title": "Effective Date",
              "type": "string",
              "format": "date-time",
              "description": "Date the member joined their current loyalty tier.",
              "meta:xdmType": "date-time"
            },
            "currentThreshold": {
              "title": "Current Point Threshold",
              "type": "integer",
              "description": "The minimum number of loyalty points the member must maintain to remain in the current tier.",
              "meta:xdmType": "int"
            },
            "nextThreshold": {
              "title": "Next Point Threshold",
              "type": "integer",
              "description": "The number of loyalty points the member must accrue to graduate to the next tier.",
              "meta:xdmType": "int"
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/c069d13ebfaaa5980d988e7694d794b37b1784fe11d754cb"
        }
      },
      "meta:xdmType": "object"
    },
    "_id": {
      "title": "Identifier",
      "type": "string",
      "format": "uri-reference",
      "description": "A unique identifier for the record.",
      "meta:xdmType": "string",
      "meta:xdmField": "@id"
    },
    "_repo": {
      "properties": {
        "createDate": {
          "type": "string",
          "format": "date-time",
          "meta:immutable": true,
          "meta:usereditable": false,
          "examples": [
            "2004-10-23T12:00:00-06:00"
          ],
          "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
          "meta:xdmType": "date-time",
          "meta:xdmField": "repo:createDate"
        },
        "modifyDate": {
          "type": "string",
          "format": "date-time",
          "meta:usereditable": false,
          "examples": [
            "2004-10-23T12:00:00-06:00"
          ],
          "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
          "meta:xdmType": "date-time",
          "meta:xdmField": "repo:modifyDate"
        }
      },
      "type": "object",
      "meta:xdmType": "object",
      "meta:xedConverted": true
    },
    "billingAddress": {
      "title": "Billing Address",
      "description": "Billing postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
        },
        "stateProvince": {
          "title": "State or province",
          "type": "string",
          "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
          "examples": [
            "US-CA",
            "DE-BB",
            "JP-13"
          ],
          "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:billingAddress"
    },
    "createdByBatchID": {
      "title": "Created by batch identifier",
      "type": "string",
      "format": "uri-reference",
      "description": "The dataset files in Catalog which has been originating the creation of the record.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:createdByBatchID"
    },
    "faxPhone": {
      "title": "Fax Phone",
      "description": "Fax phone number.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "countryCode": {
          "title": "Country Calling Code",
          "type": "string",
          "description": "Country calling code (CC) as defined by E.164.",
          "minLength": 1,
          "maxLength": 3,
          "pattern": "^[0-9]{1,3}?$",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "extension": {
          "title": "Extension",
          "type": "string",
          "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:extension"
        },
        "number": {
          "title": "Number",
          "type": "string",
          "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:number"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the phone number.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "validity": {
          "title": "Validity",
          "type": "string",
          "description": "A level of technical correctness of the phone number.",
          "meta:enum": {
            "consistent": "Consistent",
            "inconsistent": "Inconsistent",
            "incomplete": "Incomplete",
            "successfullyUsed": "Successfully used"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:validity"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
      "meta:xdmField": "xdm:faxPhone"
    },
    "homeAddress": {
      "title": "Home Address",
      "description": "A home postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
        },
        "stateProvince": {
          "title": "State or province",
          "type": "string",
          "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
          "examples": [
            "US-CA",
            "DE-BB",
            "JP-13"
          ],
          "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:homeAddress"
    },
    "homePhone": {
      "title": "Home Phone",
      "description": "Home phone number.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "countryCode": {
          "title": "Country Calling Code",
          "type": "string",
          "description": "Country calling code (CC) as defined by E.164.",
          "minLength": 1,
          "maxLength": 3,
          "pattern": "^[0-9]{1,3}?$",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "extension": {
          "title": "Extension",
          "type": "string",
          "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:extension"
        },
        "number": {
          "title": "Number",
          "type": "string",
          "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:number"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the phone number.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "validity": {
          "title": "Validity",
          "type": "string",
          "description": "A level of technical correctness of the phone number.",
          "meta:enum": {
            "consistent": "Consistent",
            "inconsistent": "Inconsistent",
            "incomplete": "Incomplete",
            "successfullyUsed": "Successfully used"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:validity"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
      "meta:xdmField": "xdm:homePhone"
    },
    "loyalty": {
      "type": "object",
      "description": "Captures details related to the customer's loyalty rewards.",
      "properties": {
        "joinDate": {
          "title": "Program Join Date",
          "type": "string",
          "format": "date-time",
          "description": "Date which the visitor registered for the loyalty program.",
          "meta:xdmType": "date-time",
          "meta:xdmField": "xdm:joinDate"
        },
        "loyaltyID": {
          "title": "Program ID",
          "type": "array",
          "items": {
            "type": "string",
            "meta:xdmType": "string"
          },
          "description": "The loyalty program ID(s) associated with a specific user, if they are enrolled in the client's loyalty program.",
          "meta:xdmType": "array",
          "meta:xdmField": "xdm:loyaltyID"
        },
        "points": {
          "title": "Program Points Balance",
          "type": "number",
          "description": "Current balance of the loyalty points/awards in a visitor's loyalty account.",
          "meta:xdmType": "number",
          "meta:xdmField": "xdm:points"
        },
        "pointsExpiration": {
          "title": "Points Expiration",
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "pointsExpirationDate": {
                "type": "string",
                "format": "date-time",
                "description": "Date on which the given portion of the loyalty points expire.",
                "meta:xdmType": "date-time",
                "meta:xdmField": "xdm:pointsExpirationDate"
              },
              "pointsExpiring": {
                "title": "Points Expiring",
                "type": "number",
                "description": "Point balance expiring as of the associated expiration date.",
                "meta:xdmType": "number",
                "meta:xdmField": "xdm:pointsExpiring"
              }
            },
            "meta:xdmType": "object"
          },
          "meta:xdmType": "array",
          "meta:xdmField": "xdm:pointsExpiration"
        },
        "pointsRedeemed": {
          "title": "Points Redeemed",
          "type": "number",
          "description": "Amount of points applied toward a purchase or otherwise redeemed.",
          "meta:xdmType": "number",
          "meta:xdmField": "xdm:pointsRedeemed"
        },
        "program": {
          "title": "Program Name",
          "type": "string",
          "description": "This should define the loyalty progam in which a visitor is enrolled.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:program"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "Captures the visitor's loyalty progam status, such as active, disabled, or suspended.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "tier": {
          "title": "Tier",
          "type": "string",
          "description": "Captures the loyalty progam tier in which a visitor is enrolled.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:tier"
        },
        "upgradeDate": {
          "title": "Program Name",
          "type": "string",
          "description": "Date which the customer was upgraded to the next tier level.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:upgradeDate"
        }
      },
      "meta:xdmType": "object",
      "meta:xdmField": "xdm:loyalty"
    },
    "mailingAddress": {
      "title": "Mailing Address",
      "description": "Mailing postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
        },
        "stateProvince": {
          "title": "State or province",
          "type": "string",
          "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
          "examples": [
            "US-CA",
            "DE-BB",
            "JP-13"
          ],
          "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:mailingAddress"
    },
    "mobilePhone": {
      "title": "Mobile Phone",
      "description": "Mobile phone number.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "countryCode": {
          "title": "Country Calling Code",
          "type": "string",
          "description": "Country calling code (CC) as defined by E.164.",
          "minLength": 1,
          "maxLength": 3,
          "pattern": "^[0-9]{1,3}?$",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "extension": {
          "title": "Extension",
          "type": "string",
          "description": "The internal dialing number used to call from a private exchange, operator, or switchboard.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:extension"
        },
        "number": {
          "title": "Number",
          "type": "string",
          "description": "The phone number. Note the phone number is a string and may include meaningful characters such as brackets '()', hyphens '-', or characters to indicate sub-dialing identifiers like extensions 'x' for example,  1-353(0)18391111 or +613 9403600x1234.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:number"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary phone number indicator. Unlike address or email address, there can be multiple primary phone numbers; one per communication channel. The communication channel is defined by the type: `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, and `fax`.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the phone number.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "validity": {
          "title": "Validity",
          "type": "string",
          "description": "A level of technical correctness of the phone number.",
          "meta:enum": {
            "consistent": "Consistent",
            "inconsistent": "Inconsistent",
            "incomplete": "Incomplete",
            "successfullyUsed": "Successfully used"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:validity"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
      "meta:xdmField": "xdm:mobilePhone"
    },
    "modifiedByBatchID": {
      "title": "Modified by batch identifier",
      "type": "string",
      "format": "uri-reference",
      "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:modifiedByBatchID"
    },
    "person": {
      "title": "Person",
      "description": "An individual actor, contact, or owner.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "birthDate": {
          "title": "Birth date(YYYY-MM-DD)",
          "type": "string",
          "format": "date",
          "description": "The full date a person was born.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:birthDate"
        },
        "birthDayAndMonth": {
          "title": "Birth date (MM-DD)",
          "type": "string",
          "pattern": "[0-1][0-9]-[0-9][0-9]",
          "description": "The day and month a person was born, in the format MM-DD. This field should be used when the day and month of a person's birth is known, but not the year.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:birthDayAndMonth"
        },
        "birthYear": {
          "title": "Birth year",
          "type": "integer",
          "description": "The year a person was born including the century, for example, 1983.  This field should be used when only the person's age is known, not the full birth date.",
          "minimum": 1,
          "maximum": 32767,
          "meta:xdmType": "short",
          "meta:xdmField": "xdm:birthYear"
        },
        "gender": {
          "title": "Gender",
          "type": "string",
          "enum": [
            "male",
            "female",
            "not_specified",
            "non_specific"
          ],
          "meta:enum": {
            "male": "Male",
            "female": "Female",
            "not_specified": "Not Specified",
            "non_specific": "Non-specific"
          },
          "description": "Gender identity of the person.\n",
          "default": "not_specified",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:gender"
        },
        "maritalStatus": {
          "title": "Marital Status",
          "type": "string",
          "enum": [
            "married",
            "single",
            "divorced",
            "widowed",
            "not_specified"
          ],
          "meta:enum": {
            "married": "Married",
            "single": "Single",
            "divorced": "Divorced",
            "widowed": "Widowed",
            "not_specified": "Not Specified"
          },
          "description": "Describes a person's relationship with a significant other.",
          "default": "not_specified",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:maritalStatus"
        },
        "name": {
          "title": "Full name",
          "description": "The person's full name.",
          "type": "object",
          "meta:xdmType": "object",
          "properties": {
            "courtesyTitle": {
              "title": "Courtesy title",
              "type": "string",
              "description": "Normally an abbreviation of a persons title, honorific, or salutation. The `courtesyTitle` is used in front of full or last name in opening texts. For example, Mr. Miss. or Dr.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:courtesyTitle"
            },
            "firstName": {
              "title": "First name",
              "type": "string",
              "description": "The first segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the preferred personal or given name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:firstName"
            },
            "fullName": {
              "title": "Full name",
              "type": "string",
              "description": "The full name of the person, in writing order most commonly accepted in the language of the name.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:fullName"
            },
            "lastName": {
              "title": "Last name",
              "type": "string",
              "description": "The last segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the inherited family name, surname, patronymic, or matronymic name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:lastName"
            },
            "middleName": {
              "title": "Middle name",
              "type": "string",
              "description": "Middle, alternative, or additional names supplied between the first name and last name.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:middleName"
            },
            "suffix": {
              "title": "Suffix",
              "type": "string",
              "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc.",
              "meta:xdmType": "string",
              "meta:xdmField": "xdm:suffix"
            }
          },
          "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person-name",
          "meta:xdmField": "xdm:name"
        },
        "nationality": {
          "title": "Nationality",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The legal relationship between a person and their state represented using the ISO 3166-1 Alpha-2 code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:nationality"
        },
        "taxId": {
          "title": "Tax ID",
          "type": "string",
          "description": "The Tax / Fiscal ID of the person, e.g. the TIN in the US or the CIF/NIF in Spain.",
          "meta:status": "deprecated",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:taxId"
        },
        "type": {
          "title": "Type",
          "type": "string",
          "description": "The type of individual in different business contexts like B2C.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:type"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/person",
      "meta:xdmField": "xdm:person"
    },
    "personID": {
      "title": "Person ID",
      "description": "Unique identifier of Person/Profile fragment.",
      "type": "string",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:personID"
    },
    "personalEmail": {
      "title": "Personal Email",
      "description": "A personal email address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "address": {
          "title": "Address",
          "type": "string",
          "format": "email",
          "description": "The technical address, for example, 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:address",
          "minLength": 1
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Additional display information that maybe available, for example, Microsoft Outlook rich address controls display 'John Smith smithjr@company.uk', 'John Smith' part is data that would be placed in the label.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary email indicator. A profile can have only one `primary` email address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the email address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "type": {
          "title": "Type",
          "type": "string",
          "description": "The way the account relates to the person for example 'work' or 'personal'.",
          "meta:enum": {
            "unknown": "Unknown",
            "personal": "Personal",
            "work": "Work",
            "education": "Education"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:type"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
      "meta:xdmField": "xdm:personalEmail",
      "required": [
        "address"
      ]
    },
    "repositoryCreatedBy": {
      "title": "Created by user identifier",
      "type": "string",
      "description": "User ID of who created the record.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:repositoryCreatedBy"
    },
    "repositoryLastModifiedBy": {
      "title": "Modified by user identifier",
      "type": "string",
      "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
      "meta:xdmType": "string",
      "meta:xdmField": "xdm:repositoryLastModifiedBy"
    },
    "shippingAddress": {
      "title": "Shipping Address",
      "description": "Shipping postal address.",
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
        "_id": {
          "title": "Coordinates ID",
          "type": "string",
          "format": "uri-reference",
          "description": "The unique identifier of the coordinates.",
          "meta:xdmType": "string",
          "meta:xdmField": "@id"
        },
        "_repo": {
          "properties": {
            "createDate": {
              "type": "string",
              "format": "date-time",
              "meta:immutable": true,
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was created in the repository, such as when an asset file is first uploaded or a directory is created by the server as the parent of a new asset. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:createDate"
            },
            "modifyDate": {
              "type": "string",
              "format": "date-time",
              "meta:usereditable": false,
              "examples": [
                "2004-10-23T12:00:00-06:00"
              ],
              "description": "The server date and time when the resource was last modified in the repository, such as when a new version of an asset is uploaded or a directory's child resource is added or removed. The date time property should conform to ISO 8601 standard. An example form is \"2004-10-23T12:00:00-06:00\".",
              "meta:xdmType": "date-time",
              "meta:xdmField": "repo:modifyDate"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "_schema": {
          "properties": {
            "description": {
              "title": "Description",
              "type": "string",
              "description": "A description of what the coordinates identify.",
              "meta:xdmType": "string",
              "meta:xdmField": "schema:description"
            },
            "elevation": {
              "title": "Elevation",
              "type": "number",
              "description": "The specific elevation of the defined coordinate. The value conforms to the [WGS84](http://gisgeography.com/wgs84-world-geodetic-system/) datum and is measured in meters.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:elevation"
            },
            "latitude": {
              "title": "Latitude",
              "type": "number",
              "minimum": -90,
              "maximum": 90,
              "description": "The signed vertical coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:latitude"
            },
            "longitude": {
              "title": "Longitude",
              "type": "number",
              "minimum": -180,
              "maximum": 180,
              "description": "The signed horizontal coordinate of a geographic point.",
              "meta:xdmType": "number",
              "meta:xdmField": "schema:longitude"
            }
          },
          "type": "object",
          "meta:xdmType": "object",
          "meta:xedConverted": true
        },
        "city": {
          "title": "City",
          "type": "string",
          "description": "The name of the city.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:city"
        },
        "country": {
          "title": "Country",
          "type": "string",
          "description": "The name of the government-administered territory. Other than `xdm:countryCode`, this is a free-form field that can have the country name in any language.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:country"
        },
        "countryCode": {
          "title": "Country code",
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "The two-character [ISO 3166-1 alpha-2](https://datahub.io/core/country-list) code for the country.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:countryCode"
        },
        "createdByBatchID": {
          "title": "Created by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The dataset files in Catalog which has been originating the creation of the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:createdByBatchID"
        },
        "dmaID": {
          "title": "Designated market area",
          "type": "integer",
          "description": "The Nielsen media research designated market area.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:dmaID"
        },
        "label": {
          "title": "Label",
          "type": "string",
          "description": "Free form name of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:label"
        },
        "lastVerifiedDate": {
          "title": "Last verified date",
          "type": "string",
          "format": "date",
          "description": "The date that the address was last verified as still associated to the person.",
          "meta:xdmType": "date",
          "meta:xdmField": "xdm:lastVerifiedDate"
        },
        "modifiedByBatchID": {
          "title": "Modified by batch identifier",
          "type": "string",
          "format": "uri-reference",
          "description": "The last dataset files in Catalog which has modified the record. At creation time, `modifiedByBatchID` is set as `createdByBatchID`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:modifiedByBatchID"
        },
        "msaID": {
          "title": "Metropolitan statistical area",
          "type": "integer",
          "description": "The metropolitan statistical area in the United States where the observation occurred.",
          "meta:xdmType": "int",
          "meta:xdmField": "xdm:msaID"
        },
        "postOfficeBox": {
          "title": "Post office box",
          "type": "string",
          "description": "Post office box of the address.",
          "maxLength": 20,
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postOfficeBox"
        },
        "postalCode": {
          "title": "Postal code",
          "type": "string",
          "description": "The postal code of the location. Postal codes are not available for all countries. In some countries, this will only contain part of the postal code.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:postalCode"
        },
        "primary": {
          "title": "Primary",
          "type": "boolean",
          "description": "Primary address indicator. A profile can have only one `primary` address at a given point of time.",
          "meta:xdmType": "boolean",
          "meta:xdmField": "xdm:primary"
        },
        "region": {
          "title": "Region",
          "type": "string",
          "description": "The region, county, or district portion of the address.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:region"
        },
        "repositoryCreatedBy": {
          "title": "Created by user identifier",
          "type": "string",
          "description": "User ID of who created the record.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryCreatedBy"
        },
        "repositoryLastModifiedBy": {
          "title": "Modified by user identifier",
          "type": "string",
          "description": "User ID of who last modified the record. At creation time, `modifiedByUser` is set as `createdByUser`.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:repositoryLastModifiedBy"
        },
        "state": {
          "title": "State",
          "type": "string",
          "description": "The name of the State. This is a free-form field.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:state"
        },
        "stateProvince": {
          "title": "State or province",
          "type": "string",
          "description": "The state, or province portion of the observation. The format follows the [ISO 3166-2 (country and subdivision)][http://www.unece.org/cefact/locode/subdivisions.html] standard.",
          "examples": [
            "US-CA",
            "DE-BB",
            "JP-13"
          ],
          "pattern": "([A-Z]{2}-[A-Z0-9]{1,3}|)",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:stateProvince"
        },
        "status": {
          "title": "Status",
          "type": "string",
          "description": "An indication as to the ability to use the address.",
          "default": "active",
          "meta:enum": {
            "active": "Active",
            "incomplete": "Incomplete",
            "pending_verification": "Pending verification",
            "blacklisted": "Blacklisted",
            "blocked": "Blocked"
          },
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:status"
        },
        "statusReason": {
          "title": "Status reason",
          "type": "string",
          "description": "A description of the current status.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:statusReason"
        },
        "street1": {
          "title": "Street 1",
          "type": "string",
          "description": "Primary street level information, apartment number, street number, and street name.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street1"
        },
        "street2": {
          "title": "Street 2",
          "type": "string",
          "description": "Optional street information second line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street2"
        },
        "street3": {
          "title": "Street 3",
          "type": "string",
          "description": "Optional street information third line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street3"
        },
        "street4": {
          "title": "Street 4",
          "type": "string",
          "description": "Optional street information fourth line.",
          "meta:xdmType": "string",
          "meta:xdmField": "xdm:street4"
        }
      },
      "meta:referencedFrom": "https://ns.adobe.com/xdm/common/address",
      "meta:xdmField": "xdm:shippingAddress"
    }
  },
  "required": [
    "personalEmail"
  ],
  "imsOrg": "{ORG_ID}",
  "meta:extensible": false,
  "meta:abstract": false,
  "meta:extends": [
    "https://ns.adobe.com/xdm/context/profile-person-details",
    "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details",
    "https://ns.adobe.com/xdm/context/profile-personal-details",
    "https://ns.adobe.com/xdm/common/auditable",
    "https://ns.adobe.com/xdm/data/record",
    "https://ns.adobe.com/xdm/context/profile",
    "https://ns.adobe.com/{TENANT_ID}/mixins/9068fd4ea2abf813f4fd2fc9c8b413ae453ff0efc7636691"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1673310304048,
    "repo:lastModifiedDate": 1673380280074,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "c590ccc7a293040d85c2b7d93276480ef4b4aa9a4fcd6991f50fbb47f58bced2",
    "meta:globalLibVersion": "1.38.2"
  },
  "meta:class": "https://ns.adobe.com/xdm/context/profile",
  "meta:containerId": "tenant",
  "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
  "meta:sandboxType": "production",
  "meta:tenantNamespace": "_{TENANT_ID}",
  "meta:immutableTags": [
    "union"
  ],
  "meta:allFieldAccess": true
}
```

+++
