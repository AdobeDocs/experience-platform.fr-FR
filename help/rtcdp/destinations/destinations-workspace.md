---
title: Espace de travail des destinations
seo-title: Espace de travail des destinations
description: Dans la plateforme de données client en temps réel Adobe, sélectionnez Destinations dans la barre de navigation de gauche pour accéder à l’espace de travail des destinations.
seo-description: Dans la plateforme de données client en temps réel Adobe, sélectionnez Destinations dans la barre de navigation de gauche pour accéder à l’espace de travail des destinations.
translation-type: tm+mt
source-git-commit: e87ddff936da88b1b2b3cf71c2d6c24ed28b39ab

---


# Espace de travail des destinations {#destinations-workspace}

Dans la plateforme de données client en temps réel Adobe, sélectionnez **Destinations** dans la barre de navigation de gauche pour accéder à l’espace de travail des destinations.

The Destinations workspace consists of four sections, **Catalog**, **Browse**, **Accounts**, and **System View**, which are described in the sections below.

![Destinations-overview](/help/rtcdp/destinations/assets/destinations-overview.png)

## Catalogue {#catalog}

The **[!UICONTROL Catalog]** tab displays a list of all destinations offered by Adobe, that you can send data to.

Utilisez la fonctionnalité de recherche de la page pour localiser une destination spécifique ou filtrer les destinations à l’aide du **[!UICONTROL Categories]** contrôle.

Sélectionnez une destination dans le catalogue pour ouvrir le rail de droite. Here, you can set up a connection to the destination (**Connect destination**), view existing destination connections (**Browse destinations**) or learn more detailed information about each destination by viewing the documentation (**View documentation**).

![Options du catalogue des destinations](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Pour plus d’informations sur les catégories de destination et sur chaque destination, consultez [Catalogue des destinations](/help/rtcdp/destinations/destinations-catalog.md).

## Parcourir {#browse}

The **[!UICONTROL Browse]** tab displays the destinations with which you have established a connection. Destinations with the **enabled** toggle turned on set the destination to active and vice-versa. Vous pouvez également consulter les destinations où les données circulent en sélectionnant **Segments > Parcourir** et en sélectionnant un segment à inspecter. Consultez le tableau ci-dessous pour toutes les informations fournies pour chaque destination dans l’onglet Parcourir :

![Onglet Parcourir](/help/rtcdp/destinations/assets/browse-tab.png)

| Elément | Description |
---------|----------
| Nom | Le nom que vous avez fourni pour votre flux d’activation vers cette destination. |
| Destination | La plateforme de destination que vous avez sélectionnée pour votre flux d’activation. |
| Type de connexion | Représente le type de connexion à votre  de  ou à votre destination. <ul><li>Pour les destinations de marketing par courrier électronique : Peut être S3 ou FTP.</li><li>Pour les destinations publicitaires en temps réel : Serveur à serveur</li></ul> |
| Nom d’utilisateur | Les informations d’identification de compte que vous avez sélectionnées pour le flux de destination. |
| Segments | Le nombre de segments activés pour cette destination. |
| Créé | La date et l’heure (UTC) de création du flux d’activation vers la destination. |
| Statut | `Active` ou `Inactive`. Indique si les données sont actuellement activées vers cette destination. Pour modifier le statut, consultez [Désactiver l’activation](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Cliquez sur une ligne de destination pour afficher plus d’informations sur la destination dans le rail de droite.

![Cliquer sur la ligne de destination](/help/rtcdp/destinations/assets/click-destination-row.png)

Sélectionnez le nom de la destination pour afficher des informations sur les segments activés vers cette destination. Click **[!UICONTROL Edit activation]** to modify or add to the segments that are being sent to this destination.

## Comptes {#accounts}

In the **[!UICONTROL Accounts]** tab, you can learn more about the connections that you have established with various destinations. Consultez le tableau ci-dessous pour obtenir toutes les informations disponibles sur chaque destination :

![Onglet Comptes](/help/rtcdp/destinations/assets/accounts-tab.png)

| Elément | Description |
---------|----------
| Plateforme | La destination pour laquelle vous avez configuré la connexion. |
| Type de connexion | Représente le type de connexion à votre  de  ou à votre destination. <ul><li>Pour les destinations de marketing par courrier électronique : Peut être S3 ou FTP.</li><li>Pour les destinations publicitaires en temps réel : Serveur à serveur</li><li>Pour Amazon S3 Cloud  des destinations  : Clé d&#39;accès </li><li>Pour le cloud SFTP   destinations de : Authentification de base pour SFTP</li></ul> |
| Nom d’utilisateur | Le nom d’utilisateur que vous avez sélectionné dans l’[assistant de connexion à la destination](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination). |
| Flux de données | Représente le nombre de flux de destination réussis uniques et connectés avec des informations de base créées pour une destination. |
| Autorisé | La date à laquelle la connexion à cette destination a été autorisée. |
| Statut | `Active` ou `Inactive`. Indique si les données sont actuellement activées vers cette destination. Pour modifier le statut, consultez [Désactiver l’activation](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

##  système {#system-view}

The **[!UICONTROL System View]** tab displays a graphic representation of the activation flows that you have set up in the Real-time Customer Data Platform.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Select any of the destinations displayed on the page and press **[!UICONTROL View flows]** to see information on all the connections you have set up for each destination.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)