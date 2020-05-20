---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: S’abonner aux Événements de confidentialité
topic: privacy events
translation-type: tm+mt
source-git-commit: e4cd042722e13dafc32b059d75fca2dab828df60
workflow-type: tm+mt
source-wordcount: '778'
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

Ce tutoriel utilise **ngrok**, un logiciel qui expose les serveurs locaux à l&#39;internet public à travers des tunnels sécurisés. Veuillez [installer ngrok](https://ngrok.com/download) avant de commencer ce tutoriel afin de suivre et de créer un webhook sur votre machine locale. Ce guide nécessite également le téléchargement d’un référentiel GIT contenant un serveur simple écrit dans [Node.js](https://nodejs.org/).

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

Dans le même répertoire et dans une nouvelle fenêtre de ligne de commande, tapez la commande suivante :

```shell
ngrok http -bind-tls=true 3000
```

Une sortie réussie ressemble à ce qui suit :

![sortie de graphique](images/privacy-events/ngrok-output.png)

Notez l&#39; `Forwarding` URL (`https://e142b577.ngrok.io`), car elle sera utilisée pour identifier votre webhook à l&#39;étape suivante.

## Créer une nouvelle intégration à l’aide de la console d’E/S d’Adobe

Connectez-vous à [Adobe I/O Console](https://console.adobe.io) et cliquez sur l’onglet **Intégrations** . La fenêtre _Intégrations_ s&#39;affiche. A partir de là, cliquez sur **Nouvelle intégration**.

![Intégrations des Vues dans la console d&#39;E/S d&#39;Adobe](images/privacy-events/integrations.png)

La fenêtre *Créer une intégration* s’affiche. Sélectionnez **Recevoir des événements temps réels** proches, puis cliquez sur **Continuer**.

![Créer une nouvelle intégration](images/privacy-events/new-integration.png)

L’écran suivant fournit des options permettant de créer des intégrations avec différents événements, produits et services disponibles pour votre organisation en fonction de vos abonnements, droits et autorisations. Pour cette intégration, sélectionnez Événements **** Privacy Service, puis cliquez sur **Continuer**.

![Sélectionner des Événements de confidentialité](images/privacy-events/privacy-events.png)

Le formulaire Détails *de l’* intégration s’affiche, vous obligeant à fournir un nom et une description pour l’intégration, ainsi qu’un certificat de clé publique.

![Détails de l’intégration](images/privacy-events/integration-details.png)

Si vous ne disposez pas d’un certificat public, vous pouvez en générer un à l’aide de la commande terminal suivante :

```shell
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub
```

Une fois que vous avez généré un certificat, faites glisser et déposez le fichier dans la zone Certificats **de clés** publiques ou cliquez sur **Sélectionner un fichier** pour parcourir votre répertoire de fichiers et sélectionner directement le certificat.

Après avoir ajouté votre certificat, l’option Enregistrement *du* Événement s’affiche. Cliquez sur **Ajouter Événement Inscription**.

![Enregistrement du Événement Ajouter](images/privacy-events/add-event-registration.png)

La boîte de dialogue se développe pour afficher d’autres commandes. Ici vous pouvez sélectionner vos types d&#39;événement et enregistrer votre webhook. Saisissez un nom pour l’enregistrement du événement, l’URL du crochet Web (l’ `Forwarding` adresse renvoyée lors de la première [création du crochet](#create-a-webhook-using-ngrok)Web), ainsi qu’une brève description. Enfin, sélectionnez les types d&#39;événement auxquels vous souhaitez vous abonner, puis cliquez sur **Enregistrer**.

![Formulaire d&#39;inscription au Événement](images/privacy-events/event-registration-form.png)

Une fois le Événement Registration form rempli, cliquez sur **Create integration** (Créer l&#39;intégration) et l&#39;intégration d&#39;E/S sera terminée.

![Créer une intégration](images/privacy-events/create-integration.png)

## Données du événement de Vue

Une fois que vous avez créé vos tâches d&#39;intégration d&#39;E/S et de confidentialité traitées, vous pouvez vue les notifications reçues pour cette intégration. Dans l&#39;onglet **Intégrations** de la console d&#39;E/S, accédez à votre intégration et cliquez sur **Vue**.

![Intégration de Vue](images/privacy-events/view-integration.png)

La page de détails de l’intégration s’affiche. Cliquez sur **Événements** pour vue des enregistrements de événement pour l’intégration. Recherchez l’enregistrement Événements de confidentialité et cliquez sur **Vue**.

![Inscription au Événement de Vue](images/privacy-events/view-registration.png)

La fenêtre Détails *du* Événement s’affiche, vous permettant de vue d’informations supplémentaires sur l’enregistrement, de modifier sa configuration ou de vue les événements réellement reçus depuis l’activation de votre webhook. Vous pouvez vue les détails du événement et accéder à l’option Suivi **du** débogage.

![Suivi du débogage](images/privacy-events/debug-tracing.png)

La section **Charge utile** fournit des détails sur le événement sélectionné, y compris son type d&#39;événement (`"com.adobe.platform.gdpr.productcomplete"`), comme indiqué dans l’exemple ci-dessus.

## Étapes suivantes

Vous pouvez répéter les étapes ci-dessus pour ajouter de nouvelles intégrations pour différentes adresses webhook, si nécessaire.