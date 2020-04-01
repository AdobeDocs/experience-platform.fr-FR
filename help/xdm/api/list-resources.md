---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Ressources '
topic: developer guide
translation-type: tm+mt
source-git-commit: 1541b027a4e572dc5e4e64de1117a269c58bafab

---


# Ressources 

Vous pouvez  un de toutes les ressources (, classes, mixins ou types de données) au sein d’unen exécutant une seule requête GET. Pour faciliter le filtrage des résultats, le Registre des  prend en charge l&#39;utilisation des paramètres  lors de la liste des ressources.

Les paramètres  les plus courants sont les suivants :

* `limit` - Limiter le nombre de ressources renvoyées. Exemple : `limit=5` renverra un de cinq ressources.
* `orderby` - Trier les résultats selon une propriété spécifique. Exemple : `orderby=title` triera les résultats par titre dans l’ordre croissant (A-Z). L’ajout d’un titre `-` avant (`orderby=-title`) triera les éléments par titre dans l’ordre décroissant (Z-A).
* `property` - Filtrez les résultats sur les attributs de niveau supérieur. Par exemple, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` renvoie uniquement les mixins qui sont compatibles avec la classe de XDM Individuel.

Lorsque vous combinez plusieurs paramètres de , ils doivent être séparés par des esperluettes (`&`).

**Format API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | où se trouvent les ressources (&quot;global&quot; ou &quot;locataire&quot;). |
| `{RESOURCE_TYPE}` | Type de ressource à récupérer de la bibliothèque de . Les types valides sont `datatypes`, `mixins`, `schemas`et `classes`. |

**Requête**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes&limit=2 \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Le format de réponse dépend de l’en-tête Accepter envoyé dans la requête. Les en-têtes Accepter suivants sont disponibles pour répertorier les ressources :

| En-tête Accepter | Description |
| ------- | ------------ |
| application/vnd.adobe.xed-id+json | Renvoie un bref résumé de chaque ressource, généralement l’en-tête préféré pour la liste. |
| application/vnd.adobe.xed+json | Renvoie le  JSON complet pour chaque ressource, avec l’original `$ref` et `allOf` inclus |

**Réponse**

La requête ci-dessus utilisait l’en-tête `application/vnd.adobe.xed-id+json` Accepter. Par conséquent, la réponse inclut uniquement les attributs `title`, `$id`, `meta:altId`et `version` pour chaque ressource. La substitution `full` dans l’en-tête Accepter renvoie tous les attributs de chaque ressource. Sélectionnez l’en-tête Accepter approprié en fonction des informations requises dans votre réponse.

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```
