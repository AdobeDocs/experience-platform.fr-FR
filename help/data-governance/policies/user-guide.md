---
keywords: Experience Platform;home;popular topics;data governance;data usage policy user guide
solution: Experience Platform
title: Guide d’utilisation des stratégies de données
topic: policies
description: La gouvernance des données d’Adobe Experience Platform fournit une interface utilisateur qui vous permet de créer et de gérer des stratégies d’utilisation des données. Ce document présente un aperçu des actions que vous pouvez effectuer dans l’espace de travail Stratégies de l’interface utilisateur de l’Experience Platform.
translation-type: tm+mt
source-git-commit: 0f3a4ba6ad96d2226ae5094fa8b5073152df90f7
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 39%

---


# Guide d’utilisation des stratégies de données

Adobe Experience Platform [!DNL Data Governance] provides a user interface that allows you to create and manage data usage policies. This document provides an overview of the actions you can perform in the _Policies_ workspace in the [!DNL Experience Platform] user interface.

>[!IMPORTANT]
>
>Toutes les stratégies d’utilisation des données (y compris les stratégies de base fournies par l’Adobe) sont désactivées par défaut. Pour qu’une stratégie individuelle soit prise en compte pour l’application de la loi, vous devez l’activer manuellement. Consultez la section relative à l’ [activation des stratégies](#enable) pour savoir comment procéder dans l’interface utilisateur.

## Conditions préalables 

This guide requires a working understanding of the following [!DNL Experience Platform] concepts:

- [[ ! Gouvernance des données DNL]](../home.md)
- [Stratégies d’utilisation des données](./overview.md)

## Affichage des stratégies d’utilisation des données {#view-policies}

In the [!DNL Experience Platform] UI, click **[!UICONTROL Policies]** to open the **[!UICONTROL Policies]** workspace. Dans l’onglet **[!UICONTROL Parcourir]**, vous pouvez voir une liste des stratégies disponibles, y compris leurs libellés associés, les actions marketing et les états.

![](../images/policies/browse-policies.png)

Cliquez sur une stratégie répertoriée pour afficher sa description et son type. Si une stratégie personnalisée est sélectionnée, d’autres contrôles s’affichent pour la modifier, la supprimer ou [activer/désactiver la stratégie](#enable).

![](../images/policies/policy-details.png)

## Création d’une stratégie d’utilisation des données personnalisée {#create-policy}

To create a new custom data usage policy, click **[!UICONTROL Create policy]** in the top-right corner of the **[!UICONTROL Browse]** tab in the **[!UICONTROL Policies]** workspace.

![](../images/policies/create-policy-button.png)

Le workflow de **[!UICONTROL création de stratégies]** s’affiche. Commencez par fournir un nom et une description à la nouvelle stratégie.

![](../images/policies/create-policy-description.png)

Ensuite, sélectionnez les libellés d’utilisation des données sur lesquels la stratégie sera basée. Lors de la sélection de plusieurs libellés, vous avez la possibilité de choisir si les données doivent contenir tous les libellés ou un seul pour que la stratégie s’applique. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Suivant]**.

![](../images/policies/add-labels.png)

L’étape **[!UICONTROL Sélectionner les actions marketing]** s’affiche. Sélectionnez les actions marketing appropriées dans la liste fournie, puis cliquez sur **[!UICONTROL Suivant]** pour continuer.

>[!NOTE]
>
> Lors de la sélection de plusieurs actions marketing, la stratégie les interprète comme une règle « OU ». En d’autres termes, la stratégie s’applique si _l’une_ des actions marketing sélectionnées est exécutée.

![](../images/policies/add-marketing-actions.png)

L’étape **[!UICONTROL Révision]** s’affiche, vous permettant de consulter les détails de la nouvelle stratégie avant de la créer. Une fois que vous êtes satisfait, cliquez sur **[!UICONTROL Terminer]** pour créer la stratégie.

![](../images/policies/policy-review.png)

L’onglet **[!UICONTROL Parcourir]** réapparaît et affiche désormais la nouvelle stratégie avec l’état « Version préliminaire ». Pour activer la stratégie, consultez la section suivante.

![](../images/policies/created-policy.png)

## Activation ou désactivation d’une stratégie d’utilisation des données {#enable}

Toutes les stratégies d’utilisation des données (y compris les stratégies de base fournies par l’Adobe) sont désactivées par défaut. Pour qu’une stratégie individuelle soit prise en compte pour l’application, vous devez l’activer manuellement par le biais de l’API ou de l’interface utilisateur.

You can enable or disable policies from the **[!UICONTROL Browse]** tab in the **[!UICONTROL Policies]** workspace. Sélectionnez une stratégie personnalisée dans la liste pour afficher ses détails à droite. Sous **[!UICONTROL État]**, sélectionnez le bouton d’activation/désactivation pour activer ou désactiver la stratégie.

![](../images/policies/enable-policy.png)

## Actions marketing vue {#view-marketing-actions}

Dans l’espace de travail **[!UICONTROL Stratégies]** , sélectionnez l’onglet Actions **** marketing pour vue d’une liste d’actions marketing disponibles définies par l’Adobe et votre propre organisation.

![](../images/policies/marketing-actions.png)

## Create a marketing action {#create-marketing-action}

Pour créer une action marketing personnalisée, cliquez sur **[!UICONTROL Créer une action]** marketing dans le coin supérieur droit de l’onglet Actions **** marketing de l’espace de travail **[!UICONTROL Stratégies]** .

![](../images/policies/create-marketing-action.png)

La boîte de dialogue **[!UICONTROL Créer une action]** marketing s’affiche. Saisissez un nom et une description pour l’action marketing, puis cliquez sur **[!UICONTROL Créer]**.

![](../images/policies/create-marketing-action-details.png)

L’action nouvellement créée s’affiche dans l’onglet Actions **** marketing. Vous pouvez désormais utiliser l’action marketing lors de la [création de nouvelles stratégies](#create-policy)d’utilisation des données.

![](../images/policies/created-marketing-action.png)

## Modification ou suppression d’une action marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Seules les actions marketing personnalisées définies par votre organisation peuvent être modifiées. Les actions marketing définies par l&#39;Adobe ne peuvent pas être modifiées ou supprimées.

Dans l’espace de travail **[!UICONTROL Stratégies]** , sélectionnez l’onglet Actions **** marketing pour vue d’une liste d’actions marketing disponibles définies par l’Adobe et votre propre organisation. Sélectionnez une action marketing personnalisée dans la liste, puis utilisez les champs fournis dans la section de droite pour modifier les détails de l’action marketing.

![](../images/policies/edit-marketing-action.png)

Si l’action marketing n’est utilisée par aucune stratégie d’utilisation existante, vous pouvez la supprimer en cliquant sur **[!UICONTROL Supprimer l’action]** marketing.

>[!NOTE]
>
>Si vous tentez de supprimer une action marketing utilisée par une stratégie existante, un message d’erreur s’affiche, indiquant que la tentative de suppression a échoué.

![](../images/policies/delete-marketing-action.png)

## Étapes suivantes

This document provided an overview of how to manage data usage policies in [!DNL Experience Platform] UI. Pour connaître les étapes de gestion des stratégies à l’aide de la section [!DNL Policy Service API], consultez le guide [du](../api/getting-started.md)développeur. Pour plus d’informations sur l’application des stratégies d’utilisation des données, voir la [présentation de l’application des stratégies](../enforcement/overview.md).

La vidéo suivante montre comment utiliser les stratégies d’utilisation dans l’ [!DNL Experience Platform] interface utilisateur :

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)