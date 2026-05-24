---
solution: Experience Platform
title: Fonctions de mappage PQL
description: Profile Query Language (PQL) offre des fonctions permettant de faciliter l'interaction avec les cartes.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
TQID: https://experienceleague.adobe.com/N5vM8IXEV9vCj8LkmfXHEuTLpXBxJVCuyb9IiBWzJbM
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2: id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 169
ht-degree: 46%

---

# Fonctions de mappage

[!DNL Profile Query Language] (PQL) offre des fonctions permettant de faciliter l&#39;interaction avec les cartes. Vous trouverez plus d’informations sur d’autres fonctions de PQL dans la [[!DNL Profile Query Language] présentation](./overview.md).

## Obtenir

La fonction `get` est utilisée pour récupérer la valeur d’un mappage pour une clé donnée en tant qu’objet .

**Format**

```sql
{MAP}.get({STRING})
```

**Exemple**

La requête PQL suivante renvoie la valeur de la carte d’identité pour la clé `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Clés

La fonction `keys` est utilisée pour récupérer toutes les clés d&#39;un mappage donné sous la forme d&#39;un tableau ou d&#39;une liste.

**Format**

```sql
{MAP}.keys()
```

**Exemple**

La requête PQL suivante renvoie toutes les clés pour la carte `identityMap`.

```sql
identityMap.keys()
```

## Valeurs

La fonction `values` est utilisée pour récupérer toutes les valeurs d&#39;un mappage donné sous la forme d&#39;un tableau ou d&#39;une liste.

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
