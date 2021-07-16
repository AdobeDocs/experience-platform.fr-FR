---
title: Manifeste d’extensions
description: Découvrez comment configurer un fichier de manifeste JSON informant Adobe Experience Platform quant à la manière correcte de consommer votre extension.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '2647'
ht-degree: 77%

---

# Manifeste d’extensions

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Dans le répertoire de base de votre extension, vous devez créer un fichier appelé `extension.json`. Cette section contient des détails importants sur votre extension, ce qui permet à Adobe Experience Platform de l’utiliser correctement. Certains contenus sont formés à l’instar du [npm `package.json`](https://docs.npmjs.com/files/package.json) de npm.

Vous trouverez un exemple d’extension `extension.json` dans le référentiel Github de l’[extension Hello World](https://github.com/adobe/reactor-helloworld-extension/blob/master/extension.json).

Un manifeste d’extensions doit être constitué des éléments suivants :

| Propriété | Description |
| --- | --- |
| `name` | Nom de l’extension. Il doit être différent du nom de toutes les autres extensions Reactor et doit respecter les [règles de nommage](#naming-rules). **Il est utilisé par les balises comme identifiant et ne doit pas être modifié après la publication de votre extension.** |
| `platform` | La plateforme de votre extension. La seule valeur acceptée pour le moment est `web`. |
| `version` | La version de votre extension. Elle doit respecter le format de version [semver](http://semver.org/). Ce format est cohérent avec le [champ de version npm](https://docs.npmjs.com/files/package.json#version). |
| `displayName` | Le nom lisible de votre extension. Cela sera présenté aux utilisateurs de Platform. Il n’est pas nécessaire de mentionner &quot;balises&quot; ou &quot;extension&quot; ; les utilisateurs savent déjà qu’ils utilisent une extension de balise. |
| `description` | La description de votre extension. Cela sera présenté aux utilisateurs de Platform. Si votre extension permet aux utilisateurs de mettre en œuvre votre produit sur leur site web, décrivez ce que fait votre produit. Il n’est pas nécessaire de mentionner &quot;balises&quot; ou &quot;extension&quot; ; les utilisateurs savent déjà qu’ils utilisent une extension de balise. |
| `iconPath` *(Facultatif)* | Chemin d’accès relatif à l’icône qui s’affichera pour l’extension. Il ne doit pas commencer par une barre oblique. Il doit référencer un fichier SVG avec une extension `.svg`. Le SVG doit être carré et peut être mis à l’échelle par Platform. |
| `author` | L’« auteur » est un objet qui doit être structuré comme suit : <ul><li>`name` : nom de l’auteur de l’extension. Vous pouvez également utiliser le nom de la société ici.</li><li>`url` *(Facultatif)* : URL permettant d’en savoir plus sur l’auteur de l’extension.</li><li>`email` *(Facultatif)* : adresse électronique de l’auteur de l’extension.</li></ul>Ceci est cohérent avec les règles [champ auteur npm](https://docs.npmjs.com/files/package.json#people-fields-author-contributors). |
| `exchangeUrl` *(Requis pour les extensions publiques)* | URL de la liste de votre extension sur Adobe Exchange. Elle doit correspondre au modèle `https://www.adobeexchange.com/experiencecloud.details.######.html`. |
| `viewBasePath` | Chemin d’accès relatif au sous-répertoire contenant toutes vos vues et ressources liées aux vues (HTML, JavaScript, CSS, images). Platform hébergera ce répertoire sur un serveur web et chargera le contenu iframe à partir de celui-ci. Il s’agit d’un champ obligatoire et il ne doit pas commencer par une barre oblique. Par exemple, si toutes vos vues sont contenues dans `src/view/`, la valeur de `viewBasePath` sera `src/view/`. |
| `hostedLibFiles` *(Facultatif)* | Nombre de nos utilisateurs préfèrent héberger tous les fichiers liés aux balises sur leur propre serveur. Ces utilisateurs disposent ainsi d’un niveau de certitude accru quant à la disponibilité des fichiers au moment de l’exécution et peuvent facilement analyser le code à la recherche de failles de sécurité. Si la partie bibliothèque de votre extension doit charger des fichiers JavaScript au moment de l’exécution, il est recommandé d’utiliser cette propriété pour répertorier ces fichiers. Les fichiers répertoriés seront hébergés en même temps que la bibliothèque du runtime de balises. Votre extension peut ensuite charger les fichiers via une URL récupérée à l’aide de la méthode [getHostedLibFileUrl](./turbine.md#get-hosted-lib-file).<br><br>Cette option contient un tableau avec les chemins relatifs des fichiers de bibliothèque tiers qui doivent être hébergés. |
| `main` *(Facultatif)* | Chemin d’accès relatif d’un module de bibliothèque qui doit être exécuté au moment de l’exécution.<br><br>Ce module sera toujours inclus dans la bibliothèque runtime et exécuté. Comme le module est toujours inclus dans la bibliothèque runtime, nous vous recommandons de n’utiliser qu’un module « principal » lorsque cela est absolument nécessaire et de maintenir sa taille de code minimale.<br><br>Il n’est pas garanti que ce module soit exécuté en premier ; d’autres modules peuvent être exécutés avant. |
| `configuration` *(Facultatif)* | Cette section décrit la partie [configuration de l’extension](./configuration.md). Cela est nécessaire si vous avez besoin que les utilisateurs fournissent des paramètres globaux pour l’extension. Voir l’[annexe](#config-object) pour obtenir plus d’informations sur la structure de ce champ. |
| `events` *(Facultatif)* | Tableau de définitions de type [d’événement](./web/event-types.md). Voir la section de l’annexe sur [les définitions de type](#type-definitions) pour la structure de chaque objet du tableau. |
| `conditions` *(Facultatif)* | Tableau de définitions de type de [condition](./web/condition-types.md). Voir la section de l’annexe sur [les définitions de type](#type-definitions) pour la structure de chaque objet du tableau. |
| `actions` *(Facultatif)* | Tableau de définitions de type [d’action](./web/action-types.md). Voir la section de l’annexe sur [les définitions de type](#type-definitions) pour la structure de chaque objet du tableau. |
| `dataElements` *(Facultatif)* | Tableau de définitions de type [d’élément de données](./web/data-element-types.md). Voir la section de l’annexe sur [les définitions de type](#type-definitions) pour la structure de chaque objet du tableau. |
| `sharedModules` *(Facultatif)* | Un tableau d’objets de définition de module partagé. Chaque objet de module partagé dans le tableau doit être structuré comme suit : <ul><li>`name` : nom du module partagé. Veuillez noter que ce nom sera utilisé lors du référencement de modules partagés à partir d’autres extensions, comme décrit dans la section [Modules partagés](./web/shared.md). Ce nom n’est jamais affiché dans aucune interface utilisateur. Il doit être différent de tous les noms des autres modules partagés dans votre extension et doit respecter les [règles d’attribution de noms](#naming-rules). **Il est utilisé par les balises comme identifiant et ne doit pas être modifié après la publication de votre extension.**</li><li>`libPath` : chemin d’accès relatif au module partagé. Il ne doit pas commencer par une barre oblique. Il doit référencer un fichier JavaScript avec une extension `.js`.</li></ul> |

## Annexe

### Règles d’attribution de noms {#naming-rules}

La valeur de tout champ `name` dans `extension.json` doit respecter les règles suivantes :

* Doit être inférieur ou égal à 214 caractères
* Ne doit pas commencer par un point ou un trait de soulignement
* Ne doit pas contenir de majuscules
* Doit uniquement contenir des caractères sécurisés pour les URL

Ces règles sont conformes aux règles [npm package name](https://docs.npmjs.com/files/package.json#name).

### Propriétés de l’objet de configuration {#config-object}

L’objet de configuration doit être structuré comme suit :

<table>
  <thead>
    <tr>
      <th>Propriété</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>viewPath</code></td>
      <td>URL relative à la vue de configuration de l’extension. Elle doit être relative à <code>viewBasePath</code> et ne doit pas commencer par une barre oblique. Elle doit référencer un fichier HTML avec une extension <code>.html</code>. Les suffixes de chaîne de requête et d’identifiant de fragment (hachages) sont acceptables.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Un objet du <a href="http://json-schema.org/">Schéma JSON</a> décrivant le format d’un objet valide enregistré à partir de la vue de configuration de l’extension. Puisque vous êtes le développeur de la vue de configuration, il est de votre responsabilité de vous assurer que tout objet settings enregistré correspond à ce schéma. Ce schéma sera également utilisé pour la validation lorsque les utilisateurs tentent d’enregistrer des données à l’aide des services de Platform <br><br>Voici un exemple d’objet schéma :
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      Nous vous recommandons d’utiliser un outil tel que le <a href="http://www.jsonschemavalidator.net/">Validateur de schémas JSON</a> pour tester manuellement votre schéma.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Facultatif)</em></td>
      <td>Un tableau d’objets dans lequel chaque objet représente une transformation qui doit être effectuée sur chaque objet settings correspondant lorsqu’il est émis dans la bibliothèque du runtime. Consultez la section <a href="#transforms">transformations</a> pour connaître les raisons de ce besoin et la manière dont il est utilisé.</td>
    </tr>
  </tbody>
</table>

### Définitions de type {#type-definitions}

Une définition de type est un objet utilisé pour décrire un type d’événement, de condition, d’action ou d’élément de données. L’objet se compose des éléments suivants :

<table>
  <thead>
    <tr>
      <th>Propriété</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>name</code></td>
      <td>Le nom du type. Il doit s’agir d’un nom unique au sein de l’extension. Le nom doit être conforme aux <a href="#naming-rules">règles d’attribution de noms</a>. <strong>Il est utilisé par les balises comme identifiant et ne doit pas être modifié après la publication de votre extension.</strong></td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>Texte qui sera utilisé pour représenter le type dans l’interface utilisateur de la collecte de données. Il doit être lisible à l’œil.</td>
    </tr>
    <tr>
      <td><code>categoryName</code> <em>(Facultatif)</em></td>
      <td>Lorsqu’il est fourni, le <code>displayName</code> est répertorié sous le <code>categoryName</code> dans l’interface utilisateur de la collecte de données. Tous les types ayant le même <code>categoryName</code> sont répertoriés dans la même catégorie. Par exemple, si votre extension a fourni un type d’événement <code>keyUp</code> et un type d’événement <code>keyDown</code> et qu’ils ont tous deux un <code>categoryName</code> de <code>Keyboard</code>, les deux types d’événement sont répertoriés dans la catégorie Clavier tandis que l’utilisateur effectue une sélection dans la liste des types d’événement disponibles lors de la création d’une règle. La valeur de <code>categoryName</code> doit être lisible à l’œil.</td>
    </tr>
    <tr>
      <td><code>libPath</code></td>
      <td>Chemin d’accès relatif au module Bibliothèque du type. Il ne doit pas commencer par une barre oblique. Il doit référencer un fichier JavaScript avec une extension <code>.js</code>.</td>
    </tr>
    <tr>
      <td><code>viewPath</code> <em>(Facultatif)</em></td>
      <td>L’URL relative à la vue du type. Elle doit être relative à <code>viewBasePath</code> et ne doit pas commencer par une barre oblique. Elle doit référencer un fichier HTML avec une extension <code>.html</code>. Les chaînes de requête et les identificateurs de fragments (hachages) sont acceptables. Si le module de bibliothèque de votre type n’utilise aucun paramètre d’un utilisateur, vous pouvez exclure cette propriété et Platform affichera à la place un espace réservé indiquant qu’aucune configuration n’est nécessaire.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Objet <a href="http://json-schema.org/">Schéma JSON</a> décrivant le format d’un objet settings valide qui peut être enregistré par l’utilisateur. Les paramètres sont généralement configurés et enregistrés par un utilisateur à l’aide de l’interface utilisateur de la collecte de données. Dans ce cas, la vue de l’extension peut prendre les mesures nécessaires pour valider les paramètres fournis par l’utilisateur. D’un autre côté, certains utilisateurs choisissent d’utiliser les API de balises directement sans l’aide d’aucune interface utilisateur. Ce schéma permet à Platform de valider correctement que les objets settings enregistrés par les utilisateurs, qu’une interface utilisateur soit ou non utilisée, sont dans un format compatible avec le module Bibliothèque qui agira sur l’objet settings lors de l’exécution.<br><br>Voici un exemple d’objet schéma :<br>
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties" : {
    "delay" : {
      "type": "number",
      "minimum" : 1
    }
  },
  "required" : [
    "delay"
  ],
  "additionalProperties" : false
}
</pre>
      Nous vous recommandons d’utiliser un outil tel que le <a href="http://www.jsonschemavalidator.net/">Validateur de schémas JSON</a> pour tester manuellement votre schéma.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Facultatif)</em></td>
      <td>Un tableau d’objets dans lequel chaque objet représente une transformation qui doit être effectuée sur chaque objet settings correspondant lorsqu’il est émis dans la bibliothèque du runtime. Consultez la section <a href="#transforms">transformations</a> pour plus d’informations sur les raisons de cette exigence et sur la manière dont il est utilisé.</td>
    </tr>
  </tbody>
</table>

### Transformations {#transforms}

Pour certains cas d’utilisation spécifiques, les extensions ont besoin que les objets settings enregistrés à partir d’une vue soient transformés par Platform avant d’être émis dans la bibliothèque du runtime de balises. Vous pouvez demander qu’une ou plusieurs de ces transformations se produisent en définissant la propriété `transforms` lors de la définition d’une définition de type dans votre `extension.json`. La propriété `transforms` est un tableau d’objets où chaque objet représente une transformation qui doit avoir lieu.

Toutes les transformations nécessitent un `type` et un `propertyPath`. `type` doit être l’un des `function`, `remove` et `file` et décrit la transformation que Platform doit appliquer à l’objet settings. `propertyPath` est une chaîne délimitée par des points qui indique aux balises où trouver la propriété qui doit être modifiée dans l’objet settings. Voici un exemple d’objet settings et quelques `propertyPath` :

```js
{
  foo: {
    bar: "A string",
    baz: [
      "A",
      "B",
      "C"
    ]
  }
}
```

* Si vous définissez `propertyPath` sur `foo.bar`, vous transformerez la valeur `"A string"`.
* Si vous définissez `propertyPath` sur `foo.baz[]`, vous transformerez chaque valeur du tableau `baz`.
* Si vous définissez `propertyPath` sur `foo.baz`, vous transformerez le tableau `baz`.

Les chemins d’accès aux propriétés peuvent utiliser n’importe quelle combinaison de notation de tableau et d’objet pour appliquer des transformations à n’importe quel niveau de l’objet settings.

>[!WARNING]
>
>L’utilisation de la notation de tableau dans l’attribut `propertyPath` (ex. `foo.baz[]`) n’est pas encore prise en charge dans l’extension sandbox*tool.

Les sections ci-dessous décrivent les transformations disponibles et comment les utiliser.

#### Transformation de fonction

La transformation de fonction permet au code écrit par les utilisateurs de Platform d’être exécuté par un module de bibliothèque dans la bibliothèque runtime de balises émise.

Supposons que nous souhaitions fournir un type d’action « script personnalisé ». La vue d’action « script personnalisé » peut fournir une zone de texte dans laquelle l’utilisateur peut entrer du code. Supposons qu’un utilisateur ait saisi le code suivant dans la zone de texte :

`console.log('Welcome, ' + username +'. This is ZomboCom.');`

Lorsque l’utilisateur enregistre la règle, l’objet settings enregistré par la vue peut se présenter comme suit :

```javascript
{
  foo: {
    bar: "console.log('Welcome, ' + username +'. This is ZomboCom.');"
  }
}
```

Lorsqu’une règle utilisant notre action se déclenche dans la bibliothèque du runtime de balises, nous souhaitons exécuter le code de l’utilisateur et lui transmettre un nom d’utilisateur.

Au moment où l’objet settings est enregistré à partir de la vue du type d’action, le code de l’utilisateur est simplement une chaîne. Cela est utile car il peut être correctement sérialisé vers et depuis JSON ; cependant, c’est également mauvais, car il serait généralement émis dans la bibliothèque runtime de balises sous la forme d’une chaîne plutôt que d’une fonction exécutable. Bien que vous puissiez tenter d’exécuter le code dans le module Bibliothèque de votre type d’action à l’aide de [`eval`](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Global_Objects/eval) ou d’une [fonction constructeur](https://developer.mozilla.org/fr-FR/docs/Web/JavaScript/Reference/Objets_globaux/Function), cela est fortement déconseillé en raison de [stratégies de sécurité de contenu](https://developer.mozilla.org/fr-FR/docs/Web/HTTP/CSP) susceptibles de bloquer l’exécution.

Pour pallier ce problème, l’utilisation de la transformation de fonction indique à Platform d’encapsuler le code de l’utilisateur dans une fonction exécutable lorsqu’il est émis dans la bibliothèque du runtime de balise. Pour résoudre le problème de notre exemple, nous définirions la transformation sur la définition de type dans `extension.json` comme suit :

```json
{
  "transforms": [
    {
      "type": "function",
      "propertyPath": "foo.bar",
      "parameters": ["username"]
    }
  ]
}
```

* `type` définit le type de transformation à appliquer à l’objet settings.
* `propertyPath` est une chaîne délimitée par des points qui indique à Platform où trouver la propriété qui doit être modifiée dans l’objet settings.
* `parameters` est un tableau de noms de paramètres qui doit être inclus dans la signature de la fonction d’encapsulation.

Lorsque l’objet settings est émis dans la bibliothèque du runtime de balises, il est transformé comme suit :

```javascript
{
  foo: {
    bar: function(username) {
      console.log('Welcome, ' + username +'. This is ZomboCom.');
    }
  }
}
```

Votre module Bibliothèque peut alors appeler la fonction contenant le code de l’utilisateur et transmettre l’argument `username`.

#### Transformation de fichier

La transformation de fichier permet l’émission de code écrit par les utilisateurs de Platform dans un fichier distinct de la bibliothèque du runtime de balises. Le fichier sera hébergé avec la bibliothèque du runtime de balises et pourra ensuite être chargé selon les besoins de votre extension au moment de l’exécution.

Supposons que nous souhaitions fournir un type d’action « script personnalisé ». La vue du type d’action peut fournir un champ de texte dans lequel l’utilisateur peut saisir du code. Supposons qu’un utilisateur ait saisi le code suivant dans la zone de texte :

`console.log('This is ZomboCom.');`

Lorsque l’utilisateur enregistre la règle, l’objet settings enregistré par la vue peut se présenter comme suit :

```js
{
  foo: {
    bar: "console.log('This is ZomboCom.');"
  }
}
```

Nous souhaitons que le code de l’utilisateur soit placé dans un fichier distinct au lieu d’être inclus dans la bibliothèque du runtime de balises. Lorsqu’une règle utilisant notre action se déclenche dans la bibliothèque du runtime de balises, nous souhaitons charger le code de l’utilisateur en ajoutant un élément de script au corps du document. Pour résoudre le problème de notre exemple, nous définirions la transformation sur la définition de type d’action dans `extension.json` comme suit :

```json
{
  "transforms": [
    {
      "type": "file",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` définit le type de transformation à appliquer à l’objet settings.
* `propertyPath` est une chaîne délimitée par des points qui indique à Platform où trouver la propriété qui doit être modifiée dans l’objet settings.

Lorsque l’objet settings est émis dans la bibliothèque du runtime de balises, il est transformé comme suit :

```javascript
{
  foo: {
    bar: "//launch.cdn.com/path/abc.js"
  }
}
```

Dans ce cas, la valeur de `foo.bar` a été transformée en URL. L’URL exacte sera déterminée au moment de la génération de la bibliothèque. Le fichier reçoit toujours une extension `.js` et est livré avec un type MIME orienté JavaScript. Nous pourrions à l’avenir ajouter la prise en charge d’autres types MIME.

#### Transformation remove

Par défaut, toutes les propriétés de l’objet settings sont émises dans la bibliothèque du runtime de balises. Si certaines propriétés ne sont utilisées que pour la vue d’extension, en particulier si elles contiennent des informations sensibles (par exemple jeton secret), vous devez utiliser la transformation remove pour empêcher l’émission des informations dans la bibliothèque runtime de balises.

Supposons que nous voudrions fournir un nouveau type d’action. La vue du type d’action peut fournir une entrée à partir de laquelle l’utilisateur peut saisir une clé secrète permettant la connexion à une API spécifique. Supposons qu’un utilisateur ait saisi le texte suivant :

`ABCDEFG`

Lorsque l’utilisateur enregistre la règle, l’objet settings enregistré par la vue peut se présenter comme suit :

```js
{
  foo: {
    bar: "ABCDEFG"
  }
}
```

Nous souhaitons ne pas inclure la propriété `bar` à l’intérieur de la bibliothèque du runtime de balises. Pour résoudre le problème de notre exemple, nous définirions la transformation sur la définition de type d’action dans `extension.json` comme suit :

```json
{
  "transforms": [
    {
      "type": "remove",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` définit le type de transformation à appliquer à l’objet settings.
* `propertyPath` est une chaîne délimitée par des points qui indique à Platform où trouver la propriété qui doit être modifiée dans l’objet settings.

Lorsque l’objet settings est émis dans la bibliothèque du runtime de balises, il est transformé comme suit :

```js
{
  foo: {
  }
}
```

Dans ce cas, la valeur de `foo.bar` a été supprimée de l’objet settings.
