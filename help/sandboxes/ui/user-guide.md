---
keywords: Experience Platform;accueil;rubriques les plus consultées;guide d’utilisation des sandbox;guide des sandbox
solution: Experience Platform
title: Guide de l’interface utilisateur des sandbox
description: Ce document fournit la procédure à suivre pour réaliser différentes opérations associées aux sandbox dans l’interface utilisateur d’Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 36%

---

# Guide de l’interface utilisateur des sandbox

Ce document fournit la procédure à suivre pour réaliser différentes opérations associées aux sandbox dans l’interface utilisateur d’Adobe Experience Platform.

## Affichage des sandbox

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sandboxes]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Browse]** pour ouvrir le tableau de bord [!UICONTROL Sandboxes]. Le tableau de bord répertorie tous les sandbox disponibles pour votre organisation, y compris leurs types respectifs (production ou développement).

![Tableau de bord des sandbox avec l’onglet Parcourir sélectionné qui affiche une liste des sandbox disponibles.](../images/ui/view-sandboxes.png)

## Basculer entre des sandbox

L’indicateur sandbox se trouve dans l’en-tête supérieur de l’interface utilisateur d’Experience Platform et affiche le titre du sandbox dans lequel vous vous trouvez actuellement, sa région et son type.

![Tableau de bord des sandbox avec l’indicateur de sandbox en surbrillance.](../images/ui/sandbox-indicator.png)

Pour basculer entre les sandbox, sélectionnez l’indicateur sandbox , puis sélectionnez la sandbox de votre choix dans la liste déroulante. Vous pouvez également rechercher le sandbox de votre choix à l’aide de la fonction de recherche dans le menu déroulant.

![Le menu déroulant des indicateurs de sandbox s’affiche, affichant une liste des sandbox auxquels vous avez accès.](../images/ui/switcher-interface.png)

Une fois qu’un sandbox est sélectionné, l’écran actualise le sandbox que vous avez sélectionné et le met à jour.

![Tableau de bord du sandbox avec l’indicateur de sandbox modifié en surbrillance.](../images/ui/sandbox-switched.png)

## Création d’un sandbox {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Nom du sandbox"
>abstract="Le nom du sandbox est le texte utilisé sur le serveur principal pour créer un identifiant unique pour ce sandbox."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Titre du sandbox"
>abstract="Le titre du sandbox est le nom d’affichage qui représente le sandbox dans les menus et les listes déroulantes de l’interface utilisateur d’Experience Platform."

>[!WARNING]
>
>La création d’un nouveau sandbox nécessite que vous l’ajoutiez à un rôle dans [[!UICONTROL Permissions]](../../access-control/abac/ui/permissions.md) avant de pouvoir commencer à l’utiliser. Pour savoir comment configurer un sandbox pour un rôle, reportez-vous à la documentation [gestion des sandbox pour un rôle](../../access-control/abac/ui/permissions.md#managing-sandboxes-for-role).

La vidéo suivante présente un aperçu rapide de l’utilisation des sandbox dans Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Pour créer un nouveau sandbox, sélectionnez **[!UICONTROL Create sandbox]** dans le coin supérieur droit de l’écran.

![créer-sandbox](../images/ui/create-sandbox.png)

La boîte de dialogue **[!UICONTROL Create sandbox]** s’affiche. Sélectionnez la liste déroulante **[!UICONTROL Type]** et choisissez le type de sandbox [!UICONTROL Development] ou [!UICONTROL Production].

![Boîte de dialogue Créer un sandbox avec le sélecteur de type de sandbox mis en surbrillance.](../images/ui/sandbox-type.png)

Après avoir sélectionné le type, indiquez un nom pour votre sandbox dans le champ **[!UICONTROL Name]** . Le nom du sandbox est un identifiant entièrement en minuscules à utiliser dans les appels API qui se doit donc d’être unique et concis. Le nom du sandbox doit commencer par une lettre, comporter au maximum 256 caractères et se composer uniquement de caractères alphanumériques et de tirets (-). Indiquez ensuite un titre pour votre sandbox dans le champ **[!UICONTROL Title]** . Le titre est destiné à être lu par un utilisateur ou une utilisatrice et doit être suffisamment descriptif pour être facilement identifiable.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Create]**.

![La boîte de dialogue Créer un sandbox avec le champ Nom et Titre et l’option Créer mise en surbrillance.](../images/ui/sandbox-info.png)

Une fois la création du sandbox terminée, actualisez la page pour que le nouveau sandbox apparaisse dans le tableau de bord **[!UICONTROL Sandboxes]** avec le statut « [!UICONTROL Creating] ». Il faut environ 30 secondes pour que le système approvisionne les nouveaux sandbox, auquel cas leur statut passera à « [!UICONTROL Active] ».

![Tableau de bord des sandbox avec le nouveau sandbox mis en surbrillance.](../images/ui/new-sandbox.png)

## Réinitialisation d’un sandbox

