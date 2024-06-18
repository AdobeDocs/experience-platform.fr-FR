---
title: (Version bêta) Utiliser des champs calculés pour exporter des tableaux dans des fichiers de schéma plats
type: Tutorial
description: Découvrez comment utiliser des champs calculés pour exporter des tableaux dans des fichiers de schéma plats de Real-Time CDP vers des destinations de stockage dans le cloud.
badge: Version bêta
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 787aaef26fab5ca3acff8303f928efa299cafa93
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 5%

---

# (Version bêta) Utiliser des champs calculés pour exporter des tableaux dans des fichiers de schéma plats {#use-calculated-fields-to-export-arrays-in-flat-schema-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="(Beta) Prise en charge de l’export des tableaux"
>abstract="Utilisez la commande **Ajouter un champ calculé** pour exporter des tableaux simples de valeurs entières, de chaîne ou booléennes d’Experience Platform vers la destination d’espace de stockage dans le cloud de votre choix. Certaines limites s’appliquent. Consultez la documentation pour obtenir des exemples complets et des fonctions prises en charge."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=fr#examples" text="Exemples"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/export-arrays-calculated-fields.html?lang=fr#known-limitations" text="Limites connues"

>[!AVAILABILITY]
>
>* La fonctionnalité d’exportation de tableaux par le biais de champs calculés est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

Découvrez comment exporter des tableaux à travers des champs calculés de Real-Time CDP dans des fichiers de schéma plats vers [destinations de stockage cloud](/help/destinations/catalog/cloud-storage/overview.md). Lisez ce document pour comprendre les cas d’utilisation activés par cette fonctionnalité.

Obtenez des informations détaillées sur les champs calculés - ce qu’ils sont et pourquoi ils comptent. Lisez les pages liées ci-dessous pour une introduction aux champs calculés dans la préparation des données et pour plus d’informations sur toutes les fonctions disponibles :

