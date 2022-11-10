---
keywords: Experience Platform;accueil;rubriques les plus consultées;guide d’utilisation des environnements de test;guide sandbox
solution: Experience Platform
title: Guide de l’interface utilisateur des environnements de test
topic-legacy: user guide
description: Ce document fournit la procédure à suivre pour réaliser différentes opérations associées aux environnements de test dans l’interface utilisateur d’Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: df0f543b18f008b656c5e411305c5243efa744ad
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 15%

---

# Guide de l’interface utilisateur des environnements de test

Ce document fournit la procédure à suivre pour réaliser différentes opérations associées aux environnements de test dans l’interface utilisateur d’Adobe Experience Platform.

## Affichage des environnements de test

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Environnements de test]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Parcourir]** pour ouvrir le [!UICONTROL Environnements de test] tableau de bord. Le tableau de bord répertorie tous les environnements de test disponibles pour votre organisation, y compris leurs types respectifs (production ou développement).

![view-sandbox](../images/ui/view-sandboxes.png)

## Basculer entre des environnements de test

L’indicateur sandbox se trouve dans l’en-tête supérieur de l’interface utilisateur de Platform et affiche le titre de l’environnement de test dans lequel vous vous trouvez actuellement, sa région et son type.

![indicateur sandbox](../images/ui/sandbox-indicator.png)

Pour passer d’un environnement de test à un autre, sélectionnez l’indicateur sandbox et sélectionnez l’environnement de test de votre choix dans la liste déroulante.

![sélecteur-interface](../images/ui/switcher-interface.png)

Une fois qu’un environnement de test est sélectionné, l’écran actualise l’environnement de test que vous avez sélectionné et le met à jour.

![sandbox-switch](../images/ui/sandbox-switched.png)

## Création d’un nouvel environnement de test {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Nom du sandbox"
>abstract="Le nom de l’environnement de test est le texte utilisé sur le serveur principal pour créer un identifiant unique pour cet environnement de test."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Titre du sandbox"
>abstract="Le titre de l’environnement de test est le nom d’affichage qui représente l’environnement de test dans les menus et les listes déroulantes de l’interface utilisateur de l’Experience Platform."

>[!NOTE]
>
>Lorsqu’un nouvel environnement de test est créé, vous devez d’abord l’ajouter à votre profil de produit dans [Adobe Admin Console](https://adminconsole.adobe.com/) avant de commencer à utiliser le nouvel environnement de test. Consultez la documentation relative à [gestion des autorisations pour un profil de produit](../../access-control/ui/permissions.md) pour plus d’informations sur la configuration d’un environnement de test à un profil de produit.

La vidéo suivante présente un aperçu rapide de l’utilisation des environnements de test dans Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Pour créer un environnement de test, sélectionnez **[!UICONTROL Création d’un environnement de test]** dans le coin supérieur droit de l’écran.

![create-sandbox](../images/ui/create-sandbox.png)

Le **[!UICONTROL Création d’un environnement de test]** s’affiche. Si vous créez un environnement de test de développement, sélectionnez **[!UICONTROL Développement]** dans le panneau déroulant. Pour créer un environnement de test de production, sélectionnez **[!UICONTROL Production]**.

![sandbox-type](../images/ui/sandbox-type.png)

Après avoir sélectionné le type , indiquez un nom et un titre à votre environnement de test. Le titre est censé être lisible par l’utilisateur et doit être suffisamment descriptif pour permettre son identification rapide. Le nom de l’environnement de test est un identifiant entièrement en minuscules à utiliser dans les appels API. Il doit donc être unique et concis. Le nom de l’environnement de test doit commencer par une lettre, comporter au maximum 256 caractères et se composer uniquement de caractères alphanumériques et de tirets (-).

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Créer]**.

![sandbox-info](../images/ui/sandbox-info.png)

