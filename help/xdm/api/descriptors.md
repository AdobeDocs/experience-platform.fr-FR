---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre de schémas;registre de schémas;descripteur;descripteur;descripteurs;descripteurs;identité;Identité;nom convivial;alternatedisplayinfo;référence;référence;relation;Relation
solution: Experience Platform
title: Point d’entrée de l’API Descriptors
description: Le point d’entrée /descriptors dans l’API Schema Registry vous permet de gérer par programmation les descripteurs XDM dans votre application d’expérience.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: d6015125e3e29bdd6a6c505b5f5ad555bd17a0e0
workflow-type: tm+mt
source-wordcount: '2192'
ht-degree: 38%

---

# Point d’entrée des descripteurs

Les schémas définissent un affichage statique des entités de données, mais ne fournissent pas de détails spécifiques sur la manière dont les données basées sur ces schémas (jeux de données, par exemple) peuvent être reliées entre elles. Adobe Experience Platform vous permet de décrire ces relations et d’autres métadonnées interprétatives relatives à un schéma à l’aide de descripteurs.

Les descripteurs de schéma sont des métadonnées au niveau du client, ce qui signifie qu’ils sont propres à votre organisation et que toutes les opérations de descripteur ont lieu dans le conteneur du client.

Une ou plusieurs entités de descripteur de schéma peuvent être appliquées à chaque schéma. Chaque entité de descripteur de schéma comprend un descripteur `@type` et le `sourceSchema` auquel il s’applique. Une fois appliqués, ces descripteurs s’appliquent à tous les jeux de données créés à l’aide du schéma.

Le point d’entrée `/descriptors` de l’API [!DNL Schema Registry] vous permet de gérer par programmation les descripteurs dans votre application d’expérience.

## Commencer