* [Guide et présentation de l’interface utilisateur](/help/data-prep/ui/mapping.md#calculated-fields)
* [Fonctions de la préparation des données](/help/data-prep/functions.md)

<!--

>[!IMPORTANT]
>
>Not all functions listed above are supported *when exporting fields to cloud storage destinations* using the calculated fields functionality. See the [supported functions section](#supported-functions) further below for more information.

-->

## Tableaux et autres types d’objets dans Platform {#arrays-strings-other-objects}

Dans Experience Platform, vous pouvez utiliser [Schémas XDM](/help/xdm/home.md) pour gérer différents types de champ. Auparavant, vous pouviez exporter des champs de type paire clé-valeur simples tels que des chaînes hors Experience Platform vers les destinations souhaitées. Voici un exemple de champ qui a été pris en charge pour l’exportation précédemment : `personalEmail.address`:`johndoe@acme.org`.

Les autres types de champ dans Experience Platform incluent les champs de tableau. En savoir plus sur [gestion des champs de tableau dans l’interface utilisateur Experience Platform](/help/xdm/ui/fields/array.md). Outre les types de champ précédemment pris en charge, vous pouvez désormais exporter des objets de tableau tels que : `organizations:[marketing, sales, engineering]`. Voir ci-dessous [exemples complets](#examples) de la manière dont vous pouvez utiliser différentes fonctions pour accéder aux éléments de tableaux, joindre des éléments de tableau dans une chaîne, etc.

## Limites connues {#known-limitations}

Notez les limites connues suivantes pour la version bêta de cette fonctionnalité :

* L’exportation vers des fichiers JSON ou Parquet avec des schémas hiérarchiques n’est pas prise en charge pour l’instant. Vous pouvez exporter des tableaux uniquement vers des fichiers CSV, JSON et Parquet de schéma plat.
* À l’heure actuelle, *vous pouvez uniquement exporter des tableaux simples (ou des tableaux de valeurs primitives) vers des destinations de stockage dans le cloud.*. Cela signifie que vous pouvez exporter des objets de tableau qui incluent des valeurs string, int ou boolean. Vous ne pouvez pas exporter de mappages ou de tableaux de mappages ou d’objets La fenêtre modale des champs calculés affiche uniquement les tableaux que vous pouvez exporter.

## Conditions préalables {#prerequisites}

[Connexion](/help/destinations/ui/connect-destination.md) vers la destination de stockage dans le cloud souhaitée, effectuez les opérations suivantes : [étapes d’activation pour les destinations de stockage dans le cloud](/help/destinations/ui/activate-batch-profile-destinations.md) et accédez au [mapping](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) étape .

## Comment exporter des champs calculés {#how-to-export-calculated-fields}

À l’étape de mappage du workflow d’activation pour les destinations de stockage dans le cloud, sélectionnez **[!UICONTROL (Version bêta) Ajouter un champ calculé]**.

![Ajoutez un champ calculé en surbrillance dans l’étape de mappage du workflow d’activation par lots.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Cela ouvre une fenêtre modale dans laquelle vous pouvez sélectionner des attributs que vous pouvez utiliser pour exporter des attributs hors d’Experience Platform.

>[!IMPORTANT]
>
>Seuls certains des champs de votre schéma XDM sont disponibles dans la variable **[!UICONTROL Champ]** vue. Vous pouvez voir des valeurs de chaîne et des tableaux de valeurs string, int et boolean. Par exemple, la variable `segmentMembership` n’est pas affiché, car il inclut d’autres valeurs de tableau.

![Fenêtre modale de la fonctionnalité de champ calculé sans fonction encore sélectionnée.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-2.png)

Par exemple, utilisez la variable `join` sur la fonction `loyaltyID` comme illustré ci-dessous pour exporter un tableau d’identifiants de fidélité sous forme de chaîne concaténée avec un trait de soulignement dans un fichier CSV. Affichage [plus d’informations à ce sujet et d’autres exemples ci-dessous](#join-function-export-arrays).

![Fenêtre modale de la fonctionnalité de champ calculé avec la fonction de jointure sélectionnée.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields-3.png)

Sélectionner **[!UICONTROL Enregistrer]** pour conserver le champ calculé et revenir à l’étape de mappage.

![Fenêtre modale de la fonctionnalité de champ calculé avec la fonction de jointure sélectionnée et le contrôle Enregistrer en surbrillance.](/help/destinations/assets/ui/export-arrays-calculated-fields/save-calculated-field.png)

De retour à l’étape de mappage du workflow, renseignez la variable **[!UICONTROL Champ cible]** avec la valeur de l’en-tête de colonne que vous souhaitez pour ce champ dans les fichiers exportés.

![Correspondance de l’étape avec le champ cible surligné.](/help/destinations/assets/ui/export-arrays-calculated-fields/fill-in-target-field.png)

![Sélectionner le champ cible 2](/help/destinations/assets/ui/export-arrays-calculated-fields/target-field-filled-in.png)

Une fois prêt, sélectionnez **[!UICONTROL Suivant]** pour passer à l’étape suivante du workflow d’activation.

![Etape de mappage avec le champ cible surligné et une valeur cible renseignée.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-next-to-proceed.png)

## Fonctions prises en charge {#supported-functions}

Tous les documents [Fonctions de préparation des données](/help/data-prep/functions.md) sont pris en charge lors de l’activation de données vers des destinations basées sur des fichiers.

Notez toutefois que des descriptions détaillées de cas d’utilisation et des exemples d’informations de sortie ne sont actuellement fournies pour les fonctions suivantes que dans la version bêta des champs calculés et de la prise en charge des tableaux pour les destinations :

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

![Exemple de mappage comprenant la fonction join .](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-join-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Notez comment les trois éléments du tableau sont concaténés en une seule chaîne à l’aide de la variable `_` caractère.

```
`First_Name,Last_Name,Personal_Email,Organization
John,Doe,johndoe@acme.org, "Marketing_Sales_Finance"
```

### `iif` fonction d’exportation de tableaux {#iif-function-export-arrays}

Utilisez la variable `iif` pour exporter des éléments d’un tableau sous certaines conditions. Par exemple, continuez avec la fonction `organizations` Objet de tableau situé au-dessus, vous pouvez créer une fonction conditionnelle simple comme `iif(organizations[0].equals("Marketing"), "isMarketing", "isNotMarketing")`.

![Exemple de mappage comprenant la fonction iif.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-iif-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Dans ce cas, le premier élément du tableau est Marketing, la personne est donc membre du service marketing.

```
`First_Name,Last_Name, Personal_Email, Is_Member_Of_Marketing_Dept
John,Doe, johndoe@acme.org, "isMarketing"
```

### `add_to_array` fonction d’exportation de tableaux {#add-to-array-function-export-arrays}

Utilisez la variable `add_to_array` pour ajouter des éléments à un tableau exporté. Vous pouvez associer cette fonction à la fonction `join` fonction décrite plus haut.

Si vous continuez avec la variable `organizations` Objet de tableau ci-dessus, vous pouvez écrire une fonction comme `source: join('_', add_to_array(organizations,"2023"))`, renvoyant les organisations dont une personne est membre en 2023.

![Exemple de mappage comprenant la fonction add_to_array .](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-add-to-array-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Notez comment les trois éléments du tableau sont concaténés en une seule chaîne à l’aide de la variable `_` et 2023 sont également ajoutés à la fin de la chaîne.

```
`First_Name,Last_Name,Personal_Email,Organization_Member_2023
John,Doe, johndoe@acme.org,"Marketing_Sales_Finance_2023"
```

### `coalesce` fonction d’exportation de tableaux {#coalesce-function-export-arrays}

Utilisez la variable `coalesce` pour accéder au premier élément non nul d’un tableau et l’exporter dans une chaîne.

Par exemple, vous pouvez combiner les champs XDM suivants comme indiqué dans la capture d’écran du mappage à l’aide d’une `coalesce(subscriptions.hasPromotion)` pour renvoyer la première `true` de `false` dans le tableau :

* `"subscriptions.hasPromotion": [null, true, null, false, true]` tableau
* `person.name.firstName` string
* `person.name.lastName` string
* `personalEmail.address` string

![Exemple de mappage comprenant la fonction coalesce.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-coalesce-function.png)

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

![Exemple de mappage comprenant la fonction size_of .](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-size-of-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Notez comment la deuxième colonne indique le nombre d’éléments dans le tableau, correspondant au nombre d’achats distincts effectués par le client.

```
`Personal_Email,Times_Purchased
johndoe@acme.org,"5"
```

### Accès aux tableaux basés sur des index {#index-based-array-access}

Vous pouvez accéder à un index d’un tableau pour exporter un seul élément du tableau. Par exemple, similaire à l’exemple ci-dessus pour la variable `size_of` , si vous souhaitez accéder à un produit spécifique et l’exporter uniquement la première fois qu’un client l’a acheté, vous pouvez utiliser `purchaseTime[0]` pour exporter le premier élément de l&#39;horodatage, `purchaseTime[1]` pour exporter le deuxième élément de l&#39;horodatage, `purchaseTime[2]` pour exporter le troisième élément de l’horodatage, etc.

![Exemple de mappage montrant comment accéder à un élément d’un tableau.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-index.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit, en exportant la première fois que le client a effectué un achat :

```
`Personal_Email,First_Purchase
johndoe@acme.org,"1538097126"
```

### `first` et `last` fonctions d’exportation de tableaux {#first-and-last-functions-export-arrays}

Utilisez la variable `first` et `last` pour exporter le premier ou le dernier élément d’un tableau. Par exemple, continuez avec la fonction `purchaseTime` avec plusieurs horodatages des exemples précédents, vous pouvez les utiliser dans des fonctions pour exporter la première ou la dernière heure d’achat effectuée par une personne.

![Exemple de mappage comprenant la première et la dernière fonctions.](/help/destinations/assets/ui/export-arrays-calculated-fields/mapping-first-last-functions.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit, en exportant la première et la dernière fois que le client a effectué un achat :

```
`Personal_Email,First_Purchase, Last_Purchase
johndoe@acme.org,"1538097126","1664327526"
```

### Fonctions de hachage {#hashing-functions}

Outre les fonctions spécifiques à l’exportation de tableaux ou d’éléments à partir d’un tableau, vous pouvez utiliser des fonctions de hachage pour hacher des attributs dans les fichiers exportés. Par exemple, si vous disposez d’informations d’identification personnelle dans les attributs, vous pouvez hacher ces champs lors de leur exportation.

Vous pouvez hacher directement des valeurs de chaîne, par exemple `md5(personalEmail.address)`. Si vous le souhaitez, vous pouvez également hacher des éléments individuels des champs de tableau, en supposant que les éléments du tableau soient des chaînes, comme ceci : `md5(purchaseTime[0])`

Les fonctions de hachage prises en charge sont les suivantes :

| Fonction | Exemple d’expression |
|---------|----------|
| `sha1` | `sha1(organizations[0])` |
| `sha256` | `sha256(organizations[0])` |
| `sha512` | `sha512(organizations[0])` |
| `hash` | `hash("crc32", organizations[0], "UTF-8")` |
| `md5` | `md5(organizations[0], "UTF-8")` |
| `crc32` | `crc32(organizations[0])` |

{style="table-layout:auto"}