---
title: Récupération d’enregistrements similaires avec des fonctions d’ordre supérieur
description: Découvrez comment identifier et récupérer des enregistrements similaires ou connexes d’un ou de plusieurs jeux de données en fonction d’une mesure de similarité et d’un seuil de similarité. Ce workflow peut mettre en évidence des relations ou des chevauchements significatifs entre des jeux de données disparates.
exl-id: 4810326a-a613-4e6a-9593-123a14927214
source-git-commit: 27eab04e409099450453a2a218659e576b8f6ab4
workflow-type: tm+mt
source-wordcount: '4031'
ht-degree: 3%

---

# Récupération d’enregistrements similaires avec des fonctions d’ordre supérieur

Utilisez les fonctions d’ordre supérieur de Data Distiller pour résoudre divers cas d’utilisation courants. Pour identifier et récupérer des enregistrements similaires ou associés d’un ou plusieurs jeux de données, utilisez le filtre, la transformation et la réduction des fonctions comme décrit dans ce guide. Pour savoir comment utiliser des fonctions d’ordre supérieur pour traiter des types de données complexes, consultez la documentation sur la [gestion des types de données de tableau et de mappage](../sql/higher-order-functions.md).

Utilisez ce guide pour identifier les produits provenant de différents jeux de données présentant une similarité significative de leurs caractéristiques ou attributs. Cette méthodologie fournit des solutions pour : déduplication des données, liaison d’enregistrements, systèmes de recommandation, récupération d’informations et analyse de texte, entre autres.

