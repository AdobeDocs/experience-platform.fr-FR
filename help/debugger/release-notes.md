---
title: Notes de mise à jour de Adobe Experience Platform Debugger
description: Dernières notes de mise à jour pour Adobe Experience Platform Debugger.
keywords: debugger;extension Experience Platform Debugger;chrome;extension;notes de mise à jour
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 5%

---

# Notes de mise à jour de Adobe Experience Platform Debugger

## Version 1.4.0 - 3 octobre 2022

* Ajout de la prise en charge du débogage AEP Assurance pour les mises en oeuvre hybrides du SDK Web.
* Ajout de la prise en charge de plusieurs onglets dans la même session AEP Assurance.
* Correction d’un problème en raison duquel les utilisateurs ne pouvaient pas changer de profil/d’organisation après connexion.
   * Pour certains comptes, il est nécessaire de se déconnecter et de se reconnecter pour changer d’entreprise.
* Ajout d’un message d’erreur lors de l’échec de l’activation de Target Trace.
* Mise à jour des dépendances.

## Version 1.3.3 - 20 juin 2022

* Correction d’un problème qui empêchait l’ouverture de fenêtres contextuelles à partir de tableaux d’événements réseau.
* Correction d’un problème qui empêchait le chargement des informations Alloy sur la page.

## Version 1.3.2 - 9 juin 2022

* Ajout d’un avatar par défaut lorsque l’utilisateur est connecté.
* Ajout d’un surlignage de la syntaxe aux objets JSON dans les journaux.

## Version 1.3.1 - 24 mai 2022

* Mise à jour des dépendances.
* Correction d’un problème d’Analytics en raison duquel les accès de post-traitement ne pouvaient pas être activés.
* Correction d’un problème en raison duquel le débogueur se joignait à la fenêtre de connexion de l’Adobe.
* Correction d’un problème d’AT.js en raison duquel les messages du journal ne s’affichaient pas dans Debugger.

## Version 1.3.0, - 28 janvier 2022

* Ajout du lien À propos pour afficher la version actuelle et les notes de mise à jour.
* Ajout d’un bouton d’activation/désactivation pour afficher les accès post-traités pour les requêtes Analytics. Le bouton bascule est disponible dans la section Analytics .
* Correction d’un problème de session de débogage à distance lorsque la session était fermée en dehors du débogueur.
* Correction d’une notification d’erreur visible dans l’onglet Transactions Edge du SDK Web.
* Correction d’un problème lié aux balises d’Adobe dans l’avertissement d’obsolescence de la page lorsque le débogueur accédait à l’objet _satellite.
* Correction de certains cas où une instance AppMeasurement était introuvable sur la page.
* Correction d’un problème de connexion à la page qui se produisait lors de la première ouverture de la fenêtre du débogueur.

## Version 1.2.0 - 26 octobre 2021

* Affichez les événements de tous les onglets du navigateur dans la vue réseau. Pour afficher uniquement les événements de l’onglet actif, sélectionnez l’icône de verrouillage dans le coin inférieur droit du débogueur.
* Mise à jour de la valorisation de marque.

## Version 1.1.0 - 5 octobre 2021

* Visualisation du débogage à distance : Organisez les événements de débogage à distance dans un diagramme de flux visuel dans la section SDK web Adobe Experience Platform > Transactions Edge .
* L’organisation du SDK Web Adobe Experience Platform utilisée sur la page doit correspondre à l’organisation connectée lors du démarrage d’une nouvelle session de débogage à distance.
* Affiche uniquement les transactions de périphérie pour l’onglet connecté. Les journaux de suivi de Target sont toujours disponibles dans la section Journaux > Edge .
* Autorisez le remplacement de la configuration de l’ID de flux de données distinct pour chaque instance du SDK Web Adobe Experience Platform sur la page. Ajoutez le bouton bascule debug enabled .
* Correction d’un problème en raison duquel le jeton de trace Adobe Target n’était pas toujours envoyé avec les sessions de débogage à distance pour le SDK Web de Adobe Experience Platform.

## Version 1.0.0 5 mai 2021

* Première version principale du débogueur Experience Platform. Destiné à remplacer l’Experience Cloud Debugger.