Le point d’entrée utilisé dans ce guide fait partie de l’API [[!DNL Schema Registry] ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Récupérer une liste de descripteurs {#list}

Vous pouvez répertorier tous les descripteurs qui ont été définis par votre organisation en effectuant une requête GET à `/tenant/descriptors`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

Le format de la réponse dépend de l’en-tête `Accept` envoyé dans la requête. Notez que le point d’entrée `/descriptors` utilise des en-têtes `Accept` différents de tous les autres points d’entrée de l’API [!DNL Schema Registry].

>[!IMPORTANT]
>
>Les descripteurs nécessitent des en-têtes de `Accept` uniques qui remplacent les `xed` par des `xdm` et offrent également une option de `link` propre aux descripteurs. Les en-têtes `Accept` appropriés ont été inclus dans les exemples d’appels ci-dessous, mais soyez très prudent pour vous assurer que les en-têtes corrects sont utilisés lors de l’utilisation de descripteurs.

| En-tête `Accept` | Description |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Renvoie un tableau d’identifiants de descripteur |
| `application/vnd.adobe.xdm-link+json` | Renvoie un tableau de chemins d’API de descripteur |
| `application/vnd.adobe.xdm+json` | Renvoie un tableau d’objets de descripteurs étendus |
| `application/vnd.adobe.xdm-v2+json` | Cet en-tête `Accept` doit être utilisé pour utiliser les fonctionnalités de pagination. |

{style="table-layout:auto"}

**Réponse**

La réponse comprend un tableau pour chaque type de descripteur possédant des descripteurs définis. En d’autres termes, s’il n’existe aucun descripteur d’un certain `@type` défini, le registre ne renvoie pas de tableau vide pour ce type de descripteur.

Lors de l’utilisation de l’en-tête `link` `Accept` , chaque descripteur s’affiche sous la forme d’un élément de tableau au format `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

{style="table-layout:auto"}

**Requête**

La requête suivante récupère un descripteur par sa valeur `@id`. Les descripteurs n’ont pas de contrôle de version. Par conséquent, aucun en-tête `Accept` n’est requis dans la requête de recherche.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
  "imsOrg": "{ORG_ID}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Créer un descripteur {#create}

Vous pouvez créer un descripteur en effectuant une requête POST vers le point d’entrée `/tenant/descriptors`.

>[!IMPORTANT]
>
>Le [!DNL Schema Registry] vous permet de définir plusieurs types de descripteur différents. Chaque type de descripteur nécessite l’envoi de ses propres champs spécifiques dans le corps de la requête. Voir [annexe](#defining-descriptors) pour obtenir la liste complète des descripteurs et des champs nécessaires pour les définir.

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante définit un descripteur d’identité dans un champ « adresse e-mail » d’un exemple de schéma. Cela [!DNL Experience Platform] indique d’utiliser l’adresse e-mail comme identifiant pour aider à rassembler les informations sur l’individu.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Une réponse réussie renvoie un état HTTP 201 (Created) et les détails du nouveau descripteur, y compris son identifiant `@id`. Le `@id` est un champ en lecture seule affecté par le [!DNL Schema Registry] et utilisé pour référencer le descripteur dans l’API.

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

Vous pouvez mettre à jour un descripteur en incluant son `@id` dans le chemin d’accès d’une requête PUT.

**Format d’API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DESCRIPTOR_ID}` | L’identifiant `@id` du descripteur que vous souhaitez mettre à jour. |

{style="table-layout:auto"}

**Requête**

Cette requête réécrit essentiellement le descripteur. Par conséquent, le corps de la requête doit inclure tous les champs requis pour définir un descripteur de ce type. En d’autres termes, la payload de requête pour mettre à jour (PUT) un descripteur est identique à la payload pour [créer (POST)un descripteur](#create) du même type.

>[!IMPORTANT]
>
>Comme pour la création de descripteurs à l’aide de requêtes POST, chaque type de descripteur nécessite l’envoi de ses propres champs spécifiques dans les payloads de la requête PUT. Voir [annexe](#defining-descriptors) pour obtenir la liste complète des descripteurs et des champs nécessaires pour les définir.

L’exemple suivant met à jour un descripteur d’identité pour référencer un autre `xdm:sourceProperty` (`mobile phone`) et remplacer le `xdm:namespace` par `Phone`.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

L’exécution d’une [requête de recherche (GET)](#lookup) pour afficher le descripteur indique que les champs ont maintenant été mis à jour pour refléter les modifications envoyées dans la requête PUT.

## Supprimer un descripteur {#delete}

Il se peut que vous deviez supprimer un descripteur que vous avez défini dans le [!DNL Schema Registry]. Pour ce faire, il vous suffit d’effectuer une requête DELETE faisant référence au `@id` du descripteur que vous souhaitez supprimer.

**Format d’API**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DESCRIPTOR_ID}` | L’identifiant `@id` du descripteur que vous souhaitez supprimer. |

{style="table-layout:auto"}

**Requête**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un état HTTP 204 (Pas de contenu) et un corps vide.

Pour confirmer que le descripteur a été supprimé, vous pouvez effectuer une [requête de recherche](#lookup) par rapport au `@id` de descripteur. La réponse renvoie le statut HTTP 404 (Introuvable), car le descripteur a été supprimé du [!DNL Schema Registry].

## Annexe

La section suivante fournit des informations supplémentaires concernant l’utilisation de descripteurs dans l’API [!DNL Schema Registry].

### Définition de descripteurs {#defining-descriptors}

>[!NOTE]
>
>Le nombre maximal de descripteurs pouvant être appliqués au sandbox d’une organisation est de 4 000.

Les sections suivantes présentent les types de descripteurs disponibles, y compris les champs nécessaires pour définir un descripteur de chaque type.

>[!IMPORTANT]
>
>Vous ne pouvez pas étiqueter l’objet d’espace de noms du client, car le système appliquerait ce libellé à chaque champ personnalisé de ce sandbox. Au lieu de cela, vous devez spécifier le nœud feuille sous cet objet que vous devez étiqueter.

#### Descripteur d’identité

Un descripteur d’identité indique que la « [!UICONTROL sourceProperty] » de « [!UICONTROL sourceSchema] » est un champ de [!DNL Identity], comme décrit par [Adobe Experience Platform Identity Service](../../identity-service/home.md).

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
| `@type` | Type de descripteur en cours de définition. Pour un descripteur d’identité, cette valeur doit être définie sur `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Le chemin vers la propriété spécifique qui sera l’identité. Le chemin doit commencer et non se terminer par un « / ». N’incluez pas « properties » dans le chemin (par exemple, utilisez « /personalEmail/address » au lieu de « /properties/personalEmail/properties/address ») |
| `xdm:namespace` | La valeur `id` ou `code` de l’espace de noms de l’identité. Vous trouverez une liste d’espaces de noms à l’aide de l’[[!DNL Identity Service API]](https://developer.adobe.com/experience-platform-apis/references/identity-service) . |
| `xdm:property` | `xdm:id` ou `xdm:code` selon l’espace de noms `xdm:namespace` utilisé. |
| `xdm:isPrimary` | Une valeur booléenne facultative. Lorsqu’elle est définie sur true, le champ est l’identité principale. Les schémas ne peuvent contenir qu’une seule identité principale. |

{style="table-layout:auto"}

#### Descripteur de nom convivial {#friendly-name}

Les descripteurs de noms conviviaux permettent à l’utilisateur de modifier les valeurs `title`, `description` et `meta:enum` des champs de schéma de la bibliothèque principale. Ils sont particulièrement utiles lorsque vous utilisez des « eVars » et d’autres champs « génériques » auxquels vous souhaitez appliquer des libellés indiquant qu’ils contiennent des informations propres à votre organisation. L’interface utilisateur peut les utiliser pour afficher un nom plus convivial ou pour n’afficher que les champs dont le nom est convivial.

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
  },
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out",
    "media.ping": "Media ping"
  }
}
```

| Propriété | Description |
| --- | --- |
| `@type` | Type de descripteur en cours de définition. Pour un descripteur de nom convivial, cette valeur doit être définie sur `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Chemin d’accès à la propriété spécifique dont vous souhaitez modifier les détails. Le chemin doit commencer par une barre oblique (`/`) et ne doit pas se terminer par une barre oblique. N’incluez pas de `properties` dans le chemin d’accès (par exemple, utilisez `/personalEmail/address` au lieu de `/properties/personalEmail/properties/address`). |
| `xdm:title` | Nouveau titre que vous souhaitez afficher pour ce champ, écrit en Title Case. |
| `xdm:description` | Vous pouvez ajouter une description facultative avec le titre. |
| `meta:enum` | Si le champ indiqué par `xdm:sourceProperty` est un champ de chaîne, `meta:enum` pouvez être utilisé pour ajouter les valeurs suggérées pour le champ dans l’interface utilisateur de segmentation. Il est important de noter que `meta:enum` ne déclare pas d’énumération ni ne fournit de validation de données pour le champ XDM.<br><br>Ceci ne doit être utilisé que pour les champs XDM principaux définis par Adobe. Si la propriété source est un champ personnalisé défini par votre organisation, vous devez plutôt modifier la propriété `meta:enum` du champ directement par le biais d’une requête PATCH vers la ressource parent du champ. |
| `meta:excludeMetaEnum` | Si le champ indiqué par `xdm:sourceProperty` est un champ de chaîne qui contient des valeurs suggérées existantes fournies sous un champ de `meta:enum`, vous pouvez inclure cet objet dans un descripteur de nom convivial pour exclure certaines ou toutes ces valeurs de la segmentation. La clé et la valeur de chaque entrée doivent correspondre à celles incluses dans la `meta:enum` d’origine du champ pour que l’entrée soit exclue. |

{style="table-layout:auto"}

#### Descripteur de relation {#relationship-descriptor}

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
| `@type` | Type de descripteur en cours de définition. Pour un descripteur de relation, cette valeur doit être définie sur `xdm:descriptorOneToOne`, sauf si vous avez accès à Real-Time CDP B2B edition. Avec B2B edition, vous avez la possibilité d’utiliser `xdm:descriptorOneToOne` ou [`xdm:descriptorRelationship`](#b2b-relationship-descriptor). |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Chemin vers le champ du schéma source dans lequel la relation est définie. Doit commencer par « / » et ne pas se terminer par « / ». N’incluez pas « properties » dans le chemin (par exemple, « /personalEmail/address » au lieu de « /properties/personalEmail/properties/address »). |
| `xdm:destinationSchema` | L’URI `$id` du schéma de référence avec lequel ce descripteur définit une relation. |
| `xdm:destinationVersion` | Version majeure du schéma de référence. |
| `xdm:destinationProperty` | (Facultatif) Chemin d’accès à un champ cible dans le schéma de référence. Si cette propriété est omise, le champ cible est déterminé par les champs qui contiennent un descripteur d’identité de référence correspondant (voir ci-dessous). |

{style="table-layout:auto"}

##### Descripteur de relation B2B {#B2B-relationship-descriptor}

Le B2B edition Real-Time CDP offre une autre méthode pour définir des relations entre les schémas, ce qui permet d’établir des relations multiples-à-un. Cette nouvelle relation doit être de type `@type: xdm:descriptorRelationship` et la payload doit inclure plus de champs que la relation `@type: xdm:descriptorOneToOne`. Pour plus d’informations, consultez le tutoriel sur la [définition d’une relation de schéma pour B2B edition](../tutorials/relationship-b2b.md).

```json
{
   "@type": "xdm:descriptorRelationship",
   "xdm:sourceSchema" : "https://ns.adobe.com/{TENANT_ID}/schemas/9f2b2f225ac642570a110d8fd70800ac0c0573d52974fa9a",
   "xdm:sourceVersion" : 1,
   "xdm:sourceProperty" : "/person-ref",
   "xdm:destinationSchema" : "https://ns.adobe.com/{TENANT_ID/schemas/628427680e6b09f1f5a8f63ba302ee5ce12afba8de31acd7",
   "xdm:destinationVersion" : 1,
   "xdm:destinationProperty": "/personId",
   "xdm:destinationNamespace" : "People", 
   "xdm:destinationToSourceTitle" : "Opportunity Roles",
   "xdm:sourceToDestinationTitle" : "People",
   "xdm:cardinality": "M:1"
}
```

| Propriété | Description |
| --- | --- |
| `@type` | Type de descripteur en cours de définition. Pour les champs suivants, la valeur doit être définie sur `xdm:descriptorRelationship`. Pour plus d’informations sur les types supplémentaires, voir la section [descripteurs de relation](#relationship-descriptor). |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Chemin vers le champ du schéma source dans lequel la relation est définie. Doit commencer par « / » et ne pas se terminer par « / ». N’incluez pas « properties » dans le chemin (par exemple, « /personalEmail/address » au lieu de « /properties/personalEmail/properties/address »). |
| `xdm:destinationSchema` | L’URI `$id` du schéma de référence avec lequel ce descripteur définit une relation. |
| `xdm:destinationVersion` | Version majeure du schéma de référence. |
| `xdm:destinationProperty` | (Facultatif) Chemin d’accès à un champ cible dans le schéma de référence, qui doit être l’identifiant principal du schéma. Si cette propriété est omise, le champ cible est déterminé par les champs qui contiennent un descripteur d’identité de référence correspondant (voir ci-dessous). |
| `xdm:destinationNamespace` | Espace de noms de l’identifiant principal à partir du schéma de référence. |
| `xdm:destinationToSourceTitle` | Nom d’affichage de la relation du schéma de référence au schéma source. |
| `xdm:sourceToDestinationTitle` | Nom d’affichage de la relation du schéma source au schéma de référence. |
| `xdm:cardinality` | La relation de jointure entre les schémas. Cette valeur doit être définie sur `M:1`, en référence à une relation multiple-à-un. |

{style="table-layout:auto"}

#### Descripteur d’identité de référence

Les descripteurs d’identité de référence fournissent un contexte de référence à l’identité principale d’un champ de schéma, ce qui permet de la référencer par des champs dans d’autres schémas. Un champ d’identité principale doit déjà être défini pour que le schéma de référence puisse être référencé par d’autres schémas à l’aide de ce descripteur.

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
| `@type` | Type de descripteur en cours de définition. Pour un descripteur d’identité de référence, cette valeur doit être définie sur `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Chemin d’accès au champ du schéma source qui sera utilisé pour faire référence au schéma de référence. Doit commencer et non se terminer par un « / ». N’incluez pas de « propriétés » dans le chemin d’accès (par exemple, `/personalEmail/address` au lieu de `/properties/personalEmail/properties/address`). |
| `xdm:identityNamespace` | Le code d’espace de noms d’identité de la propriété source. |

{style="table-layout:auto"}

#### Descripteur de champ obsolète

Vous pouvez [rendre obsolète un champ dans une ressource XDM personnalisée](../tutorials/field-deprecation-api.md#custom) en ajoutant un attribut `meta:status` défini sur `deprecated` au champ en question. Toutefois, si vous souhaitez rendre obsolètes les champs fournis par les ressources XDM standard dans vos schémas, vous pouvez affecter un descripteur de champ obsolète au schéma en question pour obtenir le même effet. À l’aide de l’en-tête de `Accept` [ correct ](../tutorials/field-deprecation-api.md#verify-deprecation), vous pouvez ensuite afficher les champs standard obsolètes d’un schéma lors de la recherche dans l’API.

```json
{
  "@type": "xdm:descriptorDeprecated",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/faxPhone"
}
```

| Propriété | Description |
| --- | --- |
| `@type` | Le type de descripteur. Pour un descripteur d’obsolescence de champ, cette valeur doit être définie sur `xdm:descriptorDeprecated`. |
| `xdm:sourceSchema` | L’`$id` de l’URI du schéma auquel vous appliquez le descripteur. |
| `xdm:sourceVersion` | La version du schéma auquel vous appliquez le descripteur. Doit être définie sur `1`. |
| `xdm:sourceProperty` | Le chemin d’accès à la propriété dans le schéma auquel vous appliquez le descripteur. Si vous souhaitez appliquer le descripteur à plusieurs propriétés, vous pouvez fournir une liste de chemins d’accès sous la forme d’un tableau (par exemple, `["/firstName", "/lastName"]`). |

{style="table-layout:auto"}
