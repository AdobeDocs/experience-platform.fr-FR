---
title: sendPushSubscription
description: Enregistrez les abonnements aux notifications push avec Adobe Experience Platform.
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 4%

---


# `sendPushSubscription` {#send-push-subscription}

>[!AVAILABILITY]
>
>Les notifications push pour le Web SDK sont actuellement en version **bêta**. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

La commande `sendPushSubscription` enregistre les abonnements aux notifications push auprès de Adobe Experience Platform. Cette commande gère la récupération des détails d’abonnement push à partir du navigateur et les envoie à votre flux de données configuré. Il est disponible dans les versions 2.29.0 ou ultérieures de Web SDK.

## Conditions préalables {#prerequisites}

Avant d’utiliser `sendPushSubscription`, vérifiez que vous disposez des éléments suivants :

1. **Notifications push configurées** : configurez la propriété de configuration [`pushNotifications`](configure/pushnotifications.md) avec votre clé publique VALIDE
2. **Autorisation utilisateur** : les utilisateurs doivent disposer d&#39;une autorisation de notification (`Notification.permission === "granted"`)
3. **Service worker** : un service worker enregistré doit être disponible sur votre site
4. **Prise en charge de Push Manager** : le navigateur doit prendre en charge les notifications push et disposer de l’API PushManager

Exécutez la commande `sendPushSubscription` lors de l’appel de votre instance configurée de Web SDK. Veillez à appeler la commande [`configure`](configure/overview.md) avec les notifications push configurées avant d&#39;appeler la commande `sendPushSubscription`.

```js
alloy("sendPushSubscription")
  .then(() => {
    console.log("Push subscription recorded successfully");
  })
  .catch((error) => {
    console.error("Failed to send push subscription:", error);
  });
```

## Fréquence d’exécution recommandée {#recommended-execution-frequency}

Pour une fonctionnalité optimale de notification push, Adobe recommande d&#39;exécuter la commande `sendPushSubscription` **une fois par jour**. Cette fréquence permet de s’assurer que :

* Les détails de l’abonnement restent à jour dans Adobe Experience Platform
* Toute modification des jetons push ou du statut d’abonnement est capturée
* Le profil de l’utilisateur reste mis à jour avec les dernières préférences de notification push

Vous pouvez le mettre en œuvre en utilisant une approche similaire à celle ci-dessous :

```js
// Check if subscription data was sent today
const lastSent = localStorage.getItem("alloy_push_last_sent");
const today = new Date().toDateString();

if (lastSent !== today) {
  alloy("sendPushSubscription").then(() => {
    localStorage.setItem("alloy_push_last_sent", today);
  });
}
```

## Fonctionnement {#how-it-works}

La commande `sendPushSubscription` effectue les actions suivantes :

1. **Valide les conditions préalables** : vérifie que les notifications push sont configurées et que l’autorisation utilisateur est accordée
2. **Attend l’identité** : attend que l’ECID de l’utilisateur soit disponible
3. **Récupère l’abonnement** : récupère l’abonnement push actif auprès de l’agent de service à l’aide de la clé VALID configurée
4. **Vérifie les modifications** : compare les détails de l’abonnement actuel aux valeurs mises en cache (ECID + détails de l’abonnement). Si les détails de l’abonnement n’ont pas changé, la commande consigne un message d’information et renvoie sans effectuer de requête réseau
5. **Envoie au flux de données** : si des modifications sont détectées, transmet les données d’abonnement au flux de données Adobe Experience Platform configuré
6. **Met à jour le cache** : stocke les détails du nouvel abonnement pour une comparaison ultérieure.

## Traitement des erreurs {#error-handling}

Conditions d’erreur courantes et leurs messages :

| Erreur | Cause |
| ------- | ---- |
| `"Push notifications module is not configured. No VAPID public key was provided."` | Configuration des notifications push manquante ou non valide |
| `"Service workers are not supported in this browser."` | Le navigateur ne prend pas en charge les agents de service |
| `"Push notifications are not supported in this browser."` | Le navigateur ne prend pas en charge les notifications push ou l’API de notification |
| `"The user has not given permission to send push notifications."` | L&#39;utilisateur n&#39;a pas accordé d&#39;autorisation de notification (`Notification.permission === "granted"`) |
| `"No service worker registration was found."` | Aucun service worker n’est enregistré pour l’origine actuelle |
| `"No VAPID public key was provided."` | Clé publique VALIDE manquante dans la configuration |

## Payload des données {#data-payload}

La commande envoie les données de notification push au format suivant :

```js
{
  pushNotificationDetails: [
    {
      appID: "example.com", // Current domain
      token: "...", // Serialized subscription details + ECID
      platform: "web", // Always "web" for Web SDK
      denylisted: false, // Always false
      identity: {
        namespace: {
          code: "ECID",
        },
        id: "12345678901234567890", // User's ECID
      },
    },
  ],
}
```

## Enregistrement d’un abonnement push à l’aide de l’extension de balise Web SDK {#register-push-subscription-tag-extension}

L’extension de balise Web SDK équivalente à ce champ utilise l’action [[!UICONTROL Send Push Subscription]](/help/tags/extensions/client/web-sdk/actions/send-push-subscription.md) dans une règle de balise.

>[!MORELIKETHIS]
>
>* [Configurer les notifications push](configure/pushnotifications.md)
>* [Spécification de l’API Web Push](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [&#x200B; API Service Worker &#x200B;](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
