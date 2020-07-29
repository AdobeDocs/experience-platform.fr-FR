---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Fonctions Spark SQL
topic: spark sql functions
translation-type: tm+mt
source-git-commit: a98e31f57c6ff4fc49d8d8f64441a6e1e18d89da
workflow-type: tm+mt
source-wordcount: '4900'
ht-degree: 99%

---


# [!DNL Spark] Fonctions SQL

The [!DNL Spark] SQL helpers provide built-in [!DNL Spark] SQL functions to extend SQL functionality.

Référence : [documentation des fonctions Spark SQL](https://spark.apache.org/docs/2.4.0/api/sql/index.html)

>[!NOTE]
>
>Certaines fonctions de la documentation externe ne sont pas prises en charge.

## Catégories

- [Fonctions et opérateurs mathématiques et statistiques](#math-and-statistical-operators-and-functions)
- [Opérateurs logiques](#logical-operators)
- [Fonctions de date/heure](#date/time-functions)
- [Fonctions d’agrégation](#aggregate-functions)
- [Tableaux](#arrays)
- [Fonctions de diffusion du type de données](#datatype-casting-functions)
- [Fonctions de conversion et de formatage](#conversion-and-formatting-functions)
- [Évaluation des données](#data-evaluation)
- [Informations actuelles](#current-information)

### Fonctions et opérateurs mathématiques et statistiques

#### Modulo

`expr1 % expr2` : renvoie le reste après `expr1`/`expr2`.

Exemples :

```
> SELECT 2 % 1.8;
 0.2
> SELECT MOD(2, 1.8);
 0.2
```

#### Multiply

`expr1 * expr2` : renvoie `expr1`*`expr2`.

Exemple :

```
> SELECT 2 * 3;
 6
```

#### Add

`expr1 + expr2` : renvoie `expr1`+`expr2`.

Exemple :

```
> SELECT 1 + 2;
 3
```

#### Subtract

`expr1 - expr2` : renvoie `expr1`-`expr2`.

Exemple :

```
> SELECT 2 - 1;
 1
```

#### Divide

`expr1 / expr2` : renvoie `expr1`/`expr2`. Cette opération effectue toujours une division à virgule flottante.

Exemples :

```
> SELECT 3 / 2;
 1.5
> SELECT 2L / 2L;
 1.0
```

#### abs

`abs(expr)` : renvoie la valeur absolue de la valeur numérique.

Exemple :

```
> SELECT abs(-1);
  1
```

#### acos

`acos(expr)` : renvoie le cosinus inverse (aussi appelé arc cosinus) de `expr`, comme s’il était calculé par `java.lang.Math.acos`.

Exemples :

```
> SELECT acos(1);
 0.0
> SELECT acos(2);
 NaN
```

#### approx_percentile

`approx_percentile(col, percentage [, accuracy])` : renvoie la valeur approximative du centile d’une colonne numérique `col` au pourcentage donné. La valeur du pourcentage doit être comprise entre 0,0 et 1,0. Le paramètre `accuracy` (par défaut : 10000) est un littéral numérique positif contrôlant la précision d’approximation au prix de la mémoire. Une valeur plus élevée de `accuracy` donne une meilleure précision, `1.0/accuracy` étant l’erreur relative de l’approximation. Lorsque `percentage` est un tableau, chaque valeur du tableau de pourcentage doit être comprise entre 0,0 et 1,0. Dans ce cas, le tableau du centile approximatif de la colonne `col` au tableau du pourcentage donné est renvoyé.

Exemples :

```
> SELECT approx_percentile(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT approx_percentile(10.0, 0.5, 100);
 10.0
```

#### asin

`asin(expr)` : renvoie le sinus inverse (aussi appelé arc sinus), l’arc sinus de `expr`, comme s’il était calculé par `java.lang.Math.asin`.

Exemples :

```
> SELECT asin(0);
 0.0
> SELECT asin(2);
 NaN
```

#### atan

`atan(expr)` : renvoie la tangente inverse (aussi appelée arc tangente) de `expr`, comme si elle était calculée par `java.lang.Math.atan`.

Exemple :

```
> SELECT atan(0);
 0.0
```

#### atan2

`atan2(exprY, exprX)` : renvoie l’angle en radians entre l’axe X positif d’un plan et le point défini par les coordonnées (`exprX`, `exprY`), comme s’il était calculé par `java.lang.Math.atan2`.

Arguments :

`exprY` : coordonnée sur l’axe Y
`exprX` : coordonnée sur l’axe X

Exemple :

```
> SELECT atan2(0, 0);
 0.0
```

#### avg

`avg(expr)` : renvoie la moyenne calculée à partir des valeurs d’un groupe.

#### cardinality

`cardinality(expr)` : renvoie la taille d’un tableau ou d’une carte. La fonction renvoie -1 si son entrée est nulle et `spark.sql.legacy.sizeOfNull` elle est définie sur true (valeur par défaut). Si `spark.sql.legacy.sizeOfNull` est défini sur false, la fonction renvoie null pour une entrée nulle.

Exemples :

```
> SELECT cardinality(array('b', 'd', 'c', 'a'));
 4
> SELECT cardinality(map('a', 1, 'b', 2));
 2
> SELECT cardinality(NULL);
 -1
```

#### cbrt

`cbrt(expr)` : renvoie la racine cubique de `expr`.

Exemple :

```
> Select cbrt(27.0);
 3.0
```

#### ceil

`ceil(expr)` : renvoie le plus petit entier qui n’est pas inférieur à `expr`.

Exemples :

```
> SELECT ceil(-0.1);
 0
> SELECT ceil(5);
 5
```

#### ceiling

`ceiling(expr)` : renvoie le plus petit entier qui n’est pas inférieur à `expr`.

Exemples :

```
> SELECT ceiling(-0.1);
 0
> SELECT ceiling(5);
 5
```

#### conv

`conv(num, from_base, to_base)` : convertit `num` de `from_base` à `to_base`

Exemples :

```
> SELECT conv('100', 2, 10);
 4
> SELECT conv(-10, 16, -10);
 -16
```

#### corr

`corr(expr1, expr2)` : renvoie le coefficient de corrélation de Pearson entre un ensemble de paires de nombres.

#### cos

`cos(expr)` : renvoie le cosinus de `expr`, comme s’il était calculé par `java.lang.Math.cos`.

Exemple :

```
> SELECT cos(0);
 1.0
```

#### cosh

`cosh(expr)` : renvoie le cosinus hyperbolique de `expr`, comme s’il était calculé par `java.lang.Math.cosh`.

Arguments :
- `expr` : angle hyperbolique

Exemple :

```
> SELECT cosh(0);
 1.0
```

#### cot

`cot(expr)` : renvoie la cotangente de `expr`, comme si elle était calculée par `1/java.lang.Math.cot`.

Arguments :
- `expr` : angle en radians

Exemple :

```
> SELECT cot(1);
 0.6420926159343306
```

#### dense_rank

`dense_rank()` : calcule le rang d’une valeur dans un groupe de valeurs. Le résultat est de un plus la valeur de rang précédemment attribuée. Contrairement à la fonction `rank`, `dense_rank` ne génère pas d’espacements dans la séquence de classement.

#### e

`e()` : renvoie le nombre d’Euler, e.

Exemple :

```
> SELECT e();
 2.718281828459045
```

#### exp

`exp(expr)` : renvoie e à la puissance de `expr`.

Exemple :

```
> SELECT exp(0);
 1.0
```

#### expml

`expm1(expr)` : renvoie exp(`expr`) - 1.

Exemple :

```
> SELECT expm1(0);
 0.0
```

#### factorial

`factorial(expr)` : renvoie la factorielle de `expr`. `expr` est [0..20]. Sinon, cette valeur est nulle.

Exemple :

```
> SELECT factorial(5);
 120
```

#### floor

`floor(expr)` : renvoie le plus grand entier qui n’est pas supérieur à `expr`.

Exemples :

```
> SELECT floor(-0.1);
 -1
> SELECT floor(5);
 5
```

#### greatest

`greatest(expr, ...)` : renvoie la valeur la plus élevée de tous les paramètres, en ignorant les valeurs nulles.

Exemple :

```
> SELECT greatest(10, 9, 2, 4, 3);
 10
```

#### hypot

`hypot(expr1, expr2)` : renvoie la racine carrée de (`expr1`<sup>2</sup> + `expr2`<sup>2</sup>).

Exemple :

```
> SELECT hypot(3, 4);
 5.0
```

#### kurtosis

`kurtosis(expr)` : renvoie la valeur de kurtosis calculée à partir des valeurs d’un groupe.


#### least

`least(expr, ...)` : renvoie la valeur la plus basse de tous les paramètres, en ignorant les valeurs nulles.

Exemple :

```
> SELECT least(10, 9, 2, 4, 3);
 2
```

#### levenshtein

`levenshtein(str1, str2)` : renvoie la distance de Levenshtein entre deux chaînes données.

Exemples :

```
> SELECT levenshtein('kitten', 'sitting');
 3
```

#### ln

`ln(expr)` : renvoie le logarithme naturel (base e) de `expr`.

Exemple :

```
> SELECT ln(1);
 0.0
```

#### log

`log(base, expr)` : renvoie le logarithme de `expr` de `base`.

Exemple :

```
> SELECT log(10, 100);
 2.0
```

#### log10

`log10(expr)` : renvoie le logarithme de `expr` de base 10.

Exemple :

```
> SELECT log10(10);
 1.0
```

#### log1p

`log1p(expr)` : renvoie `log(1 + expr)`.

Exemple :

```
> SELECT log1p(0);
 0.0
```

#### log2

`log2(expr)` : renvoie le logarithme de `expr` de base 2.

Exemple :

```
> SELECT log2(2);
 1.0
```

#### max

`max(expr)` : renvoie la valeur maximale de `expr`.

#### mean

`mean(expr)` : renvoie la moyenne calculée à partir des valeurs d’un groupe.

#### min

`min(expr)` : renvoie la valeur minimale de `expr`.

#### monotonically_increasing_id

`monotonically_increasing_id()` : renvoie des entiers 64 bits à augmentation monotone. Il est garanti que l’identifiant généré augmente de manière monotone et est unique, mais pas consécutif. La mise en œuvre actuelle place l’identifiant de partition dans les 31 bits supérieurs, tandis que les 33 bits inférieurs représentent le numéro d’enregistrement dans chaque partition. L’hypothèse est que la trame de données compte moins d’un milliard de partitions et que chaque partition compte moins de 8 milliards d’enregistrements. La fonction n’est pas déterministe, car son résultat dépend des identifiants de partition.

#### negative

`negative(expr)` : renvoie la valeur négative de `expr`.

Exemple :

```
> SELECT negative(1);
 -1
```

#### percent_rank

`percent_rank()` : calcule le classement en pourcentage d’une valeur dans un groupe de valeurs.

#### Centile

`percentile(col, percentage [, frequency])` : renvoie la valeur exacte du centile d’une colonne numérique `col` au pourcentage donné. La valeur de `percentage` doit être comprise entre 0,0 et 1,0. La valeur de `frequency` doit être un entier positif.

`percentile(col, array(percentage1 [, percentage2]...) [, frequency])` : renvoie le tableau de valeurs de centiles exactes de la colonne numérique `col` aux pourcentages donnés. Chaque valeur du tableau de pourcentage doit être comprise entre 0,0 et 1,0. La valeur de `frequency` doit être un entier positif.

#### percentile_approx

`percentile_approx(col, percentage [, accuracy])` : renvoie la valeur approximative du centile d’une colonne numérique `col` au pourcentage donné. La valeur de `percentage` doit être comprise entre 0,0 et 1,0. Le paramètre `accuracy` (par défaut : 10000) est un littéral numérique positif contrôlant la précision d’approximation au prix de la mémoire. Une valeur plus élevée de `accuracy` donne une meilleure précision, `1.0/accuracy` étant l’erreur relative de l’approximation. Lorsque `percentage` est un tableau, chaque valeur du tableau de pourcentage doit être comprise entre 0,0 et 1,0. Dans ce cas, la fonction renvoie le tableau de centile approximatif de la colonne `col` pour le tableau de pourcentage donné.

Exemples :

```
> SELECT percentile_approx(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT percentile_approx(10.0, 0.5, 100);
 10.0
```

#### pi

`pi()` : renvoie pi.

Exemple :

```
> SELECT pi();
 3.141592653589793
```

#### pmod

`pmod(expr1, expr2)` : renvoie la valeur positive de `expr1` mod `expr2`.

Exemples :

```
> SELECT pmod(10, 3);
 1
> SELECT pmod(-10, 3);
 2
```

#### positive

`positive(expr)` : renvoie la valeur positive de `expr`.

#### pow

`pow(expr1, expr2)` : élève `expr1` à la puissance de `expr2`.

Exemple :

```
> SELECT pow(2, 3);
 8.0
```

#### power

`power(expr1, expr2)` : élève `expr1` à la puissance de `expr2`.

Exemples :

```
> SELECT power(2, 3);
 8.0
```

#### radians

`radians(expr)` : convertit les degrés en radians.

Arguments :

- `expr` : angle en degrés

Exemple :

```
> SELECT radians(180);
 3.141592653589793
```

#### rand

`rand([seed])` : renvoie une valeur aléatoire parmi des valeurs indépendantes distribuées de manière identique et uniforme (i.i.d.) dans l’intervalle (0, 1).

Exemples :

```
> SELECT rand();
 0.9629742951434543
> SELECT rand(0);
 0.8446490682263027
> SELECT rand(null);
 0.8446490682263027
```

>[!NOTE]
>
>Cette fonction est non déterministe en général.

#### randn

`randn([seed])` : renvoie une valeur aléatoire avec des valeurs indépendantes et distribuées de manière identique (i.i.d.) provenant de la distribution normale standard.

Exemples :

```
> SELECT randn();
 -0.3254147983080288
> SELECT randn(0);
 1.1164209726833079
> SELECT randn(null);
 1.1164209726833079
```

>[!NOTE]
>
>Cette fonction est non déterministe en général.

#### rint

`rint(expr)` : renvoie la valeur double la plus proche en valeur de l’argument et égale à un entier mathématique.

Exemples :

```
> SELECT rint(12.3456);
 12.0
```

#### round

`round(expr, d)` : renvoie `expr` arrondi au nombre de décimales `d` à l’aide du mode arrondi HALF_UP.

Exemple :

```
> SELECT round(2.5, 0);
 3.0
```

#### sign

`sign(expr)` : renvoie -1.0, 0.0 ou 1.0 selon que `expr` est négatif, nul ou positif.

Exemple :

```
> SELECT sign(40);
 1.0
```

#### signum

`signum(expr)` : renvoie -1.0, 0.0 ou 1.0 selon que `expr` est négatif, nul ou positif.

Exemple :

```
> SELECT signum(40);
 1.0
```

#### sin

`sin(expr)` : renvoie le sinus de `expr`, comme s’il était calculé par `java.lang.Math.sin`.

Arguments :

- `expr` : angle en radians

Exemple :

```
> SELECT sin(0);
 0.0
```

#### sinh

`sinh(expr)` : renvoie le sinus hyperbolique de `expr`, comme s’il était calculé par `java.lang.Math.sinh`.

Arguments :

- `expr` : angle hyperbolique

Exemple :

```
> SELECT sinh(0);
 0.0
```

#### sqrt

`sqrt(expr)` : renvoie la racine carrée de `expr`.

Exemple :

```
> SELECT sqrt(4);
 2.0
```

#### stddev

`stddev(expr)` : renvoie l’écart-type d’échantillon calculé à partir des valeurs d’un groupe.

#### stddev_pop

`sttdev_pop(expr)` : renvoie l’écart-type de population calculé à partir des valeurs d’un groupe.

#### stddev_samp

`stddev_samp(expr)` : renvoie l’écart-type d’échantillon calculé à partir des valeurs d’un groupe.

#### sum

`sum(expr)` : renvoie la somme calculée à partir des valeurs d’un groupe.

#### tan

`tan(expr)` : renvoie la tangente de `expr`, comme si elle était calculée par `java.lang.Math.tan`.

Arguments :

- `expr` : angle en radians

Exemple :

```
> SELECT tan(0);
 0.0
```

#### tanh

`tanh(expr)` : renvoie la tangente hyperbolique de `expr`, comme si elle était calculée par `java.lang.Math.tanh`.

Arguments :

- `expr` : angle hyperbolique

Exemple :

```
> SELECT tanh(0);
 0.0
```

#### Var_pop

`var_pop(expr)` : renvoie la variance de population calculée à partir des valeurs d’un groupe.

#### Var_samp

`var_samp(expr)` : renvoie la variance d’échantillon calculée à partir des valeurs d’un groupe.

#### variance

`variance(expr)` : renvoie la variance d’échantillon calculée à partir des valeurs d’un groupe.

### Opérateurs logiques

#### Logical not

`! expr` : logique du « SAUF »

#### Less than

`expr1 < expr2` : renvoie true si `expr1` est inférieur à `expr2`.

Arguments :

- `expr1, expr2` : les deux expressions doivent être du même type ou diffusées sur un type commun et doivent être d’un type organisable. Par exemple, le type map n’est pas organisable, donc n’est pas pris en charge. Pour les types de données tels que les tableaux/structs, les types de données des champs doivent pouvoir être organisés.

Exemples :

```
> SELECT 1 < 2;
 true
> SELECT 1.1 < '1';
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') < to_date('2009-08-01 04:17:52');
 true
> SELECT 1 < NULL;
 NULL
```

#### Less than or equal to

`expr1 <= expr2` : renvoie true si `expr1` est inférieur à ou égal à `expr2`.

Arguments :

- `expr1, expr2` : les deux expressions doivent être du même type ou diffusées sur un type commun et doivent être d’un type organisable. Par exemple, le type map n’est pas organisable, donc n’est pas pris en charge. Pour les types de données tels que les tableaux/structs, les types de données des champs doivent pouvoir être organisés.

Exemples :

```
> SELECT 2 <= 2;
 true
> SELECT 1.0 <= '1';
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') <= to_date('2009-08-01 04:17:52');
 true
> SELECT 1 <= NULL;
 NULL
```

#### Equal to

`expr1 = expr2` : renvoie true si `expr1` est égal à `expr2`, ou false dans le cas contraire.

Arguments :

- `expr1, expr2` : les deux expressions doivent être du même type ou diffusées sur un type commun et doivent être d’un type utilisable dans une comparaison d’égalité. Le type map n’est pas pris en charge. Pour les types de données tels que les tableaux/structs, les types de données des champs doivent pouvoir être organisés.

Exemples :

```
> SELECT 2 = 2;
 true
> SELECT 1 = '1';
 true
> SELECT true = NULL;
 NULL
> SELECT NULL = NULL;
 NULL
```

#### Greater than

`expr1 > expr2` : renvoie true si `expr1` est plus grand que `expr2`.

Arguments :

- `expr1, expr2` : les deux expressions doivent être du même type ou diffusées sur un type commun et doivent être d’un type organisable. Par exemple, le type map n’est pas organisable, donc n’est pas pris en charge. Pour les types de données tels que les tableaux/structs, les types de données des champs doivent pouvoir être organisés.

Exemples :

```
> SELECT 2 > 1;
 true
> SELECT 2 > '1.1';
 true
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-07-30 04:17:52');
 false
> SELECT to_date('2009-07-30 04:17:52') > to_date('2009-08-01 04:17:52');
 false
> SELECT 1 > NULL;
 NULL
```

#### Greater than or equal to

`expr1 >= expr2` : renvoie true si `expr1` est supérieur à ou égal à `expr2`.

Arguments :

- `expr1, expr2` : les deux expressions doivent être du même type ou diffusées sur un type commun et doivent être d’un type organisable. Par exemple, le type map n’est pas organisable, donc n’est pas pris en charge. Pour les types de données tels que les tableaux/structs, les types de données des champs doivent pouvoir être organisés.

Exemples :

```
> SELECT 2 >= 1;
 true
> SELECT 2.0 >= '2.1';
 false
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-07-30 04:17:52');
 true
> SELECT to_date('2009-07-30 04:17:52') >= to_date('2009-08-01 04:17:52');
 false
> SELECT 1 >= NULL;
 NULL
```

#### Bitwise exclusive or

`expr1 ^ expr2` : renvoie le résultat exclusif au niveau du bit OU `expr1` et `expr2`.

Exemple :

```
> SELECT 3 ^ 5;
 2
```

#### and

`expr1 and expr2` : logique du « ET ».

#### arrays_overlap

`arrays_overlap(a1, a2)` : renvoie true si a1 contient au moins un élément non nul également présent dans a2. Si les tableaux n’ont aucun élément commun et qu’ils sont tous deux non vides et que l’un d’eux contient un élément nul, la valeur null est renvoyée. Sinon, la valeur false est renvoyée.

Exemple :

```
> SELECT arrays_overlap(array(1, 2, 3), array(3, 4, 5));
 true
```

Depuis : 2.4.0

#### assert_true

`assert_true(expr)` : lance une exception si `expr` n’est pas vrai.

Exemple :

```
> SELECT assert_true(0 < 1);
 NULL
```

#### if

`if(expr1, expr2, expr3)` : si `expr1` est évalué comme true, la fonction renvoie `expr2` ; sinon, elle renvoie `expr3`.

Exemple :

```
> SELECT if(1 < 2, 'a', 'b');
 a
```

#### ifnull

`ifnull(expr1, expr2)` : renvoie `expr2` si `expr1` est nul ou `expr1` dans le cas contraire.

Exemple :

```
> SELECT ifnull(NULL, array('2'));
 ["2"]
```

#### in

`expr1 in(expr2, expr3, ...)` : renvoie true si `expr` est égal à valN.

Arguments :
- `expr1, expr2, expr3, ...` : les arguments doivent être du même type.

Exemples :

```
> SELECT 1 in(1, 2, 3);
 true
> SELECT 1 in(2, 3, 4);
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 1), named_struct('a', 1, 'b', 3));
 false
> SELECT named_struct('a', 1, 'b', 2) in(named_struct('a', 1, 'b', 2), named_struct('a', 1, 'b', 3));
 true
```

#### isnan

`isnan(expr)` : renvoie true si `expr` est de type NaN ou false dans le cas contraire.

Exemple :

```
> SELECT isnan(cast('NaN' as double));
 true
```

#### isnotnull

`isnotnull(expr)` : renvoie true si `expr` n’est pas nul ou false dans le cas contraire.

Exemples :

```
> SELECT isnotnull(1);
 true
```

#### isnull

`isnull(expr)` : renvoie true si `expr` est nul ou false dans le cas contraire.

Exemple :

```
> SELECT isnull(1);
 false
```

#### nanvl

`nanvl(expr1, expr2)` : renvoie `expr1` s’il ne s’agit pas d’une valeur NaN ou `expr2` dans le cas contraire.

Exemple :

```
> SELECT nanvl(cast('NaN' as double), 123);
 123.0
```

#### not

`not expr` : logique du « SAUF »

#### or

`expr1 or expr2` : logique du « OU »

#### xpath_boolean

`xpath_boolean(xml, xpath)` : renvoie true si l’expression XPath est évaluée comme true ou si un nœud correspondant est trouvé.

Exemple :

```
> SELECT xpath_boolean('<a><b>1</b></a>','a/b');
 true
```

### Fonctions de date/heure

#### add_months

`add_months(start_date, num_months)` : renvoie la date postérieure de `num_months` à `start_date`.

Exemple :

```
> SELECT add_months('2016-08-31', 1);
 2016-09-30
```

Depuis : 1.5.0

#### date_add

`date_add(start_date, num_days)` : renvoie la date postérieure de `num_days` à `start_date`.

Exemple :

```
> SELECT date_add('2016-07-30', 1);
 2016-07-31
```

Depuis : 1.5.0

#### date_format

`date_format(timestamp, fmt)` : convertit `timestamp` en valeur de chaîne au format spécifié par le format de date `fmt`.

Exemple :

```
> SELECT date_format('2016-04-08', 'y');
 2016
```

Depuis : 1.5.0

#### date_sub

`date_sub(start_date, num_days)` : renvoie la date antérieure de `num_days` à `start_date`.

Exemple :

```
> SELECT date_sub('2016-07-30', 1);
 2016-07-29
```

Depuis : 1.5.0

#### date_trunc

`date_trunc(fmt, ts)` : renvoie l’horodatage (ts) tronqué à l’unité spécifiée par le modèle de format `fmt`. `fmt` doit être l’une des valeurs suivantes : [« YEAR », « YYYY », « YY », « MON », « MONTH », « MM », « DAY », « DD », « HOUR », « MINUTE », « SECOND », « WEEK », « QUARTER »]

Exemples :

```
> SELECT date_trunc('YEAR', '2015-03-05T09:32:05.359');
 2015-01-01 00:00:00
> SELECT date_trunc('MM', '2015-03-05T09:32:05.359');
 2015-03-01 00:00:00
> SELECT date_trunc('DD', '2015-03-05T09:32:05.359');
 2015-03-05 00:00:00
> SELECT date_trunc('HOUR', '2015-03-05T09:32:05.359');
 2015-03-05 09:00:00
```

Depuis : 2.3.0

#### datediff

`datediff(endDate, startDate)` : renvoie le nombre de jours compris entre `startDate` et `endDate`.

Exemples :

```
> SELECT datediff('2009-07-31', '2009-07-30');
 1

> SELECT datediff('2009-07-30', '2009-07-31');
 -1
```

Depuis : 1.5.0

#### day

`day(date)` : renvoie le jour du mois de la date/l’horodatage.

Exemple :

```
> SELECT day('2009-07-30');
 30
```

Depuis : 1.5.0

#### dayofmonth

`dayofmonth(date)` : renvoie le jour du mois de la date/l’horodatage.

Exemple :

```
> SELECT dayofmonth('2009-07-30');
 30
```

Depuis : 1.5.0

#### dayofweek

`dayofweek(date)` : renvoie le jour de la semaine pour la date/l’horodatage (1 = dimanche, 2 = lundi, ..., 7 = samedi).

Exemple :

```
> SELECT dayofweek('2009-07-30');
 5
```

Depuis : 2.3.0

#### dayofyear

`dayofyear(date)` : renvoie le jour de l’année de la date/l’horodatage.

Exemple :

```
> SELECT dayofyear('2016-04-09');
 100
```

Depuis : 1.5.0

#### from_unixtime

`from_unixtime(unix_time, format)` : renvoie `unix_time` dans le `format` spécifié.

Exemple :

```
> SELECT from_unixtime(0, 'yyyy-MM-dd HH:mm:ss');
 1970-01-01 00:00:00
```

Depuis : 1.5.0

#### from_utc_timestamp

`from_utc_timestamp(timestamp, timezone)` : interprète un horodatage comme « 2017-07-14 02:40:00.0 » en heure en UTC et convertit cette heure en horodatage dans le fuseau horaire donné. Par exemple, pour le fuseau « GMT+1 », cela donnerait « 2017-07-14 03:40:00.0 ».

Exemple :

```
> SELECT from_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-31 09:00:00
```

Depuis : 1.5.0

#### hour

`hour(timestamp)` : renvoie le composant d’heure de la chaîne/l’horodatage.

Exemple :

```
> SELECT hour('2009-07-30 12:58:59');
 12
```

Depuis : 1.5.0

#### last_day

`last_day(date):` renvoie le dernier jour du mois auquel la date se rapporte.

Exemple :

```
> SELECT last_day('2009-01-12');
 2009-01-31
```

Depuis : 1.5.0

#### minute

`minute(timestamp)` : renvoie le composant des minutes de la chaîne/l’horodatage.

Exemple :

```
> SELECT minute('2009-07-30 12:58:59');
 58
```

Depuis : 1.5.0

#### month

`month(date)` : renvoie le composant du mois de la date/l’horodatage.

Exemple :

```
> SELECT month('2016-07-30');
 7
```

Depuis : 1.5.0

#### months_between

`months_between(timestamp1, timestamp2[, roundOff])` : si `timestamp1` est postérieur à `timestamp2`, alors le résultat est positif. Si `timestamp1` et `timestamp2` concernent le même jour du mois ou le dernier jour du mois, l’heure du jour est ignorée. Dans le cas contraire, la différence est calculée sur la base de 31 jours par mois et arrondie à 8 chiffres, sauf si `roundOff=false`.

Exemples :

```
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30');
 3.94959677
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30', false);
 3.9495967741935485
```

Depuis : 1.5.0

#### next_day

`next_day(start_date, day_of_week)` : renvoie la première date postérieure à `start_date` et nommée comme indiqué.

Exemple :

```
> SELECT next_day('2015-01-14', 'TU');
 2015-01-20
```

Depuis : 1.5.0

#### quarter

`quarter(date)` : renvoie le trimestre de l’année correspondant à la date, dans la plage 1 à 4.

Exemple :

```
> SELECT quarter('2016-08-31');
 3
```

Depuis : 1.5.0

#### second

`second(timestamp)` : renvoie le composant des secondes de la chaîne/l’horodatage.

Exemple :

```
> SELECT second('2009-07-30 12:58:59');
 59
```

Depuis : 1.5.0

#### to_date

`to_date(date_str[, fmt])` : analyse l’expression `date_str` avec l’expression `fmt` d’une date. Renvoie la valeur null avec une entrée non valide. Suit par défaut les règles de diffusion d’une date si la valeur `fmt` est omise.

Exemples :

```
> SELECT to_date('2009-07-30 04:17:52');
 2009-07-30
> SELECT to_date('2016-12-31', 'yyyy-MM-dd');
 2016-12-31
```

Depuis : 1.5.0

#### to_timestamp

`to_timestamp(timestamp[, fmt])` : analyse l’expression `timestamp` avec l’expression `fmt` d’un horodatage. Renvoie la valeur null avec une entrée non valide. Suit par défaut les règles de diffusion d’un horodatage si la valeur `fmt` est omise.

Exemples :

```
> SELECT to_timestamp('2016-12-31 00:12:00');
 2016-12-31 00:12:00
> SELECT to_timestamp('2016-12-31', 'yyyy-MM-dd');
 2016-12-31 00:00:00
```

Depuis : 2.2.0

#### to_unix_timestamp

`to_unix_timestamp(expr[, pattern])` : renvoie l’horodatage UNIX de l’heure donnée.

Exemple :

```
> SELECT to_unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Depuis : 1.6.0

#### to_utc_timestamp

`to_utc_timestamp(timestamp, timezone)` : interprète un horodatage comme « 2017-07-14 02:40:00.0 » en heure dans le fuseau horaire donné et convertit cette heure en horodatage en UTC. Par exemple, pour le fuseau « GMT+1 », cela donnerait « 2017-07-14 01:40:00.0 ».

Exemple :

```
> SELECT to_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-30 15:00:00
```

Depuis : 1.5.0

#### trunc

`trunc(date, fmt)` : renvoie la date avec la partie horaire du jour tronquée à l’unité spécifiée par le modèle de format `fmt`. `fmt` peut prendre l’une des valeurs [« year », « yyyy », « yy », « mon », « month », « mm »]

Exemples :

```
> SELECT trunc('2009-02-12', 'MM');
 2009-02-01
> SELECT trunc('2015-10-27', 'YEAR');
 2015-01-01
```

Depuis : 1.5.0

#### unix_timestamp

`unix_timestamp([expr[, pattern]])` : renvoie l’horodatage UNIX de l’heure actuelle ou spécifiée.

Exemples :

```
> SELECT unix_timestamp();
 1476884637
> SELECT unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Depuis : 1.5.0

#### weekday

`weekday(date)` : renvoie le jour de la semaine pour la date/l’horodatage (0 = lundi, 1 = mardi, ..., 6 = dimanche).

Exemple :

```
> SELECT weekday('2009-07-30');
 3
```

Depuis : 2.4.0

#### week_of_year

`weekofyear(date)` : renvoie la semaine de l’année de la date donnée. On considère qu’une semaine commence le lundi, et la semaine 1 est la première semaine avec plus de 3 jours.

Exemple :

```
> SELECT weekofyear('2008-02-20');
 8
```

Depuis : 1.5.0

#### when

`CASE WHEN expr1 THEN expr2 [WHEN expr3 THEN expr4]* [ELSE expr5] END` : si `expr1` = true, la fonction renvoie `expr2` ; si `expr3` = true, la fonction renvoie `expr4` ; sinon elle renvoie `expr5`.

Arguments :

- `expr1`, `expr3` : les expressions de condition de branche doivent toutes être de type booléen.
- `expr2`, `expr4`, `expr5` : les expressions de valeur de branche et l’expression de la valeur else doivent toutes être du même type ou convertibles en un type commun.

Exemples :

```
> SELECT CASE WHEN 1 > 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 1
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 2
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 < 0 THEN 2.0 END;
 NULL
```

#### year

`year(date)` : renvoie le composant de l’année de la date/l’horodatage.

Exemple :

```
> SELECT year('2016-07-30');
 2016
```

Depuis : 1.5.0

### Fonctions d’agrégation

#### approx_count_distinct

`approx_count_distinct(expr[, relativeSD])` : renvoie la cardinalité estimée par HyperLogLog++. `relativeSD` définit l’erreur d’estimation maximale autorisée.

### Tableaux

#### array

`array(expr, ...)` : renvoie un tableau avec les éléments donnés.

Exemple :

```
> SELECT array(1, 2, 3);
 [1,2,3]
```

#### array_contains

`array_contains(array, value)` : renvoie true si le tableau contient la valeur.

Exemple :

```
> SELECT array_contains(array(1, 2, 3), 2);
 true
```

#### array_distinct

`array_distinct(array)` : supprime les doublons du tableau.

Exemple :

```
> SELECT array_distinct(array(1, 2, 3, null, 3));
 [1,2,3,null]
```

Depuis : 2.4.0

#### array_except

`array_except(array1, array2)` : renvoie un tableau des éléments de `array1`, mais pas de `array2`, sans les doublons.

Exemple :

```
> SELECT array_except(array(1, 2, 3), array(1, 3, 5));
 [2]
```

Depuis : 2.4.0

#### array_intersect

`array_intersect(array1, array2)` : renvoie un tableau des éléments situés à l’intersection de `array1` et de `array2`, sans les doublons.

Exemple :

```
> SELECT array_intersect(array(1, 2, 3), array(1, 3, 5));
 [1,3]
```

Depuis : 2.4.0

#### array_join

`array_join(array, delimiter[, nullReplacement])` : concatène les éléments du tableau donné à l’aide du délimiteur et d’une chaîne facultative pour remplacer les valeurs nulles. Si aucune valeur n’est définie pour `nullReplacement`, les éventuelles valeurs nulles sont filtrées.

Exemples :

```
> SELECT array_join(array('hello', 'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ', ',');
 hello , world
```

Depuis : 2.4.0

#### array_max

`array_max(array)` : renvoie la valeur maximale dans le tableau. Les éléments nuls sont ignorés.

Exemple :

```
> SELECT array_max(array(1, 20, null, 3));
 20
```

Depuis : 2.4.0

#### array_min

`array_min(array)` : renvoie la valeur minimale dans le tableau. Les éléments nuls sont ignorés.

Exemple :

```
> SELECT array_min(array(1, 20, null, 3));
 1
```

Depuis : 2.4.0

#### array_position

`array_position(array, element)` : renvoie l’index (de base 1) du premier élément du tableau aussi long.

Exemple :

```
> SELECT array_position(array(3, 2, 1), 1);
 3
```

Depuis : 2.4.0

#### array_remove

`array_remove(array, element)` : supprime tous les éléments égaux à l’élément du tableau.

Exemple :

```
> SELECT array_remove(array(1, 2, 3, null, 3), 3);
 [1,2,null]
```

Depuis : 2.4.0

#### array_repeat

`array_repeat(element, count)` : renvoie le tableau contenant le nombre de répétitions des éléments.

Exemple :

```
> SELECT array_repeat('123', 2);
 ["123","123"]
```

Depuis : 2.4.0

#### array_sort

`array_sort(array)` : trie le tableau d’entrée par ordre croissant. Les éléments du tableau d’entrée doivent pouvoir être classés. Les éléments nuls sont placés à la fin du tableau renvoyé.

Exemple :

```
> SELECT array_sort(array('b', 'd', null, 'c', 'a'));
 ["a","b","c","d",null]
```

Depuis : 2.4.0

#### array_union

`array_union(array1, array2)` : renvoie un tableau des éléments inclus dans l’union entre `array1` et `array2`, sans les doublons.

Exemple :

```
> SELECT array_union(array(1, 2, 3), array(1, 3, 5));
 [1,2,3,5]
```

Depuis : 2.4.0

#### array_zip

`arrays_zip(a1, a2, ...)` : renvoie un tableau fusionné de structs dans lequel le struct N contient toutes les valeurs N des tableaux d’entrée.

Exemples :

```
> SELECT arrays_zip(array(1, 2, 3), array(2, 3, 4));
 [{"0":1,"1":2},{"0":2,"1":3},{"0":3,"1":4}]
> SELECT arrays_zip(array(1, 2), array(2, 3), array(3, 4));
 [{"0":1,"1":2,"2":3},{"0":2,"1":3,"2":4}]
```

Depuis : 2.4.0

#### element_at

`element_at(array, index)` : renvoie l’élément du tableau à l’index donné (de base 1). Si `index < 0`, l’accès aux éléments se fait du dernier au premier. Renvoie NULL si l’index dépasse la longueur du tableau.

`element_at(map, key)` : renvoie la valeur d’une clé donnée ou NULL si la clé n’est pas incluse dans la map.

Exemples :

```
> SELECT element_at(array(1, 2, 3), 2);
 2
> SELECT element_at(map(1, 'a', 2, 'b'), 2);
 b
```

Depuis : 2.4.0

#### explode

`explode(expr)` : sépare les éléments de l’`expr` de tableau en plusieurs lignes, ou les éléments de l’`expr` de map en plusieurs lignes et colonnes.

Exemples :

```
> SELECT explode(array(10, 20));
 10
 20
```

#### explode_outer

`explode_outer(expr)` : sépare les éléments de l’`expr` de tableau en plusieurs lignes, ou les éléments de l’`expr` de map en plusieurs lignes et colonnes.

Exemple :

```
> SELECT explode_outer(array(10, 20));
 10
 20
```

#### find_in_set

`find_in_set(str, str_array)` : renvoie l’index (de base 1) de la chaîne donnée (`str`) dans la liste délimitée par des virgules (`str_array`). Renvoie 0 si la chaîne est introuvable ou si la chaîne donnée (`str`) contient une virgule.

Exemple :

```
> SELECT find_in_set('ab','abc,b,ab,c,def');
 3
```

#### flatten

`flatten(arrayOfArrays)` : transforme un tableau de tableaux en tableau unique.

Exemple :

```
> SELECT flatten(array(array(1, 2), array(3, 4)));
 [1,2,3,4]
```

Depuis : 2.4.0

#### inline

`inline(expr)` : morcelle un tableau de structs en un tableau.

Exemple :

```
> SELECT inline(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### inline_outer

`inline_outer(expr)` : morcelle un tableau de structs en un tableau.

Exemple :

```
> SELECT inline_outer(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### posexplode

`posexplode(expr)` : sépare les éléments de l’`expr` de tableau en plusieurs lignes, ou les éléments de l’`expr` de map en plusieurs lignes et colonnes à positions.

Exemple :

```
> SELECT posexplode(array(10,20));
 0  10
 1  20
```

#### posexplode_outer

`posexplode_outer(expr)` : sépare les éléments de l’`expr` de tableau en plusieurs lignes, ou les éléments de l’`expr` de map en plusieurs lignes et colonnes à positions.

Exemple :

```
> SELECT posexplode_outer(array(10,20));
 0  10
 1  20
```

#### reverse

`reverse(array)` : renvoie une chaîne inversée ou un tableau avec l’ordre inverse des éléments.

Exemples :

```
> SELECT reverse('Spark SQL');
 LQS krapS
> SELECT reverse(array(2, 1, 4, 3));
 [3,4,1,2]
```

Depuis : 1.5.0
>[!NOTE]
>
>La logique rse pour les tableaux est disponible depuis la version 2.4.0.

#### shuffle

`shuffle(array)` : renvoie une permutation aléatoire du tableau donné.

Exemples :

```
> SELECT shuffle(array(1, 20, 3, 5));
 [3,1,5,20]
> SELECT shuffle(array(1, 20, null, 3));
 [20,null,3,1]
```

Depuis : 2.4.0
>[!NOTE]
>
>La fonction  est non déterministe.

#### slice

`slice(x, start, length)` : sous-définit le tableau x à partir du début de l’index (ou à partir de la fin si le début est négatif) avec la longueur spécifiée.

Exemples :

```
> SELECT slice(array(1, 2, 3, 4), 2, 2);
 [2,3]
> SELECT slice(array(1, 2, 3, 4), -2, 2);
 [3,4]
```

Depuis : 2.4.0

#### sort_array

`sort_array(array[, ascendingOrder])` : trie le tableau d’entrée par ordre croissant ou décroissant selon l’ordre naturel des éléments du tableau. Les éléments nuls sont placés au début du tableau renvoyé par ordre croissant ou à la fin du tableau renvoyé par ordre décroissant.

Exemples :

```
> SELECT sort_array(array('b', 'd', null, 'c', 'a'), true);
 [null,"a","b","c","d"]
```

#### zip_with

`zip_with(left, right, func)` : fusionne les deux tableaux donnés, au niveau de l’élément, en un tableau unique à l’aide de la fonction. Si un tableau est plus court, les valeurs nulles sont ajoutées à la fin, pour correspondre à la longueur du tableau plus long, avant l’application de la fonction.

Exemples :

```
> SELECT zip_with(array(1, 2, 3), array('a', 'b', 'c'), (x, y) -> (y, x));
 [{"y":"a","x":1},{"y":"b","x":2},{"y":"c","x":3}]
> SELECT zip_with(array(1, 2), array(3, 4), (x, y) -> x + y);
 [4,6]
> SELECT zip_with(array('a', 'b', 'c'), array('d', 'e', 'f'), (x, y) -> concat(x, y));
 ["ad","be","cf"]
```

Depuis : 2.4.0

### Fonctions de diffusion du type de données

#### bigint

`bigint(expr)` : diffuse la valeur `expr` vers le type de données cibles `bigint`.

#### binary

`binary(expr)` : diffuse la valeur `expr` vers le type de données cibles `binary`.

#### boolean

`boolean(expr)` : diffuse la valeur `expr` vers le type de données cibles `boolean`.

#### cast

`cast(expr AS type)` : diffuse la valeur `expr` vers le type de données cibles `type`.

Exemple :

```
> SELECT cast('10' as int);
 10
```

#### date

`date(expr)` : diffuse la valeur `expr` vers le type de données cibles `date`.

#### decimal

`decimal(expr)` : diffuse la valeur `expr` vers le type de données cibles `decimal`.

#### double

`double(expr)` : diffuse la valeur `expr` vers le type de données cibles `double`.

#### float

`float(expr)` : diffuse la valeur `expr` vers le type de données cibles `float`.

#### int

`int(expr)` : diffuse la valeur `expr` vers le type de données cibles `int`.

#### map

`map(key0, value0, key1, value1, ...)` : crée une map avec les paires clé/valeur données.

Exemple :

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### smallint

`smallint(expr)` : diffuse la valeur `expr` vers le type de données cibles `smallint`.

#### str_to_map

`str_to_map(text[, pairDelim[, keyValueDelim]])` : crée une map après avoir divisé le texte en paires clé/valeur à l’aide de délimiteurs. Les délimiteurs par défaut sont « , » pour `pairDelim` et « : » pour `keyValueDelim`.

Exemples :

```
> SELECT str_to_map('a:1,b:2,c:3', ',', ':');
 map("a":"1","b":"2","c":"3")
> SELECT str_to_map('a');
 map("a":null)
```

#### string

`string(expr)` : diffuse la valeur `expr` vers le type de données cibles `string`.

#### struct

`struct(col1, col2, col3, ...)` : crée un struct avec les valeurs de champ données.

#### tinyint

`tinyint(expr)` : diffuse la valeur `expr` vers le type de données cibles `tinyint`.

### Fonctions de conversion et de formatage

#### ascii

`ascii(str)` : renvoie la valeur numérique du premier caractère de `str`.

Exemples :

```
> SELECT ascii('222');
 50
> SELECT ascii(2);
 50
```

#### base64

`base64(bin)` : convertit l’argument d’un `bin` binaire en chaîne en base 64.

Exemple :

```
> SELECT base64('Spark SQL');
 U3BhcmsgU1FM
```

#### bin

`bin(expr)` : renvoie la représentation sous la forme de chaîne de la valeur longue `expr` représentée en binaire.

Exemples :

```
> SELECT bin(13);
 1101
> SELECT bin(-13);
 1111111111111111111111111111111111111111111111111111111111110011
> SELECT bin(13.3);
 1101
```

#### bit_length

`bit_length(expr)` : renvoie la longueur en bits des données de chaîne ou le nombre de bits de données binaires.

Exemple :

```
> SELECT bit_length('Spark SQL');
 72
```

#### char

`char(expr)` : renvoie le caractère ASCII dont le binaire équivaut à `expr`. Si n est supérieur à 256, le résultat équivaut à `chr(n % 256)`.

Exemple :

```
> SELECT char(65);
 A
```

#### char_length

`char_length(expr)` : renvoie la longueur en caractères des données de chaîne ou le nombre de bits de données binaires. La longueur des données de chaîne inclut les espaces à la fin. La longueur des données binaires inclut des zéros binaires.

Exemples :

```
> SELECT char_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### character_length

`character_length(expr)` : renvoie la longueur en caractères des données de chaîne ou le nombre de bits de données binaires. La longueur des données de chaîne inclut les espaces à la fin. La longueur des données binaires inclut des zéros binaires.

Exemples :

```
> SELECT character_length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### chr

`chr(expr)` : renvoie le caractère ASCII dont le binaire équivaut à expr. Si n est supérieur à 256, le résultat équivaut à `chr(n % 256)`.

Exemple :

```
> SELECT chr(65);
 A
```

#### degrees

`degrees(expr)` : convertit les radians en degrés.

Arguments :
- `expr` : angle en radians

Exemple :

```
> SELECT degrees(3.141592653589793);
 180.0
```

#### format_number

`format_number(expr1, expr2)` : rédige le nombre `expr1` au format « #,###,###.## » arrondi au nombre de décimales `expr2`. Si `expr2` a une valeur de 0, le résultat ne comporte pas de décimal ni de partie fractionnaire. `expr2` accepte aussi un format spécifié par l’utilisateur. Ce format est destiné à fonctionner comme le `FORMAT` MySQL.

Exemples :

```
> SELECT format_number(12332.123456, 4);
 12,332.1235
> SELECT format_number(12332.123456, '##################.###');
 12332.123
```

#### from_json

`from_json(jsonStr, schema[, options])` : renvoie une valeur struct avec les `jsonStr` et `schema` donnés.

Exemples :

```
> SELECT from_json('{"a":1, "b":0.8}', 'a INT, b DOUBLE');
 {"a":1, "b":0.8}
> SELECT from_json('{"time":"26/08/2015"}', 'time Timestamp', map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"2015-08-26 00:00:00.0"}
```

Depuis : 2.2.0

#### hash

`hash(expr1, expr2, ...)` : renvoie une valeur de hachage des arguments.

Exemple :

```
> SELECT hash('Spark', array(123), 2);
 -1321691492
```

#### hex

`hex(expr)` : convertit `expr` en hexadécimal.

Exemples :

```
> SELECT hex(17);
 11
> SELECT hex('Spark SQL');
 537061726B2053514C
```

#### initcap

`initcap(str)` : renvoie `str` avec la première lettre de chaque mot en majuscule. Toutes les autres lettres sont en minuscules. Les mots sont délimités par des espaces blancs.

Exemple :

```
> SELECT initcap('sPark sql');
 Spark Sql
```

#### lcase

`lcase(str)` : renvoie `str` avec tous les caractères modifiés en minuscules.

Exemple :

```
> SELECT lcase('SparkSql');
 sparksql
```

#### lower

`lower(str)` : renvoie `str` avec tous les caractères modifiés en minuscules.

Exemple :

```
> SELECT lower('SparkSql');
 sparksql
```

#### lpad

`lpad(str, len, pad)` : renvoie `str` justifié à gauche avec `pad` d’une longueur de `len`. Si `str` est plus long que `len`, la valeur renvoyée est raccourcie au nombre de caractères de `len`.

Exemples :

```
> SELECT lpad('hi', 5, '??');
 ???hi
> SELECT lpad('hi', 1, '??');
 h
```

#### map

`map(key0, value0, key1, value1, ...)` : crée une map avec les paires clé/valeur données.

Exemple :

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### map_from_arrays

`map_from_arrays(keys, values)` : crée une map avec une paire des tableaux clé/valeur donnés. Les éléments des clés ne peuvent pas être nuls.

Exemple :

```
> SELECT map_from_arrays(array(1.0, 3.0), array('2', '4'));
 {1.0:"2",3.0:"4"}
```

Depuis : 2.4.0

#### map_from_entries

`map_from_entries(arrayOfEntries)` : renvoie une map créée à partir du tableau d’entrées donné.

Exemple :

```
> SELECT map_from_entries(array(struct(1, 'a'), struct(2, 'b')));
 {1:"a",2:"b"}
```

Depuis : 2.4.0

#### md5

`md5(expr)` : renvoie une somme de contrôle MD5 à 128 bits sous la forme d’une chaîne hexadécimale de `expr`.

Exemple :

```
> SELECT md5('Spark');
 8cde774d6f7333752ed72cacddb05126
```

#### rpad

`rpad(str, len, pad)` : renvoie `str` justifié à droite avec `pad` d’une longueur de `len`. Si `str` est plus long que `len`, la valeur renvoyée est raccourcie au nombre de caractères de `len`.

Exemples :

```
> SELECT rpad('hi', 5, '??');
 hi???
> SELECT rpad('hi', 1, '??');
 h
```

#### rtrim

`rtrim(str)` : supprime les espaces à la fin de `str`.

`rtrim(trimStr, str)` : supprime la chaîne de fin, qui contient les caractères de la chaîne de rognage de `str`.

Arguments :
- `str` : une expression de chaîne
- `trimStr` : les caractères de chaîne de rognage à rogner. La valeur par défaut est une espace unique.

Exemples :

```
> SELECT rtrim('    SparkSQL   ');
 SparkSQL
> SELECT rtrim('LQSa', 'SSparkSQLS');
 SSpark
```

#### sha

`sha(expr)` : renvoie une valeur de hachage `sha1` sous la forme d’une chaîne hexadécimale de l’`expr`.

Exemple :

```
> SELECT sha('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha1

`sha1(expr)` : renvoie une valeur de hachage `sha1` sous la forme d’une chaîne hexadécimale de l’`expr`.

Exemple :

```
> SELECT sha1('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha2

`sha2(expr, bitLength)` : renvoie une somme de contrôle de la famille SHA-2 sous la forme d’une chaîne hexadécimale de l’`expr`. Les formats SHA-224, SHA-256, SHA-384 et SHA-512 sont pris en charge. Une longueur en bit de 0 équivaut à 256.

Exemple :

```
> SELECT sha2('Spark', 256);
 529bc3b07127ecb7e53a4dcf1991d9152c24537d919178022b2c42657f79a26b
```

#### soundex

`soundex(str)` : renvoie le code Soundex de la chaîne.

Exemple :

```
> SELECT soundex('Miller');
 M460
```

#### stack

`stack(n, expr1, ..., exprk)` : sépare `expr1`, ..., `exprk` en `n` lignes.

Exemple :

```
> SELECT stack(2, 1, 2, 3);
 1  2
 3  NULL
```

#### substr

`substr(str, pos[, len])` : renvoie la sous-chaîne de `str`, qui démarre à `pos` et a une longueur de `len`, ou la tranche du tableau d’octet qui démarre à `pos` et a une longueur de `len`.

Exemples :

```
> SELECT substr('Spark SQL', 5);
 k SQL
> SELECT substr('Spark SQL', -3);
 SQL
> SELECT substr('Spark SQL', 5, 1);
 k
```

#### substring

`substring(str, pos[, len])` : renvoie la sous-chaîne de `str`, qui démarre à `pos` et a une longueur de `len`, ou la tranche du tableau d’octet qui démarre à `pos` et a une longueur de `len`.

Exemples :

```
> SELECT substring('Spark SQL', 5);
 k SQL
> SELECT substring('Spark SQL', -3);
 SQL
> SELECT substring('Spark SQL', 5, 1);
 k
```

#### to_json

`to_json(expr[, options])` : renvoie une chaîne JSON avec une valeur struct donnée.

Exemples :

```
> SELECT to_json(named_struct('a', 1, 'b', 2));
 {"a":1,"b":2}
> SELECT to_json(named_struct('time', to_timestamp('2015-08-26', 'yyyy-MM-dd')), map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"26/08/2015"}
> SELECT to_json(array(named_struct('a', 1, 'b', 2)));
 [{"a":1,"b":2}]
> SELECT to_json(map('a', named_struct('b', 1)));
 {"a":{"b":1}}
> SELECT to_json(map(named_struct('a', 1),named_struct('b', 2)));
 {"[1]":{"b":2}}
> SELECT to_json(map('a', 1));
 {"a":1}
> SELECT to_json(array((map('a', 1))));
 [{"a":1}]
```

Depuis : 2.2.0

#### translate

`translate(input, from, to)` : traduit la chaîne `input` en remplaçant les caractères présents dans la chaîne `from` par les caractères correspondants dans la chaîne `to`.

Exemple :

```
> SELECT translate('AaBbCc', 'abc', '123');
 A1B2C3
```

#### trim

`trim(str)` : supprime les espaces au début et à la fin de `str`.

`trim(BOTH trimStr FROM str)` : supprime les caractères `trimStr` au début et à la fin de `str`.

`trim(LEADING trimStr FROM str)` : supprime les caractères `trimStr` au début de `str`.

`trim(TRAILING trimStr FROM str)` : supprime les caractères `trimStr` à la fin de `str`.

Arguments :
- `str` : une expression de chaîne
- `trimStr` : les caractères de chaîne de rognage à rogner, la valeur par défaut étant une espace unique.
- `BOTH`, `FROM` : mots-clés servant à spécifier les caractères de chaîne de rognage aux deux extrémités de la chaîne.
- `LEADING`, `FROM` : mots-clés servant à spécifier les caractères de chaîne de rognage depuis l’extrémité gauche de la chaîne.
- `TRAILING`, `FROM` : mots-clés servant à spécifier les caractères de chaîne de rognage depuis l’extrémité droite de la chaîne.

Exemples :

```
> SELECT trim('    SparkSQL   ');
 SparkSQL
> SELECT trim('SL', 'SSparkSQLS');
 parkSQ
> SELECT trim(BOTH 'SL' FROM 'SSparkSQLS');
 parkSQ
> SELECT trim(LEADING 'SL' FROM 'SSparkSQLS');
 parkSQLS
> SELECT trim(TRAILING 'SL' FROM 'SSparkSQLS');
 SSparkSQ
```

#### ucase

`ucase(str)` : renvoie `str` avec tous les caractères modifiés en majuscules.

Exemple :

```
> SELECT ucase('SparkSql');
 SPARKSQL
```

#### unbase64

`unbase64(str)` : convertit l’argument d’un `str` à chaîne en base 64 en binaire.

Exemple :

```
> SELECT unbase64('U3BhcmsgU1FM');
 Spark SQL
```

#### unhex

`unhex(expr)` : convertit l’`expr` hexadécimal en binaire.

Exemple :

```
> SELECT decode(unhex('537061726B2053514C'), 'UTF-8');
 Spark SQL
```

#### upper

`upper(str)` : renvoie `str` avec tous les caractères modifiés en majuscules.

Exemple :

```
> SELECT upper('SparkSql');
 SPARKSQL
```

#### uuid

`uuid()` : renvoie une chaîne d’identifiant unique universelle (UUID). La valeur est renvoyée sous la forme d’une chaîne UUID canonique de 36 caractères.

Exemple :

```
> SELECT uuid();
 46707d92-02f4-4817-8116-a4c3b23e6266
```

>[!NOTE]
>
>La fonction  est non déterministe.

### Évaluation des données

#### coalesce

`coalesce(expr1, expr2, ...)` : renvoie le premier argument non nul s’il existe. Sinon, cette valeur est nulle.

Exemple :

```
> SELECT coalesce(NULL, 1, NULL);
 1
```

#### collect_list

`collect_list(expr)` : collecte et renvoie une liste d’éléments non uniques.

#### collect_set

`collect_set(expr)` : collecte et renvoie une liste d’éléments uniques.

#### concat

`concat(col1, col2, ..., colN)` : renvoie la concaténation de col1, col2, ..., colN.

Exemples :

```
> SELECT concat('Spark', 'SQL');
 SparkSQL
> SELECT concat(array(1, 2, 3), array(4, 5), array(6));
 [1,2,3,4,5,6]
```

>[!NOTE]
>
>`concat` La logique  pour les tableaux est disponible depuis la version 2.4.0.

#### concat_ws

`concat_ws(sep, [str | array(str)]+)` : renvoie la concaténation des chaînes séparées par `sep`.

Exemple :

```
> SELECT concat_ws(' ', 'Spark', 'SQL');
  Spark SQL
```

#### count

`count(*)` : renvoie le nombre total de lignes récupérées, y compris les lignes contenant des valeurs nulles.

`count(expr[, expr...])` : renvoie le nombre de lignes pour lesquelles les expressions fournies sont toutes non nulles.

`count(DISTINCT expr[, expr...])` : renvoie le nombre de lignes pour lesquelles les expressions fournies sont uniques et non nulles.

#### crc32

`crc32(expr)` : renvoie une valeur de vérification de redondance cyclique de la `expr` sous la forme de bigint.

Exemple :

```
> SELECT crc32('Spark');
 1557323817
```

#### decode

`decode(bin, charset)` : décode le premier argument à l’aide du deuxième jeu de caractères d’argument.

Exemple :

```
> SELECT decode(encode('abc', 'utf-8'), 'utf-8');
 abc
```

#### elt

`elt(n, input1, input2, ...)` : renvoie la `n`ème entrée, par exemple `input2` si `n` est égal à 2.

Exemple :

```
> SELECT elt(1, 'scala', 'java');
 scala
```

#### encode

`encode(str, charset)` : encode le premier argument à l’aide du deuxième jeu de caractères d’argument.

Exemple :

```
> SELECT encode('abc', 'utf-8');
 abc
```

#### first

`first(expr[, isIgnoreNull])` : renvoie la première valeur de `expr` pour un groupe de lignes. Si la valeur de `isIgnoreNull` est true, la fonction renvoie uniquement des valeurs non nulles.

#### first_value

`first_value(expr[, isIgnoreNull])` : renvoie la première valeur de `expr` pour un groupe de lignes. Si la valeur de `isIgnoreNull` est true, la fonction renvoie uniquement des valeurs non nulles.

#### get_json_object

`get_json_object(json_txt, path)` : extrait un objet json de `path`.

Exemple :

```
> SELECT get_json_object('{"a":"b"}', '$.a');
 b
```

#### grouping

<!-- was blank --->

#### grouping_id

<!-- was blank --->

#### instr

`instr(str, substr)` : renvoie l’index (de base 1) de la première occurrence de `substr` dans `str`.

Exemple :

```
> SELECT instr('SparkSQL', 'SQL');
 6
```

#### json_tuple

`json_tuple(jsonStr, p1, p2, ..., pn)` : renvoie un tuple comme la fonction `get_json_object`, avec plusieurs noms. Tous les paramètres d’entrée et les types de colonnes de sortie sont des chaînes.

Exemple :

```
> SELECT json_tuple('{"a":1, "b":2}', 'a', 'b');
 1  2
```

#### lag

`lag(input[, offset[, default]])` : renvoie la valeur de `input` à la `offset`ème ligne précédant la ligne actuelle dans la fenêtre. La valeur par défaut de `offset` est 1 et la valeur par défaut de `default` est nulle. Si la valeur de `input` à la `offset`ème ligne est nulle, la valeur null est renvoyée. S’il n’y a pas de ligne de décalage de ce type (par exemple, si le décalage est de 1, il n’y a aucune ligne précédant la première ligne de la fenêtre) et la fonction renvoie `default`.

#### last

`last(expr[, isIgnoreNull])` : renvoie la dernière valeur de `expr` pour un groupe de lignes. Si la valeur de `isIgnoreNull` est true, la fonction renvoie uniquement des valeurs non nulles.

#### last_value

`last_value(expr[, isIgnoreNull])` : renvoie la dernière valeur de `expr` pour un groupe de lignes. Si la valeur de `isIgnoreNull` est true, la fonction renvoie uniquement des valeurs non nulles.

#### lead

`lead(input[, offset[, default]])` : renvoie la valeur de `input` à la `offset`ème ligne située après la ligne actuelle dans la fenêtre. La valeur par défaut de `offset` est 1 et la valeur par défaut de `default` est nulle. Si la valeur de `input` à la `offset`ème ligne est nulle, la valeur null est renvoyée. S’il n’y a pas de ligne de décalage de ce type (par exemple, si le décalage est de 1, il n’y a aucune ligne suivant la dernière ligne de la fenêtre) et la fonction renvoie `default`.


#### left

`left(str, len)` : renvoie les caractères `len` (`len` peut être un type de chaîne) situés le plus à gauche de la chaîne `str`. Si `len` est inférieur ou égal à 0, le résultat est une chaîne vide.

Exemple :

> SELECT left(&#39;Spark SQL&#39;, 3);
Spa


#### length

`length(expr)` : renvoie la longueur en caractères des données de chaîne ou le nombre de bits de données binaires. La longueur des données de chaîne inclut les espaces à la fin. La longueur des données binaires inclut des zéros binaires.

Exemples :

```
> SELECT length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### locate

`locate(substr, str[, pos])` : renvoie la position de la première occurrence de `substr` dans `str` après la position `pos`. La valeur `pos` donnée et la valeur renvoyée sont de base 1.

Exemples :

```
> SELECT locate('bar', 'foobarbar');
 4
> SELECT locate('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### map_concat

`map_concat(map, ...)` : renvoie l’union de toutes les maps données.

Exemple :

```
> SELECT map_concat(map(1, 'a', 2, 'b'), map(2, 'c', 3, 'd'));
 {1:"a",2:"c",3:"d"}
```

Depuis : 2.4.0

#### map_keys

`map_keys(map)` : renvoie un tableau non ordonné contenant les clés de la map.

Exemple :

```
> SELECT map_keys(map(1, 'a', 2, 'b'));
 [1,2]
```

#### map_values

`map_values(map)` : renvoie un tableau non ordonné contenant les valeurs de la map.

Exemple :

```
> SELECT map_values(map(1, 'a', 2, 'b'));
 ["a","b"]
```

#### ntile

`ntile(n)` : divise les lignes de chaque partition de fenêtre en buckets `n` allant de 1 à un maximum de `n`.

#### nullif

`nullif(expr1, expr2)` : renvoie null si `expr1` est égal à `expr2`, ou `expr1` dans le cas contraire.

Exemple :

```
> SELECT nullif(2, 2);
 NULL
```

#### nvl

`nvl(expr1, expr2)` : renvoie `expr2` si `expr1` est nul ou `expr1` dans le cas contraire.

Exemple :

```
> SELECT nvl(NULL, array('2'));
 ["2"]
```

#### nvl2

`nvl2(expr1, expr2, expr3)` : renvoie `expr2` si `expr1` n’est pas nul, ou `expr3` dans le cas contraire.

Exemple :

```
> SELECT nvl2(NULL, 2, 1);
 1
```

#### parse_url

`parse_url(url, partToExtract[, key])` : extrait une partie d’une URL.

Exemples :

```
> SELECT parse_url('http://spark.apache.org/path?query=1', 'HOST')
 spark.apache.org
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY')
 query=1
> SELECT parse_url('http://spark.apache.org/path?query=1', 'QUERY', 'query')
 1
```

#### position

`position(substr, str[, pos])` : renvoie la position de la première occurrence de `substr` dans `str` après la position `pos`. La valeur `pos` donnée et la valeur renvoyée sont de base 1.

Exemples :

```
> SELECT position('bar', 'foobarbar');
 4
> SELECT position('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### rank

`rank()` : calcule le rang d’une valeur dans un groupe de valeurs. Le résultat est égal à 1 plus le nombre de lignes précédentes, ou égal à la ligne actuelle dans l’ordre de la partition. Les valeurs produisent des espaces dans la séquence.

#### regexp_extract

`regexp_extract(str, regexp[, idx])` : extrait un groupe correspondant à `regexp`.

Exemple :

```
> SELECT regexp_extract('100-200', '(\\d+)-(\\d+)', 1);
 100
```

#### regex_replace

`regexp_replace(str, regexp, rep)` : remplace toutes les sous-chaînes de `str` correspondant à `regexp` par `rep`.

Exemple :

```
> SELECT regexp_replace('100-200', '(\\d+)', 'num');
 num-num
```

#### repeat

`repeat(str, n)` : renvoie la chaîne qui répète la valeur de chaîne donnée n fois.

Exemple :

```
> SELECT repeat('123', 2);
 123123
```

#### replace

`replace(str, search[, replace])` : remplace toutes les occurrences de `search` par `replace`.

Arguments :
- `str` : une expression de chaîne
- `search` : une expression de chaîne. Si `search` est introuvable dans `str`, `str` est renvoyé inchangé.
- `replace` : une expression de chaîne. Si `replace` n’est pas spécifié ou est une chaîne vide, rien ne remplace la chaîne supprimée de `str`.

Exemple :

```
> SELECT replace('ABCabc', 'abc', 'DEF');
 ABCDEF
```

#### rollup

<!-- was blank -->

#### row_number

`row_number()` : attribue un numéro séquentiel unique à chaque ligne, en commençant par 1, selon l’ordre des lignes dans la partition de fenêtre.

#### schema_of_json

`schema_of_json(json[, options])` : renvoie le schéma de la chaîne JSON au format DDL.

Exemple :

```
> SELECT schema_of_json('[{"col":0}]');
 array<struct<col:int>>
```

Depuis : 2.4.0

#### sentences

`sentences(str[, lang, country])` : divise `str` en un tableau de mots.

Exemple :

```
> SELECT sentences('Hi there! Good morning.');
 [["Hi","there"],["Good","morning"]]
```

#### sequence

`sequence(start, stop, step)` : génère un tableau d’éléments du début à l’arrêt (inclus), avec une incrémentation par étape. Le type des éléments renvoyés est le même que le type des expressions d’argument.

Les types pris en charge sont les suivants : octet, court, entier, long, date, horodatage.

Les expressions `start` et `stop` doivent se résoudre par le même type. Si les expressions `start` et `stop` se résolvent par le type « date » ou « horodatage », alors l’expression `step` doit se résoudre par le type « intervalle » ; dans le cas contraire, elle se résout par le même type que les expressions `start` et `stop`.

Arguments :
- `start` : une expression. Le début de la plage.
- `stop` : une expression. La fin de la plage (incluse).
- `step` : une expression facultative. L’étape de la plage. Par défaut, `step` a une valeur de 1 si `start` est inférieur ou égal à `stop`, sinon il a une valeur de -1. Pour les séquences temporelles, les valeurs sont de 1 jour et de -1 jour, respectivement. Si `start` est supérieur à `stop`, `step` doit être négatif, et inversement.

Exemples :

```
> SELECT sequence(1, 5);
 [1,2,3,4,5]
> SELECT sequence(5, 1);
 [5,4,3,2,1]
> SELECT sequence(to_date('2018-01-01'), to_date('2018-03-01'), interval 1 month);
 [2018-01-01,2018-02-01,2018-03-01]
```

Depuis : 2.4.0

#### shiftleft

`shiftleft(base, expr)` : décalage à gauche au niveau du bit.

Exemple :

```
> SELECT shiftleft(2, 1);
 4
```

#### shiftright

`shiftright(base, expr)` : décalage à droite au niveau du bit (signé).

Exemple :

```
> SELECT shiftright(4, 1);
 2
```

#### shiftrightunsigned

`shiftrightunsigned(base, expr)` : décalage à droite au niveau du bit non signé.

Exemple :

```
> SELECT shiftrightunsigned(4, 1);
 2
```

#### size

`size(expr)` : renvoie la taille d’un tableau ou d’une carte. La fonction renvoie -1 si son entrée est nulle et si `spark.sql.legacy.sizeOfNull` est défini sur true. Si `spark.sql.legacy.sizeOfNull` est défini sur false, la fonction renvoie null pour une entrée nulle. Par défaut, le paramètre `spark.sql.legacy.sizeOfNull` est défini sur true.

Exemples :

```
> SELECT size(array('b', 'd', 'c', 'a'));
 4
> SELECT size(map('a', 1, 'b', 2));
 2
> SELECT size(NULL);
 -1
```

#### space

`space(n)` : renvoie une chaîne composée de `n` espaces.

Exemple :

```
> SELECT concat(space(2), '1');
   1
```

#### split

`split(str, regex)` : divise `str` autour d’occurrences correspondant à `regex`.

Exemple :

```
> SELECT split('oneAtwoBthreeC', '[ABC]');
 ["one","two","three",""]
```

#### substring_index

`substring_index(str, delim, count)` : renvoie la sous-chaîne de `str` avant les occurrences `count` du délimiteur `delim`. Si `count` est positif, tout ce qui se trouve à gauche du délimiteur final (en partant de la gauche) est renvoyé. Si `count` est négatif, tout ce qui se trouve à droite du délimiteur final (en partant de la droite) est renvoyé. La fonction `substring_index` effectue une correspondance sensible à la casse lors de la recherche de `delim`.

Exemple :

```
> SELECT substring_index('www.apache.org', '.', 2);
 www.apache
```

#### window

<!-- was blank -->

#### xpath

`xpath(xml, xpath)` : renvoie un tableau de chaînes de valeurs dans les nœuds du xml correspondant à l’expression XPath.

Exemple :

```
> SELECT xpath('<a><b>b1</b><b>b2</b><b>b3</b><c>c1</c><c>c2</c></a>','a/b/text()');
 ['b1','b2','b3']
```

#### xpath_double

`xpath_double(xml, xpath)` : renvoie une valeur double, zéro si aucune correspondance n’est trouvée ou NaN si une correspondance est trouvée, mais que la valeur est non numérique.

Exemple :

```
> SELECT xpath_double('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_float

`xpath_float(xml, xpath)` : renvoie une valeur en virgule flottante, zéro si aucune correspondance n’est trouvée ou NaN si une correspondance est trouvée, mais que la valeur est non numérique.

Exemple :

```
> SELECT xpath_float('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_int

`xpath_int(xml, xpath)` : renvoie une valeur entière, zéro si aucune correspondance n’est trouvée ou si une correspondance est trouvée, mais que la valeur est non numérique.

Exemple :

```
> SELECT xpath_int('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_long

`xpath_long(xml, xpath)` : renvoie une valeur entière longue, zéro si aucune correspondance n’est trouvée ou si une correspondance est trouvée, mais que la valeur est non numérique.

Exemple :

```
> SELECT xpath_long('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_number

`xpath_number(xml, xpath)` : renvoie une valeur double, zéro si aucune correspondance n’est trouvée ou NaN si une correspondance est trouvée, mais que la valeur est non numérique.

Exemple :

```
> SELECT xpath_number('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_short

`xpath_short(xml, xpath)` : renvoie une valeur entière courte, zéro si aucune correspondance n’est trouvée ou si une correspondance est trouvée, mais que la valeur est non numérique.

Exemple :

```
> SELECT xpath_short('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_string

`xpath_string(xml, xpath)` : renvoie le contenu textuel du premier nœud xml correspondant à l’expression XPath.

Exemple :

```
> SELECT xpath_string('<a><b>b</b><c>cc</c></a>','a/c');
 cc
```

### Informations actuelles

#### current_database

`current_database()` : renvoie la base de données actuelle.

Exemple :

```
> SELECT current_database();
 default
```

#### current_date

`current_date()` : renvoie la date actuelle au début de l’évaluation de requête.

Depuis : 1.5.0

#### current_timestamp

`current_timestamp()` : renvoie l’horodatage actuel au début de l’évaluation de requête.

Depuis : 1.5.0

#### now

`now()` : renvoie l’horodatage actuel au début de l’évaluation de requête.

Depuis : 1.5.0
