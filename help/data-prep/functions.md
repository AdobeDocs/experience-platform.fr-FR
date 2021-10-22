---
keywords: Experience Platform ; accueil ; rubriques populaires ; mapper csv ; mapper le fichier csv ; mapper le fichier csv à xdm ; mapper csv à xdm ; guide d'interface utilisateur ; mappeur ; mappage ; champs de mappage ; fonctions de mappage ;
solution: Experience Platform
title: Fonctions de mappage des préférences de données
topic-legacy: overview
description: Ce document présente les fonctions de mappage utilisées avec Data Prep.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 41d6374e69899108c5323df667272f8df14c3389
workflow-type: tm+mt
source-wordcount: '3970'
ht-degree: 17%

---

# Fonctions de mappage de Data Prep

Les fonctions de préparation de données peuvent être utilisées pour calculer et calculer des valeurs en fonction de ce qui est entré dans les champs source.

## Champs

Un nom de champ peut être n’importe quel identificateur légal : une séquence illimitée de lettres et de chiffres Unicode, commençant par une lettre, le signe dollar (`$`), ou le caractère de soulignement (`_`). Les noms de variables sont également sensibles à la casse.

Si un nom de champ ne suit pas cette convention, le nom de champ doit être enveloppé avec `${}`. Par exemple, si le nom du champ est &quot;Prénom&quot; ou &quot;Prénom.Nom&quot;, le nom doit être enveloppé comme `${First Name}` ou `${First.Name}` respectivement.

