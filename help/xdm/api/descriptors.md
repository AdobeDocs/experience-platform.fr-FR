---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre de schémas;registre de schémas;descripteur;descripteur;descripteurs;descripteurs;identité;Identité;nom convivial;alternatedisplayinfo;référence;référence;relation;Relation
solution: Experience Platform
title: Point d’entrée de l’API Descriptors
description: Le point d’entrée /descriptors dans l’API Schema Registry vous permet de gérer par programmation les descripteurs XDM dans votre application d’expérience.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 57981d2e4306b2245ce0c1cdd9f696065c508a1d
workflow-type: tm+mt
source-wordcount: '2916'
ht-degree: 25%

---

# Point d’entrée des descripteurs

Les schémas définissent la structure des entités de données, mais ne spécifient pas la manière dont les jeux de données créés à partir de ces schémas sont liés les uns aux autres. Dans Adobe Experience Platform, vous pouvez utiliser des descripteurs pour décrire ces relations et ajouter des métadonnées interprétatives à un schéma.

Les descripteurs sont des objets de métadonnées au niveau du client appliqués aux schémas dans Adobe Experience Platform. Ils définissent des relations structurelles, des clés et des champs comportementaux (tels que la date et l’heure ou le contrôle de version) qui influencent la manière dont les données sont validées, jointes ou interprétées en aval.

Un schéma peut comporter un ou plusieurs descripteurs. Chaque descripteur définit un `@type` et le `sourceSchema` auquel il s’applique. Le descripteur s’applique automatiquement à tous les jeux de données créés à partir de ce schéma.

Dans Adobe Experience Platform, un descripteur est une métadonnée qui ajoute des règles comportementales ou une signification structurelle à un schéma.
Il existe plusieurs types de descripteurs, notamment :

