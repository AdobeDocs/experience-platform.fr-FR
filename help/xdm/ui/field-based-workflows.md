---
title: Workflows basés sur les champs dans l’éditeur de schémas (version bêta)
description: Découvrez comment ajouter individuellement des champs provenant de groupes de champs existants à vos schémas de modèle de données d’expérience (XDM).
hide: true
hidefromtoc: true
exl-id: 0499ff30-a602-419b-b9d3-2defdd4354a7
source-git-commit: b7c6f37d3e6d824465713647b624473cff188378
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# Workflows basés sur les champs dans l’éditeur de schémas (version bêta)

>[!IMPORTANT]
>
>Les workflows décrits dans ce document sont actuellement en version bêta. La fonctionnalité et la documentation peuvent être modifiées.

Adobe Experience Platform fournit un solide ensemble de groupes de champs [normalisés](../schema/composition.md#field-group) à utiliser dans les schémas de modèle de données d’expérience (XDM). La structure et la sémantique derrière ces groupes de champs sont soigneusement conçues pour répondre à un large éventail de cas d’utilisation de la segmentation et à d’autres applications en aval dans Platform. Vous pouvez également définir vos propres groupes de champs personnalisés pour répondre à des besoins professionnels uniques.

Lorsque vous ajoutez un groupe de champs à un schéma, ce schéma hérite de tous les champs contenus dans ce groupe. Cependant, vous pouvez maintenant ajouter des champs individuels à votre schéma sans avoir à inclure d’autres champs du groupe de champs associé que vous ne pouvez pas nécessairement utiliser.

Ce guide décrit les différentes méthodes d’ajout de champs individuels à un schéma dans l’interface utilisateur de Platform.

## Conditions préalables

Ce tutoriel suppose que vous connaissez la [composition des schémas XDM](../schema/composition.md) et comment utiliser l’éditeur de schémas dans l’interface utilisateur de Platform. Pour poursuivre, vous devez lancer le processus de [création d’un nouveau schéma](./resources/schemas.md) et l’affecter à une classe standard avant de poursuivre avec ce guide.

## Supprimer les champs ajoutés des groupes de champs standard

Après avoir ajouté un groupe de champs standard à un schéma, vous pouvez supprimer tous les champs standard dont vous n’avez pas besoin.

>[!NOTE]
>
>La suppression de champs d’un groupe de champs standard affecte uniquement le schéma en cours de traitement et n’affecte pas le groupe de champs lui-même. Si vous supprimez des champs standard dans un schéma, ces champs sont toujours disponibles dans tous les autres schémas qui utilisent le même groupe de champs.

Dans l’exemple suivant, le groupe de champs standard **[!UICONTROL Détails démographiques]** a été ajouté à un schéma. Pour supprimer un champ unique, tel que `taxId`, sélectionnez le champ dans la zone de travail, puis sélectionnez **[!UICONTROL Supprimer]** dans le rail de droite.

![Supprimer un champ unique](../images/ui/field-based-workflows/remove-single-field.png)

Si vous souhaitez supprimer plusieurs champs, vous pouvez gérer le groupe dans son ensemble. Sélectionnez un champ appartenant au groupe dans la zone de travail, puis sélectionnez **[!UICONTROL Gérer les champs associés]** dans le rail de droite.

![Gestion des champs associés](../images/ui/field-based-workflows/manage-related-fields.png)

Une boîte de dialogue s’affiche, indiquant la structure du groupe de champs en question. À partir de là, vous pouvez utiliser les cases à cocher fournies pour sélectionner ou désélectionner les champs dont vous avez besoin. Lorsque vous êtes satisfait, sélectionnez **[!UICONTROL Ajouter des champs]**.

![Sélectionner les champs d’un groupe de champs](../images/ui/field-based-workflows/select-fields.png)

Le canevas réapparaît avec uniquement les champs sélectionnés présents dans la structure du schéma.

![Champs ajoutés](../images/ui/field-based-workflows/fields-added.png)

## Ajout direct de champs standard à un schéma

Vous pouvez ajouter directement à un schéma des champs provenant de groupes de champs standard sans avoir à connaître au préalable le groupe de champs correspondant. Pour ajouter un champ standard à un schéma, sélectionnez l’icône plus (**+**) en regard du nom du schéma dans la zone de travail. Un espace réservé **[!UICONTROL Champ sans titre]** apparaît dans la structure du schéma et le rail droit est mis à jour pour afficher les commandes permettant de configurer le champ.

![Espace réservé du champ](../images/ui/field-based-workflows/root-custom-field.png)

Sous **[!UICONTROL Nom du champ]**, commencez à saisir le nom du champ que vous souhaitez ajouter. Le système recherche automatiquement les champs standard correspondant à la requête et les répertorie sous **[!UICONTROL Champs standard recommandés]**, y compris les groupes de champs auxquels ils appartiennent.

![Champs standard recommandés](../images/ui/field-based-workflows/standard-field-search.png)

Bien que certains champs standard portent le même nom, leur structure peut varier en fonction du groupe de champs d’où ils proviennent. Si un champ standard est imbriqué dans un objet parent dans la structure du groupe de champs, le champ parent sera également inclus dans le schéma si le champ enfant est ajouté.

Sélectionnez l’icône d’aperçu (![Icône d’aperçu](../images/ui/field-based-workflows/preview-icon.png)) en regard d’un champ standard pour afficher la structure de son groupe de champs et mieux comprendre comment il peut être imbriqué. Pour ajouter le champ standard au schéma, sélectionnez l’icône plus (![Icône Plus](../images/ui/field-based-workflows/add-icon.png)).

![Ajouter un champ standard](../images/ui/field-based-workflows/add-standard-field.png)

Le canevas se met à jour pour afficher le champ standard ajouté au schéma, y compris tous les champs parents sous lesquels il est imbriqué dans la structure du groupe de champs. Le nom du groupe de champs est également répertorié sous **[!UICONTROL Groupes de champs]** dans le rail de gauche. Si vous souhaitez ajouter d’autres champs à partir du même groupe de champs, sélectionnez **[!UICONTROL Gérer les champs associés]** dans le rail de droite.

![Champ standard ajouté](../images/ui/field-based-workflows/standard-field-added.png)

## Ajout direct de champs personnalisés à un schéma

Si vous avez déjà [créé des groupes de champs personnalisés](./resources/field-groups.md#create), vous pouvez ajouter des champs personnalisés directement au schéma sans avoir à les ajouter séparément à un groupe de champs personnalisés au préalable.

>[!WARNING]
>
>Lorsque vous ajoutez un champ personnalisé à un schéma, vous devez toujours sélectionner un groupe de champs personnalisé existant auquel il sera associé. Cela signifie que pour ajouter directement des champs personnalisés à un schéma, vous devez disposer d’au moins un groupe de champs personnalisés défini précédemment dans l’environnement de test dans lequel vous travaillez. En outre, tous les autres schémas qui utilisent ce groupe de champs personnalisé hériteront également du nouveau champ ajouté après avoir enregistré vos modifications.

Pour ajouter des champs au niveau racine d’un schéma, sélectionnez l’icône plus (**+**) en regard du nom du schéma dans la zone de travail. Un espace réservé **[!UICONTROL Champ sans titre]** apparaît dans la structure du schéma et le rail droit est mis à jour pour afficher les commandes permettant de configurer le champ.

![Champ personnalisé racine](../images/ui/field-based-workflows/root-custom-field.png)

Commencez à saisir le nom du champ personnalisé que vous souhaitez ajouter, et le système commence automatiquement à rechercher les champs standard correspondants. Pour créer un champ personnalisé à la place, sélectionnez l’option supérieure ajoutée avec **([!UICONTROL Nouveau champ])**.

![Nouveau champ](../images/ui/field-based-workflows/custom-field-search.png)

À partir de là, indiquez un nom d’affichage et un type de données pour le champ. Sous **[!UICONTROL Attribuer un groupe de champs]**, sélectionnez le groupe de champs personnalisé auquel vous souhaitez associer le nouveau champ.

![Sélectionner un groupe de champs](../images/ui/field-based-workflows/select-field-group.png)

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]**.

![Appliquer le champ](../images/ui/field-based-workflows/apply-field.png)

Le nouveau champ est ajouté à la zone de travail et est un espace de noms situé sous votre [identifiant du client](../api/getting-started.md#know-your-tenant_id) afin d’éviter tout conflit avec les champs XDM standard. Le groupe de champs auquel vous avez associé le nouveau champ apparaît également sous **[!UICONTROL Groupes de champs]** dans le rail de gauche.

![Identifiant du client](../images/ui/field-based-workflows/tenantId.png)

>[!NOTE]
>
>Les autres champs fournis par le groupe de champs personnalisé sélectionné sont supprimés du schéma par défaut. Si vous souhaitez ajouter certains de ces champs au schéma, sélectionnez un champ appartenant au groupe, puis sélectionnez **[!UICONTROL Gérer les champs associés]** dans le rail de droite.

### Ajouter des champs personnalisés à la structure des groupes de champs standard

Si le schéma sur lequel vous travaillez comporte un champ de type objet fourni par un groupe de champs standard, vous pouvez ajouter vos propres champs personnalisés à cet objet standard. Sélectionnez l’icône plus (**+**) en regard de la racine de l’objet et fournissez les détails du champ personnalisé dans le rail de droite.

![Ajouter un champ à un objet standard](../images/ui/field-based-workflows/add-field-to-standard-object.png)

Après avoir appliqué vos modifications, le nouveau champ s’affiche sous l’espace de noms de l’identifiant du client dans l’objet standard. Cet espace de noms imbriqué empêche les conflits de nom de champ dans le groupe de champs lui-même afin d’éviter de rompre les modifications dans d’autres schémas qui utilisent le même groupe de champs.

## Étapes suivantes

Ce guide décrit les nouveaux workflows basés sur les champs de l’éditeur de schémas dans l’interface utilisateur de Platform. Pour plus d’informations sur la gestion des schémas dans l’interface utilisateur, consultez la [présentation de l’interface utilisateur](./overview.md).
