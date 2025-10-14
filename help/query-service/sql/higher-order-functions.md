---
title: Gestion des types de données de tableau et de mappage avec des fonctions d’ordre supérieur
description: Découvrez comment gérer les types de données de tableau et de mappage avec des fonctions d’ordre supérieur dans Query Service. Des exemples sont fournis avec des cas d’utilisation courants.
exl-id: dec4e4f6-ad6b-4482-ae8c-f10cc939a634
source-git-commit: d2bc580ba1cacdfab45bdc6356c630a63e7d0f6e
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 1%

---

# Gestion des types de données de tableau et de mappage avec des fonctions d’ordre supérieur

Utilisez ce guide pour découvrir comment les fonctions d’ordre supérieur peuvent traiter des types de données complexes, tels que des tableaux et des mappages. Ces fonctions suppriment la nécessité d’exploser le tableau, d’exécuter une fonction, puis de combiner le résultat. Les fonctions d’ordre supérieur sont particulièrement utiles pour l’analyse ou le traitement de jeux de données et d’analyses de série temporelle, qui présentent souvent des structures imbriquées complexes, des tableaux, des cartes et divers cas d’utilisation.

La liste suivante de cas d’utilisation contient des exemples de fonctions de manipulation de table et de mappage de l’ordre supérieur.

## Utiliser la transformation pour ajuster le total du prix de n {#adjust-price-total}

`transform(array<T>, function<T, U>): array<U>`

Le fragment de code ci-dessus applique une fonction à chaque élément du tableau et renvoie un nouveau tableau d’éléments transformés. Plus précisément, la fonction `transform` utilise un tableau de type T et convertit chaque élément de type T en type U. Elle renvoie ensuite un tableau de type U. Les types T et U réels dépendent de l’utilisation spécifique de la fonction de transformation.

`transform(array<T>, function<T, Int, U>): array<U>`

Cette fonction de transformation de tableau est similaire à l’exemple précédent, mais il existe deux arguments pour la fonction . Le deuxième argument de cette fonction reçoit également l’index de l’élément du tableau en plus d’être transformé.

**Exemple**

L’exemple SQL ci-dessous illustre ce cas pratique. La requête récupère un ensemble limité de lignes à partir du tableau spécifié, transformant le tableau `productListItems` en multipliant l’attribut `priceTotal` de chaque élément par 73. Le résultat inclut les colonnes `_id`, `productListItems` et `price_in_inr` transformées. La sélection est basée sur une plage d’horodatage spécifique.

```sql
SELECT _id,
       productListItems,
       Transform(productListItems, value -> value.priceTotal * 73) AS
       price_in_inr
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Résultat**

Les résultats pour ce SQL apparaissent comme ceux présentés ci-dessous.

```console
 productListItems | price_in_inr
-------------------+----------------
(8376, NULL, NULL) | 611448.0
{(Burbank Hills Jeans, NULL, NULL), (Thermomax Steel, NULL, NULL), (Bruin Point Shearling Boots, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL), (Timberline Survival Knife, NULL, NULL), (Thermomax Steel, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Lost Prospector Beanie, NULL, NULL), (Timpanogos Scarf, NULL, NULL), (Uintas Pro Ski Gloves, NULL, NULL)} | {0.0,0.0.0.0,0,0,0,0,0,0,0,0,0,0,0,0,0.0}
(84763,NULL, NULL) | 6187699.0
(843765, NULL, NULL) | 6.1594845E7
(199684, NULL, NULL) | 1.4576932E7

(10 rows)
```

## Il existe une utilisation pour découvrir si un produit avec un SKU spécifique existe {#confirm-product-exists}

`exists(array<T>, function<T, boolean>): boolean`

Dans le fragment de code ci-dessus, la fonction `exists` est appliquée à chaque élément du tableau et renvoie une valeur booléenne. La valeur booléenne indique s’il existe un ou plusieurs éléments dans le tableau qui répondent à une condition spécifiée. Dans ce cas, il confirme l’existence d’un produit avec un SKU spécifique.

**Exemple**

Dans l’exemple SQL ci-dessous, la requête récupère `productListItems` de la table `geometrixxx_999_xdm_pqs_1batch_10k_rows` et évalue si un élément avec un SKU égal à `123679` dans le tableau `productListItems` existe. Il filtre ensuite les résultats en fonction d’une plage spécifique d’horodatages et limite les résultats finaux à dix lignes.

```sql
SELECT productListItems
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE EXISTS( productListItems, value -> value.sku == 123679)
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')limit 10;
```

**Résultat**

Les résultats pour ce SQL apparaissent comme ceux présentés ci-dessous.

```console
productListItems
-----------------
{(123679, NULL,NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL), (150196, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL, NULL)}
{(123679, NULL,NULL)}
{(123679,NULL, NULL)}

