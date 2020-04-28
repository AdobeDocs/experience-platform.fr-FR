---
keywords: Experience Platform;insights; customer ai;popular topics
solution: Experience Platform
title: Création de segments client avec des scores prévus
topic: Create a segment
translation-type: tm+mt
source-git-commit: 66ccea896846c1da4310c1077e2dc7066a258063

---


# Création de segments client avec des scores prévus

Lorsqu’une opération de prédiction se termine, les scores de propension prévus sont automatiquement utilisés par les Profils. L’enrichissement des  avec des scores d’IA du client permet de créer des segments de clients pour trouver  en fonction de leurs scores de propension. Cette section décrit les étapes à suivre pour créer des segments à l’aide du créateur de segments. Pour un tutoriel plus complet sur la création de segments, consultez le [guide d’utilisation du créateur de segments](../../../segmentation/tutorials/create-a-segment.md).

>[!IMPORTANT] Afin d’utiliser cette méthode, le  du client en temps réel doit être activé pour le jeu de données.

In the Platform UI, click **[!UICONTROL Segments]** in the left navigation, and then click **[!UICONTROL Create segment]**.

![](../images/user-guide/segments.png)

Le *créateur de segments* s’affiche. Dans la colonne *Champs* à gauche, sous l’onglet *Attributs*, cliquez sur le dossier nommé **[!UICONTROL XDM Individual Profile]**, puis sur le dossier avec l’espace de noms de votre organisation. Le dossier nommé **[!UICONTROL Customer AI]** contient les résultats des opérations de prédiction et est nommé d’après l’instance à laquelle sont associés les scores. Cliquez sur un dossier d’instance pour accéder aux résultats de l’instance souhaitée.

![](../images/user-guide/results.png)

Faites glisser l’attribut **[!UICONTROL Score]** sur le *canevas du créateur de règles* situé au centre du créateur de segments pour définir une règle.

Sous la colonne de propriétés *de* segment de droite, attribuez un nom au segment.

![](../images/user-guide/properties.png)

Au-dessus de la colonne *Champs* de gauche, cliquez sur l’icône **d’engrenage** et sélectionnez une stratégie *de* fusion dans la liste déroulante. Cliquez sur **[!UICONTROL Save]** pour créer le segment.

![](../images/user-guide/merge_policy.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez réussi à trouver   en fonction de leurs scores de propension à l’aide du Créateur de segments. Vous pouvez désormais  votre  de en les activant vers des destinations. See the [destinations overview](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) for more information.