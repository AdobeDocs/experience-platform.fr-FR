---
title: Point de terminaison de l’API des modules d’outils Sandbox
description: Le point de terminaison /packages de l’API Sandbox Tooling vous permet de gérer les packages par programmation dans Adobe Experience Platform.
exl-id: 46efee26-d897-4941-baf4-d5ca0b8311f0
source-git-commit: 47e4616e5465ec97512647b9280f461c6971aa42
workflow-type: tm+mt
source-wordcount: '2547'
ht-degree: 10%

---

# Point de terminaison des packages

L’outil Sandbox vous permet de sélectionner différents artefacts (également appelés objets) et de les exporter dans un package. Un module peut se composer d’un ou de plusieurs artefacts (tels que des jeux de données ou des schémas). Tous les artefacts inclus dans un package doivent provenir du même environnement de test.

Le point d’entrée `/packages` de l’API des outils d’environnement de test vous permet de gérer par programmation les modules de votre organisation, y compris de publier un module et d’importer un module dans un environnement de test.

## Création d’un package {#create}

Vous pouvez créer un module à plusieurs artefacts en envoyant une requête de POST au point de terminaison `/packages` tout en fournissant des valeurs pour le nom et le type de module de votre module.

**Format d’API**

```http
POST /packages/
```

**Requête**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "name": "acme",
      "description": "Acme Business Group",
      "packageType": "PARTIAL",    
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      },
      "expiry": "2023-05-20T20:05:10Z",
      "artifacts": [
        {
          "id": "27115daa-c92b-4f17-a077-d65ffeb0c525",
          "type": "PROFILE_SEGMENT",
          "title": "Acme Profile Segment"
        }      
      ]
  }'
```

| Propriété | Description | Type | Obligatoire |
| --- | --- | --- | --- |
| `name` | Le nom de votre package. | Chaîne | Oui |
| `description` | Description pour fournir plus d’informations sur votre module. | Chaîne | Non |
| `packageType` | Le type de package est **PARTIAL** pour indiquer que vous incluez des artefacts spécifiques dans un package. | Chaîne | OUI |
| `sourceSandbox` | Environnement de test source du package. | Objet | Non |
| `expiry` | Horodatage qui définit la date d’expiration du package. La valeur par défaut est de 90 jours à compter de la date de création. Le champ d’expiration de la réponse sera l’heure UTC de l’époque. | Chaîne (format UTC Timestamp) | Non |
| `artifacts` | Liste des artefacts à exporter dans le package. La valeur `artifacts` doit être **null** ou **empty**, lorsque `packageType` est `FULL`. | Tableau | Non |

**Réponse**

Une réponse réussie renvoie le module que vous venez de créer. La réponse comprend l’identifiant de module correspondant, ainsi que des informations sur son état, son expiration et la liste des artefacts.

```json
{
    "id": "209f886b00444eac9bb5836fe32e7681",
    "version": 0,
    "createdDate": 1684475012105,
    "modifiedDate": 1684475012105,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "requestId": "devxa54a6b56d04f46119d9e3cc006fcc1cb",
    "userId": "platform_exim",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "cjm-mr",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1684613110000,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## Mettre à jour un package {#update}

Vous pouvez mettre à jour un package en envoyant une requête de PUT au point de terminaison `/packages`.

### Ajout d’artefacts à un module {#add-artifacts}

Pour ajouter des artefacts à un package, vous devez fournir un `id` et inclure **ADD** pour le `action`.

**Format d’API**

```http
PUT /packages/
```

**Requête**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "ADD",
      "expiry": "2023-05-20T20:05:10Z", 
      "artifacts": [
        {
         "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
         "type": "JOURNEY"
        }      
      ]
  }'
