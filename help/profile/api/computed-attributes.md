---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide du développeur de l’API de Profil client en temps réel
topic: guide
translation-type: tm+mt
source-git-commit: d464a6b4abd843f5f8545bc3aa8000f379a86c6d
workflow-type: tm+mt
source-wordcount: '2431'
ht-degree: 1%

---


# (Alpha) Point de terminaison des attributs calculés

>[!IMPORTANT]
>La fonctionnalité d&#39;attribut calculée décrite dans ce document est actuellement en alpha et n&#39;est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Les attributs calculés vous permettent de calculer automatiquement la valeur des champs en fonction d’autres valeurs, calculs et expressions. Les attributs calculés fonctionnent au niveau du profil, ce qui signifie que vous pouvez agrégat des valeurs sur tous les enregistrements et événements.

Chaque attribut calculé contient une expression, ou &quot;règle&quot;, qui évalue les données entrantes et stocke la valeur résultante dans un attribut de profil ou dans un événement. Ces calculs vous permettent de répondre facilement aux questions relatives à des éléments tels que la valeur d’achat sur toute la durée de vie, le délai entre les achats ou le nombre d’ouvertures de l’application, sans que vous ayez à effectuer manuellement des calculs complexes chaque fois que les informations sont nécessaires.

Ce guide vous aidera à mieux comprendre les attributs calculés dans l’Adobe Experience Platform et inclut des exemples d’appels d’API pour effectuer des opérations CRUD de base à l’aide du `/config/computedAttributes` point de terminaison.

## Prise en main

Le point de terminaison API utilisé dans ce guide fait partie de l’API [Profil client en temps](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)réel. Avant de continuer, consultez le guide [de](getting-started.md) prise en main pour obtenir des liens vers la documentation connexe, un guide pour lire les exemples d&#39;appels d&#39;API dans ce document et des informations importantes concernant les en-têtes requis nécessaires pour passer des appels à toute API Experience Platform.

## Présentation des attributs calculés

L’Adobe Experience Platform vous permet d’importer et de fusionner facilement des données provenant de plusieurs sources afin de générer des Profils client en temps réel. Chaque profil contient des informations importantes relatives à une personne, telles que ses coordonnées, ses préférences et son historique d&#39;achat, ce qui lui permet d&#39;obtenir une vue de 360 degrés du client.

Certaines informations collectées dans le profil sont facilement comprises lors de la lecture directe des champs de données (par exemple, &quot;prénom&quot;), tandis que d’autres données nécessitent plusieurs calculs ou l’utilisation d’autres champs et valeurs pour générer les informations (par exemple, &quot;total des achats sur toute la durée de vie&quot;). Pour faciliter la compréhension de ces données d’un seul coup d’oeil, Platform vous permet de créer des attributs **** calculés qui effectuent automatiquement ces références et calculs, renvoyant la valeur dans le champ approprié.

Les attributs calculés incluent la création d’une expression, ou &quot;règle&quot;, qui fonctionne sur les données entrantes et stocke la valeur résultante dans un attribut ou un événement de profil. Les Expressions peuvent être définies de plusieurs manières différentes, ce qui vous permet de spécifier qu’une règle évalue les événements entrants uniquement, un événement et des données de profil entrants ou un événement, des données de profil et des événements historiques entrants.

### Cas d’utilisation

Les cas d’utilisation des attributs calculés peuvent aller de calculs simples à des références très complexes. Voici quelques exemples d’utilisation des attributs calculés :

