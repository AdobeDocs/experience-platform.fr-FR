---
keywords: modifier l’activation, modifier la destination, modifier la destination
title: Modification des flux de données d’activation
type: Tutorial
description: Suivez les étapes de cet article pour modifier un flux de données d’activation existant dans Adobe Experience Platform.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 1%

---

# Modification des flux de données d’activation {#edit-activation-flows}

Dans Adobe Experience Platform, vous pouvez modifier divers composants des flux de données d’activation existants vers les destinations, tels que les segments et les attributs de profil exportés, la fréquence d’exportation, si le flux de données d’activation est activé ou désactivé, etc.

## Modifier les flux de données {#edit-dataflows}

Suivez les étapes ci-dessous pour modifier les flux de données d’activation existants :

1. Connectez-vous au [Interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionner **[!UICONTROL Parcourir]** dans l’en-tête supérieur pour afficher vos flux de données de destination existants.

   ![Parcourir les destinations](../assets/ui/edit-activation/browse-destinations.png)

2. Icône Sélectionner le filtre ![Icône Filtre](../assets/ui/edit-activation/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de flux de données associés à la destination sélectionnée.

   ![Filtrage des destinations](../assets/ui/edit-activation/filter-destinations.png)

3. Sélectionnez le nom du flux de données de destination que vous souhaitez modifier.

   ![Sélectionnez des destinations](../assets/ui/edit-activation/destination-select.png)

4. Le **[!UICONTROL Exécutions de flux de données]** pour la destination s’affiche, affichant ses commandes disponibles. À ce stade, vous pouvez modifier plusieurs composants du flux de données de destination :

   * Sélectionner **[!UICONTROL Activation des segments]** dans le rail de droite pour modifier les segments ou attributs de profil à envoyer à la destination. Cette action vous conduit au workflow d’activation, qui varie en fonction du type de destination. Pour plus d’informations, consultez les guides sur :
      * [activation des données d’audience pour segmenter les destinations de diffusion en continu](./activate-segment-streaming-destinations.md) (par exemple, Facebook ou Twitter) ;
      * [activation des données d’audience vers des destinations basées sur un profil de lot](./activate-batch-profile-destinations.md) (par exemple, Amazon S3 ou Oracle Eloqua) ;
      * [activation des données d’audience vers des destinations basées sur un profil de diffusion en continu](./activate-streaming-profile-destinations.md) (par exemple, API HTTP ou Amazon Kinesis).
   * De plus, vous pouvez modifier le nom et la description du flux de données de destination.
   * Vous pouvez utiliser la variable **[!UICONTROL Activé]/[!UICONTROL Désactivé]** pour démarrer et suspendre toutes les exportations de données vers la destination.

   ![Détails de la destination](../assets/ui/edit-activation/destination-details.png)

## Étapes suivantes {#next-steps}

En suivant ce tutoriel, vous avez utilisé avec succès la méthode **[!UICONTROL destinations]** espace de travail pour mettre à jour les flux de données de destination existants.

Pour plus d’informations sur les destinations, reportez-vous à la section [présentation des destinations](../catalog/overview.md).
