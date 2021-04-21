---
keywords: Experience Platform ; accueil ; rubriques populaires ; api ; API ; XDM ; système XDM ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données ; modèle de données ; modèle de données ; registre de schémas ; registre de Schémas ; descripteur ; descripteurs ; descripteurs ; identité ; identité ; nom convivial ; nom convivial ; référence ; référence ; relation ; relation
solution: Experience Platform
title: Point de terminaison de l'API descripteurs
description: Le point de terminaison /descriptors de l'API de registre de Schéma vous permet de gérer par programmation les descripteurs XDM dans votre application d'expérience.
topic-legacy: developer guide
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1613'
ht-degree: 56%

---

# Point de terminaison des descripteurs

Les schémas définissent un affichage statique des entités de données, mais ne fournissent pas de détails spécifiques sur la manière dont les données basées sur ces schémas (jeux de données, par exemple) peuvent être reliées entre elles. Adobe Experience Platform vous permet de décrire ces relations et d’autres métadonnées interprétatives relatives à un schéma à l’aide de descripteurs.

Les descripteurs de schéma sont des métadonnées au niveau du client, ce qui signifie qu’ils sont propres à votre organisation IMS et que toutes les opérations de descripteur se déroulent dans le conteneur du client.

Une ou plusieurs entités de descripteur de schéma peuvent être appliquées à chaque schéma. Chaque entité de descripteur de schéma comprend un descripteur `@type` et le `sourceSchema` auquel il s’applique. Une fois appliqués, ces descripteurs s’appliquent à tous les jeux de données créés à l’aide du schéma.

Le point de terminaison `/descriptors` de l&#39;API [!DNL Schema Registry] vous permet de gérer par programmation les descripteurs dans votre application d&#39;expérience.

## Prise en main

Le point de terminaison utilisé dans ce guide fait partie de l&#39;[[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation connexe, un guide de lecture des exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API Experience Platform.

## Récupérer une liste de descripteurs {#list}

Vous pouvez liste tous les descripteurs définis par votre organisation en adressant une demande de GET à `/tenant/descriptors`.

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

Le format de réponse dépend de l&#39;en-tête `Accept` envoyé dans la demande. Notez que le point de terminaison `/descriptors` utilise des en-têtes différents de tous les autres points de terminaison dans l’API .`Accept`[!DNL Schema Registry]

>[!IMPORTANT]
>
>Les descripteurs nécessitent des en-têtes `Accept` uniques qui remplacent `xed` par `xdm` et offre également une option `link` unique aux descripteurs. Les en-têtes `Accept` appropriés ont été inclus dans les appels d&#39;exemples ci-dessous, mais soyez prudent pour vous assurer que les en-têtes appropriés sont utilisés lors de l&#39;utilisation de descripteurs.

| En-tête `Accept` | Description |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Renvoie un tableau d’identifiants de descripteur |
| `application/vnd.adobe.xdm-link+json` | Renvoie un tableau de chemins d’API de descripteur |
| `application/vnd.adobe.xdm+json` | Renvoie un tableau d’objets de descripteurs étendus |
| `application/vnd.adobe.xdm-v2+json` | Cet en-tête `Accept` doit être utilisé pour utiliser les capacités de pagination. |

**Réponse**

La réponse comprend un tableau pour chaque type de descripteur possédant des descripteurs définis. En d’autres termes, s’il n’existe aucun descripteur d’un certain `@type` défini, le registre ne renvoie pas de tableau vide pour ce type de descripteur.

Lors de l’utilisation de l’en-tête `link``Accept`, chaque descripteur est présenté sous la forme d’un tableau au format `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

## Recherche d’un descripteur {#lookup}

Si vous souhaitez consulter les détails d’un descripteur spécifique, vous pouvez rechercher (GET) un descripteur individuel à l’aide de son identifiant `@id`.

**Format d’API**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DESCRIPTOR_ID}` | `@id` du descripteur que vous souhaitez rechercher. |

**Requête**

La requête suivante récupère un descripteur par sa valeur `@id`. Les descripteurs ne sont pas versionnés. Par conséquent, aucun en-tête `Accept` n&#39;est requis dans la demande de recherche.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails du descripteur, y compris ses `@type` et `sourceSchema`, ainsi que des informations supplémentaires qui varient selon le type de descripteur. L’identifiant `@id` renvoyé doit correspondre à l’identifiant `@id` du descripteur fourni dans la requête.

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