>[!WARNING]
>
>Voici une liste d’exceptions qui peuvent vous empêcher de réinitialiser le sandbox de production par défaut ou un sandbox de production créé par l’utilisateur ou l’utilisatrice :
>
>* Un sandbox de production créé par l’utilisateur ou l’utilisatrice et utilisé pour le partage bidirectionnel de segments avec Adobe Audience Manager ou Audience Core Service peut être réinitialisé après un message d’avertissement.
>* Avant de lancer la réinitialisation d’un sandbox, vous devrez supprimer manuellement vos compositions pour vous assurer que les données d’audience associées sont correctement nettoyées.
>* L’ID du sandbox change une fois la réinitialisation terminée.
>* Pour [Journey Optimizer B2B edition](https://experienceleague.adobe.com/fr/docs/journey-optimizer-b2b/user/guide-overview), la réinitialisation du sandbox n’est **actuellement pas prise en charge**. La réinitialisation ou la suppression d’un sandbox mappé à Journey Optimizer B2B edition peut entraîner une perte permanente de données dans Journey Optimizer B2B edition et peut nécessiter la mise en service d’une nouvelle instance Journey Optimizer B2B edition.

### Supprimer les compositions d’audience

La composition de l’audience n’est actuellement pas intégrée à la fonctionnalité de réinitialisation du sandbox. Par conséquent, les audiences devront être supprimées manuellement avant d’effectuer la réinitialisation du sandbox.

Sélectionnez **[!UICONTROL Audiences]** dans la section **[!UICONTROL Customers]** du volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Compositions]** .

![Tableau de bord Audiences avec l’onglet Compositions sélectionné et mis en surbrillance.](../images/ui/audiences.png)

Sélectionnez ensuite les points de suspension (`...`) à côté de la première audience, puis sélectionnez **[!UICONTROL Delete]**.

![Menu Audience mettant en surbrillance l’option [!UICONTROL Delete].](../images/ui/delete-composition.png)

Une confirmation de suppression réussie s’affiche et vous revenez sur l’onglet **[!UICONTROL Compositions]** .

Répétez les étapes ci-dessus avec toutes vos compositions. Toutes les audiences de l’inventaire des audiences seront supprimées. Une fois toutes les audiences supprimées, vous pouvez continuer à réinitialiser le sandbox.

### Réinitialisation d’un sandbox

La réinitialisation d’un sandbox de production ou de développement supprime toutes les ressources associées à ce sandbox (schémas, jeux de données, etc.) tout en conservant le nom et les autorisations associées du sandbox. Ce sandbox « propre » reste disponible avec le même nom auprès des utilisateurs qui y ont accès.

Sélectionnez le sandbox à réinitialiser dans la liste des sandbox. Dans le panneau de navigation de droite qui s’affiche, sélectionnez **[!UICONTROL Sandbox reset]**.

![Tableau de bord du sandbox avec le sandbox sélectionné et l’option Réinitialisation du sandbox mise en surbrillance.](../images/ui/reset.png)

Une boîte de dialogue s’affiche vous invitant à confirmer votre choix. Sélectionnez **[!UICONTROL Continue]** pour continuer.

![La boîte de dialogue de réinitialisation s’affiche avec l’option Continuer en surbrillance.](../images/ui/reset-warning.png)

Dans la fenêtre de confirmation finale, saisissez le nom du sandbox dans la boîte de dialogue et sélectionnez **[!UICONTROL Reset]**.

![La boîte de dialogue de réinitialisation avec le champ Confirmer le nom et l’option de réinitialisation en surbrillance.](../images/ui/reset-confirm.png)

## Suppression d’un sandbox

>[!WARNING]
>
>Vous ne pouvez pas supprimer le sandbox de production par défaut. Cependant, tout sandbox de production créé par l’utilisateur ou l’utilisatrice utilisé pour le partage bidirectionnel de segments avec [!DNL Audience Manager] ou [!DNL Audience Core Service] peut être supprimé après un message d’avertissement.

La suppression d’un sandbox de production ou de développement supprime définitivement toutes les ressources associées à ce sandbox, y compris les autorisations.

Sélectionnez le sandbox à supprimer dans la liste des sandbox. Dans le panneau de navigation de droite qui s’affiche, sélectionnez **[!UICONTROL Delete]**.

![Tableau de bord du sandbox avec le sandbox sélectionné et l’option Supprimer mise en surbrillance.](../images/ui/delete.png)

Une boîte de dialogue s’affiche vous invitant à confirmer votre choix. Sélectionnez **[!UICONTROL Continue]** pour continuer.

![La boîte de dialogue de suppression s’affiche avec l’option Continuer en surbrillance.](../images/ui/delete-warning.png)

Dans la fenêtre de confirmation finale, saisissez le nom du sandbox dans la boîte de dialogue et sélectionnez **[!UICONTROL Continue]**.

![La boîte de dialogue de suppression avec le champ Confirmer le nom et l’option Continuer en surbrillance.](../images/ui/delete-confirm.png)

## Étapes suivantes

Ce document vous a montré comment gérer les sandbox dans l’interface utilisateur d’Experience Platform. Maintenant que vous savez comment gérer les sandbox, apprenez à améliorer la précision de la configuration entre les sandbox et à exporter et importer en toute transparence des configurations de sandbox entre les sandbox grâce au guide [fonctionnalité d’outils de sandbox](./sandbox-tooling.md).

Pour plus d’informations sur la gestion des sandbox à l’aide de l’API Sandbox, consultez le [guide de développement des sandbox](../api/getting-started.md).
