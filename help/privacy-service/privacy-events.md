---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: S’abonner au de confidentialité
topic: privacy events
translation-type: tm+mt
source-git-commit: e4cd042722e13dafc32b059d75fca2dab828df60

---


# S’abonner au de confidentialité

Les  de confidentialité sont des messages fournis par le service de confidentialité d’Adobe Experience Platform, qui tirent parti des d’E/S Adobe envoyés à un crochet Web configuré pour faciliter l’automatisation efficace des demandes de travaux. Elles réduisent ou éliminent la nécessité de consulter l’API de Privacy Service afin de vérifier si une tâche est terminée ou si un certain jalon dans un flux de travail a été atteint.

Il existe actuellement quatre types de notifications liées au cycle de vie de la demande de travail de confidentialité :

| Type | Description |
--- | ---
| Fin de tâche | Toutes les solutions Experience Cloud ont fait l’objet de rapports et l’état global ou global de la tâche a été marqué comme terminé. |
| Erreur de tâche | Une ou plusieurs solutions ont signalé une erreur lors du traitement de la requête. |
| Produit terminé | Une des solutions associées à cette tâche a terminé son travail. |
| Erreur du produit | L’une des solutions a signalé une erreur lors du traitement de la requête. |

Ce décrit la procédure à suivre pour configurer une intégration des notifications Privacy Service dans les E/S Adobe. Pour un aperçu général de Privacy Service et de ses fonctionnalités, consultez la présentation [de](home.md)Privacy Service.

## Prise en main

Ce tutoriel utilise **ngrok**, un logiciel qui expose les serveurs locaux à l&#39;Internet public par le biais de tunnels sécurisés. Veuillez [installer ngrok](https://ngrok.com/download) avant de commencer ce tutoriel afin de suivre et créer un webhook sur votre machine locale. Ce guide nécessite également le téléchargement d’un référentiel GIT contenant un serveur simple écrit dans [Node.js](https://nodejs.org/).

## Création d’un serveur local

Votre serveur Node.js doit renvoyer un `challenge` paramètre envoyé par une requête au point de terminaison racine (`/`). Configurez votre `index.js` fichier avec le code JavaScript suivant pour ce faire :

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

A l’aide de la ligne de commande, accédez au répertoire racine du serveur Node.js. Saisissez ensuite les commandes suivantes :

1. `npm install`
1. `npm start`

Ces commandes installent toutes les dépendances et initialisent le serveur. En cas de réussite, vous pouvez trouver votre serveur s’exécutant à l’adresse http://localhost:3000/.

## Création d’un crochet Web à l’aide de ngrok

Dans le même répertoire et dans une nouvelle fenêtre de ligne de commande, saisissez la commande suivante :

```shell
ngrok http -bind-tls=true 3000
```

Une sortie réussie ressemble à ce qui suit :

![sortie ngrok](images/privacy-events/ngrok-output.png)

Prenez note de l&#39; `Forwarding` URL (`https://e142b577.ngrok.io`), car elle sera utilisée pour identifier votre webhook à l&#39;étape suivante.

## Création d’une intégration à l’aide d’Adobe I/O Console

Connectez-vous à [Adobe I/O Console](https://console.adobe.io) et cliquez sur l’onglet **Intégrations** . La fenêtre _Intégrations_ s’affiche. A partir de là, cliquez sur **Nouvelle intégration**.

![Intégrations des  dans la console d’E/S Adobe](images/privacy-events/integrations.png)

La fenêtre *Créer une nouvelle intégration* s’affiche. Sélectionnez **Recevoir les** proches du, puis cliquez sur **Continuer**.

![Créer une nouvelle intégration](images/privacy-events/new-integration.png)

L’écran suivant fournit des options permettant de créer des intégrations avec différents , produits et services disponibles pour votre organisation en fonction de vos  de vos , de vos droits et de vos autorisations. Pour cette intégration, sélectionnez **** Privacy Service, puis cliquez sur **Continuer**.

![Sélectionner un de confidentialité](images/privacy-events/privacy-events.png)

Le formulaire Détails *de l’* intégration s’affiche. Vous devez fournir un nom et une description pour l’intégration, ainsi qu’un certificat de clé publique.

![Détails de l’intégration](images/privacy-events/integration-details.png)

Si vous ne disposez pas d’un certificat public, vous pouvez en générer un à l’aide de la commande terminal suivante :

```shell
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub
```

Une fois que vous avez généré un certificat, faites glisser et déposez le fichier dans la zone Certificats **de clés** publiques ou cliquez sur **Sélectionner un fichier** pour parcourir le répertoire des fichiers et sélectionner directement le certificat.

Après avoir ajouté votre certificat, l’option *d’enregistrement* s’affiche. Cliquez sur **Ajouter  Inscription**.

![Ajouter Inscription](images/privacy-events/add-event-registration.png)

La boîte de dialogue s’étend pour afficher d’autres commandes. Ici vous pouvez sélectionner votre et enregistrer votre webhook. Entrez un nom pour l’enregistrement du , l’URL du webhook (l’ `Forwarding` adresse renvoyée lors de la [création initiale du webhook](#create-a-webhook-using-ngrok)), ainsi qu’une brève description. Enfin, sélectionnez le auquel vous souhaitez vous abonner, puis cliquez sur **Enregistrer**.

![Formulaire d&#39;inscription](images/privacy-events/event-registration-form.png)

Une fois le formulaire d&#39;inscription  rempli, cliquez sur **Créer l&#39;intégration** et l&#39;intégration E/S sera terminée.

![Créer une intégration](images/privacy-events/create-integration.png)

##  de données

Une fois que vous avez créé vos tâches d&#39;intégration d&#39;E/S et de confidentialité, vous pouvez  les notifications reçues pour cette intégration. Dans l&#39;onglet **Intégrations** de la console d&#39;E/S, accédez à votre intégration et cliquez sur ****.

![Intégration des](images/privacy-events/view-integration.png)

La page de détails de l’intégration s’affiche. Cliquez sur **** pour  les enregistrements de l&#39; pour l&#39;intégration. Recherchez l’enregistrement du de confidentialité et cliquez sur ****.

![et enregistrement](images/privacy-events/view-registration.png)

La fenêtre Détails *du* s’affiche, vous permettant de  plus d’informations sur l’enregistrement, de modifier sa configuration ou de le véritable qui a été reçu depuis l’activation de votre webhook. Vous pouvez  les détails  du et accéder à l’option Suivi du **débogage** .

![Suivi du débogage](images/privacy-events/debug-tracing.png)

La section **Charge** fournit des détails sur le  de sélectionné, y compris son  de (`"com.adobe.platform.gdpr.productcomplete"`), comme indiqué dans l’exemple ci-dessus.

## Étapes suivantes

Vous pouvez répéter les étapes ci-dessus pour ajouter de nouvelles intégrations pour différentes adresses WebHook, le cas échéant.