```

| Propriété | Description | Type | Obligatoire |
| --- | --- | --- | --- |
| `id` | Identifiant du package à mettre à jour. | Chaîne | Oui |
| `action` | Pour ajouter des artefacts dans le package, la valeur de l’action doit être **ADD**. Cette action est prise en charge uniquement pour les types de packages **PARTIAL**. | Chaîne | Oui |
| `artifacts` | Liste des artefacts à ajouter au module. Le package ne sera pas modifié si la liste est **null** ou **empty**. Les artefacts sont dédupliqués avant d’être ajoutés au module. Consultez le tableau ci-dessous pour obtenir la liste complète des artefacts pris en charge. | Tableau | Non |
| `expiry` | Horodatage qui définit la date d’expiration du package. La valeur par défaut est de 90 jours à compter de l’appel de l’API PUT si l’expiration n’est pas spécifiée dans la payload. Le champ d’expiration de la réponse sera l’heure UTC de l’époque. | Chaîne (format UTC Timestamp) | Non |

Les types d’artefacts suivants sont actuellement pris en charge.

| Artefact | Platform | Objet | Flux partiel | Environnement de test complet |
| --- | --- | --- | --- | --- |
| `JOURNEY` | Adobe Journey Optimizer | Parcours | Oui | Non |
| `ID_NAMESPACE` | Plateforme de données clients | Identités | Oui | Oui |
| `REGISTRY_DATATYPE` | Plateforme de données clients | Type de données | Oui | Oui |
| `REGISTRY_CLASS` | Plateforme de données clients | Classe | Oui | Oui |
| `REGISTRY_MIXIN` | Plateforme de données clients | Groupe de champs | Oui | Oui |
| `REGISTRY_SCHEMA` | Plateforme de données clients | Schémas | Oui | Oui |
| `CATALOG_DATASET` | Plateforme de données clients | Jeux de données | Oui | Oui |
| `DULE_CONSENT_POLICY` | Plateforme de données clients | Stratégies de consentement et de gouvernance | Oui | Oui |
| `PROFILE_SEGMENT` | Plateforme de données clients | Audiences | Oui | Oui |
| `FLOW` | Plateforme de données clients | Flux de données de sources | Oui | Oui |

**Réponse**

Une réponse réussie renvoie votre package mis à jour. La réponse comprend l’identifiant de module correspondant, ainsi que des informations sur son état, son expiration et la liste des artefacts.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 4,
    "createdDate": 1684235842000,
    "modifiedDate": 1684475861366,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1692251861352,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### Suppression d’artefacts d’un module {#delete-artifacts}

Pour supprimer des artefacts d’un package, vous devez fournir un `id` et inclure **DELETE** pour le `action`.

**Format d’API**

```http
PUT /packages/
```

**Requête**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "DELETE",
      "artifacts": [
        {
          "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
          "type": "JOURNEY"
        }      
      ]
  }'
```

| Propriété | Description | Type | Obligatoire |
| --- | --- | --- | --- |
| `id` | Identifiant du package à mettre à jour. | Chaîne | Oui |
| `action` | Pour supprimer des artefacts d’un package, la valeur de l’action doit être **DELETE**. Cette action est prise en charge uniquement pour les types de packages **PARTIAL**. | Chaîne | Oui |
| `artifacts` | Liste des artefacts à supprimer du package. Le package ne sera pas modifié si la liste est **null** ou **empty**. | Tableau | Non |

**Réponse**

Une réponse réussie renvoie votre package mis à jour. La réponse comprend l’identifiant de module correspondant, ainsi que des informations sur son état, son expiration et la liste des artefacts.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 5,
    "createdDate": 1684235842000,
    "modifiedDate": 1684478830416,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },      
    "packageType": "PARTIAL",
    "expiry": 1692254830403,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### Mise à jour des champs de métadonnées dans un package {#update-metadata}

>[!NOTE]
>
>L’action **UPDATE** est utilisée pour mettre à jour les champs de métadonnées du package et **ne peut pas** être utilisée pour ajouter/supprimer des artefacts à un package.

Pour mettre à jour les champs de métadonnées dans un package, vous devez fournir un `id` et inclure **UPDATE** pour le `action`.

**Format d’API**

```http
PUT /packages/
```

**Requête**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "UPDATE",
      "name": "acme",
      "description": "Acme Business Group",  
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      }
  }'
