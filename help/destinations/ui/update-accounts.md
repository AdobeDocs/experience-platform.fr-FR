---
keywords: Mettre à jour le compte de destination,Comptes de destination
title: Mettre à jour les comptes de destination
type: Tutoriel
description: Ce didacticiel liste les étapes de mise à jour des comptes de destination dans l’interface utilisateur de Adobe Experience Platform.
exl-id: afb41878-4205-4c64-af4d-e2740f852785
translation-type: tm+mt
source-git-commit: 07869d63f395bbab6c49a3976051facdf94d43b7
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 36%

---

# Mettre à jour les comptes de destination

## Présentation {#overview}

L&#39;onglet **[!UICONTROL Comptes]** affiche des détails sur les connexions que vous avez établies avec différentes destinations. Consultez le tableau ci-dessous pour obtenir toutes les informations disponibles sur chaque destination :

![Onglet Comptes](../assets/ui/update-accounts/destination-accounts.png)

| Élément | Description |
|---|---|
| [!UICONTROL Plateforme] | La destination pour laquelle vous avez configuré la connexion. |
| [!UICONTROL Type de connexion] | Représente le type de connexion à votre compartiment de stockage ou à votre destination. <ul><li>Pour les destinations de marketing par e-mail : peut être S3 ou FTP.</li><li>Pour les destinations publicitaires en temps réel : serveur à serveur</li><li>Pour les destinations de stockage dans le cloud Amazon S3 : clé d’accès </li><li>Pour les destinations de stockage dans le cloud SFTP : authentification de base pour SFTP</li></ul> |
| [!UICONTROL Nom d’utilisateur] | Le nom d’utilisateur que vous avez sélectionné dans l’[assistant de connexion à la destination](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinations] | Représente le nombre de flux de destination réussis uniques et connectés avec des informations de base créées pour une destination. |
| [!UICONTROL Autorisé] | La date à laquelle la connexion à cette destination a été autorisée. |

## Mettre à jour les comptes {#update}

Suivez les étapes ci-dessous pour mettre à jour les détails de connexion vers les destinations existantes.

1. Connectez-vous à l&#39;[interface utilisateur Experience Platform](https://platform.adobe.com/) et sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche. Sélectionnez **[!UICONTROL Comptes]** dans l&#39;en-tête supérieur pour vue de vos comptes existants.

   ![Onglet Comptes](../assets/ui/update-accounts/accounts-tab.png)

2. Sélectionnez l’icône de filtre ![Icône de filtre](../assets/ui/update-accounts/filter.png) en haut à gauche pour lancer le panneau de tri. Le panneau de tri fournit une liste de toutes vos destinations. Vous pouvez sélectionner plusieurs destinations dans la liste pour afficher une sélection filtrée de comptes associés aux destinations sélectionnées.

   ![Filtrer les destinations](../assets/ui/update-accounts/filter-accounts.png)

3. Sélectionnez le bouton ![Modifier le compte](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Modifier]** dans la colonne **[!UICONTROL Plateforme]** pour modifier les informations du compte.

   ![Onglet Comptes](../assets/ui/update-accounts/accounts-edit.png)

4. Entrez vos informations d’identification de compte mises à jour.

   * Pour les comptes qui utilisent un type de connexion `OAuth2`, sélectionnez **[!UICONTROL Reconnecter OAuth]** pour renouveler les informations d&#39;identification de votre compte.

      ![Modifier les détails OAuth](../assets/ui/update-accounts/edit-details-oauth.png)


   * Pour les comptes qui utilisent un type de connexion `Access Key` ou `ConnectionString`, vous pouvez modifier les informations d&#39;authentification de votre compte, y compris les informations telles que l&#39;ID d&#39;accès, les clés secrètes ou les chaînes de connexion.

      ![Modifier la clé d&#39;accès de détails](../assets/ui/update-accounts/edit-details-key.png)

5. Sélectionnez **[!UICONTROL Enregistrer]** pour terminer la mise à jour des informations d’identification.
