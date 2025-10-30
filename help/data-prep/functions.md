---
keywords: Experience Platform;accueil;rubriques les plus consultées;mapper csv;mapper le fichier csv;mapper le fichier csv à xdm;mapper csv à xdm;guide de l’interface utilisateur;mappeur;mappage;champs de mappage;fonctions de mappage;
solution: Experience Platform
title: Fonctions de mappage de la préparation des données
description: Ce document présente les fonctions de mappage utilisées avec la préparation des données.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '6009'
ht-degree: 8%

---

# Fonctions de mappage de la préparation des données

Les fonctions de préparation de données peuvent être utilisées pour calculer des valeurs en fonction de ce qui est saisi dans les champs sources.

## Champs

Un nom de champ peut être n’importe quel identifiant légal, une séquence de lettres et de chiffres Unicode d’une longueur illimitée commençant par une lettre, le signe dollar (`$`) ou le caractère de soulignement (`_`). Les noms de variables respectent également la casse.

Si un nom de champ ne suit pas cette convention, il doit être encapsulé avec des `${}`. Ainsi, par exemple, si le nom du champ est « Prénom » ou « Prénom », le nom doit être encapsulé comme `${First Name}` ou `${First\.Name}`, respectivement.

>[!TIP]
>
>Lors de l’interaction avec des hiérarchies, si un attribut enfant comporte un point (`.`), vous devez utiliser une barre oblique inverse (`\`) pour échapper les caractères spéciaux. Pour plus d’informations, consultez le guide sur l’[échappement des caractères spéciaux](home.md#escape-special-characters).

Si le nom d’un champ est **l’un** des mots-clés réservés suivants, il doit être encapsulé avec `${}{}` :

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors, do, function, empty, size
```

En outre, les mots-clés réservés incluent également l’une des fonctions de mappeur répertoriées sur cette page.

Les données des sous-champs sont accessibles à l’aide de la notation par points. Par exemple, s’il existait un objet `name`, pour accéder au champ `firstName`, utilisez `name.firstName`.

## Liste des fonctions

Les tableaux suivants répertorient toutes les fonctions de mappage prises en charge, y compris des exemples d’expressions et les sorties qui en résultent.

### Fonctions de chaîne {#string}

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Concatène les chaînes données. | <ul><li>STRING : les chaînes qui seront concaténées.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explode | Divise la chaîne en fonction d’une expression régulière et renvoie un tableau de parties. Peut éventuellement inclure une expression régulière pour fractionner la chaîne. Par défaut, la division est résolue sur « , ». Les délimiteurs suivants **doivent** doivent être précédés d’un caractère d’échappement `\` : `+, ?, ^, \|, ., [, (, {, ), *, $, \` Si vous incluez plusieurs caractères comme délimiteur, le délimiteur sera traité comme un délimiteur à plusieurs caractères. | <ul><li>STRING : **obligatoire** la chaîne qui doit être fractionnée.</li><li>REGEX : *facultatif* expression régulière qui peut être utilisée pour fractionner la chaîne.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hi, there!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Renvoie l’emplacement/l’index d’une sous-chaîne. | <ul><li>INPUT : **obligatoire** chaîne faisant l’objet de la recherche.</li><li>SOUS-CHAÎNE : **obligatoire** sous-chaîne recherchée dans la chaîne.</li><li>POSITION_DÉBUT : *facultatif* emplacement où commencer à rechercher des éléments dans la chaîne.</li><li>OCCURRENCE : *facultatif* nième occurrence à rechercher à partir de la position de départ. Par défaut, il s’agit de 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(« adobe.com », « com ») | 6 |
| replacestr | Remplace la chaîne de recherche si elle est présente dans la chaîne d’origine. | <ul><li>INPUT : **obligatoire** chaîne d’entrée.</li><li>TO_FIND : **Obligatoire** chaîne à rechercher dans l’entrée.</li><li>TO_REPLACE : **Obligatoire** chaîne qui remplacera la valeur dans « TO_FIND ».</li></ul> | replacestr(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;This is a string replace test&quot; |
| substr | Renvoie une sous-chaîne d’une longueur donnée. | <ul><li>INPUT : **obligatoire** chaîne d’entrée.</li><li>START_INDEX : **obligatoire** index de la chaîne d’entrée sur laquelle la sous-chaîne commence.</li><li>LONGUEUR : **Obligatoire** longueur de la sous-chaîne.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Convertit une chaîne en minuscules. | <ul><li>INPUT : **obligatoire** chaîne qui sera convertie en minuscules.</li></ul> | lower(INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | Convertit une chaîne en majuscules. | <ul><li>INPUT : **obligatoire** chaîne qui sera convertie en majuscules.</li></ul> | upper(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HELLO&quot; |
| split | Divise une chaîne d’entrée sur un séparateur. Le séparateur suivant **doit** doit être placé dans une séquence d’échappement avec `\` : `\`. Si vous incluez plusieurs délimiteurs, la chaîne est fractionnée sur **n’importe lequel** des délimiteurs présents dans la chaîne. **Remarque :** cette fonction renvoie uniquement des index non nuls à partir de la chaîne, quelle que soit la présence du séparateur. Si tous les index, y compris les valeurs nulles, sont requis dans le tableau obtenu, utilisez plutôt la fonction « explode ». | <ul><li>INPUT : **obligatoire** chaîne d’entrée qui va être fractionnée.</li><li>SEPARATOR : **obligatoire** chaîne utilisée pour fractionner l’entrée.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Joint une liste d’objets à l’aide du séparateur. | <ul><li>SEPARATOR : **Obligatoire** chaîne qui sera utilisée pour joindre les objets.</li><li>OBJETS : **Obligatoire** Tableau de chaînes qui seront jointes.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | Complète le côté gauche d’une chaîne avec l’autre chaîne donnée. | <ul><li>INPUT : **obligatoire** chaîne qui va être complétée. Cette chaîne peut être nulle.</li><li>COUNT : **obligatoire** taille de la chaîne à remplir.</li><li>MARGE INTÉRIEURE : **obligatoire** chaîne avec laquelle remplir l’entrée. Si nul ou vide, il sera traité comme un espace unique.</li></ul> | load(INPUT, COUNT, PADDING) | lpad(« bat », 8, « yz ») | « yzyzybat » |
| rpad | Complète le côté droit d’une chaîne avec l’autre chaîne donnée. | <ul><li>INPUT : **obligatoire** chaîne qui va être complétée. Cette chaîne peut être nulle.</li><li>COUNT : **obligatoire** taille de la chaîne à remplir.</li><li>MARGE INTÉRIEURE : **obligatoire** chaîne avec laquelle remplir l’entrée. Si nul ou vide, il sera traité comme un espace unique.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(« bat », 8, « yz ») | « batyzyzy » |
| left | Obtient les premiers caractères « n » de la chaîne donnée. | <ul><li>STRING : **Obligatoire** chaîne pour laquelle vous obtenez les premiers caractères « n ».</li><li>COUNT : **Obligatoire** les caractères « n » que vous souhaitez obtenir à partir de la chaîne.</li></ul> | left(STRING, COUNT) | left(« abcde », 2) | « ab » |
| droite | Obtient les « n » derniers caractères de la chaîne donnée. | <ul><li>STRING : **Obligatoire** chaîne pour laquelle vous obtenez les « n » derniers caractères.</li><li>COUNT : **Obligatoire** les caractères « n » que vous souhaitez obtenir à partir de la chaîne.</li></ul> | right(STRING, COUNT) | right(« abcde », 2) | « de » |
| ltrim | Supprime l’espace au début de la chaîne. | <ul><li>STRING : **Obligatoire** chaîne dont vous souhaitez supprimer l’espace.</li></ul> | ltrim(STRING) | ltrim(«  hello ») | &quot;hello&quot; |
| rtrim | Supprime l’espace à la fin de la chaîne. | <ul><li>STRING : **Obligatoire** chaîne dont vous souhaitez supprimer l’espace.</li></ul> | rtrim(STRING) | rtrim(« hello  ») | &quot;hello&quot; |
| trim | Supprime les espaces blancs du début et de la fin de la chaîne. | <ul><li>STRING : **Obligatoire** chaîne dont vous souhaitez supprimer l’espace.</li></ul> | trim(STRING) | trim(«  hello  ») | &quot;hello&quot; |
| est égal à | Compare deux chaînes pour vérifier si elles sont égales. Cette fonction respecte la casse. | <ul><li>STRING1 : **Obligatoire** première chaîne à comparer.</li><li>STRING2 : **Obligatoire** deuxième chaîne à comparer.</li></ul> | STRING1. &#x200B;égal à(&#x200B;STRING2) | « string1 ». &#x200B;equals&#x200B;(« STRING1 ») | False |
| equalsIgnoreCase | Compare deux chaînes pour vérifier si elles sont égales. Cette fonction n’est **pas** sensible à la casse. | <ul><li>STRING1 : **Obligatoire** première chaîne à comparer.</li><li>STRING2 : **Obligatoire** deuxième chaîne à comparer.</li></ul> | STRING1. &#x200B;equalsIgnoreCase&#x200B;(STRING2) | « string1 ». &#x200B;equalsIgnoreCase&#x200B;(« STRING1) | vrai |

{style="table-layout:auto"}

### Fonctions d’expressions régulières

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | Extrait les groupes de la chaîne d’entrée, en fonction d’une expression régulière. | <ul><li>STRING : **obligatoire** chaîne à partir de laquelle vous extrayez les groupes.</li><li>REGEX : **obligatoire** expression régulière à laquelle vous souhaitez que le groupe corresponde.</li></ul> | extract_regex(STRING, REGEX) | extract_regex&#x200B;(« E259,E259B_009,1_1 »&#x200B;, « ([^,]+),[^,]*,([^,]+) ») | [« E259,E259B_009,1_1 », « E259 », « 1_1 »] |
| matches_regex | Vérifie si la chaîne correspond à l’expression régulière saisie. | <ul><li>STRING : **Obligatoire** la chaîne que vous vérifiez correspond à l’expression régulière.</li><li>REGEX : **obligatoire** expression régulière à laquelle vous effectuez une comparaison.</li></ul> | matches_regex(STRING, REGEX) | matches_regex(« E259,E259B_009,1_1 », « ([^,]+),[^,]*,([^,]+) ») | vrai |

{style="table-layout:auto"}

### Fonctions de hachage {#hashing}

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Prend une entrée et génère une valeur de hachage à l’aide de l’algorithme de hachage sécurisé 1 (SHA-1). | <ul><li>INPUT : **obligatoire** texte brut à hacher.</li><li>CHARSET : *facultatif* nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(« mon texte », « UTF-8 ») | c3599c11e47719df18a24&#x200B;48690840c5dfcce3c80 |
| sha256 | Prend une entrée et génère une valeur de hachage à l’aide de l’algorithme de hachage sécurisé 256 (SHA-256). | <ul><li>INPUT : **obligatoire** texte brut à hacher.</li><li>CHARSET : *facultatif* nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | sha256(INPUT, CHARSET) | sha256(« mon texte », « UTF-8 ») | 7330d2b39ca35eaf4cb95fc846c21&#x200B;ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Prend une entrée et produit une valeur de hachage à l’aide de l’algorithme de hachage sécurisé 512 (SHA-512). | <ul><li>INPUT : **obligatoire** texte brut à hacher.</li><li>CHARSET : *facultatif* nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | sha512(INPUT, CHARSET) | sha512(« mon texte », « UTF-8 ») | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef&#x200B;708bf11b4232bb21d2a8704ada2cdcd7b367dd0788a89&#x200B;a5c908cfe377aceb1072a7b388 b7d4fd2ff68a8fd24d16 |
| md5 | Prend une entrée et génère une valeur de hachage à l’aide de MD5. | <ul><li>INPUT : **obligatoire** texte brut à hacher.</li><li>CHARSET : *facultatif* nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(« mon texte », « UTF-8 ») | d3b96ce8c9fb4&#x200B;e9bd0198d03ba6852c7 |
| crc32 | Prend une entrée utilise un algorithme de contrôle de redondance cyclique (CRC) pour produire un code cyclique de 32 bits. | <ul><li>INPUT : **obligatoire** texte brut à hacher.</li><li>CHARSET : *facultatif* nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(« mon texte », « UTF-8 ») | 8df92e80 |

{style="table-layout:auto"}

### Fonctions d’URL {#url}

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Retourne le protocole à partir de l’URL donnée. Si l’entrée n’est pas valide, elle renvoie la valeur null. | <ul><li>URL : **Obligatoire** URL à partir de laquelle le protocole doit être extrait.</li></ul> | get_url_protocol&#x200B;(URL) | get_url_protocol(« https://platform&#x200B;.adobe.com/home ») | https |
| get_url_host | Renvoie l’hôte de l’URL donnée. Si l’entrée n’est pas valide, elle renvoie la valeur null. | <ul><li>URL : **Obligatoire** URL à partir de laquelle l’hôte doit être extrait.</li></ul> | get_url_host&#x200B;(URL) | get_url_host&#x200B;(« https://platform&#x200B;.adobe.com/home ») | platform.adobe.com |
| get_url_port | Renvoie le port de l’URL donnée. Si l’entrée n’est pas valide, elle renvoie la valeur null. | <ul><li>URL : **Obligatoire** URL à partir de laquelle le port doit être extrait.</li></ul> | get_url_port(URL) | get_url_port&#x200B;(« sftp://example.com//home/&#x200B;joe/employee.csv ») | 22 |
| get_url_path | Renvoie le chemin d’accès de l’URL donnée. Par défaut, le chemin d’accès complet est renvoyé. | <ul><li>URL : **Obligatoire** URL à partir de laquelle le chemin d’accès doit être extrait.</li><li>FULL_PATH : *facultatif* valeur booléenne qui détermine si le chemin d’accès complet est renvoyé. Si elle est définie sur false, seule la fin du chemin est renvoyée.</li></ul> | get_url_path&#x200B;(URL, FULL_PATH) | get_url_path&#x200B;(« sftp://example.com//&#x200B;home/joe/employee.csv ») | « //home/joe/&#x200B;employee.csv » |
| get_url_query_str | Renvoie la chaîne de requête d’une URL donnée sous la forme d’un mappage du nom de la chaîne de requête et de la valeur de la chaîne de requête. | <ul><li>URL : **Obligatoire** URL à partir de laquelle vous essayez d’obtenir la chaîne de requête.</li><li>ANCHOR : **obligatoire** détermine ce qui sera fait avec l’ancre dans la chaîne de requête. Il peut s’agir de l’une des trois valeurs suivantes : « conserver », « supprimer » ou « ajouter ».<br><br>Si la valeur est « retain », l&#39;ancre sera attachée à la valeur renvoyée.<br>Si la valeur est « remove », l&#39;ancre sera supprimée de la valeur renvoyée.<br>Si la valeur est « append », l’ancre est renvoyée en tant que valeur distincte.</li></ul> | get_url_query_str&#x200B;(URL, ANCHOR) | get_url_query_str&#x200B;(« foo://example.com:8042&#x200B;/over/There?name=&#x200B;ferret#nose », « retain »)<br>get_url_query_str&#x200B;(« foo://example.com:8042&#x200B;/over/There?name=&#x200B;ferret#nose », « remove »)<br>get_url_query_str&#x200B; &#x200B; &#x200B;(« foo://example.com:8042/over/they?name=ferret#nose », « append ») | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |
| get_url_encoded | Cette fonction prend une URL comme entrée et remplace ou encode les caractères spéciaux avec des caractères ASCII. Pour plus d&#39;informations sur les caractères spéciaux, veuillez lire la [liste des caractères spéciaux](#special-characters) en annexe de ce document. | <ul><li>URL : **Obligatoire** URL d’entrée avec des caractères spéciaux que vous souhaitez remplacer ou coder avec des caractères ASCII.</li></ul> | get_url_encoded(URL) | get_url_encoded(« https</span>://example.com/PARTNERalliance_asia-pacific_2022 ») | https%3A%2F%2Fexample.com%2Fpartners_asia-pacific_2022 |
| get_url_decoded | Cette fonction prend une URL comme entrée et décode les caractères ASCII en caractères spéciaux.  Pour plus d&#39;informations sur les caractères spéciaux, veuillez lire la [liste des caractères spéciaux](#special-characters) en annexe de ce document. | <ul><li>URL : **Obligatoire** URL d’entrée contenant des caractères ASCII que vous souhaitez décoder en caractères spéciaux.</li></ul> | get_url_decoded(URL) | get_url_decoded(« https%3A%2F%2Fexample.com%2Fpartner_asia-pacific_2022 ») | https</span>://example.com/PARTNERalliance_asia-pacific_2022 |

{style="table-layout:auto"}

### Fonctions de date et d’heure {#date-and-time}

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau. Vous trouverez plus d’informations sur la fonction `date` dans la section dates du guide [de la gestion des formats de données](./data-handling.md#dates).

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Récupère l’heure actuelle. | | now() | now() | `2021-10-26T10:10:24Z` |
| timestamp | Récupère l’heure Unix actuelle. | | timestamp() | timestamp() | 1571850624571 |
| format | Formate la date d’entrée selon un format spécifié. | <ul><li>DATE : **Obligatoire** date d’entrée, sous la forme d’un objet ZonedDateTime, que vous souhaitez formater.</li><li>FORMAT : **Obligatoire** format dans lequel vous souhaitez que la date soit modifiée.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, « `yyyy-MM-dd HH:mm:ss` ») | `2019-10-23 11:24:35` |
| dformat | Convertit une date et une heure en chaîne de date selon un format spécifié. | <ul><li>TIMESTAMP : **obligatoire** date et heure à formater. Il est écrit en millisecondes.</li><li>FORMAT : **Obligatoire** format dans lequel vous souhaitez que l’horodatage soit défini.</li></ul> | format(TIMESTAMP, FORMAT) | dformat(1571829875000, « `yyyy-MM-dd'T'HH:mm:ss.SSSX` ») | `2019-10-23T11:24:35.000Z` |
| date | Convertit une chaîne de date en objet ZonedDateTime (format ISO 8601). | <ul><li>DATE : **Obligatoire** chaîne qui représente la date.</li><li>FORMAT : **Obligatoire** chaîne représentant le format de la date source.**Remarque :** il ne s’agit **pas** du format dans lequel vous souhaitez convertir la chaîne de date. </li><li>DEFAULT_DATE : **Obligatoire** date par défaut renvoyée, si la date fournie est nulle.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(« 2019-10-23 11:24 », « yyyy-MM-dd HH:mm », now()) | `2019-10-23T11:24:00Z` |
| date | Convertit une chaîne de date en objet ZonedDateTime (format ISO 8601). | <ul><li>DATE : **Obligatoire** chaîne qui représente la date.</li><li>FORMAT : **Obligatoire** chaîne représentant le format de la date source.**Remarque :** il ne s’agit **pas** du format dans lequel vous souhaitez convertir la chaîne de date. </li></ul> | date(DATE, FORMAT) | date(« 2019-10-23 11:24 », « aaaa-MM-jj HH:mm ») | `2019-10-23T11:24:00Z` |
| date | Convertit une chaîne de date en objet ZonedDateTime (format ISO 8601). | <ul><li>DATE : **Obligatoire** chaîne qui représente la date.</li></ul> | date(DATE) | date(« 2019-10-23 11:24 ») | « 2019-10-23T11:24:00Z » |
| date_part | Récupère les parties de la date. Les valeurs de composant suivantes sont prises en charge : <br><br>« year »<br>« yyyy »<br>« yy »<br><br>« quarter »<br>« qq »<br>« q »<br><br>« month »<br>« mm »<br>« m »<br><br>« dayofyear »<br>« y »<br>« day »<br><br> »<br> »<br>« d »<br><br>« week »<br> »<br>« w »<br><br> »<br>« weekday »<br>« dw »<br><br> »<br>« hour »<br>« hh »<br> »<br><br>« hh24 »<br> »<br>« hh12 »<br><br>« minute »<br> »<br> »<br><br>« n »<br>« « second »« ss »« s »« milliseconde | <ul><li>COMPOSANT : **Obligatoire** Chaîne représentant la partie de la date. </li><li>DATE : **Obligatoire** date au format standard.</li></ul> | date_part&#x200B;(COMPONENT, DATE) | date_part(« MM », date(« 2019-10-17 11:55:12 »)) | 10 |
| set_date_part | Remplace un composant à une date donnée. Les composants suivants sont acceptés : <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>COMPOSANT : **Obligatoire** Chaîne représentant la partie de la date. </li><li>VALEUR : **Obligatoire** valeur à définir pour le composant à une date donnée.</li><li>DATE : **Obligatoire** date au format standard.</li></ul> | set_date_part&#x200B;(COMPONENT, VALUE, DATE) | set_date_part(« m », 4, date(« 2016-11-09T11:44:44.797 ») | « 2016-04-09T11:44:44Z » |
| make_date_time | Crée une date à partir de parties. Cette fonction peut également être induite à l’aide de make_timestamp. | <ul><li>YEAR : **Obligatoire** L&#39;année, écrite dans 4 chiffres.</li><li>MOIS : **obligatoire** le mois. Les valeurs autorisées sont comprises entre 1 et 12.</li><li>JOUR : **obligatoire** le jour. Les valeurs autorisées sont comprises entre 1 et 31.</li><li>HEURE : **obligatoire** l’heure. Les valeurs autorisées sont comprises entre 0 et 23.</li><li>MINUTE : **Obligatoire** La minute. Les valeurs autorisées sont comprises entre 0 et 59.</li><li>NANOSECONDE : **obligatoire** valeurs de la nanoseconde. Les valeurs autorisées sont 0 à 999999999.</li><li>TIMEZONE : **obligatoire** fuseau horaire de la date et de l’heure.</li></ul> | make_date_time&#x200B;(YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time&#x200B;(2019, 10, 17, 11, 55, 12, 999, « America/Los_Angeles ») | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | Convertit une date de n’importe quel fuseau horaire en une date au format UTC. | <ul><li>DATE : **Obligatoire** date que vous tentez de convertir.</li></ul> | zone_date_to_utc&#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | Convertit une date d’un fuseau horaire à un autre. | <ul><li>DATE : **Obligatoire** date que vous tentez de convertir.</li><li>ZONE : **Obligatoire** fuseau horaire dans lequel vous essayez de convertir la date.</li></ul> | zone_date_to_zone&#x200B;(DATE, ZONE) | `zone_date_to_zone(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style="table-layout:auto"}

### Hiérarchies - Objets {#objects}

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | Vérifie si un objet est vide ou non. | <ul><li>INPUT : **obligatoire** l’objet que vous essayez de vérifier est vide.</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | False |
| arrays_to_object | Crée une liste d’objets. | <ul><li>INPUT : **obligatoire** regroupement de paires clé-tableau.</li></ul> | arrays_to_object(INPUT) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | Crée un objet en fonction des paires clé/valeur aplaties données. | <ul><li>INPUT : **obligatoire** liste plate de paires clé/valeur.</li></ul> | to_object(INPUT) | to_object&#x200B;(« firstName », « John », « lastName », « Doe ») | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Crée un objet à partir de la chaîne d’entrée. | <ul><li>STRING : **obligatoire** chaîne en cours d’analyse pour créer un objet.</li><li>VALUE_DELIMITER : *facultatif* délimiteur qui sépare un champ de la valeur. Le délimiteur par défaut est `:`.</li><li>FIELD_DELIMITER : *facultatif* délimiteur qui sépare les paires valeur de champ. Le délimiteur par défaut est `,`.</li></ul> | str_to_object&#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) **Remarque** : vous pouvez utiliser la fonction `get()` avec `str_to_object()` pour récupérer les valeurs des clés de la chaîne. | <ul><li>Exemple #1 : str_to_object(« firstName - John ; lastName - ; - 123 345 7890 », « - »,  »; »)</li><li>Exemple #2 : str_to_object(« firstName - John ; lastName - ; phone - 123 456 7890 », « - »,  »; »).get(« firstName »)</li></ul> | <ul><li>Exemple #1:`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>Exemple de #2 : « John »</li></ul> |
| contains_key | Vérifie si l’objet existe dans les données source. **Remarque :** cette fonction remplace la fonction `is_set()` obsolète. | <ul><li>INPUT : **obligatoire** chemin d’accès à vérifier s’il existe dans les données source.</li></ul> | contains_key(INPUT) | contains_key(« evars.evar.field1 ») | vrai |
| annuler | Définit la valeur de l’attribut sur `null`. Utilisez-le lorsque vous ne souhaitez pas copier le champ dans le schéma cible. | | nullify() | nullify() | `null` |
| get_keys | Analyse les paires clé/valeur et renvoie toutes les clés. | <ul><li>OBJET : **Obligatoire** objet à partir duquel les clés seront extraites.</li></ul> | get_keys(OBJECT) | get_keys({« livre1 »: « Fierté et préjugé », « livre2 »: « 1984 »}) | `["book1", "book2"]` |
| get_values | Analyse les paires clé/valeur et renvoie la valeur de la chaîne, en fonction de la clé donnée. | <ul><li>STRING : **obligatoire** chaîne que vous souhaitez analyser.</li><li>KEY : **Obligatoire** clé pour laquelle la valeur doit être extraite.</li><li>VALUE_DELIMITER : **obligatoire** délimiteur qui sépare le champ et la valeur. Si une `null` ou une chaîne vide est fournie, cette valeur est `:`.</li><li>FIELD_DELIMITER : *facultatif* délimiteur qui sépare les paires champ/valeur. Si une `null` ou une chaîne vide est fournie, cette valeur est `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\« firstName - John , lastName - Cena , phone - 555 420 8692\ », \« firstName\ », \« -\ », \ »,\ ») | John |
| map_get_values | Prend un mappage et une entrée de clé. Si l’entrée est une clé unique, la fonction renvoie la valeur associée à cette clé. Si l’entrée est un tableau de chaîne, la fonction renvoie toutes les valeurs correspondant aux clés fournies. Si le mappage entrant comporte des clés en double, la valeur renvoyée doit dédupliquer les clés et renvoyer des valeurs uniques. | <ul><li>MAP : **obligatoire** données de mappage d’entrée.</li><li>KEY : **obligatoire** la clé peut être une chaîne unique ou un tableau de chaînes. Si un autre type primitif (données/nombre) est fourni, il est traité comme une chaîne.</li></ul> | get_values(MAP, KEY) | Consultez l’[annexe](#map_get_values) pour obtenir un exemple de code. | |
| map_has_keys | Si une ou plusieurs clés d’entrée sont fournies, la fonction renvoie true. Si un tableau de chaînes est fourni comme entrée, la fonction renvoie true sur la première clé trouvée. | <ul><li>MAP : **obligatoire** données de mappage d’entrée</li><li>KEY : **obligatoire** la clé peut être une chaîne unique ou un tableau de chaînes. Si un autre type primitif (données/nombre) est fourni, il est traité comme une chaîne.</li></ul> | map_has_keys(MAP, KEY) | Consultez l’[annexe](#map_has_keys) pour obtenir un exemple de code. | |
| add_to_map | Accepte au moins deux entrées. Un nombre illimité de mappages peut être fourni en tant qu’entrées. La préparation de données renvoie un mappage unique qui contient toutes les paires clé-valeur de toutes les entrées. Si une ou plusieurs clés sont répétées (dans le même mappage ou sur plusieurs mappages), la préparation de données déduplique les clés afin que la première paire clé-valeur persiste dans l’ordre dans lequel elles ont été transmises dans l’entrée. | MAP : **obligatoire** données de mappage d’entrée. | add_to_map(MAP 1, MAP 2, MAP 3, ...) | Consultez l’[annexe](#add_to_map) pour obtenir un exemple de code. | |
| object_to_map (Syntaxe 1) | Utilisez cette fonction pour créer des types de données de mappage. | <ul><li>KEY : **Obligatoire** les clés doivent être une chaîne. Si d’autres valeurs primitives, telles que des entiers ou des dates, sont fournies, elles sont automatiquement converties en chaînes et traitées comme des chaînes.</li><li>ANY_TYPE : **obligatoire** fait référence à tout type de données XDM pris en charge, à l’exception des mappages.</li></ul> | object_to_map(KEY, ANY_TYPE, KEY, ANY_TYPE, ... ) | Consultez l’[annexe](#object_to_map) pour obtenir un exemple de code. | |
| object_to_map (Syntaxe 2) | Utilisez cette fonction pour créer des types de données de mappage. | <ul><li>OBJET : **obligatoire** vous pouvez fournir un objet ou un tableau d’objets entrant et pointer vers un attribut à l’intérieur de l’objet comme clé.</li></ul> | object_to_map(OBJECT) | Consultez l’[annexe](#object_to_map) pour obtenir un exemple de code. |  |
| object_to_map (Syntaxe 3) | Utilisez cette fonction pour créer des types de données de mappage. | <ul><li>OBJET : **obligatoire** vous pouvez fournir un objet ou un tableau d’objets entrant et pointer vers un attribut à l’intérieur de l’objet comme clé.</li></ul> | object_to_map(OBJECT_ARRAY, ATTRIBUTE_IN_OBJECT_TO_BE_USED_AS_A_KEY) | Consultez l’[annexe](#object_to_map) pour obtenir un exemple de code. |  |

{style="table-layout:auto"}

Pour plus d’informations sur la fonction de copie d’objet, consultez la section [ci-dessous](#object-copy).

### Hiérarchies - Tableaux {#arrays}

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| coalesce | Renvoie le premier objet non nul dans un tableau donné. | <ul><li>INPUT : **Obligatoire** tableau dont vous souhaitez rechercher le premier objet non nul.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | Récupère le premier élément du tableau donné. | <ul><li>INPUT : **Obligatoire** tableau dont vous souhaitez trouver le premier élément.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Récupère le dernier élément du tableau donné. | <ul><li>INPUT : **Obligatoire** tableau dont vous souhaitez rechercher le dernier élément.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | Ajoute des éléments à la fin du tableau. | <ul><li>TABLEAU : **obligatoire** tableau auquel vous ajoutez des éléments.</li><li>VALEURS : éléments à ajouter au tableau.</li></ul> | add_to_array&#x200B;(ARRAY, VALUES) | add_to_array&#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_arrays | Combine les tableaux entre eux. | <ul><li>TABLEAU : **obligatoire** tableau auquel vous ajoutez des éléments.</li><li>VALEURS : le ou les tableaux que vous souhaitez ajouter au tableau parent.</li></ul> | join_arrays&#x200B;(ARRAY, VALUES) | join_arrays&#x200B;([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [&#39;d&#39;, &#39;e&#39;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | Prend une liste d’entrées et la convertit en tableau. | <ul><li>INCLUDE_NULLS : **obligatoire** valeur booléenne utilisée pour indiquer si les valeurs NULL doivent être incluses ou non dans le tableau de réponse.</li><li>VALEURS : **Obligatoire** éléments à convertir en tableau.</li></ul> | to_array&#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | Renvoie la taille de l’entrée. | <ul><li>INPUT : **Obligatoire** objet dont vous essayez de déterminer la taille.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | Cette fonction est utilisée pour ajouter tous les éléments de l’ensemble du tableau d’entrée à la fin du tableau dans Profile. Cette fonction est **uniquement** applicable lors des mises à jour. Si elle est utilisée dans le contexte des insertions, cette fonction renvoie l&#39;entrée telle quelle. | <ul><li>TABLEAU : **obligatoire** tableau servant à ajouter le tableau dans le profil.</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | 123 456 [] |
| upsert_array_replace | Cette fonction est utilisée pour remplacer des éléments dans un tableau. Cette fonction est **uniquement** applicable lors des mises à jour. Si elle est utilisée dans le contexte des insertions, cette fonction renvoie l&#39;entrée telle quelle. | <ul><li>TABLEAU : **obligatoire** tableau servant à remplacer le tableau dans le profil.</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | 123 456 [] |
| [!BADGE Destinations uniquement]{type=Informative} array_to_string | Rejoint les représentations sous forme de chaînes des éléments d’un tableau à l’aide du séparateur spécifié. Si le tableau est multidimensionnel, il est aplati avant d’être joint. **Remarque** : cette fonction est utilisée dans les destinations. Pour plus d’informations, consultez la [documentation](../destinations/ui/export-arrays-maps-objects.md) . | <ul><li>SEPARATOR : **obligatoire** séparateur utilisé pour joindre les éléments du tableau.</li><li>TABLEAU : **obligatoire** tableau à joindre (après aplatissement).</li></ul> | array_to_string(SEPARATOR, ARRAY) | `array_to_string(";", ["Hello", "world"])` | « Bonjour, le monde » |
| [!BADGE Destinations uniquement]{type=Informative} filterArray* | Filtre le tableau donné en fonction d’un prédicat. **Remarque** : cette fonction est utilisée dans les destinations. Pour plus d’informations, consultez la [documentation](../destinations/ui/export-arrays-maps-objects.md) . | <ul><li>TABLEAU : **obligatoire** tableau à filtrer</li><li>PREDICATE : **Obligatoire** prédicat à appliquer à chaque élément du tableau donné. | filterArray(ARRAY, PREDICATE) | `filterArray([5, -6, 0, 7], x -> x > 0)` | 5 [ 7] |
| [!BADGE Destinations uniquement]{type=Informative} transformArray* | Transforme le tableau donné en fonction d’un prédicat. **Remarque** : cette fonction est utilisée dans les destinations. Pour plus d’informations, consultez la [documentation](../destinations/ui/export-arrays-maps-objects.md) . | <ul><li>TABLEAU : **obligatoire** tableau à transformer.</li><li>PREDICATE : **Obligatoire** prédicat à appliquer à chaque élément du tableau donné. | transformArray(ARRAY, PREDICATE) | `transformArray([5, 6, 7], x -> x + 1)` | [6, 7, 8] |
| [!BADGE Destinations uniquement]{type=Informative} flattenArray* | Aplatit le tableau donné (multidimensionnel) en un tableau unidimensionnel. **Remarque** : cette fonction est utilisée dans les destinations. Pour plus d’informations, consultez la [documentation](../destinations/ui/export-arrays-maps-objects.md) . | <ul><li>TABLEAU : **obligatoire** tableau à aplatir.</li></ul> | flattenArray(ARRAY) | flattenArray([[[&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;, &#39;d&#39;]], [[&#39;e&#39;], [&#39;f&#39;]]]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;, &#39;f&#39;] |

{style="table-layout:auto"}

### Hiérarchies - Mappage {#map}

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| array_to_map | Cette fonction prend un tableau d’objets et une clé comme entrée et renvoie un mappage du champ de la clé avec la valeur comme clé et l’élément du tableau comme valeur. | <ul><li>INPUT : **Obligatoire** tableau d’objets dont vous souhaitez rechercher le premier objet non nul.</li><li>KEY : **obligatoire** la clé doit être un nom de champ dans le tableau d’objets et l’objet doit être une valeur.</li></ul> | array_to_map(OBJECT[] INPUTS, KEY) | Lisez la [annexe](#object_to_map) pour obtenir un exemple de code. |  |
| object_to_map | Cette fonction prend un objet en tant qu’argument et renvoie un mappage de paires clé-valeur. | <ul><li>INPUT : **Obligatoire** tableau d’objets dont vous souhaitez rechercher le premier objet non nul.</li></ul> | object_to_map(OBJECT_INPUT) | « object_to_map(address) où l’entrée est «  + « adresse : {line1 : \« 345 park ave\ »,ligne2 : \« bldg 2\ »,Ville : \« san jose\ »,État : \« CA\ »,type : \« office\« } » | Renvoie un mappage avec des paires nom-valeur de champ données ou null si l’entrée est null. Par exemple : `"{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"` |
| to_map | Cette fonction prend une liste de paires clé-valeur et renvoie un mappage de paires clé-valeur. | | to_map(OBJECT_INPUT) | « to_map(\« prénom\ », \« Jean\ », \« nom\ », \« Doe\ ») » | Renvoie un mappage avec des paires nom-valeur de champ données ou null si l’entrée est null. Par exemple : `"{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"` |

{style="table-layout:auto"}

### Opérateurs logiques {#logical-operators}

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decode | Étant donné qu’une clé et une liste de paires clé-valeur sont aplaties dans un tableau, la fonction renvoie la valeur si la clé est trouvée ou renvoie une valeur par défaut si elle est présente dans le tableau. | <ul><li>KEY : **Obligatoire** clé à faire correspondre.</li><li>OPTIONS : **obligatoire** tableau aplati de paires clé/valeur. Vous pouvez éventuellement placer une valeur par défaut à la fin.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, « ca », « California », « pa », « Pennsylvania », « N/A ») | Si le code d’état donné est « ca », « California ».<br>Si le code d’état donné est « pa », « Pennsylvania ».<br>Si le code d’état ne correspond pas à ce qui suit, « N/A ». |
| iif | Évalue une expression booléenne donnée et renvoie la valeur spécifiée en fonction du résultat. | <ul><li>EXPRESSION : **obligatoire** expression booléenne en cours d’évaluation.</li><li>TRUE_VALUE : **obligatoire** valeur renvoyée si l’expression est évaluée comme vraie.</li><li>FALSE_VALUE : **obligatoire** valeur renvoyée si l’expression est évaluée comme égale à false.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style="table-layout:auto"}

### Agrégation {#aggregation}

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Renvoie le minimum des arguments donnés. Utilise l’ordre naturel. | <ul><li>OPTIONS : **obligatoire** un ou plusieurs objets pouvant être comparés les uns aux autres.</li></ul> | min (OPTIONS) | min(3, 1, 4) | 1 |
| max | Renvoie le maximum des arguments donnés. Utilise l’ordre naturel. | <ul><li>OPTIONS : **obligatoire** un ou plusieurs objets pouvant être comparés les uns aux autres.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style="table-layout:auto"}

### Conversions de type {#type-conversions}

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Convertit une chaîne en BigInteger. | <ul><li>STRING : **Obligatoire** la chaîne qui doit être convertie en BigInteger.</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(« 1000000.34 ») | 1000000,34 |
| to_decimal | Convertit une chaîne en doublon. | <ul><li>STRING : **Obligatoire** chaîne à convertir en doublon.</li></ul> | to_decimal(STRING) | to_decimal(« 20.5 ») | 20,5 |
| to_float | Convertit une chaîne en flottante. | <ul><li>STRING : **Obligatoire** chaîne à convertir en chaîne flottante.</li></ul> | to_float(STRING) | to_float(« 12.3456 ») | 12,34566 |
| to_integer | Convertit une chaîne en entier. | <ul><li>STRING : **obligatoire** chaîne à convertir en entier.</li></ul> | to_integer(STRING) | to_integer(« 12 ») | 12 |

{style="table-layout:auto"}

### Fonctions JSON {#json}

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Désérialisez le contenu JSON à partir de la chaîne donnée. | <ul><li>STRING : **obligatoire** la chaîne JSON à désérialiser.</li></ul> | json_to_object&#x200B;(STRING) | `json_to_object&#x200B;({"info":{"firstName":"John","lastName": "Doe"}})` | Objet représentant le fichier JSON. |

{style="table-layout:auto"}

### Opérations spéciales {#special-operations}

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | Génère un identifiant pseudo-aléatoire. | | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |
| `fpid_to_ecid` | Cette fonction prend une chaîne FPID et la convertit en un ECID à utiliser dans les applications Adobe Experience Platform et Adobe Experience Cloud. | <ul><li>STRING : **obligatoire** chaîne FPID à convertir en ECID.</li></ul> | `fpid_to_ecid(STRING)` | `fpid_to_ecid("4ed70bee-b654-420a-a3fd-b58b6b65e991")` | `"28880788470263023831040523038280731744"` |

{style="table-layout:auto"}

### Fonctions de l’agent utilisateur {#user-agent}

L’une des fonctions de l’agent utilisateur contenues dans le tableau ci-dessous peut renvoyer l’une des valeurs suivantes :

* Téléphone : appareil mobile doté d’un petit écran (généralement &lt; 7 pouces)
* Mobile : appareil mobile qui n’a pas encore été identifié. Cet appareil mobile peut être un eReader, une tablette, un téléphone, une montre, etc.

Pour plus d’informations sur les valeurs de champ de l’appareil, veuillez lire la [liste des valeurs de champ de l’appareil](#device-field-values) dans l’annexe de ce document.

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Extrait le nom du système d’exploitation de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **obligatoire** chaîne de l’agent utilisateur.</li></ul> | ua_os_name&#x200B;(USER_AGENT) | ua_os_name&#x200B;(« Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3 ») | iOS |
| ua_os_version_major | Extrait la version majeure du système d’exploitation de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **obligatoire** chaîne de l’agent utilisateur.</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major&#x200B;s(« Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3 ») | IOS 5 |
| ua_os_version | Extrait la version du système d’exploitation de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **obligatoire** chaîne de l’agent utilisateur.</li></ul> | ua_os_version&#x200B;(USER_AGENT) | ua_os_version&#x200B;(« Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3 ») | 5.1.1 |
| ua_os_name_version | Extrait le nom et la version du système d’exploitation de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **obligatoire** chaîne de l’agent utilisateur.</li></ul> | ua_os_name_version&#x200B;(USER_AGENT) | ua_os_name_version&#x200B;(« Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3 ») | iOS 5.1.1 |
| ua_agent_version | Extrait la version de l’agent de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **obligatoire** chaîne de l’agent utilisateur.</li></ul> | ua_agent_version&#x200B;(USER_AGENT) | ua_agent_version&#x200B;(« Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3 ») | 5,1 |
| ua_agent_version_major | Extrait le nom de l’agent et la version majeure de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **obligatoire** chaîne de l’agent utilisateur.</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major&#x200B;(« Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3 ») | Safari 5 |
| ua_agent_name | Extrait le nom de l’agent de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **obligatoire** chaîne de l’agent utilisateur.</li></ul> | ua_agent_name&#x200B;(USER_AGENT) | ua_agent_name&#x200B;(« Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3 ») | Safari |
| ua_device_class | Extrait la classe de périphérique de la chaîne de l&#39;agent utilisateur. | <ul><li>USER_AGENT : **obligatoire** chaîne de l’agent utilisateur.</li></ul> | ua_device_class&#x200B;(USER_AGENT) | ua_device_class&#x200B;(« Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3 ») | Téléphone |

{style="table-layout:auto"}

### Fonctions Analytics {#analytics}

>[!NOTE]
>
>Vous ne pouvez utiliser que les fonctions d’analyse suivantes pour les flux WebSDK et Adobe Analytics.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| aa_get_event_id | Extrait l’identifiant d’événement d’une chaîne d’événement Analytics. | <ul><li>EVENT_STRING : **obligatoire** chaîne d’événement Analytics séparée par des virgules.</li><li>EVENT_NAME : **Obligatoire** nom de l’événement à extraire et identifiant de celui-ci.</li></ul> | aa_get_event_id(EVENT_STRING, EVENT_NAME) | aa_get_event_id(« event101=5:123456,scOpen », « event101 ») | 123456 |
| aa_get_event_value | Extrait la valeur de l’événement d’une chaîne d’événement Analytics. Si la valeur de l’événement n’est pas spécifiée, 1 est renvoyée. | <ul><li>EVENT_STRING : **obligatoire** chaîne d’événement Analytics séparée par des virgules.</li><li>EVENT_NAME : **Obligatoire** nom de l’événement duquel extraire une valeur.</li></ul> | aa_get_event_value(EVENT_STRING, EVENT_NAME) | aa_get_event_value(« event101=5:123456,scOpen », « event101 ») | 5 |
| aa_get_product_categories | Extrait la catégorie de produits d’une chaîne de produits Analytics. | <ul><li>PRODUCTS_STRING : **obligatoire** chaîne de produits Analytics.</li></ul> | aa_get_product_categories(PRODUCTS_STRING) | aa_get_product_categories( »;Exemple de produit 1;1;3.50,Exemple de catégorie 2;Exemple de produit 2;1;5.99 ») | [null,« Exemple catégorie 2 »] |
| aa_get_product_names | Extrait le nom du produit d’une chaîne de produits Analytics. | <ul><li>PRODUCTS_STRING : **obligatoire** chaîne de produits Analytics.</li></ul> | aa_get_product_names(PRODUCTS_STRING) | aa_get_product_names( »;Exemple de produit 1;1;3.50,Exemple de catégorie 2;Exemple de produit 2;1;5.99 ») | [« Exemple de produit 1 »,« Exemple de produit 2 »] |
| aa_get_product_quantity | Extrait les quantités d’une chaîne de produits Analytics. | <ul><li>PRODUCTS_STRING : **obligatoire** chaîne de produits Analytics.</li></ul> | aa_get_product_quantity(PRODUCTS_STRING) | aa_get_product_quantity( »;Exemple de produit 1;1;3.50,Exemple de catégorie 2;Exemple de produit 2 ») | [« 1 », nul] |
| aa_get_product_price | Extrait le prix d’une chaîne de produits Analytics. | <ul><li>PRODUCTS_STRING : **obligatoire** chaîne de produits Analytics.</li></ul> | aa_get_product_price(PRODUCTS_STRING) | aa_get_product_price( »;Exemple de produit 1;1;3.50,Exemple de catégorie 2;Exemple de produit 2 ») | [« 3.50 », nul] |
| aa_get_product_event_values | Extrait les valeurs de l’événement nommé de la chaîne products sous la forme d’un tableau de chaînes. | <ul><li>PRODUCTS_STRING : **obligatoire** chaîne de produits Analytics.</li><li>EVENT_NAME : **Obligatoire** nom de l’événement duquel extraire les valeurs.</li></ul> | aa_get_product_event_values(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_values( »;Exemple de produit 1;1;4.20;event1=2.3\|event2=5:1,;Exemple de produit 2;1;4.20;event1=3\|event2=2:2 », « event1 ») | [« 2.3 », « 3 »] |
| aa_get_product_evars | Extrait les valeurs d’evar de l’événement nommé de la chaîne products sous la forme d’un tableau de chaînes. | <ul><li>PRODUCTS_STRING : **obligatoire** chaîne de produits Analytics.</li><li>EVAR_NAME : **obligatoire** nom d’eVar à extraire.</li></ul> | aa_get_product_evars(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_evars( »;Exemple de produit;1;6.69;;eVar1=Valeur de marchandisage », « eVar1 ») | [ « Valeur de marchandisage »] |

{style="table-layout:auto"}

<!-- | aa_get_product_events | Extracts a named event from the products string as an array of objects. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_events(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_events(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | [`{"id": "1","value", "5"}`, `{"id": "2","value", "1"}`] |
| aa_get_product_event_ids | Extracts the IDs for the named event from the products string as an array of strings. | <ul><li>PRODUCTS_STRING: **Required** The Analytics products string.</li><li>EVENT_NAME: **Required** The event name to extract values from.</li></ul> | aa_get_product_event_ids(PRODUCTS_STRING, EVENT_NAME) | aa_get_product_event_ids(";Example product 1;1;4.20;event1=2.3\|event2=5:1,;Example product 2;1;4.20;event1=3\|event2=2:2", "event2") | ["1", "2"] | -->

### Copie d’objet {#object-copy}

>[!TIP]
>
>La fonction de copie d’objet est automatiquement appliquée lorsqu’un objet de la source est mappé à un objet du XDM. Aucune action supplémentaire n’est nécessaire de la part des utilisateurs.

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

Le mappage devient alors :

```json
address -> addr
address.line1 -> addr.addrLine1
```

Dans l’exemple ci-dessus, les attributs `city` et `state` sont également ingérés automatiquement au moment de l’exécution, car l’objet `address` est mappé à `addr`. Si vous deviez créer un attribut `line2` dans la structure XDM et que vos données d’entrée contiennent également un `line2` dans l’objet `address` , il sera également ingéré automatiquement sans avoir à modifier manuellement le mappage.

Pour que le mappage automatique fonctionne, les conditions préalables suivantes doivent être remplies :

* Les objets au niveau du parent doivent être mappés ;
* De nouveaux attributs doivent avoir été créés dans le schéma XDM ;
* Les nouveaux attributs doivent avoir des noms correspondants dans le schéma source et le schéma XDM.

Si l’une des conditions préalables n’est pas remplie, vous devez mapper manuellement le schéma source au schéma XDM à l’aide de la préparation des données.

## Annexe

Vous trouverez ci-dessous des informations supplémentaires sur l’utilisation des fonctions de mappage de la préparation des données

### Caractères spéciaux {#special-characters}

Le tableau ci-dessous présente une liste des caractères réservés et les caractères codés correspondants.

| Caractère réservé | Caractère codé |
| --- | --- |
| space | %20 |
| ! | %21 |
| « | %22 |
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
| &lbrack; | %5B |
| | | %5C |
| &rbrack; | %5J |
| ^ | %5E |
| &grave; | %60 |
| ~ | %7E |

{style="table-layout:auto"}

### Valeurs de champ de l’appareil {#device-field-values}

Le tableau ci-dessous présente une liste des valeurs de champ d’appareil et leurs descriptions correspondantes.

| Appareil | Description |
| --- | --- |
| Bureau | Un ordinateur de bureau ou un ordinateur portable. |
| Anonymisé | Un appareil anonyme. Dans certains cas, ces `useragents` ont été modifiées par un logiciel d’anonymisation. |
| Inconnu | Un appareil inconnu. Il s’agit généralement de `useragents` qui ne contiennent aucune information sur le périphérique. |
| Mobile | Appareil mobile qui n’a pas encore été identifié. Cet appareil mobile peut être un eReader, une tablette, un téléphone, une montre, etc. |
| Tablette | Appareil mobile avec un grand écran (généralement > 7 pouces). |
| Téléphone | Appareil mobile doté d’un petit écran (généralement &lt; 7 pouces). |
| Regarder | Appareil mobile doté d’un petit écran (généralement &lt; 2 pouces). Ces appareils fonctionnent normalement comme un écran supplémentaire pour un appareil de type téléphone/tablette. |
| Réalité Augmentée | Un appareil mobile avec des fonctionnalités de réalité augmentée. |
| Réalité Virtuelle | Un appareil mobile avec des fonctionnalités de réalité virtuelle. |
| Reader | Appareil similaire à une tablette, mais généralement doté d’un écran [!DNL eInk]. |
| Décodeur | Un appareil connecté qui permet une interaction via un écran de la taille d’un téléviseur. |
| TV | Un appareil similaire au décodeur, mais intégré au téléviseur. |
| Appareil Électroménager | Appareil ménager (généralement de grande taille), tel qu’un réfrigérateur. |
| Console de jeux | Un système de jeu fixe comme un [!DNL Playstation] ou un [!DNL XBox]. |
| Console de jeu portable | Un système de jeu mobile comme un [!DNL Nintendo Switch]. |
| Voix | Appareil à commande vocale tel qu’un [!DNL Amazon Alexa] ou un [!DNL Google Home]. |
| Voiture | Un navigateur basé sur un véhicule. |
| Robot | Des robots qui visitent un site web. |
| Robot Mobile | Robots qui visitent un site web, mais qui indiquent qu’ils souhaitent être considérés comme des visiteurs mobiles. |
| Imitateur Robot | Des robots qui visitent un site web, prétendant être des robots comme [!DNL Google], mais ce n&#39;est pas le cas. **Note** : Dans la plupart des cas, les imitateurs de robots sont en effet des robots. |
| Cloud | Une application cloud. Ce ne sont ni des robots ni des hackers, mais des applications qui doivent se connecter. Cela inclut les serveurs [!DNL Mastodon]. |
| Hacker | Cette valeur d’appareil est utilisée si un script est détecté dans la chaîne de `useragent`. |

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

