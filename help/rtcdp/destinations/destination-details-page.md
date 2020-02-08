---
title: Page Détails des destinations
seo-title: Page Détails des destinations
description: 'La page de détails d’une destination individuelle fournit un aperçu des détails de la destination, tels que le nom de destination, l’ID, les segments mappés à la destination et les contrôles permettant de modifier l’activation et d’activer et de désactiver le flux de données. '
seo-description: 'La page de détails d’une destination individuelle fournit un aperçu des détails de la destination, tels que le nom de destination, l’ID, les segments mappés à la destination et les contrôles permettant de modifier l’activation et d’activer et de désactiver le flux de données. '
translation-type: tm+mt
source-git-commit: b784b67092ea8d30ad00cda9a40779b3890862fd

---


# Page Détails de destination {#destinations-details-page}

La page de détails d’une destination individuelle fournit un aperçu des détails de la destination, tels que le nom de destination, l’ID, les segments mappés à la destination et les contrôles permettant de modifier l’activation et d’activer et de désactiver le flux de données. Pour afficher ces détails, accédez à **Destinations** > **Parcourir** et cliquez sur le nom de la destination à utiliser.

Les composants principaux d’une destination individuelle sont les suivants :

* 1 - Nom et ID de destination
* 2 - Segments activés pour la destination
* 3 - Informations sur le rail droit
* 4 - Commandes permettant de modifier l’activation et d’activer/désactiver le flux de données

![Page Destinations numérotée](/help/rtcdp/destinations/assets/destination-page-numbered.png)

Accédez à une page de destination individuelle pour obtenir un aperçu des détails de destination, tels que :

## 1. Nom et ID de destination

Vous pouvez voir le nom de destination dans le titre de la page et l’ID de destination dans l’URL de la page.

## 2. Segments activés sur la destination

Cette section présente les segments qui sont actuellement mappés à la destination, ainsi que des informations supplémentaires sur ces segments. Pour plus d’informations, voir le tableau ci-dessous :

| Élément | Description |
---------|----------|
| Nom du segment | Nom du segment. |
| Description du segment | Description de votre segment. |
| Date de début | date à laquelle ces segments sont activés vers la destination. |
| Date de fin | Date à laquelle ces segments ne seront plus activés vers la destination. |
| ID de mappage | *Non disponible pour les destinations* de marketing par courrier électronique. Indique l’ID par lequel le segment est connu dans la plateforme de destination. |

## 3. Informations sur le rail droit

Le rail droit contient des informations sur votre destination. Pour plus d’informations, voir le tableau ci-dessous :

| Élément | Description |
---------|----------|
| Plateforme | Représente la plateforme de destination à laquelle les audiences sont envoyées. Voir Catalogue [Destinations](/help/rtcdp/destinations/destinations-catalog.md) pour plus d’informations. |
| Description | Vous pouvez modifier la description de votre flux de destination. |
| Catégorie | Indique le type de destination. Voir Catalogue [Destinations](/help/rtcdp/destinations/destinations-catalog.md) pour plus d’informations. |
| Type de connexion | Indique dans quel formulaire vos audiences sont envoyées vers la destination. Peut être basé sur **un cookie** ou un **profil**. |
| Fréquence | Indique la fréquence d’envoi des audiences vers la destination. Peut être **Diffusion en flux continu** ou **Lot**. |
| Identité | Représente l’espace de noms d’identité accepté par la destination. Par exemple, le champ Identité peut être GAID, IDFA, email. Pour tous les espaces de noms d’identité acceptés, voir espaces de noms standard dans l’aperçu [de l’espace de noms](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md)Identity. |
| Créé par | Indique l’utilisateur qui a créé ce flux de destination. |
| Créés | Indique la date et l’heure UTC auxquelles ce flux de destination a été créé. |

## 4. Contrôles pour modifier l’activation et activer/désactiver le flux de données

Le contrôle Modifier l’activation permet de modifier les segments qui sont mappés à la destination. Appuyez sur Modifier l’activation pour ouvrir le processus [d’activation des](/help/rtcdp/destinations/activate-destinations.md)segments.

Utilisez la bascule **Activer/Désactiver** pour démarrer et mettre en pause l’exportation des données vers une destination.