Le document décrit le processus d’implémentation d’une jointure par analogie, qui utilise ensuite les fonctions d’ordre supérieur de Data Distiller pour calculer la similarité entre des jeux de données et les filtrer selon des attributs sélectionnés. Des fragments de code SQL et des explications sont fournis pour chaque étape du processus. Le workflow met en oeuvre des jointures par similarité à l’aide de la mesure de similarité Jaccard et de la segmentation en jetons à l’aide des fonctions d’ordre supérieur de Data Distiller. Ces méthodes sont ensuite utilisées pour identifier et récupérer des enregistrements similaires ou associés d’un ou plusieurs jeux de données basés sur une mesure de similarité. Les sections clés du processus incluent : [segmentation en unités lexicales à l’aide de fonctions d’ordre supérieur](#data-transformation), la [ jointure croisée d’éléments uniques](#cross-join-unique-elements), le [calcul de similarité Jaccard](#compute-the-jaccard-similarity-measure) et le [&rbrace;filtrage basé sur les seuils](#similarity-threshold-filter).

## Conditions préalables

Avant de poursuivre ce document, vous devez connaître les concepts suivants :

- Une **similarité join** est une opération qui identifie et récupère des paires d&#39;enregistrements d&#39;une ou plusieurs tables en fonction d&#39;une mesure de similarité entre les enregistrements. Les principales exigences pour une jointure par analogie sont les suivantes :
   - **Mesure de similarité** : une jointure par analogie repose sur une mesure ou une mesure de similarité prédéfinie. Ces mesures incluent : la similarité Jaccard, la similarité cosinale, la distance d’édition, etc. La mesure dépend de la nature des données et du cas d’utilisation. Cette mesure quantifie le degré de similarité ou de dissimilarité de deux enregistrements.
   - **Seuil** : un seuil de similarité est utilisé pour déterminer quand les deux enregistrements sont considérés comme suffisamment similaires pour être inclus dans le résultat de la jointure. Les enregistrements avec un score de similarité supérieur au seuil sont considérés comme des correspondances.
- L’index **Jaccard similarity**, ou la mesure Jaccard similarity, est une statistique permettant d&#39;évaluer la similarité et la diversité d&#39;ensembles d&#39;échantillons. Il est défini comme la taille de l’intersection divisée par la taille de l’union des ensembles d’échantillons. La mesure similarité Jaccard est comprise entre zéro et un. Une similitude Jaccard de zéro indique qu’il n’y a aucune similitude entre les ensembles, et une similitude Jaccard de un indique que les ensembles sont identiques.
  ![Diagramme de Venn pour illustrer la mesure Jaccard sur les similarités.](../images/use-cases/jaccard-similarity.png)
- Les **fonctions d’ordre supérieur** dans Data Distiller sont des outils dynamiques intégrés qui traitent et transforment les données directement dans les instructions SQL. Ces fonctions polyvalentes éliminent la nécessité de plusieurs étapes dans la manipulation des données, en particulier lorsque [ traite de types complexes tels que des tableaux et des cartes](../sql/higher-order-functions.md). En améliorant l’efficacité des requêtes et en simplifiant les transformations, des fonctions d’ordre supérieur contribuent à une analyse plus agile et à une meilleure prise de décision dans divers scénarios commerciaux.

## Commencer

Le SKU de Data Distiller est nécessaire pour exécuter les fonctions d’ordre supérieur sur vos données Adobe Experience Platform. Si vous ne possédez pas le SKU de Data Distiller, contactez votre représentant du service client Adobe pour plus d’informations.

## Établir une similarité {#establish-similarity}

Ce cas pratique nécessite une mesure de similarité entre des chaînes de texte qui peuvent être utilisées ultérieurement pour établir un seuil de filtrage. Dans cet exemple, les produits des jeux A et B représentent les mots de deux documents.

La mesure de similarité Jaccard peut être appliquée à un large éventail de types de données, y compris des données texte, des données catégoriques et des données binaires. Il est également adapté au traitement en temps réel ou par lots, car il peut être efficace sur le plan du calcul pour calculer les jeux de données volumineux.

Les ensembles de produits A et B contiennent les données de test pour ce workflow.

- Jeu de produits A : `{iPhone, iPad, iWatch, iPad Mini}`
- Jeu de produits B : `{iPhone, iPad, Macbook Pro}`

Pour calculer la similarité Jaccard entre les ensembles de produits A et B, recherchez d’abord l’ **intersection** (éléments communs) des ensembles de produits. Dans ce cas, `{iPhone, iPad}`. Recherchez ensuite l’ **union** (tous les éléments uniques) des deux ensembles de produits. Dans cet exemple, `{iPhone, iPad, iWatch, iPad Mini, Macbook Pro}`.

Enfin, utilisez la formule de similarité Jaccard : `J(A,B) = A∪B / A∩B` pour calculer la similarité.

J = distance de Jaccard
A = définie 1
B = définie 2

La similitude Jaccard entre les ensembles de produits A et B est 0.4. Cela indique un degré modéré de similitude entre les mots utilisés dans les deux documents. Cette similarité entre les deux ensembles définit les colonnes de la jointure par similarité. Ces colonnes représentent des informations, ou des caractéristiques associées aux données, qui sont stockées dans un tableau et utilisées pour effectuer des calculs de similarité.

### Calcul de la carte par paires avec similarité de chaînes {#pairwise-similarity}

Pour comparer plus précisément les similitudes entre les chaînes, la similarité au niveau des paires doit être calculée. La similarité par paires divise les objets hautement dimensionnels en objets dimensionnels plus petits pour la comparaison et l’analyse. Pour ce faire, une chaîne de texte est divisée en unités ou en parties plus petites (jetons). Il peut s’agir de lettres individuelles, de groupes de lettres (comme des syllabes) ou de mots entiers. La similarité est calculée pour chaque paire de jetons entre chaque élément du jeu A et chaque élément du jeu B. Cette segmentation fournit une base pour les comparaisons analytiques et computationnelles, les relations et les informations à tirer des données.

Pour le calcul des similarités au niveau des paires, cet exemple utilise des bigrammes de caractères (jetons de deux caractères) pour comparer une correspondance de similarité entre les chaînes de texte des produits des jeux A et B. Un bi-gramme est une séquence consécutive de deux éléments ou éléments dans une séquence ou un texte donné. Vous pouvez généraliser ceci en n-grammes.

Cet exemple suppose que la casse n’a pas d’importance et que les espaces ne doivent pas être pris en compte. Selon ces critères, les ensembles A et B présentent les deux grammes suivants :

Jeu de produits A bi-grammes :

- iPhone (5) : &quot;ip&quot;, &quot;ph&quot;, &quot;ho&quot;, &quot;on&quot;, &quot;ne&quot;
- iPad (3) : &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;
- iWatch (5) : &quot;iw&quot;, &quot;wa&quot;, &quot;at&quot;, &quot;tc&quot;, &quot;ch&quot;
- iPad Mini (7) : &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;, &quot;dm&quot;, &quot;mi&quot;, &quot;in&quot;, &quot;ni&quot;

bi-grammes de la visionneuse de produits B :

- iPhone (5) : &quot;ip&quot;, &quot;ph&quot;, &quot;ho&quot;, &quot;on&quot;, &quot;ne&quot;
- iPad (3) : &quot;ip&quot;, &quot;pa&quot;, &quot;ad&quot;
- Macbook Pro (9) : &quot;Ma&quot;, &quot;ac&quot;, &quot;cb&quot;, &quot;bo&quot;, &quot;oo&quot;, &quot;ok&quot;, &quot;kp&quot;, &quot;pr&quot;, &quot;ro&quot;

Ensuite, calculez le coefficient de similarité Jaccard pour chaque paire :

|                   | iPhone (jeu B) | iPad (jeu B) | Macbook Pro (Jeu B) |
|-------------------|----------------------------------------------|---------------------------------------------|-------------------------------------------|
| iPhone (jeu A) | (Intersection : 5, Union : 5) = 5 / 5 = 1 | (Intersection : 1, Union : 7) =1 / 7 ≈ 0,14 | (Intersection : 0, Union : 14) = 0 / 14 = 0 |
| iPad (jeu A) | (Intersection : 1, Union : 7) = 1 / 7 ≈ 0,14 | (Intersection : 3, Union : 3) = 3 / 3 = 1 | (Intersection : 0, Union : 12) = 0 / 12 = 0 |
| iWatch (Set A) | (Intersection : 0, Union : 8) = 0 / 8 = 0 | (Intersection : 0, Union : 8) = 0 / 8 = 0 | (Intersection : 0, Union : 8) = 0 / 8 = 0 |
| iPad Mini (Set A) | (Intersection : 1, Union : 11) = 1 / 11 ≈ 0,09 | (Intersection : 3, Union : 7) = 3 / 7 ≈ 0,43 | (Intersection : 0, Union : 16) = 0 / 16 = 0 |

{style="table-layout:auto"}

## Création des données de test avec SQL {#create-test-data}

Pour créer manuellement un tableau de test pour les ensembles de produits, utilisez l’instruction SQL CREATE TABLE .

```SQL {line-numbers="true"}
CREATE TABLE featurevector1 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'iWatch'
     UNION ALL
    SELECT 'iPad Mini'
);
SELECT * FROM featurevector1;
```

Les descriptions suivantes fournissent une ventilation du bloc de code SQL ci-dessus :

- Ligne 1 : `CREATE TEMP TABLE featurevector1 AS` : cette instruction crée une table temporaire nommée `featurevector1`. En règle générale, les tables temporaires ne sont accessibles que dans la session en cours et sont automatiquement déposées à la fin de la session.
- Ligne 1 et 2 : `SELECT * FROM (...)` : cette partie du code est une sous-requête utilisée pour générer les données insérées dans la table `featurevector1`.
Dans la sous-requête, plusieurs instructions `SELECT` sont combinées à l’aide de la commande `UNION ALL`. Chaque instruction `SELECT` génère une ligne de données avec les valeurs spécifiées pour la colonne `ProductName`.
- Ligne 3 : `SELECT 'iPad' AS ProductName` : génère une ligne avec la valeur `iPad` dans la colonne `ProductName`.
- Ligne 5 : `SELECT 'iPhone'` : génère une ligne avec la valeur `iPhone` dans la colonne `ProductName`.

L’instruction SQL crée un tableau comme illustré ci-dessous :

|   | `ProductName` |
|---|---------------|
| 1 | iPad |
| 2 | iPhone |
| 3 | iWatch |
| 4 | iPad Mini |

{style="table-layout:auto"}

Pour créer le second vecteur de fonctionnalité, utilisez l’instruction SQL suivante :

```SQL
CREATE TABLE featurevector2 AS SELECT *
FROM (
    SELECT 'iPad' AS ProductName
    UNION ALL
    SELECT 'iPhone'
    UNION ALL
    SELECT 'Macbook Pro'
);
SELECT * FROM featurevector2;
```

## Conversion des données {#data-transformation}

Dans cet exemple, plusieurs actions doivent être effectuées pour comparer précisément les visionneuses. Tout d’abord, les espaces blancs sont supprimés des vecteurs de fonctionnalités, puisqu’il est supposé qu’ils ne contribuent pas à la mesure de similarité. Ensuite, tous les doublons présents dans le vecteur de fonctionnalité sont supprimés lorsqu’ils perdent le traitement informatique. Ensuite, les jetons de deux caractères (bi-grammes) sont extraits des vecteurs de fonctionnalités. Dans cet exemple, elles se chevauchent.

>[!NOTE]
>
>À titre d’illustration, les colonnes traitées sont ajoutées en regard du vecteur de la fonctionnalité pour chacune des étapes.

Les sections suivantes illustrent les transformations de données prérequises telles que le dédoublonnage, la suppression d’espaces et la conversion en minuscules avant de lancer le processus de segmentation en unités lexicales.

### Déduplication {#deduplication}

Ensuite, utilisez la clause `DISTINCT` pour supprimer les doublons. Il n’existe aucun doublon dans cet exemple, mais il s’agit d’une étape importante pour améliorer la précision de toute comparaison. Le code SQL nécessaire est affiché ci-dessous :

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct FROM featurevector1
SELECT DISTINCT(ProductName) AS featurevector2_distinct FROM featurevector2
```

### Suppression des espaces blancs {#whitespace-removal}

Dans l’instruction SQL suivante, les espaces sont supprimés des vecteurs de fonctionnalités. La partie `replace(ProductName, ' ', '') AS featurevector1_nospaces` de la requête extrait la colonne `ProductName` de la table `featurevector1` et utilise la fonction `replace()`. La fonction `REPLACE` remplace toutes les occurrences d’un espace (’ ’) par une chaîne vide (’). Cela supprime effectivement tous les espaces des valeurs `ProductName`. Le résultat comporte un alias `featurevector1_nospaces`.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, replace(ProductName, ' ', '') AS featurevector1_nospaces FROM featurevector1
```

Les résultats sont présentés dans le tableau ci-dessous :

|   | featurevector1_distinct | featurevector1_nospaces |
|---|---|---|
| 1 | iPad Mini | iPadMini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

L’instruction SQL et ses résultats sur le deuxième vecteur de fonctionnalité sont présentés ci-dessous :

+++Sélectionner pour développer

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, replace(ProductName, ' ', '') AS featurevector2_nospaces FROM featurevector2
```

Les résultats s’affichent comme suit :

|   | featurevector2_distinct | featurevector2_nospaces |
|---|---|---|
| 1 | iPad | iPad |
| 2 | Macbook Pro | MacbookPro |
| 3 | iPhone | iPhone |

{style="table-layout:auto"}

+++

### Convertir en minuscules {#lowercase-conversion}

Ensuite, le code SQL est amélioré pour convertir les noms de produits en minuscules et supprimer les espaces. La fonction inférieure (`lower(...)`) est appliquée au résultat de la fonction `replace()`. La fonction lower convertit en minuscules tous les caractères des valeurs `ProductName` modifiées. Cela garantit que les valeurs sont en minuscules, quelle que soit leur casse d’origine.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform FROM featurevector1;
```

Le résultat de cette instruction est le suivant :

|   | featurevector1_distinct | featurevector1_transform |
|---|---|---|
| 1 | iPad Mini | ipadmini |
| 2 | iPad | iPad |
| 3 | iWatch | iWatch |
| 4 | iPhone | iPhone |

{style="table-layout:auto"}

L’instruction SQL et ses résultats sur le deuxième vecteur de fonctionnalité sont présentés ci-dessous :

+++Sélectionner pour développer

```SQL
SELECT DISTINCT(ProductName) AS featurevector2_distinct, lower(replace(ProductName, ' ', '')) AS featurevector2_transform FROM featurevector2
```

Les résultats s’affichent comme suit :

|   | featurevector2_distinct | featurevector2_transform |
|---|---|---|
| 1 | iPad | ipad |
| 2 | Macbook Pro | macbookpro |
| 3 | iPhone | iphone |

{style="table-layout:auto"}

+++

### Extraction de jetons à l’aide de SQL {#tokenization}

L’étape suivante est la segmentation en unités lexicales ou le fractionnement de texte. La Tokenization est le processus consistant à prendre du texte et à le diviser en termes individuels. Cela implique généralement de diviser des phrases en mots. Dans cet exemple, les chaînes sont ventilées en bi-grammes (et n-grammes de plus grand ordre) en extrayant des jetons à l’aide de fonctions SQL telles que `regexp_extract_all`. Les doublons doivent être générés pour une segmentation efficace.

Le code SQL a été amélioré de manière à utiliser `regexp_extract_all`. `regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0) AS tokens:` Cette partie de la requête traite davantage les valeurs `ProductName` modifiées créées à l’étape précédente. Elle utilise la fonction `regexp_extract_all()` pour extraire toutes les sous-chaînes qui ne se chevauchent pas de un à deux caractères des valeurs `ProductName` modifiées et en minuscules. Le modèle d’expression régulière `.{2}` correspond à des sous-chaînes de deux caractères de longueur. La partie `regexp_extract_all(..., '.{2}', 0)` de la fonction extrait ensuite toutes les sous-chaînes correspondantes du texte d’entrée.

```SQL
SELECT DISTINCT(ProductName) AS featurevector1_distinct, lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
regexp_extract_all(lower(replace(ProductName, ' ', '')) , '.{2}', 0) AS tokens
FROM featurevector1;
```

Les résultats sont présentés dans le tableau ci-dessous :

+++Sélectionner pour développer

|   | featurevector1_distinct | featurevector1_transform | jetons |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;,&quot;ad&quot;,&quot;mi&quot;,&quot;ni&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;,&quot;ad&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;,&quot;at&quot;, &quot;ch&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;,&quot;ho&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Pour améliorer davantage la précision, le code SQL doit être utilisé pour créer des jetons qui se chevauchent. Par exemple, la chaîne &quot;iPad&quot; ci-dessus ne contient pas le jeton &quot;pa&quot;. Pour corriger ce problème, déplacez l’opérateur de recherche en amont (à l’aide de `substring`) d’une étape et générez les bigrammes.

Tout comme l’étape précédente, `regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0):` extrait des séquences de deux caractères du nom du produit modifié, mais commence par le deuxième caractère à l’aide de la méthode `substring` pour créer des jetons qui se chevauchent. Ensuite, dans les lignes 3 à 7 (`array_union(...) AS tokens`), la fonction `array_union()` combine les tableaux de séquences de deux caractères obtenus par les deux extractions d’expression régulière. Cela permet de s’assurer que le résultat contient des jetons uniques provenant de séquences qui ne se chevauchent pas et qui se chevauchent.

```SQL {line-numbers="true"}
SELECT DISTINCT(ProductName) AS featurevector1_distinct, 
       lower(replace(ProductName, ' ', '')) AS featurevector1_transform, 
       array_union(
           regexp_extract_all(lower(replace(ProductName, ' ', '')), '.{2}', 0),
           regexp_extract_all(lower(replace(substring(ProductName, 2), ' ', '')), '.{2}', 0)
       ) AS tokens
FROM featurevector1;
```

Les résultats sont présentés dans le tableau ci-dessous :

+++Sélectionner pour développer

|   | featurevector1_distinct | featurevector1_transform | jetons |
|---|--------------------------|--------------|------------------------|
| 1 | iPad Mini | ipadmini | {&quot;ip&quot;,&quot;ad&quot;,&quot;mi&quot;,&quot;ni&quot;,&quot;pa&quot;,&quot;dm&quot;,&quot;in&quot;} |
| 2 | iPad | iPad | {&quot;ip&quot;,&quot;ad&quot;,&quot;pa&quot;} |
| 3 | iWatch | iWatch | {&quot;iw&quot;,&quot;at&quot;,&quot;ch&quot;,&quot;wa&quot;,&quot;tc&quot;} |
| 4 | iPhone | iPhone | {&quot;ip&quot;,&quot;ho&quot;,&quot;ne&quot;,&quot;ph&quot;,&quot;on&quot;} |

{style="table-layout:auto"}

+++

Cependant, l’utilisation de `substring` comme solution au problème présente des limites. Si vous deviez créer des jetons à partir du texte en fonction de trois grammes (trois caractères), il faudrait utiliser deux `substrings` pour effectuer deux recherches en amont afin d’obtenir les décalages requis. Pour produire 10 grammes, vous avez besoin de neuf expressions `substring`. Cela ferait gonfler le code et cela deviendrait intenable. L’utilisation d’expressions régulières simples n’est pas appropriée. Une nouvelle approche est nécessaire.

### Ajuster à la longueur du nom du produit {#length-adjustment}

Le SQl peut être amélioré grâce aux fonctions de séquence et de longueur. Dans l’exemple suivant, `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3)` génère une séquence de nombres de un à la longueur du nom de produit modifié moins trois. Par exemple, si le nom du produit modifié est &quot;ipadmini&quot; avec une longueur de huit caractères, il génère des nombres de un à cinq (huit à trois).

L’instruction ci-dessous extrait des noms de produits uniques, puis décompose chaque nom en séquences de caractères (jetons) de quatre longueurs de caractères, à l’exclusion des espaces et les présente sous la forme de deux colonnes. Une colonne affiche les noms uniques des produits et l’autre les jetons générés.

```SQL
SELECT
   DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 3),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 4)
  ) AS tokens
FROM
  featurevector1;
```

Les résultats sont présentés dans le tableau ci-dessous :

+++Sélectionner pour développer

|   | featurevector1_distinct | jetons |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipad&quot;,&quot;padm&quot;,&quot;admi&quot;,&quot;dmin&quot;,&quot;mini&quot;} |
| 2 | iPad | {&quot;ipad&quot;} |
| 3 | iWatch | {&quot;iwat&quot;,&quot;watc&quot;,&quot;atch&quot;} |
| 4 | iPhone | {&quot;ipho&quot;,&quot;phon&quot;,&quot;hone&quot;} |

