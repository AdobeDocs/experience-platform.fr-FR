---
title: Effectuer des transformations sur les données exportées vers des destinations d’espace de stockage à l’aide de champs calculés
type: Tutorial
description: Découvrez comment utiliser la fonctionnalité de champs calculés pour effectuer des transformations sur les données exportées vers des destinations d’espace de stockage
exl-id: 1e14f964-4c03-4d0c-be8d-c3dcb48a335a
source-git-commit: bd9efc1bcf6058827cc5c603b9976c9e42c7ec9e
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 8%

---

# Effectuer des transformations sur les données exportées vers des destinations d’espace de stockage à l’aide de champs calculés {#data-transformation-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_flat_files"
>title="Ajouter des champs calculés"
>abstract="<p>Utilisez la commande **Ajouter un champ calculé** pour effectuer diverses transformations sur les données exportées vers des destinations d’espace de stockage dans le cloud. Par exemple, vous pouvez appliquer un hachage aux données, concaténer des tableaux en chaînes, etc."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/data-transformations-calculated-fields.html?lang=fr#examples" text="Exemples"

>[!AVAILABILITY]
>
>La fonctionnalité permettant d’effectuer des transformations sur les données exportées vers des destinations d’espace de stockage est généralement disponible pour les destinations suivantes : [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md), ainsi que pour toutes les destinations d’espace de stockage dans le cloud créées par des partenaires personnalisés via [Destination SDK](/help/destinations/destination-sdk/overview.md).

Pour effectuer diverses transformations sur les données exportées vers des destinations d’espace de stockage, vous devez utiliser la fonctionnalité de champs calculés dans l’étape de mappage du workflow d’exportation. Pour plus d’informations sur les champs calculés, consultez les pages liées ci-dessous. Ces pages présentent les champs calculés dans la préparation des données et contiennent des informations supplémentaires sur toutes les fonctions disponibles :

