---
title: Page de détails des destinations
seo-title: Page de détails des destinations
description: 'La page de détails d’une destination individuelle offre un aperçu des détails de la destination, tels que le nom de destination, l’identifiant, les segments mappés à la destination et les commandes permettant de modifier l’activation, d’activer et de désactiver le flux de données. '
seo-description: 'La page de détails d’une destination individuelle offre un aperçu des détails de la destination, tels que le nom de destination, l’identifiant, les segments mappés à la destination et les commandes permettant de modifier l’activation, d’activer et de désactiver le flux de données. '
translation-type: tm+mt
source-git-commit: b784b67092ea8d30ad00cda9a40779b3890862fd

---


# Page de détails des destinations {#destinations-details-page}

La page de détails d’une destination individuelle offre un aperçu des détails de la destination, tels que le nom de destination, l’identifiant, les segments mappés à la destination et les commandes permettant de modifier l’activation, d’activer et de désactiver le flux de données. Pour afficher ces détails, accédez à **Destinations** > **Parcourir** et cliquez sur le nom de la destination à utiliser.

Les composants principaux d’une destination individuelle sont les suivants :

* 1 - Nom et identifiant de la destination
* 2 - Segments activés vers la destination
* 3 - Informations sur le rail de droite
* 4 - Commandes permettant de modifier l’activation et d’activer/désactiver le flux de données

![Page de destinations numérotée](/help/rtcdp/destinations/assets/destination-page-numbered.png)

Accédez à une page de destination individuelle pour obtenir un aperçu des détails de destination suivants :

## 1. Nom et identifiant de la destination

Vous pouvez consulter le nom de la destination dans le titre de la page et l’identifiant de la destination dans l’URL de la page.

## 2. Segments activés vers la destination

Cette section affiche les segments qui sont actuellement mappés à la destination, ainsi que des informations supplémentaires sur ces segments. Pour plus d’informations, consultez le tableau ci-dessous :

| Élément | Description |
---------|----------|
| Nom du segment | Le nom du segment. |
| Description du segment | La description du segment. |
| Date de début | La date à laquelle ces segments sont activés vers la destination. |
| Date de fin | La date à laquelle ces segments ne sont plus activés vers la destination. |
| ID de mappage | *Non disponible pour les destinations de marketing par e-mail*. Indique l’identifiant sous lequel le segment est connu dans la plateforme de destination. |

## 3. Informations sur le rail de droite

Le rail de droite contient des informations sur la destination. Pour plus d’informations, consultez le tableau ci-dessous :

| Élément | Description |
---------|----------|
| Plateforme | Représente la plateforme de destination vers laquelle les audiences sont envoyées. Pour plus d’informations, consultez le [catalogue des destinations](/help/rtcdp/destinations/destinations-catalog.md). |
| Description | Vous pouvez modifier la description du flux de destination. |
| Catégorie | Indique le type de destination. Pour plus d’informations, consultez le [catalogue des destinations](/help/rtcdp/destinations/destinations-catalog.md). |
| Type de connexion | Indique la forme sous laquelle vos audiences sont envoyées vers la destination. Il peut s’agir d’un **cookie** ou d’un **profil**. |
| Fréquence | Indique la fréquence d’envoi des audiences vers la destination. Il peut s’agir d’un **flux continu** ou d’un **lot**. |
| Identité | Représente l’espace de noms d’identité accepté par la destination. Par exemple, le champ Identité peut correspondre à GAID, IDFA ou un e-mail. Pour tous les espaces de noms d’identité acceptés, consultez les espaces de noms standard dans la [présentation de l’espace de noms d’identité](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md). |
| Créé par | Indique l’utilisateur qui a créé ce flux de destination. |
| Créé | Indique la date et l’heure (UTC) de création de ce flux de destination. |

## 4. Commandes permettant de modifier l’activation et d’activer/désactiver le flux de données

La commande Modifier l’activation permet de modifier les segments qui sont mappés à la destination. Appuyez sur Modifier l’activation pour ouvrir le [workflow d’activation du segment](/help/rtcdp/destinations/activate-destinations.md).

Utilisez le bouton **Activer/désactiver** pour démarrer et suspendre l’exportation des données vers une destination.