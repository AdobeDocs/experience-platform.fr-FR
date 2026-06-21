---
title: notifications push
description: Configurez les notifications push pour le Web SDK afin d’activer la messagerie push basée sur le navigateur.
exl-id: a5cf4817-a4c2-4cf1-8f3a-7e92b807de8f
TQID: https://experienceleague.adobe.com/9rbMQjUORLLES-KeaX1laWGFmilU3Triq6yGGgDiCzg
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: d556b755-390a-43f0-be32-a08cf6236126
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 301d9785acd28811f1c6fbf9efdc5378e81d4c2c
workflow-type: tm+mt
source-wordcount: 418
ht-degree: 3%

---

# `pushNotifications` {#push-notifications}

La propriété `pushNotifications` vous permet de configurer des notifications push pour les applications web. Cette fonctionnalité permet à votre application web de recevoir des messages transmis par un serveur, même si le site web n’est pas actuellement chargé dans le navigateur.

## Conditions préalables {#prerequisites}

Avant de configurer des notifications push, vérifiez que vous disposez des éléments suivants :

1. **Autorisation utilisateur** : les utilisateurs doivent explicitement accorder une autorisation pour les notifications
2. **Service worker** : un service worker enregistré est nécessaire au fonctionnement des notifications push
3. **Clés VAPID** : générez des clés VAPID (Voluntary Application Server Identification) pour une communication sécurisée.
4. **ID de l’application** : ID de l’application utilisé lors de l’enregistrement des clés VAPID dans Adobe Journey Optimizer -> Canaux -> Paramètres de notification push -> Informations d’identification push
5. **Identifiant du jeu de données de suivi** : identifiant du jeu de données système nommé « Jeu de données d’événement d’expérience de suivi Push AJO ». Obtenir ceci à partir de Adobe Journey Optimizer -> Jeux de données

## Générer des clés VALIDES {#generate-vapid-keys}

Pour générer des clés VAPID, installez le package NPM `web-push` et exécutez :

```bash
npm install web-push -g
web-push generate-vapid-keys
```

Cette action génère une paire de clés publique et privée. Utilisez la clé publique dans votre configuration de Web SDK et stockez la clé privée dans le canal de notifications push de Adobe Journey Optimizer.

## Installation du service worker

Le code du service worker doit être diffusé à partir du même domaine que le site web. Téléchargez le code du service worker à partir du réseau CDN d’Adobe et hébergez le fichier JavaScript à partir de votre propre serveur. Le code du service worker Web SDK est disponible en utilisant la structure d’URL suivante :

- **Minifié** : `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.min.js`
- **Complet** : `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.js`

Voici un exemple d’installation du service worker :

```html
<script>
  navigator.serviceWorker.register("/alloyServiceWorker.js", { scope: "/" });
</script>
```

## Mise en œuvre

Définissez l’objet `pushNotifications` lors de l’exécution de la commande `configure` :

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey: "BEl62iUYgU[...]KGP4jAQlJz",
    appId: "my-app-id",
    trackingDatasetId: "4dc19305cdd27e03dd9a6bbe",
  },
});
```

## Propriétés {#properties}

| Propriété | Type | Obligatoire | Description |
|---|---|---|---|
| **`vapidPublicKey`** | Chaîne | Oui | Clé publique VALIDE utilisée pour les abonnements aux notifications push. Doit être une chaîne codée en Base64. |
| **`appId`** | Chaîne | Oui | ID de l’application associé à la clé publique valide. |
| **`trackingDatasetId`** | Chaîne | Oui | Identifiant du jeu de données système utilisé pour le suivi des notifications push. |

## Considérations importantes {#important-considerations}

- **Sécurité** : les abonnements aux notifications push sont liés à la clé publique VALIDE spécifique utilisée pendant l’abonnement. Si vous modifiez des clés VALIDES, les abonnements existants sont automatiquement désabonnés et recréés avec la nouvelle clé.
- **Mise en cache** : le SDK Web gère automatiquement les mises à jour des abonnements en comparant l’ECID actuel et les détails de l’abonnement avec les valeurs mises en cache. Les données d’abonnement ne sont envoyées que lorsque des modifications sont détectées.
- **Exigence du service worker** : les notifications push nécessitent un service worker enregistré. Assurez-vous que votre service worker est correctement configuré pour gérer les événements push.

## Configuration des notifications push à l’aide de l’extension de balise Web SDK {#configure-push-notifications-tag-extension}

L’extension de balise Web SDK équivalente à cette propriété est la section [[!UICONTROL Notifications push]](/help/tags/extensions/client/web-sdk/configure/push-notifications.md) lors de la configuration de l’extension.

## Étapes suivantes {#next-steps}

Après avoir configuré les notifications push, utilisez la commande [sendPushSubscription](../sendpushsubscription.md) pour enregistrer les abonnements push avec Adobe Experience Platform.