```

| Propriété | Description | Type | Obligatoire |
| --- | --- | --- | --- |
| `id` | Identifiant du package à mettre à jour. | Chaîne | Oui |
| `action` | Pour mettre à jour les champs de métadonnées dans un package, la valeur de l’action doit être **UPDATE**. Cette action est prise en charge uniquement pour les types de packages **PARTIAL**. | Chaîne | Oui |
| `name` | Nom mis à jour du module. Les noms de modules en double ne sont pas autorisés. | Tableau | Oui |
| `sourceSandbox` | L’environnement de test Source doit appartenir à la même organisation que celle spécifiée dans l’en-tête de la requête. | Objet | Oui |

**Réponse**

Une réponse réussie renvoie votre package mis à jour. La réponse comprend l’identifiant de module correspondant, ainsi que des informations sur sa description, son état, son expiration et la liste des artefacts.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 6,
    "createdDate": 1684235842000,
    "modifiedDate": 1684479094129,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",    
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "packageType": "PARTIAL",
    "expiry": 1692255094127,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## Suppression d’un package {#delete}

Pour supprimer un package, envoyez une requête de DELETE au point de terminaison `/packages` et spécifiez l’identifiant du package que vous souhaitez supprimer.

**Format d’API**

```http
DELETE /packages/{PACKAGE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{PACKAGE_ID}` | L’identifiant du module que vous souhaitez supprimer. |

**Requête**

La requête suivante supprime le package avec l’ID {PACKAGE_ID}.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie une raison qui indique que l’ID de module a été supprimé.

```json
{
    "reason": "Package d30e0424a37b46ada6a5cf37f47a86ff deleted"
}
```

## Publish d’un package {#publish}

Pour permettre l’importation d’un package dans un environnement de test, vous devez le publier. Effectuez une requête de GET au point de terminaison `/packages` tout en spécifiant l’identifiant du module que vous souhaitez publier.

**Format d’API**

```http
GET /packages/{PACKAGE_ID}/export
```

| Paramètre | Description |
| --- | --- |
| `{PACKAGE_ID}` | L’identifiant du module que vous souhaitez publier. |

**Requête**

La requête suivante publie le package avec l’ID {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

| Propriété | Description | Type | Obligatoire |
| --- | --- | --- | --- |
| `expiryPeriod` | Cette période spécifiée par l’utilisateur définit la date d’expiration du module (en jours) à partir du moment où le module a été publié. Cette valeur ne doit pas être négative.<br> Si aucune valeur n’est spécifiée, la valeur par défaut est calculée à 90 (jours) à partir de la date de publication. | Nombre entier | Non |

**Réponse**

Une réponse réussie renvoie le module publié.

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285",
    "jobId": "18abab44e25f40c284a4bd6e8f52fd29"
}
```

## Recherche d’un module {#look-up-package}

Vous pouvez rechercher un package individuel en envoyant une requête GET au point de terminaison `/packages` qui inclut l’identifiant correspondant du package dans le chemin d’accès de la requête.

**Format d’API**

```http
GET /packages/{PACKAGE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{PACKAGE_ID}` | L’identifiant du module que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère des informations pour {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie les détails de l’ID de module interrogé. La réponse comprend le nom, la description, la date de publication et la date d’expiration, l’environnement de test source du module, ainsi qu’une liste d’artefacts.

```json
{
    "id": "8f585fad94d042cd82dbcba594108a41",
    "version": 2,
    "createdDate": 1685597784000,
    "modifiedDate": 1685597810000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
    "packageType": "PARTIAL",
    "expiry": 1693373810000,
    "publishDate": 1685597810000,
    "status": "PUBLISHED",
    "artifactsList": [
        {
            "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ],
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    }
}
```

## Lister des packages {#list-packages}

Vous pouvez répertorier tous les modules de votre organisation en envoyant une requête GET au point de terminaison `/packages`.

**Format d’API**

```http
GET /packages/?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs pour filtrer les résultats. Pour plus d’informations, consultez la section sur les [paramètres de requête](./appendix.md) . |

**Requête**

La requête suivante récupère les informations des modules en fonction de {QUERY_PARAMS}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/?property=status==DRAFT,PUBLISHED&property=createdDate>=2023-05-11T18:29:59.999Z&property=createdDate<=2023-05-16T18:29:59.999Z&start=0&orderby=-createdDate&limit=20 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie une liste des modules appartenant à votre organisation, y compris des détails tels que le nom, l’état, l’expiration et la liste des artefacts.

```json
{
    "totalElements": 109,
    "currentPage": 0,
    "totalPages": 6,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "8f585fad94d042cd82dbcba594108a41",
            "version": 2,
            "createdDate": 1685597784000,
            "modifiedDate": 1685597810000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "c875b077162b40409c1327b16da99c1b",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693373810000,
            "publishDate": 1685597810000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                },
                {
                    "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        },
        {
            "id": "0d7e427ce4cb4dc1b78e30ef61b125c1",
            "version": 2,
            "createdDate": 1685555213000,
            "modifiedDate": 1685555275000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "7d7d8bbe3c7c4a8ea701cc5e42c57aeb",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693331275000,
            "publishDate": 1685555275000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "626a9669a9f5b818db270e95",
                    "type": "CATALOG_DATASET",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        }
    ]
}
```

## Importer un package {#import}

Ce point de terminaison est utilisé pour récupérer les objets en conflit dans l’environnement de test cible spécifié. Les objets en conflit représentent des objets similaires déjà présents dans l’environnement de test cible.

**Format d’API**

```http
GET /packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName
```

| Paramètre | Description |
| --- | --- |
| `{PACKAGE_ID}` | L’identifiant du module que vous souhaitez rechercher. |

**Requête**

La requête suivante importe le {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Les conflits sont renvoyés dans la réponse. La réponse affiche le package d’origine plus le fragment `alternatives` sous la forme d’un tableau trié par classement.

+++Affichage de la réponse

```json
[
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
            "type": "REGISTRY_SCHEMA",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/176f33f6a8ff6542de1256f8dc01cce4be1b3a68fd5f5bc5",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686403052050"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/1b37c3403e4e12c7aa46ea9dfe380a9f2b72d4da9db62b46",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686218766627"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_SCHEMA::https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
    },
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
            "type": "REGISTRY_CLASS",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/1dd81d61cdaa89a89382d0a424db77494475bd1db3105feb",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686564843736"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/classes/2511fb5396a630b2cd3d5d9e9b69d42ce66a4289db8ac917",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686408152916"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_CLASS::https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
    },
    {
        "artifact": {
            "id": "4d4c874ec3344d64bf8b3160e60ac78b",
            "type": "MAPPING_SET",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: 4d4c874ec3344d64bf8b3160e60ac78b"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "6b49c959d77c48e9904f7616fe2e7848",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "7b363da9e6704afb9716f57193d5246f",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "93ca0b4f437c4eaf9f1986408679e965",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::MAPPING_SET::4d4c874ec3344d64bf8b3160e60ac78b"
    }
]
```

+++

## Envoyer un import {#submit-import}

>[!NOTE]
>
>La résolution des conflits implique que l’artefact alternatif existe déjà dans l’environnement de test cible.

Vous pouvez soumettre un import pour un package une fois que vous avez examiné les conflits et fourni des substitutions en effectuant une requête de POST sur le point de terminaison `/packages`. Le résultat est fourni sous la forme d’un payload, qui lance la tâche d’importation pour l’environnement de test de destination, comme indiqué dans le payload.

La charge utile accepte également le nom et la description de la tâche d’importation spécifiés par l’utilisateur. Si le nom et la description spécifiés par l’utilisateur ne sont pas disponibles, le nom et la description du module sont utilisés pour le nom et la description de la tâche.

**Format d’API**

```http
POST /packages/import
```

**Requête**

La requête suivante récupère les packages à importer. La payload est une carte de substitutions où, si une entrée existe, la clé est le `artifactId` fourni par le package et l’alternative est la valeur. Si la carte ou la charge utile est **vide**, aucune substitution n’est effectuée.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/import/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
       "id": "09484a599f5f4a5faa43986643964615",
       "name": "acme",
       "description": "Acme Business Group",
       "destinationSandbox": {
         "name": "cjm-mr",
         "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
     },
     "alternatives": {
       "https://ns.adobe.com/cjmstage/schemas/ac33bbd22eb4ad6656e1c7e12e9f520261fb39fd28a902a9": {
         "id": "https://ns.adobe.com/cjmstage/schemas/a3b935344685afad4e52c753161cf673ec23d4fb1b3e9ce",
         "type": "REGISTRY_SCHEMA"
       }
     }
  }'
```

