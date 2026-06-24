---
title: Gestionnaire d’autorisations de contrôle d’accès basé sur les attributs
description: Découvrez comment utiliser le Gestionnaire d’autorisations dans Adobe Experience Platform pour générer des rapports et valider les autorisations d’accès.
exl-id: 4c2b8b8e-ac4f-4c6e-a23f-66f658bb6e24
TQID: https://experienceleague.adobe.com/qhUKfblB85FWurnfDDqxd69sQdlOmA3CpZDbrEbUG04
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 606
ht-degree: 9%

---

# Gestionnaire d’autorisations

>[!NOTE]
>
>Pour accéder au [!UICONTROL Gestionnaire d’autorisations], vous devez être administrateur de produit. Si vous ne disposez pas de droits d’administrateur, contactez votre administrateur système pour obtenir l’accès.

Utilisez des requêtes simples dans le [!UICONTROL Gestionnaire d’autorisations] pour créer des rapports concis qui vous aideront à comprendre la gestion des accès et à gagner du temps lors de la validation des autorisations d’accès sur de nombreux workflows et niveaux de granularité. Vous pouvez utiliser le [!UICONTROL Gestionnaire d’autorisations] pour rechercher des utilisateurs qui appartiennent à un groupe d’utilisateurs et qui disposent de droits d’accès spécifiés, ainsi que des rôles dotés de libellés spécifiques.

## Rechercher des utilisateurs et utilisatrices au sein d’un groupe de personnes spécifique {#search-users}

>[!CONTEXTUALHELP]
>id="platform_permission_manager"
>title="Gestionnaire d’autorisations"
>abstract="Utilisez les sélecteurs de liste déroulante sur la page pour obtenir des rapports de niveau d’accès de différents niveaux de granularité pour les utilisateurs et utilisatrices et les rôles."
<!-- >additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-manager/permissions.html?lang=fr" text="Permission manager" -->

Dans la liste déroulante, sélectionnez l’attribut **[!UICONTROL Utilisateurs]**.

![Liste déroulante d’attributs mettant en surbrillance Utilisateurs.](../../images/permission-manager/users-select.png)

Sélectionnez ensuite le **[!UICONTROL Groupe d’utilisateurs]** que vous souhaitez rechercher à l’aide de la liste déroulante.

>[!INFO]
>
>[!UICONTROL Groupe d’utilisateurs] n’est pas un champ obligatoire. Vous ne pouvez sélectionner qu’un seul groupe d’utilisateurs pour chaque rapport.

![Le menu déroulant du groupe d’utilisateurs est mis en surbrillance.](../../images/permission-manager/user-group-select.png)

Pour obtenir un rapport plus granulaire, vous pouvez spécifier la ressource avec des actions dans un sandbox spécifique. Sélectionnez les **[!UICONTROL Ressource]**, **[!UICONTROL Actions]** et **[!UICONTROL Sandbox]** dans la liste déroulante, puis sélectionnez **[!UICONTROL Afficher les résultats]**.

>[!INFO]
>
>[!UICONTROL Ressource], [!UICONTROL Actions] et [!UICONTROL Sandbox] ne sont pas des champs obligatoires. Une action ou un sandbox peut être supprimé(e) une fois ajouté(e) en sélectionnant l’**du** en regard de la sélection que vous souhaitez supprimer.

![Les listes déroulantes Ressource, Actions, Sandbox et Afficher les résultats sont mises en surbrillance](../../images/permission-manager/users-additional-attributes-select.png)

Une liste d’utilisateurs et leur adresse e-mail sont signalés en fonction des critères sélectionnés. Utilisez le menu de filtre à gauche pour mettre à jour les attributs et les résultats. Pour plus d’informations sur un utilisateur spécifique, sélectionnez-le dans la liste.

![Rapport généré basé sur les attributs sélectionnés mis en surbrillance](../../images/permission-manager/users-report.png)

## Rechercher des rôles avec des libellés spécifiques {#search-roles}

Dans la liste déroulante, sélectionnez l’attribut **[!UICONTROL Rôles]**.

>[!INFO]
>
>[!UICONTROL Libellés] n’est pas un champ obligatoire. Vous pouvez sélectionner plusieurs libellés qui seront répertoriés sous cette liste déroulante une fois sélectionnés. Vous pouvez supprimer un libellé une fois qu’il a été ajouté en sélectionnant le **’x’** en regard de l’action.

![Liste déroulante d’attributs mettant en surbrillance les rôles.](../../images/permission-manager/roles-select.png)

Sélectionnez ensuite le **[!UICONTROL Libellés]** à rechercher à l’aide de la liste déroulante.

![Le menu déroulant Libellés est mis en surbrillance.](../../images/permission-manager/roles-labels-select.png)

Pour obtenir un rapport plus granulaire, vous pouvez spécifier la ressource avec des actions dans un sandbox spécifique. Sélectionnez les **[!UICONTROL Ressource]**, **[!UICONTROL Actions]** et **[!UICONTROL Sandbox]** dans la liste déroulante, puis sélectionnez **[!UICONTROL Afficher les résultats]**.

>[!INFO]
>
>[!UICONTROL Ressource], [!UICONTROL Actions] et [!UICONTROL Sandbox] ne sont pas des champs obligatoires. Un seul [!UICONTROL Ressource] peut être sélectionné pour chaque rapport. Une action ou un sandbox peut être supprimé(e) une fois ajouté(e) en sélectionnant l’**du** en regard de la sélection que vous souhaitez supprimer.

![Les listes déroulantes Ressource, Actions, Sandbox et Afficher les résultats sont mises en surbrillance](../../images/permission-manager/roles-additional-attributes-select.png)

Une liste de rôles est générée en fonction des critères sélectionnés. Utilisez le menu de filtre à gauche pour mettre à jour les attributs et les résultats. Pour plus d’informations sur un rôle spécifique, sélectionnez-le dans la liste.

Les informations suivantes s’affichent pour chaque rôle correspondant à vos critères :

| Attribut | Description |
| --- | --- |
| Description | Brève description du rôle. |
| Étiquettes | Liste des libellés associés au rôle. |
| Sandbox | Liste des sandbox contenant ce rôle. |
| Modifié le | Date et heure de la dernière mise à jour du rôle. |
| Date de création | Date et heure de la création du rôle. |
| Créé par | Détails du créateur du rôle. |

![Rapport généré basé sur les attributs sélectionnés mis en surbrillance](../../images/permission-manager/roles-report.png)

## Étapes suivantes

Vous savez maintenant comment générer des rapports pour les utilisateurs et les rôles. Pour en savoir plus sur le contrôle d’accès basé sur les attributs, consultez la [présentation du contrôle d’accès basé sur les attributs](../overview.md).
