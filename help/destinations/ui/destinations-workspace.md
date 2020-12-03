---
keywords: RTCDP;rtcdp
title: Espace de travail des destinations
seo-title: Espace de travail des destinations
description: 'L’espace de travail Destinations se compose de quatre sections : Catalogue, Parcourir, Comptes et Vue du système, décrites dans les sections ci-dessous.'
seo-description: Dans la plateforme de données client en temps réel , sélectionnez Destinations dans la barre de navigation de gauche pour accéder à l’espace de travail des destinations.
translation-type: tm+mt
source-git-commit: 5f120a716cc3396ef7749463bb6052a8ced2fbb4
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 51%

---


# Espace de travail des destinations {#destinations-workspace}

Dans la plateforme de données client en temps réel , sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche pour accéder à l’espace de travail des destinations.

L’espace de travail [!UICONTROL Destinations] se compose de quatre sections : [!UICONTROL Catalogue], [!UICONTROL Parcourir], [!UICONTROL Comptes] et [!UICONTROL Vue du système], décrites dans les sections ci-dessous.

![Présentation des destinations](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Catalogue] {#catalog}

The **[!UICONTROL Catalog]** tab displays a list of all destinations available in Real-time CDP, that you can send data to.

L’interface utilisateur CDP en temps réel fournit un certain nombre d’options de recherche et de filtrage sur la page de catalogue de destinations :

* Utilisez la fonctionnalité de recherche de la page pour localiser une destination spécifique.
* Filtrez les destinations à l’aide du contrôle [!UICONTROL Catégories] .
* Basculez entre [!UICONTROL Toutes les destinations] et [!UICONTROL Mes destinations]. Lorsque **[!UICONTROL Toutes les destinations]** sont sélectionnées, toutes les destinations CDP disponibles en temps réel s’affichent. Lorsque **[!UICONTROL Mes destinations]** est sélectionné, vous ne pouvez voir que les destinations avec lesquelles vous avez établi une connexion.
* Sélectionnez vue **[!UICONTROL Connections]** et/ou **[!UICONTROL Extensions]**. Pour comprendre la différence entre les deux catégories, voir Types et Catégories [de](../destination-types.md)destination.

![destinations filtrage et démonstration de recherche](../assets/ui/workspace/destinations-search-and-filter.gif)

Les cartes de destination contiennent un contrôle **[!UICONTROL Configurer]** ou **[!UICONTROL Activer]** , et un contrôle secondaire qui affiche d&#39;autres options. Ils sont tous décrits ci-dessous :

| Contrôle | Description |
---------|----------
| [!UICONTROL Configuration] | Permet de créer une connexion à la destination. |
| [!UICONTROL Activer] | Une fois que vous avez établi une connexion à la destination, vous pouvez activer des segments. |
| [!UICONTROL Compte vue] | Vue des comptes que vous avez connectés pour une destination. |
| [!UICONTROL Flux de données de vue] | Vue des flux d’activation de données qui existent pour une destination. |
| [!UICONTROL Documentation sur la vue] | Ouvre un lien vers la page de documentation de cette destination spécifique, pour plus d’informations et pour vous aider à la configurer. |

![Contrôles sur la carte de destination](../assets/ui/workspace/destination-card-options.png)

Sélectionnez une carte de destination dans le catalogue pour ouvrir le rail de droite.  Vous pouvez voir ici une description de la destination. Le rail droit fournit les mêmes commandes que celles décrites dans le tableau ci-dessus, ainsi qu&#39;une description de la destination et une indication de la catégorie et du type de destination.

![Options du catalogue des destinations](../assets/ui/workspace/destination-right-rail.png)

Pour plus d&#39;informations sur les catégories de destination et sur chaque destination, consultez le catalogue [de](../catalog/overview.md) destination et les types et Catégories [de](../destination-types.md)destination.

## [!UICONTROL Comptes] {#accounts}

Dans l’onglet **[!UICONTROL Comptes]**, vous pouvez en savoir plus sur les connexions que vous avez établies avec différentes destinations. Consultez le tableau ci-dessous pour obtenir toutes les informations disponibles sur chaque destination :

>[!TIP]
>
>Utilisez le bouton ![](../assets/ui/workspace/add-data-symbol.png) Ajouter les données de la colonne **[!UICONTROL Plateforme]** pour créer une nouvelle connexion de destination pour ce compte.

![Onglet Comptes](../assets/ui/workspace/edit-account-destinations.png)

| Élément | Description |
---------|----------
| [!UICONTROL Plateforme] | La destination pour laquelle vous avez configuré la connexion. |
| [!UICONTROL Type de connexion] | Représente le type de connexion à votre compartiment de stockage ou à votre destination. <ul><li>Pour les destinations de marketing par e-mail : peut être S3 ou FTP.</li><li>Pour les destinations publicitaires en temps réel : serveur à serveur</li><li>Pour les destinations de stockage dans le cloud Amazon S3 : clé d’accès </li><li>Pour les destinations de stockage dans le cloud SFTP : authentification de base pour SFTP</li></ul> |
| [!UICONTROL Nom d’utilisateur] | Le nom d’utilisateur que vous avez sélectionné dans l’[assistant de connexion à la destination](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinations] | Représente le nombre de flux de destination réussis uniques et connectés avec des informations de base créées pour une destination. |
| [!UICONTROL Autorisé] | La date à laquelle la connexion à cette destination a été autorisée. |

De plus, vous pouvez modifier ou mettre à jour les informations de votre compte. Sélectionnez le bouton ![](../assets/ui/workspace/pencil-icon.png) Modifier le compte dans la colonne **[!UICONTROL Plateforme]** pour modifier les informations du compte.

Pour les comptes qui utilisent un type de `OAuth2` connexion, vous pouvez sélectionner **[!UICONTROL Reconnecter OAuth]** pour renouveler vos informations d’identification de compte.

![Image Oauth](../assets/ui/workspace/reconnect-oauth.png)

Pour les comptes qui utilisent un type `Access Key` ou `ConnectionString` de connexion, vous pouvez modifier les informations d’authentification de votre compte, y compris les informations telles que l’ID d’accès, les clés secrètes ou les chaînes de connexion.

![Image d’informations du compte](../assets/ui/workspace/edit-account-details.png)

Une fois que vous avez terminé de modifier les détails de votre compte, sélectionnez **[!UICONTROL Enregistrer]** pour terminer la mise à jour.

## [!UICONTROL Parcourir] {#browse}

L’onglet **[!UICONTROL Parcourir]** affiche les destinations avec lesquelles vous avez établi une connexion. Destinations with the **[!UICONTROL Enabled]** toggle turned on set the destination to active and vice-versa. You can also view the destinations where you have data flowing by selecting **[!UICONTROL Segments]** > **[!UICONTROL Browse]** and selecting a segment to inspect. Consultez le tableau ci-dessous pour toutes les informations fournies pour chaque destination dans l’onglet Parcourir :

>[!TIP]
>
>Utilisez le bouton ![](../assets/ui/workspace/add-data-symbol.png) Ajouter les données de la colonne **[!UICONTROL Nom]** pour activer des segments supplémentaires vers cette destination.

![Onglet Parcourir](../assets/ui/workspace/browse-tab.png)

| Élément | Description |
---------|----------
| Nom | Le nom que vous avez fourni pour votre flux d’activation vers cette destination. |
| [!UICONTROL Destination] | La plateforme de destination que vous avez sélectionnée pour votre flux d’activation. |
| [!UICONTROL Type de connexion] | Représente le type de connexion à votre compartiment de stockage ou à votre destination. <ul><li>Pour les destinations de marketing par e-mail : peut être S3 ou FTP.</li><li>Pour les destinations publicitaires en temps réel : serveur à serveur</li></ul> |
| [!UICONTROL Nom d’utilisateur] | Les informations d’identification de compte que vous avez sélectionnées pour le flux de destination. |
| [!UICONTROL Segments] | Le nombre de segments activés pour cette destination. |
| [!UICONTROL Créé] | La date et l’heure (UTC) de création du flux d’activation vers la destination. |
| [!UICONTROL État] | `Active` ou `Inactive`. Indique si les données sont actuellement activées vers cette destination. Pour modifier le statut, consultez [Désactiver l’activation](./activate-destinations.md#disable-activation). |

Cliquez sur une ligne de destination pour afficher plus d’informations sur la destination dans le rail de droite.

![Cliquer sur la ligne de destination](../assets/ui/workspace/click-destination-row.png)

Sélectionnez le nom de la destination pour afficher des informations sur les segments activés vers cette destination. Cliquez sur **[!UICONTROL Modifier l’activation]** pour modifier ou ajouter les segments envoyés vers cette destination.

## [!UICONTROL Vue du système] {#system-view}

L’onglet **[!UICONTROL Vue du système]** affiche une représentation graphique des flux d’activation que vous avez configurés dans la plateforme de données clients en temps réel.

![Flux de données 1](../assets/ui/workspace/data-flows1.png)

Sélectionnez l’une des destinations affichées sur la page et appuyez sur **[!UICONTROL Afficher les flux]** pour afficher les informations sur toutes les connexions que vous avez configurées pour chaque destination.

![Flux de données 2](../assets/ui/workspace/data-flows2.png)