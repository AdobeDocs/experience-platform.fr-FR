---
title: Mise en œuvre de l’extension Adobe Experience Platform Assurance
description: Ce guide explique comment implémenter et installer l’extension Adobe Experience Platform Assurance.
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
TQID: https://experienceleague.adobe.com/C2q6JWgloytbZFx-gac44fNJkFpb85at43uM-YPpxNE
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: ae2cba0e-54f2-464b-a3b3-ad371e8a886a
  - id: b64298cc-90cc-46b7-8917-ee391f1c7516
  - id: c1f1ac67-ccab-4be9-a93a-b7faba1192c4
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: f6ff4d13-7b5c-4533-8556-95e76673d4cb
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 409
ht-degree: 2%

---

# Mise en œuvre de l’extension Adobe Experience Platform Assurance

Ce tutoriel explique comment installer et implémenter l’extension Experience Platform Assurance dans Mobile SDK. Pour obtenir des instructions sur l’ajout de l’extension Assurance à votre application, veuillez lire la [présentation de l’extension Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Prise en main

Pour installer et implémenter l’extension Assurance, vous devez avoir accès aux services suivants :

- Interface utilisateur de la collecte de données de Adobe Experience Platform [&#128279;](https://experience.adobe.com/#/data-collection/)
- [Assurance d’Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## Création d’une propriété mobile

>[!NOTE]
>
>Si vous disposez déjà d’une propriété mobile, vous pouvez passer à l’étape suivante.

Dans l’interface utilisateur de collecte de données, sélectionnez **[!UICONTROL Tags]**. Une liste des propriétés mobiles et web s’affiche, avec des informations sur les propriétés appartenant à votre organisation. Sélectionnez **[!UICONTROL New property]** pour créer une propriété.

![Le bouton Nouvelle propriété est mis en surbrillance et indique les éléments que vous sélectionnez pour créer une propriété](./images/implement-assurance/create-new-property.png)

La page **[!UICONTROL Create Property]** s’affiche. Saisissez le nom de votre nouvelle propriété et sélectionnez **[!UICONTROL Mobile]** comme plateforme. Après avoir inséré vos détails, sélectionnez **[!UICONTROL Save]** pour créer la propriété mobile.

>[!NOTE]
>
>Le paramètre de **[!UICONTROL Privacy]** de la propriété mobile n’affecte **pas** la collecte de données d’Assurance.

![La page Créer une propriété s’affiche. Vous pouvez insérer des informations sur votre propriété mobile ici.](./images/implement-assurance/create-property.png)

## Installation de l’extension Assurance

Sélectionnez la propriété mobile dans laquelle vous souhaitez installer l’extension Assurance.

![La page Propriétés de la balise s’affiche avec la propriété mobile sélectionnée en surbrillance.](./images/implement-assurance/select-mobile-property.png)

La page **détails de la propriété mobile** s’affiche. Sélectionnez **[!UICONTROL Extensions]** pour afficher la liste des extensions actuellement associées à votre propriété mobile.

![La page de détails des propriétés mobiles s’affiche. Des informations sur les activités récentes s’affichent. L’onglet Extensions est mis en surbrillance.](./images/implement-assurance/tag-properties.png)

Sélectionnez **[!UICONTROL Catalog]** pour afficher la liste des extensions que vous pouvez ajouter à la propriété mobile. À l’aide du filtre, recherchez l’extension **[!UICONTROL AEP Assurance]**, puis sélectionnez **[!UICONTROL Install]**.

![Le catalogue d’extensions s’affiche. L’extension Assurance est filtrée et affichée, avec le bouton d’installation en surbrillance.](./images/implement-assurance/assurance-extension.png)

## Étapes suivantes

Maintenant que vous avez installé l’extension Assurance dans votre propriété mobile, vous pouvez commencer à utiliser Assurance dans vos applications. Pour savoir comment ajouter l’extension Assurance à votre application, veuillez lire la présentation de l’extension [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Pour savoir comment utiliser Assurance, consultez le [guide d’utilisation d’Assurance](./using-assurance.md).