{style="table-layout:auto"}

+++

### Vérification de la longueur du jeton définie {#ensure-set-token-length}

Des conditions supplémentaires peuvent être ajoutées à l’instruction pour s’assurer que les séquences générées ont une longueur spécifique. L’instruction SQL suivante développe la logique de génération de jeton en rendant la fonction `transform` plus complexe. L’instruction utilise la fonction `filter` dans `transform` pour s’assurer que les séquences générées ont une longueur de six caractères. Il gère les cas où cela n’est pas possible en attribuant des valeurs NULL à ces positions.

```SQL
SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 5),
      i -> i + 5 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 6)) = 6
               THEN substring(lower(replace(ProductName, ' ', '')), i, 6)
               ELSE NULL
          END
  ) AS tokens
FROM
  featurevector1;
```

Les résultats sont présentés dans le tableau ci-dessous :

+++Sélectionner pour développer

|   | featurevector1_distinct | jetons |
|---|--------------------------|------------------------|
| 1 | iPad Mini | {&quot;ipadmi&quot;,&quot;padmin&quot;,&quot;admini&quot;} |
| 2 | iPad | {null} |
| 3 | iWatch | {&quot;iwatch&quot;} |
| 4 | iPhone | {&quot;iphone&quot;} |

{style="table-layout:auto"}

