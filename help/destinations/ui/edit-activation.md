---
keywords: modifier l’activation, modifier la destination, modifier la destination
title: Modifier des flux de données d’activation
type: Tutorial
description: Suivez les étapes de cet article pour modifier un flux de données d’activation existant dans Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: ca33131c505803b74075f6d8331095b016a301a0
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 18%

---

# Modifier des flux de données d’activation {#edit-activation-flows}

Dans Adobe Experience Platform, vous pouvez configurer divers composants des flux de données d’activation existants vers des destinations, tels que :

* [Activer ou désactiver les flux de données d’activation](#enable-disable-dataflows) ;
* [Ajouter des audiences et des attributs de profil supplémentaires](#add-audiences) aux flux de données d’activation ;
* [Ajouter des jeux de données supplémentaires](#add-datasets) aux workflows d’activation ;
* [Modifiez les noms et descriptions](#edit-names-descriptions) pour vos flux de données d’activation ;

<!-- * [Apply access labels](#apply-access-labels) to exported data; -->

## Parcourir les flux de données d’activation {#browse-activation-dataflows}

Suivez les étapes ci-dessous pour parcourir vos flux de données d’activation existants et identifier celui que vous souhaitez modifier.

1. Connectez-vous à l’[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionnez **[!UICONTROL Parcourir]** dans l’en-tête supérieur pour afficher vos flux de données de destination existants.

   ![Parcourir les destinations](../assets/ui/edit-activation/browse-destinations.png)

2. Sélectionnez l’icône filtre ![Icône Filtre](../../images/icons/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrer les destinations](../assets/ui/edit-activation/filter-destinations.png)

3. Sélectionnez le nom du flux de données de destination que vous souhaitez modifier.

   ![Sélectionnez des destinations](../assets/ui/edit-activation/destination-select.png)

4. La page **[!UICONTROL Flux de données en cours d’exécution]** pour la destination s’affiche, affichant ses commandes disponibles. Selon le type de destination, vous pouvez effectuer diverses opérations de flux de données. Consultez les sections suivantes pour chaque opération de flux de données prise en charge.

## Activation ou désactivation des flux de données d’activation {#enable-disable-dataflows}

Utilisez la bascule **[!UICONTROL Activé]/[!UICONTROL Désactivé]** pour démarrer ou suspendre toutes les exportations de données vers la destination.

![Image de l’interface utilisateur Experience Platform montrant le bouton bascule d’exécution de flux de données activé/désactivé.](../assets/ui/edit-activation/enable-toggle.png)

## Ajout d’audiences à un flux de données d’activation {#add-audiences}

Sélectionnez **[!UICONTROL Activer les audiences]** dans le rail de droite pour modifier les audiences ou les attributs de profil à envoyer à la destination. Cette action vous conduit au workflow d’activation, qui varie en fonction du type de destination.

![Image de l’interface utilisateur Experience Platform montrant l’option d’exécution Activer le flux de données d’audiences.](../assets/ui/edit-activation/activate-audiences.png)

Pour plus d’informations sur les workflows d’activation pour chaque type de destination, consultez les guides suivants :

* [Activer les audiences vers des destinations de diffusion en continu](./activate-segment-streaming-destinations.md) (par exemple, Facebook ou Twitter) ;
* [Activer les audiences vers les destinations d’exportation de profil de lot](./activate-batch-profile-destinations.md) (par exemple, Amazon S3 ou Oracle Eloqua) ;
* [Activez les audiences vers les destinations d’exportation de profils en continu](./activate-streaming-profile-destinations.md) (par exemple, API HTTP ou Kinesis Amazon).

## Ajout de jeux de données à un flux de données d’activation {#add-datasets}

Sélectionnez **[!UICONTROL Exporter des jeux de données]** dans le rail de droite pour sélectionner des jeux de données supplémentaires à exporter vers votre destination. Cette option vous permet d’accéder au [workflow d’exportation du jeu de données](export-datasets.md).

>[!NOTE]
>
>Cette option est uniquement visible pour les [destinations qui prennent en charge l’exportation de jeux de données](export-datasets.md#supported-destinations).

![Image de l’interface utilisateur Experience Platform montrant l’option d’exécution de flux de données Exporter des jeux de données.](../assets/ui/edit-activation/export-datasets.png)

<!-- ## Apply access labels {#apply-access-labels}

Select **[!UICONTROL Apply access labels]** to edit the data usage labels for the exported data. See the [data usage labels documentation](../../data-governance/labels/overview.md) to learn more.

![Experience Platform UI image showing the Export datasets dataflow run option.](../assets/ui/edit-activation/apply-access-labels.png) -->

## Modification des noms et descriptions des flux de données d’activation {#edit-names-descriptions}

Pour modifier le nom et la description du flux de données d’activation, utilisez les champs **[!UICONTROL Nom de destination]** et **[!UICONTROL Description]** .

![Détails de la destination](../assets/ui/edit-activation/edit-destination-name-description.png)

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez utilisé l’espace de travail **[!UICONTROL destinations]** pour mettre à jour les flux de données de destination existants.

Pour plus d’informations sur les destinations, consultez la [présentation des destinations](../catalog/overview.md).
