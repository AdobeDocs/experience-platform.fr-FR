---
title: Profils de prospects
description: Découvrez comment créer et utiliser des profils de prospects pour rassembler des informations sur des clients inconnus à l’aide d’informations tierces.
type: Documentation
exl-id: 194d25d6-88ae-4a7a-9b79-39120bced5c7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 4%

---

# Profils de prospects

Adobe Experience Platform vous permet d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes, quel que soit l’endroit ou le moment où ils interagissent avec votre marque.

Les profils de prospects sont utilisés pour représenter des personnes qui n’ont pas encore interagi avec votre entreprise, mais avec lesquelles vous souhaitez établir un contact. Avec les profils de prospect, vous pouvez compléter vos profils client avec des attributs provenant de partenaires tiers de confiance.

## Parcourir {#browse}

Pour accéder aux profils des prospects, sélectionnez **[!UICONTROL Profils]** dans la section **[!UICONTROL Prospects]**.

La page **[!UICONTROL Parcourir]** s’affiche. Une liste de tous les profils de prospects de votre organisation s’affiche.

![Le bouton [!UICONTROL Profils] est mis en surbrillance et affiche la page [!UICONTROL Parcourir] pour les profils de prospects.](../images/prospect-profile/browse-profiles.png)

>[!IMPORTANT]
>
>Bien que la plupart des fonctionnalités de navigation entre les profils client et les profils de prospects soient les mêmes, vous **ne pouvez pas** parcourir les profils de prospects par politique de fusion. En effet, les profils de prospects sont automatiquement régis par une politique de fusion temporelle conçue par le système. Vous trouverez plus d’informations sur les politiques de fusion dans la [présentation des politiques de fusion](../merge-policies/overview.md).

Pour plus d’informations sur la navigation dans les profils, veuillez lire la section [navigation du guide d’utilisation de Profile](./user-guide.md#browse-identity).

## Détails du profil du prospect {#profile-details}

>[!IMPORTANT]
>
>Un profil de prospect expire automatiquement après 25 jours de résidence dans Adobe Experience Platform.

Pour afficher plus d’informations sur un profil de prospect spécifique, sélectionnez un profil sur la page [!UICONTROL Parcourir].

![Un profil de prospect est mis en surbrillance sur la page de navigation.](../images/prospect-profile/select-specific-profile.png)

Des informations sur le profil du prospect s’affichent, y compris les attributs associés au profil et l’appartenance à l’audience.

![La page des détails du profil du prospect s’affiche.](../images/prospect-profile/profile-details.png)

Pour plus d’informations sur ces onglets, veuillez lire la section [Afficher les détails du profil) du guide d’utilisation du profil](./user-guide.md#profile-detail).

Vous pouvez également afficher tous les attributs au format JSON en sélectionnant **[!UICONTROL Afficher JSON]**.

![Le bouton [!UICONTROL Afficher JSON] est mis en surbrillance sur la page des détails du profil du prospect.](../images/prospect-profile/profile-select-view-json.png)

La boîte de dialogue [!UICONTROL Afficher JSON] s’affiche. Les attributs du profil du prospect sont désormais affichés au format JSON.

![Les attributs du profil du prospect sont affichés au format JSON.](../images/prospect-profile/profile-view-json.png)

## Exemples d’utilisation {#use-cases}

Pour découvrir comment utiliser la fonctionnalité de profils de prospect d’Experience Platform en combinaison avec d’autres fonctionnalités d’Experience Platform, veuillez lire la documentation de cas d’utilisation suivante :

- [Atteindre et acquérir une nouvelle clientèle à l’aide de la fonctionnalité de prospection](../../rtcdp/partner-data/prospecting.md)

## Étapes suivantes

Après avoir lu ce guide, vous comprenez maintenant comment les profils de prospect peuvent être utilisés dans Adobe Experience Platform. Pour savoir comment ces profils de prospects peuvent être utilisés dans les audiences, veuillez lire le guide [Audiences de prospects](../../segmentation/types/prospect-audiences.md).
