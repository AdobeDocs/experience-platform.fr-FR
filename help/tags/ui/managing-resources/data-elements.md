---
title: Éléments de données
description: Les éléments de données sont les blocs de construction de votre dictionnaire de données (ou mappage de données). Utilisez des éléments de données pour recueillir, organiser et diffuser des données dans les technologies marketing et publicitaires.
exl-id: 1e7b03cc-5a54-403d-bf8d-dbc206cfeb2d
source-git-commit: 0956a28a8ff6eacb3a55f7c333293ed5b6c81cce
workflow-type: tm+mt
source-wordcount: '1614'
ht-degree: 91%

---

# Éléments de données

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Les éléments de données sont les blocs de construction de votre dictionnaire de données (ou mappage de données). Utilisez des éléments de données pour recueillir, organiser et diffuser des données dans les technologies marketing et publicitaires.

Un seul élément de données est une variable dont la valeur peut être mappée à des chaînes de requête, des URL, des valeurs de cookie, des variables JavaScript, etc. Vous pouvez référencer cette valeur par son nom de variable dans Adobe Experience Platform. Cette collection d’éléments de données devient le dictionnaire des données définies que vous pouvez utiliser pour créer vos règles (événements, conditions et actions). Ce dictionnaire de données est partagé entre les balises afin d’être utilisé avec toute extension ajoutée à votre propriété.

>[!IMPORTANT]
>
>Les modifications ne prennent effet que lorsqu’elles sont [publiées](../publishing/overview.md).

Utilisez les éléments de données autant que possible lors de la création de règles pour consolider la définition des données dynamiques et optimiser l’efficacité de votre processus de balisage. Vous définissez les règles de données une seule fois et vous pouvez ensuite les utiliser en plusieurs endroits.

Les éléments de données réutilisables sont efficaces et devraient être utilisés en tant que bonnes pratiques.

Par exemple, si vous référencez de manière particulière les noms de page ou les ID de produit ou si vous obtenez des informations des paramètres de chaîne de requête à partir d’un lien marketing affilié ou de [!DNL AdWords], etc., vous pouvez créer un dictionnaire de données (éléments de données) en obtenant des informations de plusieurs sources et en utilisant ces données dans différentes règles de balises.

En prenant l’utilisation des noms de page comme exemple, supposons que vous utilisez un schéma page-nom spécifique en référençant une couche de données, l’élément `document.title` ou une balise de titre dans le site web. Les balises dans Adobe Experience Platform vous permettent de créer un élément de données comme point de référence unique pour ce point de données particulier. Vous pouvez ensuite utiliser cet élément de données dans n’importe quelle règle qui doit référencer le nom de page. Si pour une raison quelconque, vous décidez à l’avenir de modifier la manière dont vous référencez les noms de page (vous avez par exemple référencé `document.title` et vous souhaitez à présent référencer une couche de données spécifique), il n’est pas nécessaire de modifier plusieurs règles différentes pour changer cette référence. Il suffit de modifier la référence une seule fois dans l’élément de données. Toutes les règles référençant cet élément de données sont alors automatiquement mises à jour.

>[!NOTE]
>
>Si un élément de données n’est pas référencé dans une règle, il n’est pas chargé dans la page, à moins qu’il ne soit appelé dans un script personnalisé.

Les éléments de données sont remplis par des données lorsqu’ils sont utilisés dans des règles ou lorsqu’ils sont appelés manuellement dans un script. À un haut niveau, vous :