En outre, si un nom de champ est **quelconque** parmi les mots-clés réservés suivants, il doit être entouré de `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

Les données des sous-champs sont accessibles à l’aide de la notation par point. Par exemple, s’il y avait un `name` pour accéder à l’objet `firstName` champ, utiliser `name.firstName`.

## Liste des fonctions

Les tableaux suivants répertorient toutes les fonctions de mappage prises en charge, y compris les exemples d’expressions et leurs sorties résultantes.

### Fonctions de chaîne {#string}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Concatène les chaînes données. | <ul><li>CHAÎNE : Les chaînes qui seront concaténées.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explode | Divise la chaîne sur base d’un regex et renvoie un tableau de parties. Peut éventuellement inclure regex pour fractionner la chaîne. Par défaut, la division prend la valeur &quot;,&quot;. Délimiteurs suivants **besoin** à échapper par `\`: `+, ?, ^, |, ., [, (, {, ), *, $, \` Si vous incluez plusieurs caractères comme délimiteur, le délimiteur sera traité comme délimiteur à plusieurs caractères. | <ul><li>CHAÎNE : **Obligatoire** Chaîne à fractionner.</li><li>REGEX : *Facultatif* Expression régulière pouvant être utilisée pour fractionner la chaîne.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hi, there!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Renvoie l’emplacement/l’index d’une sous-chaîne. | <ul><li>ENTRÉE : **Obligatoire** Chaîne en cours de recherche.</li><li>SOUS-CHAÎNE : **Obligatoire** La sous-chaîne recherchée dans la chaîne.</li><li>START_POSITION : *Facultatif* Emplacement où commencer à chercher dans la chaîne.</li><li>OCCURRENCE : *Facultatif* La neuvième occurrence à rechercher à partir de la position de départ. Par défaut, elle est définie sur 1. </li></ul> | (INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | (&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| replacestr | Remplace la chaîne de recherche si elle est présente dans la chaîne d’origine. | <ul><li>ENTRÉE : **Obligatoire** Chaîne d’entrée.</li><li>TO_FIND : **Obligatoire** Chaîne à rechercher dans l’entrée.</li><li>TO_REPLACE : **Obligatoire** Chaîne qui remplacera la valeur dans &quot;TO_FIND&quot;.</li></ul> | replacestr(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;This is a string replace test&quot; |
| substr | Renvoie une sous-chaîne d’une longueur donnée. | <ul><li>ENTRÉE : **Obligatoire** Chaîne d’entrée.</li><li>START_INDEX : **Obligatoire** Index de la chaîne d&#39;entrée où commence la sous-chaîne.</li><li>LONGUEUR : **Obligatoire** Longueur de la sous-chaîne.</li></ul> | ◘(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Convertit une chaîne en minuscules. | <ul><li>ENTRÉE : **Obligatoire** Chaîne qui sera convertie en minuscules.</li></ul> | lower(INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | Convertit une chaîne en majuscules. | <ul><li>ENTRÉE : **Obligatoire** Chaîne qui sera convertie en majuscules.</li></ul> | high(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HELLO&quot; |
| split | Divise une chaîne d’entrée sur un séparateur. Le séparateur suivant **besoins** à échapper par `\`: `\`. Si vous incluez plusieurs délimiteurs, la chaîne sera scindée sur **quelconque** des délimiteurs présents dans la chaîne. | <ul><li>ENTRÉE : **Obligatoire** Chaîne d&#39;entrée qui va être fractionnée.</li><li>SÉPARATEUR : **Obligatoire** Chaîne utilisée pour fractionner l’entrée.</li></ul> | split (ENTRÉE, SÉPARATEUR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Joint une liste d’objets à l’aide du séparateur. | <ul><li>SÉPARATEUR : **Obligatoire** Chaîne qui sera utilisée pour joindre les objets.</li><li>OBJETS : **Obligatoire** Tableau de chaînes qui seront jointes.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | Fait glisser le côté gauche d’une chaîne avec l’autre chaîne donnée. | <ul><li>ENTRÉE : **Obligatoire** La chaîne qui va être ajoutée. Cette chaîne peut être null.</li><li>COMPTE : **Obligatoire** Taille de la chaîne à ajouter.</li><li>PADDING : **Obligatoire** Chaîne avec laquelle ajouter l’entrée. Si elle est nulle ou vide, elle sera traitée comme un espace unique.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| rpad | Applique le côté droit d’une chaîne à l’autre chaîne donnée. | <ul><li>ENTRÉE : **Obligatoire** La chaîne qui va être ajoutée. Cette chaîne peut être null.</li><li>COMPTE : **Obligatoire** Taille de la chaîne à ajouter.</li><li>PADDING : **Obligatoire** Chaîne avec laquelle ajouter l’entrée. Si elle est nulle ou vide, elle sera traitée comme un espace unique.</li></ul> | rpad(ENTRÉE, COMPTE, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Obtient les premiers caractères &quot;n&quot; de la chaîne donnée. | <ul><li>CHAÎNE : **Obligatoire** Chaîne pour laquelle vous obtenez les premiers caractères &quot;n&quot;.</li><li>COMPTE : **Obligatoire** Les caractères &quot;n&quot; que vous voulez obtenir de la chaîne.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| droit | Obtient les derniers caractères &quot;n&quot; de la chaîne donnée. | <ul><li>CHAÎNE : **Obligatoire** Chaîne pour laquelle vous obtenez les derniers caractères &quot;n&quot;.</li><li>COMPTE : **Obligatoire** Les caractères &quot;n&quot; que vous voulez obtenir de la chaîne.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Supprime l’espace blanc du début de la chaîne. | <ul><li>CHAÎNE : **Obligatoire** Chaîne dont vous souhaitez supprimer l’espace blanc.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;bonjour&quot; |
| rtrim | Supprime l’espace blanc de la fin de la chaîne. | <ul><li>CHAÎNE : **Obligatoire** Chaîne dont vous souhaitez supprimer l’espace blanc.</li></ul> | rtrim(STRING) | rtrim(&quot;hello&quot;) | &quot;bonjour&quot; |
| trim | Supprime l’espace blanc du début et de la fin de la chaîne. | <ul><li>CHAÎNE : **Obligatoire** Chaîne dont vous souhaitez supprimer l’espace blanc.</li></ul> | trim(STRING) | trim(&quot; bonjour &quot;) | &quot;bonjour&quot; |
| est égal à | Compare deux chaînes pour vérifier si elles sont égales. Cette fonction respecte la casse. | <ul><li>STRING1 : **Obligatoire** La première chaîne à comparer.</li><li>STRING2 : **Obligatoire** La deuxième chaîne à comparer.</li></ul> | STRING1. &#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;est égal à &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Compare deux chaînes pour vérifier si elles sont égales. Cette fonction est **non** sensible à la casse. | <ul><li>STRING1 : **Obligatoire** La première chaîne à comparer.</li><li>STRING2 : **Obligatoire** La deuxième chaîne à comparer.</li></ul> | STRING1. &#x200B;equalsIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;. &#x200B;equalsIgnoreCase &#x200B;(&quot;STRING1&quot;) | vrai |

{style=&quot;table-layout:auto&quot;}

### Fonctions d’expressions régulières

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | Extrait les groupes de la chaîne d’entrée, en fonction d’une expression régulière. | <ul><li>CHAÎNE : **Obligatoire** Chaîne à partir de laquelle vous extrayez les groupes.</li><li>REGEX : **Obligatoire** L’expression régulière à laquelle le groupe doit correspondre.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| match_regex | Vérifie si la chaîne correspond à l’expression régulière saisie. | <ul><li>CHAÎNE : **Obligatoire** La chaîne que vous vérifiez correspond à l’expression régulière.</li><li>REGEX : **Obligatoire** Expression régulière par rapport à laquelle vous comparez.</li></ul> | match_regex(STRING, REGEX) | match_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | vrai |

{style=&quot;table-layout:auto&quot;}

### Fonctions de hachage {#hashing}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Prend une entrée et produit une valeur de hachage à l’aide de l’algorithme de hachage sécurisé 1 (SHA-1). | <ul><li>ENTRÉE : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Prend une entrée et produit une valeur de hachage à l’aide de l’algorithme de hachage sécurisé 256 (SHA-256). | <ul><li>ENTRÉE : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | sha256(ENTRÉE, CHARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Prend une entrée et produit une valeur de hachage à l’aide de l’algorithme de hachage sécurisé 512 (SHA-512). | <ul><li>ENTRÉE : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | sha512(ENTRÉE, CHARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd00 788a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Prend une entrée et produit une valeur de hachage à l’aide de MD5. | <ul><li>ENTRÉE : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Prend une entrée utilise un algorithme de contrôle de redondance cyclique (CRC) pour produire un code cyclique 32 bits. | <ul><li>ENTRÉE : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | crc32(ENTRÉE, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style=&quot;table-layout:auto&quot;}

### Fonctions URL {#url}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Renvoie le protocole à partir de l&#39;URL donnée. Si l’entrée n’est pas valide, elle renvoie la valeur Null. | <ul><li>URL : **Obligatoire** URL à partir de laquelle le protocole doit être extrait.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Renvoie l&#39;hôte de l&#39;URL donnée. Si l’entrée n’est pas valide, elle renvoie la valeur Null. | <ul><li>URL : **Obligatoire** URL à partir de laquelle l&#39;hôte doit être extrait.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Renvoie le port de l&#39;URL donnée. Si l’entrée n’est pas valide, elle renvoie la valeur Null. | <ul><li>URL : **Obligatoire** URL à partir de laquelle le port doit être extrait.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Renvoie le chemin d’accès de l’URL donnée. Par défaut, le chemin d’accès complet est renvoyé. | <ul><li>URL : **Obligatoire** URL à partir de laquelle le chemin d’accès doit être extrait.</li><li>FULL_PATH : *Facultatif* Valeur booléenne qui détermine si le chemin complet est renvoyé. Si la valeur est false, seule la fin du tracé est renvoyée.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/ &#x200B; employee.csv&quot; |
| get_url_query_str | Renvoie la chaîne de requête d&#39;une URL donnée. | <ul><li>URL : **Obligatoire** URL à partir de laquelle vous tentez d&#39;obtenir la chaîne de requête.</li><li>ANCRAGE : **Obligatoire** Détermine ce qui sera fait avec l&#39;ancre dans la chaîne de requête. Il peut s’agir de l’une des trois valeurs suivantes : &quot;preserve&quot;, &quot;remove&quot; ou &quot;append&quot;.<br><br>Si la valeur est &quot;conserver&quot;, l’ancre est attachée à la valeur renvoyée.<br>Si la valeur est &quot;remove&quot;, l’ancrage sera supprimé de la valeur renvoyée.<br>Si la valeur est &quot;append&quot;, l’ancre est renvoyée sous la forme d’une valeur distincte.</li></ul> | get_url_query_str &#x200B;(URL, ANCHOR) | get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/here?name= &#x200B; furet#nose&quot;, &quot;preserve&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/here?name= &#x200B; furet#nose&quot;, &quot;remove&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com &#x200B;:8042/over/here/here &#x200B;?name=furet#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

{style=&quot;table-layout:auto&quot;}

### Fonctions de date et d’heure {#date-and-time}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau. Plus d’informations sur la `date` se trouve dans la section dates du [guide de gestion des formats de données](./data-handling.md#dates).

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Récupère l’heure actuelle. |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | Récupère l’heure Unix actuelle. |  | timestamp() | timestamp() | 1571850624571 |
| format | Formate la date d’entrée selon un format spécifié. | <ul><li>DATE : **Obligatoire** La date d&#39;entrée, en tant qu&#39;objet ZonedDateTime, que vous souhaitez mettre en forme.</li><li>FORMAT : **Obligatoire** Format dans lequel vous souhaitez modifier la date.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;aaaa-MM-jj HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35 pouces |
| dformat | Convertit une date et une heure en chaîne de date selon un format spécifié. | <ul><li>TIMESTAMP : **Obligatoire** L’horodatage à formater. Ceci est écrit en millisecondes.</li><li>FORMAT : **Obligatoire** Format que vous souhaitez que l’horodatage devienne.</li></ul> | dformat &#x200B;(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;yyy-MM-dd&#39;T&#39;HH:mm:ss.SSSX&quot;) | &quot;2019-10-23T11:24:35,000Z&quot; |
| date | Convertit une chaîne de date en objet ZonedDateTime (format ISO 8601). | <ul><li>DATE : **Obligatoire** Chaîne représentant la date.</li><li>FORMAT : **Obligatoire** Chaîne représentant le format de la date source.**Remarque :** Cette opération **non** représente le format dans lequel vous souhaitez convertir la chaîne de date. </li><li>DEFAULT_DATE : **Obligatoire** La date par défaut renvoyée, si la date fournie est nulle.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-jj HH:mm&quot;, now())) | &quot;2019-10-23T11:24Z&quot; |
| date | Convertit une chaîne de date en objet ZonedDateTime (format ISO 8601). | <ul><li>DATE : **Obligatoire** Chaîne représentant la date.</li><li>FORMAT : **Obligatoire** Chaîne représentant le format de la date source.**Remarque :** Cette opération **non** représente le format dans lequel vous souhaitez convertir la chaîne de date. </li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-jj HH:mm&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date | Convertit une chaîne de date en objet ZonedDateTime (format ISO 8601). | <ul><li>DATE : **Obligatoire** Chaîne représentant la date.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date_part | Récupère les parties de la date. Les valeurs de composant suivantes sont prises en charge : <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;weekday&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecond&quot;<br>&quot;ms&quot; | <ul><li>COMPOSANT : **Obligatoire** Chaîne représentant la partie de la date. </li><li>DATE : **Obligatoire** La date, dans un format standard.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12 pouces)) | 10 |
| set_date_part | Remplace un composant à une date donnée. Les composants suivants sont acceptés : <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>COMPOSANT : **Obligatoire** Chaîne représentant la partie de la date. </li><li>VALEUR : **Obligatoire** Valeur à définir pour le composant pour une date donnée.</li><li>DATE : **Obligatoire** La date, dans un format standard.</li></ul> | set_date_part &#x200B;(COMPOSANT, VALEUR, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44,797&quot;) | &quot;2016-04-09T11:44:44,797 po |
| make_date_time | Crée une date à partir de parties. Cette fonction peut également être induite à l&#39;aide de make_timestamp. | <ul><li>ANNÉE : **Obligatoire** L&#39;année, écrite en quatre chiffres.</li><li>MOIS : **Obligatoire** Le mois. Les valeurs autorisées sont comprises entre 1 et 12.</li><li>JOUR : **Obligatoire** Le jour. Les valeurs autorisées sont comprises entre 1 et 31.</li><li>HEURE : **Obligatoire** L&#39;heure. Les valeurs autorisées sont comprises entre 0 et 23.</li><li>MINUTE : **Obligatoire** La minute. Les valeurs autorisées sont comprises entre 0 et 59.</li><li>NANOSECOND : **Obligatoire** Valeurs de nanoseconde. Les valeurs autorisées sont comprises entre 0 et 9999999999.</li><li>TIMEZONE : **Obligatoire** Fuseau horaire pour l’heure de la date.</li></ul> | make_date_time &#x200B;(ANNÉE, MOIS, JOUR, HEURE, MINUTE, SECONDE, NANOSECOND, TIMEZONE) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | Convertit une date dans n&#39;importe quel fuseau horaire en date UTC. | <ul><li>DATE : **Obligatoire** La date que vous tentez de convertir.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12.000000999-&#x200B;07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | Convertit une date d’un fuseau horaire en un autre fuseau horaire. | <ul><li>DATE : **Obligatoire** La date que vous tentez de convertir.</li><li>ZONE : **Obligatoire** Fuseau horaire vers lequel vous tentez de convertir la date.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:12&#x200B;.000000999-07:00&#x200B;[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

{style=&quot;table-layout:auto&quot;}
&#x200B;

### Hiérarchies - Objets {#objects}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| size_of | Renvoie la taille de l&#39;entrée. | <ul><li>ENTRÉE : **Obligatoire** L&#39;objet dont vous essayez de trouver la taille.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_blank | Vérifie si un objet est vide ou non. | <ul><li>ENTRÉE : **Obligatoire** L&#39;objet que vous essayez de vérifier est vide.</li></ul> | is_blank(INPUT) | `is_empty([1, 2, 3])` | false |
| array_to_object | Crée une liste d’objets. | <ul><li>ENTRÉE : **Obligatoire** Groupe de paires de clés et de tableaux.</li></ul> | array_to_object(INPUT) | exemple nécessaire | exemple nécessaire |
| to_object | Crée un objet basé sur les paires clé/valeur plate données. | <ul><li>ENTRÉE : **Obligatoire** Liste plate de paires clé/valeur.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Crée un objet à partir de la chaîne d’entrée. | <ul><li>CHAÎNE : **Obligatoire** Chaîne analysée pour créer un objet.</li><li>VALUE_DELIMITER : *Facultatif* Délimiteur qui sépare un champ de la valeur. Le délimiteur par défaut est `:`.</li><li>FIELD_DELIMITER : *Facultatif* Délimiteur qui sépare les paires de valeurs de champ. Le délimiteur par défaut est `,`.</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | téléphone - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| contient_key | Vérifie si l&#39;objet existe dans les données source. **Remarque :** Cette fonction remplace la fonction obsolète `is_set()` fonction. | <ul><li>ENTRÉE : **Obligatoire** Chemin d’accès à vérifier s’il existe dans les données source.</li></ul> | includes_key(INPUT) | contents_key(&quot;evars.evar.field1&quot;) | vrai |
| annuler | Définit la valeur de l’attribut sur `null`. Cette option doit être utilisée lorsque vous ne souhaitez pas copier le champ dans le schéma cible. |  | nullify() | nullify() | `null` |
| get_keys | Analyse les paires clé/valeur et renvoie toutes les clés. | <ul><li>OBJET : **Obligatoire** Objet à partir duquel les clés seront extraites.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;) : &quot;Fierté et préjugé&quot;, &quot;book2&quot; : &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | Analyse les paires clé/valeur et renvoie la valeur de la chaîne, en fonction de la clé donnée. | <ul><li>CHAÎNE : **Obligatoire** Chaîne que vous souhaitez analyser.</li><li>CLÉ : **Obligatoire** La clé pour laquelle la valeur doit être extraite.</li><li>VALUE_DELIMITER : **Obligatoire** Le délimiteur qui sépare le champ de la valeur. Si `null` ou une chaîne vide est fournie, cette valeur est `:`.</li><li>FIELD_DELIMITER : *Facultatif* Délimiteur qui sépare les paires de champs et de valeurs. Si `null` ou une chaîne vide est fournie, cette valeur est `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John, lastName - Cena, téléphone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | John |

{style=&quot;table-layout:auto&quot;}

### Hiérarchies - Tableaux {#arrays}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| coalesce | Renvoie le premier objet non nul dans un tableau donné. | <ul><li>ENTRÉE : **Obligatoire** Tableau dont vous souhaitez trouver le premier objet non nul.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | Récupère le premier élément du tableau donné. | <ul><li>ENTRÉE : **Obligatoire** Tableau dont vous souhaitez trouver le premier élément.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Récupère le dernier élément du tableau donné. | <ul><li>ENTRÉE : **Obligatoire** Tableau dont vous souhaitez trouver le dernier élément.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | Ajoute des éléments à la fin du tableau. | <ul><li>ARRAY : **Obligatoire** Tableau auquel vous ajoutez des éléments.</li><li>VALEURS : Les éléments que vous souhaitez ajouter au tableau.</li></ul> | add_to_array &#x200B;(ARRAY, VALUES) | add_to_array &#x200B;([&#39;a&#39;, &#39;b&#39;], &quot;c&quot;, &quot;d&quot;) | [a, b, c, d] |
| join_array | Combine les tableaux les uns avec les autres. | <ul><li>ARRAY : **Obligatoire** Tableau auquel vous ajoutez des éléments.</li><li>VALEURS : La ou les baies que vous souhaitez ajouter à la baie parent.</li></ul> | jointure_array &#x200B;(ARRAY, VALUES) | join_array &#x200B;([&#39;a&#39;, &#39;b&#39;], [&quot;c&quot;], [&#39;d&#39;, &#39;e&#39;]) | [a, b, c, d, e] |
| to_array | Prend une liste d’entrées et la convertit en tableau. | <ul><li>INCLUDE_NULLS : **Obligatoire** Valeur booléenne indiquant si les valeurs nulles doivent être incluses ou non dans le tableau de réponses.</li><li>VALEURS : **Obligatoire** Les éléments à convertir en tableau.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

{style=&quot;table-layout:auto&quot;}

### Opérateurs logiques {#logical-operators}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decode | Étant donné qu’une clé et une liste de paires clé-valeur sont aplaties dans un tableau, la fonction renvoie la valeur si la clé est trouvée ou renvoie une valeur par défaut si elle est présente dans le tableau. | <ul><li>CLÉ : **Obligatoire** La clé à mettre en correspondance.</li><li>OPTIONS : **Obligatoire** Tableau aplati de paires clé/valeur. Si vous le souhaitez, une valeur par défaut peut être définie à la fin.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Si le code d&#39;état donné est &quot;ca&quot;, &quot;California&quot;.<br>Si le code d&#39;état donné est &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Si la propriété stateCode ne correspond pas à la propriété suivante, &quot;S/O&quot;. |
| iif | Évalue une expression booléenne donnée et renvoie la valeur spécifiée en fonction du résultat. | <ul><li>EXPRESSION : **Obligatoire** Expression booléenne en cours d&#39;évaluation.</li><li>TRUE_VALUE : **Obligatoire** Valeur renvoyée si l’expression est évaluée sur true.</li><li>FALSE_VALUE : **Obligatoire** Valeur renvoyée si l’expression est évaluée sur false.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style=&quot;table-layout:auto&quot;}

### Agrégation {#aggregation}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Renvoie le minimum des arguments donnés. Utilise l’ordre naturel. | <ul><li>OPTIONS : **Obligatoire** Un ou plusieurs objets pouvant être comparés.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Renvoie le maximum des arguments donnés. Utilise l’ordre naturel. | <ul><li>OPTIONS : **Obligatoire** Un ou plusieurs objets pouvant être comparés.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style=&quot;table-layout:auto&quot;}

### Conversions de type {#type-conversions}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Convertit une chaîne en objet BigInteger. | <ul><li>CHAÎNE : **Obligatoire** Chaîne à convertir en type BigInteger.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;1000000.34&quot;) | 1000000,34 |
| to_decimal | Convertit une chaîne en double. | <ul><li>CHAÎNE : **Obligatoire** Chaîne à convertir en double.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Convertit une chaîne en virgule flottante. | <ul><li>CHAÎNE : **Obligatoire** Chaîne à convertir en Flottant.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_entier | Convertit une chaîne en entier. | <ul><li>CHAÎNE : **Obligatoire** Chaîne à convertir en entier.</li></ul> | to_entier(STRING) | to_entier(&quot;12&quot;) | 12 |

{style=&quot;table-layout:auto&quot;}

### Fonctions JSON {#json}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Désérialise le contenu JSON à partir de la chaîne donnée. | <ul><li>CHAÎNE : **Obligatoire** Chaîne JSON à désérialiser.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot; : &quot;Doe&quot;}}) | Objet représentant le fichier JSON. |

{style=&quot;table-layout:auto&quot;}

### Opérations spéciales {#special-operations}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | Génère un identifiant pseudo-aléatoire. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fcda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

{style=&quot;table-layout:auto&quot;}

### Fonctions de l&#39;agent utilisateur {#user-agent}

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Extrait le nom du système d&#39;exploitation de la chaîne de l&#39;agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l&#39;agent utilisateur.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone ; Processeur iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extrait la version principale du système d&#39;exploitation de la chaîne de l&#39;agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l&#39;agent utilisateur.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone ; Processeur iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Extrait la version du système d&#39;exploitation de la chaîne de l&#39;agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l&#39;agent utilisateur.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone ; Processeur iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Extrait le nom et la version du système d&#39;exploitation de la chaîne de l&#39;agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l&#39;agent utilisateur.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone ; Processeur iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extrait la version de l&#39;agent de la chaîne de l&#39;agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l&#39;agent utilisateur.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone ; Processeur iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | Extrait le nom de l&#39;agent et la version principale de la chaîne de l&#39;agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l&#39;agent utilisateur.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone ; Processeur iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extrait le nom de l&#39;agent de la chaîne de l&#39;agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l&#39;agent utilisateur.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone ; Processeur iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extrait la classe device de la chaîne de l&#39;agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l&#39;agent utilisateur.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone ; Processeur iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Téléphone |

{style=&quot;table-layout:auto&quot;}
