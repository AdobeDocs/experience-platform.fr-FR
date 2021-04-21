---
keywords: Experience Platform ; accueil ; rubriques populaires ; gouvernance des données ; guide de l’utilisateur de la stratégie d’utilisation des données
solution: Experience Platform
title: Gérer les stratégies d’utilisation des données dans l’interface utilisateur
topic-legacy: policies
description: La gouvernance des données d’Adobe Experience Platform fournit une interface utilisateur qui vous permet de créer et de gérer des stratégies d’utilisation des données. Ce document présente un aperçu des actions que vous pouvez effectuer dans l’espace de travail Stratégies de l’interface utilisateur de l’Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 31%

---

# Gestion des stratégies d’utilisation des données dans l’interface utilisateur

Adobe Experience Platform [!DNL Data Governance] fournit une interface utilisateur qui vous permet de créer et de gérer des stratégies d’utilisation des données. Ce document présente un aperçu des actions que vous pouvez effectuer dans l&#39;espace de travail **Stratégies** de l&#39;interface utilisateur [!DNL Experience Platform].

>[!IMPORTANT]
>
>Toutes les stratégies d’utilisation des données (y compris les stratégies de base fournies par l’Adobe) sont désactivées par défaut. Pour qu’une stratégie individuelle soit prise en compte pour l’application de la loi, vous devez l’activer manuellement. Consultez la section [activation des stratégies](#enable) pour savoir comment procéder dans l’interface utilisateur.

## Conditions préalables

Ce guide nécessite une compréhension pratique des concepts [!DNL Experience Platform] suivants :

- [[!DNL Data Governance]](../home.md)
- [Stratégies d’utilisation des données](./overview.md)

## Vue des stratégies existantes {#view-policies}

Dans l&#39;interface utilisateur [!DNL Experience Platform], sélectionnez **[!UICONTROL Stratégies]** pour ouvrir l&#39;espace de travail **[!UICONTROL Stratégies]**. Dans l’onglet **[!UICONTROL Parcourir]**, vous pouvez voir une liste des stratégies disponibles, y compris leurs libellés associés, les actions marketing et les états.

![](../images/policies/browse-policies.png)

Sélectionnez une stratégie répertoriée pour en vue la description et le type. Si une stratégie personnalisée est sélectionnée, d’autres contrôles s’affichent pour la modifier, la supprimer ou [activer/désactiver la stratégie](#enable).

![](../images/policies/policy-details.png)

## Créer une stratégie personnalisée {#create-policy}

Pour créer une stratégie d&#39;utilisation des données personnalisée, sélectionnez **[!UICONTROL Créer une stratégie]** dans le coin supérieur droit de l&#39;onglet **[!UICONTROL Parcourir]** de l&#39;espace de travail **[!UICONTROL Stratégies]**.

![](../images/policies/create-policy-button.png)

Le workflow de **[!UICONTROL création de stratégies]** s’affiche. Commencez par fournir un nom et une description à la nouvelle stratégie.

![](../images/policies/create-policy-description.png)

Ensuite, sélectionnez les libellés d’utilisation des données sur lesquels la stratégie sera basée. Lors de la sélection de plusieurs libellés, vous avez la possibilité de choisir si les données doivent contenir tous les libellés ou un seul pour que la stratégie s’applique. Sélectionnez **[!UICONTROL Suivant]** une fois terminé.

![](../images/policies/add-labels.png)

L’étape **[!UICONTROL Sélectionner les actions marketing]** s’affiche. Choisissez les actions marketing appropriées dans la liste fournie, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

>[!NOTE]
>
> Lors de la sélection de plusieurs actions marketing, la stratégie les interprète comme une règle « OU ». En d’autres termes, la stratégie s’applique si **l’une** des actions marketing sélectionnées est exécutée.

![](../images/policies/add-marketing-actions.png)

L’étape **[!UICONTROL Révision]** s’affiche, vous permettant de consulter les détails de la nouvelle stratégie avant de la créer. Une fois que vous êtes satisfait, sélectionnez **[!UICONTROL Terminer]** pour créer la stratégie.

![](../images/policies/policy-review.png)

L’onglet **[!UICONTROL Parcourir]** réapparaît et affiche désormais la nouvelle stratégie avec l’état « Version préliminaire ». Pour activer la stratégie, consultez la section suivante.

![](../images/policies/created-policy.png)

## Activer ou désactiver une stratégie {#enable}

Toutes les stratégies d’utilisation des données (y compris les stratégies de base fournies par l’Adobe) sont désactivées par défaut. Pour qu’une stratégie individuelle soit prise en compte pour l’application, vous devez l’activer manuellement par le biais de l’API ou de l’interface utilisateur.

Vous pouvez activer ou désactiver des stratégies dans l&#39;onglet **[!UICONTROL Parcourir]** de l&#39;espace de travail **[!UICONTROL Stratégies]**. Sélectionnez une stratégie personnalisée dans la liste pour afficher ses détails à droite. Sous **[!UICONTROL État]**, sélectionnez le bouton d’activation/désactivation pour activer ou désactiver la stratégie.

![](../images/policies/enable-policy.png)

## Actions marketing de vue {#view-marketing-actions}

Dans l&#39;espace de travail **[!UICONTROL Stratégies]**, sélectionnez l&#39;onglet **[!UICONTROL Actions marketing]** pour vue une liste d&#39;actions marketing disponibles définies par l&#39;Adobe et votre propre organisation.

![](../images/policies/marketing-actions.png)

## Créer une action marketing {#create-marketing-action}

Pour créer une action marketing personnalisée, sélectionnez **[!UICONTROL Créer une action marketing]** dans le coin supérieur droit de l&#39;onglet **[!UICONTROL Actions marketing]** dans l&#39;espace de travail **[!UICONTROL Stratégies]**.

![](../images/policies/create-marketing-action.png)

La boîte de dialogue **[!UICONTROL Créer une action marketing]** s&#39;affiche. Saisissez un nom et une description pour l’action marketing, puis sélectionnez **[!UICONTROL Créer]**.

![](../images/policies/create-marketing-action-details.png)

L’action nouvellement créée s’affiche dans l’onglet **[!UICONTROL Actions marketing]**. Vous pouvez désormais utiliser l’action marketing lorsque [vous créez de nouvelles stratégies d’utilisation des données](#create-policy).

![](../images/policies/created-marketing-action.png)

## Modifier ou supprimer une action marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Seules les actions marketing personnalisées définies par votre organisation peuvent être modifiées. Les actions marketing définies par l&#39;Adobe ne peuvent pas être modifiées ou supprimées.

Dans l&#39;espace de travail **[!UICONTROL Stratégies]**, sélectionnez l&#39;onglet **[!UICONTROL Actions marketing]** pour vue une liste d&#39;actions marketing disponibles définies par l&#39;Adobe et votre propre organisation. Sélectionnez une action marketing personnalisée dans la liste, puis utilisez les champs fournis dans la section de droite pour modifier les détails de l’action marketing.

![](../images/policies/edit-marketing-action.png)

Si l&#39;action marketing n&#39;est utilisée par aucune stratégie d&#39;utilisation existante, vous pouvez la supprimer en sélectionnant **[!UICONTROL Supprimer l&#39;action marketing]**.

>[!NOTE]
>
>Si vous tentez de supprimer une action marketing utilisée par une stratégie existante, un message d’erreur s’affiche, indiquant que la tentative de suppression a échoué.

![](../images/policies/delete-marketing-action.png)

## Étapes suivantes

Ce document fournit une vue d&#39;ensemble de la gestion des stratégies d&#39;utilisation des données dans [!DNL Experience Platform] l&#39;interface utilisateur. Pour savoir comment gérer les stratégies à l&#39;aide de [!DNL Policy Service API], consultez le [guide du développeur](../api/getting-started.md). Pour plus d’informations sur l’application des stratégies d’utilisation des données, voir la [présentation de l’application des stratégies](../enforcement/overview.md).

La vidéo suivante montre comment utiliser les stratégies d&#39;utilisation dans l&#39;[!DNL Experience Platform] interface utilisateur :

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
