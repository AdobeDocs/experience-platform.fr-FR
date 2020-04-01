---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Descripteurs
topic: developer guide
translation-type: tm+mt
source-git-commit: 599991af774e283d9fb60216e3d3bd5b17cf8193

---


# Descripteurs

Les  définissent un statique d’entités de données, mais ne fournissent pas de détails spécifiques sur la manière dont les données basées sur ces  (jeux de données, par exemple) peuvent se relier les unes aux autres. Adobe Experience Platform vous permet de décrire ces relations et d’autres métadonnées interprétatives relatives à un à l’aide de descripteurs.

Les descripteurs de  de sont des métadonnées au niveau du client, ce qui signifie qu’ils sont propres à votre organisation IMS et que toutes les opérations de descripteur se déroulent dans le du client.

Une ou plusieurs entités de descripteur de  de peuvent être appliquées à chaque . Chaque entité descripteur de  de comprend un descripteur `@type` et `sourceSchema` à quoi il s’applique. Une fois appliqués, ces descripteurs s’appliquent à tous les jeux de données créés à l’aide du .

Ce fournit des exemples d’appels d’API pour les descripteurs, ainsi qu’un complet de descripteurs disponibles et des champs requis pour la définition de chaque type.

>[!NOTE] Les descripteurs nécessitent des en-têtes Accept uniques qui remplacent `xed` par `xdm`, mais qui, dans le cas contraire, ressemblent beaucoup aux en-têtes Accepter utilisés ailleurs dans le registre des  de. Les en-têtes Accepter appropriés ont été inclus dans les exemples d’appels ci-dessous, mais soyez très prudent pour vous assurer que les en-têtes appropriés sont utilisés.

## descripteurs de 

Une requête GET unique peut être utilisée pour renvoyer un  de tous les descripteurs définis par votre organisation.

**Format API**

```http
GET /tenant/descriptors
```

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

Le format de réponse dépend de l’en-tête Accepter envoyé dans la requête. Notez que le `/descriptors` point de fin utilise des en-têtes Accepter différents de tous les autres points de fin dans l’API de Registre  du.

Les en-têtes d’acceptation du descripteur se remplacent `xed` par `xdm`, et   une `link` option propre aux descripteurs.

| Accepter | Description |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Renvoie un tableau d’ID de descripteur |
| `application/vnd.adobe.xdm-link+json` | Renvoie un tableau de chemins d’API descripteur |
| `application/vnd.adobe.xdm+json` | Renvoie un tableau d’objets descripteurs étendus |

**Réponse**

La réponse comprend un tableau pour chaque type de descripteur qui a défini des descripteurs. En d’autres termes, s’il n’existe aucun descripteur d’un certain `@type` paramètre défini, le registre ne renvoie pas de tableau vide pour ce type de descripteur.

Lors de l’utilisation de l’en-tête `link` Accepter, chaque descripteur est présenté sous la forme d’un tableau au format `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

```JSON
{
  "xdm:alternateDisplayInfo": [
    "/tenant/descriptors/85dc1bc8b91516ac41163365318e38a9f1e4f351",
    "/tenant/descriptors/49bd5abb5a1310ee80ebc1848eb508d383a462cf",
    "/tenant/descriptors/b3b3e548f1c653326bcf5459ceac4140fc0b9e08"
  ],
  "xdm:descriptorIdentity": [
    "/tenant/descriptors/f7a4bc25429496c4740f8f9a7a49ba96862c5379"
  ],
  "xdm:descriptorOneToOne": [
    "/tenant/descriptors/cb509fd6f8ab6304e346905441a34b58a0cd481a"
  ]
}
```

## Rechercher un descripteur

Si vous souhaitez  les détails d&#39;un descripteur spécifique, vous pouvez rechercher (GET) un descripteur individuel à l&#39;aide de son `@id`.

**Format API**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DESCRIPTOR_ID}` | Le nom `@id` du descripteur à rechercher. |

**Requête**

Les descripteurs ne sont pas versionnés. Par conséquent, aucun en-tête Accepter n’est requis dans la demande de recherche.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails du descripteur, y compris son `@type` et `sourceSchema`, ainsi que des informations supplémentaires qui varient selon le type de descripteur. La valeur renvoyée `@id` doit correspondre au descripteur `@id` fourni dans la requête.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "createdUser": "{CREATED_USER}",
  "imsOrg": "{IMS_ORG}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Créer un descripteur