+++

## Exploration des solutions à l’aide des fonctions d’ordre supérieur de Data Distiller {#higher-order-function-solutions}

Les fonctions d’ordre supérieur sont des constructions puissantes qui vous permettent de mettre en oeuvre une &quot;programmation&quot; comme la syntaxe dans Data Distiller. Ils peuvent être utilisés pour itérer une fonction sur plusieurs valeurs d’un tableau.

Dans le contexte de Data Distiller, les fonctions d’ordre supérieur sont idéales pour créer des n-grammes et itérer sur des séquences de caractères.

La fonction `reduce`, en particulier lorsqu’elle est utilisée dans des séquences générées par `transform`, permet d’obtenir des valeurs cumulatives ou des agrégats, qui peuvent être essentiels dans divers processus d’analyse et de planification.

Par exemple, dans l’instruction SQl ci-dessous, la fonction `reduce()` agrège des éléments dans un tableau à l’aide d’un agrégateur personnalisé. Il simule une boucle for pour **créer les sommes cumulées de tous les nombres entiers** de un à cinq. `1, 1+2, 1+2+3, 1+2+3+4, 1+2+3+4`.

```SQL {line-numbers="true"}
SELECT transform(
    sequence(1, 5), 
    x -> reduce(
        sequence(1, x),  
        0,  -- Initial accumulator value
        (acc, y) -> acc + y  -- Higher-order function to add numbers
    )
) AS sum_result;
```

