---
keywords: activer les destinations;activer les données
title: Présentation de l’activation
type: Tutorial
description: Découvrez comment activer les audiences que vous avez dans Adobe Experience Platform vers différents types de destinations.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
TQID: https://experienceleague.adobe.com/57dVog9ZkGiqnfLTf6oHgvyanMB0Hl12jzoRO-K63Q8
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 358
ht-degree: 25%

---

# Présentation de l’activation

>[!IMPORTANT]
>
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

[!DNL Adobe Experience Platform] prend en charge un large éventail de destinations. Le workflow d’activation des audiences varie entre les destinations, en fonction du type de données d’audience qu’elles prennent en charge, et de la fréquence d’exportation des données.

## Méthodes d’activation {#activation-methods}

Après avoir [configuré la destination](connect-destination.md), vous pouvez activer les audiences de plusieurs manières :

### Activer des audiences à partir du catalogue des destinations {#activate-from-catalog}

Consultez les guides suivants pour obtenir des informations détaillées sur l’activation des audiences vers la destination à partir du catalogue des destinations :

* [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](activate-segment-streaming-destinations.md)
* [Activer les données d’audience vers des destinations d’exportation de profils de diffusion en continu](activate-streaming-profile-destinations.md)
* [Activer les données d’audience vers des destinations d’exportation de profils par lots](activate-batch-profile-destinations.md)

### Activer des audiences à partir de la page [!UICONTROL Parcourir] {#activate-from-browse}

Suivez les étapes ci-dessous pour activer des données vers vos destinations à partir de la page **[!UICONTROL Parcourir]**.

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Parcourir]**.

   ![Onglet Parcourir](../assets/ui/activation-overview/browse-tab.png)

1. Recherchez la connexion de destination à utiliser pour activer des segments, sélectionnez les trois points de la colonne [!UICONTROL Nom], puis sélectionnez **[!UICONTROL Activer des audiences]**.

   ![bouton Activer les audiences](../assets/ui/activation-overview/activate-segments.png)

1. En fonction de la destination sélectionnée, suivez les étapes décrites dans les articles ci-dessous, en commençant par l’étape **[!UICONTROL Sélectionner des segments]**, pour terminer le workflow d’activation :

   * [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](activate-segment-streaming-destinations.md)
   * [Activer les données d’audience vers des destinations d’exportation de profils de diffusion en continu](activate-streaming-profile-destinations.md)
   * [Activer les données d’audience vers des destinations d’exportation de profils par lots](activate-batch-profile-destinations.md)

### Activer des audiences à partir de la page des détails de l’audience {#activate-audience-details}

Vous pouvez activer des audiences vers des destinations à partir de la page des détails de l’audience. Voir [Détails de l’audience](../../segmentation/ui/audience-portal.md#audience-details) pour plus d’informations.

Selon la destination sélectionnée, suivez les étapes décrites dans les articles ci-dessous pour terminer le workflow d’activation :

* [Activer les données d’audience vers des destinations d’export d’audiences en flux continu](activate-segment-streaming-destinations.md)
* [Activer les données d’audience vers des destinations d’exportation de profils de diffusion en continu](activate-streaming-profile-destinations.md)
* [Activer les données d’audience vers des destinations d’exportation de profils par lots](activate-batch-profile-destinations.md)
