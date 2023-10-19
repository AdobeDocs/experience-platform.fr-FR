---
title: Notes de mise à jour d’Adobe Experience Platform Debugger
description: Dernières notes de mise à jour pour Adobe Experience Platform Debugger.
keywords: debugger ; extension experience cloud debugger ; chrome ; extension ; notes de mise à jour
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: 70abe974aa7f94ea172d7ab90aacaf765b88de0e
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 82%

---

# Notes de mise à jour d’Adobe Experience Platform Debugger

## Version 1.5.0 - 19 octobre 2023

### Nouvelles fonctionnalités

* Affichez les liens vers la propriété, l’environnement et les règles dans le résumé et les journaux des balises.

### Correctifs et améliorations

* Correction d’un problème en raison duquel les données de résumé des balises n’étaient pas envoyées.
* Correction d’un problème en raison duquel les sessions d’assurance généraient une erreur CORS.
* Correction d’un problème qui empêchait l’affichage de Target Trace.
* Correction du bouton &quot;Envoyer un retour&quot;.
* Correction de l’absence de l’&quot;ID de flux de données&quot; dans le résumé du SDK Web pour la version ≥2.18.0.
* Correction d’un problème en raison duquel les journaux Edge ne pouvaient pas faire l’objet de recherches.
* Ajout d’une remarque concernant les profils supplémentaires pour certains types de compte.

## Version 1.4.1 - 1er novembre 2022

* Amélioration des performances sur les pages comportant de nombreux événements Adobe Experience Platform Assurance.

## Version 1.4.0 - 3 octobre 2022

* Ajout de la prise en charge du débogage AEP Assurance pour les implémentations hybrides du SDK web.
* Ajout de la prise en charge de plusieurs onglets dans la même session AEP Assurance.
* Correction d’un problème en raison duquel les utilisateurs et utilisatrices ne pouvaient pas changer de profil/d’organisation après connexion.
   * Pour certains comptes, il est nécessaire de se déconnecter et de se reconnecter pour changer d’organisation.
* Ajout d’un message d’erreur lors de l’échec de l’activation de Target Trace.
* Mise à jour des dépendances.

## Version 1.3.3 - 20 juin 2022

* Correction d’un problème qui empêchait l’ouverture de fenêtres contextuelles à partir de tableaux d’événements réseau.
* Correction d’un problème qui empêchait le chargement des informations Alloy sur la page.

## Version 1.3.2 - 9 juin 2022

* Ajout d’un avatar par défaut lorsque la personne est connectée.
* Ajout d’une mise en surbrillance de la syntaxe pour les objets JSON dans les journaux.

## Version 1.3.1 - 24 mai 2022

* Mise à jour des dépendances.
* Correction d’un problème d’Analytics en raison duquel les accès de post-traitement ne pouvaient pas être activés.
* Correction d’un problème en raison duquel Debugger se joignait à la fenêtre de connexion d’Adobe.
* Correction d’un problème d’AT.js en raison duquel les messages du journal ne s’affichaient pas dans Debugger.

## Version 1.3.0 - 28 janvier 2022

* Ajout du lien À propos pour afficher la version actuelle et les notes de mise à jour.
* Ajout d’un bouton (bascule) pour afficher les accès post-traités pour les requêtes Analytics. Le bouton (bascule) est disponible dans la section Analytics.
* Correction d’un problème de session de débogage à distance lorsque la session était fermée en dehors de Debugger.
* Correction d’une notification d’erreur visible dans l’onglet Transactions Edge du SDK web.
* Correction d’un problème lié aux balises d’Adobe dans l’avertissement d’obsolescence de la page lorsque Debugger accédait à l’objet _satellite.
* Correction de certains cas dans lesquels une instance AppMeasurement était introuvable sur la page.
* Correction d’un problème de connexion à la page qui se produisait lors de la première ouverture de la fenêtre de Debugger.

## Version 1.2.0 - 26 octobre 2021

* Afficher les événements de tous les onglets du navigateur dans la vue réseau. Pour afficher uniquement les événements de l’onglet actif, sélectionnez l’icône de verrouillage dans le coin inférieur droit de Debugger.
* Mise à jour de l’image de marque.

## Version 1.1.0 - 5 octobre 2021

* Visualisation du débogage à distance : organisez les événements de débogage à distance dans un diagramme de flux visuel dans le SDK web d’Adobe Experience Platform > section Transactions Edge.
* L’organisation du SDK web d’Adobe Experience Platform utilisée sur la page doit correspondre à l’organisation connectée lors du démarrage d’une nouvelle session de débogage à distance.
* Affiche uniquement les transactions Edge pour l’onglet connecté. Les journaux de Target Trace sont toujours disponibles dans la section Journaux > Edge.
* Autorisation du remplacement de la configuration de l’ID de flux de données distinct pour chaque instance du SDK web d’Adobe Experience Platform sur la page. Ajout du bouton (bascule) d’activation du débogage.
* Correction d’un problème en raison duquel le jeton d’Adobe Target Trace n’était pas toujours envoyé avec les sessions de débogage à distance pour le SDK web d’Adobe Experience Platform.

## Version 1.0.0 - 5 mai 2021

* Première version principale d’Experience Platform Debugger. Destiné à remplacer l’Experience Cloud Debugger.
