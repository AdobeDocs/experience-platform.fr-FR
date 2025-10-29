---
title: sendPushSubscription
description: Enregistrez les abonnements aux notifications push avec Adobe Experience Platform.
source-git-commit: 84faff58bac199c1113d7451f8cc865b6a870680
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 3%

---


# `sendPushSubscription` {#send-push-subscription}

>[!AVAILABILITY]
>
> Les notifications push pour le Web SDK sont actuellement en version **bêta**. Les fonctionnalités et la documentation peuvent changer.

La commande `sendPushSubscription` enregistre les abonnements aux notifications push auprès de Adobe Experience Platform. Cette commande gère la récupération des détails d’abonnement push à partir du navigateur et les envoie à votre flux de données configuré.

## Conditions préalables {#prerequisites}

Avant d’utiliser `sendPushSubscription`, vérifiez que vous disposez des éléments suivants :

1. **Notifications push configurées** : configurez la propriété de configuration [`pushNotifications`](configure/pushnotifications.md) avec votre clé publique VALIDE
2. **Autorisation utilisateur** : les utilisateurs doivent disposer d&#39;une autorisation de notification (`Notification.permission === "granted"`)
3. **Service worker** : un service worker enregistré doit être disponible sur votre site
4. **Prise en charge de Push Manager** : le navigateur doit prendre en charge les notifications push et disposer de l’API PushManager

## Enregistrement d’un abonnement push à l’aide de l’extension de balise Web SDK {#register-push-subscription-tag-extension}

L’envoi des données d’abonnement push est effectué en tant qu’action dans une règle de l’interface Balises de collecte de données Adobe Experience Platform.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL Adobe Experience Platform Web SDK]** et définissez la [!UICONTROL Action Type] sur **[!UICONTROL Send Push Subscription]**.
1. Cliquez sur **[!UICONTROL Keep Changes]**, puis exécutez votre workflow de publication.

## Enregistrement d’un abonnement push à l’aide de la bibliothèque JavaScript Web SDK {#register-push-subscription-javascript}

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

Pour une fonctionnalité optimale de notification push, Adobe recommande d&#39;exécuter la commande `sendPushSubscription` **une fois par jour**. Cela permet de s’assurer que :

- Les détails de l’abonnement restent à jour dans Adobe Experience Platform
- Toute modification des jetons push ou du statut d’abonnement est capturée
- Le profil de l’utilisateur reste mis à jour avec les dernières préférences de notification push

Vous pouvez le mettre en œuvre en utilisant une approche similaire à celle ci-dessous :

```js
// Check if we've sent subscription data today
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
| `"The user has not given permission to send push notifications."` | L’utilisateur n’a pas accordé d’autorisation de notification |
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

## Documentation connexe

- [Configurer les notifications push](configure/pushnotifications.md)
- [Spécification de l’API Web Push](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
- [ API Service Worker ](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