Voici une analyse de l’instruction SQL :

- La ligne 1 : `transform` applique la fonction `x -> reduce` sur chaque élément généré dans la séquence.
- Ligne 2 : `sequence(1, 5)` génère une séquence de nombres de un à cinq.
- Ligne 3 : `x -> reduce(sequence(1, x), 0, (acc, y) -> acc + y)` effectue une opération de réduction pour chaque élément x de la séquence (de 1 à 5).
   - La fonction `reduce` prend une valeur d’accumulateur initiale de 0, une séquence de 1 à la valeur actuelle de `x` et une fonction d’ordre supérieur `(acc, y) -> acc + y` pour ajouter les nombres.
   - La fonction d&#39;ordre supérieur `acc + y` accumule la somme en ajoutant la valeur actuelle `y` à l&#39;accumulateur `acc`.
- Ligne 8 : `AS sum_result` renomme la colonne obtenue en tant que sum_result.

Pour résumer, cette fonction d’ordre supérieur prend deux paramètres (`acc` et `y`) et définit l’opération à effectuer, qui dans ce cas ajoute `y` à l’accumulateur `acc`. Cette fonction d’ordre supérieur est exécutée pour chaque élément de la séquence pendant le processus de réduction.

La sortie de cette instruction est une seule colonne (`sum_result`) qui contient les sommes cumulées de nombres comprises entre 1 et 5.

### La valeur des fonctions d’ordre supérieur {#value-of-higher-order-functions}

Cette section analyse une version abrégée d’une instruction SQL à trois grammes afin de mieux comprendre la valeur des fonctions d’ordre supérieur dans Data Distiller pour créer des n-grammes plus efficacement.

