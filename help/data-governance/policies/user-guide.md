---
keywords: Experience Platform;accueil;rubriques populaires;gouvernance des données;guide d’utilisation des stratégies d’utilisation des données
solution: Experience Platform
title: Gestion des politiques d’utilisation des données dans l’interface utilisateur
description: La gouvernance des données d’Adobe Experience Platform fournit une interface utilisateur qui vous permet de créer et de gérer des politiques d’utilisation des données. Ce document offre une vue d’ensemble des actions que vous pouvez effectuer dans l’espace de travail Stratégies de l’interface utilisateur d’Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: e539b1e165227d9a888bfe12d8205e285b3ce259
workflow-type: ht
source-wordcount: '1413'
ht-degree: 100%

---

# Gestion des politiques d’utilisation des données dans l’interface utilisateur {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_description"
>title="Description"
>abstract=""

Ce document explique comment utiliser l’espace de travail **[!UICONTROL Stratégies]** dans l’interface utilisateur d’Adobe Experience Platform pour créer et gérer des stratégies d’utilisation des données.

>[!NOTE]
>
>Pour plus d’informations sur la gestion des stratégies de contrôle d’accès dans l’interface utilisateur, reportez-vous au [guide de l’interface utilisateur du contrôle d’accès basé sur les attributs](../../access-control/abac/ui/policies.md).

