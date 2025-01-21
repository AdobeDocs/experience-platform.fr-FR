---
title: Exporter des objets de tableau de Real-Time CDP vers des destinations d’espace de stockage dans le cloud
type: Tutorial
description: Découvrez comment utiliser des champs calculés pour exporter des tableaux de Real-Time CDP vers des destinations d’espace de stockage sous forme de chaînes.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: a99fc58b8296b2b9ce6e30d14857529570cd3e8a
workflow-type: tm+mt
source-wordcount: '1622'
ht-degree: 7%

---

# Exporter des objets de tableau de Real-Time CDP vers des destinations d’espace de stockage dans le cloud {#export-arrays-cloud-storage}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Prise en charge de l’export des tableaux"
>abstract="<p>Utilisez la commande **Ajouter un champ calculé** pour exporter des tableaux simples d’entiers, de chaînes, de valeurs booléennes ou d’objets d’Experience Platform vers la destination d’espace de stockage dans le cloud de votre choix.</p><p> Les tableaux doivent être exportés en tant que chaînes à l’aide de la fonction `array_to_string`. Consultez la documentation pour obtenir des exemples complets et des fonctions prises en charge.</p>"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=fr#examples" text="Exemples"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=fr#known-limitations" text="Limites connues"

>[!AVAILABILITY]
>
>La fonctionnalité d’exportation de baies vers des destinations d’espace de stockage est généralement disponible.

Découvrez comment exporter des tableaux de Real-Time CDP vers des [destinations de stockage dans le cloud](/help/destinations/catalog/cloud-storage/overview.md). Lisez ce document pour comprendre le workflow d’exportation, les cas d’utilisation activés par cette fonctionnalité et les limites connues.

Les tableaux doivent actuellement être exportés sous forme de chaînes à l’aide de la fonction `array_to_string` .

