---
title: Présentation de l’extension Marketo Munchkin
description: Découvrez l’extension de balises Marketo Munchkin dans Adobe Experience Platform.
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 97%

---

# Présentation de l’extension Marketo Munchkin

Utilisez cette extension pour intégrer le code de suivi JavaScript [!DNL Marketo Munchkin] à votre propriété. [!DNL Marketo Munchkin] JavaScript permet le suivi des visites et des clics des pages des utilisateurs finaux vers vos pages web externes et vos pages de destination Marketo.

## Installer l’extension Marketo Munchkin

Si l’extension [!DNL Marketo Munchkin] n’est pas encore installée, ouvrez votre propriété, puis cliquez sur **[!UICONTROL Extensions > Catalog]**, survolez l’extension [!DNL Marketo Munchkin] avec votre souris et cliquez sur **[!UICONTROL Install]**.

Cette extension n’a pas besoin d’être configurée.

## Types d’action de l’extension Marketo Munchkin

Cette section décrit les types d’actions disponibles dans l’extension [!DNL Marketo Munchkin].

### Initialiser

![](../../../images/munchkin-Init.png)

**Munchkin ID : (obligatoire)** ID de compte Munchkin situé sous Admin > Intégration > Menu Munchkin.

**Configurations :** tous les paramètres configurables sont détaillés [ici](https://developers.marketo.com/javascript-api/lead-tracking/configuration/).

### Visite de page web

![](../../../images/munchkin-visit-page.png)

**url : (obligatoire)** chemin d’accès au fichier URL utilisé pour enregistrer la visite d’une page.

**params :** chaîne de requête des paramètres que vous souhaitez enregistrer.

**name :** nom personnalisé de la ressource de la page Web.

### Lien de clic

![](../../../images/munchkin-click-link.png)

**href : (obligatoire)** chemin d’accès au fichier URL utilisé pour enregistrer un clic sur les liens.