(10 rows)
```

## Utilisez le filtre pour rechercher les produits où SKU > 100000 {#find-specific-products}

`filter(array<T>, function<T, boolean>): array<T>`

Cette fonction filtre un tableau d’éléments en fonction d’une condition donnée qui évalue chaque élément comme une valeur booléenne. Elle renvoie ensuite un nouveau tableau qui inclut uniquement les éléments pour lesquels la condition a renvoyé une valeur true.

**Exemple**

La requête ci-dessous sélectionne la colonne `productListItems`, applique un filtre afin d’inclure uniquement les éléments dont le SKU est supérieur à 100000, et limite l’ensemble de résultats aux lignes d’une plage d’horodatage spécifique. Le tableau filtré est ensuite alias `_filter` dans la sortie.

```sql
SELECT productListItems,
    Filter(productListItems, value -> value.sku > 100000) AS _filter
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**Résultat**

Les résultats pour ce SQL apparaissent comme ceux présentés ci-dessous.

```console
productListItems | _filter
-----------------+---------
(123679, NULL, NULL) (123679, NULL, NULL)
(1346, NULL, NULL) |
(98347, NULL, NULL) |
(176015, NULL, NULL) | (176015, NULL, NULL)

(10 rows)
```

## Utilisez l’agrégat pour additionner les SKU de tous les éléments de liste de produits associés à un ID spécifique et doubler le total obtenu. {#sum-specific-skus-and-double-the-resulting-total}

`aggregate(array<T>, A, function<A, T, A>[, function<A, R>]): R`

Cette opération d’agrégat applique un opérateur binaire à un état initial et à tous les éléments du tableau . Il réduit également plusieurs valeurs à un seul état. Après cette réduction, l’état final est ensuite converti en résultat final à l’aide d’une fonction de finition. La fonction de finition prend le dernier état obtenu après l’application de l’opérateur binaire à tous les éléments du tableau et fait quelque chose avec lui pour produire le résultat final.

**Exemple**

Cet exemple de requête calcule la valeur maximale de SKU du tableau `productListItems` au cours de la période d’horodatage donnée et double le résultat. La sortie inclut le tableau `productListItems` d’origine et le `max_value` calculé.

```sql
SELECT productListItems,
aggregate(productListItems, 0, (acc, value) ->
case
WHEN (
value.sku > acc) THEN cast(value.sku AS int)
ELSE cast(acc AS int)
END, acc -> acc * 2) AS max_value
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 50;
```

**Résultat**

Les résultats pour ce SQL apparaissent comme ceux présentés ci-dessous.

```console
productListItems | max_value
-----------------+---------
(123679, NULL, NULL) | 247358
(1346,NULL, NULL) | 2692
(98347, NULL, NULL) | 196694
(176015, NULL, NULL) | 352030

(10 rows)
```

## Utilisez zip_with pour attribuer un numéro de séquence à tous les éléments de la liste de produits. {#assign-a-sequence-number}

`zip_with(array<T>, array<U>, function<T, U, R>): array<R>`

Ce fragment de code combine les éléments de deux tableaux en un seul nouveau tableau. L’opération est effectuée indépendamment sur chaque élément du tableau et génère des paires de valeurs. Si un tableau est plus court, des valeurs nulles sont ajoutées pour correspondre à la longueur du tableau plus long. Cela se produit avant l’application de la fonction.

**Exemple**