1. **Pourcentages :** Un attribut calculé simple peut inclure la prise de deux champs numériques sur un enregistrement et leur division pour créer un pourcentage. Par exemple, vous pouvez prendre le nombre total de courriers électroniques envoyés à un individu et le diviser par le nombre de courriers électroniques ouverts par ce dernier. Si vous examinez le champ d’attribut calculé qui en résulte, le pourcentage du nombre total de courriers électroniques ouverts par l’utilisateur est rapidement affiché.
1. **Utilisation de l&#39;application :** Un autre exemple inclut la possibilité d’agrégat du nombre d’ouvertures d’une application par un utilisateur. En suivant le nombre total d’ouvertures de l’application, en fonction de événements d’ouverture individuels, vous pouvez fournir des offres ou des messages spéciaux aux utilisateurs lors de leur 100e ouverture, ce qui encourage un engagement plus profond envers votre marque.
1. **Valeurs de durée de vie :** Il peut s’avérer très difficile de rassembler des totaux d’exécution, tels qu’une valeur d’achat à vie pour un client. Cela nécessite la mise à jour du total historique chaque fois qu’un nouveau événement d’achat se produit. Un attribut calculé vous permet de le faire beaucoup plus facilement en conservant la valeur de durée de vie dans un seul champ qui est mis à jour automatiquement après chaque événement d&#39;achat réussi lié au client.

## Configurer un attribut calculé

Pour configurer un attribut calculé, vous devez d’abord identifier le champ qui contiendra la valeur de l’attribut calculé. Ce champ peut être créé à l’aide d’un mixin pour ajouter le champ à un schéma existant ou en sélectionnant un champ que vous avez déjà défini dans un schéma.

>[!NOTE]
>Les attributs calculés ne peuvent pas être ajoutés aux champs des mixins définis par Adobe. Le champ doit se trouver dans l’ `tenant` espace de nommage, ce qui signifie qu’il doit s’agir d’un champ que vous définissez et ajoutez à un schéma.

Pour définir avec succès un champ d&#39;attribut calculé, le schéma doit être activé pour le Profil et apparaître dans le schéma d&#39;union pour la classe sur laquelle le schéma est basé. Pour plus d&#39;informations sur les schémas et unions activés pour le Profil, veuillez consulter la section du guide du développeur du registre des Schémas sur l&#39; [activation d&#39;un schéma pour le Profil et l&#39;affichage de schémas](../../xdm/api/getting-started.md)d&#39;union. Il est également recommandé d&#39;examiner la [section relative aux unions](../../xdm/schema/composition.md) dans la documentation de base sur la composition des schémas.

