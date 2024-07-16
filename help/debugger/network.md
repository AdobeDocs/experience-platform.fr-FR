---
title: Onglet Réseau
description: Découvrez comment utiliser l’onglet Réseau dans Adobe Experience Platform Debugger.
keywords: debugger;extension Experience Platform Debugger;chrome;extension;réseau;informations
seo-description: Experience Platform Debugger Network screen
seo-title: Network Tab
uuid: 839686c9-6e4f-4661-acf6-150ea24dc47f
exl-id: ed0579ef-ec26-43df-9453-a395c105038a
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 59%

---

# Onglet Réseau

L’onglet **Réseau** regroupe tous les appels de solution Adobe Experience Cloud effectués sur la page et les affiche dans l’ordre de gauche à droite. Les paramètres standard sont automatiquement étiquetés avec des noms conviviaux et organisés pour regrouper des paramètres communs sur le même rôle.

![](images/network.jpg)

Cet écran est utile pour comparer des paires clé-valeur entre les accès. Vous pouvez confirmer que les paramètres utilisés pour les intégrations, tels que l’identifiant visiteur Experience Cloud ou l’ID de données supplémentaires, sont cohérents entre les intégrations.

>[!NOTE]
>
>Actuellement, tous les paramètres transmis dans les appels de solution (par exemple, les variables contextuelles Analytics, les paramètres personnalisés Target ou les ID de client du service Experience Cloud ID) ne sont pas visibles dans l’écran Réseau.

Pour modifier les informations par solution, sélectionnez la solution que vous souhaitez afficher depuis la liste dans le volet de navigation de gauche. L’exemple suivant est filtré pour n’afficher qu’Analytics :

![](images/network-analytics.jpg)

Pour revenir à l’affichage de toutes les solutions, sélectionnez **[!UICONTROL Network]**

Sélectionnez sur un élément de la vue Réseau pour afficher une vue étendue. Vous pouvez copier les informations affichées dans le Presse-papiers à partir de la fenêtre d’affichage agrandie.

![](images/network-expand.jpg)

<!--Use the icon at the top of each column to copy the server call URL to your clipboard, where you can paste it into another document for reference or debugging purposes.

![](images/copy.jpg)-->

Pour effacer la liste, sélectionnez **[!UICONTROL Supprimer les événements]**.

Pour télécharger un fichier Excel contenant les informations de cet écran, sélectionnez **[!UICONTROL Télécharger]**.
