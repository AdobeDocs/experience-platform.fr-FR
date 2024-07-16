---
title: Filtrage des réponses dans l’API Reactor
description: Découvrez comment filtrer les résultats lorsque les ressources sont répertoriées dans l’API Reactor.
exl-id: 8a91f3dd-4ead-4a10-abb1-e71acb0d73b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 100%

---

# Filtrage des réponses dans l’API Reactor

Lors de l’utilisation de points d’entrée de liste (GET) dans l’API Reactor, vous trouverez peut-être nécessaire de limiter les résultats renvoyés à un sous-ensemble d’enregistrements. Pour ce faire, de nombreux points d’entrée de liste de l’API prennent en charge la possibilité d’effectuer un filtrage en fonction d’attributs spécifiques. Si vous préférez effectuer des requêtes structurées vers l’API, consultez le guide consacré à la [recherche](./search.md).

## Syntaxe de filtrage

L’exemple suivant décrit les méthodes d’implémentation de filtres pour vos requêtes GET.

**Format d&#39;API**

Pour filtrer la réponse pour un point d’entrée de liste donné, vous devez fournir un paramètre de requête `filter` dans le chemin d’accès de la requête.

>[!NOTE]
>
>Le modèle ci-dessous utilise des crochets (`[]`) et des espaces pour faciliter la lecture. En pratique, ces caractères doivent être encodés en URI, comme indiqué dans le document [RFC 3986](https://tools.ietf.org/html/rfc3986). Un exemple de chemin d’accès de requête correctement encodé est présenté plus loin dans ce guide.
>
>Veuillez noter que si la structure de vos filtres est incorrecte, aucun filtre n’est appliqué et le jeu de résultats complet est renvoyé.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| Propriété | Description |
| --- | --- |
| `{ENDPOINT}` | Point d’entrée de liste dans l’API Reactor qui prend en charge les paramètres de filtre. |
| `{ATTRIBUTE_NAME}` | Nom d’un attribut spécifique en fonction duquel filtrer les résultats. Gardez en tête que différents points d’entrée prennent en charge différents attributs pour le filtrage. Reportez-vous au guide de référence du point d’entrée que vous utilisez pour obtenir la liste des attributs de filtrage disponibles. |
| `{OPERATOR}` | L’opérateur qui détermine la manière dont les résultats sont évalués en fonction de la valeur `{VALUE}` fournie. Les opérateurs pris en charge sont répertoriés dans la [section annexe](#supported-operators). |
| `{VALUE}` | Valeur en fonction de laquelle comparer les résultats renvoyés. Lors de la comparaison relative à l’égalité à l’aide de l’opérateur `EQ`, la valeur doit avoir une correspondance exacte et sensible à la casse pour être incluse dans la réponse. |

{style="table-layout:auto"}

**Requête**

L’exemple de requête ci-dessous récupère une liste de bibliothèques publiées en appliquant un filtre qui nécessite que l’attribut `state` de la bibliothèque soit égal à `published`.

Avant l’encodage URI, la syntaxe de ce filtre dans le chemin d’accès de la requête est similaire à celle-ci :

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

Une fois le chemin d’accès et les paramètres de requête codés en URI, ils peuvent être utilisés dans des requêtes API comme celle ci-dessous :

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

## Filtrage sur plusieurs valeurs {#multiple-values}

Pour effectuer le filtrage d’un seul attribut en fonction de plusieurs valeurs, fournissez les valeurs sous forme de liste séparée par des virgules.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## Utilisation de plusieurs filtres

Pour appliquer des filtres à plusieurs attributs, fournissez un paramètre `filter` à chaque attribut. Les paramètres doivent être séparés par des esperluettes (`&`).

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>Si, pour une même requête, vous spécifiez le même attribut dans plusieurs filtres, seul le dernier filtre fourni pour cet attribut est appliqué.

## Annexe

La section suivante contient des informations supplémentaires relatives à l’utilisation de filtres dans l’API Reactor.

### Opérateurs de filtre pris en charge {#operators}

Le tableau suivant répertorie les valeurs d’opérateur prises en charge pour les paramètres de filtre. Gardez en tête que, selon l’attribut en fonction duquel vous effectuez le filtrage, tous les opérateurs de filtre disponibles ne sont pas applicables. C’est notamment le cas pour l’utilisation d’opérateurs « inférieur à » ou « supérieur à » pour les attributs de chaîne.

| Opérateur | Description |
| --- | --- |
| `EQ` | La valeur de l’attribut doit être égale à la valeur fournie. |
| `NOT` | La valeur de l’attribut ne doit pas être égale à la valeur fournie. |
| `LT` | La valeur de l’attribut doit être inférieure à la valeur fournie. |
| `GT` | La valeur de l’attribut doit être supérieure à la valeur fournie. |
| `BETWEEN` | La valeur de l’attribut doit se trouver dans une plage de valeurs spécifiée. Lors de l’utilisation de cet opérateur, [deux valeurs](#multiple-values) doivent être fournies pour indiquer les valeurs minimale et maximale de la plage souhaitée. |
| `CONTAINS` | L’attribut doit contenir la valeur fournie, par exemple un ensemble de caractères dans un attribut de chaîne. |
