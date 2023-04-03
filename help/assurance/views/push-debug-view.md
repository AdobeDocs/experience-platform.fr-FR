---
title: Push Debug View
description: Ce guide contient des informations détaillées sur la vue Débogage Push dans Adobe Experience Platform Assurance.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 1%

---


# Push Debug view

La vue de débogage Push dans Adobe Experience Platform Assurance permet de valider la configuration Push de votre application et d’envoyer un message de test à votre appareil.

## Clients

![Clients push](./images/push-debug-view/clients.png)

La liste déroulante client comporte une liste de chaque client unique connecté à cette session d’assurance. Un client est un appareil unique ou une installation d’application unique pour un appareil. Par exemple, si un appareil Android et un appareil iOS ont été connectés à la session, ces clients apparaissent dans la liste déroulante Clients .

Après avoir réinstallé et reconnecté l’application sur un appareil, un autre client s’affiche. Si un appareil portant ce nom existe déjà, la nouvelle liste déroulante ajoute un #2 au nom.

Cette vue n’est activée que pour un seul client. La sélection d’un autre client modifie donc les détails à l’écran.

## Validation de la configuration

Le **[!UICONTROL Validation de la configuration]** tab valide et fournit des détails supplémentaires sur la configuration push de l’application. Trois panneaux effectuent des validations. Une coche verte s’affiche si les validations réussissent toutes. S’il existe trois coches vertes, l’application a été correctement configurée pour la messagerie push, écrit des jetons push sur le profil utilisateur et a une surface d’application associée configurée.

Si quelque chose ne fonctionne pas comme prévu, une alerte vous indique comment résoudre ce problème :

![État non valide](./images/push-debug-view/invalid-state.png)

### Détails du client

Ce panneau vérifie si l’appareil est correctement configuré. Cela inclut la configuration de l’extension dans l’interface utilisateur de la collecte de données, l’initialisation de l’extension et de ses conditions préalables dans votre application et la capture du jeton push à partir de l’appareil.

S’il est valide, le panneau affiche l’ECID de l’appareil, le jeton push et le nom et le type de l’environnement de test Edge.

### Détails du profil

Une fois votre client configuré correctement, ce panneau vérifie si l’appareil écrit dans le profil. Il valide également que le jeton push dans le profil correspond à celui de l’appareil.

S’il est valide, le panneau affiche l’ECID de l’appareil, le jeton push, l’ID de l’application de votre application, la plateforme de messagerie et si le jeton push a été placé sur liste refusée. Le jeton peut être placé sur liste refusée pour diverses raisons, par exemple pour la désinstallation de l’application ou pour la désactivation de la messagerie push par l’utilisateur.

![Bloquée](./images/push-debug-view/deny-list-blocked.png)

Enfin, au bas du panneau se trouve un lien qui ouvre ce profil spécifique dans un nouvel onglet.

### Informations d’identification et configuration d’AppStore

Ce panneau valide la création d’une surface d’application correspondante pour l’ID de l’application et la plateforme de messagerie enregistrée dans le profil. Une surface d’application est l’endroit où les informations d’identification push de l’application sont chargées.

S’il est valide, le profil affiche le nom de la surface de l’application, l’identifiant de l’application et le nom du service de messagerie.

Enfin, au bas du panneau se trouve un lien qui ouvre cette surface d’application spécifique dans un nouvel onglet.

## Envoyer un test push

Le **[!UICONTROL Envoyer le test push]** peut être utilisé pour envoyer un message de test à votre appareil.

Plusieurs volets peuvent être configurés pour tester différentes fonctionnalités iOS et Android push. Une fois la configuration effectuée, sélectionnez **[!UICONTROL Envoi de la notification push de test]** pour envoyer votre message.

![Envoyer push](./images/push-debug-view/send.png)

### Message

Dans le **[!UICONTROL Message]** vous pouvez fournir un titre et un corps pour le message. La fonctionnalité de notification silencieuse peut également être activée ici.

![Volet Message](./images/push-debug-view/message-pane.png)

### Cible push

Le **[!UICONTROL Cible push]** vous permet de personnaliser le jeton push et la surface de l’application à utiliser lors de l’envoi du message push.

Ces informations sont fournies par défaut si la variable **[!UICONTROL Validation de la configuration]** affiche trois coches vertes. Cependant, vous pouvez fournir votre propre jeton push et votre propre surface d’application, même si votre application n’est pas entièrement configurée.

![Volet Cible](./images/push-debug-view/target-pane.png)

### Comportement des clics

Dans la **[!UICONTROL Comportement des clics]** , vous pouvez choisir le comportement à adopter lorsque vous cliquez sur la notification push sur l’appareil. Par défaut, l’application s’ouvre, mais elle peut ouvrir un lien profond ou une page web.

Si vous choisissez d’utiliser un lien profond, le développeur de l’application doit en créer un pour vous.

![Volet Comportement](./images/push-debug-view/click-behavior.png)

### Média enrichi

Le **[!UICONTROL Média enrichi]** vous permet d’ajouter des médias supplémentaires à votre message, tels qu’une image, une vidéo ou un GIF. Le développeur de l’application doit ajouter du code à l’application pour activer cette fonctionnalité.

![Volet enrichi](./images/push-debug-view/rich-pane.png)

### Boutons

Le **[!UICONTROL Boutons]** vous permet d’ajouter des boutons supplémentaires à la notification push. Chaque bouton peut ouvrir l’application, ouvrir un lien profond dans l’application ou ouvrir une page web.

Le développeur de l’application doit ajouter du code à l’application pour activer cette fonctionnalité.

![Volet Boutons](./images/push-debug-view/buttons-pane.png)

### Données personnalisées

Le **[!UICONTROL Données personnalisées]** vous permet d’ajouter des données personnalisées à la notification push. Chaque paire clé/valeur est envoyée sous forme de métadonnées avec le message et peut être utilisée par les développeurs pour créer des expériences puissantes et ajouter un suivi supplémentaire.

![Volet personnalisé](./images/push-debug-view/custom-pane.png)

## Résultats du test

Une fois que vous avez envoyé un message, la variable **[!UICONTROL Résultats du test]** reçoit les données des services push du message. Vous pouvez voir ici si le message a été envoyé aux services de messagerie Google/iOS :

![Résultats du test](./images/push-debug-view/test-results.png)

Si des problèmes se sont produits, ils s’affichent ici :

![Erreur des résultats du test](./images/push-debug-view/test-error.png)

## Advanced

### Affichage de la payload du message

En regard de **[!UICONTROL Envoi de la notification push de test]** est un ensemble de points de suspension avec un menu contextuel. À partir de là, vous pouvez afficher la payload du message. Vous pouvez ainsi voir le message exact qui sera envoyé au service de messagerie distant. Vous pouvez consulter cette payload ou la copier et la coller dans un outil de test push de bureau.

![Volet personnalisé](./images/push-debug-view/message-payload.png)
