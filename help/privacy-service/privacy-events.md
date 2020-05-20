---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: S’abonner aux Événements de confidentialité
topic: privacy events
translation-type: tm+mt
source-git-commit: ab29c7771122267634dea24582b07f605abd7ed8
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---


# S’abonner aux Événements de confidentialité

Les Événements de confidentialité sont des messages fournis par Adobe Experience Platform Privacy Service, qui tirent parti des Événements d’E/S Adobe envoyés à un crochet Web configuré pour faciliter l’automatisation efficace des demandes de travaux. Elles réduisent ou éliminent le besoin de consulter l’API de Privacy Service pour vérifier si une tâche est terminée ou si un certain jalon dans un flux de travail a été atteint.

Il existe actuellement quatre types de notifications liées au cycle de vie de la demande de travail de confidentialité :

| Type | Description |
--- | ---
| Fin de tâche | Toutes les solutions Experience Cloud ont fait l’objet de rapports et l’état global ou global de la tâche a été marqué comme terminé. |
| Erreur de tâche | Une ou plusieurs solutions ont signalé une erreur lors du traitement de la demande. |
| Produit terminé | L&#39;une des solutions associées à ce travail a terminé son travail. |
| Erreur du produit | L’une des solutions a signalé une erreur lors du traitement de la demande. |

Ce document décrit la procédure à suivre pour configurer une intégration des notifications Privacy Service dans les E/S Adobe. Pour un aperçu général de Privacy Service et de ses fonctionnalités, consultez la présentation [de](home.md)Privacy Service.

## Prise en main

Ce tutoriel utilise **ngrok**, un logiciel qui expose les serveurs locaux à l&#39;internet public à travers des tunnels sécurisés. Veuillez [installer ngrok](https://ngrok.com/download) avant de commencer ce tutoriel afin de suivre et de créer un webhook sur votre machine locale. Ce guide nécessite également le téléchargement d’un référentiel GIT contenant un simple serveur [Node.js](https://nodejs.org/) .

## Création d’un serveur local

Votre serveur Node.js doit renvoyer un `challenge` paramètre envoyé par une requête au point de terminaison (`/`) racine. Configurez votre `index.js` fichier avec le code JavaScript suivant pour ce faire :

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

A l’aide de la ligne de commande, accédez au répertoire racine du serveur Node.js. Ensuite, tapez les commandes suivantes :

1. `npm install`
1. `npm start`

Ces commandes installent toutes les dépendances et initialisent le serveur. En cas de réussite, vous pouvez trouver votre serveur en cours d’exécution à l’adresse http://localhost:3000/.

## Création d’un hook Web à l’aide de ngrok

Ouvrez une nouvelle fenêtre de ligne de commande et accédez au répertoire dans lequel vous avez installé ngrok précédemment. A partir de là, tapez la commande suivante :

```shell
./ngrok http -bind-tls=true 3000
```

Une sortie réussie ressemble à ce qui suit :

![sortie de graphique](images/privacy-events/ngrok-output.png)

Notez l&#39; `Forwarding` URL (`https://212d6cd2.ngrok.io`), car elle sera utilisée pour identifier votre webhook à l&#39;étape suivante.

## Création d’un projet dans Adobe Developer Console

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le didacticiel relatif à la [création d’un projet](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vide dans la documentation d’Adobe Developer Console.

## Événements de confidentialité Ajouter au projet

Une fois que vous avez terminé de créer un projet dans la console, cliquez sur **[!UICONTROL Ajouter événement]** dans l’écran Présentation _du_ projet.

![](./images/privacy-events/add-event-button.png)

La boîte de dialogue événements __ Ajouter apparaît. Sélectionnez **[!UICONTROL Experience Cloud]** pour filtrer la liste d’un type d&#39;événement disponible, puis sélectionnez Événements **** Privacy Service avant de cliquer sur **[!UICONTROL Suivant]**.

![](./images/privacy-events/add-privacy-events.png)

La boîte de dialogue _Configurer l&#39;enregistrement_ du événement s&#39;affiche. Sélectionnez les événements que vous souhaitez recevoir en cochant les cases correspondantes. Les Événements que vous sélectionnez apparaissent sous Événements __abonnés dans la colonne de gauche. Lorsque vous avez terminé, cliquez sur**[!UICONTROL  Suivant ]**.

![](./images/privacy-events/choose-subscriptions.png)

L’écran suivant vous invite à fournir une clé publique pour l’enregistrement du événement. Vous avez la possibilité de générer automatiquement une paire de clés ou de télécharger votre propre clé publique générée dans le terminal.

Pour les besoins de ce didacticiel, la première option est suivie. Cliquez sur la zone d’options **[!UICONTROL Générer une paire]** de clés, puis cliquez sur le bouton **[!UICONTROL Générer la paire de clés]** dans le coin inférieur droit.

![](./images/privacy-events/generate-key-value.png)

Lorsque la paire de clés est générée, elle est automatiquement téléchargée par le navigateur. Vous devez stocker ce fichier vous-même, car il n’est pas conservé dans la Console développeur.

L’écran suivant vous permet de vérifier les détails de la paire de clés nouvellement générée. Cliquez sur **[!UICONTROL Suivant]** pour continuer.

![](./images/privacy-events/keypair-generated.png)

Dans l’écran suivant, indiquez le nom et la description de l’enregistrement du événement. Il est recommandé de créer un nom unique et facilement identifiable afin de différencier cette inscription de événement des autres sur le même projet.

![](./images/privacy-events/event-details.png)

Plus loin dans le même écran, vous disposez de deux options pour configurer la manière de recevoir des événements. Sélectionnez **[!UICONTROL Webhook]** et fournissez l’ `Forwarding` URL du webhook de réseau créé précédemment sous URL __Webhook. Ensuite, sélectionnez votre style de diffusion préféré (unique ou par lot) avant de cliquer sur**[!UICONTROL  Enregistrer les événements ]**configurés pour terminer l’enregistrement du événement.

![](./images/privacy-events/webhook-details.png)

La page de détails de votre projet réapparaît, les Événements de confidentialité s’affichant sous _[!UICONTROL Événements]_dans le volet de navigation de gauche.

## Données du événement de Vue

Une fois que vous avez enregistré des Événements de confidentialité avec votre projet et que vos tâches de confidentialité ont été traitées, vous pouvez vue les notifications reçues pour cette inscription. Dans l’onglet **[!UICONTROL Projets]** de la Console développeur, sélectionnez votre projet dans la liste pour ouvrir la page d’aperçu _des_ produits. Sélectionnez Événements **[!UICONTROL de]** confidentialité dans le volet de navigation de gauche.

![](./images/privacy-events/events-left-nav.png)

L&#39;onglet Détails __ d&#39;inscription s&#39;affiche, vous permettant de vue d&#39;informations supplémentaires sur l&#39;inscription, de modifier sa configuration ou de vue des événements reçus depuis l&#39;activation de votre webhook.

![](./images/privacy-events/registration-details.png)

Cliquez sur l’onglet Suivi **** du débogage pour vue d’une liste de événements reçus. Cliquez sur un événement répertorié pour en vue les détails.

![](images/privacy-events/debug-tracing.png)

La section _[!UICONTROL Charge utile]_fournit des détails sur le événement sélectionné, y compris son type d&#39;événement (`com.adobe.platform.gdpr.productcomplete`), comme indiqué dans l’exemple ci-dessus.

## Étapes suivantes

Vous pouvez répéter les étapes ci-dessus pour ajouter de nouvelles intégrations pour différentes adresses webhook, si nécessaire.