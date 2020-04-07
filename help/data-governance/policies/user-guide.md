---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de l’utilisateur des stratégies d’utilisation des données
topic: policies
translation-type: tm+mt
source-git-commit: 304a84b81758b2f2a343977533f9120857a1fb33

---


# Guide de l’utilisateur des stratégies d’utilisation des données

La gouvernance des données d’Adobe Experience Platform fournit une interface utilisateur qui vous permet de créer et de gérer des stratégies d’utilisation des données. Ce présente les actions que vous pouvez effectuer dans l’espace de travail _Stratégies_ de l’interface utilisateur de la plateforme d’expérience.

## Conditions préalables

Ce guide nécessite une compréhension pratique des concepts de la plateforme d’expérience suivants :

- [Gouvernance des données](../home.md)
- [Stratégies d’utilisation des données](./overview.md)

## Stratégies d’utilisation des données 

Dans l’interface utilisateur de la plate-forme d’expérience, cliquez **[!UICONTROL Policies]** pour ouvrir l’ *[!UICONTROL Policies]* espace de travail. Dans l’ **[!UICONTROL Browse]** onglet, vous pouvez voir un des stratégies disponibles, y compris leurs étiquettes associées, les actions marketing et l’état.

![](../images/policies/browse-policies.png)

Cliquez sur une stratégie répertoriée pour  sa description et son type. Si une stratégie personnalisée est sélectionnée, d’autres contrôles s’affichent pour la modifier, la supprimer ou [activer/désactiver la stratégie](#enable).

![](../images/policies/policy-details.png)

## Création d’une stratégie d’utilisation des données personnalisée

Pour créer une stratégie d’utilisation des données personnalisée, cliquez **[!UICONTROL Create policy]** dans le coin supérieur droit de l’espace de travail *Stratégies* .

![](../images/policies/create-policy-button.png)

Le *[!UICONTROL Create policy]* processus s’affiche.  en fournissant un nom et une description pour la nouvelle stratégie.

![](../images/policies/create-policy-description.png)

Ensuite, sélectionnez les étiquettes d’utilisation des données sur lesquelles la stratégie sera basée. Lors de la sélection de plusieurs étiquettes, vous avez la possibilité de choisir si les données doivent contenir toutes les étiquettes ou une seule pour que la stratégie s’applique. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Next]**.

![](../images/policies/add-labels.png)

L’ *[!UICONTROL Select marketing actions]* étape s’affiche. Sélectionnez les actions marketing appropriées dans le  fourni, puis cliquez sur **[!UICONTROL Next]** pour continuer.

>[!NOTE] Lors de la sélection de plusieurs actions marketing, la stratégie les interprète comme une règle &quot;OU&quot;. En d’autres termes, la stratégie s’applique si _l’une_ des actions marketing sélectionnées est exécutée.

![](../images/policies/add-marketing-actions.png)

L’ *[!UICONTROL Review]* étape s’affiche, vous permettant de consulter les détails de la nouvelle stratégie avant de la créer. Une fois que vous êtes satisfait, cliquez sur **[!UICONTROL Finish]** pour créer la stratégie.

![](../images/policies/policy-review.png)

L’ *[!UICONTROL Browse]* onglet s’affiche à nouveau, ce qui permet désormais de la nouvelle stratégie dans l’état &quot;Version préliminaire&quot;. Pour activer la stratégie, consultez la section suivante.

![](../images/policies/created-policy.png)

## Activation ou désactivation d’une stratégie d’utilisation des données {#enable}

Vous pouvez activer ou désactiver les stratégies d’utilisation des données personnalisées dans l’ *[!UICONTROL Browse]* onglet de l’ *[!UICONTROL Policies]* espace de travail. Sélectionnez une stratégie personnalisée dans le  pour afficher ses détails à droite. Sous *[!UICONTROL Status]*, sélectionnez le bouton bascule pour activer ou désactiver la stratégie.

![](../images/policies/enable-policy.png)

## Étapes suivantes

Ce  un aperçu de la gestion des stratégies d’utilisation des données dans l’interface utilisateur de la plateforme d’expérience. Pour savoir comment gérer les stratégies à l’aide de l’API de stratégie DULE, consultez le didacticiel [sur la création de stratégies d’](./create.md)API. Pour plus d’informations sur l’application des stratégies d’utilisation des données, voir la présentation [de l’application des](../enforcement/overview.md)stratégies.