Le flux de travaux de ce didacticiel utilise un schéma compatible Profil et suit les étapes de définition d’un nouveau mixin contenant le champ d’attribut calculé et s’assurant qu’il s’agit de l’espace de nommage correct. Si un champ se trouve déjà dans l’espace de nommage correct dans un schéma compatible Profil, vous pouvez passer directement à l’étape de [création d’un attribut](#create-a-computed-attribute)calculé.

### Vue d’un schéma

Les étapes qui suivent utilisent l’interface utilisateur de l’Adobe Experience Platform pour localiser un schéma, ajouter un mixin et définir un champ. Si vous préférez utiliser l&#39;API Schéma Registry, reportez-vous au guide [du développeur](../../xdm/api/getting-started.md) Schéma Registry pour savoir comment créer un mixin, ajouter un mixin à un schéma et activer un schéma à utiliser avec le Profil client en temps réel.

Dans l’interface utilisateur, cliquez sur **Schémas** dans le rail de gauche et utilisez la barre de recherche de l’onglet *Parcourir* pour trouver rapidement le schéma à mettre à jour.

![](../images/computed-attributes/Schemas-Browse.png)

Une fois le schéma localisé, cliquez sur son nom pour ouvrir l’éditeur de Schéma dans lequel vous pouvez apporter des modifications au schéma.

![](../images/computed-attributes/Schema-Editor.png)

### Création d’un mixin

Pour créer un nouveau mixin, cliquez sur **Ajouter** en regard de *mixins* dans la section *Composition* située à gauche de l’éditeur. Cette opération ouvre la boîte de dialogue **Ajouter le mixin** où vous pouvez voir les mixins existants. Cliquez sur le bouton radio pour **Créer un nouveau mixin** afin de définir votre nouveau mixin.

Donnez un nom et une description au mixin, puis cliquez sur **Ajouter le mixin** une fois terminé.

![](../images/computed-attributes/Add-mixin.png)

### Ajouter un champ d’attribut calculé au schéma

Votre nouveau mixin doit maintenant apparaître dans la section *Mélanges* sous *Composition*. Cliquez sur le nom du mixin et plusieurs boutons de champs **de** Ajoute s&#39;affichent dans la section *Structure* de l&#39;éditeur.

Sélectionnez **Ajouter le champ** en regard du nom du schéma pour ajouter un champ de niveau supérieur ou vous pouvez ajouter le champ n’importe où dans le schéma de votre choix.

Après avoir cliqué sur **Ajouter un champ** , un nouvel objet s’ouvre, nommé en fonction de votre ID de client, indiquant que le champ se trouve dans l’espace de nommage approprié. Dans cet objet, un champ ** Nouveau s’affiche. Ceci si le champ dans lequel vous allez définir l&#39;attribut calculé.

![](../images/computed-attributes/New-field.png)

### Configurer le champ

A l’aide de la section Propriétés *des* champs située sur le côté droit de l’éditeur, fournissez les informations nécessaires pour votre nouveau champ, y compris son nom, son nom d’affichage et son type.

>[!NOTE]
>Le type du champ doit être identique à celui de la valeur d’attribut calculée. Par exemple, si la valeur d’attribut calculée est une chaîne, le champ défini dans le schéma doit être une chaîne.

Lorsque vous avez terminé, cliquez sur **Appliquer** et le nom du champ, ainsi que son type, s’affichent dans la section *Structure* de l’éditeur.

![](../images/computed-attributes/Apply.png)

### Activer le schéma pour le Profil

Avant de continuer, assurez-vous que le schéma a été activé pour le Profil. Cliquez sur le nom du schéma dans la section *Structure* de l’éditeur afin que l’onglet Propriétés *du* Schéma s’affiche. Si le curseur **Profil** est bleu, le schéma a été activé pour le Profil.

>[!NOTE]
>L&#39;activation d&#39;un schéma pour le Profil ne peut pas être annulée. Par conséquent, si vous cliquez sur le curseur une fois qu&#39;il a été activé, vous n&#39;avez pas à risquer de le désactiver.

![](../images/computed-attributes/Profile.png)

Vous pouvez maintenant cliquer sur **Enregistrer** pour enregistrer le schéma mis à jour et continuer avec le reste du didacticiel à l’aide de l’API.

### Création d’un attribut calculé {#create-a-computed-attribute}

Avec votre champ d&#39;attribut calculé identifié et la confirmation que le schéma est activé pour le Profil, vous pouvez maintenant configurer un attribut calculé.

Commencez par envoyer une requête POST au point de `/config/computedAttributes` terminaison avec un corps de requête contenant les détails de l’attribut calculé que vous souhaitez créer.

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
| `name` | Nom du champ d’attribut calculé, sous forme de chaîne. |
| `path` | Chemin d’accès au champ contenant l’attribut calculé. Ce chemin d’accès se trouve dans l’ `properties` attribut du schéma et ne doit PAS inclure le nom du champ dans le chemin d’accès. Lors de l’écriture du chemin, omettez les multiples niveaux d’ `properties` attributs. |
| `{TENANT_ID}` | Si vous ne connaissez pas votre ID de locataire, reportez-vous aux étapes de recherche de votre ID de locataire dans le guide [du développeur du registre des](../../xdm/api/getting-started.md#know-your-tenant_id)Schémas. |
| `description` | Description de l’attribut calculé. Cela s&#39;avère particulièrement utile une fois que plusieurs attributs calculés ont été définis, car cela aidera d&#39;autres personnes de votre organisation IMS à déterminer l&#39;attribut calculé approprié à utiliser. |
| `expression.value` | expression PQL (Profil Requête Language) valide. Pour plus d&#39;informations sur PQL et les liens vers les requêtes prises en charge, veuillez lire la présentation [de](../../segmentation/pql/overview.md)PQL. |
| `schema.name` | Classe sur laquelle repose le schéma contenant le champ d&#39;attribut calculé. Exemple : `_xdm.context.experienceevent` pour un schéma basé sur la classe XDM ExperienceEvent. |

**Réponse**

Un attribut calculé créé avec succès renvoie HTTP Status 200 (OK) et un corps de réponse contenant les détails de l&#39;attribut calculé nouvellement créé. Ces détails incluent un attribut système unique, en lecture seule, qui peut être utilisé `id` pour référencer l&#39;attribut calculé lors d&#39;autres opérations d&#39;API.

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
| `id` | Identifiant unique généré par le système, en lecture seule, qui peut être utilisé pour référencer l’attribut calculé lors d’autres opérations d’API. |
| `imsOrgId` | L’organisation IMS associée à l’attribut calculé doit correspondre à la valeur envoyée dans la demande. |
| `sandbox` | L&#39;objet sandbox contient les détails du sandbox dans lequel l&#39;attribut calculé a été configuré. Ces informations proviennent de l’en-tête sandbox envoyé dans la requête. Pour plus d&#39;informations, consultez la présentation [des](../../sandboxes/home.md)sandbox. |
| `positionPath` | Tableau contenant la déconstruction `path` au champ qui a été envoyé dans la demande. |
| `returnSchema.meta:xdmType` | Type du champ dans lequel l&#39;attribut calculé sera stocké. |
| `definedOn` | Tableau présentant les schémas d&#39;union sur lesquels l&#39;attribut calculé a été défini. Contient un objet par schéma d&#39;union, ce qui signifie qu&#39;il peut y avoir plusieurs objets dans la baie si l&#39;attribut calculé a été ajouté à plusieurs schémas en fonction de différentes classes. |
| `active` | Valeur booléenne indiquant si l’attribut calculé est actuellement actif ou non. By default the value is `true`. |
| `type` | Le type de ressource créée, dans ce cas &quot;ComputedAttribute&quot; est la valeur par défaut. |
| `createEpoch` et `updateEpoch` | Heure à laquelle l&#39;attribut calculé a été créé et mis à jour en dernier, respectivement. |


## Accès aux attributs calculés

Lorsque vous utilisez des attributs calculés à l’aide de l’API, vous disposez de deux options pour accéder aux attributs calculés définis par votre organisation. La première consiste à liste tous les attributs calculés, la seconde à vue un attribut calculé spécifique par son `id`unique.

Les étapes permettant de répertorier tous les attributs calculés et d’afficher un attribut calculé spécifique sont décrites dans les sections suivantes.

### Attributs calculés de Liste {#list-computed-attributes}

Votre organisation IMS peut créer plusieurs attributs calculés et exécuter une requête GET sur le `/config/computedAttributes` point de terminaison vous permet de liste tous les attributs calculés existants pour votre organisation.

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

Une réponse réussie inclut un `_page` attribut qui fournit le nombre total d’attributs calculés (`totalCount`) et le nombre d’attributs calculés sur la page (`pageSize`).

La réponse comprend également un `children` tableau composé d&#39;un ou plusieurs objets, chacun contenant les détails d&#39;un attribut calculé. Si votre organisation n&#39;a pas d&#39;attributs calculés, le et `totalCount` sera 0 (zéro) et la `pageSize` `children` baie sera vide.

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
| `_page.totalCount` | Nombre total d&#39;attributs calculés définis par votre organisation IMS. |
| `_page.pageSize` | Nombre d’attributs calculés renvoyés sur cette page de résultats. Si `pageSize` est égal à `totalCount`, cela signifie qu’il n’y a qu’une seule page de résultats et que tous les attributs calculés ont été renvoyés. S’ils ne sont pas égaux, d’autres pages de résultats sont accessibles. See `_links.next` for details. |
| `children` | Tableau composé d’un ou de plusieurs objets, chacun contenant les détails d’un attribut calculé unique. Si aucun attribut calculé n&#39;a été défini, le `children` tableau est vide. |
| `id` | Valeur générée par le système, en lecture seule et unique, affectée automatiquement à un attribut calculé lors de sa création. Pour plus d&#39;informations sur les composants d&#39;un objet d&#39;attribut calculé, consultez la section sur la [création d&#39;un attribut](#create-a-computed-attribute) calculé plus tôt dans ce didacticiel. |
| `_links.next` | Si une seule page d’attributs calculés est renvoyée, `_links.next` il s’agit d’un objet vide, comme illustré dans l’exemple de réponse ci-dessus. Si votre entreprise dispose de nombreux attributs calculés, ils sont renvoyés sur plusieurs pages auxquelles vous pouvez accéder en faisant une demande GET à la `_links.next` valeur. |

### Vue d’un attribut calculé {#view-a-computed-attribute}

Vous pouvez également vue un attribut calculé spécifique en exécutant une requête GET sur le point de `/config/computedAttributes` terminaison et en incluant l’ID d’attribut calculé dans le chemin de requête.

**Format d’API**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Paramètre | Description |
|---|---|
| `{ATTRIBUTE_ID}` | ID de l’attribut calculé que vous souhaitez vue. |

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

## Mettre à jour un attribut calculé

Si vous devez mettre à jour un attribut calculé existant, vous pouvez effectuer cette opération en envoyant une requête PATCH au point de `/config/computedAttributes` terminaison et en incluant l’ID de l’attribut calculé que vous souhaitez mettre à jour dans le chemin de requête.

**Format d’API**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Paramètre | Description |
|---|---|
| `{ATTRIBUTE_ID}` | ID de l’attribut calculé que vous souhaitez mettre à jour. |

**Requête**

Cette requête utilise la mise en forme [des correctifs](http://jsonpatch.com/) JSON pour mettre à jour la &quot;valeur&quot; du champ &quot;expression&quot;.

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
| `{NEW_EXPRESSION_VALUE}` | expression PQL (Profil Requête Language) valide. Pour plus d&#39;informations sur PQL et les liens vers les requêtes prises en charge, veuillez lire la présentation [de](../../segmentation/pql/overview.md)PQL. |

**Réponse**

Une mise à jour réussie renvoie l’état HTTP 204 (aucun contenu) et un corps de réponse vide. Si vous souhaitez confirmer que la mise à jour a réussi, vous pouvez exécuter une requête GET pour vue l’attribut calculé par son identifiant.

## Suppression d’un attribut calculé

Il est également possible de supprimer un attribut calculé à l’aide de l’API. Pour ce faire, vous devez envoyer une requête de DELETE au point de `/config/computedAttributes` terminaison et inclure l’ID de l’attribut calculé que vous souhaitez supprimer dans le chemin d’accès de la requête.

>[!Note] :
>Soyez prudent lors de la suppression d&#39;un attribut calculé, car il peut être utilisé dans plusieurs schémas et l&#39;opération du DELETE ne peut pas être annulée.

**Format d’API**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Paramètre | Description |
|---|---|
| `{ATTRIBUTE_ID}` | ID de l&#39;attribut calculé que vous souhaitez supprimer. |

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

Une requête de suppression réussie renvoie HTTP Status 200 (OK) et un corps de réponse vide. Pour confirmer que la suppression a réussi, vous pouvez exécuter une requête GET pour rechercher l’attribut calculé selon son identifiant. Si l&#39;attribut a été supprimé, vous recevrez une erreur HTTP Status 404 (Not Found).

## Étapes suivantes

Maintenant que vous avez appris les bases des attributs calculés, vous êtes prêt à commencer à les définir pour votre entreprise.