L’instruction ci-dessous fonctionne sur la colonne `ProductName` de la table `featurevector1`. Elle produit un ensemble de sous-chaînes de trois caractères dérivées des noms de produits modifiés dans le tableau, à l’aide de positions obtenues à partir de la séquence générée.

```SQL {line-numbers="true"}
SELECT
  transform(
    sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2),
    i -> substring(lower(replace(ProductName, ' ', '')), i, 3)
  ) 
FROM
  featurevector1
```

Voici une analyse de l’instruction SQL :

- Ligne 2 : `transform` applique une fonction d’ordre supérieur à chaque entier de la séquence.
- La ligne 3 : `sequence(1, length(lower(replace(ProductName, ' ', ''))) - 2)` génère une séquence d’entiers entre `1` et la longueur du nom du produit modifié moins deux.
   - `length(lower(replace(ProductName, ' ', '')))` calcule la longueur de `ProductName` après l&#39;avoir fait en minuscules et après avoir supprimé des espaces.
   - `- 2` soustrait deux de la longueur pour s’assurer que la séquence génère des positions de départ valides pour les sous-chaînes de 3 caractères. Si vous soustrayez 2, vous aurez suffisamment de caractères après chaque position de départ pour extraire une sous-chaîne de 3 caractères. La fonction de sous-chaîne ici fonctionne comme un opérateur de recherche en amont.
- Ligne 4 : `i -> substring(lower(replace(ProductName, ' ', '')), i, 3)` est une fonction d’ordre supérieur qui fonctionne sur chaque entier `i` de la séquence générée.
   - La fonction `substring(...)` extrait une sous-chaîne de 3 caractères de la colonne `ProductName`.
   - Avant d’extraire la sous-chaîne, `lower(replace(ProductName, ' ', ''))` convertit les `ProductName` en minuscules et supprime les espaces pour garantir la cohérence.

La sortie est une liste de sous-chaînes de trois caractères, extraites des noms de produits modifiés, en fonction des positions spécifiées dans la séquence.

## Filtrer les résultats {#filter-results}

