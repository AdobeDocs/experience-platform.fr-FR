---
title: Espace de travail des destinations
seo-title: Espace de travail des destinations
description: Dans la plateforme de données client en temps réel Adobe, sélectionnez Destinations dans la barre de navigation de gauche pour accéder à l’espace de travail des destinations.
seo-description: Dans la plateforme de données client en temps réel Adobe, sélectionnez Destinations dans la barre de navigation de gauche pour accéder à l’espace de travail des destinations.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 66%

---


# Espace de travail des destinations {#destinations-workspace}

Dans la plateforme de données client en temps réel Adobe, sélectionnez **[!UICONTROL Destinations]** dans la barre de navigation de gauche pour accéder à l’espace de travail des destinations.

The [!UICONTROL Destinations] workspace consists of four sections, **[!UICONTROL Catalog]**, **[!UICONTROL Browse]**, **[!UICONTROL Accounts]**, and **[!UICONTROL System View]**, which are described in the sections below.

![Destinations-overview](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catalogue] {#catalog}

L’onglet **[!UICONTROL Catalogue]** affiche une liste de toutes les destinations proposées par Adobe, auxquelles vous pouvez envoyer des données.

Utilisez la fonctionnalité de recherche de la page pour localiser une destination spécifique ou filtrer les destinations à l&#39;aide du contrôle **[!UICONTROL Catégories]** .

Sélectionnez une destination dans le catalogue pour ouvrir le rail de droite. Here, you can set up a connection to the destination (**[!UICONTROL Connect destination]**), view existing destination connections (**[!UICONTROL Browse destinations]**) or learn more detailed information about each destination by viewing the documentation (**[!UICONTROL View documentation]**).

![Options du catalogue des destinations](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Pour plus d’informations sur les catégories de destination et sur chaque destination, consultez [Catalogue des destinations](/help/rtcdp/destinations/destinations-catalog.md).

## [!UICONTROL Parcourir] {#browse}

L’onglet **[!UICONTROL Parcourir]** affiche les destinations avec lesquelles vous avez établi une connexion. Destinations with the **[!UICONTROL enabled]** toggle turned on set the destination to active and vice-versa. Vous pouvez également consulter les destinations où les données circulent en sélectionnant **[!UICONTROL Segments > Parcourir]** et en sélectionnant un segment à inspecter. Consultez le tableau ci-dessous pour toutes les informations fournies pour chaque destination dans l’onglet Parcourir :

![Onglet Parcourir](/help/rtcdp/destinations/assets/browse-tab.png)

| Élément | Description |
---------|----------
| Nom | Le nom que vous avez fourni pour votre flux d’activation vers cette destination. |
| [!UICONTROL Destination] | La plateforme de destination que vous avez sélectionnée pour votre flux d’activation. |
| [!UICONTROL Type de connexion] | Représente le type de connexion au compartiment ou à la destination de votre enregistrement. <ul><li>Pour les destinations de marketing par courriel : Peut être S3 ou FTP.</li><li>Pour les destinations publicitaires en temps réel : Serveur à serveur</li></ul> |
| [!UICONTROL Nom d’utilisateur] | Les informations d’identification de compte que vous avez sélectionnées pour le flux de destination. |
| [!UICONTROL Segments] | Le nombre de segments activés pour cette destination. |
| [!UICONTROL Créé] | La date et l’heure (UTC) de création du flux d’activation vers la destination. |
| [!UICONTROL État] | `Active` ou `Inactive`. Indique si les données sont actuellement activées vers cette destination. Pour modifier le statut, consultez [Désactiver l’activation](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Cliquez sur une ligne de destination pour afficher plus d’informations sur la destination dans le rail de droite.

![Cliquer sur la ligne de destination](/help/rtcdp/destinations/assets/click-destination-row.png)

Sélectionnez le nom de la destination pour afficher des informations sur les segments activés vers cette destination. Cliquez sur **[!UICONTROL Modifier l’activation]** pour modifier ou ajouter les segments envoyés vers cette destination.

## [!UICONTROL Comptes] {#accounts}

Dans l’onglet **[!UICONTROL Comptes]**, vous pouvez en savoir plus sur les connexions que vous avez établies avec différentes destinations. Consultez le tableau ci-dessous pour obtenir toutes les informations disponibles sur chaque destination :

![Onglet Comptes](/help/rtcdp/destinations/assets/accounts-tab.png)

| Élément | Description |
---------|----------
| [!UICONTROL Plateforme] | La destination pour laquelle vous avez configuré la connexion. |
| [!UICONTROL Type de connexion] | Représente le type de connexion au compartiment ou à la destination de votre enregistrement. <ul><li>Pour les destinations de marketing par courriel : Peut être S3 ou FTP.</li><li>Pour les destinations publicitaires en temps réel : Serveur à serveur</li><li>Pour les destinations d’enregistrement cloud Amazon S3 : Clé d&#39;accès </li><li>Pour les destinations d’enregistrement cloud SFTP : Authentification de base pour SFTP</li></ul> |
| [!UICONTROL Nom d’utilisateur] | Le nom d’utilisateur que vous avez sélectionné dans l’[assistant de connexion à la destination](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination). |
| [!UICONTROL Flux de données] | Représente le nombre de flux de destination réussis uniques et connectés avec des informations de base créées pour une destination. |
| [!UICONTROL Autorisé] | La date à laquelle la connexion à cette destination a été autorisée. |
| [!UICONTROL État] | `Active` ou `Inactive`. Indique si les données sont actuellement activées vers cette destination. Pour modifier le statut, consultez [Désactiver l’activation](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

## [!UICONTROL Vue système] {#system-view}

The **[!UICONTROL System View]** tab displays a graphic representation of the activation flows that you have set up in the Real-time Customer Data Platform.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Select any of the destinations displayed on the page and press **[!UICONTROL View flows]** to see information on all the connections you have set up for each destination.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)