La requête suivante utilise la fonction `zip_with` pour créer des paires de valeurs à partir de deux tableaux. Pour ce faire, il ajoute les valeurs SKU du tableau `productListItems` à une séquence entière, générée à l’aide de la fonction `Sequence`. Le résultat est sélectionné avec la colonne `productListItems` d’origine et est limité en fonction d’une plage d’horodatage.

```sql
SELECT productListItems,
zip_with(Sequence(1,5), Transform(productListItems, p -> p.sku), (x,y) -> struct(x, y)) AS zip_with
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**Résultat**

Les résultats pour ce SQL apparaissent comme ceux présentés ci-dessous.

```console
productListItems     | zip_with
---------------------+---------
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(123679, NULL, NULL) | {(1,123679), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3, NULL),(4,NULL), (5,NULL)}
(1346,NULL, NULL)    | {(1,1346), (2,NULL),(3,NULL),(4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL),(4,NULL), (5,NULL)}
(98347, NULL, NULL)  | {(1,98347), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}
(176015, NULL, NULL) | {(1,176015),(2,NULL), (3,NULL), (4,NULL), (5,NULL)}
                     | {(1,NULL), (2,NULL), (3,NULL), (4,NULL), (5,NULL)}

(10 rows)
```

## Utilisez map_from_entry pour attribuer un numéro de séquence à chaque élément de la liste de produits et obtenir le résultat final sous forme de carte. {#assign-a-sequence-number-return-result-as-map}

`map_from_entries(array<struct<K, V>>): map<K, V>`

Ce fragment de code convertit un tableau de paires clé-valeur en une carte. Il est utile lorsque vous traitez des données de paires clé-valeur qui pourraient bénéficier d’une structure plus organisée et plus efficace.

**Exemple**

La requête suivante crée des paires de valeurs à partir d’une séquence et du tableau productListItems, convertit ces paires en une map à l’aide de map_from_entry, puis sélectionne la colonne productListItems d’origine avec la colonne map_from_entry nouvellement créée. Le résultat est filtré et limité en fonction de la plage d’horodatage spécifiée.

```sql
SELECT productListItems,      map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))) AS map_from_entries
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  timestamp > to_timestamp('2017-11-01 00:00:00')
AND    timestamp < to_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**Résultat**

