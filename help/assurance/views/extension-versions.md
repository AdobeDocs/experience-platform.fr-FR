---
title: Vue des versions des extensions
description: Ce guide détaille les informations sur la vue Versions des extensions dans Adobe Experience Platform Assurance.
exl-id: a3a649da-1ef1-45a3-a1ed-6a7bc16c2987
TQID: https://experienceleague.adobe.com/gv2F7ceZv5wnWwYkXPj2zq8oVQh7BYfSVWg32IDY-Cc
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 186
ht-degree: 0%

---

# Vue Versions d’extension

La vue Version des extensions vous permet de classer et de visualiser rapidement les extensions mobiles Adobe Experience Platform que vous avez installées et si elles sont à jour dans un client connecté à une session Assurance.

## Prise en main des vues des versions d’extension

Après avoir [configuré Assurance](../tutorials/implement-assurance.md), dans la vue **Accueil**, sélectionnez **[!UICONTROL Extension Versions]**

![Versions d’extension](./images/versions/versions-extension.png)

## Vérifier si votre version est à jour

Dans cette vue, un tableau affiche la dernière version de chaque Mobile SDK, ainsi que la version actuelle que vous avez installée, le cas échéant. Lorsqu’une version est synchronisée avec la dernière version, la version installée affiche un badge vert. Sinon, le badge sera affiché en rouge.

![Comparaison des versions d’extension](./images/versions/versions-extension-version.png)

## Exporter les versions

En haut à droite de la vue, vous pouvez sélectionner **[!UICONTROL Export Versions]** qui vous donne une payload JSON avec toutes les informations d’extensions, ainsi que la plateforme utilisée par le client. Vous pouvez choisir d’exporter ces données vers un fichier JSON ou de les copier dans le presse-papiers.

![&#x200B; Exportation des versions d’extension &#x200B;](./images/versions/versions-extension-export.png)
