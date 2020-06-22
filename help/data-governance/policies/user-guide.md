---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de l’utilisateur des stratégies d’utilisation des données
topic: policies
translation-type: tm+mt
source-git-commit: c4554e3fbc0dd527606b81e2767cb5777b6e81e7
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 1%

---


# Guide de l’utilisateur des stratégies d’utilisation des données

La gouvernance des données d’Adobe Experience Platform fournit une interface utilisateur qui vous permet de créer et de gérer des stratégies d’utilisation des données. Ce document présente un aperçu des actions que vous pouvez effectuer dans l’espace de travail _Stratégies_ de l’interface utilisateur Experience Platform.

>[!IMPORTANT] Toutes les stratégies d’utilisation des données (y compris les stratégies de base fournies par Adobe) sont désactivées par défaut. Pour qu’une stratégie individuelle soit prise en compte pour l’application de la loi, vous devez l’activer manuellement. Consultez la section relative à l’ [activation des stratégies](#enable) pour savoir comment procéder dans l’interface utilisateur.

## Conditions préalables

Ce guide nécessite une bonne compréhension des concepts Experience Platform suivants :

- [Gouvernance des données](../home.md)
- [Stratégies d’utilisation des données](./overview.md)

## Stratégies d’utilisation des données de Vue {#view-policies}

Dans l’interface utilisateur de l’Experience Platform, cliquez sur **[!UICONTROL Stratégies]** pour ouvrir l’espace de travail *[!UICONTROL Stratégies]* . Dans l’onglet **[!UICONTROL Parcourir]** , vous pouvez voir une liste des stratégies disponibles, y compris leurs étiquettes associées, leurs actions marketing et leur état.

![](../images/policies/browse-policies.png)

Cliquez sur une stratégie répertoriée pour en vue la description et le type. Si une stratégie personnalisée est sélectionnée, d’autres contrôles s’affichent pour modifier, supprimer ou [activer/désactiver la stratégie](#enable).

![](../images/policies/policy-details.png)

## Création d’une stratégie d’utilisation des données personnalisée {#create-policy}

Pour créer une stratégie d’utilisation des données personnalisée, cliquez sur **[!UICONTROL Créer une stratégie]** dans le coin supérieur droit de l’onglet **[!UICONTROL Parcourir]** de l’espace de travail *Stratégies* .

![](../images/policies/create-policy-button.png)

Le processus de *[!UICONTROL création de stratégie]* s’affiche. Début en fournissant un nom et une description pour la nouvelle stratégie.

![](../images/policies/create-policy-description.png)

Ensuite, sélectionnez les étiquettes d’utilisation des données sur lesquelles la stratégie sera basée. Lors de la sélection de plusieurs étiquettes, vous avez la possibilité de choisir si les données doivent contenir toutes les étiquettes ou une seule pour que la stratégie s’applique. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Suivant]**.

![](../images/policies/add-labels.png)

L’étape *[!UICONTROL Sélectionner les actions]* marketing s’affiche. Sélectionnez les actions marketing appropriées dans la liste fournie, puis cliquez sur **[!UICONTROL Suivant]** pour continuer.

>[!NOTE] Lors de la sélection de plusieurs actions marketing, la stratégie les interprète comme une règle &quot;OU&quot;. En d’autres termes, la stratégie s’applique si _l’une_ des actions marketing sélectionnées est exécutée.

![](../images/policies/add-marketing-actions.png)

L’étape *[!UICONTROL Révision]* s’affiche, vous permettant de vérifier les détails de la nouvelle stratégie avant de la créer. Une fois que vous êtes satisfait, cliquez sur **[!UICONTROL Terminer]** pour créer la stratégie.

![](../images/policies/policy-review.png)

L’onglet *[!UICONTROL Parcourir]* réapparaît, qui liste désormais la nouvelle stratégie à l’état &quot;Version préliminaire&quot;. Pour activer la stratégie, consultez la section suivante.

![](../images/policies/created-policy.png)

## Activation ou désactivation d’une stratégie d’utilisation des données {#enable}

Toutes les stratégies d’utilisation des données (y compris les stratégies de base fournies par Adobe) sont désactivées par défaut. Pour qu’une stratégie individuelle soit prise en compte pour l’application, vous devez l’activer manuellement par le biais de l’API ou de l’interface utilisateur.

Vous pouvez activer ou désactiver des stratégies à partir de l’onglet *[!UICONTROL Parcourir]* de l’espace de travail *[!UICONTROL Stratégies]* . Sélectionnez une stratégie personnalisée dans la liste pour afficher ses détails à droite. Sous *[!UICONTROL Etat]*, sélectionnez le bouton bascule pour activer ou désactiver la stratégie.

![](../images/policies/enable-policy.png)

## Actions marketing Vue {#view-marketing-actions}

Dans l’espace de travail **[!UICONTROL Stratégies]** , sélectionnez l’onglet Actions **** marketing pour vue d’une liste d’actions marketing disponibles définies par Adobe et votre propre organisation.

![](../images/policies/marketing-actions.png)

## Création d’une action marketing {#create-marketing-action}

Pour créer une action marketing personnalisée, cliquez sur **[!UICONTROL Créer une action]** marketing dans le coin supérieur droit de l’onglet Actions **** marketing de l’espace de travail *[!UICONTROL Stratégies]* .

![](../images/policies/create-marketing-action.png)

La boîte de dialogue *[!UICONTROL Créer une action]* marketing s’affiche. Saisissez un nom et une description pour l’action marketing, puis cliquez sur **[!UICONTROL Créer]**.

![](../images/policies/create-marketing-action-details.png)

L’action nouvellement créée s’affiche dans l’onglet Actions ** marketing. Vous pouvez désormais utiliser l’action marketing lors de la [création de nouvelles stratégies](#create-policy)d’utilisation des données.

![](../images/policies/created-marketing-action.png)

## Modification ou suppression d’une action marketing {#edit-delete-marketing-action}

>[!NOTE] Seules les actions marketing personnalisées définies par votre organisation peuvent être modifiées. Les actions marketing définies par Adobe ne peuvent pas être modifiées ni supprimées.

Dans l’espace de travail **[!UICONTROL Stratégies]** , sélectionnez l’onglet Actions **** marketing pour vue d’une liste d’actions marketing disponibles définies par Adobe et votre propre organisation. Sélectionnez une action marketing personnalisée dans la liste, puis utilisez les champs fournis dans la section de droite pour modifier les détails de l’action marketing.

![](../images/policies/edit-marketing-action.png)

Si l’action marketing n’est utilisée par aucune stratégie d’utilisation existante, vous pouvez la supprimer en cliquant sur **[!UICONTROL Supprimer l’action]** marketing.

>[!NOTE] Si vous tentez de supprimer une action marketing utilisée par une stratégie existante, un message d’erreur s’affiche, indiquant que la tentative de suppression a échoué.

![](../images/policies/delete-marketing-action.png)

## Étapes suivantes

Ce document fournit un aperçu de la gestion des stratégies d’utilisation des données dans l’interface utilisateur Experience Platform. Pour savoir comment gérer les stratégies à l’aide de l’API DULE Policy, consultez le guide [du](../api/getting-started.md)développeur. Pour plus d’informations sur la manière d’appliquer des stratégies d’utilisation des données, voir l’aperçu [de l’application des](../enforcement/overview.md)stratégies.

La vidéo suivante montre comment utiliser les stratégies d’utilisation dans l’interface utilisateur de l’Experience Platform :

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)