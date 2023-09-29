---
title: (Version bêta) Utilisation de champs calculés pour exporter des tableaux dans des fichiers de schéma plats
type: Tutorial
description: Découvrez comment utiliser des champs calculés pour exporter des tableaux dans des fichiers de schéma plats de Real-Time CDP vers des destinations de stockage dans le cloud.
badge: « Version bêta »
source-git-commit: 77fd0ace252bae66478f73a1dc4b7d4a3ccb867d
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 2%

---


# (Version bêta) Utilisation de champs calculés pour exporter des tableaux dans des fichiers de schéma plats {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Version bêta) Prise en charge des tableaux d’exportation"
>abstract="Exportez des tableaux simples de valeurs int, string ou booléennes de l’Experience Platform vers la destination de stockage dans le cloud souhaitée. Certaines restrictions s’appliquent. Consultez la documentation pour obtenir des exemples complets et des fonctions prises en charge."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#examples" text="Exemples"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html#known-limitations" text="Limites connues"

>[!AVAILABILITY]
>
>* La fonctionnalité d’exportation de tableaux par le biais de champs calculés est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

Découvrez comment exporter des tableaux à travers des champs calculés de Real-Time CDP dans des fichiers de schéma plats vers des destinations de stockage dans le cloud. Lisez ce document pour comprendre les cas d’utilisation activés par cette fonctionnalité.

Obtenez des informations détaillées sur les champs calculés - ce qu’ils sont et pourquoi ils comptent. Lisez les pages liées ci-dessous pour une introduction aux champs calculés dans la préparation des données et pour plus d’informations sur toutes les fonctions disponibles :

