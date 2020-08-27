---
keywords: Experience Platform;insights;customer ai;popular topics
solution: Experience Platform
title: Création de segments client avec des scores prévus
topic: Create a segment
description: Lorsqu’une opération de prédiction se termine, les scores de propension prévus sont automatiquement utilisés par les Profils. L’enrichissement des profils avec les scores Customer AI permet de créer des segments client pour trouver des audiences en fonction de leurs scores de propension. Cette section décrit les étapes à suivre pour créer des segments à l’aide du créateur de segments.
translation-type: tm+mt
source-git-commit: c30bbaead775e68f869b080e24e18d4a23cda973
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 88%

---


# Création de segments client avec des scores prévus

Lorsqu’une opération de prédiction se termine, les scores de propension prévus sont automatiquement utilisés par les Profils. L’enrichissement des profils avec les scores Customer AI permet de créer des segments client pour trouver des audiences en fonction de leurs scores de propension. Cette section décrit les étapes à suivre pour créer des segments à l’aide du créateur de segments. Pour un tutoriel plus complet sur la création de segments, consultez le [guide d’utilisation du créateur de segments](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Afin d’utiliser cette méthode, Real-time Customer Profile doit être activé pour le jeu de données.

Dans l’interface utilisateur de Platform, cliquez sur **[!UICONTROL Segments]** dans le volet de navigation de gauche, puis cliquez sur **[!UICONTROL Créer un segment]**.

![](../images/user-guide/segments.png)

Le *créateur de segments* s’affiche. Dans la colonne *Champs* à gauche, sous l’onglet *Attributs*, cliquez sur le dossier nommé **[!UICONTROL XDM Individual Profile]**, puis sur le dossier avec l’espace de noms de votre organisation. Le dossier nommé **[!UICONTROL Customer AI]** contient les résultats des opérations de prédiction et est nommé d’après l’instance à laquelle sont associés les scores. Cliquez sur un dossier d’instance pour accéder à ses résultats pour l’instance souhaitée.

![](../images/user-guide/results.png)

Faites glisser l’attribut **[!UICONTROL Score]** sur le *canevas du créateur de règles* situé au centre du créateur de segments pour définir une règle.

Sous la colonne de droite *Propriétés du segment*, indiquez un nom pour le segment.

![](../images/user-guide/properties.png)

Above the left-hand *Fields* column, click the **gear** icon and select a *Merge policy* from the drop-down. Cliquez sur **[!UICONTROL Enregistrer]** pour créer le segment.

![](../images/user-guide/merge_policy.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à trouver des audiences basées sur leurs scores de propension à l’aide du Créateur de segments. Vous pouvez désormais cibler vos audiences en les activant sur les destinations. Pour plus d’informations, consultez [Présentation des destinations](https://docs.adobe.com/content/help/fr-FR/experience-platform/rtcdp/destinations/destinations-overview.html).