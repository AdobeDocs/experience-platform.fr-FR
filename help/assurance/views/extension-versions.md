---
title: Affichage des versions des extensions
description: Ce guide contient des informations détaillées sur la vue Versions des extensions dans Adobe Experience Platform Assurance.
exl-id: a3a649da-1ef1-45a3-a1ed-6a7bc16c2987
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Affichage des versions d’extension

La vue Version des extensions vous permet de classer et d’afficher rapidement les extensions mobiles Adobe Experience Platform que vous avez installées et si elles sont à jour dans un client connecté à une session d’assurance.

## Prise en main des vues Versions d’extension

Après avoir [ configuré Assurance](../tutorials/implement-assurance.md), dans la vue **Home**, sélectionnez **[!UICONTROL Extension Versions]**

![Versions d’extension](./images/versions/versions-extension.png)

## Vérifiez si votre version est à jour

Dans cette vue, un tableau affiche la dernière version de chaque SDK Mobile, ainsi que la version actuelle que vous avez installée, le cas échéant. Lorsqu’une version est synchronisée avec la dernière version, la version installée affiche un badge vert. Sinon, le badge s&#39;affichera en rouge.

![Comparaison des versions d’extension](./images/versions/versions-extension-version.png)

## Exporter les versions

En haut à droite de la vue, vous pouvez sélectionner **[!UICONTROL Exporter les versions]** qui vous donne une charge utile JSON avec toutes les informations d’extension, ainsi que la plateforme utilisée par le client. Vous pouvez choisir d’exporter ces données vers un fichier JSON ou de les copier dans le presse-papiers.

![Exportation de versions d’extension](./images/versions/versions-extension-export.png)