| Propriété | Description | Type | Obligatoire |
| --- | --- | --- | --- |
| `alternatives` | `alternatives` représente le mappage des artefacts sandbox source aux artefacts sandbox cible existants. Comme elles sont déjà présentes, la tâche d’importation évite de créer ces artefacts dans l’environnement de test cible. | Chaîne | Non |

**Réponse**

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "destinationSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285",
    "jobId": "18abab44e25f40c284a4bd6e8f52fd29"
}
```

## Liste de tous les objets dépendants {#dependent-objects}

Répertorier tous les objets dépendants pour les objets exportés dans un package en effectuant une requête de POST sur le point de terminaison `/packages` tout en spécifiant l’identifiant du package.

**Format d’API**

```http
POST /packages/{PACKAGE_ID}/children
```

| Paramètre | Description |
| --- | --- |
| `{PACKAGE_ID}` | L’identifiant du package. |

**Requête**

La requête suivante répertorie tous les objets dépendants pour le {PACKAGE_ID}.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/children \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'[
      {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "type": "REGISTRY_SCHEMA"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "type": "REGISTRY_CLASS"
      }
  ]'
```

**Réponse**

Une réponse réussie renvoie une liste d’enfants pour les objets.

```json
[
    {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "title": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
                "type": "REGISTRY_SCHEMA"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
        "type": "REGISTRY_SCHEMA",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
                "type": "REGISTRY_CLASS"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
        "type": "REGISTRY_CLASS",
        "children": []
    }
]
```

## Vérification des autorisations basées sur les rôles pour importer tous les artefacts de package {#role-based-permissions}

Vous pouvez vérifier si vous disposez des autorisations nécessaires pour importer des artefacts de package en envoyant une requête GET au point de terminaison `/packages` tout en spécifiant l’identifiant du package et le nom de l’environnement de test cible.

**Format d’API**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| Paramètre | Description |
| --- | --- |
| `{PACKAGE_ID}` | L’identifiant du package que vous souhaitez importer. |

