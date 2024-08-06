---
keywords: Experience Platform;accueil;rubriques les plus consultées;mapper csv;mapper le fichier csv;mapper le fichier csv à xdm;mapper csv à xdm;guide de l’interface utilisateur;mappeur;mappage;champs de mappage;fonctions de mappage
solution: Experience Platform
title: Fonctions de mappage de prép de données
description: Ce document présente les fonctions de mappage utilisées avec Data Prep.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 5a4e0b3c97d315262ded35ca5bfada3612ed6db4
workflow-type: tm+mt
source-wordcount: '5805'
ht-degree: 8%

---

# Fonctions de mappage de la préparation des données

Les fonctions de préparation de données peuvent être utilisées pour calculer les valeurs en fonction de ce qui est entré dans les champs sources.

## Champs

Un nom de champ peut être n’importe quel identifiant légal : une séquence de lettres et de chiffres Unicode à longueur illimitée, commençant par une lettre, le symbole du dollar (`$`) ou le caractère de soulignement (`_`). Les noms de variables sont également sensibles à la casse.

Si un nom de champ ne respecte pas cette convention, il doit être encapsulé avec `${}`. Ainsi, par exemple, si le nom du champ est &quot;Prénom&quot; ou &quot;Prénom&quot;, le nom doit être enveloppé comme `${First Name}` ou `${First\.Name}`, respectivement.

