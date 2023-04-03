---
title: Affichage des versions des extensions
description: Ce guide contient des informations détaillées sur la vue Versions des extensions dans Adobe Experience Platform Assurance.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Affichage des versions d’extension

La vue Version des extensions vous permet de classer et d’afficher rapidement les extensions mobiles Adobe Experience Platform que vous avez installées et si elles sont à jour dans un client connecté à une session d’assurance.

## Prise en main des vues Versions d’extension

Après [configuration de Assurance](../tutorials/implement-assurance.md), dans la variable **Accueil** vue, sélectionnez **[!UICONTROL Versions d’extension]**

![Versions d’extension](./images/versions/versions-extension.png)

## Vérifiez si votre version est à jour

Dans cette vue, un tableau affiche la dernière version de chaque SDK Mobile, ainsi que la version actuelle que vous avez installée, le cas échéant. Lorsqu’une version est synchronisée avec la dernière version, la version installée affiche un badge vert. Sinon, le badge s&#39;affichera en rouge.

![Comparaison des versions d’extension](./images/versions/versions-extension-version.png)

## Exporter les versions

En haut à droite de la vue, vous pouvez sélectionner **[!UICONTROL Exportation de versions]** qui fournit une charge utile JSON avec toutes les informations d’extension, ainsi que la plateforme utilisée par le client. Vous pouvez choisir d’exporter ces données vers un fichier JSON ou de les copier dans le presse-papiers.

![Exportation des versions d’extension](./images/versions/versions-extension-export.png)