**Requête**

La requête suivante vérifie vos autorisations pour {PACKAGE_ID} et l’environnement de test.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/preflight/{PACKAGE_ID}?targetSandbox=<sandbox_name> \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie des autorisations de ressources pour l’environnement de test cible, y compris une liste des autorisations requises, des autorisations manquantes, un type d’artefact et une décision sur l’autorisation de la création.

+++Affichage de la réponse

```json
{
  "packageID": "b7bda68eb1214c86824f1d7204616e51",
  "targetSandboxName": "acme-sandbox",
  "permissionResponse": [
    {
      "artifactID": "4aca57b6-8b83-450b-a460-e8a07ca79a44",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "Schema",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "Segment",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Composition",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Query",
            "resourcePermissions": [
              "write"
            ]
          },
          {
            "palmResourceType": "SegmentDashboard",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": []
      },
      "artifactType": "PROFILE_SEGMENT",
      "creationAllowed": true
    },
    {
      "artifactID": "36bb82bc-a00d-4d6b-a598-227d43e027c1",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": [
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "artifactType": "PROFILE_MERGE",
      "creationAllowed": false
    }
  ]
}
```

+++

## Liste des traitements d&#39;export/d&#39;import {#list-jobs}

Vous pouvez répertorier les tâches d’exportation/d’importation actuelles en effectuant une requête de GET sur le point de terminaison `/packages`.

**Format d’API**

```http
GET /packages/jobs?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{QUERY_PARAMS}` | Paramètres de requête facultatifs pour filtrer les résultats. Pour plus d’informations, consultez la section sur les [paramètres de requête](./appendix.md) . |

**Requête**

La requête suivante répertorie toutes les tâches d’importation réussies.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/jobs?property=requestType==IMPORT&property=jobStatus==SUCCESS&orderby=createdDate&start=0&limit=5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie renvoie toutes les tâches d’importation réussies.

```json
{
    "totalElements": 42,
    "currentPage": 0,
    "totalPages": 9,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "3c1b92cf47a246d7bfbe6fd507c5d543",
            "name": "acme",
            "updated": 1685973675401,
            "created": 1685973675401,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "ead59d21405f4184a94dd786a1bf040d",
            "name": "acme1",
            "updated": 1685986367198,
            "created": 1685986367198,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "85ddaa3c2f6c475088167cde7a9d4326",
            "name": "acme2",
            "updated": 1686147692568,
            "created": 1686147692568,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "c49a4fcb31954cbd828ece1da096c8f5",
            "name": "acme3",
            "updated": 1686148007586,
            "created": 1686148007586,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "a3669315baed4cf2af49bf9ce90b8158",
            "name": "acme4",
            "updated": 1686148651910,
            "created": 1686148651910,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        }
    ]
}
```

## Partage de modules dans toutes les organisations {#org-linking}

Le point d’entrée `/handshake` de l’API d’outils de test vous permet de collaborer avec d’autres organisations pour partager des modules.

### Envoi d’une demande de partage {#send-request}

Envoyez une demande à une organisation partenaire cible pour le partage de l’approbation en envoyant une demande de POST au point de terminaison `/handshake/bulkCreate`. Cela est nécessaire avant de pouvoir partager des modules privés.

**Format d’API**

```http
POST /handshake/bulkCreate
```

**Requête**

La requête suivante déclenche l’approbation du partage entre une organisation partenaire cible et l’organisation source.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/handshake/bulkCreate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "targetIMSOrgIds":["acme@AdobeOrg"],
      "sourceIMSDetails":{
        "id":"acme@AdobeOrg",
        "name":"acme_org"
      } 
  }' 
```

| Propriété | Description | Type | Obligatoire |
| --- | --- | --- | --- |
| `targetIMSOrgIds` | Liste des organisations cibles auxquelles envoyer la demande de partage. | Tableau | Oui |
| `sourceIMSDetails` | Informations détaillées sur l’organisation source. | Objet | Oui |

**Réponse**

Une réponse réussie renvoie des détails sur votre demande de partage.

```json
{
    "successfulRequests": {
        "acme@AdobeOrg": {
            "id": "{ID}",
            "version": 0,
            "createdDate": 1724938816798,
            "modifiedDate": 1724938816798,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va6",
            "sourceIMSOrgName": "{SOURCE_NAME}",
            "status": "APPROVAL_PENDING",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{ORG_ID}",
            "statusHistory": "[{\"actionTakenBy\":\"acme@98ff67fa661fdf6549420b.e\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724938816885}]",
            "linkingId": "{LINKIND_ID}"
        }
    },
    "failedRequests": {}
}
```

### Valider les demandes de partage reçues {#approve-requests}

Approuvez les demandes de partage provenant d’organisations partenaires cibles en envoyant une demande de POST au point de terminaison `/handshake/action`. Après approbation, les organisations partenaires sources peuvent partager des modules privés.

**Format d’API**

```http
POST /handshake/action
```

**Demandes**

La requête suivante approuve une demande de partage d’une organisation partenaire cible.

```shell
curl -X POST  \
  https://platform.adobe.io/data/foundation/exim/handshake/action \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "linkingID":"{LINKING_ID}",
      "status":"APPROVED",
      "reason":"Done",
      "targetIMSOrgDetails":{
          "id":"acme@AdobeOrg",
          "name":"acme",
          "region":"va7"
      }
  }'
