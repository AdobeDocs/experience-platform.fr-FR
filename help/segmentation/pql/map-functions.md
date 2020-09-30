---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;map functions;map;
solution: Experience Platform
title: Fonctions de mappage
topic: developer guide
description: Le langage de requête de profil (PQL) offre des fonctions pour faciliter l’interaction avec des cartes.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 86%

---


# Fonctions de mappage

[!DNL Profile Query Language] (PQL) offre des fonctions pour faciliter l&#39;interaction avec les cartes. More information about other PQL functions can be found in the [[!DNL Profile Query Language] overview](./overview.md).

## Get

La fonction `get` est utilisée pour récupérer la valeur d’une carte pour une clé donnée.

**Format**

```sql
{MAP}.get({STRING})
```

**Exemple**

La requête PQL suivante renvoie la valeur de la carte d’identité pour la clé `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Keys

La fonction `keys` est utilisée pour récupérer toutes les clés d’une carte donnée.

**Format**

```sql
{MAP}.keys()
```

**Exemple**

La requête PQL suivante renvoie toutes les clés pour la carte `identityMap`.

```sql
identityMap.keys()
```

## Values

La fonction `values` est utilisée pour récupérer toutes les valeurs d’une carte donnée.

**Format**

```sql
{MAP}.values()
```

**Exemple**

La requête PQL suivante renvoie toutes les valeurs pour la carte `identityMap`.

```sql
identityMap.values()
```

## Étapes suivantes

Maintenant que vous en savez plus sur les fonctions de carte, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).