- [Descripteur d’identité](#identity-descriptor) - marque un champ comme identité
- [descripteur de clé de Principal ](#primary-key-descriptor) - applique l&#39;unicité
- [Descripteur de relation](#relationship-descriptor) - Définit une jointure de clé étrangère.
- [ Autre descripteur d’informations d’affichage ](#friendly-name) - permet de renommer un champ de l’interface utilisateur
- Descripteurs [Version](#version-descriptor) et [horodatage](#timestamp-descriptor) : suivez l’ordre des événements et la détection des modifications

Le point d’entrée `/descriptors` de l’API [!DNL Schema Registry] vous permet de gérer par programmation les descripteurs dans votre application d’expérience.

## Commencer

Le point d’entrée utilisé dans ce guide fait partie de l’API [[!DNL Schema Registry] ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

Outre les descripteurs standard, le [!DNL Schema Registry] prend en charge les types de descripteurs pour les schémas relationnels, tels que **clé primaire**, **version** et **horodatage**. Ils assurent l’unicité, contrôlent le contrôle de version et définissent des champs de série temporelle au niveau du schéma. Si vous ne connaissez pas les schémas relationnels, consultez la présentation de Data Mirror [](../data-mirror/overview.md) et la [référence technique des schémas relationnels](../schema/relational.md) avant de continuer.

>[!NOTE]
>
>Dans les versions antérieures de la documentation de Adobe Experience Platform, les schémas relationnels étaient auparavant appelés schémas basés sur des modèles. La fonctionnalité de descripteur et les points d’entrée de l’API restent inchangés. Seule la terminologie a été mise à jour pour plus de clarté.

>[!IMPORTANT]
>
>Voir l’[annexe](#defining-descriptors) pour plus d’informations sur tous les types de descripteur.

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

Pour afficher les détails d’un descripteur spécifique, envoyez une requête GET à l’aide de son `@id` .

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

## Annexe {#appendix}

La section suivante fournit des informations supplémentaires concernant l’utilisation de descripteurs dans l’API [!DNL Schema Registry].

### Définition de descripteurs {#defining-descriptors}

>[!NOTE]
>
>Le nombre maximal de descripteurs pouvant être appliqués au sandbox d’une organisation est de 4 000.

Les sections suivantes présentent les types de descripteurs disponibles, y compris les champs nécessaires pour définir un descripteur de chaque type.

>[!IMPORTANT]
>
>Vous ne pouvez pas étiqueter l’objet d’espace de noms du client, car le système appliquerait ce libellé à chaque champ personnalisé de ce sandbox. Au lieu de cela, vous devez spécifier le nœud feuille sous cet objet que vous devez étiqueter.

#### Descripteur d’identité {#identity-descriptor}

Un descripteur d’identité indique que le « [!UICONTROL sourceProperty] » du « [!UICONTROL sourceSchema] » est un champ [!DNL Identity], comme décrit par [Experience Platform Identity Service](../../identity-service/home.md).

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

Les descripteurs de relation décrivent une relation entre deux schémas différents, en fonction des propriétés décrites dans `xdm:sourceProperty` et `xdm:destinationProperty`. Pour plus d’informations, consultez le tutoriel sur [la définition d’une relation entre deux schémas](../tutorials/relationship-api.md).

Utilisez ces propriétés pour déclarer la manière dont un champ source (clé étrangère) est associé à un champ de destination ([clé primaire](#primary-key-descriptor) ou clé candidate).

>[!TIP]
>
>Une **clé étrangère** est un champ du schéma source (défini par `xdm:sourceProperty`) qui fait référence à un champ de clé d’un autre schéma. Une **clé candidate** est tout champ (ou ensemble de champs) du schéma de destination qui identifie de manière unique un enregistrement et peut être utilisé à la place de la clé primaire.

L’API prend en charge deux modèles :

- `xdm:descriptorOneToOne` : relation standard 1:1
- `xdm:descriptorRelationship` : modèle général pour les nouveaux schémas de travail et relationnels (prend en charge les cibles de cardinalité, de dénomination et de clés non primaires).

##### Relation un-à-un (schémas standard)

Utilisez-le lors de la maintenance des intégrations de schémas standard existantes qui reposent déjà sur `xdm:descriptorOneToOne`.

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

Le tableau suivant décrit les champs requis pour définir un descripteur de relation un-à-un.

| Propriété | Description |
| --- | --- |
| `@type` | Type de descripteur en cours de définition. Pour un descripteur de relation, cette valeur doit être définie sur `xdm:descriptorOneToOne`, sauf si vous avez accès à Real-Time CDP B2B edition. Avec B2B edition, vous avez la possibilité d’utiliser `xdm:descriptorOneToOne` ou [`xdm:descriptorRelationship`](#b2b-relationship-descriptor). |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Chemin vers le champ du schéma source dans lequel la relation est définie. Doit commencer par « / » et ne pas se terminer par « / ». N’incluez pas « properties » dans le chemin (par exemple, « /personalEmail/address » au lieu de « /properties/personalEmail/properties/address »). |
| `xdm:destinationSchema` | L’URI `$id` du schéma de référence avec lequel ce descripteur définit une relation. |
| `xdm:destinationVersion` | Version majeure du schéma de référence. |
| `xdm:destinationProperty` | (Facultatif) Chemin d’accès à un champ cible dans le schéma de référence. Si cette propriété est omise, le champ cible est déterminé par les champs qui contiennent un descripteur d’identité de référence correspondant (voir ci-dessous). |

##### Relation générale (schémas relationnels et recommandé pour les nouveaux projets)

Utilisez ce descripteur pour toutes les nouvelles mises en œuvre et pour les schémas relationnels. Il vous permet de définir la cardinalité de la relation (par exemple un-à-un ou plusieurs-à-un), de spécifier des noms de relation et de créer un lien vers un champ de destination qui n’est pas la clé primaire (clé non primaire).

Les exemples suivants montrent comment définir un descripteur de relation général.

**Exemple minimal :**

Cet exemple minimal comprend uniquement les champs requis pour définir une relation multiple-à-un entre deux schémas.

```json
{
  "@type": "xdm:descriptorRelationship",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceProperty": "/customer_ref",
  "xdm:sourceVersion": 1,
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:cardinality": "M:1"
}
```

**Exemple avec tous les champs facultatifs :**

Cet exemple inclut tous les champs facultatifs, tels que les noms de relation, les titres d’affichage et un champ de destination de clé non primaire explicite.

```json
{
  "@type": "xdm:descriptorRelationship",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/customer_ref",
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:destinationProperty": "/customer_id",
  "xdm:sourceToDestinationName": "CampaignToCustomer",
  "xdm:destinationToSourceName": "CustomerToCampaign",
  "xdm:sourceToDestinationTitle": "Customer campaigns",
  "xdm:destinationToSourceTitle": "Campaign customers",
  "xdm:cardinality": "M:1"
}
```

##### Choix d’un descripteur de relation

Suivez les instructions suivantes pour choisir le descripteur de relation à appliquer :

| Situation | Descripteur à utiliser |
| --------------------------------------------------------------------- | ----------------------------------------- |
| Nouveaux schémas de travail ou relationnels | `xdm:descriptorRelationship` |
| Mappage 1:1 existant dans les schémas standard | Continuez à utiliser `xdm:descriptorOneToOne` sauf si vous avez besoin de fonctionnalités prises en charge uniquement par `xdm:descriptorRelationship`. |
| cardinalité multiple-à-un ou facultative (`1:1`, `1:0`, `M:1`, `M:0`) | `xdm:descriptorRelationship` |
| Noms ou titres de relation nécessaires pour la lisibilité de l’interface utilisateur/en aval | `xdm:descriptorRelationship` |
| Cible de destination requise autre qu’une identité | `xdm:descriptorRelationship` |

>[!NOTE]
>
>Pour les descripteurs de `xdm:descriptorOneToOne` existants dans les schémas standard, continuez à les utiliser, à moins que vous n’ayez besoin de fonctionnalités telles que les cibles de destination d’identité non principales, les noms personnalisés ou les options de cardinalité étendue.

##### Comparaison des fonctionnalités

Le tableau suivant compare les fonctionnalités des deux types de descripteur :

| Fonctionnalité | `xdm:descriptorOneToOne` | `xdm:descriptorRelationship` |
| ------------------ | ------------------------ | ------------------------------------------------------------------------ |
| Cardinalité | 1:1 | 1:1, 1:0, M:1, M:0 (informatif) |
| Cible de destination | Champ Identité/Explicite | Clé de Principal par défaut, ou clé non primaire via `xdm:destinationProperty` |
| Nommage de champs | Non pris en charge | `xdm:sourceToDestinationName`, `xdm:destinationToSourceName` et titres |
| Ajustement relationnel | Limité | Modèle de Principal pour les schémas relationnels |

##### Contraintes et validation

Suivez ces exigences et recommandations lors de la définition d’un descripteur de relation général :

- Pour les schémas relationnels, placez le champ source (clé étrangère) au niveau racine. Il s’agit d’une limitation technique actuelle pour l’ingestion, et pas seulement d’une recommandation de bonne pratique.
- Assurez-vous que les types de données des champs source et de destination sont compatibles (numérique, date, booléen, chaîne).
- N&#39;oubliez pas que la cardinalité est informative et que le stockage ne l&#39;applique pas. Spécifiez la cardinalité au format `<source>:<destination>`. Les valeurs acceptées sont : `1:1`, `1:0`, `M:1` ou `M:0`.

#### descripteur de clé de Principal {#primary-key-descriptor}

Le descripteur de clé primaire (`xdm:descriptorPrimaryKey`) applique des contraintes d’unicité et non nulles à un ou plusieurs champs d’un schéma.

```json
{
  "@type": "xdm:descriptorPrimaryKey",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": ["/orderId", "/orderLineId"]
}
```

| Propriété | Description |
| -------------------- | ----------------------------------------------------------------------------- |
| `@type` | Doit être `xdm:descriptorPrimaryKey`. |
| `xdm:sourceSchema` | `$id` URI du schéma. |
| `xdm:sourceProperty` | Pointeurs JSON vers le ou les champs de clé primaire. Utilisez un tableau pour les clés composites. Pour les schémas de série temporelle, la clé composite doit inclure le champ d’horodatage pour garantir l’unicité des enregistrements d’événement. |

#### Descripteur de version {#version-descriptor}

>[!NOTE]
>
>Dans l’éditeur de schémas de l’interface utilisateur, le descripteur de version s’affiche sous la forme « [!UICONTROL Version identifier] ».

Le descripteur de version (`xdm:descriptorVersion`) désigne un champ pour détecter et empêcher les conflits d’événements de modification dans le désordre.

```json
{
  "@type": "xdm:descriptorVersion",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": "/versionNumber"
}
```

| Propriété | Description |
| -------------------- | ------------------------------------------------------------- |
| `@type` | Doit être `xdm:descriptorVersion`. |
| `xdm:sourceSchema` | `$id` URI du schéma. |
| `xdm:sourceProperty` | Pointeur JSON vers le champ de version. Doit être marqué `required`. |

#### Descripteur d’horodatage {#timestamp-descriptor}

>[!NOTE]
>
>Dans l’éditeur de schéma de l’interface utilisateur, le descripteur d’horodatage s’affiche sous la forme « [!UICONTROL Timestamp identifier] ».

Le descripteur d’horodatage (`xdm:descriptorTimestamp`) désigne un champ date et heure comme horodatage pour les schémas avec `"meta:behaviorType": "time-series"`.

```json
{
  "@type": "xdm:descriptorTimestamp",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": "/eventTime"
}
```

| Propriété | Description |
| -------------------- | ------------------------------------------------------------------------------------------ |
| `@type` | Doit être `xdm:descriptorTimestamp`. |
| `xdm:sourceSchema` | `$id` URI du schéma. |
| `xdm:sourceProperty` | Pointeur JSON vers le champ d’horodatage. Doit être marqué `required` et être de type `date-time`. |

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
| `xdm:destinationProperty` | (Facultatif) Chemin d’accès à un champ cible dans le schéma de référence. Elle doit être résolue sur l’identifiant principal du schéma, ou sur un autre champ avec un type de données compatible à `xdm:sourceProperty`. Si cet attribut est omis, la relation risque de ne pas fonctionner comme prévu. |
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

Vous pouvez [rendre obsolète un champ dans une ressource XDM personnalisée](../tutorials/field-deprecation-api.md#custom) en ajoutant un attribut `meta:status` défini sur `deprecated` au champ en question. Toutefois, si vous souhaitez rendre obsolètes les champs fournis par les ressources XDM standard dans vos schémas, vous pouvez affecter un descripteur de champ obsolète au schéma en question pour obtenir le même effet. À l’aide de l’en-tête de [ `Accept` correct ](../tutorials/field-deprecation-api.md#verify-deprecation), vous pouvez ensuite afficher les champs standard obsolètes d’un schéma lors de la recherche dans l’API.

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