```

| Propriété | Description | Type | Obligatoire |
| --- | --- | --- | --- |
| `linkingID` | ID de la demande de partage à laquelle vous répondez. | Chaîne | Oui |
| `status` | L’action effectuée sur la demande de partage. Les valeurs possibles sont `APPROVED` ou `REJECTED`. | Chaîne | Oui |
| `reason` | La raison pour laquelle l’action est entreprise. | Chaîne | Oui |
| `targetIMSOrgDetails` | Détails sur l’organisation cible où la valeur de l’identifiant doit être l’ **ID** de l’organisation cible, la valeur de nom doit être le **NAME** de l’organisation cible et la valeur de région doit être l’organisation cible **REGION**. | Objet | Oui |

**Réponse**

Une réponse réussie renvoie des détails sur la demande de partage approuvée.

```json
{
    "id": "{ID}",
    "version": 1,
    "createdDate": 1726737474000,
    "modifiedDate": 1726737541731,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "sourceRegion": "va7",
    "targetRegion": "va7",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetOrgName": "{TARGET_ORG}",
    "status": "APPROVED",
    "createdByName": "{CREATED_BY}",
    "modifiedByIMSOrgId": "{MODIFIED_BY}",
    "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"acme@AdobeOrg\",\"action\":\"INITIATED\",\"actionTimeStamp\":1726737474450,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":null,\"actionTakenByImsOrgID\":\"745F37C35E4B776E0A49421B@AdobeOrg\",\"action\":\"APPROVED\",\"actionTimeStamp\":1726737541818,\"reason\":\"Done\"}]",
    "linkingId": "{LINKING_ID}"
}
```

### Liste des demandes de partage sortantes/entrantes {#outgoing-and-incoming-requests}

Listez les requêtes de partage sortantes et entrantes en effectuant une requête GET sur le point de terminaison `handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING`.

**Format d’API**

```http
GET handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING
```

| Paramètre | Valeurs acceptées/par défaut |
| --- | --- |
| `property` | Spécifie la propriété à filtrer, par exemple l’état. Les valeurs possibles pour l’état sont : `APPROVED`, `REJECTED` et `IN_PROGRESS`. |
| `start` | La valeur par défaut de start est `0`. |
| `limit` | La valeur par défaut de limit est `20`. |
| `orderBy` | Trie les enregistrements par ordre croissant ou décroissant. |
| `requestType` | Accepte `INCOMING` ou `OUTGOING`. |

**Requête**

La requête suivante renvoie une liste de toutes les requêtes de partage sortantes et entrantes.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id:{ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**Réponse**

Une réponse réussie renvoie une liste des demandes de partage sortantes et entrantes, ainsi que leurs détails.

```json
{
    "totalElements": 1,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "version": 1,
            "createdDate": 1724929446000,
            "modifiedDate": 1724929617000,
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va7",
            "targetRegion": "va6",
             "sourceOrgName": "{SOURCE_ORG}",
            "targetOrgName": "{TARGET_ORG}",
            "status": "APPROVED",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{MODIFIED_BY}",
            "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724929442467,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"APPROVED\",\"actionTimeStamp\":1724929617531,\"reason\":\"Done\"}]",
            "linkingId": "{LINKING_ID}"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

## Transférer les packages

Utilisez le point d’entrée `/transfer` de l’API de l’outil de test pour récupérer et créer de nouvelles demandes de partage de package.

### Nouvelle demande de partage {#share-request}

Récupérez le package d’une organisation source publiée et partagez-le avec une organisation cible en envoyant une requête de POST au point de terminaison `/transfer` tout en fournissant l’ID de package et l’ID de l’organisation cible.

**Format d’API**

```http
POST /transfer
```

**Requête**

La requête suivante récupère un package d’organisations source et le partage avec une organisation cible.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "packageId": "{PACKAGE_ID}",
      "targets": [
          {
              "imsOrgId": "{TARGET_IMS_ORG}"
          }
      ]
  }'
