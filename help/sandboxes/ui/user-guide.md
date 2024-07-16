---
keywords: Experience Platform;accueil;rubriques les plus consultées;guide d’utilisation des sandbox;guide des sandbox
solution: Experience Platform
title: Guide de l’interface utilisateur des sandbox
description: Ce document fournit la procédure à suivre pour réaliser différentes opérations associées aux sandbox dans l’interface utilisateur d’Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 0db23e475d6546ebb886a56d5915d023ea215125
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 80%

---

# Guide de l’interface utilisateur des sandbox

Ce document fournit la procédure à suivre pour réaliser différentes opérations associées aux sandbox dans l’interface utilisateur d’Adobe Experience Platform.

## Affichage des sandbox

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sandbox]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Parcourir]** pour ouvrir le tableau de bord [!UICONTROL Sandbox]. Le tableau de bord répertorie tous les sandbox disponibles pour votre organisation, y compris leurs types respectifs (production ou développement).

![afficher-sandbox](../images/ui/view-sandboxes.png)

## Basculer entre des sandbox

L’indicateur sandbox se trouve dans l’en-tête supérieur de l’interface utilisateur de Platform et affiche le titre du sandbox dans lequel vous vous trouvez actuellement, sa région et son type.

![indicateur-sandbox](../images/ui/sandbox-indicator.png)

Pour passer d’un sandbox à l’autre, cliquez sur l’indicateur sandbox et sélectionnez le sandbox souhaité depuis la liste déroulante.

![sélecteur-interface](../images/ui/switcher-interface.png)

Une fois qu’un sandbox est sélectionné, l’écran actualise le sandbox que vous avez sélectionné et le met à jour.

![basculement-sandbox](../images/ui/sandbox-switched.png)

## Création d’un sandbox {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Nom du sandbox"
>abstract="Le nom du sandbox est le texte utilisé sur le serveur principal pour créer un identifiant unique pour ce sandbox."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Titre du sandbox"
>abstract="Le titre du sandbox est le nom d’affichage qui représente le sandbox dans les menus et les listes déroulantes de l’interface utilisateur d’Experience Platform."

>[!NOTE]
>
>La création d’un nouvel environnement de test nécessite que vous l’ajoutiez à un rôle dans [[!UICONTROL Permissions]](../../access-control/abac/ui/permissions.md) avant de pouvoir commencer à l’utiliser. Pour savoir comment configurer un environnement de test pour un rôle, reportez-vous à la documentation [gestion des environnements de test pour un rôle](../../access-control/abac/ui/permissions.md#managing-sandboxes-for-role) .

La vidéo suivante présente un aperçu rapide de l’utilisation des sandbox dans Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Pour créer un nouveau sandbox, sélectionnez **[!UICONTROL Créer un sandbox]** dans le coin supérieur droit de l’écran.

![créer-sandbox](../images/ui/create-sandbox.png)

La boîte de dialogue **[!UICONTROL Créer un sandbox]** s’affiche. Si vous créez un sandbox de développement, sélectionnez **[!UICONTROL Développement]** dans le panneau déroulant. Pour créer un nouveau sandbox de production, sélectionnez **[!UICONTROL Production]**.

![type-sandbox](../images/ui/sandbox-type.png)

Après avoir sélectionné le type, indiquez un nom et un titre à votre sandbox. Le titre est prévu pour être lu par un utilisateur ou une utilisatrice et doit être suffisamment descriptif pour permettre son identification rapide. Le nom du sandbox est un identifiant entièrement en minuscules à utiliser dans les appels API qui se doit donc d’être unique et concis. Le nom du sandbox doit commencer par une lettre, comporter au maximum 256 caractères et se composer uniquement de caractères alphanumériques et de tirets (-).

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Créer]**.

![sandbox-info](../images/ui/sandbox-info.png)

Lorsque vous avez terminé de créer le sandbox, actualisez la page pour que le nouveau sandbox apparaisse dans le tableau de bord **[!UICONTROL Sandbox]** avec le statut « [!UICONTROL En cours de création] ». Il faut environ 30 secondes pour que le système approvisionne les nouveaux sandbox, auquel cas leur statut passera à « [!UICONTROL Actif] ».

![nouvelle-sandbox](../images/ui/new-sandbox.png)

## Réinitialisation d’un sandbox

