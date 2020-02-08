---
title: Espace de travail Destinations
seo-title: Espace de travail Destinations
description: Dans la plateforme de données clientes Adobe en temps réel, sélectionnez Destinations dans la barre de navigation de gauche pour accéder à l’espace de travail des destinations.
seo-description: Dans la plateforme de données clientes Adobe en temps réel, sélectionnez Destinations dans la barre de navigation de gauche pour accéder à l’espace de travail des destinations.
translation-type: tm+mt
source-git-commit: 132bc9787a86045adba559c769b02927a6045b17

---


# Espace de travail Destinations {#destinations-workspace}

Dans la plateforme de données clientes Adobe en temps réel, sélectionnez **Destinations** dans la barre de navigation de gauche pour accéder à l’espace de travail Destinations.

L’espace de travail Destinations se compose de quatre sections : **Catalogue**, **Parcourir**, **Comptes** et Flux de **données, qui sont décrites dans les sections ci-dessous.**

![Destinations-présentation](/help/rtcdp/destinations/assets/destinations-overview.png)

## Catalog (Catalogue){#catalog}

L’onglet **[!UICONTROL Catalogue]** affiche la liste de toutes les destinations proposées par Adobe, auxquelles vous pouvez envoyer des données. Sélectionnez une destination dans le catalogue pour ouvrir le rail droit. Ici, vous pouvez configurer une connexion à la destination (destination **** Connect) ou en savoir plus sur chaque destination en consultant la documentation (**Afficher la documentation**).

![Options de catalogue de destination](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Pour plus d’informations sur les catégories de destination et les informations sur chaque destination, voir Catalogue [de](/help/rtcdp/destinations/destinations-catalog.md)destination.

## Parcourir {#browse}

L’onglet **[!UICONTROL Parcourir]** affiche les destinations avec lesquelles vous avez établi une connexion. Les destinations pour lesquelles l’option d’activation est activée définissent la destination comme étant active et inversement. Vous pouvez également afficher les destinations où circulent les données en sélectionnant **Segments > Parcourir** et en sélectionnant un segment à inspecter. Consultez le tableau ci-dessous pour toutes les informations fournies pour chaque destination dans l’onglet Parcourir :

![Onglet Parcourir](/help/rtcdp/destinations/assets/browse-tab.png)

| Élément | Description |
---------|----------
| Nom de la destination | Le nom que vous avez fourni pour votre flux d’activation vers cette destination. |
| Destination | Plateforme de destination que vous avez sélectionnée pour votre flux d’activation. |
| Créés | date et heure UTC de création du flux d’activation vers la destination. |
| Type de connexion | *Pour les destinations de marketing par courrier électronique uniquement*. Représente le type de connexion à votre compartiment de stockage. Peut être S3 ou FTP. |
| Nom d’utilisateur | Informations d’identification de compte que vous avez sélectionnées pour le flux de destination. |
| Segments | Nombre de segments activés pour cette destination. |
| État | `Active` ou `Inactive`. Indique si les données sont actuellement activées pour cette destination. Pour modifier l’état, voir [Désactivation de l’activation](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Cliquez sur une ligne de destination pour afficher plus d’informations sur la destination dans le rail droit.

![Ligne de destination du clic](/help/rtcdp/destinations/assets/click-destination-row.png)

Sélectionnez le nom de destination pour afficher des informations sur les segments activés pour cette destination. Cliquez sur **[!UICONTROL Modifier l’activation]** pour modifier ou ajouter les segments envoyés vers cette destination.

## Comptes {#accounts}

Dans l’onglet **[!UICONTROL Comptes]** , vous pouvez en savoir plus sur les connexions que vous avez établies avec différentes destinations. Consultez le tableau ci-dessous pour obtenir toutes les informations disponibles sur chaque destination :

![Onglet Comptes](/help/rtcdp/destinations/assets/accounts-tab.png)

| Élément | Description |
---------|----------
| Plateforme | Destination pour laquelle vous avez configuré la connexion. |
| Nom d’utilisateur | Nom d’utilisateur que vous avez sélectionné dans l’assistant [de](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)connexion de destination. |
| Flux | Représente le nombre de flux de destination réussis uniques liés aux informations de base créées pour une destination. |
| Autorisé | date à laquelle la connexion à cette destination a été autorisée. |

## Flux de données {#data-flows}

L’onglet Flux **[!UICONTROL de]** données affiche une représentation graphique des flux d’activation que vous avez configurés dans la plateforme de données clientes en temps réel.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Sélectionnez l’une des destinations affichées sur la page et appuyez sur **[!UICONTROL Afficher les flux]** pour afficher les informations sur tous les flux de données que vous avez configurés pour chaque destination.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)