Une fois la création de l’environnement de test terminée, actualisez la page pour que le nouvel environnement de test apparaisse dans la variable **[!UICONTROL Environnements de test]** tableau de bord avec le statut &quot;[!UICONTROL Création]&quot;. Les nouveaux environnements de test prennent environ 30 secondes pour être configurés par le système, après quoi leur état passe à &quot;[!UICONTROL Principal]&quot;.

![new-sandbox](../images/ui/new-sandbox.png)

## Réinitialisation d’un environnement de test

>[!WARNING]
>
>Voici une liste d’exceptions qui peut vous empêcher de réinitialiser l’environnement de test de production par défaut ou un environnement de test de production créé par l’utilisateur : <ul><li>L’environnement de test de production par défaut ne peut pas être réinitialisé si le graphique d’identités hébergé dans l’environnement de test est également utilisé par Adobe Analytics pour la variable [Analyses entre appareils (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=fr) fonction .</li><li>L’environnement de test de production par défaut ne peut pas être réinitialisé si le graphique d’identités hébergé dans l’environnement de test est également utilisé par Adobe Audience Manager pour la variable [Destinations basées sur les personnes (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=fr).</li><li>L’environnement de test de production par défaut ne peut pas être réinitialisé s’il contient des données pour les fonctionnalités des analyses entre appareils et des analyses entre appareils (PBD).</li><li>Un environnement de test de production créé par l’utilisateur et utilisé pour le partage bidirectionnel de segments avec Adobe Audience Manager ou Audience Core Service peut être réinitialisé après un message d’avertissement.</li></ul>

La réinitialisation d’un environnement de test de production ou de développement supprime toutes les ressources associées à cet environnement de test (schémas, jeux de données, etc.), tout en conservant le nom de l’environnement de test et les autorisations associées. Cet environnement de test « propre » reste disponible avec le même nom auprès des utilisateurs qui y ont accès.

Sélectionnez l’environnement de test à réinitialiser dans la liste des environnements de test. Dans le panneau de navigation de droite qui s’affiche, sélectionnez **[!UICONTROL Réinitialisation des environnements de test]**.

![reset](../images/ui/reset.png)

Une boîte de dialogue s’affiche, vous invitant à confirmer votre choix. Sélectionner **[!UICONTROL Continuer]** pour continuer.

![reset-warning](../images/ui/reset-warning.png)

Dans la fenêtre de confirmation finale, saisissez le nom de l’environnement de test dans la boîte de dialogue et sélectionnez **[!UICONTROL Réinitialiser]**.

![reset-confirm](../images/ui/reset-confirm.png)

## Suppression d’un environnement de test

>[!WARNING]
>
>Vous ne pouvez pas supprimer l’environnement de test de production par défaut. Cependant, tout environnement de test de production créé par l’utilisateur utilisé pour le partage bidirectionnel de segments avec [!DNL Audience Manager] ou [!DNL Audience Core Service] peut être supprimé après un message d’avertissement.

La suppression d’un environnement de test de production ou de développement supprime définitivement toutes les ressources associées à cet environnement de test, y compris les autorisations.

Sélectionnez l’environnement de test à supprimer dans la liste des environnements de test. Dans le panneau de navigation de droite qui s’affiche, sélectionnez **[!UICONTROL Supprimer]**.

![delete](../images/ui/delete.png)

Une boîte de dialogue s’affiche, vous invitant à confirmer votre choix. Sélectionner **[!UICONTROL Continuer]** pour continuer.

![delete-warning](../images/ui/delete-warning.png)

Dans la fenêtre de confirmation finale, saisissez le nom de l’environnement de test dans la boîte de dialogue et sélectionnez  **[!UICONTROL Continuer]**.

![delete-confirm](../images/ui/delete-confirm.png)

## Étapes suivantes

Ce document vous a montré comment gérer les environnements de test dans l’interface utilisateur d’Experience Platform. Pour plus d’informations sur la gestion des environnements de test à l’aide de l’API Sandbox, consultez le [guide de développement des environnements de test](../api/getting-started.md).
