---
title: Profils de prospects
description: Découvrez comment créer et utiliser des profils de prospect pour collecter des informations sur des clients inconnus à l’aide d’informations tierces.
type: Documentation
exl-id: 194d25d6-88ae-4a7a-9b79-39120bced5c7
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 4%

---

# Profils de prospects

Adobe Experience Platform vous permet d’offrir à vos clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque.

Les profils de prospects sont utilisés pour représenter les personnes qui n’ont pas encore interagi avec votre entreprise, mais auxquelles vous souhaitez tendre la main. Avec les profils de prospect, vous pouvez compléter vos profils client avec les attributs de partenaires tiers approuvés.

## Parcourir {#browse}

Pour accéder aux profils de prospect, sélectionnez **[!UICONTROL Profils]** dans la section **[!UICONTROL Prospects]** .

La page **[!UICONTROL Parcourir]** s’affiche. Une liste de tous les profils de prospect pour votre organisation s’affiche.

![Le bouton [!UICONTROL Profils] est mis en surbrillance et affiche la page [!UICONTROL Parcourir] pour les profils de prospect.](../images/prospect-profile/browse-profiles.png)

>[!IMPORTANT]
>
>Bien que la plupart des fonctionnalités de navigation entre les profils client et prospect soient identiques, vous **ne pouvez pas** parcourir les profils de prospect par stratégie de fusion. En effet, les profils de prospect sont automatiquement régis par une stratégie de fusion temporelle conçue par le système. Vous trouverez plus d’informations sur les stratégies de fusion dans la [présentation des stratégies de fusion](../merge-policies/overview.md).

Pour plus d’informations sur la navigation dans les profils, consultez la [section de navigation du guide d’utilisation de Profile](./user-guide.md#browse-identity).

## Détails du profil de projet {#profile-details}

>[!IMPORTANT]
>
>Un profil de prospect expirera automatiquement après 25 jours de résidence dans Adobe Experience Platform.

Pour afficher plus d’informations sur un profil de prospect spécifique, sélectionnez un profil sur la page [!UICONTROL Parcourir].

![Un profil de prospect est mis en surbrillance sur la page de navigation.](../images/prospect-profile/select-specific-profile.png)

Des informations sur le profil du prospect s’affichent, notamment les attributs associés au profil et à l’appartenance à l’audience.

![ La page des détails du profil de prospect s&#39;affiche.](../images/prospect-profile/profile-details.png)

Pour plus d’informations sur ces onglets, consultez la section [Afficher les détails du profil du guide d’utilisation du profil](./user-guide.md#profile-detail).

Vous pouvez également afficher tous les attributs au format JSON en sélectionnant **[!UICONTROL Afficher JSON]**.

![Le bouton [!UICONTROL Afficher JSON] est mis en surbrillance sur la page des détails du profil de prospect.](../images/prospect-profile/profile-select-view-json.png)

La boîte de dialogue [!UICONTROL Afficher JSON] s’affiche. Les attributs du profil de prospect sont désormais affichés dans le formulaire JSON.

![Les attributs du profil de prospect sont affichés dans le formulaire JSON.](../images/prospect-profile/profile-view-json.png)

## Exemples d’utilisation {#use-cases}

Pour savoir comment utiliser la fonctionnalité de profils de prospect en Experience Platform avec d’autres fonctionnalités de Platform, consultez la documentation de cas d’utilisation suivante :

- [Atteindre et acquérir une nouvelle clientèle à l’aide de la fonctionnalité de prospection](../../rtcdp/partner-data/prospecting.md)

## Étapes suivantes

Après avoir lu ce guide, vous comprenez désormais comment les profils de prospect peuvent être utilisés dans Adobe Experience Platform. Pour découvrir comment ces profils de prospect peuvent être utilisés dans les audiences, consultez le [guide des audiences de prospects](../../segmentation/ui/prospect-audience.md).
