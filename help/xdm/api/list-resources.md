---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Liste des ressources
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 32%

---


# Liste des ressources

Vous pouvez vue une liste de toutes les ressources d’un certain type (classes, mixins, schémas, types de données ou descripteurs) au sein d’un conteneur en exécutant une seule requête de GET. [!DNL Schema Registry]

>[!NOTE]
>
>Lors de la mise en vente de ressources, le résultat [!DNL Schema Registry] limite à 300 éléments. Pour renvoyer des ressources au-delà de cette limite, vous devez utiliser des paramètres [de](#paging)pagination. Il est également recommandé d’utiliser des paramètres de requête pour [filtrer les résultats](#filtering) et réduire le nombre de ressources renvoyées.

**Format d’API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | Le conteneur où se trouvent les ressources (« global » ou « client »). |
| `{RESOURCE_TYPE}` | The type of resource to retrieve from the [!DNL Schema Library]. Valid types are `classes`, `mixins`, `schemas`, `datatypes`, and `descriptors`. |
| `{QUERY_PARAMS`} | Paramètres de requête facultatifs pour filtrer les résultats en fonction. See the section on [query parameters](#query) for more information. |

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

Le format de la réponse dépend de l’en-tête Accept envoyé dans la requête. Vous pouvez utiliser les en-têtes Accept suivants pour répertorier des ressources :

| En-tête Accept | Description |
| ------- | ------------ |
| application/vnd.adobe.xed-id+json | Renvoie un bref résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour la liste des ressources. (Limite : 300) |
| application/vnd.adobe.xed+json | Renvoie la totalité du schéma JSON de chaque ressource, en incluant le `$ref` et l’`allOf` d’origine. (Limite : 300) |
| application/vnd.adobe.xdm-v2+json | Lors de l’utilisation du point de `/descriptors` terminaison, cet en-tête Accepter doit être utilisé pour utiliser les capacités de pagination. |

**Réponse**

La requête ci-dessus utilisait l’en-tête Accept `application/vnd.adobe.xed-id+json`, c’est pourquoi la réponse n’inclut que les attributs `title`, `$id`, `meta:altId` et `version` de chaque ressource. Substituer `full` dans l’en-tête Accept renvoie tous les attributs de chaque ressource. Sélectionnez l’en-tête Accept approprié en fonction des informations dont vous avez besoin dans votre réponse.

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

## Utilisation des paramètres de requête {#query}

Le [!DNL Schema Registry] prend en charge l&#39;utilisation de paramètres de requête pour la page et le filtrage des résultats lors de la mise en vente des ressources.

>[!NOTE]
>
>Lorsque vous combinez plusieurs paramètres de requête, ceux-ci doivent être séparés par des esperluettes (`&`).

### Pagination {#paging}

Les paramètres de requête les plus courants pour la pagination sont les suivants :

| Paramètre | Description |
| --- | --- |
| `start` | Indiquez où doivent commencer les résultats répertoriés. Cette valeur peut être obtenue à partir de l’ `_page.next` attribut d’une réponse de liste et utilisée pour accéder à la page de résultats suivante. Si la `_page.next` valeur est nulle, aucune page supplémentaire n’est disponible. |
| `limit` | Limite le nombre de ressources renvoyé. Exemple : `limit=5` renverra une liste de cinq ressources. |
| `orderby` | Trie les résultats en fonction d’une propriété spécifique. Exemple : `orderby=title` triera les résultats par titre dans l’ordre croissant (A-Z). L’ajout d’un `-` devant le titre (`orderby=-title`) triera les éléments par titre dans l’ordre décroissant (Z-A). |

### Filtrage {#filtering}

Vous pouvez filtrer les résultats en utilisant le `property` paramètre, qui est utilisé pour appliquer un opérateur spécifique à une propriété JSON donnée dans les ressources récupérées. Les opérateurs pris en charge sont les suivants :

| Opérateur | Description | Exemple |
| --- | --- | --- |
| `==` | Filtres selon si la propriété est égale à la valeur fournie. | `property=title==test` |
| `!=` | Filtres selon si la propriété n’est pas égale à la valeur fournie. | `property=title!=test` |
| `<` | Filtres selon si la propriété est inférieure à la valeur fournie. | `property=version<5` |
| `>` | Filtres selon si la propriété est supérieure à la valeur fournie. | `property=version>5` |
| `<=` | Filtres selon si la propriété est inférieure ou égale à la valeur fournie. | `property=version<=5` |
| `>=` | Filtres selon si la propriété est supérieure ou égale à la valeur fournie. | `property=version>=5` |
| `~` | Filtres selon si la propriété correspond à une expression régulière fournie. | `property=title~test$` |
| (Aucun) | Le fait de spécifier uniquement le nom de la propriété renvoie uniquement les entrées où la propriété existe. | `property=title` |

>[!TIP]
>
>Vous pouvez utiliser le `property` paramètre pour filtrer les mixins selon leur classe compatible. For example, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` returns only mixins that are compatible with the [!DNL XDM Individual Profile] class.