1. [créez un élément de données](#create-a-data-element), le cas échéant ;
1. utilisez l’élément de données dans une [règle](./rules.md) ou un script personnalisé.

## Utilisation des éléments de données

### In rules

Vous pouvez utiliser des éléments de données dans l’interface d’édition de règles à l’aide de la zone de recherche pour rechercher le nom de votre élément de données.

### In custom script

Vous pouvez utiliser des éléments de données dans des scripts personnalisés à l’aide de la syntaxe d’objet `_satellite` :

`_satellite.getVar('data element name');`

## Créer un élément de données {#create-a-data-element}

Les éléments de données constituent les blocs de construction des règles. Ils vous permettent de créer un dictionnaire de données (ou mappage de données) des éléments utilisés couramment sur une page, indépendamment de leur origine (chaînes de requête, URL ou valeurs de cookie), pour n’importe quel objet contenu sur le site.

1. Sur une page Propriété, ouvrez lʼonglet [!UICONTROL Éléments de données], puis sélectionnez **[!UICONTROL Créer un élément de données]**.
1. Nommez l’élément de données.
1. Sélectionnez une extension et un type.

   Les types d’éléments de données disponibles sont déterminés par l’extension. Pour plus d’informations sur les types disponibles avec l’extension de balise Core, reportez-vous à [Types d&#39;éléments de données](data-elements.md#types-of-data-elements).

1. Fournissez toutes les informations demandées à propos du type choisi dans les champs fournis.
1. (Facultatif) Saisissez une valeur par défaut.

   Si vous ne sélectionnez pas cette option, il n’existe aucune valeur par défaut. La plupart des utilisateurs conservent cet état par défaut. Différents systèmes traitent différemment une variable vide. Certaines personnes choisissent de saisir une valeur telle que « aucune » ou « s/o » pour garder une cohérence dans les rapports lorsque l’élément de données ne renvoie pas de valeur.

1. Indiquez si vous voulez forcer une valeur minuscule et si vous souhaitez supprimer des sauts de ligne et des espaces.
1. Sélectionnez une durée.

   Les choix disponibles sont les suivants :

   * Aucun
      * The value is not stored.
   * Page view
      * La valeur est maintenue dans une variable JavaScript jusqu’à ce que la page soit actualisée ou qu’une nouvelle page soit chargée.
      * Peut être créé et défini dans des scripts à l’aide de la syntaxe d’objet `_satellite` :

        `_satellite.setVar('data_element_name')`
   * Session
      * Les valeurs persistent dans le stockage de session du navigateur jusqu’à ce que l’onglet du navigateur soit fermé.
      * Disponible tout au long de la visite du site.
   * Visitor
      * La valeur est stockée indéfiniment dans le stockage local du navigateur.

1. Sélectionnez **[!UICONTROL Enregistrer]**.

Lors de la création ou de la modification d’éléments, vous pouvez enregistrer et créer une [bibliothèque active](../publishing/libraries.md#active-library). Cette opération enregistre immédiatement votre modification dans votre bibliothèque et exécute une version. Le statut de la version s’affiche. Vous pouvez également créer une bibliothèque à partir de la liste déroulante [!UICONTROL Bibliothèque active].

## Types d’éléments de données {#types-of-data-elements}

>[!NOTE]
>
>Les types d’éléments de données sont déterminés par l’extension. Les types qui peuvent être créés ne sont pas limités.

Les sections suivantes décrivent les types d’éléments de données disponibles dans l’ **extension Core**. D’autres extensions utilisent d’autres types d’éléments de données.

### Cookie

Tout cookie de domaine disponible peut être référencé dans le champ du nom du cookie.

#### Exemple :

`cookieName`

### Custom code

Il est possible dʼentrer du code JavaScript personnalisé dans lʼinterface utilisateur en cliquant sur [!UICONTROL Ouvrir lʼéditeur] et en insérant le code dans la fenêtre de lʼéditeur.

Une instruction de retour est nécessaire dans la fenêtre de l’éditeur afin d’indiquer quelle valeur doit être définie en tant que valeur de l’élément de données. Si aucune instruction de retour n’est incluse, l’élément de données est résolu sur `undefined`. Cela déclenche une recherche de secours pour une valeur stockée, puis pour une valeur par défaut si aucune valeur stockée n’est présente.

**Exemple :**

```text
var pageType = $('div.page-wrapper').attr('class').split('')[1];
if (window.location.pathname == '/') {
  return 'homepage';
} else {
  return pageType;
}
```

Le code personnalisé peut accepter `event` l’objet de la règle d’appel comme argument. Cela permet au code d’y lire la valeur.

**Exemple :**

```text
// `event` is the default object provided by the rule
var eventType = event.$type;
return eventType; // if this data element is called from a "DOM Ready" event, then `core.dom-ready` is returned
```

Vous pouvez alors les utiliser dans des scripts personnalisés à l’aide de la `_satellite` syntaxe d’objet :

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

Lors de l’utilisation de la syntaxe percent (`%`), il vous suffit de spécifier le nom de l’élément de données. Vous n&#39;avez pas besoin de spécifier `event`.

```text
%data element name%
```

### Attribut DOM

N’importe quelle valeur d’élément peut être récupérée (balise div ou H1, par exemple).

#### Exemple :

Chaîne de sélecteur CSS :

`id#dc logo img`

Obtention de la valeur de :

`src`

### Variable JavaScript

N’importe quelle variable ou n’importe quel objet JavaScript peut être référencé à l’aide du champ de chemin d’accès.

Si vous souhaitez collecter des variables JavaScript ou des propriétés d’objet dans vos balises et les utiliser avec l’une de vos extensions ou règles, des éléments de données peuvent être utilisés pour capturer ces valeurs. Ainsi, vous pouvez vous reporter à l’élément de données dans vos règles. Si la source des données venait à changer, il vous suffirait de modifier la référence à la source (l’élément de données) à un seul emplacement.

Par exemple, supposons que vos balises contiennent une variable JavaScript nommée « `Page_Name` » comme illustré ci-dessous :

```markup
<script>
  //data layer
  var Page_Name = "Homepage"
</script>
```

Vous devez indiquer le chemin d’accès à cette variable lorsque vous créez l’élément de données.

Si vous utilisez un objet collecteur de données dans votre couche de données, utilisez simplement la notation point dans le chemin pour faire référence à l’objet et la propriété que vous souhaitez capturer dans l’élément de données, par exemple `_myData.pageName`, `digitalData.pageName`, etc.

#### Exemple :

`window.document.title`

### Stockage local

Indiquez le nom de votre élément de stockage local dans le champ [!UICONTROL Local Storage Item Name].

Le stockage local permet aux navigateurs de stocker des informations d’une page à l’autre ([https://www.w3schools.com/html/html5_webstorage.asp](https://www.w3schools.com/html/html5_webstorage.asp)). Le stockage local est très similaire aux cookies, mais est beaucoup plus volumineux et plus souple.

Utilisez le champ fourni pour spécifier la valeur que vous avez créée pour un élément de stockage local, comme `lastProductViewed.`

### Informations sur la page

Utilisez ces points de données pour recueillir les informations sur la page à utiliser dans la logique votre règle ou pour envoyer des informations à [!DNL Analytics] ou à des systèmes de suivi externes.

Vous pouvez sélectionner l’un des attributs de page suivants à utiliser dans votre élément de données :

* URL
* Hostname
* Nom du chemin
* Protocol
* Référent
* Title

### Query String Parameter

Spécifiez un paramètre dʼURL unique dans le champ [!UICONTROL URL Parameter].

Seule la section de nom est nécessaire. Les indicateurs spéciaux tels que « ? » ou « = » doivent être omis.

#### Exemple :

`contentType`

### Nombre aléatoire

Utilisez cet élément de données pour générer un nombre aléatoire. Il est souvent utilisé pour échantillonner des données ou pour créer des identifiants, tels qu’un identifiant d’accès. Le nombre aléatoire peut également être utilisé pour obscurcir ou appliquer un salage aux données sensibles. Voici quelques exemples :

* Générer un ID d’accès
* Concaténer le nombre à un jeton utilisateur ou à un horodatage pour garantir l’unicité
* Réaliser un hachage unidirectionnel sur des données personnelles identifiables (PII)
* Déterminer de manière aléatoire à quel moment il convient d’afficher une demande d’enquête sur le site

Indiquez les valeurs minimale et maximale de votre nombre aléatoire.

**Valeurs par défaut :**

Minimum : 0

Maximum : 1 000 000 000

### Stockage de session

Indiquez le nom de votre élément de stockage de session dans le champ [!UICONTROL Session Storage Item Name].

Le stockage de session est similaire au stockage local, sauf que les données sont perdues une fois la session terminée, alors qu’un stockage local ou un cookie peut conserver les données.

### Comportement du visiteur

Similaire aux informations sur la page, cet élément de données utilise des types de comportements courants pour enrichir la logique dans les règles ou d’autres solutions Platform.

Sélectionnez l’un des attributs de comportement du visiteur suivants :

* Page de destination
* Traffic source
* Minutes on site
* Session count
* Session page view count
* Lifetime page view count
* Is new visitor

Voici quelques cas d’utilisation courants :

* Afficher une enquête une fois qu’un visiteur a consulté le site pendant cinq minutes
* S’il s’agit de la page de destination de la visite, renseigner une mesure [!DNL Analytics]
* Afficher une nouvelle offre au visiteur après un nombre de sessions égal à X
* Afficher un abonnement à la newsletter s’il s’agit d’un nouveau visiteur

## Éléments de données intégrés

Vous devez créer des éléments de données personnalisés supplémentaires si vous avez déjà utilisé l’un des éléments de données suivants :

* URI
* Protocol
* Hostname
