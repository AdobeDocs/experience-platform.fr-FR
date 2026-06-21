---
title: Onglet Réseau
description: Découvrez comment utiliser l’onglet Réseau dans Adobe Experience Platform Debugger.
keywords: debugger;extension Experience Platform Debugger;chrome;extension;réseau;informations
seo-description: Experience Platform Debugger Network screen
seo-title: Network Tab
uuid: 839686c9-6e4f-4661-acf6-150ea24dc47f
exl-id: ed0579ef-ec26-43df-9453-a395c105038a
TQID: https://experienceleague.adobe.com/pHNSxx-HRE2sJKyKq8nLQKAu3ps7cO3gb1iMVntSV58
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: ed0d8d0e-04b9-4326-be72-a0fbca265377
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 219
ht-degree: 59%

---

# Onglet Réseau

L’onglet **Réseau** agrège tous les appels de solution Adobe Experience Cloud effectués sur la page et les affiche dans l’ordre de gauche à droite. Les paramètres standard sont automatiquement étiquetés avec des noms conviviaux et organisés pour regrouper des paramètres communs sur le même rôle.

![](images/network.jpg)

Cet écran est utile pour comparer des paires clé-valeur entre les accès. Vous pouvez confirmer que les paramètres utilisés pour les intégrations, tels que l’identifiant visiteur Experience Cloud ou l’ID de données supplémentaires, sont cohérents entre les intégrations.

>[!NOTE]
>
>Actuellement, tous les paramètres transmis dans les appels de solution (par exemple, les variables contextuelles Analytics, les paramètres personnalisés Target ou les ID de client du service Experience Cloud ID) ne sont pas visibles dans l’écran Réseau.

Pour modifier les informations par solution, sélectionnez la solution que vous souhaitez afficher depuis la liste dans le volet de navigation de gauche. L’exemple suivant est filtré pour n’afficher qu’Analytics :

![](images/network-analytics.jpg)

Pour revenir à l’affichage de toutes les solutions, sélectionnez **[!UICONTROL Réseau]**

Sélectionnez un élément dans la vue Réseau pour afficher une vue développée. Vous pouvez copier les informations affichées dans le Presse-papiers à partir de la fenêtre d’affichage agrandie.

![](images/network-expand.jpg)

<!--
Use the icon at the top of each column to copy the server call URL to your clipboard, where you can paste it into another document for reference or debugging purposes.

![](images/copy.jpg)
-->

Pour effacer la liste, sélectionnez **[!UICONTROL Supprimer les événements]**.

Pour télécharger un fichier Excel contenant les informations affichées sur cet écran, sélectionnez **[!UICONTROL Télécharger]**.
