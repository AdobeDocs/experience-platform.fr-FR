---
title: Gestion des étiquettes d’utilisation des données pour un schéma
description: Découvrez comment ajouter des libellés d’utilisation des données aux champs de schéma du modèle de données d’expérience (XDM) dans l’interface utilisateur de Adobe Experience Platform.
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: 6fe11b909369797e96d8fa52542ebd5761a27b03
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 10%

---

# Gérer les libellés d’utilisation des données pour un schéma

>[!IMPORTANT]
>
>L’étiquetage basé sur les schémas fait partie de [contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md), actuellement disponible dans une version limitée pour les clients de santé basés aux États-Unis. Cette fonctionnalité sera disponible pour tous les clients Adobe Real-time Customer Data Platform une fois qu’elle sera entièrement publiée.

Toutes les données introduites dans Adobe Experience Platform sont contraintes par les schémas du modèle de données d’expérience (XDM). Ces données peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques. Pour en tenir compte, la plateforme vous permet de restreindre l’utilisation de certains jeux de données et champs par l’utilisation de [libellés d’utilisation des données](../../data-governance/labels/overview.md).

Un libellé appliqué à un champ de schéma indique les stratégies d’utilisation qui s’appliquent aux données contenues dans ce champ spécifique.

Les libellés peuvent être appliqués à des schémas individuels, ainsi qu’aux champs de ces schémas. Lorsque des libellés sont appliqués directement à un schéma, ces libellés sont propagés à tous les jeux de données existants et futurs basés sur ce schéma.

En outre, tout libellé de champ que vous ajoutez dans un schéma se propage à tous les autres schémas qui utilisent le même champ d’une classe partagée ou d’un groupe de champs. Cela permet de s’assurer que les règles d’utilisation des champs similaires sont cohérentes dans l’ensemble de votre modèle de données.

Ce tutoriel décrit les étapes à suivre pour ajouter des libellés à un schéma à l’aide de l’éditeur de schémas dans l’interface utilisateur de Platform.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM) System]](../home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
   * [Éditeur de schéma](../ui/overview.md): découvrez comment créer et gérer des schémas et d’autres ressources dans l’interface utilisateur de Platform.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): fournit l’infrastructure permettant d’appliquer des restrictions d’utilisation des données aux opérations de Platform à l’aide de stratégies qui définissent les actions marketing pouvant (ou non) être effectuées sur des données étiquetées.

## Sélectionner un schéma ou un champ auquel ajouter des libellés {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="Modifier les libellés de gouvernance"
>abstract="Appliquez un libellé à un champ de schéma pour indiquer les stratégies d&#39;utilisation qui s&#39;appliquent aux données contenues dans ce champ."

Pour commencer à ajouter des libellés, vous devez d’abord [sélectionner un schéma existant à modifier ;](../ui/resources/schemas.md#edit) ou [créer un nouveau schéma ;](../ui/resources/schemas.md#create) pour afficher sa structure dans l’éditeur de schémas.

Pour modifier les libellés d’un champ, vous pouvez sélectionner le champ dans la zone de travail, puis sélectionner **[!UICONTROL Gérer l’accès]** dans le rail de droite.

>[!IMPORTANT]
>
>300 libellés au maximum peuvent être appliqués à n’importe quel schéma.

![Sélectionnez un champ dans le canevas de l’éditeur de schémas](../images/tutorials/labels/manage-access.png)

Vous pouvez également sélectionner la variable **[!UICONTROL Étiquettes]** , sélectionnez le champ de votre choix dans la liste, puis sélectionnez **[!UICONTROL Appliquer les étiquettes d’accès et de gouvernance des données]** dans le rail de droite.

![Sélectionnez un champ dans le [!UICONTROL Étiquettes] tab](../images/tutorials/labels/select-field-on-labels-tab.png)

Pour modifier les libellés de l’ensemble du schéma, dans le **[!UICONTROL Étiquettes]** , cochez la case située sous l’icône de filtre. Cela sélectionne tous les champs disponibles dans le schéma. Ensuite, sélectionnez **[!UICONTROL Appliquer les étiquettes d’accès et de gouvernance des données]** dans le rail de droite.

![Sélectionnez le nom du schéma dans la [!UICONTROL Étiquettes] tab](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>Un message d’avertissement s’affiche lorsque vous tentez pour la première fois de modifier les libellés d’un schéma ou d’un champ, expliquant comment l’utilisation des libellés affecte les opérations en aval en fonction des stratégies de votre entreprise. Sélectionner **[!UICONTROL Continuer]** pour continuer la modification.
>
>![Avertissement sur l’utilisation des libellés](../images/tutorials/labels/disclaimer.png)

## Modification des libellés du schéma ou du champ {#edit-labels}

Une boîte de dialogue s’affiche, vous permettant de modifier les libellés du champ sélectionné. Si vous avez sélectionné un champ de type objet individuel, le rail de droite répertorie les sous-champs vers lesquels les libellés appliqués seront propagés.

![La boîte de dialogue Appliquer les étiquettes d’accès et de gouvernance des données avec les champs sélectionnés mis en surbrillance.](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>Si vous modifiez des champs pour l’ensemble du schéma, le rail de droite ne répertorie pas les champs applicables et affiche le nom du schéma à la place.

Utilisez la liste affichée pour sélectionner les libellés à ajouter au schéma ou au champ. À mesure que les libellés sont sélectionnés, la variable **[!UICONTROL Libellés appliqués]** mises à jour de section pour afficher les libellés qui ont été sélectionnés jusqu’à présent.

![La boîte de dialogue Appliquer les étiquettes d’accès et de gouvernance des données avec les étiquettes appliquées surlignées.](../images/tutorials/labels/applied-labels.png)

Pour filtrer les libellés affichés par type, sélectionnez la catégorie de votre choix dans le rail de gauche. Pour créer une étiquette personnalisée, sélectionnez **[!UICONTROL Créer une étiquette]**.

![La boîte de dialogue Appliquer les étiquettes d’accès et de gouvernance des données avec un filtre de type de libellé appliqué et Créer le libellé mis en surbrillance.](../images/tutorials/labels/filter-and-create-custom.png)

Une fois que vous êtes satisfait des libellés que vous choisissez, sélectionnez **[!UICONTROL Enregistrer]** pour les appliquer au champ ou au schéma.

![La boîte de dialogue Appliquer les étiquettes d’accès et de gouvernance des données avec l’option Enregistrer mise en surbrillance.](../images/tutorials/labels/save-labels.png)

La variable **[!UICONTROL Étiquettes]** réapparaît, affichant les libellés appliqués pour le schéma.

![Onglet Libellés de l’espace de travail des schémas avec les libellés de champ appliqués mis en surbrillance.](../images/tutorials/labels/field-labels-added.png)

## Étapes suivantes

Ce guide explique comment gérer les libellés d’utilisation des données pour les schémas et les champs. Pour plus d’informations sur la gestion des libellés d’utilisation des données, y compris sur la manière de les ajouter à des jeux de données spécifiques plutôt qu’au niveau du schéma, voir la section [Guide d’utilisation des libellés d’utilisation des données](../../data-governance/labels/user-guide.md).
