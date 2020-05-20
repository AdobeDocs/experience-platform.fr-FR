---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ressources de Liste
topic: developer guide
translation-type: tm+mt
source-git-commit: 58549241f05f1bd604f33762f681c60946fa52f5
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 2%

---


# Ressources de Liste

Vous pouvez vue une liste de toutes les ressources de registre de Schéma d&#39;un certain type (classes, mixins, schémas, types de données ou descripteurs) dans un conteneur en exécutant une seule requête GET.

>[!NOTE] Lors de la mise en vente de ressources, le Registre des Schémas limite les résultats à 300 éléments. Pour renvoyer des ressources au-delà de cette limite, vous devez utiliser des paramètres [de](#paging)pagination. Il est également recommandé d’utiliser des paramètres de requête pour [filtrer les résultats](#filtering) et réduire le nombre de ressources renvoyées.

**Format d’API**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| Paramètre | Description |
| --- | --- |
| `{CONTAINER_ID}` | conteneur où se trouvent les ressources (&quot;global&quot; ou &quot;locataire&quot;). |
| `{RESOURCE_TYPE}` | Type de ressource à récupérer de la bibliothèque de Schémas. Les types valides sont `classes`, `mixins`, `schemas`, `datatypes`et `descriptors`. |
| `{QUERY_PARAMS`} | Paramètres de requête facultatifs pour filtrer les résultats en fonction. Pour plus d&#39;informations, consultez la section sur les paramètres [de](#query) requête. |

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

| Accepter l’en-tête | Description |
| ------- | ------------ |
| application/vnd.adobe.xed-id+json | Renvoie un bref résumé de chaque ressource. Il s’agit de l’en-tête recommandé pour la liste des ressources. (Limite : 300) |
| application/vnd.adobe.xed+json | Renvoie le schéma JSON complet pour chaque ressource, avec l’original `$ref` et `allOf` inclus. (Limite : 300) |
| application/vnd.adobe.xdm-v2+json | Lors de l’utilisation du point de `/descriptors` terminaison, cet en-tête Accepter doit être utilisé pour utiliser les capacités de pagination. |

**Réponse**

La requête ci-dessus utilisait l’en-tête `application/vnd.adobe.xed-id+json` Accepter. Par conséquent, la réponse inclut uniquement les `title`attributs, `$id`, `meta:altId`et `version` pour chaque ressource. La substitution `full` dans l&#39;en-tête Accepter renvoie tous les attributs de chaque ressource. Sélectionnez l’en-tête Accepter approprié en fonction des informations que vous souhaitez obtenir dans votre réponse.

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

Le Registre des Schémas prend en charge l&#39;utilisation de paramètres de requête pour la page et filtrer les résultats lors de la liste des ressources.

>[!NOTE] Lorsque vous combinez plusieurs paramètres de requête, ils doivent être séparés par des esperluettes (`&`).

### Pagination {#paging}

Les paramètres de requête les plus courants pour la pagination sont les suivants :

| Paramètre | Description |
| --- | --- |
| `start` | Spécifiez où les résultats répertoriés doivent être enregistrés. Exemple : `start=2` aura liste les résultats du troisième élément renvoyé plus tard. |
| `limit` | Limiter le nombre de ressources renvoyées. Exemple : `limit=5` retournera une liste de cinq ressources. |
| `orderby` | Triez les résultats selon une propriété spécifique. Exemple : `orderby=title` triera les résultats par titre dans l’ordre croissant (A-Z). L&#39;ajout d&#39;un titre `-` avant le titre (`orderby=-title`) triera les éléments par titre dans l&#39;ordre décroissant (Z-A). |

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

>[!TIP] Vous pouvez utiliser le `property` paramètre pour filtrer les mixins selon leur classe compatible. Par exemple, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` renvoie uniquement les mixins compatibles avec la classe de Profil XDM Individuel.
