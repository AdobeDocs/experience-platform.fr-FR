---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de l’utilisateur des stratégies d’utilisation des données
topic: policies
translation-type: tm+mt
source-git-commit: 235a43ad72dee45db1b3d35ae84ce9a1c4d729b8
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 2%

---


# Guide de l’utilisateur des stratégies d’utilisation des données

La gouvernance des données d’Adobe Experience Platform fournit une interface utilisateur qui vous permet de créer et de gérer des stratégies d’utilisation des données. Ce document présente un aperçu des actions que vous pouvez effectuer dans l’espace de travail _Stratégies_ de l’interface utilisateur de la plateforme d’expérience.

## Conditions préalables

Ce guide nécessite une bonne compréhension des concepts suivants de la plate-forme d’expérience :

- [Gouvernance des données](../home.md)
- [Stratégies d’utilisation des données](./overview.md)

## Stratégies d’utilisation des données de Vue

Dans l’interface utilisateur de la plateforme d’expérience, cliquez sur **[!UICONTROL Stratégies]** pour ouvrir l’espace de travail *[!UICONTROL Stratégies]* . Dans l’onglet **[!UICONTROL Parcourir]** , vous pouvez voir une liste des stratégies disponibles, y compris leurs étiquettes associées, leurs actions marketing et leur état.

![](../images/policies/browse-policies.png)

Cliquez sur une stratégie répertoriée pour en vue la description et le type. Si une stratégie personnalisée est sélectionnée, d’autres contrôles s’affichent pour modifier, supprimer ou [activer/désactiver la stratégie](#enable).

![](../images/policies/policy-details.png)

## Création d’une stratégie d’utilisation des données personnalisée

Pour créer une stratégie d’utilisation des données personnalisée, cliquez sur **[!UICONTROL Créer une stratégie]** dans le coin supérieur droit de l’espace de travail *Stratégies* .

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

Vous pouvez activer ou désactiver les stratégies d’utilisation des données personnalisées dans l’onglet *[!UICONTROL Parcourir]* de l’espace de travail *[!UICONTROL Stratégies]* . Sélectionnez une stratégie personnalisée dans la liste pour afficher ses détails à droite. Sous *[!UICONTROL Etat]*, sélectionnez le bouton bascule pour activer ou désactiver la stratégie.

![](../images/policies/enable-policy.png)

## Étapes suivantes

Ce document fournit un aperçu de la gestion des stratégies d’utilisation des données dans l’interface utilisateur de la plateforme d’expérience. Pour savoir comment gérer les stratégies à l’aide de l’API DULE Policy, consultez le guide [du](../api/getting-started.md)développeur. Pour plus d’informations sur la manière d’appliquer des stratégies d’utilisation des données, voir l’aperçu [de l’application des](../enforcement/overview.md)stratégies.