## Créer un descripteur {#create}

Vous pouvez créer un nouveau descripteur en adressant une requête de POST au point de terminaison `/tenant/descriptors`.

>[!IMPORTANT]
>
>[!DNL Schema Registry] vous permet de définir plusieurs types de descripteurs différents. Chaque type de descripteur nécessite l’envoi de ses propres champs spécifiques dans le corps de la requête. Voir l&#39;[annexe](#defining-descriptors) pour une liste complète des descripteurs et des champs nécessaires pour les définir.

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante définit un descripteur d’identité dans un champ « adresse électronique » d’un exemple de schéma. [!DNL Experience Platform] est ainsi invité à utiliser l’adresse électronique comme identifiant afin de mieux rassembler les informations sur l’individu.

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

Une réponse réussie renvoie un état HTTP 201 (Created) et les détails du nouveau descripteur, y compris son identifiant `@id`. `@id` est un champ en lecture seule attribué par [!DNL Schema Registry] et utilisé pour référencer le descripteur dans l&#39;API.

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

## Mettre à jour un descripteur {#put}

Vous pouvez mettre à jour un descripteur en incluant `@id` dans le chemin d’une requête de PUT.

**Format d’API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DESCRIPTOR_ID}` | L’identifiant `@id` du descripteur que vous souhaitez mettre à jour. |

**Requête**

Cette requête réécrit essentiellement le descripteur. Le corps de la requête doit donc inclure tous les champs nécessaires pour définir un descripteur de ce type. En d’autres termes, la charge utile de requête pour mettre à jour (PUT) un descripteur est identique à la charge utile pour [créer (POST) un descripteur](#create) du même type.

>[!IMPORTANT]
>
>Tout comme pour la création de descripteurs à l’aide de requêtes de POST, chaque type de descripteur nécessite l’envoi de ses propres champs spécifiques dans les charges de requête de PUT. Voir l&#39;[annexe](#defining-descriptors) pour une liste complète des descripteurs et des champs nécessaires pour les définir.

L&#39;exemple suivant met à jour un descripteur d&#39;identité pour référencer un `xdm:sourceProperty` différent (`mobile phone`) et remplacer `xdm:namespace` par `Phone`.

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

**Réponse**

Une réponse réussie renvoie un état HTTP 201 (Created) et l’identifiant `@id` du descripteur mis à jour (qui doit correspondre à l’identifiant `@id` envoyé dans la requête).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

L&#39;exécution d&#39;une requête [de recherche (GET)](#lookup) à la vue du descripteur montre que les champs ont maintenant été mis à jour pour refléter les modifications envoyées dans la demande de PUT.

## Supprimer un descripteur {#delete}

Il peut arriver que vous deviez supprimer un descripteur que vous avez défini dans le [!DNL Schema Registry]. Pour ce faire, effectuez une requête DELETE en référençant l’identifiant `@id` du descripteur que vous souhaitez supprimer.

**Format d’API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DESCRIPTOR_ID}` | L’identifiant `@id` du descripteur que vous souhaitez supprimer. |

**Requête**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

