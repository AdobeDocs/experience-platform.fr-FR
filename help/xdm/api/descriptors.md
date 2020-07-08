---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Descripteurs
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 2%

---


# Descripteurs

Les Schémas définissent une vue statique des entités de données, mais ne fournissent pas de détails spécifiques sur la manière dont les données basées sur ces schémas (jeux de données, par exemple) peuvent se relier les unes aux autres. L’Adobe Experience Platform vous permet de décrire ces relations et d’autres métadonnées interprétatives sur un schéma à l’aide de descripteurs.

Les descripteurs de Schéma sont des métadonnées au niveau du client, ce qui signifie qu&#39;ils sont propres à votre organisation IMS et que toutes les opérations de descripteurs ont lieu dans le conteneur du client.

Un ou plusieurs descripteurs de schéma peuvent être appliqués à chaque schéma. Chaque entité descripteur de schéma comprend un descripteur `@type` et le `sourceSchema` auquel il s&#39;applique. Une fois appliqués, ces descripteurs s&#39;appliquent à tous les jeux de données créés à l&#39;aide du schéma.

Ce document fournit des exemples d&#39;appels d&#39;API pour les descripteurs, ainsi qu&#39;une liste complète des descripteurs disponibles et des champs requis pour définir chaque type.

>[!NOTE]
>
>Les descripteurs nécessitent des en-têtes Accept uniques qui remplacent `xed` par `xdm`, mais qui, autrement, ressemblent beaucoup aux en-têtes Accept utilisés ailleurs dans le registre des Schémas. Les en-têtes Accepter appropriés ont été inclus dans les exemples d’appels ci-dessous, mais soyez prudent pour vous assurer que les en-têtes appropriés sont utilisés.

## descripteurs de Liste

Une seule requête GET peut être utilisée pour renvoyer une liste de tous les descripteurs définis par votre organisation.

**Format d’API**

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

Le format de réponse dépend de l’en-tête Accepter envoyé dans la requête. Notez que le `/descriptors` point de terminaison utilise des en-têtes Accepter différents de tous les autres points de terminaison dans l&#39;API de Registre de Schéma.

Les en-têtes Accepter du descripteur remplacent `xed` par `xdm`et offre une `link` option propre aux descripteurs.

| Accepter | Description |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Renvoie un tableau d’ID de descripteur. |
| `application/vnd.adobe.xdm-link+json` | Renvoie un tableau de chemins d’API descripteur. |
| `application/vnd.adobe.xdm+json` | Renvoie un tableau d’objets descripteurs étendus |

**Réponse**

La réponse comprend un tableau pour chaque type de descripteur qui a défini des descripteurs. En d&#39;autres termes, s&#39;il n&#39;y a pas de descripteurs d&#39;un certain `@type` type défini, le registre ne retournera pas un tableau vide pour ce type de descripteur.

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

Si vous souhaitez vue les détails d&#39;un descripteur spécifique, vous pouvez rechercher (GET) un descripteur individuel à l&#39;aide de son `@id`nom.

**Format d’API**

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

Une réponse réussie renvoie les détails du descripteur, y compris son `@type` et `sourceSchema`ainsi que des informations supplémentaires qui varient selon le type de descripteur. La valeur renvoyée `@id` doit correspondre au descripteur `@id` fourni dans la requête.

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

Le Registre des Schémas vous permet de définir plusieurs types de descripteurs différents. Chaque type de descripteur nécessite l’envoi de ses propres champs spécifiques dans la demande POST. Une liste complète des descripteurs et des champs nécessaires pour les définir est disponible dans la section de l&#39;annexe sur la [définition des descripteurs](#defining-descriptors).

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante définit un descripteur d’identité sur un champ &quot;adresse électronique&quot; dans un exemple de schéma. Cela indique à l’Experience Platform d’utiliser l’adresse électronique comme identifiant pour réunir les informations sur l’individu.

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

Une réponse réussie renvoie l’état HTTP 201 (Créé) et les détails du descripteur nouvellement créé, y compris son `@id`nom. Il `@id` s’agit d’un champ en lecture seule attribué par le Registre du Schéma et utilisé pour référencer le descripteur dans l’API.

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

