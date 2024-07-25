---
keywords: mettre à jour le compte de destination, les comptes de destination, comment mettre à jour les comptes, mettre à jour la destination
title: Mettre à jour les comptes de destination
type: Tutorial
description: Ce tutoriel répertorie les étapes de mise à jour des comptes de destination dans l’interface utilisateur de Adobe Experience Platform.
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 10%

---

# Mettre à jour les comptes de destination

## Vue d’ensemble {#overview}

L’onglet **[!UICONTROL Comptes]** vous montre des détails sur les connexions que vous avez établies avec différentes destinations. Reportez-vous à la [présentation des comptes](../ui/destinations-workspace.md#accounts) pour toutes les informations que vous pouvez obtenir sur chaque compte de destination.

Ce tutoriel décrit les étapes à suivre pour mettre à jour les détails du compte de destination à l’aide de l’interface utilisateur Experience Platform.

Vous pouvez mettre à jour les détails du compte de destination afin d’actualiser et de réauthentifier les informations d’identification de vos comptes actuels ou expirés pour les destinations que vous utilisez actuellement. En règle générale, les jetons OAuth et porteur ont une durée de vie limitée, selon la plateforme de destination. Lorsque ces jetons expirent, vous pouvez les actualiser dans le workflow décrit ci-dessous. Ce workflow vous invite à passer par le workflow OAuth ou à réinsérer un jeton. De même, si un mot de passe ou un accès utilisateur a changé sur la plateforme en aval, vous pouvez actualiser les informations d’identification.

Pour les destinations par lot, vous pouvez mettre à jour la clé d’accès ou secrète, si l’une d’elles a été modifiée. En outre, si vous souhaitez chiffrer vos fichiers à partir de maintenant, vous pouvez insérer une clé publique RSA et vos fichiers exportés seront chiffrés à partir de maintenant.

![Onglet Comptes](../assets/ui/update-accounts/destination-accounts.png)

## Mettre à jour des comptes {#update}

Suivez les étapes ci-dessous pour mettre à jour les détails de connexion vers les destinations existantes.

1. Connectez-vous à l’[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionnez **[!UICONTROL Comptes]** dans l’en-tête supérieur pour afficher vos comptes existants.

   ![Onglet Comptes](../assets/ui/update-accounts/accounts-tab.png)

2. Sélectionnez l’icône filtre ![Icône Filtre](/help/images/icons/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de comptes associés aux destinations sélectionnées.

   ![Filtrer les comptes de destination](../assets/ui/update-accounts/filter-accounts.png)

3. Sélectionnez les points de suspension (`...`) en regard du nom du compte que vous avez l’intention de mettre à jour. Un panneau contextuel s’affiche, fournissant des options pour **[!UICONTROL Activer les audiences]**, **[!UICONTROL Modifier les détails]** et **[!UICONTROL Supprimer]** du compte. Sélectionnez le bouton ![Modifier les détails](/help/images/icons/edit.png) **[!UICONTROL Modifier les détails]** pour modifier les informations du compte.

   ![Modifier le compte](../assets/ui/update-accounts/accounts-edit.png)

4. Entrez vos informations d’identification de compte mises à jour.

   * Pour les comptes qui utilisent un type de connexion `OAuth1` ou `OAuth2`, sélectionnez **[!UICONTROL Reconnecter OAuth]** pour renouveler les informations d’identification de votre compte. Vous pouvez également mettre à jour le nom et la description de votre compte.

   ![Modifier les détails OAuth](../assets/ui/update-accounts/edit-details-oauth.png)

   * Pour les comptes qui utilisent un type de connexion `Access Key` ou `ConnectionString`, vous pouvez modifier les informations d’authentification de votre compte, y compris les informations telles que l’identifiant d’accès, les clés secrètes ou les chaînes de connexion. Vous pouvez également mettre à jour le nom et la description de votre compte.

   ![Modifier la clé d’accès des détails](../assets/ui/update-accounts/edit-details-key.png)

   * Pour les comptes qui utilisent un type de connexion `Bearer token`, vous pouvez saisir un nouveau jeton porteur, si nécessaire. Vous pouvez également mettre à jour le nom et la description de votre compte.

   ![Modifier les détails Jeton de porteur](../assets/ui/update-accounts/edit-details-bearer.png)

   * Pour les comptes qui utilisent un type de connexion `Server to server`, vous pouvez mettre à jour le nom et la description de votre compte.

   ![Modifier les détails Serveur à serveur](../assets/ui/update-accounts/edit-details-s2s.png)

5. Sélectionnez **[!UICONTROL Enregistrer]** pour terminer la mise à jour des détails du compte.

## Étapes suivantes

En suivant ce tutoriel, vous avez utilisé l’espace de travail **[!UICONTROL destinations]** pour mettre à jour les comptes existants.

Pour plus d’informations sur les destinations, consultez la [présentation des destinations](../catalog/overview.md).