Le Registre des  vous permet de définir plusieurs types de descripteurs différents. Chaque type de descripteur nécessite l’envoi de ses propres champs spécifiques dans la requête POST. Un complet de descripteurs, ainsi que les champs nécessaires pour les définir, sont disponibles dans la section de l&#39;annexe sur la [définition des descripteurs](#defining-descriptors).

**Format API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante définit un descripteur d’identité sur un champ &quot;adresse électronique&quot; dans un exemple de . Cela indique à la plateforme d’expérience d’utiliser l’adresse électronique comme identifiant pour faciliter la collecte d’informations sur l’individu.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 (Créé) et les détails du nouveau descripteur, y compris son `@id`nom. Il `@id` s’agit d’un champ en lecture seule attribué par le Registre des  du et utilisé pour référencer le descripteur dans l’API.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Mettre à jour le descripteur

Vous pouvez mettre à jour un descripteur en effectuant une requête PUT qui référence le descripteur `@id` que vous souhaitez mettre à jour dans le chemin de la requête.

**Format API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DESCRIPTOR_ID}` | Le descripteur `@id` que vous souhaitez mettre à jour. |

**Requête**

Cette requête _réécrit_ essentiellement le descripteur. Le corps de la requête doit donc inclure tous les champs nécessaires pour définir un descripteur de ce type. En d’autres termes, la charge utile de requête pour mettre à jour (PUT) un descripteur est identique à la charge utile pour créer (POST) un descripteur du même type.

Dans cet exemple, le descripteur d’identité est mis à jour pour faire référence à un autre `xdm:sourceProperty` (téléphone mobile) et remplacer le `xdm:namespace` par &quot;téléphone&quot;.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/mobilePhone/number",
        "xdm:namespace": "Phone",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

Des détails concernant les propriétés `xdm:namespace` et `xdm:property`, y compris leur accès, sont disponibles dans la section de l&#39;annexe sur la [définition des descripteurs](#defining-descriptors).

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 (Créé) et le descripteur mis à jour (qui doit correspondre au `@id` `@id` contenu envoyé dans la requête).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

L’exécution d’une demande de recherche (GET) pour au descripteur  que les champs ont été mis à jour pour refléter les modifications envoyées dans la demande de recherche (PUT).

## Supprimer le descripteur

Il peut arriver que vous deviez supprimer un descripteur que vous avez défini du Registre des  de. Pour ce faire, vous devez effectuer une requête DELETE faisant référence au descripteur `@id` que vous souhaitez supprimer.

**Format API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DESCRIPTOR_ID}` | Le descripteur `@id` que vous souhaitez supprimer. |

**Requête**

Les en-têtes d’acceptation ne sont pas obligatoires lors de la suppression de descripteurs.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 204 (aucun contenu) et un corps vide.

Pour confirmer la suppression du descripteur, vous pouvez exécuter une requête de recherche par rapport au descripteur `@id`. La réponse renvoie l’état HTTP 404 (Introuvable), car le descripteur a été supprimé du Registre des .

## Annexe

La section suivante fournit des informations supplémentaires sur l’utilisation des descripteurs dans l’API de Registre  du.

### Définition de descripteurs

Les sections suivantes présentent un aperçu des types de descripteurs disponibles, y compris les champs obligatoires pour définir un descripteur de chaque type.

#### descripteur d’identité

