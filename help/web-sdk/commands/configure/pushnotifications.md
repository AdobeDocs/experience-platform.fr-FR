---
title: notifications push
description: Configurez les notifications push pour le Web SDK afin d’activer la messagerie push basée sur le navigateur.
source-git-commit: 9c3f19cc2b32ab70869584b620f5a55d5b808751
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---


# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
> Les notifications push pour le Web SDK sont actuellement en version **bêta**. Les fonctionnalités et la documentation peuvent changer.

La propriété `pushNotifications` vous permet de configurer des notifications push pour les applications web. Cette fonctionnalité permet à votre application web de recevoir des messages transmis par un serveur, même lorsque le site web n’est pas actuellement chargé dans le navigateur ou même lorsque le navigateur n’est pas en cours d’exécution.

## Conditions préalables {#prerequisites}

Avant de configurer des notifications push, vérifiez les points suivants :

1. **Autorisation utilisateur** : les utilisateurs doivent explicitement accorder une autorisation pour les notifications
2. **Service worker** : un service worker enregistré est nécessaire au fonctionnement des notifications push
3. **Clés VAPID** : générez des clés VAPID (Voluntary Application Server Identification) pour une communication sécurisée.

## Générer des clés VALIDES {#generate-vapid-keys}

Pour générer des clés VAPID, installez le package NPM `web-push` et exécutez :

```bash
npm install web-push -g
web-push generate-vapid-keys
```

Cela génère une paire de clés publique et privée. Utilisez la clé publique dans votre configuration de Web SDK et stockez la clé privée dans le canal de notifications push de Adobe Journey Optimizer.

## Configuration des notifications push à l’aide de l’extension de balise Web SDK {#configure-push-notifications-tag-extension}

Pour activer et configurer les notifications push, procédez comme suit :

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la vignette [!UICONTROL Adobe Experience Platform Web SDK].
1. **Activez les notifications push** à partir de la section « Composants de version personnalisés ».
1. Faites défiler la page vers le bas pour accéder à la section [!UICONTROL Notifications push].
1. Saisissez votre clé publique VAPID dans le champ **[!UICONTROL Clé publique VAPID]**.
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
  },
});
```

## Propriétés {#properties}

| Propriété | Type | Obligatoire | Description |
| ------ | ------ | -------- | ----- |
| `vapidPublicKey` | Chaîne | Oui | Clé publique VALIDE utilisée pour l’abonnement push. Doit être une chaîne codée en Base64. |

## Considérations importantes {#important-considerations}

- **Sécurité** : les abonnements aux notifications push sont liés à la clé publique VALIDE spécifique utilisée pendant l’abonnement. Si vous modifiez des clés VALIDES, les abonnements existants sont automatiquement désabonnés et recréés avec la nouvelle clé.
- **Mise en cache** : le SDK Web gère automatiquement les mises à jour des abonnements en comparant l’ECID actuel et les détails de l’abonnement avec les valeurs mises en cache. Les données d’abonnement ne sont envoyées que lorsque des modifications sont détectées.
- **Exigence du service worker** : les notifications push nécessitent un service worker enregistré. Assurez-vous que votre service worker est correctement configuré pour gérer les événements push.

## Étapes suivantes {#next-steps}

Après avoir configuré les notifications push, utilisez la commande [`sendPushSubscription`](../sendPushSubscription.md) pour enregistrer les abonnements push avec Adobe Experience Platform.
