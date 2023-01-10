---
keywords: Experience Platform;accueil;rubriques les plus consultées;guide d’utilisation des sandbox;guide des sandbox
solution: Experience Platform
title: Guide de l’interface utilisateur des sandbox
description: Ce document fournit la procédure à suivre pour réaliser différentes opérations associées aux sandbox dans l’interface utilisateur d’Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 100%

---

# Guide de l’interface utilisateur des sandbox

Ce document fournit la procédure à suivre pour réaliser différentes opérations associées aux sandbox dans l’interface utilisateur d’Adobe Experience Platform.

## Affichage des sandbox

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sandbox]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Parcourir]** pour ouvrir le tableau de bord [!UICONTROL Sandbox]. Le tableau de bord répertorie toutes les sandbox disponibles pour votre organisation, y compris leurs types respectifs (production ou développement).

![afficher-sandbox](../images/ui/view-sandboxes.png)

## Basculer entre des sandbox

L’indicateur sandbox se trouve dans l’en-tête supérieur de l’interface utilisateur de Platform et affiche le titre de la sandbox dans laquelle vous vous trouvez actuellement, sa région et son type.

![indicateur-sandbox](../images/ui/sandbox-indicator.png)

Pour passer d’une sandbox à l’autre, cliquez sur l’indicateur sandbox et sélectionnez la sandbox souhaitée depuis la liste déroulante.

![sélecteur-interface](../images/ui/switcher-interface.png)

Une fois qu’une sandbox est sélectionnée, l’écran actualise la sandbox que vous avez sélectionnée et la met à jour.

![basculement-sandbox](../images/ui/sandbox-switched.png)

## Créer une sandbox {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Nom de la sandbox"
>abstract="Le nom de la sandbox est le texte utilisé sur le serveur principal pour créer un identifiant unique pour cette sandbox."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Titre de la sandbox"
>abstract="Le titre de la sandbox est le nom d’affichage qui représente la sandbox dans les menus et les listes déroulantes de l’interface utilisateur d’Experience Platform."

>[!NOTE]
>
>Lorsqu’une nouvelle sandbox est créée, vous devez d’abord l’ajouter à votre profil de produit dans [Adobe Admin Console](https://adminconsole.adobe.com/) avant de commencer à utiliser la nouvelle sandbox. Consultez la documentation relative à la [gestion des autorisations pour un profil de produit](../../access-control/ui/permissions.md) pour plus d’informations sur la configuration d’une sandbox en fonction d’un profil de produit.

La vidéo suivante présente un aperçu rapide de l’utilisation des sanbdox dans Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Pour créer une nouvelle sandbox, sélectionnez **[!UICONTROL Créer une sandbox]** dans le coin supérieur droit de l’écran.

![créer-sandbox](../images/ui/create-sandbox.png)

La boîte de dialogue **[!UICONTROL Créer une sandbox]** s’affiche. Si vous créez une sandbox de développement, sélectionnez **[!UICONTROL Développement]** dans le panneau déroulant. Pour créer une nouvelle sandbox de production, sélectionnez **[!UICONTROL Production]**.

![type-sandbox](../images/ui/sandbox-type.png)

Après avoir sélectionné le type, indiquez un nom et un titre à votre sandbox. Le titre est prévu pour être lu par un utilisateur ou une utilisatrice et doit être suffisamment descriptif pour permettre son identification rapide. Le nom de la sandbox est un identifiant entièrement en minuscules à utiliser dans les appels API qui se doit donc d’être unique et concis. Le nom de la sandbox doit commencer par une lettre, comporter au maximum 256 caractères et se composer uniquement de caractères alphanumériques et de tirets (-).

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Créer]**.

![sandbox-info](../images/ui/sandbox-info.png)

