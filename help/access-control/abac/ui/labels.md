---
keywords: Experience Platform;accueil;rubriques populaires;contrôle d’accès;contrôle d’accès basé sur les attributs
title: Gestion des libellés de contrôle d’accès basé sur les attributs
description: Gérez les libellés via l’interface Autorisations dans Adobe Experience Cloud.
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: 855f0a1384f658d39aa9d4fbb6bcb032933e59db
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 13%

---

# Gérer les libellés

Vous pouvez utiliser des libellés pour classer les jeux de données et les champs en fonction de l’utilisation des données et des politiques de contrôle d’accès basées sur les attributs. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Les bonnes pratiques recommandent de libeller les données dès qu’elles sont ingérées dans Adobe Experience Platform, ou dès que les données sont disponibles pour utilisation. Lisez ce document pour savoir comment gérer les libellés dans l’interface utilisateur Autorisations.

Pour obtenir une liste complète des libellés et des politiques de gouvernance correspondantes, consultez le guide sur [les principaux libellés d’utilisation des données](../../../data-governance/labels/reference.md){target="_blank"}.

>[!NOTE]
>
>Pour créer ou afficher des [attributs calculés](../../../profile/computed-attributes/overview.md){target="_blank"} avec des champs contenant un libellé donné, vous devez avoir accès à ce libellé.

## Explorer les libellés {#explore-labels}

Pour afficher tous les libellés disponibles, accédez à **[!UICONTROL Permissions]** dans [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Sélectionnez **[!UICONTROL Labels]** dans le panneau de gauche.

![Espace de travail des libellés dans Autorisations avec les libellés mis en surbrillance dans le panneau de gauche.](../../images/ui/labels/labels-home.png){zoomable="yes"}

Les libellés sont classés par type et appartiennent à l’une des catégories suivantes :

| Type | Description |
| --- | --- |
| [&#x200B; Contrat &#x200B;](../../../data-governance/labels/reference.md#contract){target="_blank"} | Cette catégorie est utilisée pour classer les données contenant des obligations contractuelles ou liées aux politiques de gouvernance des données de votre organisation. |
| [Identité](../../../data-governance/labels/reference.md#identity){target="_blank"} | Cette catégorie est utilisée pour classer les données qui peuvent identifier directement ou indirectement une personne. |
| [&#x200B; Sensible &#x200B;](../../../data-governance/labels/reference.md#sensitive){target="_blank"} | Cette catégorie est utilisée pour classer les données que votre organisation considère comme sensibles. |
| [Réseau Partenaires](../../../data-governance/labels/reference.md#partner){target="_blank"} | Cette catégorie est utilisée pour classer les données obtenues à partir de sources externes à votre organisation. |
| Engagement responsable | Cette catégorie contient une étiquette unique, **[!UICONTROL Potential for Bias]**, qui reflète les données susceptibles d&#39;introduire un biais. |
| Valeur personnalisée | Cette catégorie comprend les libellés créés par votre organisation. |

Pour filtrer les libellés, sélectionnez l’icône de filtre (![icône de filtre](/help/images/icons/filter.png)), puis sélectionnez le type de libellé de votre choix dans la liste déroulante **[!UICONTROL Type]**.

![Espace de travail des libellés avec l’option de filtre développée et la liste déroulante de type mise en surbrillance.](../../images/ui/labels/label-filter.png){zoomable="yes"}

Pour afficher une étiquette individuelle, sélectionnez son nom dans la liste. La page de détails du libellé s’affiche. Les libellés de base d’Adobe ne sont **pas** modifiables.

![Page de détails d’une étiquette individuelle.](../../images/ui/labels/label-details.png){zoomable="yes"}

## Création d’un libellé personnalisé {#create-custom-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="Utilisation des libellés"
>abstract="Vous pouvez utiliser des libellés personnalisés pour appliquer à vos données des configurations de gouvernance des données et de contrôle d&#39;accès."

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Créer un libellé"
>abstract="Vous pouvez créer vos propres libellés personnalisés selon les besoins de votre entreprise. Les libellés personnalisés peuvent être utilisés pour appliquer à vos données à la fois des configurations de gouvernance des données et de contrôle d&#39;accès."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=fr#manage-labels" text="Gérer les libellés personnalisés"

>[!NOTE]
>
>Pour créer un libellé personnalisé, vous avez besoin d’un rôle contenant les autorisations **[!UICONTROL Manage Usage Labels]** et le sandbox `Prod`.

Pour créer un libellé, sélectionnez **[!UICONTROL Labels]** dans le panneau de gauche de l’espace de travail **[!UICONTROL Permissions]**, puis sélectionnez **[!UICONTROL Create label]**.

![Espace de travail des libellés avec l’option Créer un libellé mise en surbrillance.](../../images/ui/labels/create-label.png){zoomable="yes"}

La boîte de dialogue **[!UICONTROL Create new label]** s’affiche, vous invitant à saisir un **[!UICONTROL Name]**, un **[!UICONTROL Friendly name]** et un **[!UICONTROL Description]**.

>[!IMPORTANT]
>
> La [!UICONTROL Name] du libellé ne peut pas être modifiée une fois le libellé créé et la suppression du libellé n’est actuellement pas prise en charge.

Sélectionnez **[!UICONTROL Confirm]** pour terminer la création de votre étiquette.

![La boîte de dialogue Créer un libellé avec le nom, le nom convivial et la description renseignés et l’option Confirmer mise en surbrillance.](../../images/ui/labels/create-new-label.png){zoomable="yes"}

## Modification d’un libellé personnalisé {#edit-custom-label}

Bien que vous ne puissiez pas modifier le **[!UICONTROL Name]** d’une étiquette personnalisée, vous pouvez modifier les **[!UICONTROL Friendly name]** et les **[!UICONTROL Description]**. Pour modifier un libellé personnalisé, sélectionnez-le dans la liste de l’espace de travail **[!UICONTROL Labels]**.

![Espace de travail Libellés avec le libellé en surbrillance.](../../images/ui/labels/select-label.png){zoomable="yes"}

Modifiez l’un des champs, puis cliquez n’importe où en dehors de la zone de texte pour enregistrer vos modifications. Un message de confirmation s’affiche à l’écran et le nom du **[!UICONTROL Modified by]** ainsi que la date de **[!UICONTROL Modified]** changent.

![Page de détails du libellé avec un message « mis à jour avec succès » affiché.](../../images/ui/labels/edit-label.png){zoomable="yes"}

## Étapes suivantes

Maintenant que vous connaissez mieux les libellés, vous pouvez commencer [à les appliquer aux schémas](../../../xdm/tutorials/labels.md).
