---
keywords: Experience Platform;accueil;rubriques populaires;segmentation;Segmentation;Segmentation Service;pql;PQL;langage de requête de profil;quantificateurs logiques;quantificateur logique
solution: Experience Platform
title: Quantificateurs logiques PQL
topic-legacy: developer guide
description: Les quantificateurs logiques peuvent être utilisés pour insérer des conditions dans des tableaux dans le langage de requête de profil (PQL).
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 79%

---

# Fonctions de quantificateur logique

Les quantificateurs logiques peuvent être utilisés pour insérer des conditions dans des tableaux. [!DNL Profile Query Language] (PQL). Vous trouverez plus d’informations sur les autres fonctions PQL dans la section [[!DNL Profile Query Language] aperçu](./overview.md).

## Existe

La fonction `exists` détermine la présence d’un élément dans un tableau à condition qu’il remplisse la condition indiquée.

**Format**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Description |
| ---------- | ----------- |
| `{VARIABLE}` | Un nom de variable. |
| `{EXPRESSION}` | Le tableau en cours de vérification. |
| `{CONDITION}` | Une expression facultative qui filtre les valeurs du tableau renvoyé. |

**Exemple**

La requête PQL suivante récupère tous les événements dont le prix est supérieur à 50 $ ou qui ont un SKU « PS ».

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Pour tous

La fonction `forall` détermine tous les éléments d’un tableau qui répondent à toutes les conditions données.

**Format**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Description |
| ---------- | ----------- |
| `{VARIABLE}` | Un nom de variable. |
| `{EXPRESSION}` | Le tableau en cours de vérification. |
| `{CONDITION}` | Une expression facultative qui filtre les valeurs du tableau renvoyé. |

**Exemple**

La requête PQL suivante récupère tous les événements dont le prix est supérieur à 50 $ et qui ont un SKU « PS ».

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Étapes suivantes

Maintenant que vous en savez plus sur les quantificateurs logiques, vous pouvez les utiliser dans vos requêtes PQL. Pour plus d’informations sur les autres fonctions PQL, consultez la [présentation du langage de requête de profil](./overview.md).