* [Guide et présentation de l’interface utilisateur](/help/data-prep/ui/mapping.md#calculated-fields)
* [Fonctions de la préparation des données](/help/data-prep/functions.md)

## Prérequis {#prerequisites}

Pour utiliser des champs calculés pour les transformations de données :

1. [Connexion](/help/destinations/ui/connect-destination.md) à une destination d’espace de stockage souhaitée. Lors de la connexion à la destination cloud souhaitée, activez l’option **[!UICONTROL Exporter des tableaux, des mappages]** des objets [ désactivée](/help/destinations/ui/export-arrays-maps-objects.md##export-arrays-maps-objects-toggle).
2. Parcourez les [étapes d’activation pour les destinations de stockage dans le cloud](/help/destinations/ui/activate-batch-profile-destinations.md) et accédez à l’étape [mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).

## Utiliser des champs calculés {#how-to-export-calculated-fields}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_control"
>title="Activer le schéma de sortie hiérarchique"
>abstract="Activez ce paramètre pour activer l’export de tableaux, de mappages et d’objets vers des fichiers JSON ou Parquet."

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_calculated_field_disabled"
>title="« Ajouter des champs calculés » désactivé"
>abstract="Cette commande est désactivée, car vous avez *activé* le bouton **Exporter des tableaux, des mappages et des objets** lors de la configuration de cette connexion de destination. Pour utiliser les champs calculés et les fonctions disponibles, configurez une nouvelle connexion de destination avec le bouton bascule **Exporter des tableaux, des mappages et des objets** *désactivé*."

>[!IMPORTANT]
>
>Lorsque vous utilisez des champs calculés, vous devez non seulement appliquer une fonction de transformation des données, mais également utiliser la fonction `array_to_string` pour concaténer des champs en chaîne.

À l’étape de mappage du workflow d’activation pour les destinations d’espace de stockage, sélectionnez **[!UICONTROL Ajouter un champ calculé]**.

>[!TIP]
>
>Le contrôle **[!UICONTROL Ajouter un champ calculé]** est désactivé pour les connexions de destination pour lesquelles le contrôle **[!UICONTROL Exporter des tableaux, des mappages et des objets]** a été désactivé. [En savoir plus](/help/destinations/ui/export-arrays-maps-objects.md#export-arrays-maps-objects-toggle).

![Ajouter un champ calculé en surbrillance à l’étape de mappage du workflow d’activation par lots.](/help/destinations/assets/ui/export-arrays-calculated-fields/add-calculated-fields.png)

Une fenêtre modale s’ouvre, dans laquelle vous pouvez sélectionner les fonctions et les champs à exporter en dehors d’Experience Platform.

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

## Exemples de fonctions prises en charge pour effectuer des transformations de données {#supported-functions}

Toutes les [fonctions de préparation de données](/help/data-prep/functions.md) documentées sont prises en charge lors de l’activation de données vers des destinations basées sur des fichiers.

Les fonctions ci-dessous, spécifiques à la gestion des exportations de tableaux ou à l’application d’un hachage aux champs, sont documentées avec des exemples.

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

## Exemples de fonctions utilisées pour effectuer des transformations de données {#examples}

Consultez des exemples et des informations supplémentaires dans les sections ci-dessous pour certaines des fonctions répertoriées ci-dessus. Pour le reste des fonctions répertoriées, reportez-vous à la documentation sur les fonctions [générales) dans la section Préparation des données ](/help/data-prep/functions.md).

### `array_to_string` fonction pour exporter des tableaux {#array-to-string-function-export-arrays}

Utilisez la fonction `array_to_string` pour concaténer les éléments d’un tableau en chaîne, à l’aide du séparateur souhaité, tel que `_` ou `|`. Cette fonction est utile lorsque vous souhaitez exporter les éléments d’un tableau d’Experience Platform dans un fichier CSV.

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

### `filterArray` fonction pour exporter des tableaux filtrés {#filter-array}

Utilisez la fonction `filterArray` pour filtrer les éléments d’un tableau exporté. Vous pouvez combiner cette fonction avec la fonction `array_to_string` décrite plus haut.

En poursuivant avec l’objet de tableau `organizations` ci-dessus, vous pouvez écrire une fonction telle que `array_to_string('_', filterArray(organizations, org -> org.founded > 2021))`, qui renvoie les organisations avec une valeur pour `founded` en 2021 ou plus récent.

![Exemple de la fonction filterArray.](/help/destinations/assets/ui/export-arrays-calculated-fields/filter-array-function.png)

Dans ce cas, votre fichier de sortie ressemble à ce qui suit. Notez comment les deux éléments du tableau qui répondent au critère sont concaténés en une seule chaîne à l’aide du caractère `_` .

```
John,Doe,johndoe@acme.org, "{'id':123,'orgName':'Acme Inc','founded':1990,'latestInteraction':1708041600000}_{'id':789,'orgName':'Energy Corp','founded':2021,'latestInteraction':1725753600000}"
```

### `transformArray` fonction pour exporter des tableaux transformés {#transform-array}

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

### `flattenArray` fonction pour exporter des tableaux aplatis {#flatten-array}

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

### Fonctions de hachage {#hashing-functions}

D’autres fonctions disponibles sont spécifiques à l’exportation de tableaux ou d’éléments à partir d’un tableau. Vous pouvez utiliser des fonctions de hachage pour hacher les attributs dans les fichiers exportés. Par exemple, si vous disposez d’informations d’identification personnelle dans les attributs, vous pouvez hacher ces champs lors de leur exportation.

Vous pouvez hacher directement des valeurs de chaîne, par exemple `md5(personalEmail.address)`. Si vous le souhaitez, vous pouvez également hacher des éléments individuels des champs de tableau, en supposant que les éléments du tableau soient des chaînes, comme suit : `md5(purchaseTime[0])`

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
