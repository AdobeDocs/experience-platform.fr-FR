---
keywords: modifier l’activation, modifier la destination, modifier la destination
title: Modifier des flux de données d’activation
type: Tutorial
description: Suivez les étapes de cet article pour modifier un flux de données d’activation existant dans Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 25%

---

# Modifier des flux de données d’activation {#edit-activation-flows}

Dans Adobe Experience Platform, vous pouvez modifier divers composants des flux de données d’activation existants vers les destinations, tels que les audiences et les attributs de profil exportés, la fréquence d’exportation, si le flux de données d’activation est activé ou désactivé, etc.

## Modifier les flux de données {#edit-dataflows}

Suivez les étapes ci-dessous pour modifier les flux de données d’activation existants :

1. Connectez-vous à l’[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionnez **[!UICONTROL Parcourir]** dans l’en-tête supérieur pour afficher vos flux de données de destination existants.

   ![Parcourir les destinations](../assets/ui/edit-activation/browse-destinations.png)

2. Sélectionnez l’icône filtre ![Icône Filtre](../assets/ui/edit-activation/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrer les destinations](../assets/ui/edit-activation/filter-destinations.png)

3. Sélectionnez le nom du flux de données de destination que vous souhaitez modifier.

   ![Sélectionnez des destinations](../assets/ui/edit-activation/destination-select.png)

4. La page **[!UICONTROL Flux de données en cours d’exécution]** pour la destination s’affiche, affichant ses commandes disponibles. À ce stade, vous pouvez modifier plusieurs composants du flux de données de destination :

   * Sélectionnez **[!UICONTROL Activer les audiences]** dans le rail de droite pour modifier les audiences ou les attributs de profil à envoyer à la destination. Cette action vous conduit au workflow d’activation, qui varie en fonction du type de destination. Pour plus d’informations, consultez les guides sur :
      * [activation des données d’audience vers des destinations de diffusion en continu d’audience](./activate-segment-streaming-destinations.md) (par exemple, Facebook ou Twitter) ;
      * [activation des données d’audience vers des destinations basées sur un profil de lot](./activate-batch-profile-destinations.md) (par exemple, Amazon S3 ou Oracle Eloqua) ;
      * [activation des données d’audience vers des destinations basées sur un profil de diffusion en continu](./activate-streaming-profile-destinations.md) (par exemple, API HTTP ou Kinesis Amazon).

   * De plus, vous pouvez modifier le nom et la description du flux de données de destination.
   * Vous pouvez utiliser la bascule **[!UICONTROL Activé]/[!UICONTROL Désactivé]** pour démarrer et suspendre toutes les exportations de données vers la destination.

   ![Détails de la destination](../assets/ui/edit-activation/destination-details.png)

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez utilisé l’espace de travail **[!UICONTROL destinations]** pour mettre à jour les flux de données de destination existants.

Pour plus d’informations sur les destinations, consultez la [présentation des destinations](../catalog/overview.md).
