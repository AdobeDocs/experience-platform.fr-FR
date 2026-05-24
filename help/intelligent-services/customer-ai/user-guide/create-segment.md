---
keywords: Experience Platform;informations;ia dédiée aux clients;rubriques populaires;segments ia dédiée aux clients
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Créer des segments de clients avec les scores prévus
description: Lorsqu’une opération de prédiction se termine, les scores de propension prévus sont automatiquement utilisés par les Profils. L’enrichissement des profils avec les scores Customer AI permet de créer des segments client pour trouver des audiences en fonction de leurs scores de propension. Cette section décrit les étapes à suivre pour créer des segments à l’aide du créateur de segments.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
TQID: https://experienceleague.adobe.com/PxH6ueD8AhgcHy8Jy6a-itezQ-p543PLPInSBp205Xo
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 329
ht-degree: 48%

---

# Création de segments client avec des scores prévus

Lorsqu’une opération de prédiction se termine, les scores de propension prévus sont automatiquement utilisés par les Profils. L’enrichissement des profils avec les scores Customer AI permet de créer des segments client pour trouver des audiences en fonction de leurs scores de propension. Cette section décrit les étapes à suivre pour créer des segments à l’aide du créateur de segments. Pour un tutoriel plus complet sur la création de segments, consultez le [guide d’utilisation du créateur de segments](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Pour utiliser cette méthode, le profil client en temps réel doit être activé pour le jeu de données.

Dans l’interface utilisateur d’Experience Platform, cliquez sur **[!UICONTROL Segments]** dans le volet de navigation de gauche, puis cliquez sur **[!UICONTROL Create segment]**.

![Copie d’écran de la page Segments dans l’interface utilisateur d’Experience Platform, présentant l’option de création d’un segment.](../images/user-guide/segments_new.png)

Le **créateur de segments** s’affiche. Dans la colonne de **[!UICONTROL Fields]** de gauche et sous l’onglet **[!UICONTROL Attributes]** , cliquez sur le dossier nommé **[!UICONTROL XDM Individual Profile]**, puis cliquez sur le dossier avec l’espace de noms de votre organisation. Le dossier nommé **[!UICONTROL Customer AI]** contient les résultats des exécutions de prédiction et est nommé en fonction de l’instance à laquelle les scores appartiennent. Cliquez sur un dossier d’instance pour accéder à ses résultats pour l’instance souhaitée.

![](../images/user-guide/results_new.png)

Situé au centre du créateur de segments, faites glisser et déposez l’attribut **[!UICONTROL Score]** sur la zone de travail du *créateur de règles* pour définir une règle.

Sous la colonne de droite *Propriétés du segment*, indiquez un nom pour le segment.

![](../images/user-guide/properties_new.png)

Au-dessus de la colonne de gauche *Champs*, cliquez sur l’icône **engrenage** et sélectionnez une *Politique de fusion* dans la liste déroulante. Cliquez sur **[!UICONTROL Save]** pour créer le segment.

![](../images/user-guide/merge_policy_new.png)

## Étapes suivantes

Ce tutoriel vous a permis de trouver des audiences en fonction de leurs scores de propension à l’aide du créateur de segments. Vous pouvez désormais cibler vos audiences en les activant sur les destinations. Pour plus d’informations, consultez [Présentation des destinations](../../../destinations/home.md).
