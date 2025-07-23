---
keywords: modifier l’activation, modifier la destination, modifier la destination
title: Modifier des flux de données d’activation
type: Tutorial
description: Suivez les étapes de cet article pour modifier un flux de données d’activation existant dans Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: 24951f7680f134beb64c7679a94bac9b18042af1
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 10%

---

# Modifier des flux de données d’activation {#edit-activation-flows}

Dans Adobe Experience Platform, vous pouvez configurer différents composants des flux de données d’activation existants vers les destinations, tels que :

* [Activer ou désactiver](#enable-disable-dataflows) les flux de données d’activation
* [Ajouter des audiences supplémentaires](#add-audiences) aux flux de données d’activation
* [Modifier les attributs et les identités mappés](#edit-mapped-attributes)
* [Modifier le planning d’activation et la fréquence d’exportation](#edit-schedule-frequency)
* [Ajouter des jeux de données supplémentaires](#add-datasets) au workflow d’activation
* [Appliquer des libellés d’accès](#apply-access-labels) aux données exportées
* [Modifier les noms et les descriptions](#edit-names-descriptions) pour vos flux de données d’activation

## Parcourir les flux de données d’activation {#browse-activation-dataflows}

Suivez les étapes ci-dessous pour parcourir vos flux de données d’activation existants et identifier celui que vous souhaitez modifier.

1. Connectez-vous à l’[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionnez **[!UICONTROL Parcourir]** dans l’en-tête supérieur pour afficher vos flux de données de destination existants.

   ![Parcourir les destinations](../assets/ui/edit-activation/browse-destinations.png)

2. Sélectionnez l’icône filtre ![Icône Filtre](../../images/icons/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrer les destinations](../assets/ui/edit-activation/filter-destinations.png)

3. Sélectionnez le nom du flux de données de destination à modifier.

   ![Sélectionnez des destinations](../assets/ui/edit-activation/destination-select.png)

4. La page **[!UICONTROL Exécution du flux de données]** de la destination s’affiche, affichant ses commandes disponibles. Selon le type de destination, vous pouvez effectuer diverses opérations de flux de données. Reportez-vous aux sections suivantes pour chaque opération de flux de données prise en charge.

## Activer ou désactiver les flux de données d’activation {#enable-disable-dataflows}

Utilisez le bouton (bascule) **[!UICONTROL Activé]/[!UICONTROL Désactivé]** pour démarrer ou suspendre toutes les exportations de données vers la destination.

![Image de l’interface utilisateur d’Experience Platform affichant le bouton (bascule) Activer/Désactiver l’exécution du flux de données.](../assets/ui/edit-activation/enable-toggle.png)

## Ajouter des audiences à un flux de données d’activation {#add-audiences}

Sélectionnez **[!UICONTROL Activer les audiences]** dans le rail de droite pour modifier les audiences à envoyer à la destination. Cette action vous mène au workflow d’activation.

![Image de l’interface utilisateur d’Experience Platform montrant l’option Activer le flux de données des audiences.](../assets/ui/edit-activation/activate-audiences.png)

À l’étape **[!UICONTROL Sélectionner des audiences]** du workflow d’activation, vous pouvez supprimer des audiences existantes ou ajouter de nouvelles audiences au workflow d’activation.

Le workflow d’activation diffère légèrement en fonction du type de destination. Pour plus d’informations sur les workflows d’activation pour chaque type de destination, lisez les guides suivants :

* [ Activer les audiences vers des destinations de diffusion en continu (par exemple, Facebook ou Twitter](./activate-segment-streaming-destinations.md)
* [Activer les audiences vers des destinations d’exportation de profils par lots](./activate-batch-profile-destinations.md) (par exemple, Amazon S3 ou Oracle Eloqua) ;
* [Activez les audiences vers des destinations d’exportation de profil de diffusion en continu](./activate-streaming-profile-destinations.md) (par exemple, API HTTP ou Amazon Kinesis).

## Modifier le planning d’activation et la fréquence d’exportation {#edit-schedule-frequency}

Sélectionnez **[!UICONTROL Activer les audiences]** dans le rail de droite. Cette action vous mène au workflow d’activation.

![Image de l’interface utilisateur d’Experience Platform montrant l’option Activer le flux de données des audiences.](../assets/ui/edit-activation/activate-audiences.png)

Sélectionnez l’étape **[!UICONTROL Planification]** dans le workflow d’activation pour modifier le planning d’activation et la fréquence d’exportation de votre flux de données. Cette étape vous permet de configurer la fréquence d’exportation des données vers la destination.

À l’étape **[!UICONTROL Planification]** du workflow d’activation, vous pouvez :
* Ajustez la fréquence d’exportation.
* Définissez ou modifiez les dates de début et de fin du flux de données d’activation, etc.

Les opérations de planification que vous pouvez effectuer varient légèrement en fonction du type de destination. Pour plus d’informations sur les workflows d’activation pour chaque type de destination, lisez les guides suivants :

* [ Activer les audiences vers des destinations de diffusion en continu (par exemple, Facebook ou Twitter](./activate-segment-streaming-destinations.md)
* [Activer les audiences vers des destinations d’exportation de profils par lots](./activate-batch-profile-destinations.md) (par exemple, Amazon S3 ou Oracle Eloqua) ;
* [Activez les audiences vers des destinations d’exportation de profil de diffusion en continu](./activate-streaming-profile-destinations.md) (par exemple, API HTTP ou Amazon Kinesis).

## Modifier les attributs et les identités mappés {#edit-mapped-attributes}

Sélectionnez **[!UICONTROL Activer les audiences]** dans le rail de droite. Cette action vous mène au workflow d’activation.

![Image de l’interface utilisateur d’Experience Platform montrant l’option Activer le flux de données des audiences.](../assets/ui/edit-activation/activate-audiences.png)

Sélectionnez l’étape **[!UICONTROL Mappage]** dans le workflow d’activation pour modifier les attributs et les identités mappés pour votre flux de données d’activation. Vous pouvez ainsi ajuster les attributs de profil et les identités à exporter vers la destination.

À l’étape **[!UICONTROL Mappage]** du workflow d’activation, vous pouvez :

* Ajoutez de nouveaux attributs ou de nouvelles identités au mappage.
* Supprimez les attributs ou les identités existants du mappage.
* Ajustez l’ordre des mappages pour définir l’ordre des colonnes dans les fichiers exportés.

Le workflow d’activation diffère légèrement en fonction du type de destination. Pour plus d’informations sur les workflows d’activation pour chaque type de destination, lisez les guides suivants :

* [ Activer les audiences vers des destinations de diffusion en continu (par exemple, Facebook ou Twitter](./activate-segment-streaming-destinations.md)
* [Activer les audiences vers des destinations d’exportation de profils par lots](./activate-batch-profile-destinations.md) (par exemple, Amazon S3 ou Oracle Eloqua) ;
* [Activez les audiences vers des destinations d’exportation de profil de diffusion en continu](./activate-streaming-profile-destinations.md) (par exemple, API HTTP ou Amazon Kinesis).

## Ajouter des jeux de données à un flux de données d’activation {#add-datasets}

Sélectionnez **[!UICONTROL Exporter des jeux de données]** dans le rail de droite pour sélectionner des jeux de données supplémentaires à exporter vers la destination. Cette option vous mène au [workflow d’exportation de jeu de données](export-datasets.md).

>[!NOTE]
>
>Cette option est uniquement visible pour les [destinations qui prennent en charge l’exportation des jeux de données](export-datasets.md#supported-destinations).

![Image de l’interface utilisateur d’Experience Platform montrant l’option d’exécution Exporter le flux de données des jeux de données.](../assets/ui/edit-activation/export-datasets.png)

## Appliquer les libellés d’accès {#apply-access-labels}

Sélectionnez **[!UICONTROL Appliquer les libellés d’accès]** pour modifier les libellés d’utilisation des données pour les données exportées. Pour en savoir plus[ consultez la documentation sur les ](../../data-governance/labels/overview.md) libellés d’utilisation des données .

![Image de l’interface utilisateur d’Experience Platform montrant l’option d’exécution Exporter le flux de données des jeux de données.](../assets/ui/edit-activation/apply-access-labels.png)

## Modifier les noms et descriptions des flux de données d’activation {#edit-names-descriptions}

Pour modifier le nom et la description du flux de données d’activation, utilisez les champs **[!UICONTROL Nom de la destination]** et **[!UICONTROL Description]**.

![Détails de la destination](../assets/ui/edit-activation/edit-destination-name-description.png)

## Étapes suivantes {#next-steps}

Ce tutoriel vous a permis d’utiliser l’espace de travail **[!UICONTROL destinations]** pour mettre à jour les flux de données de destination existants.

Pour plus d’informations sur les destinations, consultez la [présentation des destinations](../catalog/overview.md).