>[!IMPORTANT]
>
>Toutes les stratégies d’utilisation des données (y compris les stratégies de base fournies par Adobe) sont désactivées par défaut. Pour qu’une stratégie individuelle soit prise en compte pour l’application, vous devez l’activer manuellement. Consultez la section relative à l’[activation des stratégies](#enable) pour savoir comment procéder dans l’interface utilisateur.

## Conditions préalables

Ce guide nécessite une bonne compréhension des concepts [!DNL Experience Platform] suivants :

* [Gouvernance des données](../home.md)
* [Stratégies d’utilisation des données](./overview.md)

## Affichage des stratégies existantes {#view-policies}

Dans l’interface utilisateur [!DNL Experience Platform], cliquez sur **[!UICONTROL Stratégies]** pour ouvrir l’espace de travail **[!UICONTROL Stratégies]**. Dans l’onglet **[!UICONTROL Parcourir]**, vous pouvez voir une liste des stratégies disponibles, y compris leurs libellés associés, les actions marketing et les états.

![](../images/policies/browse-policies.png)

Si vous avez accès aux stratégies de consentement, activez le bouton (bascule) **[!UICONTROL Stratégies de consentement]** pour les afficher dans l’onglet [!UICONTROL Parcourir].

![](../images/policies/consent-policy-toggle.png)

Cliquez sur une stratégie répertoriée pour en afficher la description et le type. Si une stratégie personnalisée est sélectionnée, d’autres contrôles s’affichent pour la modifier, la supprimer ou [activer/désactiver la stratégie](#enable).

![](../images/policies/policy-details.png)

## Création dʼune stratégie personnalisée {#create-policy}

Pour créer une politique d’utilisation des données personnalisée, cliquez sur **[!UICONTROL Créer une politique]** dans le coin supérieur droit de l’onglet **[!UICONTROL Parcourir]** dans l’espace de travail **[!UICONTROL Politiques]**.

![](../images/policies/create-policy-button.png)

Selon que vous fassiez partie de la version bêta des stratégies de consentement, l’un des événements suivants se produit :

* Si vous ne faites pas partie de la version bêta, vous êtes immédiatement redirigé(e) vers le workflow pour [créer une stratégie de gouvernance des données](#create-governance-policy).
* Si vous faites partie de la version bêta, une boîte de dialogue vous offre une option supplémentaire pour [créer une stratégie de consentement](#consent-policy).
   ![](../images/policies/choose-policy-type.png)

### Créer une stratégie de gouvernance des données {#create-governance-policy}

Le workflow de **[!UICONTROL création de stratégies]** s’affiche. Commencez par fournir un nom et une description à la nouvelle stratégie.

![](../images/policies/create-policy-description.png)

Ensuite, sélectionnez les libellés d’utilisation des données sur lesquels la stratégie sera basée. Lors de la sélection de plusieurs libellés, vous avez la possibilité de choisir si les données doivent contenir tous les libellés ou un seul pour que la stratégie s’applique. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Suivant]**.

![](../images/policies/add-labels.png)

L’étape **[!UICONTROL Sélectionner les actions marketing]** s’affiche. Sélectionnez les actions marketing appropriées dans la liste fournie, puis cliquez sur **[!UICONTROL Suivant]** pour continuer.

>[!NOTE]
>
>Lors de la sélection de plusieurs actions marketing, la stratégie les interprète comme une règle « OU ». En d’autres termes, la stratégie s’applique si **l’une** des actions marketing sélectionnées est exécutée.

![](../images/policies/add-marketing-actions.png)

L’étape **[!UICONTROL Révision]** s’affiche, vous permettant de consulter les détails de la nouvelle stratégie avant de la créer. Une fois que vous êtes satisfait, cliquez sur **[!UICONTROL Terminer]** pour créer la stratégie.

![](../images/policies/policy-review.png)

L’onglet **[!UICONTROL Parcourir]** réapparaît et affiche désormais la nouvelle stratégie avec l’état « Version préliminaire ». Pour activer la stratégie, consultez la section suivante.

![](../images/policies/created-policy.png)

### Créer une stratégie de consentement {#consent-policy}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_instructions"
>title="Instructions"
>abstract=""

>[!IMPORTANT]
>
>Les stratégies de consentement ne sont disponibles que pour les organisations qui ont acheté **Adobe Healthcare Shield** ou **Adobe Privacy &amp; Security Shield**.

Si vous choisissez de créer une stratégie de consentement, un nouvel écran vous permettant de configurer la nouvelle stratégie s’affiche.

![](../images/policies/consent-policy-dialog.png)

Pour pouvoir utiliser des stratégies de consentement, des attributs de consentement doivent être présents dans vos données de profil. Consultez le guide sur le [traitement du consentement dans Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md) pour obtenir des instructions détaillées sur la manière d’inclure les attributs obligatoires dans votre schéma d’union.

Les stratégies de consentement se composent de deux éléments logiques :

* **[!UICONTROL Si]** : la condition qui déclenchera la vérification de la stratégie. Elle peut dépendre d’une certaine action marketing en cours, de la présence de certains libellés d’utilisation des données ou d’une combinaison des deux.
* **[!UICONTROL Alors]** : attributs de consentement devant être présents pour qu’un profil soit inclus dans l’action qui a déclenché la stratégie.

#### Configurer les conditions {#consent-conditions}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentif"
>title="Condition Si"
>abstract="Définissez d’abord les conditions qui déclencheront la vérification de la stratégie. Les conditions peuvent inclure certaines actions marketing entreprises, certaines étiquettes de gouvernance des données présentes ou une combinaison des deux."

Sous la section **[!UICONTROL Si]**, sélectionnez les actions marketing et/ou les libellés d’utilisation des données qui doivent déclencher cette stratégie. Sélectionnez **[!UICONTROL Afficher tout]** et **[!UICONTROL Sélectionner des libellés]** pour afficher les listes complètes des actions marketing et des libellés disponibles, respectivement.

Une fois que vous avez ajouté au moins une condition, vous pouvez sélectionner **[!UICONTROL Ajouter une condition]** pour continuer à ajouter d’autres conditions si nécessaire, en choisissant le type de condition approprié dans la liste déroulante.

![](../images/policies/add-condition.png)

Si vous sélectionnez plusieurs conditions, vous pouvez utiliser l’icône qui s’affiche entre elles pour changer la relation conditionnelle entre « ET » et « OU ».

![](../images/policies/and-or-selection.png)

#### Sélectionner les attributs de consentement {#consent-attributes}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentthen"
>title="Condition Alors"
>abstract="Une fois votre condition « Si » définie, utilisez la section « Alors » pour sélectionner au moins un attribut de consentement dans le schéma d’union. Il s’agit de l’attribut qui doit être présent pour que les profils soient inclus dans l’action régie par cette stratégie."

Sous la section **[!UICONTROL Alors]**, sélectionnez au moins un attribut de consentement dans le schéma d’union. Il s’agit de l’attribut qui doit être présent pour que les profils soient inclus dans l’action régie par cette stratégie. Vous pouvez choisir l’une des options fournies dans la liste ou sélectionner **[!UICONTROL Afficher tout]** pour sélectionner directement l’attribut dans le schéma d’union.

Lors de la sélection de l’attribut de consentement, sélectionnez les valeurs de l’attribut que vous souhaitez que cette stratégie vérifie.

![](../images/policies/select-schema-field.png)

Après avoir sélectionné au moins un attribut de consentement, le panneau **[!UICONTROL Propriétés de la stratégie]** se met à jour pour afficher le nombre estimé de profils qui seraient autorisés par cette stratégie, y compris le pourcentage du total de la boutique de profils. Cette estimation est automatiquement mise à jour lorsque vous ajustez la configuration de la stratégie.

![](../images/policies/audience-preview.png)

Pour ajouter d’autres attributs de consentement à la stratégie, sélectionnez **[!UICONTROL Ajouter un résultat]**.

![](../images/policies/add-result.png)

Vous pouvez continuer à ajouter et à ajuster des conditions et des attributs de consentement à la stratégie, si nécessaire. Lorsque vous êtes satisfait(e) de la configuration, indiquez un nom et une description facultative pour la stratégie avant de sélectionner **[!UICONTROL Enregistrer]**.

![](../images/policies/name-and-save.png)

La stratégie de consentement est maintenant créée et son état est défini sur [!UICONTROL Désactivé] par défaut. Pour activer immédiatement la stratégie, activez le bouton **[!UICONTROL Statut]** dans le rail de droite.

![](../images/policies/enable-consent-policy.png)

#### Vérifier l’application des stratégies

Après avoir créé et activé une stratégie de consentement, vous pouvez prévisualiser l’impact de cette règle sur vos audiences consentantes lors de l’activation de segments vers les destinations. Voir la section sur l’[évaluation des stratégies de consentement](../enforcement/auto-enforcement.md#consent-policy-evaluation) pour plus d’informations.

## Activation ou désactivation d’une stratégie {#enable}

Toutes les stratégies d’utilisation des données (y compris les stratégies de base fournies par Adobe) sont désactivées par défaut. Pour qu’une stratégie individuelle soit prise en compte pour son application, vous devez l’activer manuellement par le biais de l’API ou de l’interface utilisateur.

Vous pouvez activer ou désactiver les stratégies à partir de l’onglet **[!UICONTROL Parcourir]** dans l’espace de travail **[!UICONTROL Stratégies]**. Sélectionnez une stratégie personnalisée dans la liste pour afficher ses détails à droite. Sous **[!UICONTROL État]**, sélectionnez le bouton d’activation/désactivation pour activer ou désactiver la stratégie.

![](../images/policies/enable-policy.png)

## Affichage des actions marketing {#view-marketing-actions}

Dans l’espace de travail **[!UICONTROL Stratégies]**, cliquez sur l’onglet **[!UICONTROL Actions marketing]** pour afficher une liste d’actions marketing mises à votre disposition et définies par Adobe et votre organisation.

![](../images/policies/marketing-actions.png)

## Création d’une action marketing {#create-marketing-action}

Pour créer une action marketing personnalisée, sélectionnez **[!UICONTROL Créer une action marketing]** dans le coin supérieur droit de l’onglet **[!UICONTROL Actions marketing]** dans l’espace de travail **[!UICONTROL Stratégies]**.

![](../images/policies/create-marketing-action.png)

La boîte de dialogue **[!UICONTROL Créer une action marketing]** apparaît. Saisissez un nom et une description pour l’action marketing, puis sélectionnez **[!UICONTROL Créer]**.

![](../images/policies/create-marketing-action-details.png)

L’action nouvellement créée s’affiche dans l’onglet **[!UICONTROL Actions marketing]**. Vous pouvez désormais utiliser l’action marketing lors de la [création de stratégies d’utilisation des données](#create-policy).

![](../images/policies/created-marketing-action.png)

## Modification ou suppression d’une action marketing {#edit-delete-marketing-action}

>[!NOTE]
>
>Seules les actions marketing personnalisées définies par votre organisation peuvent être modifiées. Il n’est pas possible de modifier ou supprimer des actions marketing définies par Adobe.

Dans l’espace de travail **[!UICONTROL Stratégies]**, cliquez sur l’onglet **[!UICONTROL Actions marketing]** pour afficher une liste d’actions marketing mises à votre disposition et définies par Adobe et votre organisation. Sélectionnez une action marketing personnalisée répertoriée dans la liste, puis utilisez les champs fournis dans la section de droite pour modifier les détails de cette action.

![](../images/policies/edit-marketing-action.png)

Si l’action marketing n’est utilisée par aucune stratégie d’utilisation existante, vous pouvez la supprimer en cliquant sur **[!UICONTROL Supprimer l’action marketing]**.

>[!NOTE]
>
>Si vous tentez de supprimer une action marketing utilisée par une stratégie existante, un message d’erreur s’affiche, indiquant que la tentative de suppression a échoué.

![](../images/policies/delete-marketing-action.png)

## Étapes suivantes

Ce document offre un aperçu de la gestion des stratégies d’utilisation des données dans l’interface utilisateur [!DNL Experience Platform]. Pour savoir comment gérer les stratégies à l’aide de l’[!DNL Policy Service API], consultez le [guide du développement](../api/getting-started.md). Pour plus d’informations sur l’application des stratégies d’utilisation des données, voir la [présentation de l’application des politiques](../enforcement/overview.md).

La vidéo qui suit montre comment utiliser les stratégies d’utilisation dans l’interface utilisateur [!DNL Experience Platform] :

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
