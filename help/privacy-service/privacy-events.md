---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Abonnement à des événements de confidentialité
topic: privacy events
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 31%

---


# S’abonner à [!DNL Privacy Events]

[!DNL Privacy Events] sont des messages fournis par Adobe Experience Platform [!DNL Privacy Service], qui tirent parti des Événements d&#39;E/S d&#39;Adobe envoyés à un webhook configuré pour faciliter l&#39;automatisation efficace des demandes d&#39;emploi. They reduce or eliminate the need to poll the [!DNL Privacy Service] API in order to check if a job is complete or if a certain milestone within a workflow has been reached.

Il existe actuellement quatre types de notifications liées au cycle de vie de la tâche de demande d’accès à des informations personnelles :

| Type | Description |
--- | ---
| Fin de tâche | All [!DNL Experience Cloud] solutions have reported back and the overall or global status of the job has been marked as complete. |
| Erreur de tâche | Une ou plusieurs solutions ont signalé une erreur lors du traitement de la requête. |
| Produit terminé | L’une des solutions associées à cette tâche a terminé son travail. |
| Erreur de produit | L’une des solutions a signalé une erreur lors du traitement de la requête. |

This document provides steps for setting up an integration for [!DNL Privacy Service] notifications within Adobe I/O. For a high-level overview of [!DNL Privacy Service] and its features, see the [Privacy Service overview](home.md).

## Prise en main

Ce tutoriel utilise **ngrok**, un logiciel exposant les serveurs locaux à l’Internet public par le biais de canaux sécurisés. Avant de commencer, [installez ngrok](https://ngrok.com/download) pour suivre ce tutoriel et créer un webhook sur votre machine locale. This guide also requires you to have a GIT repository downloaded that contains a simple [Node.js](https://nodejs.org/) server.

## Création d’un serveur local

Votre serveur Node.js doit renvoyer un paramètre `challenge` envoyé par une requête au point de terminaison racine (`/`). Pour ce faire, configurez votre fichier `index.js` avec le code JavaScript suivant :

```js
var express = require('express')
var app = express()

app.set('port', (process.env.PORT || 3000))
app.use(express.static(__dirname + '/public'))

app.get('/', function(request, response) {
  response.send(request.originalUrl.split('?challenge=')[1]);
})

app.listen(app.get('port'), function() {
  console.log("Node app is running at localhost:" + app.get('port'))
})
```

À l’aide de la ligne de commande, accédez au répertoire racine du serveur Node.js. Exécutez ensuite les commandes suivantes :

1. `npm install`
1. `npm start`

Ces commandes installent toutes les dépendances et initialisent le serveur. En cas de réussite, votre serveur s’exécute à l’adresse http://localhost:3000/.

## Création d’un webhook à l’aide de ngrok

Ouvrez une nouvelle fenêtre de ligne de commande et accédez au répertoire dans lequel vous avez installé ngrok précédemment. A partir de là, tapez la commande suivante :

```shell
./ngrok http -bind-tls=true 3000
```

Une sortie réussie a l’apparence suivante :

![sortie ngrok](images/privacy-events/ngrok-output.png)

Prenez note de l’URL `Forwarding` (`https://212d6cd2.ngrok.io`) qui sera utilisée pour identifier votre webhook à l’étape suivante.

## Créer un projet dans la console de développement Adobe

Go to [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_fr) and sign in with your Adobe ID. Suivez ensuite les étapes décrites dans le didacticiel sur la [création d&#39;un projet](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vide dans la documentation de la Console développeur d&#39;Adobes.

## ajouter des Événements de confidentialité au projet

Une fois que vous avez terminé de créer un projet dans la console, cliquez sur **[!UICONTROL Ajouter le événement]** dans l’écran Présentation _du_ projet.

![](./images/privacy-events/add-event-button.png)

The _Add events_ dialog appears. Sélectionnez **[!UICONTROL Experience Cloud]** pour filtrer la liste d’un type d&#39;événement disponible, puis sélectionnez Événements **** Privacy Service avant de cliquer sur **[!UICONTROL Suivant]**.

![](./images/privacy-events/add-privacy-events.png)

La boîte de dialogue _Configurer l&#39;enregistrement_ du événement s&#39;affiche. Sélectionnez les événements que vous souhaitez recevoir en cochant les cases correspondantes. Les événements que vous sélectionnez apparaissent sous Événements **** abonnés dans la colonne de gauche. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Suivant]**.

![](./images/privacy-events/choose-subscriptions.png)

L’écran suivant vous invite à fournir une clé publique pour l’enregistrement du événement. Vous avez la possibilité de générer automatiquement une paire de clés ou de télécharger votre propre clé publique générée dans le terminal.

Pour les besoins de ce didacticiel, la première option est suivie. Cliquez sur la zone d’options **[!UICONTROL Générer une paire]** de clés, puis cliquez sur le bouton **[!UICONTROL Générer la paire de clés]** dans le coin inférieur droit.

![](./images/privacy-events/generate-key-value.png)

Lorsque la paire de clés est générée, elle est automatiquement téléchargée par le navigateur. Vous devez stocker ce fichier vous-même, car il n’est pas conservé dans la Console développeur.

L’écran suivant vous permet de vérifier les détails de la paire de clés nouvellement générée. Cliquez sur **[!UICONTROL Suivant]** pour continuer.

![](./images/privacy-events/keypair-generated.png)

Dans l’écran suivant, indiquez le nom et la description de l’enregistrement du événement. Il est recommandé de créer un nom unique et facilement identifiable afin de différencier cette inscription de événement des autres sur le même projet.

![](./images/privacy-events/event-details.png)

Plus loin dans le même écran, vous disposez de deux options pour configurer la manière de recevoir des événements. Sélectionnez **[!UICONTROL Webhook]** et fournissez l’ `Forwarding` URL du webhook de réseau créé précédemment sous URL **** Webhook. Ensuite, sélectionnez votre style de diffusion préféré (unique ou par lot) avant de cliquer sur **[!UICONTROL Enregistrer les événements]** configurés pour terminer l’enregistrement du événement.

![](./images/privacy-events/webhook-details.png)

La page de détails de votre projet réapparaît et s’ [!DNL Privacy Events] affiche sous **[!UICONTROL Événements]** dans le volet de navigation de gauche.

## Affichage des données d’événement

Une fois que vous vous êtes inscrit [!DNL Privacy Events] à votre projet et que les tâches de confidentialité ont été traitées, vous pouvez vue les notifications reçues pour cette inscription. Dans l’onglet **[!UICONTROL Projets]** de la Console développeur, sélectionnez votre projet dans la liste pour ouvrir la page d’aperçu _des_ produits. Sélectionnez Événements **[!UICONTROL de]** confidentialité dans le volet de navigation de gauche.

![](./images/privacy-events/events-left-nav.png)

The _Registration Details_ tab appears, allowing you to view more information about the registration, edit its configuration, or view the actual events that were received since activating your webhook.

![](./images/privacy-events/registration-details.png)

Cliquez sur l’onglet Suivi **** du débogage pour vue d’une liste de événements reçus. Cliquez sur un événement répertorié pour en vue les détails.

![](images/privacy-events/debug-tracing.png)

La section **[!UICONTROL Payload]** fournit des détails sur l’événement sélectionné, y compris sur le type d’événement (`com.adobe.platform.gdpr.productcomplete`), comme indiqué dans l’exemple ci-dessus.

## Étapes suivantes

Vous pouvez répéter les étapes ci-dessus afin d’ajouter de nouvelles intégrations pour différentes adresses webhook, le cas échéant.