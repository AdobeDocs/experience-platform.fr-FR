---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;spark sql;Spark sql;spark;fonctions spark sql;fonctions
solution: Experience Platform
title: Fonctions Spark SQL dans Query Service
topic-legacy: spark sql functions
description: Cette documentation contient des informations sur les fonctions Spark SQL qui étendent les fonctionnalités de SQL.
exl-id: 59e6d82b-3317-456d-8c56-3efd5978433a
source-git-commit: f291c0db5b751227e979e70ea8f91a0c133ecf34
workflow-type: tm+mt
source-wordcount: '3866'
ht-degree: 1%

---

# [!DNL Spark] Fonctions SQL

Adobe Experience Platform Query Service fournit plusieurs fonctions Spark SQL intégrées pour étendre les fonctionnalités SQL. Ce document répertorie les fonctions Spark SQL prises en charge par Query Service.

Pour plus d’informations sur les fonctions, notamment leur syntaxe, leur utilisation et des exemples, veuillez lire la section [Documentation sur les fonctions Spark SQL](https://spark.apache.org/docs/latest/api/sql/index.html).

>[!NOTE]
>
>Certaines fonctions de la documentation externe ne sont pas prises en charge.

## Fonctions et opérateurs mathématiques et statistiques {#math}

| Opérateur/fonction | Description |
| ----------------- | ----------- |
| [`%`](https://spark.apache.org/docs/latest/api/sql/index.html#_3) | Renvoie le reste des deux nombres |
| [`*`](https://spark.apache.org/docs/latest/api/sql/index.html#_5) | Multiplie les deux nombres |
| [`+`](https://spark.apache.org/docs/latest/api/sql/index.html#_6) | Ajoute les deux nombres |
| [`-`](https://spark.apache.org/docs/latest/api/sql/index.html#_7) | Enlève les deux nombres |
| [`/`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Divise les deux nombres |
| [`abs`](https://spark.apache.org/docs/latest/api/sql/index.html#abs) | Renvoie la valeur absolue de l’entrée |
| [`acos`](https://spark.apache.org/docs/latest/api/sql/index.html#acos) | Renvoie la valeur cosinale inverse |
| [`approx_count_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_count_distinct) | Renvoie la cardinalité estimée par HyperLogLog++ |
| [`approx_percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#approx_percentile) | Renvoie la valeur approximative du centile au pourcentage donné |
| [`asin`](https://spark.apache.org/docs/latest/api/sql/index.html#asin) | Renvoie la valeur inversée du sinus |
| [`atan`](https://spark.apache.org/docs/latest/api/sql/index.html#atan) | Renvoie la valeur de tangente inverse |
| [`atan2`](https://spark.apache.org/docs/latest/api/sql/index.html#atan2) | Renvoie l&#39;angle entre le plan de l&#39;axe X positif et les points donnés par les coordonnées |
| [`avg`](https://spark.apache.org/docs/latest/api/sql/index.html#avg) | Renvoie la valeur moyenne |
| [`cbrt`](https://spark.apache.org/docs/latest/api/sql/index.html#cbrt) | Renvoie la racine cubique |
| [`ceil`](https://spark.apache.org/docs/latest/api/sql/index.html#ceil) ou [`ceiling`](https://spark.apache.org/docs/latest/api/sql/index.html#ceiling) | Renvoie le plus petit entier non supérieur à la valeur saisie |
| [`conv`](https://spark.apache.org/docs/latest/api/sql/index.html#conv) | Convertir d’une base en une autre |
| [`corr`](https://spark.apache.org/docs/latest/api/sql/index.html#corr) | Renvoie le coefficient de Pearson entre les nombres |
| [`cos`](https://spark.apache.org/docs/latest/api/sql/index.html#cos) | Renvoie la valeur cosine |
| [`cosh`](https://spark.apache.org/docs/latest/api/sql/index.html#cosh) | Renvoie la valeur du cosinus hyperbolique |
| [`cot`](https://spark.apache.org/docs/latest/api/sql/index.html#cot) | Renvoie la valeur de la cotangente |
| [`dense_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#dense_rank) | Renvoie le rang d&#39;une valeur dans un groupe de valeurs |
| [`e`](https://spark.apache.org/docs/latest/api/sql/index.html#e) | Renvoie le nombre d’Euler |
| [`exp`](https://spark.apache.org/docs/latest/api/sql/index.html#exp) | Renvoie e à la puissance de la valeur |
| [`expm1`](https://spark.apache.org/docs/latest/api/sql/index.html#expm1) | Renvoie e à la puissance de la valeur moins 1 |
| [`factorial`](https://spark.apache.org/docs/latest/api/sql/index.html#factorial) | Renvoie la factorielle de la valeur |
| [`floor`](https://spark.apache.org/docs/latest/api/sql/index.html#floor) | Renvoie le plus grand entier non inférieur à la valeur |
| [`greatest`](https://spark.apache.org/docs/latest/api/sql/index.html#greatest) | Renvoie la valeur la plus grande de tous les paramètres |
| [`hypot`](https://spark.apache.org/docs/latest/api/sql/index.html#hypot) | Renvoie l&#39;hypothèse de l&#39;utilisation des deux valeurs données |
| [`kurtosis`](https://spark.apache.org/docs/latest/api/sql/index.html#kurtosis) | Renvoie la valeur de kurtosis du groupe |
| [`least`](https://spark.apache.org/docs/latest/api/sql/index.html#least) | Renvoie la plus petite valeur de tous les paramètres |
| [`ln`](https://spark.apache.org/docs/latest/api/sql/index.html#ln) | Renvoie le logarithme népérien de la valeur |
| [`log`](https://spark.apache.org/docs/latest/api/sql/index.html#log) | Renvoie le logarithme de la valeur |
| [`log10`](https://spark.apache.org/docs/latest/api/sql/index.html#log10) | Renvoie le logarithme, en base 10, de la valeur |
| [`log1p`](https://spark.apache.org/docs/latest/api/sql/index.html#log1p) | Renvoie le logarithme de la valeur plus 1 |
| [`log2`](https://spark.apache.org/docs/latest/api/sql/index.html#log2) | Renvoie le logarithme, en base 2, de la valeur |
| [`max`](https://spark.apache.org/docs/latest/api/sql/index.html#max) | Renvoie la valeur maximale de l&#39;expression |
| [`mean`](https://spark.apache.org/docs/latest/api/sql/index.html#mean) | Renvoie la moyenne calculée à partir des valeurs |
| [`min`](https://spark.apache.org/docs/latest/api/sql/index.html#min) | Renvoie la valeur minimale de l’expression |
| [`monotonically_increasing_id`](https://spark.apache.org/docs/latest/api/sql/index.html#monotonically_increasing_id) | Renvoie des identifiants à augmentation monotone |
| [`negative`](https://spark.apache.org/docs/latest/api/sql/index.html#negative) | Renvoie la valeur négative |
| [`percent_rank`](https://spark.apache.org/docs/latest/api/sql/index.html#percent_rank) | Renvoie le classement en pourcentage d&#39;une valeur |
| [`percentile`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile) | Renvoie le centile exact à un pourcentage donné |
| [`percentile_approx`](https://spark.apache.org/docs/latest/api/sql/index.html#percentile_approx) | Renvoie le centile approximatif à un pourcentage donné |
| [`pi`](https://spark.apache.org/docs/latest/api/sql/index.html#pi) | Renvoie pi |
| [`pmod`](https://spark.apache.org/docs/latest/api/sql/index.html#pmod) | Renvoie le modulo positif entre deux valeurs |
| [`positive`](https://spark.apache.org/docs/latest/api/sql/index.html#positive) | Renvoie la valeur positive |
| [`pow`](https://spark.apache.org/docs/latest/api/sql/index.html#pow), [`power`](https://spark.apache.org/docs/latest/api/sql/index.html#power) | Renvoie la première valeur à la puissance de la seconde valeur |
| [`radians`](https://spark.apache.org/docs/latest/api/sql/index.html#radians) | Convertit la valeur en radians |
| [`rand`](https://spark.apache.org/docs/latest/api/sql/index.html#rand) | Renvoie un nombre aléatoire compris entre 0 et 1 |
| [`randn`](https://spark.apache.org/docs/latest/api/sql/index.html#randn) | Renvoie une valeur aléatoire |
| [`rint`](https://spark.apache.org/docs/latest/api/sql/index.html#rint) | Renvoie la valeur double la plus proche |
| [`round`](https://spark.apache.org/docs/latest/api/sql/index.html#round) | Renvoie la valeur arrondie la plus proche |
| [`sign`](https://spark.apache.org/docs/latest/api/sql/index.html#sign), [`signum`](https://spark.apache.org/docs/latest/api/sql/index.html#signum) | Renvoie le signe du nombre |
| [`sin`](https://spark.apache.org/docs/latest/api/sql/index.html#sin) | Renvoie le sinus de la valeur |
| [`sinh`](https://spark.apache.org/docs/latest/api/sql/index.html#sinh) | Renvoie le sinus hyperbolique de la valeur |
| [`sqrt`](https://spark.apache.org/docs/latest/api/sql/index.html#sqrt) | Renvoie la racine carrée de la valeur |
| [`stddev`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev) | Renvoie l&#39;écart type de la valeur |
| [`sttdev_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#sttdev_pop) | Renvoie l&#39;écart type de population de la valeur |
| [`stddev_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#stddev_samp) | Renvoie l&#39;écart type échantillon de la valeur |
| [`sum`](https://spark.apache.org/docs/latest/api/sql/index.html#sum) | Renvoie la somme des valeurs |
| [`tan`](https://spark.apache.org/docs/latest/api/sql/index.html#tan) | Renvoie la tangente de la valeur |
| [`tanh`](https://spark.apache.org/docs/latest/api/sql/index.html#tanh) | Renvoie la tangente hyperbolique de la valeur |
| [`var_pop`](https://spark.apache.org/docs/latest/api/sql/index.html#var_pop) | Renvoie la variance de population calculée |
| [`var_samp`](https://spark.apache.org/docs/latest/api/sql/index.html#var_samp), [`variance`](https://spark.apache.org/docs/latest/api/sql/index.html#variance) | Renvoie la variance d’échantillon calculée |

### Opérateurs logiques et fonctions {#logical-operators}

| Opérateur/fonction | Description |
| ----------------- | ----------- |
| [`!`](https://spark.apache.org/docs/latest/api/sql/index.html#_1) ou [`not`](https://spark.apache.org/docs/latest/api/sql/index.html#not) | Logical not |
| [`<`](https://spark.apache.org/docs/latest/api/sql/index.html#_8) | Inférieur à |
| [`<=`](https://spark.apache.org/docs/latest/api/sql/index.html#_9) | Inférieur ou égal à |
| [`=`](https://spark.apache.org/docs/latest/api/sql/index.html#_12) | Equal to |
| [`>`](https://spark.apache.org/docs/latest/api/sql/index.html#_14) | Greater than |
| [`>=`](https://spark.apache.org/docs/latest/api/sql/index.html#_15) | Supérieur ou égal à |
| [`^`](https://spark.apache.org/docs/latest/api/sql/index.html#_16) | Bitwise exclusive or |
| [`\|`](https://spark.apache.org/docs/latest/api/sql/index.html#_17) | Au niveau du bit ou |
| [`~`](https://spark.apache.org/docs/latest/api/sql/index.html#_19) | Au niveau du bit |
| [`arrays_overlap`](https://spark.apache.org/docs/latest/api/sql/index.html#arrays_overlap) | Renvoie les éléments communs |
| [`assert_true`](https://spark.apache.org/docs/latest/api/sql/index.html#assert_true) | Affirme si l’expression est vraie |
| [`if`](https://spark.apache.org/docs/latest/api/sql/index.html#if) | Si l’expression renvoie true (vrai), renvoyez la seconde expression. Sinon, renvoie la troisième expression. |
| [`ifnull`](https://spark.apache.org/docs/latest/api/sql/index.html#ifnull) | Si l’expression est nulle, elle renvoie la seconde expression. Sinon, elle renvoie la première expression. |
| [`in`](https://spark.apache.org/docs/latest/api/sql/index.html#in) | Renvoie true si la première expression se trouve dans l’une des expressions suivantes. |
| [`isnan`](https://spark.apache.org/docs/latest/api/sql/index.html#isnan) | Renvoie true si la valeur n’est pas un nombre |
| [`isnotnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnotnull) | Renvoie true si la valeur n’est pas nulle |
| [`isnull`](https://spark.apache.org/docs/latest/api/sql/index.html#isnull) | Renvoie true si la valeur est nulle |
| [`nanvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nanvl) | Renvoie la première expression si ce n&#39;est pas un nombre, renvoie la seconde expression dans le cas contraire |
| [`or`](https://spark.apache.org/docs/latest/api/sql/index.html#or) | Logique ou |
| [`when`](https://spark.apache.org/docs/latest/api/sql/index.html#when) | Quand peut-on utiliser pour créer des conditions de branche à des fins de comparaison ? |
| [`xpath_boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_boolean) | Renvoie true si l’expression XPath est évaluée comme true ou si un noeud correspondant est trouvé |

### Fonctions de date/heure {#datetime-functions}

| Fonction | Description |
| -------- | ----------- |
| [`add_months`](https://spark.apache.org/docs/latest/api/sql/index.html#add_months) | Ajouter des mois à jour |
| [`date_add`](https://spark.apache.org/docs/latest/api/sql/index.html#date_add) | Ajouter les jours à jour |
| [`date_format`](https://spark.apache.org/docs/latest/api/sql/index.html#date_format) | Modifier le format de date |
| [`date_sub`](https://spark.apache.org/docs/latest/api/sql/index.html#date_sub) | Soustraire les jours à partir de la date |
| [`date_trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#date_trunc) | Renvoie la date tronquée à l’unité spécifiée |
| [`datediff`](https://spark.apache.org/docs/latest/api/sql/index.html#datediff) | Renvoie la différence entre les dates en jours |
| [`day`](https://spark.apache.org/docs/latest/api/sql/index.html#day), [`dayofmonth`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofmonth) | Renvoie le jour du mois |
| [`dayofweek`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofweek) | Renvoie le jour de la semaine (1-7) |
| [`dayofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#dayofyear) | Renvoie le jour de l’année |
| [`from_unixtime`](https://spark.apache.org/docs/latest/api/sql/index.html#from_unixtime) | Renvoie la date en heure Unix |
| [`from_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#from_utc_timestamp) | Renvoie la date en heure UTC |
| [`hour`](https://spark.apache.org/docs/latest/api/sql/index.html#hour) | Renvoie l’heure de l’entrée |
| [`last_day`](https://spark.apache.org/docs/latest/api/sql/index.html#last_day) | Renvoie le dernier jour du mois auquel la date appartient |
| [`minute`](https://spark.apache.org/docs/latest/api/sql/index.html#minute) | Renvoie la minute de l’entrée |
| [`month`](https://spark.apache.org/docs/latest/api/sql/index.html#month) | Renvoie le mois de l’entrée |
| [`months_between`](https://spark.apache.org/docs/latest/api/sql/index.html#months_between) | Nombre de mois entre |
| [`next_day`](https://spark.apache.org/docs/latest/api/sql/index.html#next_day) | Renvoie le premier jour après l’entrée |
| [`quarter`](https://spark.apache.org/docs/latest/api/sql/index.html#quarter) | Renvoie le trimestre de l’entrée |
| [`second`](https://spark.apache.org/docs/latest/api/sql/index.html#second) | Renvoie la seconde de la chaîne |
| [`to_date`](https://spark.apache.org/docs/latest/api/sql/index.html#to_date) | Convertit la chaîne en date. **Remarque :** Chaîne **must** être au format `yyyy-mm-ddTHH24:MM:SS`. |
| [`to_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_timestamp) | Convertit la chaîne en horodatage. **Remarque :** Chaîne **must** être au format `yyyy-mm-ddTHH24:MM:SS`. |
| [`to_unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_unix_timestamp) | Convertit la chaîne en horodatage Unix |
| [`to_utc_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#to_utc_timestamp) | Convertit la chaîne en horodatage UTC |
| [`trunc`](https://spark.apache.org/docs/latest/api/sql/index.html#trunc) | Tronque la date |
| [`unix_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#unix_timestamp) | Renvoie l’horodatage Unix |
| [`weekday`](https://spark.apache.org/docs/latest/api/sql/index.html#weekday) | Jour de la semaine (0-6) |
| [`weekofyear`](https://spark.apache.org/docs/latest/api/sql/index.html#weekofyear) | Renvoie la semaine de l&#39;année pour une date donnée |
| [`year`](https://spark.apache.org/docs/latest/api/sql/index.html#year) | Renvoie l’année de la chaîne |

### Tableaux {#arrays}

| Fonction | Description |
| -------- | ----------- |
| [`array`](https://spark.apache.org/docs/latest/api/sql/index.html#array) | Crée un tableau avec les éléments donnés |
| [`array_contains`](https://spark.apache.org/docs/latest/api/sql/index.html#array_contains) | Vérifie si le tableau contient la valeur |
| [`array_distinct`](https://spark.apache.org/docs/latest/api/sql/index.html#array_distinct) | Supprime les valeurs en double du tableau |
| [`array_except`](https://spark.apache.org/docs/latest/api/sql/index.html#array_except) | Renvoie un tableau des éléments du premier tableau, mais pas du second |
| [`array_intersect`](https://spark.apache.org/docs/latest/api/sql/index.html#array_intersect) | Renvoie l’intersection des deux tableaux |
| [`array_join`](https://spark.apache.org/docs/latest/api/sql/index.html#array_join) | Associe deux tableaux |
| [`array_max`](https://spark.apache.org/docs/latest/api/sql/index.html#array_max) | Renvoie la valeur maximale du tableau |
| [`array_min`](https://spark.apache.org/docs/latest/api/sql/index.html#array_min) | Renvoie la valeur minimale du tableau |
| [`array_position`](https://spark.apache.org/docs/latest/api/sql/index.html#array_position) | Renvoie la position de l’élément basée sur 1 |
| [`array_remove`](https://spark.apache.org/docs/latest/api/sql/index.html#array_remove) | Supprime tous les éléments égaux à l’élément . |
| [`array_repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#array_repeat) | Crée un tableau contenant la valeur count times |
| [`array_sort`](https://spark.apache.org/docs/latest/api/sql/index.html#array_sort) | Trie le tableau |
| [`array_union`](https://spark.apache.org/docs/latest/api/sql/index.html#array_union) | Rejoint le tableau, sans aucun doublon |
| [`arrays_zip`](https://spark.apache.org/docs/latest/api/sql/index.html#array_zip) | Combine les valeurs de tableaux donnés avec les valeurs d’une collection d’origine à un index donné. |
| [`cardinality`](https://spark.apache.org/docs/latest/api/sql/index.html#cardinality) | Renvoie la taille du tableau |
| [`element_at`](https://spark.apache.org/docs/latest/api/sql/index.html#element_at) | Renvoyer l’élément en position |
| [`explode`](https://spark.apache.org/docs/latest/api/sql/index.html#explode) | Séparez les éléments du tableau en plusieurs lignes, à l’exception de null |
| [`explode_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#explode_outer) | Séparez les éléments du tableau en plusieurs lignes, y compris la valeur nulle |
| [`find_in_set`](https://spark.apache.org/docs/latest/api/sql/index.html#find_in_set) | Renvoie la position de base 1 du tableau |
| [`flatten`](https://spark.apache.org/docs/latest/api/sql/index.html#flatten) | Aplatit un tableau de tableaux |
| [`inline`](https://spark.apache.org/docs/latest/api/sql/index.html#inline) | Tableau distinct de structs dans un tableau, à l’exclusion de null |
| [`inline_outer`](https://spark.apache.org/docs/latest/api/sql/index.html#inline_outer) | Tableau distinct de structs dans un tableau, y compris null |
| [`posexplode`](https://spark.apache.org/docs/latest/api/sql/index.html#posexplode) | Séparez les éléments du tableau en plusieurs lignes avec des positions, à l’exception de null |
| [`reverse`](https://spark.apache.org/docs/latest/api/sql/index.html#reverse) | Éléments inversés du tableau |
| [`shuffle`](https://spark.apache.org/docs/latest/api/sql/index.html#shuffle) | Renvoie une permutation aléatoire du tableau |
| [`slice`](https://spark.apache.org/docs/latest/api/sql/index.html#slice) | Sous-définit un tableau |
| [`sort_array`](https://spark.apache.org/docs/latest/api/sql/index.html#sort_array) | Tri d’un tableau selon un ordre donné |
| [`zip_with`](https://spark.apache.org/docs/latest/api/sql/index.html#zip_with) | Fusionne les deux tableaux en un seul tableau, avant d’appliquer une fonction |

### Fonctions de diffusion du type de données {#datatype-casting}

| Fonction | Description |
| -------- | ----------- |
| [`bigint`](https://spark.apache.org/docs/latest/api/sql/index.html#bigint) | Remplacer le type de données par bigint |
| [`binary`](https://spark.apache.org/docs/latest/api/sql/index.html#binary) | Remplacer le type de données par binaire |
| [`boolean`](https://spark.apache.org/docs/latest/api/sql/index.html#boolean) | Remplacez le type de données par booléen. |
| [`type`](https://spark.apache.org/docs/latest/api/sql/index.html#type) | Remplacer le type de données par le type spécifié |
| [`date`](https://spark.apache.org/docs/latest/api/sql/index.html#date) | Modifier le type de données à ce jour |
| [`decimal`](https://spark.apache.org/docs/latest/api/sql/index.html#decimal) | Remplacer le type de données par décimal |
| [`double`](https://spark.apache.org/docs/latest/api/sql/index.html#double) | Remplacez le type de données par double |
| [`float`](https://spark.apache.org/docs/latest/api/sql/index.html#float) | Modifier le type de données pour qu’il soit flottant |
| [`int`](https://spark.apache.org/docs/latest/api/sql/index.html#int) | Remplacez le type de données par int . |
| [`smallint`](https://spark.apache.org/docs/latest/api/sql/index.html#smallint) | Remplacez le type de données par small |
| [`str_to_map`](https://spark.apache.org/docs/latest/api/sql/index.html#str_to_map) | Création d’une carte à partir d’une chaîne |
| [`string`](https://spark.apache.org/docs/latest/api/sql/index.html#string) | Remplacer le type de données par une chaîne |
| [`struct`](https://spark.apache.org/docs/latest/api/sql/index.html#struct) | Création d’un struct |
| [`tinyint`](https://spark.apache.org/docs/latest/api/sql/index.html#tinyint) | Remplacez le type de données par tinyint. |

### Fonctions de conversion et de formatage {#conversion}

| Fonction | Description |
| -------- | ----------- |
| [`ascii`](https://spark.apache.org/docs/latest/api/sql/index.html#ascii) | Renvoie la valeur numérique (ASCII) |
| [`base64`](https://spark.apache.org/docs/latest/api/sql/index.html#base64) | Remplacer l’argument par une chaîne base64 |
| [`bin`](https://spark.apache.org/docs/latest/api/sql/index.html#bin) | Remplacer l’argument par une valeur binaire |
| [`bit_length`](https://spark.apache.org/docs/latest/api/sql/index.html#bit_length) | Renvoie la longueur en bits |
| [`char`](https://spark.apache.org/docs/latest/api/sql/index.html#char), [`chr`](https://spark.apache.org/docs/latest/api/sql/index.html#chr) | Renvoyer le caractère ASCII |
| [`char_length`](https://spark.apache.org/docs/latest/api/sql/index.html#char_length), [`character_length`](https://spark.apache.org/docs/latest/api/sql/index.html#character_length) | Renvoie la longueur de la chaîne |
| [`crc32`](https://spark.apache.org/docs/latest/api/sql/index.html#crc32) | Renvoie la valeur de vérification de redondance cyclique |
| [`degrees`](https://spark.apache.org/docs/latest/api/sql/index.html#degrees) | Convertir les radians en degrés |
| [`format_number`](https://spark.apache.org/docs/latest/api/sql/index.html#format_number) | Modifier le format du nombre |
| [`from_json`](https://spark.apache.org/docs/latest/api/sql/index.html#from_json), [`get_json_object`](https://spark.apache.org/docs/latest/api/sql/index.html#get_json_object) | Obtenir des données à partir de JSON |
| [`hash`](https://spark.apache.org/docs/latest/api/sql/index.html#hash) | Renvoie la valeur de hachage |
| [`hex`](https://spark.apache.org/docs/latest/api/sql/index.html#hex) | Convertir l’argument en valeur hexadécimale |
| [`initcap`](https://spark.apache.org/docs/latest/api/sql/index.html#initcap) | Modification de la chaîne à mettre en cache par le titre |
| [`lcase`](https://spark.apache.org/docs/latest/api/sql/index.html#lcase), [`lower`](https://spark.apache.org/docs/latest/api/sql/index.html#lower) | Modifie la chaîne en minuscules. |
| [`lpad`](https://spark.apache.org/docs/latest/api/sql/index.html#lpad) | Pad le côté gauche d’une chaîne |
| [`map`](https://spark.apache.org/docs/latest/api/sql/index.html#map) | Création d’une carte |
| [`map_from_arrays`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_arrays) | Création d’une carte à partir d’un tableau |
| [`map_from_entries`](https://spark.apache.org/docs/latest/api/sql/index.html#map_from_entries) | Création d’une carte à partir d’un tableau de structs |
| [`md5`](https://spark.apache.org/docs/latest/api/sql/index.html#md5) | Renvoie la valeur md5 |
| [`rpad`](https://spark.apache.org/docs/latest/api/sql/index.html#rpad) | Pad du côté droit d’une chaîne |
| [`rtrim`](https://spark.apache.org/docs/latest/api/sql/index.html#rtrim) | Suppression des espaces à la fin |
| [`sha`](https://spark.apache.org/docs/latest/api/sql/index.html#sha), [`sha1`](https://spark.apache.org/docs/latest/api/sql/index.html#sha1) | Renvoie la valeur SHA1 |
| [`sha2`](https://spark.apache.org/docs/latest/api/sql/index.html#sha2) | Renvoie la valeur SHA2 |
| [`soundex`](https://spark.apache.org/docs/latest/api/sql/index.html#soundex) | Renvoie le code soundex |
| [`stack`](https://spark.apache.org/docs/latest/api/sql/index.html#stack) | Séparation des valeurs en lignes |
| [`substr`](https://spark.apache.org/docs/latest/api/sql/index.html#substr), [`substring`](https://spark.apache.org/docs/latest/api/sql/index.html#substring) | Renvoie la sous-chaîne |
| [`to_json`](https://spark.apache.org/docs/latest/api/sql/index.html#to_json) | Renvoie une chaîne JSON |
| [`translate`](https://spark.apache.org/docs/latest/api/sql/index.html#translate) | Remplacement des valeurs dans une chaîne |
| [`trim`](https://spark.apache.org/docs/latest/api/sql/index.html#trim) | Suppression des caractères de début et de fin |
| [`ucase`](https://spark.apache.org/docs/latest/api/sql/index.html#ucase), [`upper`](https://spark.apache.org/docs/latest/api/sql/index.html#upper) | Modifier la chaîne pour qu’elle soit entièrement en majuscules |
| [`unbase64`](https://spark.apache.org/docs/latest/api/sql/index.html#unbase64) | Convertir la chaîne base64 en binaire |
| [`unhex`](https://spark.apache.org/docs/latest/api/sql/index.html#unhex) | Convertir l’hexadécimal en binaire |
| [`uuid`](https://spark.apache.org/docs/latest/api/sql/index.html#uuid) | Renvoie un UUID |

### Évaluation des données {#data-evaluation}

| Fonction | Description |
| -------- | ----------- |
| [`coalesce`](https://spark.apache.org/docs/latest/api/sql/index.html#coalesce) | Renvoie le premier argument non nul |
| [`collect_list`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_list) | Renvoie une liste d’éléments non uniques |
| [`collect_set`](https://spark.apache.org/docs/latest/api/sql/index.html#collect_set) | Renvoie un ensemble d’éléments uniques |
| [`concat`](https://spark.apache.org/docs/latest/api/sql/index.html#concat) | Concaténation |
| [`concat_ws`](https://spark.apache.org/docs/latest/api/sql/index.html#concat_ws) | Concaténation avec séparateur |
| [`count`](https://spark.apache.org/docs/latest/api/sql/index.html#count) | Renvoie le nombre total de lignes |
| [`decode`](https://spark.apache.org/docs/latest/api/sql/index.html#decode) | Décodage à l’aide d’un jeu de caractères |
| [`elt`](https://spark.apache.org/docs/latest/api/sql/index.html#elt) | Renvoie la variable [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n)entrée |
| [`encode`](https://spark.apache.org/docs/latest/api/sql/index.html#encode) | Codage à l’aide d’un jeu de caractères |
| [`first`](https://spark.apache.org/docs/latest/api/sql/index.html#first), [`first_value`](https://spark.apache.org/docs/latest/api/sql/index.html#first_value) | Renvoie la première valeur |
| [`grouping`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping) | Indique si une colonne est regroupée |
| [`grouping_id`](https://spark.apache.org/docs/latest/api/sql/index.html#grouping_id) | Renvoie le niveau de groupement |
| [`instr`](https://spark.apache.org/docs/latest/api/sql/index.html#instr) | Renvoie un index de base 1 d’occurrence de caractère |
| [`json_tuple`](https://spark.apache.org/docs/latest/api/sql/index.html#json_tuple) | Renvoie un tuple à partir d’une entrée JSON |
| [`lag`](https://spark.apache.org/docs/latest/api/sql/index.html#lag), [`lead`](https://spark.apache.org/docs/latest/api/sql/index.html#lead) | Renvoie la valeur avant le décalage |
| [`last`](https://spark.apache.org/docs/latest/api/sql/index.html#last), [`last_value`](https://spark.apache.org/docs/latest/api/sql/index.html#last_value) | Renvoie la dernière valeur |
| [`left`](https://spark.apache.org/docs/latest/api/sql/index.html#left) | Renvoie le premier [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) caractères |
| [`length`](https://spark.apache.org/docs/latest/api/sql/index.html#length) | Renvoie la longueur de la chaîne |
| [`levenshtein`](https://spark.apache.org/docs/latest/api/sql/index.html#levenshtein) | Renvoie la distance de Levenshtein entre les chaînes |
| [`locate`](https://spark.apache.org/docs/latest/api/sql/index.html#locate), [`position`](https://spark.apache.org/docs/latest/api/sql/index.html#position) | Renvoie la position de la première occurrence d’une sous-chaîne |
| [`map_concat`](https://spark.apache.org/docs/latest/api/sql/index.html#map_concat) | Concaténer une carte |
| [`map_keys`](https://spark.apache.org/docs/latest/api/sql/index.html#map_keys) | Renvoi des clés d’une carte |
| [`map_values`](https://spark.apache.org/docs/latest/api/sql/index.html#map_values) | Renvoie les valeurs d’une carte |
| [`ntile`](https://spark.apache.org/docs/latest/api/sql/index.html#ntile) | Diviser les lignes en partitions |
| [`nullif`](https://spark.apache.org/docs/latest/api/sql/index.html#nullif) | Renvoie null si true |
| [`nvl`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl) | Renvoie la valeur si null |
| [`nvl2`](https://spark.apache.org/docs/latest/api/sql/index.html#nvl2) | Renvoie la valeur si non nul |
| [`parse_url`](https://spark.apache.org/docs/latest/api/sql/index.html#parse_url) | Extrait une partie d&#39;une URL |
| [`rank`](https://spark.apache.org/docs/latest/api/sql/index.html#rank) | Calcule le rang d’une valeur |
| [`regexp_extract`](https://spark.apache.org/docs/latest/api/sql/index.html#regexp_extract) | Extrait quelque chose qui correspond à l’expression régulière |
| [`regex_replace`](https://spark.apache.org/docs/latest/api/sql/index.html#regex_replace) | Remplace quelque chose qui correspond à l’expression régulière |
| [`repeat`](https://spark.apache.org/docs/latest/api/sql/index.html#repeat) | Renvoie une chaîne qui répète |
| [`replace`](https://spark.apache.org/docs/latest/api/sql/index.html#replace) | Remplacer toutes les instances d’une chaîne |
| [`rollup`](https://spark.apache.org/docs/latest/api/sql/index.html#rollup) | Création d’un cumul multidimensionnel |
| [`row_number`](https://spark.apache.org/docs/latest/api/sql/index.html#row_number) | Attribue un numéro de ligne unique |
| [`schema_of_json`](https://spark.apache.org/docs/latest/api/sql/index.html#schema_of_json) | Renvoie le schéma du JSON |
| [`sentences`](https://spark.apache.org/docs/latest/api/sql/index.html#sentences) | Divise la chaîne en un tableau de mots |
| [`sequence`](https://spark.apache.org/docs/latest/api/sql/index.html#sequence) | Génère un tableau d’éléments |
| [`shiftleft`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftleft) | Déplacement au niveau du bit signé à gauche |
| [`shiftright`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftright) | Déplacement au niveau du bit signé à droite |
| [`shiftrightunsigned`](https://spark.apache.org/docs/latest/api/sql/index.html#shiftrightunsigned) | Déplacement au niveau du bit non effectué à droite |
| [`size`](https://spark.apache.org/docs/latest/api/sql/index.html#size) | Renvoie la taille du tableau |
| [`space`](https://spark.apache.org/docs/latest/api/sql/index.html#space) | Renvoie une chaîne avec [`n`](https://spark.apache.org/docs/latest/api/sql/index.html#n) espaces |
| [`split`](https://spark.apache.org/docs/latest/api/sql/index.html#split) | Fractionner la chaîne |
| [`substring_index`](https://spark.apache.org/docs/latest/api/sql/index.html#substring_index) | Retourne l’index de la sous-chaîne |
| [`window`](https://spark.apache.org/docs/latest/api/sql/index.html#window) | Période |
| [`xpath`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath) | Analyse des noeuds XML |
| [`xpath_double`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_double), [`xpath_number`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_number) | Parcourir les noeuds XML pour le double |
| [`xpath_float`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_float) | Analyse des noeuds XML pour les flotteurs |
| [`xpath_int`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_int) | Analyse des noeuds XML pour un entier |
| [`xpath_long`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_long) | Analyse des noeuds XML pour les longues |
| [`xpath_short`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_short) | Analyse des noeuds XML pour un nombre entier court |
| [`xpath_string`](https://spark.apache.org/docs/latest/api/sql/index.html#xpath_string) | Analyse des noeuds XML pour la chaîne |

### Informations actuelles {#current-information}

| Fonction | Description |
| -------- | ----------- |
| [`current_database`](https://spark.apache.org/docs/latest/api/sql/index.html#current_database) | Renvoie la base de données actuelle |
| [`current_date`](https://spark.apache.org/docs/latest/api/sql/index.html#current_date) | Renvoie la date courante |
| [`current_timestamp`](https://spark.apache.org/docs/latest/api/sql/index.html#current_timestamp), [`now`](https://spark.apache.org/docs/latest/api/sql/index.html#now) | Renvoie l’horodatage actuel |

### Fonctions d’ordre supérieur {#higher-order}

| Fonction | Description |
| -------- | ----------- |
| [`transform`](https://spark.apache.org/docs/latest/api/sql/index.html#transform) | Transformation d’éléments dans un tableau |
| [`exists`](https://spark.apache.org/docs/latest/api/sql/index.html#exists) | Vérifier si l’élément existe |
| [`filter`](https://spark.apache.org/docs/latest/api/sql/index.html#filter) | Filtrage du tableau d’entrée |
| [`aggregate`](https://spark.apache.org/docs/latest/api/sql/index.html#aggregate) | Application d’un opérateur binaire à tous les éléments |