>[!TIP]
>
>Lors de l’interaction avec des hiérarchies, si un attribut enfant comporte un point (`.`), vous devez utiliser une barre oblique inverse (`\`) pour échapper les caractères spéciaux. Pour plus d’informations, consultez le guide sur l’ [échappement des caractères spéciaux](home.md#escape-special-characters).

Si un nom de champ est **n’importe lequel** des mots-clés réservés suivants, il doit être encapsulé avec `${}{}` :

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors, do, function, empty, size
```

En outre, les mots-clés réservés incluent également l’une des fonctions du mappeur répertoriées sur cette page.

Les données des sous-champs sont accessibles à l’aide de la notation par points. Par exemple, si un objet `name` a été présent, utilisez `name.firstName` pour accéder au champ `firstName`.

## Liste des fonctions

Les tableaux suivants répertorient toutes les fonctions de mappage prises en charge, y compris les exemples d’expressions et les sorties qui en résultent.

### Fonctions de chaîne {#string}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Concatène les chaînes données. | <ul><li>STRING : chaînes qui seront concaténées.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explode | Divise la chaîne en fonction d’un regex et renvoie un tableau de parties. Peut éventuellement inclure une expression régulière pour fractionner la chaîne. Par défaut, la division est résolue sur &quot;,&quot;. Les délimiteurs suivants **doivent** être précédés d’une séquence d’échappement avec `\` : `+, ?, ^, \|, ., [, (, {, ), *, $, \` Si vous incluez plusieurs caractères comme délimiteur, le délimiteur sera traité comme un délimiteur à plusieurs caractères. | <ul><li>STRING : **Required** Chaîne devant être partagée.</li><li>REGEX : *Optional* Expression régulière pouvant être utilisée pour fractionner la chaîne.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hi, there!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Renvoie l’emplacement/l’index d’une sous-chaîne. | <ul><li>INPUT : **Obligatoire** Chaîne recherchée.</li><li>SUBSTRING : **Required** La sous-chaîne recherchée dans la chaîne.</li><li>START_POSITION : *Facultatif* Emplacement où commencer la recherche dans la chaîne.</li><li>OCCURRENCE : *Facultatif* La nième occurrence à rechercher à partir de la position de départ. Par défaut, elle est définie sur 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| replacestr | Remplace la chaîne de recherche si elle est présente dans la chaîne d’origine. | <ul><li>INPUT : **Obligatoire** Chaîne d’entrée.</li><li>TO_FIND : **Obligatoire** Chaîne à rechercher dans l’entrée.</li><li>TO_REPLACE : **Required** Chaîne qui remplacera la valeur dans &quot;TO_FIND&quot;.</li></ul> | replacester(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;This is a string replace test&quot; |
| substr | Renvoie une sous-chaîne d’une longueur donnée. | <ul><li>INPUT : **Obligatoire** Chaîne d’entrée.</li><li>START_INDEX : **Required** Index de la chaîne d’entrée où la sous-chaîne commence.</li><li>LONGUEUR : **Obligatoire** Longueur de la sous-chaîne.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Convertit une chaîne en minuscules. | <ul><li>INPUT : **Obligatoire** Chaîne qui sera convertie en minuscules.</li></ul> | lower(INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | Convertit une chaîne en majuscules. | <ul><li>INPUT : **Obligatoire** Chaîne qui sera convertie en majuscules.</li></ul> | upper(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HELLO&quot; |
| split | Divise une chaîne d’entrée sur un séparateur. Le séparateur suivant **doit être échappé avec `\` : `\`.** Si vous incluez plusieurs délimiteurs, la chaîne sera fractionnée sur **n’importe lequel** des délimiteurs présents dans la chaîne. **Remarque :** Cette fonction renvoie uniquement des index non nuls de la chaîne, indépendamment de la présence du séparateur. Si tous les index, y compris les valeurs nulles, sont requis dans le tableau obtenu, utilisez plutôt la fonction &quot;explode&quot;. | <ul><li>INPUT : **Obligatoire** Chaîne d’entrée qui va être fractionnée.</li><li>SÉPARATEUR : **Obligatoire** Chaîne utilisée pour fractionner l’entrée.</li></ul> | split(INPUT, SEPAROR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Joint une liste d’objets à l’aide du séparateur. | <ul><li>SÉPARATEUR : **Obligatoire** Chaîne qui sera utilisée pour joindre les objets.</li><li>OBJETS : **Obligatoire** Tableau de chaînes qui seront jointes.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | Ajoute le côté gauche d’une chaîne à l’autre chaîne donnée. | <ul><li>INPUT : **Obligatoire** Chaîne qui va être complétée. Cette chaîne peut être nulle.</li><li>COUNT : **Obligatoire** Taille de la chaîne à ajouter.</li><li>PADDING : **Obligatoire** Chaîne avec laquelle remplir l’entrée. S’il est nul ou vide, il est traité comme un espace unique.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzyzybat&quot; |
| rpad | Ajoute le côté droit d’une chaîne à l’autre chaîne donnée. | <ul><li>INPUT : **Obligatoire** Chaîne qui va être complétée. Cette chaîne peut être nulle.</li><li>COUNT : **Obligatoire** Taille de la chaîne à ajouter.</li><li>PADDING : **Obligatoire** Chaîne avec laquelle remplir l’entrée. S’il est nul ou vide, il est traité comme un espace unique.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Obtient les premiers caractères &quot;n&quot; de la chaîne donnée. | <ul><li>STRING : **Required** Chaîne pour laquelle vous obtenez les premiers caractères &quot;n&quot;.</li><li>COUNT : **Obligatoire** Les n caractères que vous souhaitez obtenir de la chaîne.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Obtient les derniers caractères &quot;n&quot; de la chaîne donnée. | <ul><li>STRING : **Required** Chaîne pour laquelle vous obtenez les derniers caractères &quot;n&quot;.</li><li>COUNT : **Obligatoire** Les n caractères que vous souhaitez obtenir de la chaîne.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Supprime l’espace blanc du début de la chaîne. | <ul><li>STRING : **Required** Chaîne dont vous souhaitez supprimer l’espace blanc.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | Supprime l’espace blanc de la fin de la chaîne. | <ul><li>STRING : **Required** Chaîne dont vous souhaitez supprimer l’espace blanc.</li></ul> | rtrim(STRING) | rtrim(&quot;hello&quot;) | &quot;hello&quot; |
| trim | Supprime l’espace blanc du début et de la fin de la chaîne. | <ul><li>STRING : **Required** Chaîne dont vous souhaitez supprimer l’espace blanc.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| est égal à | Compare deux chaînes pour confirmer si elles sont égales. Cette fonction respecte la casse. | <ul><li>STRING1 : **Obligatoire** Première chaîne à comparer.</li><li>STRING2 : **Obligatoire** La deuxième chaîne que vous souhaitez comparer.</li></ul> | STRING1. &#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;est égal à &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Compare deux chaînes pour confirmer si elles sont égales. Cette fonction est **non** sensible à la casse. | <ul><li>STRING1 : **Obligatoire** Première chaîne à comparer.</li><li>STRING2 : **Obligatoire** La deuxième chaîne que vous souhaitez comparer.</li></ul> | STRING1. &#x200B;equalsIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;. &#x200B;equalsIgnoreCase &#x200B;(&quot;STRING1) | vrai |

{style="table-layout:auto"}

### Fonctions d’expressions régulières

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | Extrait les groupes de la chaîne d’entrée, en fonction d’une expression régulière. | <ul><li>STRING : **Required** Chaîne à partir de laquelle vous extrayez les groupes.</li><li>REGEX : **Obligatoire** Expression régulière que vous souhaitez que le groupe corresponde.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | Vérifie si la chaîne correspond à l’expression régulière saisie. | <ul><li>STRING : **Required** La chaîne que vous cochez correspond à l’expression régulière.</li><li>REGEX : **Obligatoire** Expression régulière par rapport à laquelle vous effectuez une comparaison.</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | vrai |

{style="table-layout:auto"}

### Fonctions de hachage {#hashing}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Prend une entrée et produit une valeur de hachage à l’aide de l’algorithme de hachage sécurisé 1 (SHA-1). | <ul><li>INPUT : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Prend une entrée et produit une valeur de hachage à l’aide de l’algorithme de hachage sécurisé 256 (SHA-256). | <ul><li>INPUT : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Prend une entrée et produit une valeur de hachage à l’aide de l’algorithme de hachage sécurisé 512 (SHA-512). | <ul><li>INPUT : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | sha512 (ENTRÉE, CHARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd00 788a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Prend une entrée et produit une valeur de hachage à l’aide de MD5. | <ul><li>INPUT : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Prend une entrée utilise un algorithme de vérification de redondance cyclique (CRC) pour produire un code cyclique 32 bits. | <ul><li>INPUT : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style="table-layout:auto"}

### Fonctions d’URL {#url}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Renvoie le protocole de l’URL donnée. Si l’entrée n’est pas valide, elle renvoie null. | <ul><li>URL : **Obligatoire** URL à partir de laquelle le protocole doit être extrait.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Renvoie l’hôte de l’URL donnée. Si l’entrée n’est pas valide, elle renvoie null. | <ul><li>URL : **Obligatoire** URL à partir de laquelle l’hôte doit être extrait.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Renvoie le port de l’URL donnée. Si l’entrée n’est pas valide, elle renvoie null. | <ul><li>URL : **Obligatoire** URL à partir de laquelle le port doit être extrait.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Renvoie le chemin d’accès de l’URL donnée. Par défaut, le chemin d’accès complet est renvoyé. | <ul><li>URL : **Obligatoire** URL à partir de laquelle le chemin d’accès doit être extrait.</li><li>FULL_PATH : *Facultatif* Une valeur booléenne qui détermine si le chemin d’accès complet est renvoyé. S’il est défini sur false, seule la fin du chemin est renvoyée.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/ &#x200B; employee.csv&quot; |
| get_url_query_str | Renvoie la chaîne de requête d’une URL donnée sous la forme d’un mappage de nom de chaîne de requête et de valeur de chaîne de requête. | <ul><li>URL : **Obligatoire** URL à partir de laquelle vous essayez d’obtenir la chaîne de requête.</li><li>ANCHOR : **Obligatoire** : détermine ce qui sera fait avec l’ancre dans la chaîne de requête. Il peut s’agir de l’une des trois valeurs suivantes : &quot;keep&quot; (conserver), &quot;remove&quot; (supprimer) ou &quot;append&quot; (ajouter).<br><br>Si la valeur est &quot;keep&quot; (conserver), l’ancre est associée à la valeur renvoyée.<br>Si la valeur est &quot;remove&quot;, l’ancre est supprimée de la valeur renvoyée.<br>Si la valeur est &quot;append&quot;, l’ancre est renvoyée sous la forme d’une valeur distincte.</li></ul> | get_url_query_str &#x200B;(URL, ANCHOR) | get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/here?name= &#x200B; furet#nose&quot;, &quot;keep&quot;)<br>get_url_query_str(&quot;foo://example.com:8042 /over/here?name=  furet#nose&quot;, &quot;remove&quot;)<br>get_url_query_str(&quot;foo://example.com :8042/over/here?name nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |
| get_url_encoded | Cette fonction utilise une URL comme entrée et remplace ou code les caractères spéciaux avec des caractères ASCII. Pour plus d’informations sur les caractères spéciaux, consultez la [liste des caractères spéciaux](#special-characters) de l’annexe de ce document. | <ul><li>URL : **Obligatoire** URL d’entrée avec des caractères spéciaux que vous souhaitez remplacer ou coder avec des caractères ASCII.</li></ul> | get_url_encoded(URL) | get_url_encoded(&quot;https</span>://example.com/partner_asia-pacifique_2022&quot;) | https%3A%2F%2Fexample.com%2Fpartner_asia-pacifique_2022 |
| get_url_décoded | Cette fonction utilise une URL comme entrée et décode les caractères ASCII en caractères spéciaux.  Pour plus d’informations sur les caractères spéciaux, consultez la [liste des caractères spéciaux](#special-characters) de l’annexe de ce document. | <ul><li>URL : **Obligatoire** L’URL d’entrée avec des caractères ASCII que vous souhaitez décoder en caractères spéciaux.</li></ul> | get_url_décoded(URL) | get_url_décoded(&quot;https%3A%2F%2Fexample.com%2Fpartner_asia-pacifique_2022&quot;) | https</span>://example.com/partner_asia-pacifique_2022 |

{style="table-layout:auto"}

### Fonctions de date et d’heure {#date-and-time}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau. Vous trouverez plus d’informations sur la fonction `date` dans la section des dates du [ guide de gestion du format de données](./data-handling.md#dates).

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Récupère l’heure actuelle. | | now() | now() | `2021-10-26T10:10:24Z` |
| timestamp | Récupère l’heure Unix actuelle. | | timestamp() | timestamp() | 1571850624571 |
| format | Formate la date d’entrée selon un format spécifié. | <ul><li>DATE : **Obligatoire** La date d’entrée, en tant qu’objet ZonedDateTime, que vous souhaitez mettre en forme.</li><li>FORMAT : **Obligatoire** Format dans lequel vous souhaitez que la date soit modifiée.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;`yyyy-MM-dd HH:mm:ss`&quot;) | `2019-10-23 11:24:35` |
| dformat | Convertit une date et une heure en chaîne de date selon un format spécifié. | <ul><li>TIMESTAMP : **Obligatoire** Horodatage que vous souhaitez mettre en forme. Il est écrit en millisecondes.</li><li>FORMAT : **Obligatoire** Format que vous souhaitez que l’horodatage devienne.</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;`yyyy-MM-dd'T'HH:mm:ss.SSSX`&quot;) | `2019-10-23T11:24:35.000Z` |
| date | Convertit une chaîne de date en objet ZonedDateTime (format ISO 8601). | <ul><li>DATE : **Obligatoire** Chaîne représentant la date.</li><li>FORMAT : **Obligatoire** Chaîne représentant le format de la date source.**Remarque :** Cela ne représente **pas** le format dans lequel vous souhaitez convertir la chaîne de date. </li><li>DEFAULT_DATE : **Required** La date par défaut renvoyée, si la date fournie est nulle.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-jj HH:mm&quot;, now()) | `2019-10-23T11:24:00Z` |
| date | Convertit une chaîne de date en objet ZonedDateTime (format ISO 8601). | <ul><li>DATE : **Obligatoire** Chaîne représentant la date.</li><li>FORMAT : **Obligatoire** Chaîne représentant le format de la date source.**Remarque :** Cela ne représente **pas** le format dans lequel vous souhaitez convertir la chaîne de date. </li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-jj HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| date | Convertit une chaîne de date en objet ZonedDateTime (format ISO 8601). | <ul><li>DATE : **Obligatoire** Chaîne représentant la date.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24:00Z&quot; |
| date_part | Récupère les parties de la date. Les valeurs de composant suivantes sont prises en charge : <br><br>&quot;year&quot;<br>&quot;yyy&quot;<br>&quot;yy&quot;<br><br>&quot;quart&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot; 3}&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;www&quot;<br>&quot;w&quot;<br><br>&quot;week-end&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br> &quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;seconde&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;milliseconde&quot;<br>&quot;SSS&quot;<br> | <ul><li>COMPOSANT : **Obligatoire** Chaîne représentant la partie de la date. </li><li>DATE : **Obligatoire** Date, dans un format standard.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;)) | 10 |
| set_date_part | Remplace un composant à une date donnée. Les composants suivants sont acceptés : <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>COMPOSANT : **Obligatoire** Chaîne représentant la partie de la date. </li><li>VALEUR : **Obligatoire** Valeur à définir pour le composant pour une date donnée.</li><li>DATE : **Obligatoire** Date, dans un format standard.</li></ul> | set_date_part &#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44Z&quot; |
| make_date_time | Crée une date à partir de parties. Cette fonction peut également être induite à l’aide de make_timestamp. | <ul><li>ANNÉE : **Obligatoire** L’année, écrite à quatre chiffres.</li><li>MOIS : **Obligatoire** Mois. Les valeurs autorisées sont comprises entre 1 et 12.</li><li>JOUR : **Obligatoire** Le jour. Les valeurs autorisées sont comprises entre 1 et 31.</li><li>HEURE : **Obligatoire** Heure. Les valeurs autorisées sont comprises entre 0 et 23.</li><li>MINUTE : **Obligatoire** La minute. Les valeurs autorisées sont comprises entre 0 et 59.</li><li>NANOSECOND : **Obligatoire** Valeurs nanosecondes. Les valeurs autorisées sont 0 à 999999999.</li><li>TIMEZONE : **Obligatoire** Fuseau horaire de la date et de l’heure.</li></ul> | make_date_time &#x200B;(ANNÉE, MOIS, JOUR, HEURE, MINUTE, SECONDE, NANOSECOND, TIMEZONE) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;Amérique/Los_Angeles&quot;) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | Convertit une date de n’importe quel fuseau horaire en date en UTC. | <ul><li>DATE : **Obligatoire** Date à laquelle vous essayez de convertir.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | Convertit une date d’un fuseau horaire en un autre. | <ul><li>DATE : **Obligatoire** Date à laquelle vous essayez de convertir.</li><li>ZONE : **Obligatoire** Fuseau horaire auquel vous essayez de convertir la date.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_zone(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style="table-layout:auto"}

### Hiérarchies - Objets {#objects}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | Vérifie si un objet est vide ou non. | <ul><li>INPUT : **Obligatoire** L’objet que vous essayez de vérifier est vide.</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | false |
| array_to_object | Crée une liste d’objets. | <ul><li>INPUT : **Obligatoire** Groupe de paires clé-tableau.</li></ul> | array_to_object(INPUT) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | Crée un objet basé sur les paires clé/valeur plate données. | <ul><li>INPUT : **Obligatoire** Une liste plate de paires clé/valeur.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Crée un objet à partir de la chaîne d’entrée. | <ul><li>STRING : **Required** Chaîne analysée pour créer un objet.</li><li>VALUE_DELIMITER : *Facultatif* Délimiteur qui sépare un champ de la valeur. Le délimiteur par défaut est `:`.</li><li>FIELD_DELIMITER : *Facultatif* Délimiteur qui sépare les paires valeur de champ. Le délimiteur par défaut est `,`.</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) **Remarque** : Vous pouvez utiliser la fonction `get()` avec `str_to_object()` pour récupérer les valeurs des clés dans la chaîne. | <ul><li>Exemple #1 : str_to_object(&quot;firstName - John ; lastName - ; - 123 345 7890&quot;, &quot;-&quot;, &quot;;&quot;)</li><li>Exemple #2 : str_to_object(&quot;firstName - John ; lastName - ; phone - 123 456 7890&quot;, &quot;-&quot;, &quot;;&quot;).get(&quot;firstName&quot;)</li></ul> | <ul><li>Exemple #1:`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>Exemple #2 : &quot;John&quot;</li></ul> |
| contains_key | Vérifie si l’objet existe dans les données source. **Remarque :** Cette fonction remplace la fonction `is_set()` obsolète. | <ul><li>INPUT : **Obligatoire** Chemin à vérifier s’il existe dans les données source.</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | vrai |
| nullify | Définit la valeur de l’attribut sur `null`. Vous devez l’utiliser lorsque vous ne souhaitez pas copier le champ dans le schéma cible. | | nullify() | nullify() | `null` |
| get_keys | Analyse les paires clé/valeur et renvoie toutes les clés. | <ul><li>OBJET : **Obligatoire** Objet duquel les clés seront extraites.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;: &quot;Pride and Prejudices&quot;, &quot;book2&quot;: &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | Analyse les paires clé/valeur et renvoie la valeur de la chaîne, en fonction de la clé donnée. | <ul><li>STRING : **Required** Chaîne que vous souhaitez analyser.</li><li>KEY : **Obligatoire** Clé pour laquelle la valeur doit être extraite.</li><li>VALUE_DELIMITER : **Required** Délimiteur qui sépare le champ et la valeur. Si une chaîne `null` ou vide est fournie, cette valeur est `:`.</li><li>FIELD_DELIMITER : *Facultatif* Délimiteur qui sépare les paires champ/valeur. Si une chaîne `null` ou vide est fournie, cette valeur est `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena , phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | John |
| map_get_values | Prend une carte et une entrée clé. Si l’entrée est une clé unique, la fonction renvoie la valeur associée à cette clé. Si l’entrée est un tableau de chaîne, la fonction renvoie toutes les valeurs correspondant aux clés fournies. Si la carte entrante comporte des clés en double, la valeur renvoyée doit dédupliquer les clés et renvoyer des valeurs uniques. | <ul><li>MAP : **Obligatoire** Données de mappage d’entrée.</li><li>CLÉ : **Obligatoire** La clé peut être une chaîne unique ou un tableau de chaîne. Si un autre type primitif (données/nombre) est fourni, il est traité comme une chaîne.</li></ul> | get_values(MAP, KEY) | Consultez l’ [annexe](#map_get_values) pour obtenir un exemple de code. | |
| map_has_keys | Si une ou plusieurs clés d’entrée sont fournies, la fonction renvoie true (vrai). Si un tableau de chaîne est fourni comme entrée, la fonction renvoie true (vrai) sur la première clé trouvée. | <ul><li>MAP : **Obligatoire** Les données de carte d’entrée</li><li>CLÉ : **Obligatoire** La clé peut être une chaîne unique ou un tableau de chaîne. Si un autre type primitif (données/nombre) est fourni, il est traité comme une chaîne.</li></ul> | map_has_keys(MAP, KEY) | Consultez l’ [annexe](#map_has_keys) pour obtenir un exemple de code. | |
| add_to_map | Accepte au moins deux entrées. Tout nombre de cartes peut être fourni en tant qu’entrées. La préparation de données renvoie une carte unique qui contient toutes les paires clé-valeur de toutes les entrées. Si une ou plusieurs clés sont répétées (dans la même carte ou sur plusieurs cartes), la préparation de données déduplique les clés afin que la première paire clé-valeur persiste dans l’ordre dans lequel elles ont été transmises dans l’entrée. | MAP : **Obligatoire** Données de mappage d’entrée. | add_to_map(MAP 1, MAP 2, MAP 3, etc.) | Consultez l’ [annexe](#add_to_map) pour obtenir un exemple de code. | |
| object_to_map (Syntaxe 1) | Utilisez cette fonction pour créer des types de données de carte. | <ul><li>CLÉ : **Obligatoire** Les clés doivent être une chaîne. Si d’autres valeurs primitives, telles que des nombres entiers ou des dates, sont fournies, elles sont automatiquement converties en chaînes et sont traitées comme des chaînes.</li><li>ANY_TYPE : **Obligatoire** Fait référence à tout type de données XDM pris en charge, à l’exception des cartes.</li></ul> | object_to_map(KEY, ANY_TYPE, KEY, ANY_TYPE, etc.) | Consultez l’ [annexe](#object_to_map) pour obtenir un exemple de code. | |
| object_to_map (Syntaxe 2) | Utilisez cette fonction pour créer des types de données de carte. | <ul><li>OBJET : **Obligatoire** Vous pouvez fournir un objet ou un tableau d’objets entrant et pointer vers un attribut à l’intérieur de l’objet comme clé.</li></ul> | object_to_map(OBJECT) | Consultez l’ [annexe](#object_to_map) pour obtenir un exemple de code. |
| object_to_map (Syntaxe 3) | Utilisez cette fonction pour créer des types de données de carte. | <ul><li>OBJET : **Obligatoire** Vous pouvez fournir un objet ou un tableau d’objets entrant et pointer vers un attribut à l’intérieur de l’objet comme clé.</li></ul> | object_to_map(OBJECT_ARRAY, ATTRIBUTE_IN_OBJECT_TO_BE_USED_AS_A_KEY) | Consultez l’ [annexe](#object_to_map) pour obtenir un exemple de code. |

{style="table-layout:auto"}

Pour plus d’informations sur la fonctionnalité de copie d’objet, reportez-vous à la section [ci-dessous](#object-copy).

### Hiérarchies - Tableaux {#arrays}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| coalesce | Renvoie le premier objet non nul d’un tableau donné. | <ul><li>INPUT : **Obligatoire** Tableau dont vous souhaitez trouver le premier objet non nul.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | Récupère le premier élément du tableau donné. | <ul><li>INPUT : **Obligatoire** Tableau dont vous souhaitez trouver le premier élément.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Récupère le dernier élément du tableau donné. | <ul><li>INPUT : **Obligatoire** Tableau dont vous souhaitez trouver le dernier élément.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | Ajoute des éléments à la fin du tableau. | <ul><li>ARRAY : **Obligatoire** Tableau auquel vous ajoutez des éléments.</li><li>VALEURS : éléments que vous souhaitez ajouter au tableau.</li></ul> | add_to_array &#x200B;(ARRAY, VALUES) | add_to_array &#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_arrays | Combine les tableaux les uns avec les autres. | <ul><li>ARRAY : **Obligatoire** Tableau auquel vous ajoutez des éléments.</li><li>VALEURS : tableau(s) que vous souhaitez ajouter au tableau parent.</li></ul> | join_arrays &#x200B;(ARRAY, VALES) | join_arrays &#x200B;([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [&#39;d&#39;, &#39;e&#39;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | Prend une liste d’entrées et la convertit en tableau. | <ul><li>INCLUDE_NULLS : **Required** Une valeur booléenne pour indiquer s’il faut inclure ou non des valeurs nulles dans le tableau de réponse.</li><li>VALEURS : **Obligatoire** Les éléments à convertir en tableau.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | Renvoie la taille de l’entrée. | <ul><li>INPUT : **Obligatoire** Objet dont vous essayez de trouver la taille.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | Cette fonction est utilisée pour ajouter tous les éléments du tableau d’entrée entier à la fin du tableau dans Profile. Cette fonction est **uniquement** applicable lors des mises à jour. Si elle est utilisée dans le contexte d’insertions, cette fonction renvoie l’entrée telle quelle. | <ul><li>ARRAY : **Obligatoire** Tableau à ajouter au tableau dans le profil.</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123, 456] |
| upsert_array_replace | Cette fonction est utilisée pour remplacer des éléments d’un tableau. Cette fonction est **uniquement** applicable lors des mises à jour. Si elle est utilisée dans le contexte d’insertions, cette fonction renvoie l’entrée telle quelle. | <ul><li>ARRAY : **Obligatoire** Le tableau pour remplacer le tableau dans le profil.</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123, 456] |

{style="table-layout:auto"}

### Hiérarchies - Carte {#map}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| array_to_map | Cette fonction prend un tableau d’objets et une clé comme entrée et renvoie un mappage du champ de la clé avec la valeur comme clé et l’élément de tableau comme valeur. | <ul><li>INPUT : **Obligatoire** Le tableau d’objets dont vous souhaitez trouver le premier objet non nul.</li><li>CLÉ : **Obligatoire** La clé doit être un nom de champ dans le tableau d’objets et l’objet comme valeur.</li></ul> | array_to_map(OBJECT[] INPUTS, KEY) | Lisez l’ [annexe](#object_to_map) pour un exemple de code. |
| object_to_map | Cette fonction prend un objet comme argument et renvoie une carte de paires clé-valeur. | <ul><li>INPUT : **Obligatoire** Le tableau d’objets dont vous souhaitez trouver le premier objet non nul.</li></ul> | object_to_map(OBJECT_INPUT) | &quot;object_to_map(address) où l’entrée est &quot; + &quot;address: {line1 : \&quot;345 park ave\&quot;,line2: \&quot;bldg 2\&quot;,Ville : \&quot;san jose\&quot;,État : \&quot;CA\&quot;,type : \&quot;office\&quot;}&quot; | Renvoie une map avec des paires nom-valeur de champ données ou valeur nulle si l’entrée est nulle. Par exemple : `"{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"` |
| to_map | Cette fonction prend une liste de paires clé-valeur et renvoie un mappage de paires clé-valeur. | | to_map(OBJECT_INPUT) | &quot;to_map(\&quot;firstName\&quot;, \&quot;John\&quot;, \&quot;lastName\&quot;, \&quot;Doe\&quot;)&quot; | Renvoie une map avec des paires nom-valeur de champ données ou valeur nulle si l’entrée est nulle. Par exemple : `"{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"` |

{style="table-layout:auto"}

### Opérateurs logiques {#logical-operators}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decode | Étant donné qu’une clé et une liste de paires clé-valeur sont aplaties dans un tableau, la fonction renvoie la valeur si la clé est trouvée ou renvoie une valeur par défaut si elle est présente dans le tableau. | <ul><li>CLÉ : **Obligatoire** Clé à associer.</li><li>OPTIONS : **Obligatoire** Un tableau aplati de paires clé/valeur. Vous pouvez éventuellement placer une valeur par défaut à la fin.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Si le code d’état donné est &quot;ca&quot;, &quot;California&quot;.<br>Si le code d&#39;état donné est &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Si stateCode ne correspond pas à ce qui suit, &quot;S.O.&quot; |
| iif | Évalue une expression booléenne donnée et renvoie la valeur spécifiée en fonction du résultat. | <ul><li>EXPRESSION : **Obligatoire** Expression booléenne en cours d’évaluation.</li><li>TRUE_VALUE : **Required** La valeur renvoyée si l’expression renvoie true (vrai).</li><li>FALSE_VALUE : **Required** La valeur renvoyée si l’expression est évaluée comme false.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style="table-layout:auto"}

### Agrégation {#aggregation}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Renvoie le minimum des arguments donnés. Utilise l’ordre naturel. | <ul><li>OPTIONS : **Obligatoire** Un ou plusieurs objets pouvant être comparés les uns aux autres.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Renvoie le maximum des arguments donnés. Utilise l’ordre naturel. | <ul><li>OPTIONS : **Obligatoire** Un ou plusieurs objets pouvant être comparés les uns aux autres.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style="table-layout:auto"}

### Conversions de type {#type-conversions}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Convertit une chaîne en BigInteger. | <ul><li>STRING : **Required** Chaîne à convertir en BigInteger.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;1000000.34&quot;) | 1000000,34 |
| to_decimal | Convertit une chaîne en double. | <ul><li>STRING : **Required** Chaîne à convertir en double.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Convertit une chaîne en chaîne flottante. | <ul><li>STRING : **Required** Chaîne à convertir en flottante.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_integer | Convertit une chaîne en entier. | <ul><li>STRING : **Required** Chaîne à convertir en entier.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style="table-layout:auto"}

### Fonctions JSON {#json}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Désérialisez le contenu JSON à partir de la chaîne donnée. | <ul><li>STRING : **Required** Chaîne JSON à désérialiser.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;: &quot;Doe&quot;}) | Objet représentant le fichier JSON. |

{style="table-layout:auto"}

### Opérations spéciales {#special-operations}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | Génère un identifiant pseudo-aléatoire. | | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fcda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |
| `fpid_to_ecid ` | Cette fonction prend une chaîne FPID et la convertit en ECID à utiliser dans les applications Adobe Experience Platform et Adobe Experience Cloud. | <ul><li>STRING : **Required** Chaîne FPID à convertir en ECID.</li></ul> | `fpid_to_ecid(STRING)` | `fpid_to_ecid("4ed70bee-b654-420a-a3fd-b58b6b65e991")` | `"28880788470263023831040523038280731744"` |

{style="table-layout:auto"}

### Fonctions de l’agent utilisateur {#user-agent}

Toutes les fonctions de l’agent utilisateur contenues dans le tableau ci-dessous peuvent renvoyer l’une des valeurs suivantes :

* Phone : appareil mobile avec un petit écran (généralement &lt; 7&quot;).
* Mobile : périphérique mobile qui n’est pas encore identifié. Ce périphérique mobile peut être un lecteur électronique, une tablette, un téléphone, une montre, etc.

Pour plus d’informations sur les valeurs de champ de périphérique, consultez la [liste des valeurs de champ de périphérique](#device-field-values) de l’annexe de ce document.

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Extrait le nom du système d’exploitation de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extrait la version principale du système d’exploitation de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | IOS 5 |
| ua_os_version | Extrait la version du système d’exploitation de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Extrait le nom et la version du système d’exploitation de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extrait la version de l’agent de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5,1 |
| ua_agent_version_major | Extrait le nom de l’agent et la version majeure de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extrait le nom de l’agent de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extrait la classe device de la chaîne user agent. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Téléphone |

{style="table-layout:auto"}

### Fonctions Analytics {#analytics}

>[!NOTE]
>
>Vous ne pouvez utiliser que les fonctions d’analyse suivantes pour les flux WebSDK et Adobe Analytics.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| aa_get_event_id | Extrait l’ID d’événement d’une chaîne d’événement Analytics. | <ul><li>EVENT_STRING : **Required** Chaîne d’événement Analytics séparée par des virgules.</li><li>EVENT_NAME : **Required** Nom de l’événement à partir duquel extraire et ID.</li></ul> | aa_get_event_id(EVENT_STRING, EVENT_NAME) | aa_get_event_id(&quot;event101=5:123456,scOpen&quot;, &quot;event101&quot;) | 123456 |
| aa_get_event_value | Extrait la valeur d’événement d’une chaîne d’événement Analytics. Si la valeur de l’événement n’est pas spécifiée, 1 est renvoyé. | <ul><li>EVENT_STRING : **Required** Chaîne d’événement Analytics séparée par des virgules.</li><li>EVENT_NAME : **Required** Nom de l’événement duquel extraire une valeur.</li></ul> | aa_get_event_value(EVENT_STRING, EVENT_NAME) | aa_get_event_value(&quot;event101=5:123456,scOpen&quot;, &quot;event101&quot;) | 5 |
| aa_get_product_categories | Extrait la catégorie de produits d’une chaîne de produits Analytics. | <ul><li>PRODUCTS_STRING : **Obligatoire** Chaîne de produits Analytics.</li></ul> | aa_get_product_categories(PRODUCTS_STRING) | aa_get_product_categories(&quot;;Exemple de produit 1;1;3.50,Exemple de catégorie 2;Exemple de produit 2;1;5.99&quot;) | [null,&quot;Exemple de catégorie 2&quot;] |
| aa_get_product_names | Extrait le nom du produit d’une chaîne de produits Analytics. | <ul><li>PRODUCTS_STRING : **Obligatoire** Chaîne de produits Analytics.</li></ul> | aa_get_product_names(PRODUCTS_STRING) | aa_get_product_names(&quot;;Exemple de produit 1;1;3.50,Exemple de catégorie 2;Exemple de produit 2;1;5.99&quot;) | [&quot;Exemple de produit 1&quot;,&quot;Exemple de produit 2&quot;] |
| aa_get_product_quantités | Extrait les quantités d’une chaîne de produits Analytics. | <ul><li>PRODUCTS_STRING : **Obligatoire** Chaîne de produits Analytics.</li></ul> | aa_get_product_grandeurs(PRODUCTS_STRING) | aa_get_product_quantités(&quot;;Exemple de produit 1;1;3.50,Exemple de catégorie 2;Exemple de produit 2&quot;) | [&quot;1&quot;, null] |
| aa_get_product_prix | Extrait le prix d’une chaîne de produits Analytics. | <ul><li>PRODUCTS_STRING : **Obligatoire** Chaîne de produits Analytics.</li></ul> | aa_get_product_prix(PRODUCTS_STRING) | aa_get_product_price(&quot;;Exemple de produit 1;1;3.50,Exemple de catégorie 2;Exemple de produit 2&quot;) | [&quot;3.50&quot;, null] |
| aa_get_product_event_values | Extrait les valeurs de l’événement nommé de la chaîne products sous la forme d’un tableau de chaînes. | <ul><li>PRODUCTS_STRING : **Obligatoire** Chaîne de produits Analytics.</li><li>EVENT_NAME : **Required** Nom de l’événement duquel extraire des valeurs.</li></ul> | aa_get_product_event_values(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_values(&quot;;Exemple produit 1;1;4.20;event1=2.3\|event2=5:1,;Exemple produit 2;1;4.20;event1=3\|event2=2:2&quot;, &quot;event1&quot;) | [&quot;2.3&quot;, &quot;3&quot;] |
| aa_get_product_evars | Extrait les valeurs evar de l’événement nommé de la chaîne products sous la forme d’un tableau de chaînes. | <ul><li>PRODUCTS_STRING : **Obligatoire** Chaîne de produits Analytics.</li><li>EVAR_NAME : **Obligatoire** Nom de l’eVar à extraire.</li></ul> | aa_get_product_evars(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_evars(&quot;;Exemple de produit;1;6.69;;eVar1=Valeur de marchandisage&quot;, &quot;eVar1&quot;) | [&quot;Valeur de marchandisage&quot;] |

{style="table-layout:auto"}

<!-- | aa_get_product_events | Extracts a named event from the products string as an array of objects. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_events(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_events(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | [`{"id": "1","value", "5"}`, `{"id": "2","value", "1"}`] |
| aa_get_product_event_ids | Extracts the IDs for the named event from the products string as an array of strings. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_event_ids(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_ids(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | ["1", "2"] | -->

### Copie d’objet {#object-copy}

>[!TIP]
>
>La fonction de copie d’objet est automatiquement appliquée lorsqu’un objet de la source est mappé à un objet dans XDM. Aucune action supplémentaire n’est nécessaire de la part des utilisateurs.

Vous pouvez utiliser la fonction de copie d’objet pour copier automatiquement les attributs d’un objet sans apporter de modifications au mappage. Par exemple, si vos données source ont une structure de :

```json
address{
        line1: 4191 Ridgebrook Way,
        city: San Jose,
        state: California
        }
```

et une structure XDM de :

```json
addr{
    addrLine1: 4191 Ridgebrook Way,
    city: San Jose,
    state: California
    }
```

Ensuite, le mappage devient :

```json
address -> addr
address.line1 -> addr.addrLine1
```

Dans l’exemple ci-dessus, les attributs `city` et `state` sont également ingérés automatiquement au moment de l’exécution car l’objet `address` est mappé sur `addr`. Si vous deviez créer un attribut `line2` dans la structure XDM et que vos données d’entrée contiennent également un `line2` dans l’objet `address`, il sera également ingéré automatiquement sans avoir à modifier manuellement le mappage.

Pour que le mappage automatique fonctionne, les conditions préalables suivantes doivent être remplies :

* Les objets de niveau parent doivent être mappés ;
* De nouveaux attributs doivent avoir été créés dans le schéma XDM ;
* Les nouveaux attributs doivent avoir des noms correspondants dans le schéma source et le schéma XDM.

Si aucune des conditions préalables n’est remplie, vous devez mapper manuellement le schéma source au schéma XDM à l’aide de la préparation des données.

## Annexe

Vous trouverez ci-dessous des informations supplémentaires sur l’utilisation des fonctions de mappage de la préparation de données

### Caractères spéciaux {#special-characters}

Le tableau ci-dessous présente une liste de caractères réservés et les caractères codés correspondants.

| Caractère réservé | Caractère codé |
| --- | --- |
| space | %20 |
| ! | %21 |
| &quot; | %22 |
| # | %23 |
| $ | %24 |
| % | %25 |
| &amp; | %26 |
| &#39; | %27 |
| ( | %28 |
| ) | %29 |
| * | %2A |
| + | %2B |
| , | %2C |
| / | %2F |
| : | %3A |
|   | %3B |
| &lt; | %3C |
| = | %3D |
| > | %3E |
| ? | %3F |
| @ | %40 |
| [ | %5B |
| | | %5C |
| ] | %5D |
| ^ | %5E |
| ` | %60 |
| ~ | %7E |

{style="table-layout:auto"}

### Valeurs de champ du périphérique {#device-field-values}

Le tableau ci-dessous présente une liste des valeurs de champ d’appareil et leurs descriptions correspondantes.

| Appareil | Description |
| --- | --- |
| Bureau | Un ordinateur de bureau ou un ordinateur portable de type appareil. |
| Anonymisé | Un appareil anonyme. Dans certains cas, il s’agit de `useragents` qui ont été modifiés par un logiciel d’anonymisation. |
| Inconnu | Un appareil inconnu. Il s’agit généralement de `useragents` qui ne contiennent aucune information sur l’appareil. |
| Mobile | Appareil mobile qui n’est pas encore identifié. Ce périphérique mobile peut être un lecteur électronique, une tablette, un téléphone, une montre, etc. |
| Tablette | Appareil mobile avec un grand écran (généralement > 7 pouces). |
| Téléphone | Appareil mobile avec un petit écran (généralement &lt; 7 pouces). |
| Regarder | Un appareil mobile avec un petit écran (généralement &lt; 2&quot;). Ces appareils fonctionnent normalement comme un écran supplémentaire pour un type de téléphone/tablette. |
| La réalité augmentée | Un appareil mobile avec des fonctionnalités de AR. |
| La réalité virtuelle | Un appareil mobile avec des fonctionnalités de réalité virtuelle. |
| eReader | Appareil similaire à une tablette, mais généralement avec un écran [!DNL eInk]. |
| Cadre de configuration | Appareil connecté qui permet l’interaction par le biais d’un écran de la taille d’une télévision. |
| TV | Un appareil semblable à la visionneuse, mais intégré à la télévision. |
| Approvisionnement maison | Un appareil domestique (généralement grand), comme un réfrigérateur. |
| Console de jeu | Un système de jeu fixe tel que [!DNL Playstation] ou [!DNL XBox]. |
| Console de jeu pour portables | Un système de jeu mobile comme un [!DNL Nintendo Switch]. |
| Voix | Un appareil piloté par la voix tel qu’un [!DNL Amazon Alexa] ou un [!DNL Google Home]. |
| Voiture | Navigateur basé sur un véhicule. |
| Robot | Des robots qui visitent un site web. |
| Robot Mobile | Robots qui visitent un site web mais qui indiquent qu’ils souhaitent être vus comme un visiteur mobile. |
| Robot Imitator | Des robots qui visitent un site web, prétendant être des robots comme [!DNL Google], mais ce n&#39;est pas le cas. **Remarque** : Dans la plupart des cas, les simulateurs de robots sont effectivement des robots. |
| Cloud | Une application cloud. Ce ne sont ni des robots ni des hackers, mais des applications qui doivent se connecter. Cela inclut les serveurs [!DNL Mastodon]. |
| Hacker | Cette valeur device est utilisée au cas où un script serait détecté dans la chaîne `useragent`. |

{style="table-layout:auto"}

### Exemples de code {#code-samples}

#### map_get_values {#map-get-values}

+++Sélectionner pour afficher l’exemple

```json
 example = "map_get_values(book_details,\"author\") where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "{\"author\": \"George R. R. Martin\"}"
```

+++

#### map_has_keys {#map_has_keys}

+++Sélectionner pour afficher l’exemple

```json
 example = "map_has_keys(book_details,\"author\")where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "true"
```

+++

#### add_to_map {#add_to_map}

+++Sélectionner pour afficher l’exemple

```json
example = "add_to_map(book_details, book_details2) where input is {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}" +
        "{\n" +
        "    \"book_details2\":\n" +
        "    {\n" +
        "        \"author\": \"Neil Gaiman\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-0-380-97365-0\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      result = "{\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      returns = "A new map with all elements from map and addends"
```

+++

#### object_to_map {#object_to_map}

**Syntaxe 1**

+++Sélectionner pour afficher l’exemple

```json
example = "object_to_map(\"firstName\", \"John\", \"lastName\", \"Doe\")",
result = "{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"
```

+++

**Syntaxe 2**

+++Sélectionner pour afficher l’exemple

```json
example = "object_to_map(address) where input is " +
  "address: {line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}",
result = "{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"
```

+++

**Syntaxe 3**

+++Sélectionner pour afficher l’exemple

```json
example = "object_to_map(addresses,type)" +
        "\n" +
        "[\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "]" ,
result = "{\n" +
        "    \"home\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    \"work\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    \"office\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "}" 
```

+++

#### array_to_map {#array_to_map}

+++Sélectionner pour afficher l’exemple

```json
example = "array_to_map(addresses, \"type\") where addresses is\n" +
  "\n" +
  "[\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "]" ,
result = "{\n" +
  "    \"home\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    \"work\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    \"office\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "}",
returns = "Returns a map with given field name and value pairs or null if input is null"
```

+++