Un descripteur d’identité signale que la &quot;sourceProperty&quot; de la &quot;sourceSchema&quot; est un champ d’identité, comme décrit par [Adobe Experience Platform Identity Service](../../identity-service/home.md).

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false
}
```

| Propriété | Description |
| --- | --- |
| `@type` | Type de descripteur en cours de définition. |
| `xdm:sourceSchema` | URI `$id` du dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du source . |
| `xdm:sourceProperty` | Chemin d’accès à la propriété spécifique qui sera l’identité. Le chemin doit commencer par un &quot;/&quot; et ne pas se terminer par un. N’incluez pas de &quot;propriétés&quot; dans le chemin d’accès (par exemple, utilisez &quot;/PersonalEmail/address&quot; au lieu de &quot;/properties/PersonalEmail/properties/address&quot;). |
| `xdm:namespace` | La `id` valeur ou `code` la valeur de l’identité  . Vous trouverez un de    à l’aide de l’API [Service d’](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)identité. |
| `xdm:property` | Soit `xdm:id` soit `xdm:code`, selon l’ `xdm:namespace` utilisation utilisée. |
| `xdm:isPrimary` | Valeur booléenne facultative. Lorsque la valeur est true, le champ est l’identité principale.  ne peut contenir qu&#39;une seule identité primaire. |

#### Descripteur de nom convivial

Les descripteurs de nom conviviaux permettent à l’utilisateur de modifier les valeurs `title` et les `description` valeurs des champs de de bibliothèque principaux. Particulièrement utile lorsque vous travaillez avec des &quot;eVars&quot; et d’autres champs &quot;génériques&quot; que vous souhaitez étiqueter comme contenant des informations propres à votre entreprise. L’interface utilisateur peut les utiliser pour afficher un nom plus convivial ou uniquement pour afficher les champs dont le nom est convivial.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1
  "xdm:sourceProperty": "/eVars/eVar1",
  "xdm:title": {
    "en_us":{"Loyalty ID"}
  },
  "xdm:description": {
    "en_us":{"Unique ID of loyalty program member."}
  },
}
```

| Propriété | Description |
| --- | --- |
| `@type` | Type de descripteur en cours de définition. |
| `xdm:sourceSchema` | URI `$id` du dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du source . |
| `xdm:sourceProperty` | Chemin d’accès à la propriété spécifique qui sera l’identité. Le chemin doit commencer par un &quot;/&quot; et ne pas se terminer par un. N’incluez pas de &quot;propriétés&quot; dans le chemin d’accès (par exemple, utilisez &quot;/PersonalEmail/address&quot; au lieu de &quot;/properties/PersonalEmail/properties/address&quot;). |
| `xdm:title` | Le nouveau titre que vous souhaitez afficher pour ce champ, écrit dans la casse de titre. |
| `xdm:description` | Une description facultative peut être ajoutée avec le titre. |

#### Descripteur de relation

Les descripteurs de relation décrivent une relation entre deux  de différents, en fonction des propriétés décrites dans les sections `sourceProperty` et `destinationProperty`. Pour plus d’informations, consultez le didacticiel sur la [définition d’une relation entre deux](../tutorials/relationship-api.md) .

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": 
    "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

| Propriété | Description |
| --- | --- |
| `@type` | Type de descripteur en cours de définition. |
| `xdm:sourceSchema` | URI `$id` du dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du source . |
| `xdm:sourceProperty` | Chemin d’accès au champ dans le source  où la relation est définie. Doit commencer par un &quot;/&quot; et ne pas se terminer par un. N’incluez pas &quot;properties&quot; dans le chemin d’accès (par exemple, &quot;/PersonalEmail/address&quot; au lieu de &quot;/properties/PersonalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | L&#39; `$id` URI du de destination  ce descripteur définit une relation avec. |
| `xdm:destinationVersion` | Version principale du de destination. |
| `xdm:destinationProperty` | Chemin d’accès facultatif à un champ de  dans le de destination. Si cette propriété est omise, le champ de  du est déduit par les champs qui contiennent un descripteur d’identité de référence correspondant (voir ci-dessous). |


#### Descripteur d’identité de référence

Les descripteurs d’identité de référence fournissent un contexte de référence à un champ de , ce qui permet de le lier au champ d’identité principal d’un  de destination. Les champs doivent déjà être étiquetés avec un descripteur d’identité avant qu’un descripteur de référence ne puisse leur être appliqué.

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:identityNamespace": "Email"
}
```

| Propriété | Description |
| --- | --- |
| `@type` | Type de descripteur en cours de définition. |
| `xdm:sourceSchema` | URI `$id` du dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du source . |
| `xdm:sourceProperty` | Chemin d’accès au champ dans le source  où le descripteur est en cours de définition. Doit commencer par un &quot;/&quot; et ne pas se terminer par un. N’incluez pas &quot;properties&quot; dans le chemin d’accès (par exemple, &quot;/PersonalEmail/address&quot; au lieu de &quot;/properties/PersonalEmail/properties/address&quot;). |
| `xdm:identityNamespace` | L’identité  le code  de la propriété source. |