```

| Propriété | Description | Type | Obligatoire |
| --- | --- | --- | --- |
| `packageId` | Identifiant du module que vous souhaitez partager. | Chaîne | Oui |
| `targets` | Liste des organisations avec lesquelles partager des modules. | Tableau | Oui |

**Réponse**

Une réponse réussie renvoie les détails du module demandé et son état de partage.

```json
[
    {
        "id": "{ID}",
        "version": 0,
        "createdDate": 1726480559313,
        "modifiedDate": 1726480559313,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceIMSOrgId": "{ORG_ID}",
        "targetIMSOrgId": "{TARGET_ID}",
        "packageId": "{PACKAGE_ID}",
        "status": "PENDING",
        "initiatedBy": "acme@3ec9197a65a86f34494221.e",
        "requestType": "PRIVATE"
    }
]
```

### Récupération d’une demande de partage par identifiant {#fetch-transfer-by-id}

Récupérez les détails d’une requête de partage en effectuant une requête de GET sur le point de terminaison `/transfer/{TRANSFER_ID}` tout en fournissant l’ID de transfert.

**Format d’API**

```http
GET /transfer/{TRANSFER_ID}
```

| Paramètre | Description |
| --- | --- |
| `{TRANSFER_ID}` | L’identifiant du transfert que vous souhaitez récupérer. |

**Requête**

La requête suivante récupère un transfert avec l’identifiant {TRANSFER_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/0c843180a64c445ca1beece339abc04b \
  -H 'x-api-key: {API__KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Réponse**

Une réponse de succès renvoie les détails d’une requête de partage.

```json
{
    "id": "{ID}",
    "sourceIMSOrgId": "{ORG_ID}",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetIMSOrgId": "{TARGET_ID}",
    "targetOrgName": "{TARGET_ORG}",
    "packageId": "{PACKAGE_ID}",
    "packageName": "{PACKAGE_NAME}",
    "status": "COMPLETED",
    "initiatedBy": "{INITIATED_BY}",
    "createdDate": 1724442856000,
    "requestType": "PRIVATE"
}
```

### Récupérer la liste de partage {#transfers-list}

Récupérez une liste de requêtes de transfert en effectuant une requête de GET sur le point de terminaison `/transfer/list?{QUERY_PARAMETERS}`, en modifiant les paramètres de requête selon les besoins.

**Format d’API**

```http
GET `/transfer/list?{QUERY_PARAMETERS}`
```

| Paramètre | Valeurs acceptées/par défaut |
| --- | --- |
| `property` | Spécifie la propriété à filtrer, par exemple l’état. Les valeurs possibles pour l’état sont : `COMPLETED`, `PENDING`, `IN_PROGRESS`, `FAILED`. |
| `start` | La valeur par défaut de start est `0`. |
| `limit` | La valeur par défaut de limit est `20`. |
| `orderBy` | L’ordre accepte uniquement le champ `createdDate`. |

**Requête**

La requête suivante récupère une liste de requêtes de transfert à partir des paramètres de recherche fournis.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status==COMPLETED&start=0&limit=2&orderBy=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**Réponse**

Une réponse réussie renvoie une liste de toutes les requêtes de transfert à partir des paramètres de recherche fournis.

```json
{
    "totalElements": 43,
    "currentPage": 0,
    "totalPages": 22,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726129077000,
            "createdDate": 1726129062000,
            "requestType": "PRIVATE"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726066046000,
            "createdDate": 1726065936000,
            "requestType": "PRIVATE"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

### Mise à jour de la disponibilité des packages du privé au public {#update-availability}

Remplacez un module de privé à public en effectuant une requête de GET sur le point de terminaison `/packages/update`. Par défaut, un package est créé avec une disponibilité privée.

**Format d’API**

```http
PUT `/packages/update`
```

**Requête**

La requête suivante modifie la disponibilité des packages du privé au public.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
      "id":"{ID}",
      "action":"UPDATE",
      "packageVisibility":"PUBLIC"
  }'