Vous pouvez mettre à jour un descripteur en exécutant une requête PUT qui référence le descripteur que vous souhaitez mettre à jour dans le chemin d’accès `@id` de la requête.

**Format d’API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DESCRIPTOR_ID}` | Le nom `@id` du descripteur à mettre à jour. |

**Requête**

Cette requête _réécrit_ essentiellement le descripteur, de sorte que le corps de la requête doit inclure tous les champs nécessaires pour définir un descripteur de ce type. En d’autres termes, la charge utile de requête pour mettre à jour (PUT) un descripteur est identique à la charge utile pour créer (POST) un descripteur du même type.

Dans cet exemple, le descripteur d&#39;identité est en cours de mise à jour afin de référencer un autre `xdm:sourceProperty` (téléphone mobile) et de remplacer le `xdm:namespace` mot par &quot;téléphone&quot;.

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

Des détails concernant les propriétés `xdm:namespace` et `xdm:property`les méthodes d&#39;accès sont disponibles dans la section de l&#39;annexe consacrée à la [définition des descripteurs](#defining-descriptors).

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 (Créé) et le descripteur mis à jour (qui doit correspondre à celui `@id` `@id` envoyé dans la demande).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

L’exécution d’une demande de recherche (GET) à la vue du descripteur indique que les champs ont été mis à jour pour refléter les modifications envoyées dans la demande de recherche (PUT).

## Supprimer le descripteur

Il peut arriver que vous deviez supprimer un descripteur que vous avez défini dans le Registre des Schémas. Pour ce faire, il vous suffit de faire une demande de DELETE référençant le descripteur `@id` que vous souhaitez supprimer.

**Format d’API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DESCRIPTOR_ID}` | Le nom `@id` du descripteur à supprimer. |

**Requête**

Les en-têtes d’acceptation ne sont pas requis lors de la suppression de descripteurs.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie l’état HTTP 204 (Aucun contenu) et un corps vide.

Pour confirmer que le descripteur a été supprimé, vous pouvez exécuter une requête de recherche sur le descripteur `@id`. La réponse renvoie l’état HTTP 404 (Introuvable) car le descripteur a été supprimé du registre de Schéma.

## Annexe

La section suivante fournit des informations supplémentaires sur l&#39;utilisation des descripteurs dans l&#39;API de registre de Schéma.

### Définition de descripteurs

Les sections suivantes présentent un aperçu des types de descripteurs disponibles, y compris les champs requis pour définir un descripteur de chaque type.

#### Descripteur d&#39;identité

