---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Spark SQL, fonctions
topic: spark sql functions
translation-type: tm+mt
source-git-commit: a23ee02a9e801531a38b5ff70ef07497aa21b174

---


# Spark SQL, fonctions

Les assistants SQL Spark fournissent des fonctions Spark SQL intégrées pour étendre les fonctionnalités SQL.

Référence : Documentation de la fonction [Spark SQL](https://spark.apache.org/docs/2.4.0/api/sql/index.html)

>[!NOTE] Certaines fonctions de la documentation externe ne sont pas prises en charge.

## Catégories

- [Opérateurs et fonctions mathématiques et statistiques](#math-and-statistical-operators-and-functions)
- [Opérateurs logiques](#logical-operators)
- [Fonctions Date/Heure](#date/time-functions)
- [, fonctions](#aggregate-functions)
- [Tableaux  ](#arrays)
- [Fonctions de diffusion du type de données](#datatype-casting-functions)
- [Fonctions de conversion et de formatage](#conversion-and-formatting-functions)
- [Évaluation des données](#data-evaluation)
- [Informations actuelles](#current-information)

### Opérateurs et fonctions mathématiques et statistiques

#### Modulo

`expr1 % expr2`: Renvoie le reste après `expr1`/`expr2`.

Exemples :

```
> SELECT 2 % 1.8;
 0.2
> SELECT MOD(2, 1.8);
 0.2
```

#### Multiplier

`expr1 * expr2`: Renvoie `expr1`*`expr2`.

Exemple :

```
> SELECT 2 * 3;
 6
```

#### Add (Ajouter)

`expr1 + expr2`: Renvoie `expr1`+`expr2`.

Exemple :

```
> SELECT 1 + 2;
 3
```

#### Soustraire

`expr1 - expr2`: Renvoie `expr1`-`expr2`.

Exemple :

```
> SELECT 2 - 1;
 1
```

#### Diviser

`expr1 / expr2`: Renvoie `expr1`/`expr2`. Il effectue toujours une division à virgule flottante.

Exemples :

```
> SELECT 3 / 2;
 1.5
> SELECT 2L / 2L;
 1.0
```

#### abs

`abs(expr)`: Renvoie la valeur absolue de la valeur numérique.

Exemple :

```
> SELECT abs(-1);
  1
```

#### acos

`acos(expr)`: Renvoie le cosinus inverse (également appelé arc cosinus) de `expr`, comme s’il était calculé par `java.lang.Math.acos`.

Exemples :

```
> SELECT acos(1);
 0.0
> SELECT acos(2);
 NaN
```

#### approx_percentile

`approx_percentile(col, percentage [, accuracy])`: Renvoie la valeur approximative du percentile d’une colonne numérique `col` au pourcentage donné. La valeur du pourcentage doit être comprise entre 0,0 et 1,0. Le `accuracy` paramètre (par défaut : 10000) est un littéral numérique positif qui contrôle la précision de l&#39;approximation au prix de la mémoire. Une valeur plus élevée de `accuracy` donne une meilleure précision, `1.0/accuracy` est l&#39;erreur relative de l&#39;approximation. Lorsqu’ `percentage` il s’agit d’un tableau, chaque valeur du tableau de pourcentage doit être comprise entre 0,0 et 1,0. Dans ce cas, le tableau du percentile approximatif de la colonne `col` au tableau du pourcentage donné est renvoyé.

Exemples :

```
> SELECT approx_percentile(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT approx_percentile(10.0, 0.5, 100);
 10.0
```

#### asin

`asin(expr)`: Renvoie le sinus inverse (également appelé arc sinus), l’arc sinus de `expr`, comme s’il était calculé par `java.lang.Math.asin`.

Exemples :

```
> SELECT asin(0);
 0.0
> SELECT asin(2);
 NaN
```

#### atan

`atan(expr)`: Renvoie la tangente inverse (également appelée tangente arc) de `expr`, comme si elle était calculée par `java.lang.Math.atan`

Exemple :

```
> SELECT atan(0);
 0.0
```

#### atan2

`atan2(exprY, exprX)`: Renvoie l’angle en radians entre l’axe X positif d’un plan et le point donné par les coordonnées (`exprX`, `exprY`), comme si calculé par `java.lang.Math.atan2`.

Arguments :

`exprY`: Coordonnée sur l’axe`exprX`y : Coordonnée sur l&#39;axe X

Exemple :

```
> SELECT atan2(0, 0);
 0.0
```

#### avg

`avg(expr)`: Renvoie la moyenne calculée à partir des valeurs d’un groupe.

#### cardinalité

`cardinality(expr)`: Renvoie la taille d’un tableau ou d’un mappage. La fonction renvoie -1 si son entrée est nulle et `spark.sql.legacy.sizeOfNull` définie sur true (valeur par défaut). Si `spark.sql.legacy.sizeOfNull` est défini sur false, la fonction renvoie null pour une entrée nulle.

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

`cbrt(expr)`: Renvoie la racine  du de `expr`.

Exemple :

```
> Select cbrt(27.0);
 3.0
```

#### ceil

`ceil(expr)`: Renvoie le plus petit entier non plus petit que `expr`.

Exemples :

```
> SELECT ceil(-0.1);
 0
> SELECT ceil(5);
 5
```

#### plafond

`ceiling(expr)`: Renvoie le plus petit entier non plus petit que `expr`.

Exemples :

```
> SELECT ceiling(-0.1);
 0
> SELECT ceiling(5);
 5
```

#### conv

`conv(num, from_base, to_base)`: Convertir `num` de `from_base` en `to_base`

Exemples :

```
> SELECT conv('100', 2, 10);
 4
> SELECT conv(-10, 16, -10);
 -16
```

#### corr

`corr(expr1, expr2)`: Renvoie le coefficient Pearson de corrélation entre un ensemble de paires de nombres.

#### cos

`cos(expr)`: Renvoie le cosinus de `expr`, comme si calculé par `java.lang.Math.cos`.

Exemple :

```
> SELECT cos(0);
 1.0
```

#### cosh

`cosh(expr)`: Renvoie le cosinus hyperbolique de `expr`, comme s’il était calculé par `java.lang.Math.cosh`.

Arguments :
- `expr`: Angle hyperbolique

Exemple :

```
> SELECT cosh(0);
 1.0
```

#### cot

`cot(expr)`: Renvoie la cotangente de `expr`, comme si elle était calculée par `1/java.lang.Math.cot`.

Arguments :
- `expr`: Angle en radians

Exemple :

```
> SELECT cot(1);
 0.6420926159343306
```

#### dense_grade

`dense_rank()`: Calcule le rang d’une valeur dans un groupe de valeurs. Le résultat est un plus la valeur de rang précédemment attribuée. Contrairement à la fonction `rank`, `dense_rank` ne produit pas d’espaces dans la séquence de classement.

#### e

`e()`: Renvoie le nombre d’Euler, e.

Exemple :

```
> SELECT e();
 2.718281828459045
```

#### exp

`exp(expr)`: Renvoie e à la puissance de `expr`.

Exemple :

```
> SELECT exp(0);
 1.0
```

#### expml

`expm1(expr)`: Renvoie exp(`expr`) - 1.

Exemple :

```
> SELECT expm1(0);
 0.0
```

#### factoriel

`factorial(expr)`: Renvoie la factorielle de `expr`. `expr` est [0,20]. Sinon, null.

Exemple :

```
> SELECT factorial(5);
 120
```

#### étage

`floor(expr)`: Renvoie l’entier le plus grand n’est pas supérieur à `expr`.

Exemples :

```
> SELECT floor(-0.1);
 -1
> SELECT floor(5);
 5
```

#### plus grand

`greatest(expr, ...)`: Renvoie la valeur la plus élevée de tous les paramètres, en ignorant les valeurs nulles.

Exemple :

```
> SELECT greatest(10, 9, 2, 4, 3);
 10
```

#### hypothétique

`hypot(expr1, expr2)`: Renvoie sqrt(`expr1`<sup>2</sup> + `expr2`<sup>2</sup>).

Exemple :

```
> SELECT hypot(3, 4);
 5.0
```

#### kurtosis

`kurtosis(expr)`: Renvoie la valeur de kurtosis calculée à partir des valeurs d’un groupe.


#### less

`least(expr, ...)`: Renvoie la valeur minimale de tous les paramètres, en ignorant les valeurs nulles.

Exemple :

```
> SELECT least(10, 9, 2, 4, 3);
 2
```

#### levenshtein

`levenshtein(str1, str2)`: Renvoie la distance Levenshtein entre les deux chaînes données.

Exemples :

```
> SELECT levenshtein('kitten', 'sitting');
 3
```

#### ln

`ln(expr)`: Renvoie le logarithme naturel (base e) de `expr`.

Exemple :

```
> SELECT ln(1);
 0.0
```

#### journal

`log(base, expr)`: Renvoie le logarithme de `expr` par `base`.

Exemple :

```
> SELECT log(10, 100);
 2.0
```

#### log10

`log10(expr)`: Renvoie le logarithme de `expr` avec la base 10.

Exemple :

```
> SELECT log10(10);
 1.0
```

#### log1p

`log1p(expr)`: Retours `log(1 + expr)`.

Exemple :

```
> SELECT log1p(0);
 0.0
```

#### log2

`log2(expr)`: Renvoie le logarithme de `expr` avec base 2.

Exemple :

```
> SELECT log2(2);
 1.0
```

#### max

`max(expr)`: Renvoie la valeur maximale de `expr`.

#### moyenne

`mean(expr)`: Renvoie la moyenne calculée à partir des valeurs d’un groupe.

#### min

`min(expr)`: Renvoie la valeur minimale de `expr`.

#### monotonics_adding_id

`monotonically_increasing_id()`: Renvoie des entiers 64 bits qui augmentent de manière monotone. L’ID généré est garanti qu’il augmente de manière monotone et qu’il est unique, mais pas consécutif. L’implémentation actuelle place l’ID de partition dans les 31 bits supérieurs et les 33 bits inférieurs représentent le numéro d’enregistrement dans chaque partition. L&#39;hypothèse est que le bloc de données a moins d&#39;un milliard de partitions, et que chaque partition a moins de 8 milliards d&#39;enregistrements. La fonction n’est pas déterministe, car son résultat dépend des ID de partition.

#### négatif

`negative(expr)`: Renvoie la valeur de négation de `expr`.

Exemple :

```
> SELECT negative(1);
 -1
```

#### percent_grade

`percent_rank()`: Calcule le classement en pourcentage d’une valeur dans un groupe de valeurs.

#### percentile

`percentile(col, percentage [, frequency])`: Renvoie la valeur du percentile exact de la colonne numérique `col` au pourcentage donné. La valeur de `percentage` doit être comprise entre 0.0 et 1.0. La valeur de `frequency` doit être intégrale positive.

`percentile(col, array(percentage1 [, percentage2]...) [, frequency])`: Renvoie le tableau de valeurs exactes du centile de la colonne numérique `col` aux pourcentages donnés. Chaque valeur du tableau de pourcentage doit être comprise entre 0,0 et 1,0. La valeur de `frequency` doit être intégrale positive.

#### percentile_approx

`percentile_approx(col, percentage [, accuracy])`: Renvoie la valeur approximative du percentile d’une colonne numérique `col` au pourcentage donné. La valeur de `percentage` doit être comprise entre 0.0 et 1.0. Le `accuracy` paramètre (par défaut : 10000) est un littéral numérique positif qui contrôle la précision de l&#39;approximation au prix de la mémoire. Une valeur plus élevée de `accuracy` donne une meilleure précision, `1.0/accuracy` est l&#39;erreur relative de l&#39;approximation. Lorsqu’ `percentage` il s’agit d’un tableau, chaque valeur du tableau de pourcentage doit être comprise entre 0,0 et 1,0. Dans ce cas, renvoie le tableau du percentile approximatif de la colonne `col` au tableau du pourcentage donné.

Exemples :

```
> SELECT percentile_approx(10.0, array(0.5, 0.4, 0.1), 100);
 [10.0,10.0,10.0]
> SELECT percentile_approx(10.0, 0.5, 100);
 10.0
```

#### pi

`pi()`: Renvoie pi.

Exemple :

```
> SELECT pi();
 3.141592653589793
```

#### pmod

`pmod(expr1, expr2)`: Renvoie la valeur positive de `expr1` mod `expr2`.

Exemples :

```
> SELECT pmod(10, 3);
 1
> SELECT pmod(-10, 3);
 2
```

#### positif

`positive(expr)`: Renvoie la valeur positive de `expr`

#### pow

`pow(expr1, expr2)`: Soulève `expr1` le pouvoir de `expr2`.

Exemple :

```
> SELECT pow(2, 3);
 8.0
```

#### puissance

`power(expr1, expr2)`: Soulève `expr1` le pouvoir de `expr2`.

Exemples :

```
> SELECT power(2, 3);
 8.0
```

#### radians

`radians(expr)`: Convertit les degrés en radians.

Arguments :

- `expr`: Angle en degrés

Exemple :

```
> SELECT radians(180);
 3.141592653589793
```

#### rand

`rand([seed])`: Renvoie une valeur aléatoire avec des valeurs distribuées de manière uniforme et indépendante (i.i.d.) dans (0, 1).

Exemples :

```
> SELECT rand();
 0.9629742951434543
> SELECT rand(0);
 0.8446490682263027
> SELECT rand(null);
 0.8446490682263027
```

>[!NOTE] Cette fonction est généralement non déterministe.

#### randn

`randn([seed])`: Renvoie une valeur aléatoire avec des valeurs indépendantes et distribuées de manière identique (i.i.d.) provenant de la distribution normale standard.

Exemples :

```
> SELECT randn();
 -0.3254147983080288
> SELECT randn(0);
 1.1164209726833079
> SELECT randn(null);
 1.1164209726833079
```

>[!NOTE] Cette fonction est généralement non déterministe.

#### rint

`rint(expr)`: Renvoie la valeur de  de la plus proche en valeur de l’argument et égale à un entier mathématique.

Exemples :

```
> SELECT rint(12.3456);
 12.0
```

#### round

`round(expr, d)`: Renvoie `expr` arrondi aux `d` décimales à l’aide du mode arrondi HALF_UP.

Exemple :

```
> SELECT round(2.5, 0);
 3.0
```

#### signer

`sign(expr)`: Renvoie -1.0, 0.0 ou 1.0 comme `expr` est négatif, 0 ou positif.

Exemple :

```
> SELECT sign(40);
 1.0
```

#### signe

`signum(expr)`: Renvoie -1.0, 0.0 ou 1.0 comme `expr` est négatif, 0 ou positif.

Exemple :

```
> SELECT signum(40);
 1.0
```

#### sin

`sin(expr)`: Renvoie le sinus de `expr`, comme si calculé par `java.lang.Math.sin`.

Arguments :

- `expr`: Angle en radians

Exemple :

```
> SELECT sin(0);
 0.0
```

#### sinh

`sinh(expr)`: Renvoie le sinus hyperbolique de `expr`, comme si calculé par `java.lang.Math.sinh`.

Arguments :

- `expr`: Angle hyperbolique

Exemple :

```
> SELECT sinh(0);
 0.0
```

#### sqrt

`sqrt(expr)`: Renvoie la racine carrée de `expr`.

Exemple :

```
> SELECT sqrt(4);
 2.0
```

#### stddev

`stddev(expr)`: Renvoie l’écart type calculé à partir des valeurs d’un groupe.

#### stddev_pop

`sttdev_pop(expr)`: Renvoie l’écart type de population calculé à partir des valeurs d’un groupe.

#### stddev_samp

`stddev_samp(expr)`: Renvoie l’écart type calculé à partir des valeurs d’un groupe.

#### sum

`sum(expr)`: Renvoie la somme calculée à partir des valeurs d’un groupe.

#### tan

`tan(expr)`: Renvoie la tangente de `expr`, comme si elle était calculée par `java.lang.Math.tan`.

Arguments :

- `expr`: Angle en radians

Exemple :

```
> SELECT tan(0);
 0.0
```

#### tanh

`tanh(expr)`: Renvoie la tangente hyperbolique de `expr`, comme si elle était calculée par `java.lang.Math.tanh`.

Arguments :

- `expr`: Angle hyperbolique

Exemple :

```
> SELECT tanh(0);
 0.0
```

#### Var_pop

`var_pop(expr)`: Renvoie la variance de population calculée à partir des valeurs d’un groupe.

#### Var_samp

`var_samp(expr)`: Renvoie la variance d’échantillon calculée à partir des valeurs d’un groupe.

#### variance

`variance(expr)`: Renvoie la variance d’échantillon calculée à partir des valeurs d’un groupe.

### Opérateurs logiques

#### Logique non

`! expr`: Logique non.

#### Inférieur à

`expr1 < expr2`: Renvoie true si `expr1` est inférieur à `expr2`.

Arguments :

- `expr1, expr2`: Les deux   doivent être du même type ou peuvent être fondus sur un type commun et doivent être un type pouvant être ordonné. Par exemple, le type de mappage n’est pas modifiable. Il n’est donc pas pris en charge. Pour les types complexes tels que array/struct, les types de données des champs doivent pouvoir être classés.

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

#### Inférieur ou égal à

`expr1 <= expr2`: Renvoie true si `expr1` est inférieur ou égal à `expr2`.

Arguments :

- `expr1, expr2`: Les deux   doivent être du même type ou peuvent être fondus sur un type commun et doivent être d’un type pouvant être ordonné. Par exemple, le type de mappage n’est pas modifiable. Il n’est donc pas pris en charge. Pour les types complexes tels que tableau/structure, les types de données des champs doivent pouvoir être classés.

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

#### Egal à

`expr1 = expr2`: Renvoie true si `expr1` est égal `expr2`, ou false dans le cas contraire.

Arguments :

- `expr1, expr2`: Les deux   doivent être du même type ou peuvent être fondus sur un type commun et doivent être un type pouvant être utilisé dans la comparaison de l’égalité. Le type de mappage n’est pas pris en charge. Pour les types complexes tels que array/struct, les types de données des champs doivent pouvoir être classés.

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

#### Supérieur à

`expr1 > expr2`: Renvoie true si `expr1` est supérieur à `expr2`.

Arguments :

- `expr1, expr2`: Les deux   doivent être du même type ou peuvent être fondus sur un type commun et doivent être un type pouvant être ordonné. Par exemple, le type de mappage n’est pas modifiable. Il n’est donc pas pris en charge. Pour les types complexes tels que array/struct, les types de données des champs doivent pouvoir être classés.

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

#### Supérieur ou égal à

`expr1 >= expr2`: Renvoie true si `expr1` est supérieur ou égal à `expr2`.

Arguments :

- `expr1, expr2`: Les deux   doivent être du même type ou peuvent être fondus sur un type commun et doivent être un type pouvant être ordonné. Par exemple, le type de mappage n’est pas modifiable. Il n’est donc pas pris en charge. Pour les types complexes tels que array/struct, les types de données des champs doivent pouvoir être classés.

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

#### Exclusif ou exclusif au niveau du bit

`expr1 ^ expr2`: Renvoie le résultat de l’opérateur OU exclusif au niveau du bit de `expr1` et `expr2`.

Exemple :

```
> SELECT 3 ^ 5;
 2
```

#### et

`expr1 and expr2`: Logique ET.

#### array_overlings

`arrays_overlap(a1, a2)`: Renvoie true si a1 contient au moins un élément non nul présent également dans a2. Si les tableaux n’ont aucun élément commun et qu’ils sont tous deux non vides et que l’un d’eux contient un élément nul, la valeur null est renvoyée. Sinon, false est renvoyé.

Exemple :

```
> SELECT arrays_overlap(array(1, 2, 3), array(3, 4, 5));
 true
```

Depuis : 2.4.0

#### assert_true

`assert_true(expr)`: Lance une exception si `expr` ce n’est pas vrai.

Exemple :

```
> SELECT assert_true(0 < 1);
 NULL
```

#### if

`if(expr1, expr2, expr3)`: Si `expr1` est évalué sur true, renvoie `expr2`; renvoie sinon `expr3`.

Exemple :

```
> SELECT if(1 < 2, 'a', 'b');
 a
```

#### ifnull

`ifnull(expr1, expr2)`: Renvoie `expr2` si `expr1` est nul ou `expr1` non.

Exemple :

```
> SELECT ifnull(NULL, array('2'));
 ["2"]
```

#### in

`expr1 in(expr2, expr3, ...)`: Renvoie true si `expr` est égal à valN.

Arguments :
- `expr1, expr2, expr3, ...`: Les arguments doivent être du même type.

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

`isnan(expr)`: Renvoie true si `expr` est NaN ou false dans le cas contraire.

Exemple :

```
> SELECT isnan(cast('NaN' as double));
 true
```

#### isnotnull

`isnotnull(expr)`: Renvoie true si `expr` n’est pas nul, ou false dans le cas contraire.

Exemples :

```
> SELECT isnotnull(1);
 true
```

#### isnull

`isnull(expr)`: Renvoie true si `expr` est nul ou false dans le cas contraire.

Exemple :

```
> SELECT isnull(1);
 false
```

#### nanvl

`nanvl(expr1, expr2)`: Renvoie `expr1` s’il ne s’agit pas de NaN, ou `expr2` autrement.

Exemple :

```
> SELECT nanvl(cast('NaN' as double), 123);
 123.0
```

#### not

`not expr`: Logique non.

#### ou

`expr1 or expr2`: Logique ou.

#### xpath_boolean

`xpath_boolean(xml, xpath)`: Renvoie true si le  XPath  est évalué sur true ou si un noeud correspondant est trouvé.

Exemple :

```
> SELECT xpath_boolean('<a><b>1</b></a>','a/b');
 true
```

### Fonctions Date/Heure

#### add_month

`add_months(start_date, num_months)`: Renvoie la date `num_months` postérieure `start_date`.

Exemple :

```
> SELECT add_months('2016-08-31', 1);
 2016-09-30
```

Depuis : 1.5.0

#### date_add

`date_add(start_date, num_days)`: Renvoie la date `num_days` postérieure `start_date`.

Exemple :

```
> SELECT date_add('2016-07-30', 1);
 2016-07-31
```

Depuis : 1.5.0

#### date_format

`date_format(timestamp, fmt)`: Convertit `timestamp` en valeur de chaîne au format spécifié par le format de date `fmt`.

Exemple :

```
> SELECT date_format('2016-04-08', 'y');
 2016
```

Depuis : 1.5.0

#### date_sub

`date_sub(start_date, num_days)`: Renvoie la date antérieure `num_days` à `start_date`.

Exemple :

```
> SELECT date_sub('2016-07-30', 1);
 2016-07-29
```

Depuis : 1.5.0

#### date_trunc

`date_trunc(fmt, ts)`: Renvoie l’horodatage tronqué à l’unité spécifiée par le modèle de format `fmt`. `fmt` doit être l’une des valeurs suivantes : [&quot;ANNÉE&quot;, &quot;AAAA&quot;, &quot;AAAA&quot;, &quot;MON&quot;, &quot;MOIS&quot;, &quot;MM&quot;, &quot;JOUR&quot;, &quot;JOUR&quot;, &quot;HEURE&quot;, &quot;MINUTE&quot;, &quot;SECOND&quot;, &quot;SEMAINE&quot;, &quot;TRIMESTRE&quot;]

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

Depuis : 2.3.0

#### datediff

`datediff(endDate, startDate)`: Renvoie le nombre de jours compris entre `startDate` et `endDate`.

Exemples :

```
> SELECT datediff('2009-07-31', '2009-07-30');
 1

> SELECT datediff('2009-07-30', '2009-07-31');
 -1
```

Depuis : 1.5.0

#### day

`day(date)`: Renvoie le jour du mois de la date/de l’horodatage.

Exemple :

```
> SELECT day('2009-07-30');
 30
```

Depuis : 1.5.0

#### day of month

`dayofmonth(date)`: Renvoie le jour du mois de la date/de l’horodatage.

Exemple :

```
> SELECT dayofmonth('2009-07-30');
 30
```

Depuis : 1.5.0

#### jour de la semaine

`dayofweek(date)`: Renvoie le jour de la semaine pour la date/l’horodatage (1 = dimanche, 2 = lundi, ..., 7 = samedi).

Exemple :

```
> SELECT dayofweek('2009-07-30');
 5
```

Depuis : 2.3.0

#### jour de l&#39;année

`dayofyear(date)`: Renvoie le jour de l’année de la date/de l’horodatage.

Exemple :

```
> SELECT dayofyear('2016-04-09');
 100
```

Depuis : 1.5.0

#### from_unixtime

`from_unixtime(unix_time, format)`: Renvoie `unix_time` dans le champ spécifié `format`.

Exemple :

```
> SELECT from_unixtime(0, 'yyyy-MM-dd HH:mm:ss');
 1970-01-01 00:00:00
```

Depuis : 1.5.0

#### from_utc_timestamp

`from_utc_timestamp(timestamp, timezone)`: Interprète un horodatage du type &quot;2017-07-14 02:40:00.0&quot; comme une heure en UTC, et effectue le rendu de cette heure comme un horodatage dans le fuseau horaire donné. Par exemple, &#39;GMT+1&#39; renverrait &#39;2017-07-14 03:40:00.0&#39;.

Exemple :

```
> SELECT from_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-31 09:00:00
```

Depuis : 1.5.0

#### heure

`hour(timestamp)`: Renvoie le composant d’heure de la chaîne/de l’horodatage.

Exemple :

```
> SELECT hour('2009-07-30 12:58:59');
 12
```

Depuis : 1.5.0

#### last_day

`last_day(date):` Renvoie le dernier jour du mois auquel la date appartient.

Exemple :

```
> SELECT last_day('2009-01-12');
 2009-01-31
```

Depuis : 1.5.0

#### minute

`minute(timestamp)`: Renvoie le composant Minute de la chaîne/horodatage.

Exemple :

```
> SELECT minute('2009-07-30 12:58:59');
 58
```

Depuis : 1.5.0

#### month

`month(date)` Renvoie le composant month de la date/de l’horodatage.

Exemple :

```
> SELECT month('2016-07-30');
 7
```

Depuis : 1.5.0

#### month_between

`months_between(timestamp1, timestamp2[, roundOff])`: Si `timestamp1` est postérieure à `timestamp2`, le résultat est positif. Si `timestamp1` et `timestamp2` sont le même jour du mois, ou les deux sont le dernier jour du mois, l’heure du jour est ignorée. Dans le cas contraire, la différence est calculée sur la base de 31 jours par mois et arrondie à 8 chiffres, sauf `roundOff=false`.

Exemples :

```
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30');
 3.94959677
> SELECT months_between('1997-02-28 10:30:00', '1996-10-30', false);
 3.9495967741935485
```

Depuis : 1.5.0

#### next_day

`next_day(start_date, day_of_week)`: Renvoie la première date postérieure à `start_date` et nommée comme indiqué.

Exemple :

```
> SELECT next_day('2015-01-14', 'TU');
 2015-01-20
```

Depuis : 1.5.0

#### trimestre

`quarter(date)`: Renvoie le trimestre de l’année pour la date, dans la plage 1 à 4.

Exemple :

```
> SELECT quarter('2016-08-31');
 3
```

Depuis : 1.5.0

#### second

`second(timestamp)`: Renvoie le deuxième composant de la chaîne/horodatage.

Exemple :

```
> SELECT second('2009-07-30 12:58:59');
 59
```

Depuis : 1.5.0

#### to_date

`to_date(date_str[, fmt])`: Analyse le    avec le `date_str` `fmt` de la  à une date. Renvoie la valeur null avec une entrée non valide. Par défaut, elle suit les règles d’attribution à une date si la valeur `fmt` est omise.

Exemples :

```
> SELECT to_date('2009-07-30 04:17:52');
 2009-07-30
> SELECT to_date('2016-12-31', 'yyyy-MM-dd');
 2016-12-31
```

Depuis : 1.5.0

#### to_timestamp

`to_timestamp(timestamp[, fmt])`: Analyse le  de  avec le `timestamp` de l’ `fmt` en horodatage. Renvoie la valeur null avec une entrée non valide. Par défaut, les règles d’attribution sont associées à un horodatage si la valeur `fmt` est omise.

Exemples :

```
> SELECT to_timestamp('2016-12-31 00:12:00');
 2016-12-31 00:12:00
> SELECT to_timestamp('2016-12-31', 'yyyy-MM-dd');
 2016-12-31 00:00:00
```

Depuis : 2.2.0

#### to_unix_timestamp

`to_unix_timestamp(expr[, pattern])`: Renvoie l’horodatage UNIX de l’heure donnée.

Exemple :

```
> SELECT to_unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Depuis : 1.6.0

#### to_utc_timestamp

`to_utc_timestamp(timestamp, timezone)`: Interprète un horodatage du type &quot;2017-07-14 02:40:00.0&quot; comme une heure dans le fuseau horaire donné, et effectue le rendu de cette heure comme un horodatage en UTC. Par exemple, &quot;GMT+1&quot; renverrait &quot;2017-07-14 01:40:00.0&quot;.

Exemple :

```
> SELECT to_utc_timestamp('2016-08-31', 'Asia/Seoul');
 2016-08-30 15:00:00
```

Depuis : 1.5.0

#### trunc

`trunc(date, fmt)`: Renvoie la date avec la partie horaire du jour tronquée à l’unité spécifiée par le modèle de format `fmt`. `fmt` est l’un des [&quot;an&quot;, &quot;aaaa&quot;, &quot;yy&quot;, &quot;mon&quot;, &quot;mois&quot;, &quot;mm&quot;]

Exemples :

```
> SELECT trunc('2009-02-12', 'MM');
 2009-02-01
> SELECT trunc('2015-10-27', 'YEAR');
 2015-01-01
```

Depuis : 1.5.0

#### unix_timestamp

`unix_timestamp([expr[, pattern]])`: Renvoie l’horodatage UNIX de l’heure actuelle ou spécifiée.

Exemples :

```
> SELECT unix_timestamp();
 1476884637
> SELECT unix_timestamp('2016-04-08', 'yyyy-MM-dd');
 1460041200
```

Depuis : 1.5.0

#### jour ouvrable

`weekday(date)`: Renvoie le jour de la semaine pour la date/l’horodatage (0 = lundi, 1 = mardi, ..., 6 = dimanche).

Exemple :

```
> SELECT weekday('2009-07-30');
 3
```

Depuis : 2.4.0

#### week_of_year

`weekofyear(date)`: Renvoie la semaine de l’année de la date donnée. Une semaine est considérée comme le lundi et la semaine 1 est la première semaine avec plus de 3 jours.

Exemple :

```
> SELECT weekofyear('2008-02-20');
 8
```

Depuis : 1.5.0

#### when

`CASE WHEN expr1 THEN expr2 [WHEN expr3 THEN expr4]* [ELSE expr5] END`: Lorsque `expr1` = true, renvoie `expr2`; else lorsque `expr3` = true, renvoie `expr4`; else renvoie `expr5`.

Arguments :

- `expr1`, `expr3`: La condition de branche   doit toutes être de type booléen.
- `expr2`, `expr4`, `expr5`: La valeur de la branche   et la valeur d&#39;inverse  doivent toutes être du même type ou être convertibles en un type commun.

Exemples :

```
> SELECT CASE WHEN 1 > 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 1
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 > 0 THEN 2.0 ELSE 1.2 END;
 2
> SELECT CASE WHEN 1 < 0 THEN 1 WHEN 2 < 0 THEN 2.0 END;
 NULL
```

#### année

`year(date)`: Renvoie le composant d’année de la date/de l’horodatage.

Exemple :

```
> SELECT year('2016-07-30');
 2016
```

Depuis : 1.5.0

### Aggregate fonctions

#### approx_count_distinct

`approx_count_distinct(expr[, relativeSD])`: Renvoie la cardinalité estimée par HyperLogLog++. `relativeSD` définit l’erreur d’estimation maximale autorisée.

### Tableaux  

#### tableau

`array(expr, ...)`: Renvoie un tableau avec les éléments donnés.

Exemple :

```
> SELECT array(1, 2, 3);
 [1,2,3]
```

#### array_contains

`array_contains(array, value)`: Renvoie true si le tableau contient la valeur.

Exemple :

```
> SELECT array_contains(array(1, 2, 3), 2);
 true
```

#### array_distinct

`array_distinct(array)`: Supprime les valeurs  du tableau.

Exemple :

```
> SELECT array_distinct(array(1, 2, 3, null, 3));
 [1,2,3,null]
```

Depuis : 2.4.0

#### array_excepté

`array_except(array1, array2)`: Renvoie un tableau des éléments dans `array1` mais pas dans `array2`, sans .

Exemple :

```
> SELECT array_except(array(1, 2, 3), array(1, 3, 5));
 [2]
```

Depuis : 2.4.0

#### array_intersect

`array_intersect(array1, array2)`: Renvoie un tableau des éléments situés à l’intersection de `array1` et `array2`, sans.

Exemple :

```
> SELECT array_intersect(array(1, 2, 3), array(1, 3, 5));
 [1,3]
```

Depuis : 2.4.0

#### array_join

`array_join(array, delimiter[, nullReplacement])`: Concatène les éléments du tableau donné à l’aide du délimiteur et d’une chaîne facultative pour remplacer les valeurs nulles. Si aucune valeur n’est définie pour `nullReplacement`, toute valeur nulle est filtrée.

Exemples :

```
> SELECT array_join(array('hello', 'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ');
 hello world
> SELECT array_join(array('hello', null ,'world'), ' ', ',');
 hello , world
```

Depuis : 2.4.0

#### array_max

`array_max(array)`: Renvoie la valeur maximale dans le tableau. Les éléments nuls sont ignorés.

Exemple :

```
> SELECT array_max(array(1, 20, null, 3));
 20
```

Depuis : 2.4.0

#### array_min

`array_min(array)`: Renvoie la valeur minimale dans le tableau. Les éléments nuls sont ignorés.

Exemple :

```
> SELECT array_min(array(1, 20, null, 3));
 1
```

Depuis : 2.4.0

#### array_position

`array_position(array, element)`: Renvoie l’index (de base 1) du premier élément du tableau aussi long.

Exemple :

```
> SELECT array_position(array(3, 2, 1), 1);
 3
```

Depuis : 2.4.0

#### array_remove

`array_remove(array, element)`: Supprimez tous les éléments égaux à l’élément du tableau.

Exemple :

```
> SELECT array_remove(array(1, 2, 3, null, 3), 3);
 [1,2,null]
```

Depuis : 2.4.0

#### array_repeat

`array_repeat(element, count)`: Renvoie le tableau contenant les heures de nombre d’éléments.

Exemple :

```
> SELECT array_repeat('123', 2);
 ["123","123"]
```

Depuis : 2.4.0

#### array_sort

`array_sort(array)`: Trie le tableau d’entrée par ordre croissant. Les éléments du tableau d’entrée doivent pouvoir être classés. Les éléments nuls sont placés à la fin du tableau renvoyé.

Exemple :

```
> SELECT array_sort(array('b', 'd', null, 'c', 'a'));
 ["a","b","c","d",null]
```

Depuis : 2.4.0

#### array_

`array_union(array1, array2)`: Renvoie un tableau des éléments dans le   de `array1` et `array2`, sans.

Exemple :

```
> SELECT array_union(array(1, 2, 3), array(1, 3, 5));
 [1,2,3,5]
```

Depuis : 2.4.0

#### array_zip

`arrays_zip(a1, a2, ...)`: Renvoie un tableau fusionné de structs dans lequel le N-th struct contient toutes les valeurs N-th des tableaux d’entrée.

Exemples :

```
> SELECT arrays_zip(array(1, 2, 3), array(2, 3, 4));
 [{"0":1,"1":2},{"0":2,"1":3},{"0":3,"1":4}]
> SELECT arrays_zip(array(1, 2), array(2, 3), array(3, 4));
 [{"0":1,"1":2,"2":3},{"0":2,"1":3,"2":4}]
```

Depuis : 2.4.0

#### element_at

`element_at(array, index)`: Renvoie l’élément du tableau à l’index donné (de base 1). Si `index < 0`, accède aux éléments de la dernière à la première. Renvoie NULL si l’index dépasse la longueur du tableau.

`element_at(map, key)`: Renvoie la valeur d’une clé donnée ou NULL si la clé n’est pas contenue dans le mappage.

Exemples :

```
> SELECT element_at(array(1, 2, 3), 2);
 2
> SELECT element_at(map(1, 'a', 2, 'b'), 2);
 b
```

Depuis : 2.4.0

#### exploser

`explode(expr)`: Sépare les éléments du tableau `expr` en plusieurs lignes ou les éléments du mappage `expr` en plusieurs lignes et colonnes.

Exemples :

```
> SELECT explode(array(10, 20));
 10
 20
```

#### explode_outer

`explode_outer(expr)`: Sépare les éléments du tableau `expr` en plusieurs lignes ou les éléments du mappage `expr` en plusieurs lignes et colonnes.

Exemple :

```
> SELECT explode_outer(array(10, 20));
 10
 20
```

#### find_in_set

`find_in_set(str, str_array)`: Renvoie l’index (de base 1) de la chaîne donnée (`str`) dans le délimité par des virgules (`str_array`). Renvoie 0 si la chaîne est introuvable ou si la chaîne donnée (`str`) contient une virgule.

Exemple :

```
> SELECT find_in_set('ab','abc,b,ab,c,def');
 3
```

#### aplatir

`flatten(arrayOfArrays)`: Transforme un tableau en tableau unique.

Exemple :

```
> SELECT flatten(array(array(1, 2), array(3, 4)));
 [1,2,3,4]
```

Depuis : 2.4.0

#### inline

`inline(expr)`: Explose un tableau de structures.

Exemple :

```
> SELECT inline(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### inline_outer

`inline_outer(expr)`: Explose un tableau de structures.

Exemple :

```
> SELECT inline_outer(array(struct(1, 'a'), struct(2, 'b')));
 1  a
 2  b
```

#### posexplosé

`posexplode(expr)`: Sépare les éléments du tableau `expr` en plusieurs lignes avec des positions ou les éléments du mappage `expr` en plusieurs lignes et colonnes avec des positions.

Exemple :

```
> SELECT posexplode(array(10,20));
 0  10
 1  20
```

#### posexplode_outer

`posexplode_outer(expr)`: Sépare les éléments du tableau `expr` en plusieurs lignes avec des positions ou les éléments du mappage `expr` en plusieurs lignes et colonnes avec des positions.

Exemple :

```
> SELECT posexplode_outer(array(10,20));
 0  10
 1  20
```

#### inverser

`reverse(array)`: Renvoie une chaîne inversée ou un tableau avec l’ordre inverse des éléments.

Exemples :

```
> SELECT reverse('Spark SQL');
 LQS krapS
> SELECT reverse(array(2, 1, 4, 3));
 [3,4,1,2]
```

Depuis : 1.5.0
>[!NOTE] La logique rse pour les tableaux est disponible depuis la version 2.4.0.

#### mélanger

`shuffle(array)`: Renvoie une permutation aléatoire du tableau donné.

Exemples :

```
> SELECT shuffle(array(1, 20, 3, 5));
 [3,1,5,20]
> SELECT shuffle(array(1, 20, null, 3));
 [20,null,3,1]
```

Depuis : 2.4.0
>[!NOTE] n’est pas déterministe.

#### tranche

`slice(x, start, length)`: Sous-définit le tableau x en commençant à partir du  d’index (ou en commençant à partir de la fin si le  est négatif) avec la longueur spécifiée.

Exemples :

```
> SELECT slice(array(1, 2, 3, 4), 2, 2);
 [2,3]
> SELECT slice(array(1, 2, 3, 4), -2, 2);
 [3,4]
```

Depuis : 2.4.0

#### sort_array

`sort_array(array[, ascendingOrder])`: Trie le tableau d’entrée par ordre croissant ou décroissant selon l’ordre naturel des éléments du tableau. Les éléments nuls sont placés au début du tableau renvoyé dans l’ordre croissant ou à la fin du tableau renvoyé dans l’ordre décroissant.

Exemples :

```
> SELECT sort_array(array('b', 'd', null, 'c', 'a'), true);
 [null,"a","b","c","d"]
```

#### zip_with

`zip_with(left, right, func)`: Fusionne les deux tableaux donnés, au niveau de l’élément, dans un tableau unique à l’aide de la fonction. Si un tableau est plus court, les valeurs nulles sont ajoutées à la fin pour correspondre à la longueur du tableau plus long, avant d’appliquer la fonction.

Exemples :

```
> SELECT zip_with(array(1, 2, 3), array('a', 'b', 'c'), (x, y) -> (y, x));
 [{"y":"a","x":1},{"y":"b","x":2},{"y":"c","x":3}]
> SELECT zip_with(array(1, 2), array(3, 4), (x, y) -> x + y);
 [4,6]
> SELECT zip_with(array('a', 'b', 'c'), array('d', 'e', 'f'), (x, y) -> concat(x, y));
 ["ad","be","cf"]
```

Depuis : 2.4.0

### Fonctions de diffusion du type de données

#### bigent

`bigint(expr)`: Place la valeur `expr` au type de données  du `bigint`.

#### binaire

`binary(expr)`: Place la valeur `expr` au type de données  du `binary`.

#### booléen

`boolean(expr)`: Place la valeur `expr` au type de données  du `boolean`.

#### cast

`cast(expr AS type)`: Place la valeur `expr` au type de données  du `type`.

Exemple :

```
> SELECT cast('10' as int);
 10
```

#### date

`date(expr)`: Place la valeur `expr` au type de données  du `date`.

#### décimal

`decimal(expr)`: Place la valeur `expr` au type de données  du `decimal`.

#### double

`double(expr)`: Place la valeur `expr` au type de données  du `double`.

#### float

`float(expr)`: Place la valeur `expr` au type de données  du `float`.

#### int

`int(expr)`: Place la valeur `expr` au type de données  du `int`.

#### map

`map(key0, value0, key1, value1, ...)`: Crée un mappage avec les paires clé/valeur données.

Exemple :

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### petite

`smallint(expr)`: Place la valeur `expr` au type de données  du `smallint`.

#### str_to_map

`str_to_map(text[, pairDelim[, keyValueDelim]])`: Crée un mappage après avoir divisé le texte en paires clé/valeur à l’aide de délimiteurs. Les délimiteurs par défaut sont &#39;,&#39; pour `pairDelim` et &#39;:&#39; pour `keyValueDelim`.

Exemples :

```
> SELECT str_to_map('a:1,b:2,c:3', ',', ':');
 map("a":"1","b":"2","c":"3")
> SELECT str_to_map('a');
 map("a":null)
```

#### chaîne

`string(expr)`: Place la valeur `expr` au type de données  du `string`.

#### struct

`struct(col1, col2, col3, ...)`: Crée un struct avec les valeurs de champ données.

#### tinyint

`tinyint(expr)`: Place la valeur `expr` au type de données  du `tinyint`.

### Fonctions de conversion et de formatage

#### ascii

`ascii(str)`: Renvoie la valeur numérique du premier caractère de `str`.

Exemples :

```
> SELECT ascii('222');
 50
> SELECT ascii(2);
 50
```

#### base64

`base64(bin)`: Convertit l’argument d’un binaire `bin` en chaîne de base 64.

Exemple :

```
> SELECT base64('Spark SQL');
 U3BhcmsgU1FM
```

#### bin

`bin(expr)`: Renvoie la représentation sous forme de chaîne de la valeur longue `expr` représentée en binaire.

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

`bit_length(expr)`: Renvoie la longueur en bits des données de chaîne ou le nombre de bits de données binaires.

Exemple :

```
> SELECT bit_length('Spark SQL');
 72
```

#### char

`char(expr)`: Renvoie le caractère ASCII dont le binaire est équivalent à `expr`. Si n est supérieur à 256, le résultat est équivalent à `chr(n % 256)`.

Exemple :

```
> SELECT char(65);
 A
```

#### char_length

`char_length(expr)`: Renvoie la longueur en caractères des données de chaîne ou le nombre d’octets des données binaires. La longueur des données de chaîne inclut les espaces de fin. La longueur des données binaires inclut des zéros binaires.

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

`character_length(expr)`: Renvoie la longueur en caractères des données de chaîne ou le nombre d’octets des données binaires. La longueur des données de chaîne inclut les espaces de fin. La longueur des données binaires inclut des zéros binaires.

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

`chr(expr)`: Renvoie le caractère ASCII dont le binaire est équivalent à expr. Si n est supérieur à 256, le résultat est équivalent à `chr(n % 256)`

Exemple :

```
> SELECT chr(65);
 A
```

#### degrés

`degrees(expr)`: Convertit les radians en degrés.

Arguments :
- `expr`: Angle en radians

Exemple :

```
> SELECT degrees(3.141592653589793);
 180.0
```

#### format_number

`format_number(expr1, expr2)`: Formate le nombre `expr1` comme &quot;#,###,###.##&#39;, arrondi aux `expr2` décimales. Si `expr2` la valeur est 0, le résultat n’a pas de point décimal ou de partie fractionnaire. `expr2` accepte également un format spécifié par l’utilisateur. Ceci est destiné à fonctionner comme MySQL `FORMAT`.

Exemples :

```
> SELECT format_number(12332.123456, 4);
 12,332.1235
> SELECT format_number(12332.123456, '##################.###');
 12332.123
```

#### from_json

`from_json(jsonStr, schema[, options])`: Renvoie une valeur struct avec les valeurs données `jsonStr` et `schema`.

Exemples :

```
> SELECT from_json('{"a":1, "b":0.8}', 'a INT, b DOUBLE');
 {"a":1, "b":0.8}
> SELECT from_json('{"time":"26/08/2015"}', 'time Timestamp', map('timestampFormat', 'dd/MM/yyyy'));
 {"time":"2015-08-26 00:00:00.0"}
```

Depuis : 2.2.0

#### hash

`hash(expr1, expr2, ...)`: Renvoie une valeur de hachage des arguments.

Exemple :

```
> SELECT hash('Spark', array(123), 2);
 -1321691492
```

#### hex

`hex(expr)`: Convertit `expr` en hexadécimal.

Exemples :

```
> SELECT hex(17);
 11
> SELECT hex('Spark SQL');
 537061726B2053514C
```

#### initcap

`initcap(str)`: Renvoie `str` la première lettre de chaque mot en majuscules. Toutes les autres lettres sont en minuscules. Les mots sont délimités par des espaces blancs.

Exemple :

```
> SELECT initcap('sPark sql');
 Spark Sql
```

#### minuscule

`lcase(str)`: Renvoie `str` avec tous les caractères changés en minuscules.

Exemple :

```
> SELECT lcase('SparkSql');
 sparksql
```

#### lower

`lower(str)`: Renvoie `str` avec tous les caractères changés en minuscules.

Exemple :

```
> SELECT lower('SparkSql');
 sparksql
```

#### lpad

`lpad(str, len, pad)`: Renvoie `str`, avec le remplissage à gauche `pad` sur une longueur de `len`. Si `str` est plus long que `len`, la valeur renvoyée est raccourcie en `len` caractères.

Exemples :

```
> SELECT lpad('hi', 5, '??');
 ???hi
> SELECT lpad('hi', 1, '??');
 h
```

#### map

`map(key0, value0, key1, value1, ...)`: Crée un mappage avec les paires clé/valeur données.

Exemple :

```
> SELECT map(1.0, '2', 3.0, '4');
 {1.0:"2",3.0:"4"}
```

#### map_from_array

`map_from_arrays(keys, values)`: Crée un mappage avec une paire des tableaux clé/valeur donnés. Les éléments des clés ne peuvent pas être nuls.

Exemple :

```
> SELECT map_from_arrays(array(1.0, 3.0), array('2', '4'));
 {1.0:"2",3.0:"4"}
```

Depuis : 2.4.0

#### map_from_entry

`map_from_entries(arrayOfEntries)`: Renvoie un mappage créé à partir du tableau d’entrées donné.

Exemple :

```
> SELECT map_from_entries(array(struct(1, 'a'), struct(2, 'b')));
 {1:"a",2:"b"}
```

Depuis : 2.4.0

#### md5

`md5(expr)`: Renvoie une somme de contrôle MD5 128 bits sous la forme d’une chaîne hexadécimale de `expr`.

Exemple :

```
> SELECT md5('Spark');
 8cde774d6f7333752ed72cacddb05126
```

#### rpad

`rpad(str, len, pad)`: Renvoie `str`, avec le remplissage à droite `pad` d’une longueur de `len`. Si `str` est plus long que `len`, la valeur renvoyée est raccourcie en `len` caractères.

Exemples :

```
> SELECT rpad('hi', 5, '??');
 hi???
> SELECT rpad('hi', 1, '??');
 h
```

#### rtrim

`rtrim(str)`: Supprime les caractères d’espace de fin `str`.

`rtrim(trimStr, str)`: Supprime de la chaîne de fin, qui contient les caractères de la chaîne de rognage du `str`.

Arguments :
- `str`: Chaîne  
- `trimStr`: Caractères de chaîne de rognage à rogner. La valeur par défaut est un espace unique.

Exemples :

```
> SELECT rtrim('    SparkSQL   ');
 SparkSQL
> SELECT rtrim('LQSa', 'SSparkSQLS');
 SSpark
```

#### sha

`sha(expr)`: Renvoie une valeur de `sha1` hachage sous la forme d’une chaîne hexadécimale du `expr`.

Exemple :

```
> SELECT sha('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha1

`sha1(expr)`: Renvoie une valeur de `sha1` hachage sous la forme d’une chaîne hexadécimale du `expr`.

Exemple :

```
> SELECT sha1('Spark');
 85f5955f4b27a9a4c2aab6ffe5d7189fc298b92c
```

#### sha2

`sha2(expr, bitLength)`: Renvoie une somme de contrôle de la famille SHA-2 sous la forme d’une chaîne hexadécimale de `expr`. Les formats SHA-224, SHA-256, SHA-384 et SHA-512 sont pris en charge. La longueur du bit de 0 équivaut à 256.

Exemple :

```
> SELECT sha2('Spark', 256);
 529bc3b07127ecb7e53a4dcf1991d9152c24537d919178022b2c42657f79a26b
```

#### soundex

`soundex(str)`: Renvoie le code Soundex de la chaîne.

Exemple :

```
> SELECT soundex('Miller');
 M460
```

#### empiler

`stack(n, expr1, ..., exprk)`: Sépare `expr1`, ..., `exprk` en `n` lignes.

Exemple :

```
> SELECT stack(2, 1, 2, 3);
 1  2
 3  NULL
```

#### substr

`substr(str, pos[, len])`: Renvoie la sous-chaîne de `str` ce à `pos` et est de longueur `len`, ou la tranche du tableau d’octets qui à `pos` et est de longueur `len`.

Exemples :

```
> SELECT substr('Spark SQL', 5);
 k SQL
> SELECT substr('Spark SQL', -3);
 SQL
> SELECT substr('Spark SQL', 5, 1);
 k
```

#### sous-chaîne

`substring(str, pos[, len])`: Renvoie la sous-chaîne de `str` ce à `pos` et est de longueur `len`, ou la tranche du tableau d’octets qui à `pos` et est de longueur `len`.

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

`to_json(expr[, options])`: Renvoie une chaîne JSON avec une valeur struct donnée.

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

Depuis : 2.2.0

#### traduire

`translate(input, from, to)`: Traduit la `input` chaîne en remplaçant les caractères présents dans la `from` chaîne par les caractères correspondants dans la `to` chaîne.

Exemple :

```
> SELECT translate('AaBbCc', 'abc', '123');
 A1B2C3
```

#### trim

`trim(str)`: Supprime les caractères d’espace de début et de fin `str`.

`trim(BOTH trimStr FROM str)`: Supprimez les `trimStr` caractères de début et de fin de `str`.

`trim(LEADING trimStr FROM str)`: Supprimez les `trimStr` caractères de début de `str`.

`trim(TRAILING trimStr FROM str)`: Supprimez les `trimStr` caractères de fin de `str`.

Arguments :
- `str`: Chaîne  
- `trimStr`: Caractères de chaîne de rognage à rogner, la valeur par défaut étant un espace unique
- `BOTH`, `FROM`: Il s’agit de mots-clés pour spécifier des caractères de chaîne de rognage provenant des deux extrémités de la chaîne.
- `LEADING`, `FROM`: Il s’agit de mots-clés pour spécifier les caractères de chaîne de rognage à partir de la fin gauche de la chaîne.
- `TRAILING`, `FROM`: Il s’agit de mots-clés permettant de spécifier des caractères de chaîne à partir de la fin droite de la chaîne.

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

#### guérir

`ucase(str)`: Renvoie `str` avec tous les caractères en majuscules.

Exemple :

```
> SELECT ucase('SparkSql');
 SPARKSQL
```

#### unbase64

`unbase64(str)`: Convertit l’argument d’une chaîne de base 64 `str` en argument binaire.

Exemple :

```
> SELECT unbase64('U3BhcmsgU1FM');
 Spark SQL
```

#### unhex

`unhex(expr)`: Convertit le format hexadécimal `expr` en format binaire.

Exemple :

```
> SELECT decode(unhex('537061726B2053514C'), 'UTF-8');
 Spark SQL
```

#### upper

`upper(str)`: Renvoie `str` avec tous les caractères en majuscules.

Exemple :

```
> SELECT upper('SparkSql');
 SPARKSQL
```

#### uuid

`uuid()`: Renvoie une chaîne d’identifiant unique universel (UUID). La valeur est renvoyée sous la forme d’une chaîne de 36 caractères UUID canonique.

Exemple :

```
> SELECT uuid();
 46707d92-02f4-4817-8116-a4c3b23e6266
```

>[!NOTE] Fonction non déterministe.

### Évaluation des données

#### collier

`coalesce(expr1, expr2, ...)`: Renvoie le premier argument non nul s’il existe. Sinon, null.

Exemple :

```
> SELECT coalesce(NULL, 1, NULL);
 1
```

#### collection__

`collect_list(expr)`: Collecte et renvoie un  d’éléments non uniques.

#### collection_set

`collect_set(expr)`: Collecte et renvoie un ensemble d’éléments uniques.

#### concat

`concat(col1, col2, ..., colN)`: Renvoie la concaténation de col1, col2, ..., colN.

Exemples :

```
> SELECT concat('Spark', 'SQL');
 SparkSQL
> SELECT concat(array(1, 2, 3), array(4, 5), array(6));
 [1,2,3,4,5,6]
```

>[!NOTE] La logique `concat` des tableaux est disponible depuis la version 2.4.0.

#### concat_ws

`concat_ws(sep, [str | array(str)]+)`: Renvoie la concaténation des chaînes séparées par `sep`.

Exemple :

```
> SELECT concat_ws(' ', 'Spark', 'SQL');
  Spark SQL
```

#### count

`count(*)`: Renvoie le nombre total de lignes récupérées, y compris les lignes contenant la valeur null.

`count(expr[, expr...])`: Renvoie le nombre de lignes pour lesquelles les  de  fournis ne sont pas tous nuls.

`count(DISTINCT expr[, expr...])`: Renvoie le nombre de lignes pour lesquelles les  de  fournies sont uniques et non nulles.

#### crc32

`crc32(expr)`: Renvoie une valeur de contrôle de redondance cyclique de la `expr` valeur as a bigint.

Exemple :

```
> SELECT crc32('Spark');
 1557323817
```

#### décoder

`decode(bin, charset)`: Décode le premier argument à l’aide du deuxième jeu de caractères.

Exemple :

```
> SELECT decode(encode('abc', 'utf-8'), 'utf-8');
 abc
```

#### elt

`elt(n, input1, input2, ...)`: Renvoie la `n`-ème entrée, par exemple, `input2` lorsque `n` est 2.

Exemple :

```
> SELECT elt(1, 'scala', 'java');
 scala
```

#### encoder

`encode(str, charset)`: Code le premier argument à l’aide du deuxième jeu de caractères.

Exemple :

```
> SELECT encode('abc', 'utf-8');
 abc
```

#### first

`first(expr[, isIgnoreNull])`: Renvoie la première valeur de `expr` pour un groupe de lignes. Si `isIgnoreNull` est true, renvoie uniquement des valeurs non nulles.

#### first_value

`first_value(expr[, isIgnoreNull])`: Renvoie la première valeur de `expr` pour un groupe de lignes. Si `isIgnoreNull` est true, renvoie uniquement des valeurs non nulles.

#### get_json_object

`get_json_object(json_txt, path)`: Extrait un objet json de `path`.

Exemple :

```
> SELECT get_json_object('{"a":"b"}', '$.a');
 b
```

#### regroupement

<!-- was blank --->

#### group_id

<!-- was blank --->

#### entity

`instr(str, substr)`: Renvoie l’index (de base 1) de la première occurrence de `substr` in `str`.

Exemple :

```
> SELECT instr('SparkSQL', 'SQL');
 6
```

#### json_tuple

`json_tuple(jsonStr, p1, p2, ..., pn)`: Renvoie un tuple comme la fonction `get_json_object`, mais il prend plusieurs noms. Tous les paramètres d’entrée et les types de colonnes de sortie sont des chaînes.

Exemple :

```
> SELECT json_tuple('{"a":1, "b":2}', 'a', 'b');
 1  2
```

#### rapporter

`lag(input[, offset[, default]])`: Renvoie la valeur de `input` la `offset`ligne précédant la ligne active dans la fenêtre. La valeur par défaut de `offset` est 1 et la valeur par défaut de `default` est nulle. Si la valeur de `input` la `offset`ligne est nulle, la valeur null est renvoyée. S’il n’existe pas de ligne de décalage de ce type (par exemple, lorsque le décalage est de 1, la première ligne de la fenêtre ne comporte aucune ligne précédente), elle `default` est renvoyée.

#### last

`last(expr[, isIgnoreNull])`: Renvoie la dernière valeur de `expr` pour un groupe de lignes. Si `isIgnoreNull` est true, renvoie uniquement des valeurs non nulles.

#### last_value

`last_value(expr[, isIgnoreNull])`: Renvoie la dernière valeur de `expr` pour un groupe de lignes. Si `isIgnoreNull` est true, renvoie uniquement des valeurs non nulles.

#### plomb

`lead(input[, offset[, default]])`: Renvoie la valeur de `input` la `offset`ligne située après la ligne active dans la fenêtre. La valeur par défaut de `offset` est 1 et la valeur par défaut de `default` est nulle. Si la valeur de `input` la `offset`ligne est nulle, la valeur null est renvoyée. S’il n’existe pas de ligne de décalage de ce type (par exemple, lorsque le décalage est de 1, la dernière ligne de la fenêtre n’a aucune ligne suivante), elle `default` est renvoyée.


#### left

`left(str, len)`: Renvoie les caractères les plus à gauche `len` (`len` peuvent être de type chaîne) de la chaîne `str`. Si `len` est inférieur ou égal à 0, le résultat est une chaîne vide.

Exemple :

> SELECT left(&#39;Spark SQL&#39;, 3);
Spa


#### length

`length(expr)`: Renvoie la longueur en caractères des données de chaîne ou le nombre d’octets des données binaires. La longueur des données de chaîne inclut les espaces de fin. La longueur des données binaires inclut des zéros binaires.

Exemples :

```
> SELECT length('Spark SQL ');
 10
> SELECT CHAR_LENGTH('Spark SQL ');
 10
> SELECT CHARACTER_LENGTH('Spark SQL ');
 10
```

#### localiser

`locate(substr, str[, pos])`: Renvoie la position de la première occurrence de `substr` in `str` after position `pos`. La valeur donnée `pos` et la valeur renvoyée sont basées sur 1.

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

`map_concat(map, ...)`: Renvoie le   de toutes les cartes données.

Exemple :

```
> SELECT map_concat(map(1, 'a', 2, 'b'), map(2, 'c', 3, 'd'));
 {1:"a",2:"c",3:"d"}
```

Depuis : 2.4.0

#### map_keys

`map_keys(map)`: Renvoie un tableau non ordonné contenant les clés du mappage.

Exemple :

```
> SELECT map_keys(map(1, 'a', 2, 'b'));
 [1,2]
```

#### map_values

`map_values(map)`: Renvoie un tableau non ordonné contenant les valeurs du mappage.

Exemple :

```
> SELECT map_values(map(1, 'a', 2, 'b'));
 ["a","b"]
```

#### ntile

`ntile(n)`: Divise les lignes de chaque partition de fenêtre en `n` intervalles allant de 1 à au plus `n`.

#### nullif

`nullif(expr1, expr2)`: Renvoie null si `expr1` est égal à `expr2`, ou `expr1` autrement.

Exemple :

```
> SELECT nullif(2, 2);
 NULL
```

#### nvl

`nvl(expr1, expr2)`: Renvoie `expr2` si `expr1` est nul ou `expr1` non.

Exemple :

```
> SELECT nvl(NULL, array('2'));
 ["2"]
```

#### nvl2

`nvl2(expr1, expr2, expr3)`: Renvoie `expr2` si `expr1` n’est pas nul ou `expr3` autrement.

Exemple :

```
> SELECT nvl2(NULL, 2, 1);
 1
```

#### parse_url

`parse_url(url, partToExtract[, key])`: Extrait une partie d’une URL.

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

`position(substr, str[, pos])`: Renvoie la position de la première occurrence de `substr` in `str` after position `pos`. La valeur donnée `pos` et la valeur renvoyée sont basées sur 1.

Exemples :

```
> SELECT position('bar', 'foobarbar');
 4
> SELECT position('bar', 'foobarbar', 5);
 7
> SELECT POSITION('bar' IN 'foobarbar');
 4
```

#### grade

`rank()`: Calcule le rang d’une valeur dans un groupe de valeurs. Le résultat est un plus le nombre de lignes précédant ou égal à la ligne active dans l&#39;ordre de la partition. Les valeurs produisent des espaces dans la séquence.

#### regexp_extract

`regexp_extract(str, regexp[, idx])`: Extrait un groupe qui correspond `regexp`.

Exemple :

```
> SELECT regexp_extract('100-200', '(\\d+)-(\\d+)', 1);
 100
```

#### regex_replace

`regexp_replace(str, regexp, rep)`: Remplace toutes les sous-chaînes de `str` cette correspondance `regexp` par `rep`.

Exemple :

```
> SELECT regexp_replace('100-200', '(\\d+)', 'num');
 num-num
```

#### repeat

`repeat(str, n)`: Renvoie la chaîne qui répète la valeur de chaîne donnée n fois.

Exemple :

```
> SELECT repeat('123', 2);
 123123
```

#### replace

`replace(str, search[, replace])`: Remplace toutes les occurrences de `search` par `replace`.

Arguments :
- `str`: Chaîne  
- `search`: Chaîne  . Si `search` l’option n’est pas trouvée dans `str`, `str` est renvoyée sans modification.
- `replace`: Chaîne  . Si `replace` n’est pas spécifié ou s’il s’agit d’une chaîne vide, rien ne remplace la chaîne supprimée de `str`.

Exemple :

```
> SELECT replace('ABCabc', 'abc', 'DEF');
 ABCDEF
```

#### cumul

<!-- was blank -->

#### row_number

`row_number()`: Attribue un numéro séquentiel unique à chaque ligne, en commençant par une, selon l’ordre des lignes dans la partition de la fenêtre.

#### _de_json

`schema_of_json(json[, options])`: Renvoie des  au format DDL de la chaîne JSON.

Exemple :

```
> SELECT schema_of_json('[{"col":0}]');
 array<struct<col:int>>
```

Depuis : 2.4.0

#### phrases

`sentences(str[, lang, country])`: Se divise `str` en un tableau de mots.

Exemple :

```
> SELECT sentences('Hi there! Good morning.');
 [["Hi","there"],["Good","morning"]]
```

#### séquence

`sequence(start, stop, step)`: Génère un tableau d’éléments du  à l’arrêt (inclus), incrémenté par étape. Le type des éléments renvoyés est le même que le type d’argument  .

Les types pris en charge sont les suivants : octet, court, entier, long, date, horodatage.

Le  `start` `stop` et le  de doivent être résolus avec le même type. Si `start` et `stop`   sont résolus en &quot;date&quot; ou &quot;horodatage&quot;, le `step` doit se résoudre en &quot;intervalle&quot; ; dans le cas contraire, il est résolu de la même façon que le `start` `stop` et le de la .

Arguments :
- `start`: Un  .  de la plage.
- `stop`: Un  . Fin de la plage (incluse).
- `step`: Un  facultatif . Étape de la plage. Par défaut, `step` la valeur est 1 si `start` est inférieure ou égale à `stop`, sinon -1. Pour les séquences temporelles, c&#39;est respectivement 1 jour et -1 jour. Si `start` est supérieur à `stop`, le `step` paramètre doit être négatif, et inversement.

Exemples :

```
> SELECT sequence(1, 5);
 [1,2,3,4,5]
> SELECT sequence(5, 1);
 [5,4,3,2,1]
> SELECT sequence(to_date('2018-01-01'), to_date('2018-03-01'), interval 1 month);
 [2018-01-01,2018-02-01,2018-03-01]
```

Depuis : 2.4.0

#### décaler vers la gauche

`shiftleft(base, expr)`: Décalage gauche au niveau du bit.

Exemple :

```
> SELECT shiftleft(2, 1);
 4
```

#### gouverne

`shiftright(base, expr)`: Décalage droit au niveau du bit (signé).

Exemple :

```
> SELECT shiftright(4, 1);
 2
```

#### décaltrighttunsigned

`shiftrightunsigned(base, expr)`: Décalage droit non signé au niveau du bit.

Exemple :

```
> SELECT shiftrightunsigned(4, 1);
 2
```

#### taille

`size(expr)`: Renvoie la taille d’un tableau ou d’un mappage. La fonction renvoie -1 si son entrée est nulle et `spark.sql.legacy.sizeOfNull` définie sur true. Si `spark.sql.legacy.sizeOfNull` est défini sur false, la fonction renvoie null pour une entrée nulle. Par défaut, le `spark.sql.legacy.sizeOfNull` paramètre est défini sur true.

Exemples :

```
> SELECT size(array('b', 'd', 'c', 'a'));
 4
> SELECT size(map('a', 1, 'b', 2));
 2
> SELECT size(NULL);
 -1
```

#### espace

`space(n)`: Renvoie une chaîne composée d’ `n` espaces.

Exemple :

```
> SELECT concat(space(2), '1');
   1
```

#### fractionner

`split(str, regex)`: Divise `str` les occurrences qui correspondent `regex`.

Exemple :

```
> SELECT split('oneAtwoBthreeC', '[ABC]');
 ["one","two","three",""]
```

#### Sous-chaîne_index

`substring_index(str, delim, count)`: Renvoie la sous-chaîne `str` avant `count` les occurrences du délimiteur `delim`. Si `count` est positif, tout ce qui se trouve à gauche du délimiteur final (comptage à partir de la gauche) est renvoyé. Si `count` est négatif, tout à droite du délimiteur final (en comptant à droite) est renvoyé. La fonction `substring_index` effectue une correspondance sensible à la casse lors de la recherche `delim`.

Exemple :

```
> SELECT substring_index('www.apache.org', '.', 2);
 www.apache
```

#### fenêtre

<!-- was blank -->

#### xpath

`xpath(xml, xpath)`: Renvoie un tableau de chaînes de valeurs dans les noeuds du xml qui correspondent au  XPath .

Exemple :

```
> SELECT xpath('<a><b>b1</b><b>b2</b><b>b3</b><c>c1</c><c>c2</c></a>','a/b/text()');
 ['b1','b2','b3']
```

#### xpath_

`xpath_double(xml, xpath)`: Renvoie une valeur de , la valeur zéro si aucune correspondance n’est trouvée ou NaN si une correspondance est trouvée mais que la valeur est non numérique.

Exemple :

```
> SELECT xpath_double('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_float

`xpath_float(xml, xpath)`: Renvoie une valeur en virgule flottante, la valeur zéro si aucune correspondance n’est trouvée ou NaN si une correspondance est trouvée mais que la valeur est non numérique.

Exemple :

```
> SELECT xpath_float('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_int

`xpath_int(xml, xpath)`: Renvoie une valeur entière, ou la valeur zéro si aucune correspondance n’est trouvée, ou une correspondance est trouvée, mais la valeur est non numérique.

Exemple :

```
> SELECT xpath_int('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_long

`xpath_long(xml, xpath)`: Renvoie une valeur entière longue, ou la valeur zéro si aucune correspondance n’est trouvée, ou une correspondance est trouvée, mais la valeur est non numérique.

Exemple :

```
> SELECT xpath_long('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_number

`xpath_number(xml, xpath)`: Renvoie une valeur de , la valeur zéro si aucune correspondance n’est trouvée ou NaN si une correspondance est trouvée mais que la valeur est non numérique.

Exemple :

```
> SELECT xpath_number('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3.0
```

#### xpath_short

`xpath_short(xml, xpath)`: Renvoie une valeur entière courte, ou la valeur zéro si aucune correspondance n’est trouvée, ou une correspondance est trouvée, mais la valeur est non numérique.

Exemple :

```
> SELECT xpath_short('<a><b>1</b><b>2</b></a>', 'sum(a/b)');
 3
```

#### xpath_string

`xpath_string(xml, xpath)`: Renvoie le contenu textuel du premier noeud xml correspondant au  XPath .

Exemple :

```
> SELECT xpath_string('<a><b>b</b><c>cc</c></a>','a/c');
 cc
```

### Informations actuelles

#### current_database

`current_database()`: Renvoie la base de données active.

Exemple :

```
> SELECT current_database();
 default
```

#### current_date

`current_date()`: Renvoie la date actuelle au  de l’évaluation .

Depuis : 1.5.0

#### current_timestamp

`current_timestamp()`: Renvoie l’horodatage actuel à l’ de l’évaluation .

Depuis : 1.5.0

#### now

`now()`: Renvoie l’horodatage actuel à l’ de l’évaluation .

Depuis : 1.5.0
