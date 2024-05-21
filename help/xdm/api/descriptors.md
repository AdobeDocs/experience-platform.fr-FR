---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre des schémas;descripteur;descripteur;descripteurs;descripteurs;identité;identité;nom convivial;nom alternatif;afficher;référence;relation;relation
solution: Experience Platform
title: Point de terminaison de l’API Descripteurs
description: Le point de terminaison /descriptors de l’API Schema Registry vous permet de gérer par programmation les descripteurs XDM dans votre application d’expérience.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 44355aa2ddf03b20aca64c6675414b73682bc2b5
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 40%

---

# Point d’entrée Descripteurs

Les schémas définissent un affichage statique des entités de données, mais ne fournissent pas de détails spécifiques sur la manière dont les données basées sur ces schémas (jeux de données, par exemple) peuvent être reliées entre elles. Adobe Experience Platform vous permet de décrire ces relations et d’autres métadonnées interprétatives relatives à un schéma à l’aide de descripteurs.

Les descripteurs de schéma sont des métadonnées au niveau du client, ce qui signifie qu’ils sont propres à votre organisation et que toutes les opérations de descripteur ont lieu dans le conteneur du client.

Une ou plusieurs entités de descripteur de schéma peuvent être appliquées à chaque schéma. Chaque entité de descripteur de schéma comprend un descripteur `@type` et le `sourceSchema` auquel il s’applique. Une fois appliqués, ces descripteurs s’appliquent à tous les jeux de données créés à l’aide du schéma.

La variable `/descriptors` du point de terminaison [!DNL Schema Registry] L’API vous permet de gérer par programmation les descripteurs dans votre application d’expérience.

## Commencer