La fonction `filter`, avec les [transformations de données](#data-transformation) suivantes, permet une extraction plus précise et plus affinée des informations pertinentes à partir des données de texte. Cela vous permet d’obtenir des informations, d’améliorer la qualité des données et de faciliter de meilleurs processus de prise de décision.

La fonction `filter` de l’instruction SQL suivante sert à affiner et à limiter la séquence de positions dans la chaîne à partir de laquelle les sous-chaînes sont extraites à l’aide de la fonction de transformation suivante.

```SQL
SELECT
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 6),
      i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 7)) = 7
               THEN substring(lower(replace(ProductName, ' ', '')), i, 7)
               ELSE NULL
          END
  )
FROM
  featurevector1;
```

La fonction `filter` génère une séquence de positions de départ valides dans le `ProductName` modifié et extrait les sous-chaînes d’une longueur spécifique. Seules les positions de départ permettant d’extraire une sous-chaîne de sept caractères sont autorisées.

La condition `i -> i + 6 <= length(lower(replace(ProductName, ' ', '')))` garantit que la position de départ `i` plus `6` (la longueur de la sous-chaîne de sept caractères souhaitée moins une) ne dépasse pas la longueur du `ProductName` modifié.

L’instruction `CASE` est utilisée pour inclure ou exclure de manière conditionnelle des sous-chaînes en fonction de leur longueur. Seules les sous-chaînes de sept caractères sont incluses ; les autres sont remplacées par NULL. Ces sous-chaînes sont ensuite utilisées par la fonction `transform` pour créer une séquence de sous-chaînes à partir de la colonne `ProductName` de la table `featurevector1`.

>[!TIP]
>
>Vous pouvez utiliser la fonction [modèles paramétrés](../ui/parameterized-queries.md) pour réutiliser et abstraire la logique dans vos requêtes. Par exemple, lorsque vous créez des fonctions d’utilitaire d’usage général (comme celle affichée ci-dessus pour les chaînes de jeton), vous pouvez utiliser des modèles paramétrés de Data Distiller où le nombre de caractères serait un paramètre.

## Calcul de la jointure croisée d’éléments uniques sur deux vecteurs de fonctionnalités {#cross-join-unique-elements}

Identifier les différences ou les incohérences entre les deux jeux de données en fonction d’une transformation spécifique des données est un processus courant pour maintenir la précision des données, améliorer la qualité des données et assurer la cohérence entre les jeux de données.

Cette instruction SQL ci-dessous extrait les noms de produits uniques présents dans `featurevector2`, mais pas dans `featurevector1` après avoir appliqué les transformations.

```SQL
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector2
EXCEPT
SELECT lower(replace(ProductName, ' ', '')) FROM featurevector1;
```

>[!TIP]
>
>Outre `EXCEPT`, vous pouvez également utiliser `UNION` et `INTERSECT` en fonction de votre cas d’utilisation. Vous pouvez également tester les clauses `ALL` ou `DISTINCT` pour voir la différence entre l’inclusion de toutes les valeurs et le renvoi uniquement des valeurs uniques pour les colonnes spécifiées.

Les résultats sont présentés dans le tableau ci-dessous :

+++Sélectionner pour développer

|   | lower(replace(ProductName, &#39;, &#39;&#39;)) |
|---|---------------------------------------|
| 1 | macbookpro |

{style="table-layout:auto"}

+++

Effectuez ensuite une jointure croisée pour combiner les éléments des deux vecteurs de fonctionnalités afin de créer des paires d’éléments à des fins de comparaison. La première étape de ce processus est de créer un vecteur à jetons.

Un vecteur à jetons est une représentation structurée de données de texte dans laquelle chaque mot, expression ou unité de signification (jeton) est converti en un format numérique. Cette conversion permet aux algorithmes de traitement de langage naturel de comprendre et d’analyser les informations textuelles.

Le SQl ci-dessous crée un vecteur à jetons.

```SQL
CREATE TABLE featurevector1tokenized AS SELECT
  DISTINCT(ProductName) AS featurevector1_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
  (SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector1);
SELECT * FROM featurevector1tokenized;
```

>[!NOTE]
>
>Si vous utilisez [!DNL DbVisualizer], après avoir créé ou supprimé une table, actualisez la connexion à la base de données afin que le cache de métadonnées de la table soit actualisé. Data Distiller n’évite pas les mises à jour de métadonnées.

Les résultats sont présentés dans le tableau ci-dessous :

+++Sélectionner pour développer

|   | featurevector1_distinct | jetons |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} |
| 2 | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 3 | iwatch | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} |
| 4 | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Répétez ensuite le processus pour `featurevector2` :

```SQL
CREATE TABLE featurevector2tokenized AS 
SELECT
  DISTINCT(ProductName) AS featurevector2_distinct,
  transform(
    filter(
      sequence(1, length(lower(replace(ProductName, ' ', ''))) - 1),
      i -> i + 1 <= length(lower(replace(ProductName, ' ', '')))
    ),
    i -> CASE WHEN length(substring(lower(replace(ProductName, ' ', '')), i, 2)) = 2
               THEN substring(lower(replace(ProductName, ' ', '')), i, 2)
               ELSE NULL
          END
  ) AS tokens
FROM
(SELECT lower(replace(ProductName, ' ', '')) AS ProductName FROM featurevector2
);
SELECT * FROM featurevector2tokenized;
```

Les résultats sont présentés dans le tableau ci-dessous :

+++Sélectionner pour développer

|   | featurevector2_distinct | jetons |
|---|--------------------------|------------------------|
| 1 | ipadmini | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 2 | macbookpro | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 3 | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

Une fois les deux vecteurs segmentés en unités terminées, vous pouvez désormais créer la jointure croisée. Ceci est illustré dans le SQL ci-dessous :

```SQL {line-numbers="true"}
SELECT
    A.featurevector1_distinct AS SetA_ProductNames,
    B.featurevector2_distinct AS SetB_ProductNames,
    A.tokens AS SetA_tokens1,
    B.tokens AS SetB_tokens2
FROM
    featurevector1tokenized A
CROSS JOIN
    featurevector2tokenized B;
```

Voici un résumé de l’interface utilisateur graphique utilisée pour créer la jointure croisée :

- Ligne 2 : `A.featurevector1_distinct AS SetA_ProductNames` sélectionne la colonne `featurevector1_distinct` de la table `A` et lui attribue un alias `SetA_ProductNames`. Cette section de SQL génère une liste de noms de produits distincts du premier jeu de données.
- Ligne 4 : `A.tokens AS SetA_tokens1` sélectionne la colonne `tokens` de la table ou de la sous-requête `A` et lui attribue un alias `SetA_tokens1`. Cette section de SQL génère une liste de valeurs segmentées en unités lexicales associées aux noms de produits du premier jeu de données.
- Ligne 8 : l’opération `CROSS JOIN` combine toutes les combinaisons possibles de lignes des deux jeux de données. En d’autres termes, il associe chaque nom de produit et ses jetons associés à partir de la première table (`A`) à chaque nom de produit et à ses jetons associés à partir de la seconde table (`B`). Cela génère un produit cartésien des deux jeux de données, où chaque ligne de la sortie représente une combinaison d’un nom de produit et de ses jetons associés à partir des deux jeux de données.

Les résultats sont présentés dans le tableau ci-dessous :

+++Sélectionner pour développer

| * | SetA_ProductNames | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 |
|---|---------------------|-------------------|---|---|
| 1 | ipadmini | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 3 | ipadmini | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 4 | ipad | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 5 | ipad | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 6 | ipad | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 7 | iwatch | ipad | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 8 | iwatch | macbookpro | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 9 | iwatch | iphone | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |
| 10 | iphone | ipad | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} |
| 11 | iphone | macbookpro | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} |
| 12 | iphone | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} |

{style="table-layout:auto"}

+++

## Calculez la mesure de similarité Jaccard {#compute-the-jaccard-similarity-measure}

Ensuite, calculez l’utilisation du coefficient de similarité Jaccard pour effectuer une analyse des similarités entre les deux ensembles de noms de produits en comparant leurs représentations segmentées en unités lexicales. La sortie du script SQL ci-dessous fournit les éléments suivants : noms de produits des deux ensembles, leurs représentations en unités lexicales, le nombre de jetons uniques communs et totaux et le coefficient de similarité Jaccard calculé pour chaque paire de jeux de données.


```SQL {line-numbers="true"}
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) /    size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    );
```

Voici un résumé du SQL utilisé pour calculer le coefficient de similarité Jaccard :

