---
title: Filtrage des réponses dans l'API Reactor
description: Découvrez comment filtrer les résultats lors de la liste des ressources dans l’API Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---

# Filtrage des réponses dans l&#39;API Reactor

Lors de l’utilisation de points de terminaison list (GET) dans l’API Reactor, vous trouverez peut-être nécessaire de limiter les résultats renvoyés à un sous-ensemble d’enregistrements. Pour ce faire, de nombreux points de terminaison de liste de l’API prennent en charge la possibilité de filtrer selon des attributs spécifiques. Si vous souhaitez effectuer plutôt des requêtes structurées vers l’API, consultez le guide sur la [recherche](./search.md).

## Syntaxe du filtrage

L’exemple suivant explique comment implémenter des filtres pour vos requêtes de GET.

**Format d&#39;API**

Pour filtrer la réponse d’un point de terminaison de liste donné, vous devez fournir un paramètre de requête `filter` dans le chemin de requête.

>[!NOTE]
>
>Le modèle ci-dessous utilise des crochets (`[]`) et des espaces pour faciliter la lecture. En pratique, ces caractères doivent être encodés en URI, comme indiqué dans la [RFC 3986](https://tools.ietf.org/html/rfc3986). Un exemple de chemin de requête correctement encodé est présenté plus loin dans ce guide.
>
>Notez que si la structure de vos filtres est incorrecte, aucun filtre n’est appliqué et le jeu de résultats complet est renvoyé.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| Propriété | Description |
| --- | --- |
| `{ENDPOINT}` | Point de terminaison de liste dans l’API Reactor qui prend en charge les paramètres de filtre. |
| `{ATTRIBUTE_NAME}` | Nom d’un attribut spécifique selon lequel filtrer les résultats. Gardez à l’esprit que les différents points de terminaison prennent en charge différents attributs pour le filtrage. Reportez-vous au guide de référence du point de terminaison que vous utilisez pour obtenir la liste des attributs de filtrage disponibles. |
| `{OPERATOR}` | L’opérateur qui détermine la manière dont les résultats sont évalués par rapport au `{VALUE}` fourni. Les opérateurs pris en charge sont répertoriés dans la [section de l’annexe](#supported-operators). |
| `{VALUE}` | Valeur par rapport à laquelle comparer les résultats renvoyés. Lors de la comparaison pour l’égalité à l’aide de l’opérateur `EQ`, la valeur doit être une correspondance exacte et sensible à la casse pour être incluse dans la réponse. |

{style=&quot;table-layout:auto&quot;}

**Requête**

L’exemple de requête ci-dessous récupère une liste de bibliothèques publiées en appliquant un filtre qui nécessite que l’attribut `state` de la bibliothèque soit égal à `published`.

Avant le codage URI, la syntaxe de ce filtre dans le chemin d’accès de la requête est similaire à celle-ci :

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

Une fois que le chemin et les paramètres de requête ont été codés en URI, ils peuvent être utilisés dans des requêtes API comme celle ci-dessous :

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

## Filtrage sur plusieurs valeurs {#multiple-values}

Pour filtrer par plusieurs valeurs pour un seul attribut, fournissez les valeurs sous la forme d’une liste séparée par des virgules.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## Utilisation de plusieurs filtres

Pour appliquer des filtres pour plusieurs attributs, indiquez un paramètre `filter` pour chaque attribut. Les paramètres doivent être séparés par des caractères d’esperluette (`&`).

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>Si vous spécifiez le même attribut dans plusieurs filtres sur la même requête, seul le dernier filtre fourni pour cet attribut sera appliqué.

## Annexe

La section suivante contient des informations supplémentaires sur l’utilisation des filtres dans l’API Reactor.

### Opérateurs de filtre pris en charge {#operators}

Le tableau suivant répertorie les valeurs d’opérateur prises en charge pour les paramètres de filtre. Gardez à l’esprit que selon l’attribut par lequel vous filtrez, tous les opérateurs de filtre disponibles ne seront pas applicables, comme l’utilisation d’opérateurs &quot;inférieur à&quot; ou &quot;supérieur à&quot; pour les attributs de chaîne.

| Opérateur | Description |
| --- | --- |
| `EQ` | L’attribut doit être égal à la valeur fournie. |
| `NOT` | L’attribut ne doit pas être égal à la valeur fournie. |
| `LT` | L’attribut doit être inférieur à la valeur fournie. |
| `GT` | L’attribut doit être supérieur à la valeur fournie. |
| `BETWEEN` | L’attribut doit se trouver dans une plage de valeurs spécifiée. Lors de l’utilisation de cet opérateur, [deux valeurs](#multiple-values) doivent être fournies pour indiquer les valeurs minimale et maximale de la plage souhaitée. |
| `CONTAINS` | L’attribut doit contenir la valeur fournie, par exemple un ensemble de caractères dans un attribut string . |
