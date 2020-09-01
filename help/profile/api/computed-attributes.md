---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Attributs calculés - API Profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '2403'
ht-degree: 83%

---


# (Alpha) Point de terminaison des attributs calculés

>[!IMPORTANT]
>
>La fonctionnalité d’attribut calculé décrite dans ce document est actuellement en version alpha et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Les attributs calculés vous permettent de calculer automatiquement la valeur des champs en fonction d’autres valeurs, calculs et expressions. Les attributs calculés fonctionnent au niveau du profil, ce qui signifie que vous pouvez agréger des valeurs sur tous les enregistrements et tous les événements.

Chaque attribut calculé contient une expression, ou « règle », qui évalue les données entrantes et stocke la valeur obtenue dans un attribut de profil ou dans un événement. Ces calculs vous aident à répondre facilement aux questions liées à des éléments tels que la valeur d’achat de durée de vie, le temps écoulé entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que ces informations sont nécessaires.

Ce guide vous aidera à mieux comprendre les attributs calculés dans Adobe Experience Platform et comprend des exemples d’appels API pour effectuer des opérations de création, de lecture, de mise à jour et de suppression de base à l’aide du point de terminaison `/config/computedAttributes`.

## Prise en main

The API endpoint used in this guide is part of the [Real-time Customer Profile API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Avant de continuer, consultez le guide [de](getting-started.md) prise en main pour obtenir des liens vers la documentation connexe, un guide pour lire les exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute [!DNL Experience Platform] API.

## Comprendre les attributs calculés

Adobe Experience Platform enables you to easily import and merge data from multiple sources in order to generate [!DNL Real-time Customer Profiles]. Chaque profil contient des informations importantes liées à une personne, comme ses coordonnées de contact, ses préférences et son historique d’achat, vous offrant une vision à 360 degrés du client.

Certaines des informations collectées dans le profil sont facilement comprises lorsque vous lisez directement les champs de données (par exemple, « prénom ») tandis que d’autres données nécessitent la réalisation de plusieurs calculs ou comptent sur d’autres champs et d’autres valeurs afin de générer les informations (par exemple, « total d’achat depuis le début »). To make this data easier to understand at a glance, [!DNL Platform] allows you to create **[!UICONTROL computed attributes]** that automatically perform these references and calculations, returning the value in the appropriate field.

Les attributs calculés incluent la création d’une expression ou « règle » qui agit sur les données entrantes et conserve la valeur obtenue dans un attribut de profil ou dans un événement. Les expressions peuvent être définies de plusieurs manières différentes, ce qui vous permet de préciser qu’une règle n’évalue que les événements entrants, un événement entrant et les données du profil ou un événement entrant, les données du profil et les événements historiques.

### Cas d’utilisation

Les cas d’utilisation des attributs calculés peuvent aller de calculs simples à des références très complexes. Voici quelques exemples de cas d’utilisation des attributs calculés :

1. **[!UICONTROL Pourcentages]:** Un attribut calculé simple peut inclure la prise de deux champs numériques sur un enregistrement et leur division pour créer un pourcentage. Par exemple, vous pouvez prendre le nombre total d’e-mails envoyés à un destinataire et le diviser par le nombre d’e-mails que ce destinataire a ouvert. Un simple coup d’œil au champ attribut calculé obtenu donnerait rapidement le pourcentage total d’e-mails ouvert par ce destinataire.
1. **[!UICONTROL Utilisation]de l&#39;application :** Un autre exemple inclut la possibilité d’agrégat du nombre d’ouvertures d’une application par un utilisateur. En suivant le nombre total d’ouvertures de l’application, en fonction des événements d’ouverture individuels, vous pourriez diffuser des offres spéciales ou des messages aux utilisateurs à leur centième ouverture pour encourager un engagement plus approfondi avec votre marque.
1. **[!UICONTROL Valeurs]de durée de vie :** Il peut s’avérer très difficile de rassembler des totaux d’exécution, tels qu’une valeur d’achat à vie pour un client. Cela nécessite la mise à jour de l’historique total chaque fois qu’un nouvel événement d’achat se produit. Un attribut calculé vous permet de faire ceci beaucoup plus facilement en conservant la valeur de durée de vie dans un champ unique qui est mis à jour automatiquement à chaque événement d’achat réussi associé au client.

## Configuration d’un attribut calculé

Pour configurer un attribut calculé, vous devez d’abord identifier le champ dans lequel la valeur d’attribut calculé sera conservée. Vous pouvez créer ce champ à l’aide d’un mixin qui ajoutera le champ à un schéma existant ou en sélectionnant un champ que vous avez déjà défini dans un schéma.

>[!NOTE]
>
>Il n’est pas possible d’ajouter des attributs calculés à des champs au sein de mixins définis par Adobe. Le champ doit se trouver dans l’espace de noms `tenant`, ce qui signifie qu’il doit s’agir d’un champ que vous définissez et ajoutez à un schéma.

In order to successfully define a computed attribute field, the schema must be enabled for [!DNL Profile] and appear as part of the union schema for the class upon which the schema is based. For more information on [!DNL Profile]-enabled schemas and unions, please review the section of the [!DNL Schema Registry] developer guide section on [enabling a schema for Profile and viewing union schemas](../../xdm/api/getting-started.md). Nous vous recommandons également de consulter la [section relative aux unions](../../xdm/schema/composition.md) dans la documentation des principes de base de la composition des schémas.

The workflow in this tutorial uses a [!DNL Profile]-enabled schema and follows the steps for defining a new mixin containing the computed attribute field and ensuring it is the correct namespace. Si vous disposez déjà d’un champ qui se trouve dans l’espace de noms correct dans un schéma activé dans Profile, vous pouvez passer directement à l’étape de [création d’un attribut calculé](#create-a-computed-attribute).

### Affichage d’un schéma

Les étapes qui suivent utilisent l’interface utilisateur d’Adobe Experience Platform pour localiser un schéma, ajouter un mixin et définir un champ. If you prefer to use the [!DNL Schema Registry] API, please refer to the [Schema Registry developer guide](../../xdm/api/getting-started.md) for steps on how to create a mixin, add a mixin to a schema, and enable a schema for use with [!DNL Real-time Customer Profile].

Dans l’interface utilisateur, cliquez sur **[!UICONTROL Schémas]** dans le rail de gauche et utilisez la barre de recherche dans l’onglet **[!UICONTROL Parcourir]** pour trouver rapidement le schéma que vous souhaitez mettre à jour.

![](../images/computed-attributes/Schemas-Browse.png)

Once you have located the schema, click its name to open the [!DNL Schema Editor] where you can make edits to the schema.

![](../images/computed-attributes/Schema-Editor.png)

### Création d’un mixin

Pour créer un nouveau mixin, cliquez sur **[!UICONTROL Ajouter]** en regard de *Mixins* dans la section **[!UICONTROL Composition]** située à gauche de l’éditeur. Cela ouvre la boîte de dialogue **[!UICONTROL Ajouter un mixin]** dans laquelle les mixins existants s’affichent. Cliquez sur le bouton radio **[!UICONTROL Créer un nouveau mixin]** qui vous permet de définir votre nouveau mixin.

Donnez un nom et une description au mixin, puis cliquez sur **[!UICONTROL Ajouter un mixin]** lorsque vous avez terminé.

![](../images/computed-attributes/Add-mixin.png)

### Ajout d’un champ attribut calculé au schéma

Votre nouveau mixin devrait maintenant apparaître dans la section **[!UICONTROL Mixins]** en dessous de **[!UICONTROL Composition]**. Click on the name of the mixin and multiple **[!UICONTROL Add field]** buttons will appear in the *[!UICONTROL Structure]** section of the editor.

Sélectionnez **[!UICONTROL Ajouter un champ]** en regard du nom du schéma afin d’ajouter un champ de niveau supérieur. Vous pouvez également ajouter le champ n’importe où dans le schéma que vous préférez.

Après avoir cliqué sur **[!UICONTROL Ajouter un champ]**, un nouvel objet portant l’identifiant du client s’ouvre et affiche que ce champ se trouve dans le bon espace de noms. Dans cet objet, un **[!UICONTROL Nouveau champ]** apparaît. Il s’agit du champ dans lequel vous définirez l’attribut calculé.

![](../images/computed-attributes/New-field.png)

### Configuration du champ

À l’aide de la section **[!UICONTROL Propriétés du champ]** située sur le côté droit de l’éditeur, renseignez les informations nécessaires pour votre nouveau champ, notamment son nom, son nom d’affichage et son type.

>[!NOTE]
>
>Le type de champ doit être identique à celui de la valeur de l’attribut calculé. Par exemple, si la valeur de l’attribut calculé est une chaîne, le champ défini dans le schéma doit être une chaîne.

Une fois que vous avez terminé, cliquez sur **[!UICONTROL Appliquer]** et le nom du champ, ainsi que son type, s’afficheront dans la section **[!UICONTROL Structure]** de l’éditeur.

![](../images/computed-attributes/Apply.png)

### Enable schema for [!DNL Profile]

Avant de poursuivre, assurez-vous que le schéma a été activé dans [!DNL Profile]. Cliquez sur le nom du schéma dans la section **[!UICONTROL Structure]** de l’éditeur pour faire apparaître l’onglet **[!UICONTROL Propriétés du schéma]**. If the **[!UICONTROL Profile]** slider is blue, the schema has been enabled for [!DNL Profile].

>[!NOTE]
>
>Enabling a schema for [!DNL Profile] cannot be undone, so if you click on the slider once it has been enabled, you do not have to risk disabling it.

![](../images/computed-attributes/Profile.png)

Vous pouvez cliquer à présent sur **[!UICONTROL Enregistrer]** pour enregistrer le schéma mis à jour et poursuivre avec le reste du tutoriel d’utilisation de l’API.

### Création d’un attribut calculé {#create-a-computed-attribute}

With your computed attribute field identified, and confirmation that the schema is enabled for [!DNL Profile], you can now configure a computed attribute.

Commencez par effectuer une requête POST sur le point de terminaison `/config/computedAttributes` avec un corps de requête contenant les détails de l’attribut calculé que vous souhaitez créer.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
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
| `expression.value` | Expression valide [!DNL Profile Query Language] (PQL). Pour plus d’informations sur PQL et les liens vers les requêtes prises en charge, veuillez lire la [présentation de PQL](../../segmentation/pql/overview.md). |
| `schema.name` | La classe sur laquelle le schéma contenant le champ attribut calculé est basé. Par exemple : `_xdm.context.experienceevent` pour un schéma basé sur la classe XDM ExperienceEvent. |

**Réponse**

Un attribut calculé créé avec succès renvoie un état HTTP 200 (OK) et un corps de réponse contenant les détails de l’attribut calculé que vous venez de créer. Ces détails incluent un `id` unique, en lecture seule, généré par le système que vous pouvez utiliser pour faire référence à l’attribut calculé pendant les autres opérations API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
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

| Propriété | Description |
|---|---|
| `id` | Un identifiant unique, en lecture seule, généré par le système que vous pouvez utiliser pour faire référence à l’attribut calculé pendant les autres opérations API. |
| `imsOrgId` | L’organisation IMS associée à l’attribut calculé doit correspondre à la valeur envoyée dans la requête. |
| `sandbox` | L’objet Environnement de test contient des détails sur l’environnement de test sur lequel l’attribut calculé a été configuré. Ces informations sont tirées de l’en-tête de l’environnement de test envoyé dans la requête. Pour plus d’informations, consultez la [présentation des environnements de test](../../sandboxes/home.md). |
| `positionPath` | Un tableau contenant le `path` déconstruit vers le champ envoyé dans la requête. |
| `returnSchema.meta:xdmType` | Le type du champ dans lequel l’attribut calculé sera stocké. |
| `definedOn` | Un tableau affichant les schémas d’union sur lesquels l’attribut calculé a été défini. Contient un objet par schéma d’union, ce qui signifie qu’il peut y avoir plusieurs objets dans le tableau si l’attribut calculé a été ajouté à plusieurs schémas selon différentes classes. |
| `active` | Une valeur booléenne affichant si l’attribut calculé est actuellement actif ou non. Par défaut, la valeur est `true`. |
| `type` | Le type de ressource créé, dans la case « ComputedAttribute » est la valeur par défaut. |
| `createEpoch` et `updateEpoch` | L’heure à laquelle l’attribut calculé a été respectivement créé et mis à jour pour la dernière fois. |


## Accès aux attributs calculés

Lorsque vous travaillez avec des attributs calculés en utilisant l’API, vous avez deux options pour accéder aux attributs calculés définis par votre organisation. La première consiste à répertorier tous les attributs calculés, la seconde à afficher un attribut calculé spécifique selon son `id` unique.

Les étapes permettant de répertorier tous les attributs calculés et d’afficher un attribut calculé spécifique sont soulignées dans les sections qui suivent.

### Liste des attributs calculés {#list-computed-attributes}

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

Une réponse réussie inclut un attribut `_page` qui fournit le nombre total d’attributs calculés (`totalCount`) et le nombre d’attributs calculés sur la page (`pageSize`).

La réponse inclut également un tableau `children` composé d’un ou de plusieurs objets qui contiennent chacun les détails d’un attribut calculé. Si votre organisation ne dispose pas d’attribut calculé, le `totalCount` et `pageSize` seront de 0 (zéro) et le tableau `children` sera vide.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
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
            "imsOrgId": "{IMS_ORG}",
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
                "type" : "PQL", 
                "format" : "pql/text", 
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

Vous pouvez également afficher un attribut calculé spécifique en effectuant une requête GET sur le point de terminaison `/config/computedAttributes` et en incluant l’identifiant d’attribut calculé dans le chemin d’accès.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Réponse**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
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

Cette requête utilise le [format du correctif JSON](http://jsonpatch.com/) pour mettre à jour la « valeur » du champ « expression ».

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Propriété | Description |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Expression valide [!DNL Profile Query Language] (PQL). Pour plus d’informations sur PQL et les liens vers les requêtes prises en charge, veuillez lire la [présentation de PQL](../../segmentation/pql/overview.md). |

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
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Réponse**

Une requête de suppression réussie renvoie un état HTTP 200 (OK) et un corps de réponse vide. Pour confirmer que la suppression a réussi, vous pouvez effectuer une requête GET pour rechercher l’attribut calculé à l’aide de son identifiant. Si l’attribut a été supprimé, vous recevrez un état HTTP 404 (Not Found).

## Étapes suivantes

Maintenant que vous avez appris les bases des attributs calculés, vous êtes prêt à commencer à les définir pour votre organisation.