* [Guide et présentation de l’interface utilisateur](/help/data-prep/ui/mapping.md#calculated-fields)
* [Fonctions de préparation des données](/help/data-prep/functions.md)

>[!IMPORTANT]
>
>Toutes les fonctions répertoriées ci-dessus ne sont pas prises en charge *lors de l’exportation de champs vers des destinations de stockage dans le cloud* en utilisant la fonctionnalité des champs calculés . Voir [section fonctions prises en charge](#supported-functions) pour plus d’informations, voir ci-dessous.

## Tableaux et autres types d’objets dans Platform {#arrays-strings-other-objects}

Dans Experience Platform, vous pouvez utiliser [Schémas XDM](/help/xdm/home.md) pour gérer différents types de champ. Auparavant, vous pouviez exporter des champs de type paire clé-valeur simples tels que des chaînes hors Experience Platform vers les destinations souhaitées. Voici un exemple de champ qui a été pris en charge pour l’exportation précédemment : `personalEmail.address`:`johndoe@acme.org`.

Les autres types de champ dans Experience Platform incluent les champs de tableau. En savoir plus sur [gestion des champs de tableau dans l’interface utilisateur Experience Platform](/help/xdm/ui/fields/array.md). Outre les types de champ précédemment pris en charge, vous pouvez désormais exporter des objets de tableau tels que : `organizations:[marketing, sales, engineering]`. Voir ci-dessous [exemples complets](#examples) de la manière dont vous pouvez utiliser différentes fonctions pour accéder aux éléments de tableaux, joindre des éléments de tableau dans une chaîne, etc.

## Limites connues {#known-limitations}

Notez les limites connues suivantes pour la version bêta de cette fonctionnalité :

* L’exportation vers des fichiers JSON ou Parquet avec des schémas hiérarchiques n’est pas prise en charge pour l’instant. Vous pouvez exporter des tableaux uniquement vers des fichiers CSV, JSON et Parquet de schéma plat.
* À l’heure actuelle, *vous pouvez uniquement exporter des tableaux simples (ou des tableaux de valeurs primitives) vers des destinations de stockage dans le cloud.*. Cela signifie que vous pouvez exporter des objets de tableau qui incluent des valeurs string, int ou boolean. Vous ne pouvez pas exporter de mappages ou de tableaux de mappages ou d’objets La fenêtre modale des champs calculés affiche uniquement les tableaux que vous pouvez exporter.

## Conditions préalables {#prerequisites}

Progression de la [étapes d’activation pour les destinations de stockage dans le cloud](/help/destinations/ui/activate-batch-profile-destinations.md) et accédez au [mapping](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) étape .

## Comment exporter des champs calculés {#how-to-export-calculated-fields}

À l’étape de mappage du workflow d’activation pour les destinations de stockage dans le cloud, sélectionnez **[!UICONTROL (Version bêta) Ajouter un champ calculé]**.

![Ajouter un champ calculé à exporter](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Cela ouvre une fenêtre modale dans laquelle vous pouvez sélectionner des attributs que vous pouvez utiliser pour exporter des attributs hors d’Experience Platform.

>[!IMPORTANT]
>
>Seuls certains des champs de votre schéma XDM sont disponibles dans la variable **[!UICONTROL Champ]** vue. Vous pouvez voir des valeurs de chaîne et des tableaux de valeurs string, int et boolean. Par exemple, la variable `segmentMembership` n’est pas affiché, car il inclut d’autres valeurs de tableau.

![Fenêtre modale 1](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Par exemple, utilisez la variable `join` sur la fonction `loyaltyID` comme illustré ci-dessous pour exporter un tableau d’identifiants de fidélité sous forme de chaîne concaténée avec un trait de soulignement dans un fichier CSV. Affichage [plus d’informations à ce sujet et d’autres exemples ci-dessous](#join-function-export-arrays).

![Fenêtre modale 2](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Sélectionner **[!UICONTROL Enregistrer]** pour conserver le champ calculé et revenir à l’étape de mappage.

![Fenêtre modale 3](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

De retour à l’étape de mappage du workflow, renseignez la variable **[!UICONTROL Champ cible]** avec la valeur de l’en-tête de colonne que vous souhaitez pour ce champ dans les fichiers exportés.

![Sélectionner le champ cible 1](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Sélectionner le champ cible 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Une fois prêt, sélectionnez **[!UICONTROL Suivant]** pour passer à l’étape suivante du workflow d’activation.

![Sélectionner en regard de la procédure](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Fonction  prise en charge {#supported-functions}

Notez que seules les fonctions suivantes sont prises en charge dans la version bêta des champs calculés et de la prise en charge des tableaux pour les destinations :

* `join`
* `coalesce`
* `size_of`
* `iif`
* `index-based array access`
* `add_to_array`
* `to_array`
* `first`
* `last`
* `sha256`
* `md5`

## Exemples de fonctions utilisées pour exporter des tableaux {#examples}

Consultez des exemples et des informations supplémentaires dans les sections ci-dessous pour connaître certaines des fonctions répertoriées ci-dessus. Pour le reste des fonctions répertoriées, reportez-vous à la section [documentation générale sur les fonctions dans la section Préparation des données](/help/data-prep/functions.md).

### `join` fonction d’exportation de tableaux {#join-function-export-arrays}

Utilisez la variable `join` pour concaténer les éléments d’un tableau dans une chaîne, à l’aide d’un séparateur souhaité, tel que `_` ou `|`.

Par exemple, vous pouvez combiner les champs XDM suivants comme indiqué dans la capture d’écran du mappage à l’aide d’une `join('_',loyalty.loyaltyID)` syntaxe :

* `"organizations": ["Marketing","Sales,"Finance"]` tableau
* `person.name.firstName` string
* `person.name.lastName` string
* `personalEmail.address` string

![Copie d’écran de mappage](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Notez comment les trois éléments du tableau sont concaténés en une seule chaîne à l’aide de la variable `_` caractère.

```
`First_Name,Last_Name,Organization
John,Doe,"Marketing_Sales_Finance"
```

### `coalesce` fonction d’exportation de tableaux {#coalesce-function-export-arrays}

Utilisez la variable `coalesce` pour accéder au premier élément non nul d’un tableau et l’exporter dans une chaîne.

Par exemple, vous pouvez combiner les champs XDM suivants comme indiqué dans la capture d’écran du mappage à l’aide d’une `coalesce(subscriptions.hasPromotion)` pour renvoyer la première valeur true de false dans le tableau :

* `"subscriptions.hasPromotion": [null, true, null, false, true]` tableau
* `person.name.firstName` string
* `person.name.lastName` string
* `personalEmail.address` string

![Copie d’écran de mappage pour la fonction coalesce](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Remarquez comment la première valeur non nulle `true` dans le tableau est exportée dans le fichier .

```
First_Name,Last_Name,hasPromotion
John,Doe,true
```


### `size_of` fonction d’exportation de tableaux {#sizeof-function-export-arrays}

Utilisez la variable `size_of` pour indiquer le nombre d’éléments figurant dans un tableau. Par exemple, si vous avez une `purchaseTime` objet de tableau avec plusieurs horodatages, vous pouvez utiliser la variable `size_of` pour indiquer le nombre d’achats distincts effectués par une personne.

Par exemple, vous pouvez combiner les champs XDM suivants comme indiqué dans la capture d’écran du mappage.

* `"purchaseTime": ["1538097126","1569633126,"1601255526","1632791526","1664327526"]` tableau indiquant cinq heures d’achat distinctes par le client
* `personalEmail.address` string

![Copie d’écran de mappage de la fonction size_of](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Notez comment la deuxième colonne indique le nombre d’éléments dans le tableau, correspondant au nombre d’achats distincts effectués par le client.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Accès aux tableaux basés sur des index {#index-based-array-access}

Vous pouvez accéder à un index d’un tableau pour exporter un seul élément du tableau. Par exemple, similaire à l’exemple ci-dessus pour la variable `size_of` , si vous souhaitez accéder à un produit spécifique et l’exporter uniquement la première fois qu’un client l’a acheté, vous pouvez utiliser `purchaseTime[0]` pour exporter le premier élément de l&#39;horodatage, `purchaseTime[1]` pour exporter le deuxième élément de l&#39;horodatage, `purchaseTime[2]` pour exporter le troisième élément de l’horodatage, etc.

![Copie d’écran de mappage pour l’accès à l’index](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

Dans ce cas, votre fichier de sortie se présente comme suit :

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` et `last` fonctions d’exportation de tableaux {#first-and-last-functions-export-arrays}

Utilisez la variable `first` et `last` pour exporter le premier ou le dernier élément d’un tableau. Par exemple, continuez avec la fonction `purchaseTime` avec plusieurs horodatages des exemples précédents, vous pouvez les utiliser dans des fonctions pour exporter la première ou la dernière heure d’achat effectuée par une personne.

![Copie d’écran du mappage pour les première et dernière fonctions](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

Dans ce cas, votre fichier de sortie se présente comme suit :

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

<!--

### `iif` function to export arrays {#iif-function-export-arrays}

Here are some examples of how you could use the `iif` function to access and export arrays and other fields: (STILL TO DO)

-->

### `md5` et `sha256` fonctions de hachage {#hashing-functions}

Outre les fonctions spécifiques à l’exportation de tableaux ou d’éléments à partir d’un tableau, vous pouvez utiliser des fonctions de hachage pour hacher des attributs. Par exemple, si vous disposez d’informations d’identification personnelle dans les attributs, vous pouvez hacher ces champs lors de leur exportation.

Vous pouvez hacher directement des valeurs de chaîne, par exemple `md5(personalEmail.address)`. Si vous le souhaitez, vous pouvez également hacher des éléments individuels des champs de tableau, comme ceci : `md5(purchaseTime[0])`



