---
title: Exporter des tableaux, des mappages et des objets à partir de Real-Time CDP
type: Tutorial
description: Découvrez comment exporter des tableaux, des mappages et des objets de Real-Time CDP vers des destinations d’espace de stockage.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: f7ff10dd6489842adb8de49b3f8634c20d77cc71
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 13%

---

# Exporter des tableaux, des mappages et des objets à partir de Real-Time CDP {#export-arrays-cloud-storage}

>[!AVAILABILITY]
>
>La fonctionnalité d’exportation de tableaux et d’autres objets complexes vers des destinations d’espace de stockage est généralement disponible pour les destinations suivantes : [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md).
>
>De plus, vous pouvez exporter des champs de type mappage vers les destinations suivantes : [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [API HTTP](/help/destinations/catalog/streaming/http-destination.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md).


Découvrez comment exporter des tableaux, des mappages et des objets de Real-Time CDP vers des [destinations d’espace de stockage](/help/destinations/catalog/cloud-storage/overview.md). De plus, vous pouvez exporter des champs de type mappage vers des [destinations d’entreprise](/help/destinations/destination-types.md#advanced-enterprise-destinations) et des [destinations de personnalisation Edge limitées](/help/destinations/destination-types.md#edge-personalization-destinations). Lisez ce document pour comprendre le workflow d’exportation, les cas d’utilisation activés par cette fonctionnalité et les limites connues. Consultez le tableau ci-dessous pour comprendre les fonctionnalités disponibles par type de destination.

| Type de destination | Possibilité d’exporter des tableaux, mappages et autres objets personnalisés |
|---|---|
| Destinations de stockage dans le cloud créées par Adobe (Amazon S3, Azure Blob, Azure Data Lake Storage Gen2, zone d’atterrissage des données, stockage dans le cloud Google, SFTP) | Oui, avec le bouton (bascule) Activer l’exportation de tableaux, de mappages et d’objets lors de la configuration d’une connexion de destination. |
| Destinations de marketing par e-mail basées sur des fichiers (Adobe Campaign, Oracle Eloqua, Oracle Responsys, Salesforce Marketing Cloud) | Non |
| Destinations de stockage dans le cloud existantes personnalisées créées par les partenaires (destinations personnalisées basées sur des fichiers créées via Destination SDK) | Non |
| Destinations d’entreprise (Amazon Kinesis, Azure Event Hubs, API HTTP) | Partiellement. Vous pouvez sélectionner et exporter des objets de type map à l’étape de mapping du workflow d’activation. |
| Destinations de streaming (par exemple : Facebook, Braze, le ciblage par liste de clients de Google, etc.) | Non |
| Destinations de personnalisation Edge | Non |

{style="table-layout:auto"}

Utilisez cette page comme référence pour tout ce que vous souhaitez savoir sur l’exportation de tableaux, de mappages et d’autres types d’objets à partir d’Experience Platform.

## Ligne du bas vers le haut

Obtenez les informations les plus importantes sur les fonctionnalités de cette section, et continuez ci-dessous vers les autres sections du document pour obtenir des informations détaillées.

* Pour les destinations de stockage dans le cloud, la possibilité d’exporter des tableaux, des mappages et des objets dépend de votre sélection du bouton (bascule) **Exporter des tableaux, des mappages, des objets**. En savoir plus à ce sujet [plus bas sur la page](#export-arrays-maps-objects-toggle).
* Vous pouvez exporter des tableaux, des mappages et des objets vers des destinations d’espace de stockage dans des fichiers `JSON` et `Parquet`. Pour les destinations de personnalisation d’entreprise et Edge, le type de données exporté est `JSON`. Les audiences de personnes et de prospects sont prises en charge, contrairement aux audiences de compte.
* Pour les destinations de stockage dans le cloud basées sur des fichiers, vous *pouvez* exporter des tableaux, des mappages et des objets vers des fichiers CSV, mais uniquement en utilisant la fonctionnalité de champs calculés et en les concaténant dans une chaîne à l’aide de la fonction `array_to_string`.

## Tableaux et autres types d’objets dans Experience Platform {#arrays-strings-other-objects}

Dans Experience Platform, vous pouvez utiliser des [schémas XDM](/help/xdm/home.md) pour gérer différents types de champs. Avant l’ajout de la prise en charge des exportations de tableaux, vous pouviez exporter des champs de type paire clé-valeur simples, tels que des chaînes, à partir d’Experience Platform vers les destinations souhaitées. `personalEmail.address`:`johndoe@acme.org` est un exemple de champ de ce type, précédemment pris en charge pour l’exportation.

Les autres types de champs d’Experience Platform incluent les champs de tableau. En savoir plus sur la [gestion des champs de tableau dans l’interface utilisateur d’Experience Platform](/help/xdm/ui/fields/array.md). Vous pouvez désormais exporter des objets de tableau, comme dans l’exemple ci-dessous.

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

En plus des tableaux, vous pouvez également exporter des mappages et des objets d’Experience Platform vers la destination d’espace de stockage de votre choix. Pour en savoir plus sur les [mappages](/help/xdm/ui/fields/map.md) et [objets](/help/xdm/ui/fields/object.md), consultez Experience Platform.

## Prérequis {#prerequisites}

[Connectez-vous](/help/destinations/ui/connect-destination.md) à une destination d’espace de stockage souhaitée, suivez les [étapes d’activation pour les destinations d’espace de stockage](/help/destinations/ui/activate-batch-profile-destinations.md) et accédez à l’étape [mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping). Lors de la connexion à la destination cloud souhaitée, vous devez activer le bouton (bascule) **[!UICONTROL Exporter des tableaux, des mappages]** des objets . Pour plus d’informations, reportez-vous à la section ci-dessous.

>[!NOTE]
>
>Pour les destinations de personnalisation d’entreprise et Edge, la prise en charge de l’exportation des champs de type mappage est disponible sans qu’il soit nécessaire de sélectionner un bouton (bascule) **[!UICONTROL Exporter des tableaux, des mappages, des objets]** . Ce bouton (bascule) n’est pas disponible ni requis lors de la connexion à ces types de destinations.

## Bouton bascule Exporter des tableaux, mappages et objets {#export-arrays-maps-objects-toggle}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_maps_objects"
>title="Exporter des tableaux, mappages et objets"
>abstract="<p> <b>Activez</b> ce paramètre pour activer l’export de tableaux, de mappages et d’objets vers des fichiers JSON ou Parquet. Vous pouvez sélectionner ces types d’objets dans la vue du champ source de l’étape de mappage. Lorsque le bouton (bascule) est activé, vous ne pouvez pas utiliser l’option champs calculés à l’étape de mappage.</p><p>Lorsque ce bouton (bascule) est <b>désactivé</b>, vous pouvez utiliser l’option de champs calculés et appliquer diverses fonctions de transformation des données lors de l’activation des audiences. Cependant, vous <i>ne pouvez pas</i> exporter de tableaux, de mappages et d’objets vers des fichiers JSON ou Parquet et devez configurer une destination distincte à cet effet.</p>"

Lors de la connexion à une destination d’espace de stockage basé sur des fichiers, vous pouvez activer ou désactiver le bouton **[!UICONTROL Exporter des tableaux, des mappages]** des objets.

![Le bouton (bascule) Exporter des tableaux, mappages et objets est activé ou désactivé, et la fenêtre contextuelle est mise en surbrillance.](/help/destinations/assets/ui/export-arrays-calculated-fields/export-objects-toggle.gif)

**Activez** ce paramètre pour activer l’export de tableaux, de mappages et d’objets vers des fichiers JSON ou Parquet. Vous pouvez sélectionner ces types d’objets dans la vue du champ source de l’[étape de mappage](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) lors de l’activation d’audiences vers des destinations d’espace de stockage. Cependant, lorsque ce paramètre est activé, vous ne pouvez pas utiliser l’option champs calculés pour transformer les données lors de l’activation.

Lorsque ce bouton (bascule) est **désactivé**, vous pouvez utiliser l’option de champs calculés et appliquer diverses fonctions de transformation des données lors de l’activation des audiences. Cependant, vous ne pouvez pas exporter des tableaux, des mappages et des objets vers des fichiers JSON ou Parquet et devez configurer une destination distincte à cet effet.

## Basculement entre les tableaux, mappages et objets d’exportation *activé* {#export-arrays-maps-objects-toggle-on}

Lorsque ce paramètre est activé, vous pouvez exporter des objets entiers (par exemple, des `person.name`) et des tableaux en les sélectionnant via le sélecteur de champ source dans l’étape de mappage du workflow d’activation.

![Sélectionnez des objets via le sélecteur de champ source à l’étape de mappage du workflow d’activation.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-object.gif)

Lorsque cette option est sélectionnée, l’interface utilisateur empêche les utilisateurs d’utiliser des champs calculés et le contrôle **[!UICONTROL Ajouter des champs calculés]** est désactivé, comme illustré ci-dessous. Pour utiliser les champs calculés pour les transformations de données, configurez une connexion de destination en désactivant l’option .

![Contrôle des champs calculés désactivé.](/help/destinations/assets/ui/export-arrays-calculated-fields/calculated-fields-disabled.png)

## Basculement entre les tableaux, mappages et objets d’exportation *désactivé* {#export-arrays-maps-objects-toggle-off}

Lorsque cette option est définie sur *désactivée*, vous pouvez utiliser l’option champs calculés et appliquer diverses fonctions de transformation des données lors de l’activation des audiences. Cependant, vous ne pouvez pas exporter des tableaux, des mappages et des objets vers des fichiers JSON ou Parquet et devez configurer une destination distincte à cet effet.

Vous *pouvez* exporter des tableaux, des mappages et des objets vers des fichiers CSV à l’aide de la fonctionnalité de champs calculés et les concaténer dans une chaîne à l’aide de la fonction `array_to_string` . [En savoir plus](#array-to-string-function-export-arrays) sur l’utilisation de cette fonction.

En savoir plus sur l’utilisation des champs calculés pour [effectuer des transformations sur les données exportées vers des destinations d’espace de stockage](/help/destinations/ui/data-transformations-calculated-fields.md).

## Exemples de fichiers exportés {#sample-exported-files}

Grâce à cette fonctionnalité, vous pouvez exporter des fichiers Parquet et JSON dans lesquels les données préservent la structure d’Experience Platform. Consultez ci-dessous un exemple de fichier JSON exporté.

+++ Sélectionnez pour afficher le fichier JSON exporté.

```json
{
  "person_name_firstName": "John",
  "person_name_lastName": "Smith",
  "_acmeinc_customer_hs_main_address_scalar": "Oak Avenue No 12",
  "_acmeinc_customer_hs_locations_array": [
    "home address 12",
    "office address 12"
  ],
  "_acmeinc_customer_hs_date_array": [
    "2024-11-14",
    "2024-11-15"
  ],
  "_acmeinc_customer_hs_customer_obj_emails_array0": "john.smith@example.com",
  "_acmeinc_customer_hs_customer_obj": {
    "emails_array": [
      "john.smith@example.com",
      "j.smith@example.com"
    ],
    "name_scalar": "John Smith"
  },
  "_acmeinc_customer_hs_addresses_array_obj": [
    {
      "is_primary": true,
      "streetName_scalar": "Maple Street",
      "streetNo_int": 12
    },
    {
      "is_primary": false,
      "streetName_scalar": "Pine Road",
      "streetNo_int": 45
    }
  ],
  "_acmeinc_customer_hs_addresses_array_obj0": {
    "is_primary": true,
    "streetName_scalar": "Maple Street",
    "streetNo_int": 12
  }
}
```

+++