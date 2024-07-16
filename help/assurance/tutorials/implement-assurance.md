---
title: Implémentation de l’extension Adobe Experience Platform Assurance
description: Ce guide explique comment mettre en oeuvre et installer l’extension Adobe Experience Platform Assurance.
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 1%

---

# Mise en oeuvre de l’extension Adobe Experience Platform Assurance

Ce tutoriel explique comment installer et mettre en oeuvre l’extension Platform Assurance dans le SDK Mobile. Pour obtenir des instructions sur l’ajout de l’extension Assurance à votre application, consultez la [présentation de l’extension Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Commencer

Pour installer et mettre en oeuvre l’extension Assurance, vous devez accéder aux services suivants :

- [Interface utilisateur de collecte de données Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## Création d’une propriété mobile

>[!NOTE]
>
>Si vous disposez déjà d’une propriété mobile, vous pouvez passer à l’étape suivante.

Dans l’interface utilisateur de la collecte de données, sélectionnez **[!UICONTROL Balises]**. Une liste des propriétés mobiles et web s’affiche, avec des informations sur les propriétés qui appartiennent à votre organisation. Sélectionnez **[!UICONTROL Nouvelle propriété]** pour créer une propriété.

![ Le bouton Nouvelle propriété est mis en surbrillance, indiquant ce que vous choisissez pour créer une propriété ](./images/implement-assurance/create-new-property.png)

La page **[!UICONTROL Créer une propriété]** s’affiche. Saisissez le nom de votre nouvelle propriété et sélectionnez **[!UICONTROL Mobile]** comme plateforme. Après avoir inséré vos détails, sélectionnez **[!UICONTROL Enregistrer]** pour créer la propriété mobile.

>[!NOTE]
>
>Le paramètre **[!UICONTROL Privacy]** de la propriété mobile n’affecte **pas** la collecte de données d’Assurance.

![La page Créer une propriété s’affiche. Vous pouvez insérer des informations sur votre propriété mobile ici.](./images/implement-assurance/create-property.png)

## Installation de l’extension Assurance

Sélectionnez la propriété mobile dans laquelle vous souhaitez installer l’extension Assurance.

![La page Propriétés de la balise s’affiche, la propriété mobile sélectionnée étant mise en surbrillance.](./images/implement-assurance/select-mobile-property.png)

La page **détails de propriété mobile** s’affiche. Sélectionnez **[!UICONTROL Extensions]** pour afficher la liste des extensions actuellement associées à votre propriété mobile.

![La page de détails des propriétés mobiles s’affiche. Des informations sur les activités récentes s’affichent. L&#39;onglet Extensions est surligné.](./images/implement-assurance/tag-properties.png)

Sélectionnez **[!UICONTROL Catalogue]** pour afficher la liste des extensions que vous pouvez ajouter à la propriété mobile. À l’aide du filtre, recherchez l’extension **[!UICONTROL AEP Assurance]**, puis sélectionnez **[!UICONTROL Installer]**.

![Le catalogue des extensions s’affiche. L’extension Assurance est filtrée pour et affichée, le bouton d’installation étant mis en surbrillance.](./images/implement-assurance/assurance-extension.png)

## Étapes suivantes

Maintenant que vous avez installé l’extension Assurance dans votre propriété mobile, vous pouvez commencer à utiliser Assurance dans vos applications. Pour savoir comment ajouter l’extension Assurance à votre application, consultez la [présentation de l’extension Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Pour savoir comment utiliser Assurance, consultez le [guide d’assurance](./using-assurance.md).