Pour confirmer que le descripteur a été supprimé, vous pouvez exécuter une requête de recherche [](#lookup) par rapport au descripteur `@id`. La réponse renvoie l&#39;état HTTP 404 (Introuvable) car le descripteur a été supprimé de [!DNL Schema Registry].

## Annexe

La section suivante fournit des informations supplémentaires sur l&#39;utilisation des descripteurs dans l&#39;API [!DNL Schema Registry].

### Définition de descripteurs {#defining-descriptors}

Les sections suivantes présentent les types de descripteurs disponibles, y compris les champs nécessaires pour définir un descripteur de chaque type.

#### Descripteur d’identité

Un descripteur d&#39;identité signale que le champ &quot;[!UICONTROL sourceProperty]&quot; de &quot;[!UICONTROL sourceSchema]&quot; est un champ [!DNL Identity] comme décrit par [Service d&#39;identité de Adobe Experience Platform](../../identity-service/home.md).

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
| `@type` | Le type de descripteur en cours de définition. |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Le chemin vers la propriété spécifique qui sera l’identité. Le chemin doit commencer et non se terminer par un « / ». N’incluez pas « properties » dans le chemin (par exemple, utilisez « /personalEmail/address » au lieu de « /properties/personalEmail/properties/address ») |
| `xdm:namespace` | La valeur `id` ou `code` de l’espace de noms de l’identité. Une liste d&#39;espaces de nommage peut être trouvée à l&#39;aide de [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml). |
| `xdm:property` | `xdm:id` ou `xdm:code` selon l’espace de noms `xdm:namespace` utilisé. |
| `xdm:isPrimary` | Une valeur booléenne facultative. Lorsqu’elle est définie sur true, le champ est l’identité principale. Les schémas ne peuvent contenir qu’une seule identité principale. |

#### Descripteur de nom convivial

Les descripteurs de nom conviviaux permettent à un utilisateur de modifier les valeurs `title`, `description` et `meta:enum` des champs du schéma de bibliothèque principal. Ils sont particulièrement utiles lorsque vous utilisez des « eVars » et d’autres champs « génériques » auxquels vous souhaitez appliquer des libellés indiquant qu’ils contiennent des informations propres à votre organisation. L’interface utilisateur peut les utiliser pour afficher un nom plus convivial ou pour n’afficher que les champs dont le nom est convivial.

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
| `@type` | Le type de descripteur en cours de définition. |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Le chemin vers la propriété spécifique qui sera l’identité. Le chemin doit commencer et non se terminer par un « / ». N’incluez pas « properties » dans le chemin (par exemple, utilisez « /personalEmail/address » au lieu de « /properties/personalEmail/properties/address ») |
| `xdm:title` | Le nouveau titre que vous souhaitez afficher pour ce champ, écrit en Casse Titre. |
| `xdm:description` | Vous pouvez ajouter une description facultative avec le titre. |
| `meta:enum` | Si le champ indiqué par `xdm:sourceProperty` est un champ de chaîne, `meta:enum` détermine la liste des valeurs suggérées pour le champ dans l&#39;interface utilisateur [!DNL Experience Platform]. Il est important de noter que `meta:enum` ne déclare pas de énumération ou ne fournit aucune validation de données pour le champ XDM.<br><br>Ceci ne doit être utilisé que pour les champs XDM principaux définis par Adobe. Si la propriété source est un champ personnalisé défini par votre organisation, vous devez modifier la propriété `meta:enum` du champ directement par le biais d&#39;une requête de PATCH à la ressource parente du champ. |

#### Descripteur de relation

Les descripteurs de relation décrivent une relation entre deux schémas différents, en fonction des propriétés décrites dans `sourceProperty` et `destinationProperty`. Pour plus d’informations, consultez le tutoriel sur [la définition d’une relation entre deux schémas](../tutorials/relationship-api.md).

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
| `@type` | Le type de descripteur en cours de définition. |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Chemin vers le champ du schéma source dans lequel la relation est définie. Doit commencer et non se terminer par un « / ». N’incluez pas « properties » dans le chemin (par exemple, « /personalEmail/address » au lieu de « /properties/personalEmail/properties/address »). |
| `xdm:destinationSchema` | L’URI `$id` du schéma de destination avec lequel ce descripteur définit une relation. |
| `xdm:destinationVersion` | La version principale du schéma de destination. |
| `xdm:destinationProperty` | Chemin facultatif vers un champ cible dans le schéma de destination. Si cette propriété est omise, le champ cible est déterminé par les champs qui contiennent un descripteur d’identité de référence correspondant (voir ci-dessous). |


#### Descripteur d’identité de référence

Les descripteurs d&#39;identité de référence fournissent un contexte de référence à l&#39;identité Principale d&#39;un champ de schéma, ce qui permet de le référencer par des champs d&#39;autres schémas. Les champs doivent déjà disposer d’un libellé de descripteur d’identité avant qu’un descripteur de référence puisse leur être appliqué.

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
| `@type` | Le type de descripteur en cours de définition. |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Chemin vers le champ du schéma source dans lequel le descripteur est défini. Doit commencer et non se terminer par un « / ». N’incluez pas « properties » dans le chemin (par exemple, « /personalEmail/address » au lieu de « /properties/personalEmail/properties/address »). |
| `xdm:identityNamespace` | Le code d’espace de noms d’identité de la propriété source. |