Les résultats pour ce SQL apparaissent comme ceux présentés ci-dessous.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Utilisez map_form_arrays pour attribuer des numéros de séquence aux éléments de la liste de produits et renvoyer le résultat sous forme de carte. {#assign-sequence-numbers-to-items-return-the-result-as-a-map}

`map_form_arrays(array<K>, array<V>): map<K, V>`

La fonction `map_form_arrays` crée une map à l’aide de valeurs couplées issues de deux tableaux.

>[!IMPORTANT]
>
>Il ne doit pas y avoir d’éléments nuls dans les clés.

**Exemple**

Le code SQL ci-dessous crée une carte où les clés sont des nombres séquencés générés à l’aide de la fonction `Sequence`, et les valeurs sont des éléments du tableau `productListItems`. La requête sélectionne la colonne `productListItems` et utilise la fonction `Map_from_arrays` pour créer la carte en fonction de la séquence générée de nombres et des éléments du tableau. Le résultat est limité à dix lignes et filtré selon une plage d’horodatage.

```sql
SELECT productListItems,
       Map_from_arrays(Sequence(1, Size(productListItems)), productListItems) AS
       map_from_arrays
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE  Size(productListItems) > 0
       AND timestamp > To_timestamp('2017-11-01 00:00:00')
       AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Résultat**

Les résultats pour ce SQL apparaissent comme ceux présentés ci-dessous.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Utilisez map_concat pour concaténer deux cartes en une seule carte. {#concatenate-two-maps-into-as-single-map}

`map_concat(map<K, V>, ...): map<K, V>`

La fonction `map_concat` du fragment de code ci-dessus prend plusieurs mappages comme arguments et renvoie une nouvelle map qui combine toutes les paires clé-valeur des mappages d’entrée. La fonction concatène plusieurs mappages en une seule carte, et la carte résultante inclut toutes les paires clé-valeur des mappages d’entrée.

**Exemple**

Le code SQL ci-dessous crée une carte où chaque élément de `productListItems` est associé à un numéro de séquence, qui est ensuite concaténé avec une autre carte où les clés sont générées dans une plage de séquences spécifique.

```sql
SELECT productListItems,
      map_concat(           
         map_from_entries(zip_with(Sequence(1,Size(productListItems)), productListItems, (x,y) -> struct(x, y))),
         map_from_arrays(sequence(size(productListItems) + 1, size(productListItems) + size(productListItems)), productListItems) )
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE size(productListItems) > 0
AND timestamp > to_timestamp('2017-11-01 00:00:00')
AND timestamp < to_timestamp('2017-11-02 00:00:00')
limit 10;
```

**Résultat**

Les résultats pour ce SQL apparaissent comme ceux présentés ci-dessous.

```console
productListItems     | map_from_entries
---------------------+------------------
(123679, NULL, NULL) | [1 -> "(123679,NULL,NULL)",2 -> "(123679, NULL, NULL)"]
(1346, NULL, NULL)   | [1 -> "(1346, NULL, NULL)",2 -> "(1346, NULL, NULL)"]
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(176015, NULL, NULL) | [1 -> "(176015, NULL, NULL)",2 -> "(176015, NULL, NULL)"]
(92763, NULL, NULL)  | [1 -> "(92763, NULL, NULL)",2 -> "(92763, NULL, NULL)"] 
(48576, NULL, NULL)  | [1 -> "(48576, NULL, NULL)",2 -> "(48576, NULL, NULL)"] 
(135778, NULL, NULL) | [1 -> "(135778, NULL, NULL)",2 -> "(135778, NULL, NULL)"] 
(123679, NULL, NULL) | [1 -> "(123679, NULL, NULL)",2 -> "(123679, NULL, NULL)"] 
(98347, NULL, NULL)  | [1 -> "(98347, NULL, NULL)",2 -> "(98347, NULL, NULL)"]
(167753, NULL, NULL) | [1 -> "(167753, NULL, NULL)",2 -> "(167753, NULL, NULL)"] 

(10 rows)
```

## Utilisez element_at pour récupérer une valeur correspondant à &quot;AAID&quot; dans la carte d’identité pour effectuer d’autres calculs. {#retrieve-a-corresponding-value}

`element_at(array<T>, Int): T / element_at(map<K, V>, K): V`

Pour les tableaux, le fragment de code renvoie l’élément à un index spécifié (de base 1), ou la valeur associée à une clé dans une carte. Si l’index est inférieur à 0, il accède aux éléments du dernier au premier et renvoie null si l’index dépasse la longueur du tableau.

Pour les mappages, elle renvoie une valeur pour la clé donnée ou null si la clé n’est pas contenue dans la carte.

**Exemple**

La requête sélectionne la colonne `identitymap` de la table `geometrixxx_999_xdm_pqs_1batch_10k_rows` et extrait la valeur associée à la clé `AAID` pour chaque ligne. Les résultats sont limités aux lignes comprises dans la plage d’horodatage spécifiée, et la requête limite la sortie à dix lignes.

```sql
SELECT identitymap,
              Element_at(identitymap, 'AAID')
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10; 
```

**Résultat**

Les résultats pour ce SQL apparaissent comme ceux présentés ci-dessous.

```console
                                                                  identitymap                                            |  element_at(identitymap, AAID) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            | (3617FBB942466D79-5433F727AD6A0AD, false) 
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] | (533F56A682C059B1-396437F68879F61D, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             | (6A60527B9D66CCB9-29638A632B45E9, false) 
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           | (64FB4DC317E21B59-2A23602D234647E7, false) 
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           | (2E70E8CF6DB1DE86-270E55BBBA58B9C1, false) 
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            | (22E195F8A8ECCC6A-A39615C93B72A9F, false) 
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           | (1CFB3297C3146F2F-28D6902A610BA3B1, false) 
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           | (533F56A682C059B1-396437F68879F61D, false) 
(10 rows)
```

## Utilisez la cardinalité pour trouver le nombre d’identités dans la carte des identités. {#find-the-number-of-identities-in-the-identity-map}

`cardinality(array<T>): Int / cardinality(map<K, V>): Int`

Ce fragment de code renvoie la taille d’un tableau ou d’un mappage donné et fournit un alias. Elle renvoie -1 si la valeur est nulle.

**Exemple**

La requête ci-dessous récupère la colonne `identitymap` et la fonction `Cardinality` calcule le nombre d’éléments dans chaque carte dans `identitymap`. Les résultats sont limités à dix lignes et sont filtrés selon une plage d’horodatage spécifiée.

```sql
SELECT identitymap,
       Cardinality(identitymap)
FROM   geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT  10;
```

**Résultat**

Les résultats pour ce SQL apparaissent comme ceux présentés ci-dessous.

```console
                                                                  identitymap                                            |  size(identitymap) 
-------------------------------------------------------------------------------------------------------------------------+-------------------------------------
[AAID -> "(3617FBB942466D79-5433F727AD6A0AD, false)",ECID -> "(67383754798169392543508586197135045866,true)"]            |      2  
[AAID -> "[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"] |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(6A60527B9D66CCB9-29638A632B45E9, false)",ECID -> "(50117234882064422833184021414056250576,true)"]             |      2  
[AAID -> "(64FB4DC317E21B59-2A23602D234647E7, false)",ECID -> "(79785479785408621882908938960039330887,true)"]           |      2  
[AAID -> "(2E70E8CF6DB1DE86-270E55BBBA58B9C1, false)",ECID -> "(80073674009951685326146914344189474476,true)"]           |      2  
[AAID -> "(22E195F8A8ECCC6A-A39615C93B72A9F, false)",ECID -> "(57699241367342030964647681192998909474,true)"]            |      2  
[AAID -> "(1CFB3297C3146F2F-28D6902A610BA3B1, false)",ECID -> "(88251082790399360979074868101758236669,true)"]           |      2  
[AAID -> "(533F56A682C059B1-396437F68879F61D, false)",ECID -> "(91989370462250197735311833131353001213,true)"]           |      2  
(10 rows)
```

## Utilisez array_distinct pour trouver les éléments distincts dans productListItems {#find-distinct-elements}

`array_distinct(array<T>): array<T>`

Le fragment de code ci-dessus supprime les valeurs en double du tableau donné.

**Exemple**

La requête ci-dessous sélectionne la colonne `productListItems`, supprime les éléments en double des tableaux et limite la sortie à dix lignes en fonction d’une plage d’horodatage spécifiée.

```sql
SELECT productListItems,
              Array_distinct(productListItems)
FROM geometrixxx_999_xdm_pqs_1batch_10k_rows
WHERE timestamp > To_timestamp('2017-11-01 00:00:00')
AND timestamp < To_timestamp('2017-11-02 00:00:00')
LIMIT 10;
```

**Résultat**

Les résultats pour ce SQL apparaissent comme ceux présentés ci-dessous.

```console
productListItems     | array_distinct(productListItems)
---------------------+---------------------------------
                     |
(123679, NULL, NULL) | (123679, NULL, NULL)
                     |
                     |
(1346,NULL, NULL)    | (1346,NULL, NULL)
                     |
(98347, NULL, NULL)  | (98347, NULL, NULL)
                     |
(176015, NULL, NULL) | (176015, NULL, NULL)
                     |

(10 rows)
```

### Fonctions d’ordre supérieur supplémentaires {#additional-higher-order-functions}

Les exemples suivants de fonctions d’ordre supérieur sont expliqués dans le cadre de la récupération de cas d’utilisation d’enregistrements similaires. Vous trouverez un exemple et une explication de l’utilisation de chaque fonction dans la section correspondante de ce document.

L’exemple de fonction [`transform`](../use-cases/retrieve-similar-records.md#length-adjustment) couvre la segmentation en unités lexicales d’une liste de produits.

L’exemple de fonction [`filter` &#x200B;](../use-cases/retrieve-similar-records.md#filter-results) illustre une extraction plus précise et plus affinée d’informations pertinentes à partir de données de texte.

La fonction [`reduce` &#x200B;](../use-cases/retrieve-similar-records.md#higher-order-function-solutions) permet d’obtenir des valeurs cumulatives ou des agrégats, qui peuvent être essentiels dans divers processus d’analyse et de planification.