>[!WARNING]
>
>Voici une liste d’exceptions qui peuvent vous empêcher de réinitialiser le sandbox de production par défaut ou un sandbox de production créé par l’utilisateur ou l’utilisatrice :
>* Le sandbox de production par défaut ne peut pas être réinitialisé si le graphique d’identités hébergé dans le sandbox est également utilisé par Adobe Analytics pour la fonctionnalité [Analyses sur l’ensemble des appareils (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=fr).
>* Le sandbox de production par défaut ne peut pas être réinitialisé si le graphique d’identités hébergé dans le sandbox est également utilisé par Adobe Audience Manager pour les [Destinations basées sur les personnes (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=fr).
>* Le sandbox de production par défaut ne peut pas être réinitialisé s’il contient des données pour les fonctionnalités CDA et PBD en même temps.
>* Un sandbox de production créé par l’utilisateur ou l’utilisatrice et utilisé pour le partage bidirectionnel de segments avec Adobe Audience Manager ou Audience Core Service peut être réinitialisé après un message d’avertissement.
>* Avant de réinitialiser un environnement de test, vous devrez supprimer manuellement vos compositions pour vous assurer que les données d’audience associées sont correctement nettoyées.

### Suppression de compositions d’audience

La composition de l’audience n’est actuellement pas intégrée à la fonctionnalité de réinitialisation des environnements de test. Par conséquent, les audiences doivent être supprimées manuellement avant d’effectuer la réinitialisation des environnements de test.

Sélectionnez **[!UICONTROL Audiences]** dans le volet de navigation de gauche, puis **[!UICONTROL Compositions]**.

![Onglet [!UICONTROL Compositions] dans l’espace de travail [!UICONTROL Audiences].](../images/ui/audiences.png)

Sélectionnez ensuite les points de suspension (`...`) en regard de la première audience, puis sélectionnez **[!UICONTROL Supprimer]**.

![Le menu de l&#39;audience met en surbrillance l&#39;option [!UICONTROL Supprimer].](../images/ui/delete-composition.png)

Une confirmation de suppression réussie s’affiche et vous êtes renvoyé à l’onglet **[!UICONTROL Compositions]** .

Répétez les étapes ci-dessus avec toutes vos compositions. Toutes les audiences seront alors supprimées de l’inventaire des audiences. Une fois toutes les audiences supprimées, vous pouvez continuer à réinitialiser l’environnement de test.

### Réinitialisation d’un environnement de test

La réinitialisation d’un sandbox de production ou de développement supprime toutes les ressources associées à ce sandbox (schémas, jeux de données, etc.) tout en conservant le nom et les autorisations associées du sandbox. Ce sandbox « propre » reste disponible avec le même nom auprès des utilisateurs qui y ont accès.

Sélectionnez le sandbox à réinitialiser dans la liste des sandbox. Dans le panneau de navigation de droite qui s’affiche, sélectionnez **[!UICONTROL Réinitialisation du sandbox]**.

![reset](../images/ui/reset.png)

Une boîte de dialogue s’affiche vous invitant à confirmer votre choix. Sélectionnez **[!UICONTROL Continuer]** pour continuer.

![avertissement-réinitialisation](../images/ui/reset-warning.png)

Dans la fenêtre de confirmation finale, saisissez le nom du sandbox dans la boîte de dialogue et sélectionnez **[!UICONTROL Réinitialiser]**.

![confirmation-réinitialisation](../images/ui/reset-confirm.png)

## Suppression d’un sandbox

>[!WARNING]
>
>Vous ne pouvez pas supprimer le sandbox de production par défaut. Cependant, tout sandbox de production créé par l’utilisateur ou l’utilisatrice utilisé pour le partage bidirectionnel de segments avec [!DNL Audience Manager] ou [!DNL Audience Core Service] peut être supprimé après un message d’avertissement.

La suppression d’un sandbox de production ou de développement supprime définitivement toutes les ressources associées à ce sandbox, y compris les autorisations.

Sélectionnez le sandbox à supprimer dans la liste des sandbox. Dans le panneau de navigation de droite qui s’affiche, sélectionnez **[!UICONTROL Supprimer]**.

![delete](../images/ui/delete.png)

Une boîte de dialogue s’affiche vous invitant à confirmer votre choix. Sélectionnez **[!UICONTROL Continuer]** pour continuer.

![avertissement-suppression](../images/ui/delete-warning.png)

Dans la fenêtre de confirmation finale, saisissez le nom du sandbox dans la boîte de dialogue et sélectionnez **[!UICONTROL Continuer]**.

![confirmation-suppression](../images/ui/delete-confirm.png)

## Étapes suivantes

Ce document vous a montré comment gérer les sandbox dans l’interface utilisateur d’Experience Platform. Pour plus d’informations sur la gestion des sandbox à l’aide de l’API Sandbox, consultez le [guide de développement des sandbox](../api/getting-started.md).