Un descripteur d&#39;identité signale que la &quot;sourceProperty&quot; de la &quot;sourceSchema&quot; est un champ d&#39;identité tel que décrit par [Adobe Experience Platform Identity Service](../../identity-service/home.md).

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
| `xdm:sourceSchema` | URI `$id` du schéma où le descripteur est en cours de définition. |
| `xdm:sourceVersion` | Version principale du schéma source. |
| `xdm:sourceProperty` | Chemin d’accès à la propriété spécifique qui sera l’identité. Le chemin doit commencer par un &quot;/&quot; et ne pas se terminer par un. N’incluez pas de &quot;propriétés&quot; dans le chemin d’accès (par exemple, utilisez &quot;/personalEmail/address&quot; au lieu de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:namespace` | Valeur `id` ou `code` valeur de l&#39;espace de nommage d&#39;identité. Vous trouverez une liste d&#39;espaces de nommage à l&#39;aide de l&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)Identity Service. |
| `xdm:property` | Soit `xdm:id` soit `xdm:code`, selon l’ `xdm:namespace` utilisation. |
| `xdm:isPrimary` | Valeur booléenne facultative. Lorsque la valeur est true, le champ est indiqué comme identité principale. Les Schémas ne peuvent contenir qu&#39;une seule identité primaire. |

#### Descripteur de nom convivial

Les descripteurs de nom conviviaux permettent à l’utilisateur de modifier les `title`champs de schéma de bibliothèque principale, `description`et `meta:enum` les valeurs correspondantes. Particulièrement utile lorsque vous travaillez avec des &quot;eVars&quot; et d’autres champs &quot;génériques&quot; que vous souhaitez étiqueter comme contenant des informations spécifiques à votre entreprise. L’interface utilisateur peut les utiliser pour afficher un nom plus convivial ou uniquement pour afficher les champs dont le nom est convivial.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:title": {
    "en_us": "Event Type"
  },
  "xdm:description": {
    "en_us": "The type of experience event detected by the system."
  },
  "meta:enum": {
    "click": "Mouse Click",
    "addCart": "Add to Cart",
    "checkout": "Cart Checkout"
  }
}
```

| Propriété | Description |
| --- | --- |
| `@type` | Type de descripteur en cours de définition. |
| `xdm:sourceSchema` | URI `$id` du schéma où le descripteur est en cours de définition. |
| `xdm:sourceVersion` | Version principale du schéma source. |
| `xdm:sourceProperty` | Chemin d’accès à la propriété spécifique qui sera l’identité. Le chemin doit commencer par un &quot;/&quot; et ne pas se terminer par un. N’incluez pas de &quot;propriétés&quot; dans le chemin d’accès (par exemple, utilisez &quot;/personalEmail/address&quot; au lieu de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:title` | Le nouveau titre que vous souhaitez afficher pour ce champ, écrit dans la casse de titre. |
| `xdm:description` | Une description facultative peut être ajoutée avec le titre. |
| `meta:enum` | Si le champ indiqué par `xdm:sourceProperty` est un champ de chaîne, `meta:enum` détermine la liste des valeurs suggérées pour le champ dans l’interface utilisateur de l’Experience Platform. Il est important de noter que `meta:enum` ne déclare pas de énumération ou ne fournit aucune validation de données pour le champ XDM.<br><br>Ceci ne doit être utilisé que pour les champs XDM principaux définis par Adobe. Si la propriété source est un champ personnalisé défini par votre organisation, vous devez modifier la `meta:enum` propriété du champ directement via une requête [](./update-resource.md)PATCH. |

#### Descripteur de relation

Les descripteurs de relation décrivent une relation entre deux schémas différents, en fonction des propriétés décrites dans la section `sourceProperty` et `destinationProperty`. Pour plus d&#39;informations, consultez le didacticiel sur la [définition d&#39;une relation entre deux schémas](../tutorials/relationship-api.md) .

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
| `xdm:sourceSchema` | URI `$id` du schéma où le descripteur est en cours de définition. |
| `xdm:sourceVersion` | Version principale du schéma source. |
| `xdm:sourceProperty` | Chemin d’accès au champ du schéma source dans lequel la relation est définie. Doit commencer par un &quot;/&quot; et ne pas se terminer par un. N’incluez pas &quot;properties&quot; dans le chemin d’accès (par exemple, &quot;/personalEmail/address&quot; au lieu de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:destinationSchema` | L&#39; `$id` URI du schéma de destination avec lequel ce descripteur définit une relation. |
| `xdm:destinationVersion` | Version principale du schéma de destination. |
| `xdm:destinationProperty` | Chemin d’accès facultatif à un champ de cible dans le schéma de destination. Si cette propriété est omise, le champ de cible est déduit par les champs qui contiennent un descripteur d&#39;identité de référence correspondant (voir ci-dessous). |


#### Descripteur d&#39;identité de référence

Les descripteurs d&#39;identité de référence fournissent un contexte de référence à un champ de schéma, ce qui permet de le lier au champ d&#39;identité principal d&#39;un schéma de destination. Les champs doivent déjà être étiquetés avec un descripteur d&#39;identité avant qu&#39;un descripteur de référence ne puisse leur être appliqué.

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
| `xdm:sourceSchema` | URI `$id` du schéma où le descripteur est en cours de définition. |
| `xdm:sourceVersion` | Version principale du schéma source. |
| `xdm:sourceProperty` | Chemin d’accès au champ du schéma source dans lequel le descripteur est en cours de définition. Doit commencer par un &quot;/&quot; et ne pas se terminer par un. N’incluez pas &quot;properties&quot; dans le chemin d’accès (par exemple, &quot;/personalEmail/address&quot; au lieu de &quot;/properties/personalEmail/properties/address&quot;). |
| `xdm:identityNamespace` | Code d&#39;espace de nommage d&#39;identité de la propriété source. |