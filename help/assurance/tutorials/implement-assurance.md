---
title: Implémentation de l’extension Adobe Experience Platform Assurance
description: Ce guide explique comment mettre en oeuvre et installer l’extension Adobe Experience Platform Assurance.
source-git-commit: 24f452bdb923179eefe53fdb28d3a92d43e533cd
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 2%

---


# Mise en oeuvre de l’extension Adobe Experience Platform Assurance

Ce tutoriel explique comment installer et mettre en oeuvre l’extension Platform Assurance dans le SDK Mobile. Pour obtenir des instructions sur l’ajout de l’extension Assurance à votre application, veuillez lire la section [Présentation de l’extension Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Prise en main

Pour installer et mettre en oeuvre l’extension Assurance, vous devez accéder aux services suivants :

- Le [Interface utilisateur de la collecte de données Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## Créer une propriété mobile

>[!NOTE]
>
>Si vous disposez déjà d’une propriété mobile, vous pouvez passer à l’étape suivante.

Dans l’interface utilisateur de la collecte de données, sélectionnez **[!UICONTROL Balises]**. Une liste des propriétés mobiles et web s’affiche, avec des informations sur les propriétés qui appartiennent à votre organisation. Sélectionner **[!UICONTROL Nouvelle propriété]** pour créer une propriété.

![Le bouton Nouvelle propriété est mis en surbrillance et indique ce que vous choisissez pour créer une propriété.](./images/implement-assurance/create-new-property.png)

Le **[!UICONTROL Créer une propriété]** s’affiche. Saisissez le nom de la nouvelle propriété et sélectionnez **[!UICONTROL Mobile]** comme votre plateforme. Après avoir inséré vos détails, sélectionnez **[!UICONTROL Enregistrer]** pour créer la propriété mobile.

>[!NOTE]
>
>La propriété mobile de **[!UICONTROL Confidentialité]** définit **not** affectent la collecte de données d’Assurance.

![La page Créer une propriété s’affiche. Vous pouvez insérer des informations sur votre propriété mobile ici.](./images/implement-assurance/create-property.png)

## Installation de l’extension Assurance

Sélectionnez la propriété mobile dans laquelle vous souhaitez installer l’extension Assurance.

![La page Propriétés de la balise s’affiche et la propriété mobile sélectionnée est mise en surbrillance.](./images/implement-assurance/select-mobile-property.png)

Le **détails des propriétés mobiles** s’affiche. Sélectionner **[!UICONTROL Extensions]** pour afficher la liste des extensions actuellement associées à votre propriété mobile.

![La page de détails des propriétés mobiles s’affiche. Des informations sur les activités récentes s’affichent. L’onglet Extensions est mis en surbrillance.](./images/implement-assurance/tag-properties.png)

Sélectionner **[!UICONTROL Catalogue]** pour afficher la liste des extensions que vous pouvez ajouter à la propriété mobile. À l’aide du filtre, recherchez la variable **[!UICONTROL Assurance AEP]** et sélectionnez **[!UICONTROL Installer]**.

![Le catalogue des extensions s’affiche. L’extension Assurance est filtrée pour et affichée, le bouton d’installation étant surligné.](./images/implement-assurance/assurance-extension.png)

## Étapes suivantes

Maintenant que vous avez installé l’extension Assurance dans votre propriété mobile, vous pouvez commencer à utiliser Assurance dans vos applications. Pour savoir comment ajouter l’extension Assurance à votre application, veuillez lire le [Présentation de l’extension Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Pour savoir comment utiliser Assurance, veuillez lire le [utilisation du guide Assurance](./using-assurance.md).