Le point de terminaison utilisé dans ce guide fait partie du [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Avant de continuer, consultez le [guide de prise en main](./getting-started.md) pour obtenir des liens vers la documentation associée, un guide de lecture des exemples d’appels API dans ce document et des informations importantes sur les en-têtes requis pour réussir des appels vers n’importe quelle API d’Experience Platform.

## Récupération d’une liste de descripteurs {#list}

Vous pouvez répertorier tous les descripteurs définis par votre organisation en adressant une demande de GET à `/tenant/descriptors`.

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

Le format de réponse dépend de la variable `Accept` en-tête envoyé dans la requête. Notez que la variable `/descriptors` utilise des points d’entrée `Accept` en-têtes différents de tous les autres points de fin dans la variable [!DNL Schema Registry] API.

>[!IMPORTANT]
>
>Les descripteurs nécessitent des `Accept` en-têtes qui remplacent `xed` avec `xdm`, et offrent également un `link` qui est propre aux descripteurs. Le bon `Accept` des en-têtes ont été inclus dans les appels d’exemples ci-dessous, mais soyez très prudent pour vous assurer que les en-têtes corrects sont utilisés lors de l’utilisation de descripteurs.

| En-tête `Accept` | Description |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | Renvoie un tableau d’identifiants de descripteur |
| `application/vnd.adobe.xdm-link+json` | Renvoie un tableau de chemins d’API de descripteur |
| `application/vnd.adobe.xdm+json` | Renvoie un tableau d’objets de descripteurs étendus |
| `application/vnd.adobe.xdm-v2+json` | Ceci `Accept` doit être utilisé pour utiliser les fonctionnalités de pagination. |

{style="table-layout:auto"}

**Réponse**

La réponse comprend un tableau pour chaque type de descripteur possédant des descripteurs définis. En d’autres termes, s’il n’existe aucun descripteur d’un certain `@type` défini, le registre ne renvoie pas de tableau vide pour ce type de descripteur.

Lors de l’utilisation de la variable `link` `Accept` en-tête, chaque descripteur est affiché sous la forme d’un tableau au format `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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
| `{DESCRIPTOR_ID}` | La variable `@id` du descripteur que vous souhaitez rechercher. |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère un descripteur à l’aide de `@id` . Les descripteurs ne sont pas versionnés, donc pas `Accept` est requis dans la requête de recherche.

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

## Création d’un descripteur {#create}

Vous pouvez créer un descripteur en adressant une requête de POST à la fonction `/tenant/descriptors` point de terminaison .

>[!IMPORTANT]
>
>La variable [!DNL Schema Registry] vous permet de définir plusieurs types de descripteurs différents. Chaque type de descripteur nécessite l’envoi de ses propres champs spécifiques dans le corps de la requête. Voir [annexe](#defining-descriptors) pour obtenir une liste complète des descripteurs et des champs nécessaires pour les définir.

**Format d’API**

```http
POST /tenant/descriptors
```

**Requête**

La requête suivante définit un descripteur d’identité dans un champ « adresse e-mail » d’un exemple de schéma. Ceci indique : [!DNL Experience Platform] pour utiliser l’adresse électronique comme identifiant afin de faciliter l’assemblage d’informations sur l’individu.

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

Une réponse réussie renvoie un état HTTP 201 (Created) et les détails du nouveau descripteur, y compris son identifiant `@id`. La variable `@id` est un champ en lecture seule attribué par la variable [!DNL Schema Registry] et utilisé pour référencer le descripteur dans l’API.

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

## Mise à jour d’un descripteur {#put}

Vous pouvez mettre à jour un descripteur en incluant son `@id` dans le chemin d’une requête de PUT.

**Format d’API**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| Paramètre | Description |
| --- | --- |
| `{DESCRIPTOR_ID}` | L’identifiant `@id` du descripteur que vous souhaitez mettre à jour. |

{style="table-layout:auto"}

**Requête**

Cette requête réécrit essentiellement le descripteur. Le corps de la requête doit donc inclure tous les champs nécessaires pour définir un descripteur de ce type. En d’autres termes, le payload de la requête pour mettre à jour (PUT) un descripteur est identique au payload pour [créer (POST) un descripteur](#create) du même type.

>[!IMPORTANT]
>
>Comme pour la création de descripteurs à l’aide de requêtes de POST, chaque type de descripteur nécessite l’envoi de ses propres champs spécifiques dans les payloads de requête de PUT. Voir [annexe](#defining-descriptors) pour obtenir une liste complète des descripteurs et des champs nécessaires pour les définir.

L’exemple suivant met à jour un descripteur d’identité pour référencer un autre `xdm:sourceProperty` (`mobile phone`) et modifiez la variable `xdm:namespace` to `Phone`.

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

Exécution d’un [requête de recherche (GET)](#lookup) pour afficher le descripteur, indique que les champs ont désormais été mis à jour pour prendre en compte les modifications envoyées dans la demande de PUT.

## Supprimer un descripteur {#delete}

Il peut arriver que vous deviez supprimer un descripteur que vous avez défini dans la variable [!DNL Schema Registry]. Pour ce faire, effectuez une requête de DELETE en référençant la variable `@id` du descripteur que vous souhaitez supprimer.

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

Pour confirmer la suppression du descripteur, vous pouvez effectuer une [requête de recherche](#lookup) par rapport au descripteur `@id`. La réponse renvoie un état HTTP 404 (Introuvable), car le descripteur a été supprimé de la variable [!DNL Schema Registry].

## Annexe

La section suivante fournit des informations supplémentaires sur l’utilisation des descripteurs dans [!DNL Schema Registry] API.

### Définition de descripteurs {#defining-descriptors}

>[!NOTE]
>
>Le nombre maximal de descripteurs pouvant être appliqués à un schéma est de 4 000.

Les sections suivantes présentent les types de descripteurs disponibles, y compris les champs nécessaires pour définir un descripteur de chaque type.

>[!IMPORTANT]
>
>Vous ne pouvez pas étiqueter l’objet namespace du client, car le système appliquerait ce libellé à chaque champ personnalisé sur cet environnement de test. Au lieu de cela, vous devez spécifier le noeud terminal sous cet objet que vous devez étiqueter.

#### Descripteur d’identité

Un descripteur d’identité signale que la variable[!UICONTROL sourceProperty]&quot; du &quot;[!UICONTROL sourceSchema]&quot; est un [!DNL Identity] comme décrit par [Service Adobe Experience Platform Identity](../../identity-service/home.md).

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
| `@type` | Le type de descripteur en cours de définition. Pour un descripteur d’identité, cette valeur doit être définie sur `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Le chemin vers la propriété spécifique qui sera l’identité. Le chemin doit commencer et non se terminer par un « / ». N’incluez pas &quot;properties&quot; dans le chemin (par exemple, utilisez &quot;/personalEmail/address&quot; au lieu de &quot;/properties/personalEmail/properties/address&quot;) |
| `xdm:namespace` | La valeur `id` ou `code` de l’espace de noms de l’identité. Vous trouverez une liste d’espaces de noms à l’aide du [[!DNL Identity Service API]](https://developer.adobe.com/experience-platform-apis/references/identity-service). |
| `xdm:property` | `xdm:id` ou `xdm:code` selon l’espace de noms `xdm:namespace` utilisé. |
| `xdm:isPrimary` | Une valeur booléenne facultative. Lorsqu’elle est définie sur true, le champ est l’identité principale. Les schémas ne peuvent contenir qu’une seule identité principale. |

{style="table-layout:auto"}

#### Descripteur de nom convivial {#friendly-name}

Les descripteurs de nom convivial permettent à l’utilisateur de modifier la variable `title`, `description`, et `meta:enum` des champs de schéma de bibliothèque principaux. Ils sont particulièrement utiles lorsque vous utilisez des « eVars » et d’autres champs « génériques » auxquels vous souhaitez appliquer des libellés indiquant qu’ils contiennent des informations propres à votre organisation. L’interface utilisateur peut les utiliser pour afficher un nom plus convivial ou pour n’afficher que les champs dont le nom est convivial.

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
| `@type` | Le type de descripteur en cours de définition. Pour un descripteur de nom convivial, cette valeur doit être définie sur `xdm:alternateDisplayInfo`. |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Chemin d’accès à la propriété spécifique dont vous souhaitez modifier les détails. Le chemin doit commencer par une barre oblique (`/`) et ne pas se terminer par un. Ne pas inclure `properties` dans le chemin (par exemple, utilisez `/personalEmail/address` au lieu de `/properties/personalEmail/properties/address`). |
| `xdm:title` | Le nouveau titre que vous souhaitez afficher pour ce champ, écrit en Casse Titre. |
| `xdm:description` | Vous pouvez ajouter une description facultative avec le titre. |
| `meta:enum` | Si le champ indiqué par `xdm:sourceProperty` est un champ de chaîne, `meta:enum` peut être utilisé pour ajouter des valeurs suggérées pour le champ dans l’interface utilisateur de segmentation. Il est important de noter que `meta:enum` ne déclare pas d’énumération ni ne fournit de validation de données pour le champ XDM.<br><br>Cela ne doit être utilisé que pour les champs XDM principaux définis par Adobe. Si la propriété source est un champ personnalisé défini par votre organisation, vous devez modifier le `meta:enum` par le biais d’une requête de PATCH à la ressource parente du champ. |
| `meta:excludeMetaEnum` | Si le champ indiqué par `xdm:sourceProperty` est un champ de chaîne dont les valeurs suggérées existantes sont fournies sous une `meta:enum` , vous pouvez inclure cet objet dans un descripteur de nom convivial pour exclure certaines ou toutes ces valeurs de la segmentation. La clé et la valeur de chaque entrée doivent correspondre à celles incluses dans l’original. `meta:enum` du champ pour que la saisie soit exclue. |

{style="table-layout:auto"}

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
| `@type` | Le type de descripteur en cours de définition. Pour un descripteur de relation, cette valeur doit être définie sur `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Chemin vers le champ du schéma source dans lequel la relation est définie. Doit commencer et non se terminer par un « / ». N’incluez pas « properties » dans le chemin (par exemple, « /personalEmail/address » au lieu de « /properties/personalEmail/properties/address »). |
| `xdm:destinationSchema` | La variable `$id` URI du schéma de référence avec lequel ce descripteur définit une relation. |
| `xdm:destinationVersion` | La version majeure du schéma de référence. |
| `xdm:destinationProperty` | Chemin facultatif vers un champ cible dans le schéma de référence. Si cette propriété est omise, le champ cible est déterminé par les champs qui contiennent un descripteur d’identité de référence correspondant (voir ci-dessous). |

{style="table-layout:auto"}

#### Descripteur d’identité de référence

Les descripteurs d’identité de référence fournissent un contexte de référence à l’identité principale d’un champ de schéma, ce qui permet de le référencer par des champs dans d’autres schémas. Un champ d’identité principal doit déjà être défini pour le schéma de référence avant qu’il ne puisse être référencé par d’autres schémas via ce descripteur.

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
| `@type` | Le type de descripteur en cours de définition. Pour un descripteur d’identité de référence, cette valeur doit être définie sur `xdm:descriptorReferenceIdentity`. |
| `xdm:sourceSchema` | L’URI `$id` du schéma dans lequel le descripteur est défini. |
| `xdm:sourceVersion` | La version principale du schéma source. |
| `xdm:sourceProperty` | Chemin d’accès au champ du schéma source qui sera utilisé pour faire référence au schéma de référence. Doit commencer et non se terminer par un « / ». N’incluez pas &quot;properties&quot; dans le chemin (par exemple, `/personalEmail/address` au lieu de `/properties/personalEmail/properties/address`). |
| `xdm:identityNamespace` | Le code d’espace de noms d’identité de la propriété source. |

{style="table-layout:auto"}

#### Descripteur de champ obsolète

Vous pouvez [abandon d’un champ dans une ressource XDM personnalisée](../tutorials/field-deprecation-api.md#custom) en ajoutant une `meta:status` définie sur `deprecated` sur le champ en question. Toutefois, si vous souhaitez abandonner les champs fournis par les ressources XDM standard dans vos schémas, vous pouvez affecter un descripteur de champ obsolète au schéma en question pour obtenir le même effet. En utilisant la variable [correct `Accept` header](../tutorials/field-deprecation-api.md#verify-deprecation), vous pouvez ensuite afficher les champs standard obsolètes pour un schéma lors de sa recherche dans l’API.

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