Pour exporter des tableaux, vous devez utiliser la fonctionnalité de champs calculés à l’étape de mappage du workflow d’exportation, *à moins que vous n’exportiez [ des éléments individuels d’un tableau](#index-based-array-access)*. Pour plus d’informations sur les champs calculés, consultez les pages liées ci-dessous. Vous y trouverez une présentation des champs calculés dans la préparation des données et plus d’informations sur toutes les fonctions disponibles :

* [Guide et présentation de l’interface utilisateur](/help/data-prep/ui/mapping.md#calculated-fields)
* [Fonctions de la préparation des données](/help/data-prep/functions.md)

## Tableaux et autres types d’objets dans Platform {#arrays-strings-other-objects}

Dans Experience Platform, vous pouvez utiliser des [schémas XDM](/help/xdm/home.md) pour gérer différents types de champs. Avant l’ajout de la prise en charge des exportations de tableaux, vous pouviez exporter des champs de type paire clé-valeur simples, tels que des chaînes, de manière Experience Platform vers les destinations souhaitées. `personalEmail.address`:`johndoe@acme.org` est un exemple de champ de ce type, précédemment pris en charge pour l’exportation.

D’autres types de champs dans l’Experience Platform incluent les champs de tableau. En savoir plus sur la [gestion des champs de tableau dans l’interface utilisateur de l’Experience Platform ](/help/xdm/ui/fields/array.md). Outre les types de champ précédemment pris en charge, vous pouvez désormais exporter des objets de tableau tels que l’exemple ci-dessous, concaténés dans une chaîne à l’aide de la fonction `array_to_string` .

```
organizations = [{
  id: 123,
  orgName: "Acme Inc",
  founded: 1990,
  latestInteraction: "2024-02-16"
}, {
  id: 456,
  orgName: "Superstar Inc",
  founded: 2004,
  latestInteraction: "2023-08-25"
}, {
  id: 789,
  orgName: 'Energy Corp',
  founded: 2021,
  latestInteraction: "2024-09-08"
}]
```

Vous trouverez ci-dessous [des exemples détaillés](#examples) sur la manière dont vous pouvez utiliser diverses fonctions pour accéder aux éléments de tableaux, transformer et filtrer des tableaux, joindre des éléments de tableau en chaîne, etc.

## Limites connues {#known-limitations}

Notez les limites connues suivantes qui s’appliquent actuellement à cette fonctionnalité :

* L’exportation de fichiers JSON ou Parquet *avec des schémas hiérarchiques* n’est pas prise en charge pour le moment. Vous pouvez exporter des tableaux vers des fichiers CSV, JSON et Parquet *sous forme de chaînes uniquement* à l’aide de la fonction `array_to_string` .

## Conditions préalables {#prerequisites}

[Connectez-vous](/help/destinations/ui/connect-destination.md) à une destination d’espace de stockage souhaitée, suivez les [étapes d’activation pour les destinations d’espace de stockage](/help/destinations/ui/activate-batch-profile-destinations.md) et accédez à l’étape [mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).

## Comment exporter des champs calculés {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="Activer le schéma de sortie hiérarchique"
>abstract="Activez cette option pour exporter des structures hiérarchiques telles que des tableaux."

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="« Ajouter des champs calculés » désactivé"
>abstract="Cette commande est désactivée, car vous avez choisi d’exporter des structures plates lors de la connexion à la destination."

À l’étape de mappage du workflow d’activation pour les destinations d’espace de stockage, sélectionnez **[!UICONTROL Ajouter un champ calculé]**.

![Ajouter un champ calculé en surbrillance à l’étape de mappage du workflow d’activation par lots.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Une fenêtre modale s’ouvre, dans laquelle vous pouvez sélectionner des fonctions et des champs à exporter en dehors de l’Experience Platform.

![Fenêtre modale de la fonctionnalité de champ calculé, sans sélection de fonction pour le moment.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Par exemple, utilisez la fonction `array_to_string` dans le champ `organizations` comme illustré ci-dessous pour exporter le tableau organisations sous la forme d’une chaîne dans un fichier CSV. Afficher [plus d’informations à ce sujet et d’autres exemples ci-dessous](#array-to-string-function-export-arrays).

![Fenêtre modale de la fonctionnalité de champ calculé avec la fonction tableau-chaîne sélectionnée.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Sélectionnez **[!UICONTROL Enregistrer]** pour conserver le champ calculé et revenir à l’étape de mappage.

![Fenêtre modale de la fonctionnalité de champ calculé avec la fonction tableau-chaîne sélectionnée et le contrôle Enregistrer mis en surbrillance.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

De retour à l’étape de mappage du workflow, remplissez le **[!UICONTROL champ cible]** avec une valeur de l’en-tête de colonne que vous souhaitez pour ce champ dans les fichiers exportés.

![Étape de mapping avec le champ cible en surbrillance.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Sélectionnez le champ cible 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Une fois prêt, sélectionnez **[!UICONTROL Suivant]** pour passer à l’étape suivante du workflow d’activation.

![Étape de mappage avec le champ cible mis en surbrillance et une valeur cible renseignée.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Exemples de fonctions prises en charge pour exporter des tableaux {#supported-functions}

Toutes les [fonctions de préparation de données](/help/data-prep/functions.md) documentées sont prises en charge lors de l’activation de données vers des destinations basées sur des fichiers.

Les fonctions ci-dessous, spécifiques à la gestion des exportations de tableaux, sont documentées avec des exemples.

* `array_to_string`
* `flattenArray`
* `filterArray`
* `transformArray`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`

## Exemples de fonctions utilisées pour exporter des tableaux {#examples}

Consultez des exemples et des informations supplémentaires dans les sections ci-dessous pour certaines des fonctions répertoriées ci-dessus. Pour le reste des fonctions répertoriées, reportez-vous à la documentation sur les fonctions [générales) dans la section Préparation des données ](/help/data-prep/functions.md).

### `array_to_string` fonction pour exporter des tableaux {#array-to-string-function-export-arrays}

Utilisez la fonction `array_to_string` pour concaténer les éléments d’un tableau en chaîne, à l’aide du séparateur souhaité, tel que `_` ou `|`.

Par exemple, vous pouvez combiner les champs XDM suivants comme illustré dans la capture d’écran de mappage à l’aide d’une syntaxe `array_to_string('_',organizations)` :

* tableau `organizations`
* chaîne `person.name.firstName`
* chaîne `person.name.lastName`
* chaîne `personalEmail.address`

![Exemple de mapping incluant la fonction array_to_string.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-array-to-string-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Notez comment les éléments du tableau sont concaténés en une seule chaîne à l’aide du caractère `_` .

```
First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':456,'orgName':'Superstar Inc','founded':2004,'latestInteraction':1692921600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `filterArray` fonction pour exporter des tableaux filtrés

Utilisez la fonction `filterArray` pour filtrer les éléments d’un tableau exporté. Vous pouvez combiner cette fonction avec la fonction `array_to_string` décrite plus haut.

En poursuivant avec l’objet de tableau `organizations` ci-dessus, vous pouvez écrire une fonction telle que `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))`, renvoyant les organisations avec une valeur de `founded` en 2021 ou plus récent.

![Exemple de la fonction filterArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Notez comment les deux éléments du tableau qui répondent au critère sont concaténés en une seule chaîne à l’aide du caractère `_` .

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `transformArray` fonction pour exporter des tableaux transformés

Utilisez la fonction `transformArray` pour transformer les éléments d’un tableau exporté. Vous pouvez combiner cette fonction avec la fonction `array_to_string` décrite plus haut.

En poursuivant avec l’objet de tableau `organizations` ci-dessus, vous pouvez écrire une fonction telle que `array_to_string('_', transformArray(organizations, org -> ucase(org.orgName)))`, renvoyant les noms des organisations convertis en majuscules.

![Exemple de la fonction transformArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/transform-array-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Notez comment les trois éléments du tableau sont transformés et concaténés en une seule chaîne à l’aide du caractère `_` .

```
John,Doe,johndoe@acme.org,ACME INC_SUPERSTAR INC_ENERGY CORP
```

### `iif` fonction pour exporter des tableaux {#iif-function-export-arrays}

Utilisez la fonction `iif` pour exporter des éléments d&#39;un tableau sous certaines conditions. Par exemple, en poursuivant avec l’objet de tableau `organizations` ci-dessus, vous pouvez écrire une fonction conditionnelle simple telle que `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![Exemple de mapping incluant la fonction iif.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Dans ce cas, le premier élément du tableau est Marketing. Par conséquent, la personne est membre du service marketing.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array` fonction pour exporter des tableaux {#add-to-array-function-export-arrays}

Utilisez la fonction `add_to_array` pour ajouter des éléments à un tableau exporté. Vous pouvez combiner cette fonction avec la fonction `array_to_string` décrite plus haut.

En poursuivant avec l’objet de tableau `organizations` ci-dessus, vous pouvez écrire une fonction telle que `source: array_to_string('_', add_to_array(organizations,"2023"))`, renvoyant les organisations dont une personne est membre en 2023.

![Exemple de mapping incluant la fonction add_to_array.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Remarquez comment les trois éléments du tableau sont concaténés en une seule chaîne à l’aide du caractère `_` et 2023 est également ajouté à la fin de la chaîne.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `flattenArray` fonction pour exporter des tableaux aplatis

Utilisez la fonction `flattenArray` pour aplatir un tableau multidimensionnel exporté. Vous pouvez combiner cette fonction avec la fonction `array_to_string` décrite plus haut.

En poursuivant avec l’objet de tableau `organizations` ci-dessus, vous pouvez écrire une fonction telle que `array_to_string('_', flattenArray(organizations))`. Notez que la fonction `array_to_string` aplatit le tableau d’entrée par défaut en une chaîne.

La sortie résultante est la même que pour la fonction `array_to_string` décrite plus haut.

### `coalesce` fonction pour exporter des tableaux {#coalesce-function-export-arrays}

Utilisez la fonction `coalesce` pour accéder au premier élément non nul d’un tableau et l’exporter dans une chaîne.

Par exemple, vous pouvez combiner les champs XDM ci-dessous comme illustré dans la capture d’écran de mappage en utilisant une syntaxe `coalesce(subscriptions.hasPromotion)` pour renvoyer la première `true` de `false` valeur dans le tableau :

* tableau `"subscriptions.hasPromotion": [null, true, null, false, true]`
* chaîne `person.name.firstName`
* chaîne `person.name.lastName`
* chaîne `personalEmail.address`

![Exemple de mapping incluant la fonction coalesce.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Notez comment la première valeur de `true` non nulle du tableau est exportée dans le fichier .

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```

### `size_of` fonction pour exporter des tableaux {#sizeof-function-export-arrays}

Utilisez la fonction `size_of` pour indiquer le nombre d’éléments qui existent dans un tableau. Par exemple, si vous disposez d’un objet de tableau `purchaseTime` avec plusieurs horodatages, vous pouvez utiliser la fonction `size_of` pour indiquer le nombre d’achats distincts effectués par une personne.

Par exemple, vous pouvez combiner les champs XDM ci-dessous comme illustré dans la capture d’écran du mappage.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` tableau indiquant cinq heures d’achat distinctes par le client
* chaîne `personalEmail.address`

![Exemple de mapping incluant la fonction size_of.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Notez que la deuxième colonne indique le nombre d’éléments dans le tableau, correspondant au nombre d’achats distincts effectués par le client.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Accès aux tableaux basé sur les index {#index-based-array-access}

>[!IMPORTANT]
>
>Contrairement aux autres fonctions décrites sur cette page, pour exporter des éléments individuels d’un tableau, vous n’avez *pas besoin* d’utiliser le contrôle **[!UICONTROL Champs calculés]** dans l’interface utilisateur.

Vous pouvez accéder à un index d’un tableau pour exporter un seul élément du tableau . Par exemple, comme dans l’exemple ci-dessus pour la fonction `size_of` , si vous souhaitez accéder à et exporter uniquement la première fois qu’un client a acheté un certain produit, vous pouvez utiliser `purchaseTime[0]` pour exporter le premier élément de l’horodatage, `purchaseTime[1]` pour exporter le deuxième élément de l’horodatage, `purchaseTime[2]` pour exporter le troisième élément de l’horodatage, etc.

![Exemple de mappage montrant comment accéder à un élément d’un tableau.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit, en exportant le premier achat du client :

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` et fonctions de `last` pour exporter des tableaux {#first-and-last-functions-export-arrays}

Utilisez les fonctions `first` et `last` pour exporter le premier ou le dernier élément d&#39;un tableau. Par exemple, en poursuivant avec l’objet de tableau `purchaseTime` avec plusieurs horodatages des exemples précédents, vous pouvez utiliser ces fonctions pour exporter la première ou la dernière heure d’achat effectuée par une personne.

![Exemple de mapping incluant la première et la dernière fonction.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit, en exportant le premier et le dernier achat du client :

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

<!--

### Hashing functions {#hashing-functions}

In addition to the functions specific for exporting arrays or elements from an array, you can use hashing functions to hash attributes in the exported files. For example, if you have any personally identifiable information in attributes, you can hash those fields when exporting them. 

You can hash string values directly, for example `md5(personalEmail.address)`. If desired, you can also hash individual elements of array fields, assuming elements in the array are strings, like this: `md5(purchaseTime[0])`

The supported hashing functions are:

|Function | Sample expression |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` |  `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}

-->