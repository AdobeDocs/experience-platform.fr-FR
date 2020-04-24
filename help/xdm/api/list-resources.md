---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Ressources '
topic: developer guide
translation-type: tm+mt
source-git-commit: 58549241f05f1bd604f33762f681c60946fa52f5

---


# Ressources 

Vous pouvez  un de toutes les ressources de registre de tous les d’un certain type (classes, mixins,, types de données ou descripteurs) au sein d’unjeu en exécutant une seule requête GET.

>[!NOTE] Lors de la mise en vente des ressources, le Registre de  limite les résultats à 300 éléments. Pour renvoyer des ressources au-delà de cette limite, vous devez utiliser des paramètres [de](#paging)pagination. Il est également recommandé d’utiliser des paramètres  pour [filtrer les résultats](#filtering) et réduire le nombre de ressources renvoyées.

**Format API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | où se trouvent les ressources (&quot;global&quot; ou &quot;locataire&quot;). |
| `{RESOURCE_TYPE}` | Type de ressource à récupérer de la bibliothèque de . Les types valides sont `classes`, `mixins`, `schemas`, `datatypes`et `descriptors`. |
| `{QUERY_PARAMS`} | Paramètres de  facultatifs pour filtrer les résultats par. Pour plus d’informations, consultez la section sur les paramètres [de ](#query) . |

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
| application/vnd.adobe.xed-id+json | Renvoie un bref résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour répertorier les ressources. (Limite : 300) |
| application/vnd.adobe.xed+json | Renvoie le JSON complet pour chaque ressource, avec l’original `$ref` et `allOf` inclus. (Limite : 300) |
| application/vnd.adobe.xdm-v2+json | Lors de l’utilisation du `/descriptors` point de fin, cet en-tête Accepter doit être utilisé pour utiliser les capacités de pagination. |

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

## Utilisation des paramètres {#query}

Le Registre des  de prend en charge l&#39;utilisation de paramètres  de pour la page et le filtrage des résultats lors de la liste des ressources.

>[!NOTE] Lorsque vous combinez plusieurs paramètres de , ils doivent être séparés par des esperluettes (`&`).

### Pagination {#paging}

Les paramètres  les plus courants pour la pagination sont les suivants :

| Paramètre | Description |
| --- | --- |
| `start` | Spécifiez où les résultats répertoriés doivent être enregistrés. Exemple :  résultats du troisième élément renvoyé `start=2` seront. |
| `limit` | Limitez le nombre de ressources renvoyées. Exemple : `limit=5` renverra un de cinq ressources. |
| `orderby` | Triez les résultats selon une propriété spécifique. Exemple : `orderby=title` triera les résultats par titre dans l’ordre croissant (A-Z). L’ajout d’un titre `-` avant (`orderby=-title`) triera les éléments par titre dans l’ordre décroissant (Z-A). |

### Filtrage {#filtering}

Vous pouvez filtrer les résultats à l’aide du `property` paramètre, qui permet d’appliquer un opérateur spécifique à une propriété JSON donnée dans les ressources récupérées. Les opérateurs pris en charge sont les suivants :

| Opérateur | Description | Exemple |
| --- | --- | --- |
| `==` | selon si la propriété est égale à la valeur fournie. | `property=title==test` |
| `!=` | selon si la propriété n’est pas égale à la valeur fournie. | `property=title!=test` |
| `<` | selon si la propriété est inférieure à la valeur fournie. | `property=version<5` |
| `>` | selon si la propriété est supérieure à la valeur fournie. | `property=version>5` |
| `<=` | selon si la propriété est inférieure ou égale à la valeur fournie. | `property=version<=5` |
| `>=` | selon si la propriété est supérieure ou égale à la valeur fournie. | `property=version>=5` |
| `~` | selon si la propriété correspond à un  de régulier. | `property=title~test$` |
| (Aucun) | Le fait de spécifier uniquement le nom de la propriété renvoie uniquement les entrées où la propriété existe. | `property=title` |

>[!TIP] Vous pouvez utiliser le `property` paramètre pour filtrer les mixins selon leur classe compatible. Par exemple, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` renvoie uniquement les mixins qui sont compatibles avec la classe de XDM Individuel.