- Ligne 6 : `size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count` calcule le nombre de jetons communs à `SetA_tokens1` et `SetB_tokens2`. Ce calcul est réalisé en calculant la taille de l’intersection des deux tableaux de jetons.
- Ligne 7 : `size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count` calcule le nombre total de jetons uniques sur `SetA_tokens1` et `SetB_tokens2`. Cette ligne calcule la taille de l’union des deux tableaux de jetons.
- Ligne 8-10 : `ROUND(CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)), 2) AS jaccard_similarity` calcule la similarité Jaccard entre les jeux de jetons. Ces lignes divisent la taille de l’intersection de jetons par la taille de l’union de jetons et arrondissent le résultat à deux décimales. Le résultat est une valeur comprise entre zéro et un, où un indique une similarité complète.

Les résultats sont présentés dans le tableau ci-dessous :

+++Sélectionner pour développer

| * | SetA_ProductNames | SetB_ProductNames | SetA_tokens 1 | SetB_tokens 2 | token_intersect_count | token_intersect_count | Similarité de Jaccard |
|---|---------------------|-------------------|---------------------------------------|-------------------------------------------------|----|----|----|
| 1 | ipadmini | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 3 | 7 | 0,43 |
| 2 | ipadmini | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 16 | 0,0 |
| 3 | ipadmini | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;,&quot;dm&quot;,&quot;mi&quot;,&quot;in&quot;,&quot;ni&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 1 | 11 | 0,09 |
| 4 | ipad | ipad | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 3 | 3 | 1.0 |
| 5 | ipad | macbookpro | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 12 | 0,0 |
| 6 | ipad | iphone | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 1 | 7 | 0,14 |
| 7 | iwatch | ipad | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 0 | 8 | 0,0 |
| 8 | iwatch | macbookpro | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 14 | 0,0 |
| 9 | iwatch | iphone | {&quot;iw&quot;,&quot;wa&quot;,&quot;at&quot;,&quot;tc&quot;,&quot;ch&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 0 | 10 | 0,0 |
| 10 | iphone | ipad | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;pa&quot;,&quot;ad&quot;} | 1 | 7 | 0,14 |
| 11 | iphone | macbookpro | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ma&quot;,&quot;ac&quot;,&quot;cb&quot;,&quot;bo&quot;,&quot;oo&quot;,&quot;ok&quot;,&quot;kp&quot;,&quot;pr&quot;,&quot;ro&quot;} | 0 | 14 | 0,0 |
| 12 | iphone | iphone | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | {&quot;ip&quot;,&quot;ph&quot;,&quot;ho&quot;,&quot;on&quot;,&quot;ne&quot;} | 5 | 5 | 1.0 |

{style="table-layout:auto"}

+++

## Filtrage des résultats selon le seuil de similarité de parcours {#similarity-threshold-filter}

Enfin, filtrez les résultats selon un seuil prédéfini afin de sélectionner uniquement les paires répondant aux critères de similarité. L’instruction SQL ci-dessous filtre les produits avec un coefficient de similarité Jaccard d’au moins 0,4. Cela réduit les résultats en paires présentant un degré substantiel de similarité.

```SQL
SELECT 
    SetA_ProductNames, 
    SetB_ProductNames
FROM 
(SELECT 
    SetA_ProductNames, 
    SetB_ProductNames, 
    SetA_tokens1,
    SetB_tokens2,
    size(array_intersect(SetA_tokens1, SetB_tokens2)) AS token_intersect_count,
    size(array_union(SetA_tokens1, SetB_tokens2)) AS token_union_count,
    ROUND(
        CAST(size(array_intersect(SetA_tokens1, SetB_tokens2)) AS DOUBLE) / size(array_union(SetA_tokens1, SetB_tokens2)),
        2
    ) AS jaccard_similarity
FROM
    (SELECT
        A.featurevector1_distinct AS SetA_ProductNames,
        B.featurevector2_distinct AS SetB_ProductNames,
        A.tokens AS SetA_tokens1,
        B.tokens AS SetB_tokens2
    FROM
        featurevector1tokenized A
    CROSS JOIN
        featurevector2tokenized B
    )
)
WHERE jaccard_similarity>=0.4
```

Les résultats de cette requête donnent les colonnes pour la jointure par analogie, comme illustré ci-dessous :

+++Sélectionner pour développer

|   | SetA_ProductNames | SetA_ProductNames |
|---|--------------------------|------------------------|
| 1 | ipadmini | ipad |
| 2 | ipad | ipad |
| 3 | iphone | iphone |

{style="table-layout:auto"}

+++:

### Étapes suivantes {#next-steps}

En lisant ce document, vous pouvez désormais utiliser cette logique pour mettre en évidence des relations ou des chevauchements significatifs entre des jeux de données disparates. La possibilité d’identifier des produits provenant de différents jeux de données présentant une similarité significative de leurs caractéristiques ou attributs comporte de nombreuses applications réelles. Cette logique peut être utilisée pour des scénarios tels que :

- Correspondance de produits : pour regrouper ou recommander des produits similaires aux clients.
- Nettoyage des données : pour améliorer la qualité des données.
- Analyse du panier de marché : pour fournir des informations sur le comportement, les préférences et les opportunités de ventes croisées potentielles des clients.

Si vous ne l’avez pas déjà fait, nous vous recommandons de lire la [présentation du pipeline de fonctionnalités AI/ML](../data-distiller/ml-feature-pipelines/overview.md). Utilisez cet aperçu pour découvrir comment Data Distiller et votre apprentissage automatique préféré peuvent créer des modèles de données personnalisés qui prennent en charge vos cas d’utilisation marketing avec des données Experience Platform.
