---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;mapping fields;mapping functions;
solution: Experience Platform
title: Fonctions d’aperçu des données
topic: overview
description: Ce document présente les fonctions de mappage utilisées avec l’API de données.
translation-type: tm+mt
source-git-commit: 6deb8f5e11b87550601679f06c8445d90fd22709
workflow-type: tm+mt
source-wordcount: '3459'
ht-degree: 19%

---


# Fonctions d’aperçu des données

Les fonctions d’aperçu de données peuvent être utilisées pour calculer et calculer des valeurs en fonction de ce qui est entré dans les champs source.

## Champs

Un nom de champ peut être n’importe quel identifiant légal - une séquence illimitée de lettres et de chiffres Unicode, commençant par une lettre, le signe dollar (`$`) ou le caractère de soulignement (`_`). Les noms de variables sont également sensibles à la casse.

Si un nom de champ n’est pas conforme à cette convention, le nom de champ doit être enveloppé avec `${}`. Ainsi, par exemple, si le nom du champ est &quot;Prénom&quot; ou &quot;Prénom.Nom&quot;, le nom doit être encapsulé comme `${First Name}` ou `${First.Name}` respectivement.

En outre, les noms de champ sont **l&#39;un des** mots-clés réservés suivants, ils doivent être encapsulés avec `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

Les données des sous-champs sont accessibles à l’aide de la notation point. Par exemple, s’il y avait un `name` objet, pour accéder au `firstName` champ, utilisez `name.firstName`.

## Liste des fonctions

Les tableaux ci-dessous liste toutes les fonctions de mappage prises en charge, y compris les exemples d’expressions et les résultats obtenus.

