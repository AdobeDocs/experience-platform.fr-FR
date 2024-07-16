---
solution: Experience Platform
title: Fonctions de mappage PQL
description: Profile Query Language (PQL) offre des fonctions pour faciliter l’interaction avec les cartes.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 76%

---

# Fonctions de mappage

[!DNL Profile Query Language] (PQL) offre des fonctions pour faciliter l’interaction avec les cartes. Vous trouverez plus d’informations sur les autres fonctions PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Obtenir

La fonction `get` est utilisée pour récupérer la valeur d&#39;une carte pour une clé donnée.

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

La fonction `keys` est utilisée pour récupérer toutes les clés d&#39;une carte donnée.

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

La fonction `values` est utilisée pour récupérer toutes les valeurs d&#39;une carte donnée.

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
