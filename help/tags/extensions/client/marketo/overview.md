---
title: Présentation de l’extension Marketo Munchkin
description: Découvrez l’extension de balises Marketo Munchkin dans Adobe Experience Platform.
exl-id: 8efc5203-91fc-4e89-be8f-74bf1aeeee5f
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 98%

---

# Présentation de l’extension Marketo Munchkin

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Utilisez cette extension pour intégrer le code de suivi JavaScript [!DNL Marketo Munchkin] à votre propriété. [!DNL Marketo Munchkin] JavaScript permet le suivi des visites et des clics des pages des utilisateurs finaux vers vos pages web externes et vos pages de destination Marketo.

## Installer l’extension Marketo Munchkin

Si lʼextension [!DNL Marketo Munchkin] nʼest pas encore installée, ouvrez votre propriété, puis cliquez sur **[!UICONTROL Extensions > Catalogue]**, survolez lʼextension [!DNL Marketo Munchkin] et cliquez sur **[!UICONTROL Installer]**.

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
