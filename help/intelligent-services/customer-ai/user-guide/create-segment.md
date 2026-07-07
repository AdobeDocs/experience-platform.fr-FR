---
keywords: Experience Platform;informations;ia dédiée aux clients;rubriques populaires;segments ia dédiée aux clients
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Création d’audiences avec les scores prévus
description: Lorsqu’une opération de prédiction se termine, les scores de propension prévus sont automatiquement utilisés par les Profils. L’enrichissement des profils avec les scores de l’IA dédiée aux clients permet la création d’audiences pour rechercher des audiences en fonction de leurs scores de propension. Cette section décrit les étapes à suivre pour créer des audiences à l’aide du créateur de segments.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
TQID: https://experienceleague.adobe.com/PxH6ueD8AhgcHy8Jy6a-itezQ-p543PLPInSBp205Xo
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2: id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: eaa89f1252ffc001c299b985e479afb8ac33d053
workflow-type: tm+mt
source-wordcount: 332
ht-degree: 17%

---

# Création d’audiences avec des scores prévus

Lorsqu’une opération de prédiction se termine, les scores de propension prévus sont automatiquement utilisés par les Profils. L’enrichissement des profils avec les scores de l’IA dédiée aux clients permet la création d’audiences pour rechercher des audiences en fonction de leurs scores de propension. Cette section décrit les étapes à suivre pour créer des audiences à l’aide du Créateur d’audience. Pour un tutoriel plus détaillé sur la création d’audiences, consultez le [guide d’utilisation du Créateur d’audience](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Pour utiliser cette méthode, le profil client en temps réel doit être activé pour le jeu de données.

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Audiences]** dans le volet de navigation de gauche, suivi de **[!UICONTROL Créer une audience]**.

![Capture d’écran de la page Audiences de l’interface utilisateur d’Experience Platform, présentant l’option de création d’une audience.](../images/user-guide/segments_new.png)

Le **créateur de segments** s’affiche. Dans la colonne de gauche **[!UICONTROL Champs]** et sous l’onglet **[!UICONTROL Attributs]**, sélectionnez le dossier nommé **[!UICONTROL Profil individuel XDM]** puis sélectionnez le dossier avec l’espace de noms de votre organisation. Le dossier nommé **[!UICONTROL IA dédiée aux clients]** contient les résultats des exécutions de prédiction et sont nommés en fonction de l’instance à laquelle les scores appartiennent. Cliquez sur un dossier d’instance pour accéder à ses résultats pour l’instance souhaitée.

![](../images/user-guide/results_new.png)

Situé au centre du créateur de segments, faites glisser et déposez l’attribut **[!UICONTROL Score]** sur la zone de travail du créateur de règles *rule* pour définir une règle.

Dans la colonne de droite *Propriétés de l’audience*, attribuez un nom à l’audience.

![](../images/user-guide/properties_new.png)

Au-dessus de la colonne de gauche *Champs*, sélectionnez l’icône **engrenage** et sélectionnez une *Politique de fusion* dans la liste déroulante. Sélectionnez **[!UICONTROL Enregistrer]** pour créer l’audience.

![](../images/user-guide/merge_policy_new.png)

## Étapes suivantes

Ce tutoriel vous a permis de trouver des audiences en fonction de leurs scores de propension à l’aide du créateur de segments. Vous pouvez désormais cibler vos audiences en les activant sur les destinations. Pour plus d’informations, consultez [Présentation des destinations](../../../destinations/home.md).