```

| Propriété | Description | Type | Obligatoire |
| --- | --- | --- | --- |
| `id` | Identifiant du package à mettre à jour. | Chaîne | Oui |
| `action` | Pour mettre à jour la visibilité sur public, la valeur de l’action doit être **UPDATE**. | Chaîne | Oui |
| `packageVisbility` | Pour mettre à jour la visibilité, la valeur de packageVisibility doit être **PUBLIC**. | Chaîne | Oui |

**Réponse**

Une réponse réussie renvoie les détails d’un package et sa visibilité.

```json
{
    "id": "{ID}",
    "version": 7,
    "createdDate": 1729624618000,
    "modifiedDate": 1729658596340,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "name": "acme",
    "imsOrgId": "{ORG_ID}",
    "packageType": "PARTIAL",
    "expiry": 1737434596325,
    "status": "PUBLISH_FAILED",
    "packageVisibility": "PUBLIC",
    "artifactsList": [
        {
            "id": "{ID}",
            "type": "PROFILE_SEGMENT",
            "found": false,
            "count": 0,
            "title": "Acme Profile Segment"
        }
    ],
    "schemaMapping": {},
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    }
}
```

### Demande d’importation d’un package public {#pull-public-package}

Importez un package d’une organisation source avec disponibilité publique en effectuant une requête de POST sur le point de terminaison `/transfer/pullRequest`.

**Format d’API**

```http
POST /transfer/pullRequest
```

**Requête**

La requête suivante importera un package et le mettra à disposition du public.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/pullRequest \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "imsOrgId": "{ORG_ID}",
      "packageId": "{PACKAGE_ID}"
  }'
```

| Propriété | Description | Type | Obligatoire |
| --- | --- | --- | --- |
| `imsOrgId` | ID de l’organisation source du package. | Chaîne | Oui |
| `packageId` | Identifiant du package à importer. | Chaîne | Oui |

**Réponse**

Une réponse réussie renvoie les détails du package public importé.

```json
{
    "id": "{ID}",
    "version": 0,
    "createdDate": 1729658890425,
    "modifiedDate": 1729658890425,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "packageId": "{PACKAGE_ID}",
    "status": "PENDING",
    "initiatedBy": "{INITIATED_BY}",
    "pipelineMessageId": "{MESSAGE_ID}",
    "requestType": "PUBLIC"
}
```

### Liste des packages publics {#list-public-packages}

Récupérez une liste de packages avec visibilité publique en effectuant une requête GET sur le point de terminaison `/transfer/list?{QUERY_PARAMS}`.

**Format d’API**

```http
GET /transfer/list?{QUERY_PARAMS}
```

| Paramètre | Valeurs acceptées/par défaut |
| --- | --- |
| `property` | Spécifie la propriété à filtrer, par exemple l’état. Les valeurs possibles pour l’état sont : `COMPLETED` et `FAILED`. |
| `start` | La valeur par défaut de start est `0`. |
| `limit` | La valeur par défaut de limit est `20`. |
| `orderBy` | L’ordre accepte uniquement le champ `createdDate`. |
| `requestType` | Accepte `PUBLIC` ou `PRIVATE`. |

**Requête**

La requête suivante récupère une liste de packages avec une disponibilité publique.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status%3D%3DCOMPLETED%2CFAILED&requestType=PUBLIC&orderby=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**Réponse**

Une réponse réussie renvoie une liste de modules publics et leurs détails.

+++Affichage de la réponse

```json
{
    "totalElements": 14,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359318000,
            "createdDate": 1729359316000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359284000,
            "createdDate": 1729359283000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Test Private Flow Final",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284462000,
            "createdDate": 1729275962000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOUCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Fest",
            "status": "FAILED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284104000,
            "createdDate": 1729253854000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284667000,
            "createdDate": 1729253421000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284957000,
            "createdDate": 1729253143000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284562000,
            "createdDate": 1729252975000,
            "requestType": "PUBLIC"
        },
        {
               "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Private Package Test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284262000,
            "createdDate": 1729229755000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Demo Package 1016",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284784000,
            "createdDate": 1729208888000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284934000,
            "createdDate": 1729153097000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284912000,
            "createdDate": 1729153043000,
            "requestType": "PUBLIC"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

+++

## Copie de la payload du module (#package-payload)

Vous pouvez copier la charge utile d’un package public en effectuant une requête de GET sur le point de terminaison `/packages/payload` qui inclut l’identifiant correspondant du package dans le chemin d’accès de la requête.

**Format d’API**

```http
GET /packages/payload/{PACKAGE_ID}
```

| Paramètre | Description |
| --- | --- |
| `{PACKAGE_ID}` | L’identifiant du module que vous souhaitez copier. |

**Requête**

La requête suivante récupère la charge utile d’un module avec l’identifiant {PACKAGE_ID}.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/payload/{PACKAGE_ID} \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

| Propriété | Description | Type | Obligatoire |
| --- | --- | --- | --- |
| `imsOrdId` | ID de l’organisation à laquelle le module appartient. | Chaîne | Oui |
| `packageId` | L’identifiant du module qui charge utile que vous demandez. | Chaîne | Oui |

**Réponse**

Une réponse réussie renvoie la charge utile du module.

```json
{
    "imsOrgId": "{ORG_ID}",
    "packageId": "{PACKAGE_ID}"
}
```