### Fonctions de chaîne

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
-------- | ----------- | ---------- | -------| ---------- | -------------
| concat | Concatène les chaînes données. | <ul><li>CHAÎNE : Chaînes qui seront concaténées.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| explode | Divise la chaîne sur base d’un regex et renvoie un tableau de parties. Peut éventuellement inclure regex pour fractionner la chaîne. Par défaut, le fractionnement prend la valeur &quot;,&quot;. | <ul><li>CHAÎNE : **Obligatoire** Chaîne à fractionner.</li><li>REGEX : *Facultatif* expression régulière qui peut être utilisée pour fractionner la chaîne.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hi, there!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Renvoie l’emplacement/l’index d’une sous-chaîne. | <ul><li>ENTRÉE : **Obligatoire** Chaîne recherchée.</li><li>SOUS-CHAÎNE : **Obligatoire** Sous-chaîne recherchée dans la chaîne.</li><li>DÉBUT_POSITION : *Facultatif* Emplacement de l’emplacement où début la recherche dans la chaîne.</li><li>OCCURRENCE : *Facultatif* La énième occurrence à rechercher à partir de la position du début. Par défaut, elle est définie sur 1. </li></ul> | instruction(INPUT, SUBSTRING, DÉBUT_POSITION, OCCURRENCE) | instr(&quot;adobe`<span>`.com&quot;, &quot;com&quot;) | 6 |
| replacestr | Remplace la chaîne de recherche si elle est présente dans la chaîne d’origine. | <ul><li>ENTRÉE : **Obligatoire** Chaîne d’entrée.</li><li>TO_FIND : **Obligatoire** Chaîne à rechercher dans l’entrée.</li><li>TO_REPLACE : **Obligatoire** Chaîne qui remplacera la valeur dans &quot;TO_FIND&quot;.</li></ul> | replacestr(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;This is a string replace test&quot; |
| substr | Renvoie une sous-chaîne d’une longueur donnée. | <ul><li>ENTRÉE : **Obligatoire** Chaîne d’entrée.</li><li>DÉBUT_INDEX : **Obligatoire** Index de la chaîne d’entrée où début la sous-chaîne.</li><li>LENGTH: **Required** The length of the substring.</li></ul> | translate(INPUT, DÉBUT_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Convertit une chaîne en minuscules. | <ul><li>ENTRÉE : **Obligatoire** Chaîne qui sera convertie en minuscules.</li></ul> | lower(INPUT) | lower(&quot;HeLLo&quot;)<br>lcase(&quot;HeLLo&quot;) | &quot;hello&quot; |
| upper /<br>ucase | Convertit une chaîne en majuscules. | <ul><li>ENTRÉE : **Obligatoire** Chaîne qui sera convertie en majuscules.</li></ul> | upper(INPUT) | upper(&quot;HeLLo&quot;)<br>ucase(&quot;HeLLo&quot;) | &quot;HELLO&quot; |
| split | Divise une chaîne d’entrée sur un séparateur. | <ul><li>ENTRÉE : **Obligatoire** Chaîne d’entrée qui va être fractionnée.</li><li>SÉPARATEUR : **Obligatoire** Chaîne utilisée pour fractionner l’entrée.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Joint une liste d’objets à l’aide du séparateur. | <ul><li>SÉPARATEUR : **Obligatoire** Chaîne qui sera utilisée pour joindre les objets.</li><li>OBJETS : **Obligatoire** Tableau de chaînes qui seront jointes.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | Applique une pression sur le côté gauche d’une chaîne avec l’autre chaîne donnée. | <ul><li>ENTRÉE : **Obligatoire** Chaîne qui va être complétée. Cette chaîne peut être nulle.</li><li>COMPTE : **Obligatoire** Taille de la chaîne à ajouter.</li><li>REMPLISSAGE : **Obligatoire** Chaîne avec laquelle ajouter le remplissage de l’entrée. S’il est nul ou vide, il sera traité comme un espace unique.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| rpad | Applique une superposition au côté droit d’une chaîne avec l’autre chaîne donnée. | <ul><li>ENTRÉE : **Obligatoire** Chaîne qui va être complétée. Cette chaîne peut être nulle.</li><li>COMPTE : **Obligatoire** Taille de la chaîne à ajouter.</li><li>REMPLISSAGE : **Obligatoire** Chaîne avec laquelle ajouter le remplissage de l’entrée. S’il est nul ou vide, il sera traité comme un espace unique.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Récupère les premiers caractères &quot;n&quot; de la chaîne donnée. | <ul><li>CHAÎNE : **Obligatoire** Chaîne pour laquelle vous obtenez les premiers caractères &quot;n&quot;.</li><li>COMPTE : **** ObligatoireCaractères &quot;n&quot; que vous souhaitez obtenir à partir de la chaîne.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Récupère les derniers caractères &quot;n&quot; de la chaîne donnée. | <ul><li>CHAÎNE : **Obligatoire** Chaîne pour laquelle vous obtenez les derniers caractères &quot;n&quot;.</li><li>COMPTE : **** ObligatoireCaractères &quot;n&quot; que vous souhaitez obtenir à partir de la chaîne.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Supprime l’espace blanc du début de la chaîne. | <ul><li>CHAÎNE : **Obligatoire** Chaîne dont vous souhaitez supprimer l&#39;espace blanc.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | Supprime l’espace blanc de la fin de la chaîne. | <ul><li>CHAÎNE : **Obligatoire** Chaîne dont vous souhaitez supprimer l&#39;espace blanc.</li></ul> | rtrim(STRING) | rtrim(&quot;hello&quot;) | &quot;hello&quot; |
| trim | Supprime l’espace blanc du début et de la fin de la chaîne. | <ul><li>CHAÎNE : **Obligatoire** Chaîne dont vous souhaitez supprimer l&#39;espace blanc.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| est égal à | Compare deux chaînes pour vérifier si elles sont égales. Cette fonction est sensible à la casse. | <ul><li>STRING1 : **Obligatoire** Première chaîne à comparer.</li><li>STRING2 : **Obligatoire** Deuxième chaîne à comparer.</li></ul> | STRING1.equals(STRING2) | &quot;string1&quot;.equals(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Compare deux chaînes pour vérifier si elles sont égales. Cette fonction **ne respecte pas** la casse. | <ul><li>STRING1 : **Obligatoire** Première chaîne à comparer.</li><li>STRING2 : **Obligatoire** Deuxième chaîne à comparer.</li></ul> | STRING1.equalsIgnoreCase(STRING2) | &quot;string1&quot;.equalsIgnoreCase(&quot;STRING1&quot;) | vrai |

### Fonctions de hachage

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
-------- | ----------- | ---------- | -------| ---------- | -------------
| sha1 | Récupère une entrée et génère une valeur de hachage à l’aide de l’algorithme de hachage sécurisé 1 (SHA-1). | <ul><li>ENTRÉE : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Récupère une entrée et génère une valeur de hachage à l’aide de l’algorithme de hachage sécurisé 256 (SHA-256). | <ul><li>ENTRÉE : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Récupère une entrée et génère une valeur de hachage à l’aide de l’algorithme de hachage sécurisé 512 (SHA-512). | <ul><li>ENTRÉE : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd00 788a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Récupère une entrée et produit une valeur de hachage à l’aide de MD5. | <ul><li>ENTRÉE : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Prend une entrée à l’aide d’un algorithme de contrôle de redondance cyclique (CRC) pour produire un code cyclique de 32 bits. | <ul><li>ENTRÉE : **Obligatoire** Texte brut à hacher.</li><li>CHARSET : *Facultatif* Nom du jeu de caractères. Les valeurs possibles sont UTF-8, UTF-16, ISO-8859-1 et US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

### Fonctions URL

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
-------- | ----------- | ---------- | -------| ---------- | -------------
| get_url_protocol | Renvoie le protocole à partir de l’URL donnée. Si l’entrée n’est pas valide, elle renvoie null. | <ul><li>URL : **Obligatoire** URL à partir de laquelle le protocole doit être extrait.</li></ul> | get_url_protocol(URL) | get_url_protocol(&quot;https://platform.adobe.com/home&quot;) | https |
| get_url_host | Renvoie l’hôte de l’URL donnée. Si l’entrée n’est pas valide, elle renvoie null. | <ul><li>URL : **Obligatoire** URL à partir de laquelle l&#39;hôte doit être extrait.</li></ul> | get_url_host(URL) | get_url_host(&quot;https://platform.adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Renvoie le port de l’URL donnée. Si l’entrée n’est pas valide, elle renvoie null. | <ul><li>URL : **Obligatoire** URL à partir de laquelle le port doit être extrait.</li></ul> | get_url_port(URL) | get_url_port(&quot;sftp://example.com//home/joe/employee.csv&quot;) | 22 |
| get_url_path | Renvoie le chemin d’accès de l’URL donnée. Par défaut, le chemin complet est renvoyé. | <ul><li>URL : **Obligatoire** URL à partir de laquelle le chemin d’accès doit être extrait.</li><li>FULL_PATH : *Facultatif* Valeur booléenne qui détermine si le chemin complet est renvoyé. Si la valeur est définie sur false, seule la fin du chemin est renvoyée.</li></ul> | get_url_path(URL, FULL_PATH) | get_url_path(&quot;sftp://example.com//home/joe/employee.csv&quot;) | &quot;//home/joe/employee.csv&quot; |
| get_url_requête_str | Renvoie la chaîne de requête d’une URL donnée. | <ul><li>URL : **Obligatoire** URL à partir de laquelle vous tentez d’obtenir la chaîne de requête.</li><li>ANCRAGE : **Obligatoire** Détermine ce qui sera fait avec l&#39;ancre dans la chaîne de requête. Il peut s’agir de l’une des trois valeurs suivantes : &quot;preserve&quot;, &quot;remove&quot; ou &quot;append&quot;.<br><br>Si la valeur est &quot;preserve&quot;, l’ancre est attachée à la valeur renvoyée.<br>Si la valeur est &quot;remove&quot;, l’ancre est supprimée de la valeur renvoyée.<br>Si la valeur est &quot;append&quot;, l’ancre est renvoyée sous forme de valeur distincte.</li></ul> | get_url_requête_str(URL, ANCHOR) | get_url_requête_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;keep&quot;)<br>get_url_requête_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;remove&quot;)<br>get_url_requête_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

### Fonctions de date et d’heure

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
-------- | ----------- | ---------- | -------| ---------- | -------------
| now | Récupère l’heure actuelle. |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | Récupère l’heure Unix actuelle. |  | timestamp() | timestamp() | 1571850624571 |
| format | Formate la date d’entrée selon un format spécifié. | <ul><li>DATE : **Obligatoire** Date d&#39;entrée, en tant qu&#39;objet ZonedDateTime, à formater.</li><li>FORMAT : **Obligatoire** Format de la date à modifier.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;aaaa-MM-jj HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Convertit une date et une heure en chaîne de date selon un format spécifié. | <ul><li>HORODATAGE : **Obligatoire** Horodatage à mettre en forme. Ceci est écrit en millisecondes.</li><li>FORMAT : **Obligatoire** Format dans lequel vous souhaitez modifier l’horodatage.</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23-Oct-2019 11:24&quot; |
| date | Convertit une chaîne de date en objet ZonedDateTime (format ISO 8601). | <ul><li>DATE : **Obligatoire** Chaîne représentant la date.</li><li>FORMAT : **Obligatoire** Chaîne représentant le format de la date.</li><li>DEFAULT_DATE : **Obligatoire** Date par défaut renvoyée, si la date fournie est nulle.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-jj HH:mm&quot;, now()) | &quot;2019-10-23T11:24Z&quot; |
| date | Convertit une chaîne de date en objet ZonedDateTime (format ISO 8601). | <ul><li>DATE : **Obligatoire** Chaîne représentant la date.</li><li>FORMAT : **Obligatoire** Chaîne représentant le format de la date.</li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-jj HH:mm&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date | Convertit une chaîne de date en objet ZonedDateTime (format ISO 8601). | <ul><li>DATE : **Obligatoire** Chaîne représentant la date.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date_part | Récupère les parties de la date. Les valeurs de composant suivantes sont prises en charge : <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;weekday&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecond&quot;<br>&quot;ms&quot; | <ul><li>COMPOSANT : **Obligatoire** Chaîne représentant la partie de la date. </li><li>DATE : **Obligatoire** Date, dans un format standard.</li></ul> | date_part(COMPOSANT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;)) | 10 |
| set_date_part | Remplace un composant à une date donnée. Les composants suivants sont acceptés : <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>COMPOSANT : **Obligatoire** Chaîne représentant la partie de la date. </li><li>VALEUR : **Obligatoire** Valeur à définir pour le composant pour une date donnée.</li><li>DATE : **Obligatoire** Date, dans un format standard.</li></ul> | set_date_part(COMPOSANT, VALEUR, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | Crée une date à partir de parties. Cette fonction peut également être induite à l&#39;aide de make_timestamp. | <ul><li>ANNÉE : **Obligatoire** Année, écrite en quatre chiffres.</li><li>MOIS : **Obligatoire** Mois. Les valeurs autorisées sont comprises entre 1 et 12.</li><li>JOUR : **Obligatoire** Le jour. Les valeurs autorisées sont comprises entre 1 et 31.</li><li>HEURE : **Obligatoire** Heure. Les valeurs autorisées sont comprises entre 0 et 23.</li><li>MINUTE : **Obligatoire** La minute. Les valeurs autorisées sont comprises entre 0 et 59.</li><li>NANOSECOND : **Obligatoire** Valeurs nanosecondes. Les valeurs autorisées sont comprises entre 0 et 9999999999.</li><li>FUSEAU HORAIRE : **Obligatoire** Fuseau horaire pour l&#39;heure de la date.</li></ul> | make_date_time(ANNÉE, MOIS, JOUR, HEURE, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | Convertit une date dans n’importe quel fuseau horaire en une date en UTC. | <ul><li>DATE : **Obligatoire** Date à laquelle vous essayez de convertir.</li></ul> | zone_date_to_utc(DATE) | `zone_date_to_utc(2019-10-17T11:55:12.000000999-07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | Convertit une date d’un fuseau horaire en un autre fuseau horaire. | <ul><li>DATE : **Obligatoire** Date à laquelle vous essayez de convertir.</li><li>ZONE : **Obligatoire** Fuseau horaire dans lequel vous tentez de convertir la date.</li></ul> | zone_date_to_zone(DATE, ZONE) | `zone_date_to_utc(2019-10-17T11:55:12.000000999-07:00[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

### Hiérarchies - Objets

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
-------- | ----------- | ---------- | -------| ---------- | -------------
| size_of | Renvoie la taille de l’entrée. | <ul><li>ENTRÉE : **Obligatoire** Objet dont vous essayez de trouver la taille.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | Vérifie si un objet est vide ou non. | <ul><li>ENTRÉE : **Obligatoire** L&#39;objet que vous essayez de vérifier est vide.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| array_to_object | Crée une liste d’objets. | <ul><li>ENTRÉE : **Obligatoire** Groupe de paires clé/tableau.</li></ul> | array_to_object(INPUT) | exemple de besoin | exemple de besoin |
| to_object | Crée un objet basé sur les paires clé/valeur plate données. | <ul><li>ENTRÉE : **Obligatoire** liste plate de paires clé/valeur.</li></ul> | to_object(INPUT) | to_object(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Crée un objet à partir de la chaîne d’entrée. | <ul><li>CHAÎNE : **Obligatoire** Chaîne analysée pour créer un objet.</li><li>VALUE_DELIMITER : *Facultatif* Délimiteur séparant un champ de la valeur. The default delimiter is `:`.</li><li>FIELD_DELIMITER : *Facultatif* Délimiteur séparant les paires valeur-champ. The default delimiter is `,`.</li></ul> | str_to_object(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | téléphone - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | Vérifie si l’objet existe dans les données source. | <ul><li>ENTRÉE : **Obligatoire** Chemin à vérifier s&#39;il existe dans les données source.</li></ul> | is_set(INPUT) | is_set(&quot;evars.evar.field1&quot;) | vrai |
| nullify | Définit la valeur de l’attribut sur `null`. Il doit être utilisé lorsque vous ne souhaitez pas copier le champ dans le schéma de cible. |  | nullify() | nullify() | `null` |

### Hiérarchies - Tableaux

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
-------- | ----------- | ---------- | -------| ---------- | -------------
| coalesce | Renvoie le premier objet non nul dans un tableau donné. | <ul><li>ENTRÉE : **Obligatoire** Tableau dont vous souhaitez trouver le premier objet non nul.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | Récupère le premier élément du tableau donné. | <ul><li>ENTRÉE : **Obligatoire** Tableau dont vous souhaitez trouver le premier élément.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Récupère le dernier élément du tableau donné. | <ul><li>ENTRÉE : **Obligatoire** Tableau dont vous souhaitez trouver le dernier élément.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| to_array | Prend une liste d&#39;entrées et la convertit en tableau. | <ul><li>INCLUDE_NULLS : **Obligatoire** Valeur booléenne indiquant si l&#39;inclusion de nulls dans le tableau de réponses doit être indiquée ou non.</li><li>VALEURS : **Obligatoire** Éléments à convertir en tableau.</li></ul> | to_array(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

### Opérateurs logiques

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
-------- | ----------- | ---------- | -------| ---------- | -------------
| decode | Étant donné qu’une clé et une liste de paires clé-valeur sont aplaties dans un tableau, la fonction renvoie la valeur si la clé est trouvée ou renvoie une valeur par défaut si elle est présente dans le tableau. | <ul><li>CLÉ : **Obligatoire** Clé à faire correspondre.</li><li>OPTIONS : **Obligatoire** Tableau aplati de paires clé/valeur. Une valeur par défaut peut éventuellement être placée à la fin.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Si le code d&#39;état donné est &quot;ca&quot;, &quot;California&quot;.<br>Si le code d&#39;état donné est &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Si le code d’état ne correspond pas à ce qui suit, &quot;S/O&quot;. |
| iif | Évalue une expression booléenne donnée et renvoie la valeur spécifiée en fonction du résultat. | <ul><li>BOOLEAN_EXPRESSION : **Obligatoire** expression booléenne en cours d&#39;évaluation.</li><li>TRUE_VALUE : **Obligatoire** Valeur renvoyée si l’expression est évaluée sur true.</li><li>FALSE_VALUE : **Obligatoire** Valeur renvoyée si l’expression prend la valeur false.</li></ul> | iif(EXPRESSION_BOOLEAN, VALUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

### Agrégation

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
-------- | ----------- | ---------- | -------| ---------- | -------------
| min | Renvoie le minimum des arguments donnés. Utilise l’ordre naturel. | <ul><li>OPTIONS : **Obligatoire** Un ou plusieurs objets pouvant être comparés les uns aux autres.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Renvoie le maximum des arguments donnés. Utilise l’ordre naturel. | <ul><li>OPTIONS : **Obligatoire** Un ou plusieurs objets pouvant être comparés les uns aux autres.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

### Conversions de type

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
-------- | ----------- | ---------- | -------| ---------- | -------------
| to_bigint | Convertit une chaîne en un BigInteger. | <ul><li>CHAÎNE : **Obligatoire** Chaîne à convertir en BigInteger.</li></ul> | to_bigint(STRING) | to_bigint(&quot;1000000.34&quot;) | 1000000.34 |
| to_decimal | Convertit une chaîne en Doublon. | <ul><li>CHAÎNE : **Obligatoire** Chaîne à convertir en Doublon.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | Convertit une chaîne en une chaîne flottante. | <ul><li>CHAÎNE : **Obligatoire** Chaîne à convertir en Float.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | Convertit une chaîne en entier. | <ul><li>CHAÎNE : **Obligatoire** Chaîne à convertir en entier.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

### Fonctions JSON

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
-------- | ----------- | ---------- | -------| ---------- | -------------
| json_to_object | Désérialisez le contenu JSON à partir de la chaîne donnée. | <ul><li>CHAÎNE : **Obligatoire** Chaîne JSON à désérialiser.</li></ul> | json_to_object(STRING) | json_to_object({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot; : &quot;Doe&quot;}}) | Objet représentant le fichier JSON. |

### Opérations spéciales

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
-------- | ----------- | ---------- | -------| ---------- | -------------
| uuid /<br>guid | Génère un identifiant pseudo-aléatoire. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fcda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c20633 |

### Fonctions de l&#39;agent utilisateur

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour consulter l’intégralité du tableau.

| Fonction | Description | Paramètres | Syntaxe | Expression | Exemple de résultat |
-------- | ----------- | ---------- | -------| ---------- | -------------
| ua_os_name | Extrait le nom du système d’exploitation de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_os_name(USER_AGENT) | ua_os_name(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Extrait la version principale du système d’exploitation de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_os_version_major(USER_AGENT) | ua_os_version_major(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Extrait la version du système d’exploitation de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_os_version(USER_AGENT) | ua_os_version(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Extrait le nom et la version du système d’exploitation de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_os_name_version(USER_AGENT) | ua_os_name_version(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Extrait la version de l’agent de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_agent_version(USER_AGENT) | ua_agent_version(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | Extrait le nom de l’agent et la version principale de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_agent_version_major(USER_AGENT) | ua_agent_version_major(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Extrait le nom de l’agent de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_agent_name(USER_AGENT) | ua_agent_name(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Extrait la classe de périphérique de la chaîne de l’agent utilisateur. | <ul><li>USER_AGENT : **Obligatoire** Chaîne de l’agent utilisateur.</li></ul> | ua_device_class(USER_AGENT) | ua_device_class(&quot;Mozilla/5.0 (iPhone ; CPU iPhone OS 5_1_1 comme Mac OS X) AppleWebKit/534.46 (KHTML, comme Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Téléphone |