Lorsque vous avez terminé de créer la sandbox, actualisez la page pour que la nouvelle sandbox apparaisse dans le tableau de bord **[!UICONTROL Sandbox]** avec le statut « [!UICONTROL En cours de création] ». Il faut environ 30 secondes pour que le système approvisionne les nouvelles sandbox, auquel cas leur statut passera à « [!UICONTROL Actif] ».

![nouvelle-sandbox](../images/ui/new-sandbox.png)

## Réinitialiser une sandbox

>[!WARNING]
>
>Voici une liste d’exceptions qui peuvent vous empêcher de réinitialiser la sandbox de production par défaut ou une sandbox de production créée par l’utilisateur ou l’utilisatrice : <ul><li>La sandbox de production par défaut ne peut pas être réinitialisée si le graphique d’identités hébergé dans la sandbox est également utilisé par Adobe Analytics pour la fonctionnalité [Analyses sur l’ensemble des appareils (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=fr).</li><li>La sandbox de production par défaut ne peut pas être réinitialisée si le graphique d’identités hébergé dans la sandbox est également utilisé par Adobe Audience Manager pour les [Destinations basées sur les personnes (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=fr).</li><li>La sandbox de production par défaut ne peut pas être réinitialisée si elle contient des données pour les fonctionnalités CDA et PBD en même temps.</li><li>Une sandbox de production créée par l’utilisateur ou l’utilisatrice et utilisée pour le partage bidirectionnel de segments avec Adobe Audience Manager ou Audience Core Service peut être réinitialisée après un message d’avertissement.</li></ul>

La réinitialisation d’une sandbox de production ou de développement supprime toutes les ressources associées à cette sandbox (schémas, jeux de données, etc.) tout en conservant le nom et les autorisations associées de la sandbox. Cette sandbox « propre » reste disponible avec le même nom auprès des utilisateurs qui y ont accès.

Sélectionnez la sandbox à réinitialiser dans la liste des sandbox. Dans le panneau de navigation de droite qui s’affiche, sélectionnez **[!UICONTROL Réinitialisation de la sandbox]**.

![reset](../images/ui/reset.png)

Une boîte de dialogue s’affiche vous invitant à confirmer votre choix. Sélectionnez **[!UICONTROL Continuer]** pour continuer.

![avertissement-réinitialisation](../images/ui/reset-warning.png)

Dans la fenêtre de confirmation finale, saisissez le nom de la sandbox dans la boîte de dialogue et sélectionnez **[!UICONTROL Réinitialiser]**.

![confirmation-réinitialisation](../images/ui/reset-confirm.png)

## Supprimer une sandbox

>[!WARNING]
>
>Vous ne pouvez pas supprimer la sandbox de production par défaut. Cependant, toute sandbox de production créée par l’utilisateur ou l’utilisatrice utilisée pour le partage bidirectionnel de segments avec [!DNL Audience Manager] ou [!DNL Audience Core Service] peut être supprimée après un message d’avertissement.

La suppression d’une sandbox de production ou de développement supprime définitivement toutes les ressources associées à cette sandbox, y compris les autorisations.

Sélectionnez la sandbox à supprimer dans la liste des sandbox. Dans le panneau de navigation de droite qui s’affiche, sélectionnez **[!UICONTROL Supprimer]**.

![delete](../images/ui/delete.png)

Une boîte de dialogue s’affiche vous invitant à confirmer votre choix. Sélectionnez **[!UICONTROL Continuer]** pour continuer.

![avertissement-suppression](../images/ui/delete-warning.png)

Dans la fenêtre de confirmation finale, saisissez le nom de la sandbox dans la boîte de dialogue et sélectionnez **[!UICONTROL Continuer]**.

![confirmation-suppression](../images/ui/delete-confirm.png)

## Étapes suivantes

Ce document vous a montré comment gérer les environnements de test dans l’interface utilisateur d’Experience Platform. Pour plus d’informations sur la gestion des environnements de test à l’aide de l’API Sandbox, consultez le [guide de développement des environnements de test](../api/getting-started.md).
