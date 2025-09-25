---
title: notifications push
description: Configurez les notifications push pour le Web SDK afin d’activer la messagerie push basée sur le navigateur.
source-git-commit: 7c2afd6d823ebb2db0fabb4cc16ef30bcbfeef13
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 2%

---


# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
> Les notifications push pour le Web SDK sont actuellement en version **bêta**. Les fonctionnalités et la documentation peuvent changer.

La propriété `pushNotifications` vous permet de configurer des notifications push pour les applications web. Cette fonctionnalité permet à votre application web de recevoir des messages transmis par un serveur, même si le site web n’est pas actuellement chargé dans le navigateur.

## Conditions préalables {#prerequisites}

Avant de configurer des notifications push, vérifiez les points suivants :

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

Cela génère une paire de clés publique et privée. Utilisez la clé publique dans votre configuration de Web SDK et stockez la clé privée dans le canal de notifications push de Adobe Journey Optimizer.

## Installation du service worker JavaScript

Le code du service worker doit être diffusé à partir du même domaine que le site web. Téléchargez le code du service worker à partir du réseau CDN d’Adobe, puis hébergez le fichier JavaScript à partir de votre propre serveur. Le code du service worker Web SDK est disponible en utilisant la structure d’URL suivante :

- **Minifié** : `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.min.js`
- **Complet** : `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.js`

Voici un exemple d’installation du service worker :

```html
<script>
  navigator.serviceWorker.register("/alloyServiceWorker.js", { scope: "/" });
</script>
```

## Configuration des notifications push à l’aide de l’extension de balise Web SDK {#configure-push-notifications-tag-extension}

Pour activer et configurer les notifications push, procédez comme suit :

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la vignette [!UICONTROL Adobe Experience Platform Web SDK].
1. Dans la section **[!UICONTROL Composants de build personnalisés]**, activez **[!UICONTROL Notifications push]**.
1. Faites défiler la page vers le bas pour accéder à la section [!UICONTROL Notifications push].
1. Saisissez votre clé publique VAPID dans le champ **[!UICONTROL Clé publique VAPID]**.
1. Saisissez votre ID d’application dans le champ **[!UICONTROL ID d’application]**.
1. Saisissez votre identifiant de jeu de données de suivi dans le champ **[!UICONTROL Identifiant du jeu de données de suivi]**.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

>[!NOTE]
>
> Les notifications push doivent être explicitement activées dans la configuration de l’extension de balise. Cette fonction est désactivée par défaut.

## Configuration des notifications push à l&#39;aide de la bibliothèque JavaScript Web SDK {#configure-push-notifications-javascript}

Définissez l’objet `pushNotifications` lors de l’exécution de la commande `configure` :

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey:
      "BEl62iUYgUivElbkzaBgNL3r3vOAhvJyFXjS6FjjRRojYD4NElJkLBJKZvS3xAAh4_gE3WnMaZNu_KGP4jAQlJz",
    applicationId: "my-app-id",
    trackingDatasetId: "4dc19305cdd27e03dd9a6bbe",
  },
});
```

## Propriétés {#properties}

| Propriété | Type | Obligatoire | Description |
|---------|----|---------|-----------|
| `vapidPublicKey` | Chaîne | Oui | Clé publique VALIDE utilisée pour l’abonnement push. Doit être une chaîne codée en Base64. |
| `applicationId` | Chaîne | Oui | ID de l’application associé à cette clé publique valide. |
| `trackingDatasetId` | Chaîne | Oui | Identifiant du jeu de données système utilisé pour le suivi des notifications push. |

## Considérations importantes {#important-considerations}

- **Sécurité** : les abonnements aux notifications push sont liés à la clé publique VALIDE spécifique utilisée pendant l’abonnement. Si vous modifiez des clés VALIDES, les abonnements existants sont automatiquement désabonnés et recréés avec la nouvelle clé.
- **Mise en cache** : le SDK Web gère automatiquement les mises à jour des abonnements en comparant l’ECID actuel et les détails de l’abonnement avec les valeurs mises en cache. Les données d’abonnement ne sont envoyées que lorsque des modifications sont détectées.
- **Exigence du service worker** : les notifications push nécessitent un service worker enregistré. Assurez-vous que votre service worker est correctement configuré pour gérer les événements push.

## Étapes suivantes {#next-steps}

Après avoir configuré les notifications push, utilisez la commande [`sendPushSubscription`](../sendPushSubscription.md) pour enregistrer les abonnements push avec Adobe Experience Platform.
