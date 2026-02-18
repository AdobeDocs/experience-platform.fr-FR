---
title: Intégration de Slack pour les alertes destinées aux clients
description: Découvrez comment connecter Adobe I/O Events à Slack à l’aide d’Adobe App Builder.
source-git-commit: c0fa0320b32e1bfe286d47a2e1af5ea1dcf74cb9
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 0%

---

# Intégration de Slack pour les alertes destinées aux clients et clientes

Adobe Experience Platform vous permet d’utiliser un proxy webhook sur [Adobe App Builder](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app) pour recevoir [Adobe I/O Events](https://developer.adobe.com/events/docs/guides/) en [!DNL Slack]. Le proxy gère l’établissement de liaison de vérification d’Adobe et transforme les payloads d’événement en messages [!DNL Slack], afin que vous puissiez envoyer des alertes destinées aux clients dans votre espace de travail.

## Conditions préalables {#prerequisites}

Avant de commencer, vérifiez que vous disposez des éléments suivants :

* **Accès à Adobe Developer Console** : rôle d’administrateur système ou de développeur dans une organisation avec App Builder activé.
* **Node.js et npm** : Node.js (recommandé par le LTS), qui inclut npm pour l’installation de l’interface de ligne de commande Adobe et les dépendances de projet. Pour plus d’informations, consultez les guides de prise en main [Télécharger Node.js](https://nodejs.org/) et [npm](https://docs.npmjs.com/getting-started).
* **Adobe I/O CLI** : installez l’interface de ligne de commande Adobe I/O à partir de votre terminal : `npm install -g @adobe/aio-cli`.
* **Application Slack avec Webhook entrant** : application Slack dans votre espace de travail avec un **Webhook entrant** activé. Voir [Création d’une application Slack](https://api.slack.com/apps) et le [guide des Webhooks entrants Slack](https://api.slack.com/messaging/webhooks) pour créer l’application et obtenir l’URL du webhook (format : `https://hooks.slack.com/...`).

## Configuration d’un projet modélisé {#templated-project}

Pour configurer un projet modélisé, connectez-vous à Adobe Developer Console, puis sélectionnez **[!UICONTROL Create project from template]** dans l’onglet **[!UICONTROL Home]** .

![Developer Console mettant en surbrillance l’onglet Accueil et Créer un projet à partir d’un modèle.](../images/alerts/slack-integration/developer-console-home.png)

Sélectionnez le modèle de **[!UICONTROL App Builder]**, puis saisissez un **[!UICONTROL Project Title]** et sélectionnez **[!UICONTROL Add workspace]**. Enfin, sélectionnez **[!UICONTROL Save]**.

![Developer Console mettant en surbrillance le titre du projet, Ajouter un Workspace et Enregistrer.](../images/alerts/slack-integration/developer-console-save.png)

Vous recevrez une confirmation indiquant que votre projet a été créé et serez redirigé vers l’onglet **[!UICONTROL Project overview]** . À partir de là, vous pouvez ajouter un **[!UICONTROL Project description]**.

![Onglet Aperçu du projet affichant les détails du projet.](../images/alerts/slack-integration/developer-console-project.png)

## Initialiser le projet {#initialize-project}

Une fois le projet modélisé configuré, initialisez-le.

1. Ouvrez votre terminal et saisissez la commande suivante pour vous connecter à Adobe I/O.

   ```bash
   aio login
   ```

1. Initialisez l’application et attribuez-lui un nom.

   ```bash
   aio app init slack-webhook-proxy
   ```

1. Sélectionnez votre `Organization` à l’aide des touches fléchées, puis sélectionnez le `Project` que vous avez créé précédemment dans le Developer Console. Sélectionnez `Only Templates Supported By My Org` pour les modèles à rechercher.

   ![Terminal affichant la sélection d’organisations et de projets, et uniquement les modèles pris en charge par mon organisation.](../images/alerts/slack-integration/terminal-organization-project.png)

1. Ensuite, appuyez sur **Entrée** pour ignorer les modèles et installer une application autonome.

   ![Terminal affichant la sélection d’organisations et de projets, et uniquement les modèles pris en charge par mon organisation.](../images/alerts/slack-integration/terminal-skip-templates.png)

1. Spécifiez les fonctionnalités de l’application Adobe I/O à activer pour ce projet. Utilisez les touches fléchées pour faire défiler l’écran et sélectionner `Actions: Deploy Runtime actions`.

   ![Terminal affichant les fonctionnalités de l’application avec des actions : Déployer les actions d’exécution sélectionnées.](../images/alerts/slack-integration/terminal-app-features.png)

1. Utilisez les touches fléchées pour faire défiler l’écran et sélectionner `Adobe Experience Platform: Realtime Customer Profile` pour le type d’actions types que vous souhaitez créer.

   ![Terminal présentant un exemple de type d’actions avec Adobe Experience Platform : profil client en temps réel sélectionné.](../images/alerts/slack-integration/terminal-sample-actions.png)

1. Faites défiler l’écran et sélectionnez `Pure HTML/JS` pour l’interface utilisateur que vous souhaitez ajouter à votre modèle. Appuyez sur **Entrée** pour conserver les exemples d’actions par défaut, puis appuyez de nouveau sur **Entrée** pour conserver le nom par défaut.

   ![Terminal affichant la sélection de l’interface utilisateur avec HTML/JS pur sélectionné.](../images/alerts/slack-integration/terminal-ui-template.png)

   Vous recevez une confirmation indiquant que l’initialisation de l’application est terminée.

1. Accédez au répertoire du projet.

   ```bash
   cd slack-webhook-proxy
   ```

1. Ajoutez l’action web .

   ```bash
   aio app add action
   ```

1. Sélectionnez `Only Action Templates Supported By My Org`. Une liste de modèles s’affiche.

   ![Terminal affichant la liste des modèles d’action.](../images/alerts/slack-integration/terminal-action-templates.png)

1. Sélectionnez le modèle en appuyant sur la barre d’espace, puis accédez à `@adobe/generator-add-publish-events` à l’aide des flèches **Haut** et **Bas**. Enfin, sélectionnez le modèle en appuyant sur la **barre d’espacement** puis sur **Entrée**.

   ![Terminal affichant le modèle.](../images/alerts/slack-integration/terminal-action-select-template.png)

   Une confirmation s’affiche indiquant que le `npm package @adobe/generator-add-publish-events` a été installé.

1. Nommez le `webhook-proxy` d’action.

   ![Terminal affichant l’action nommée webhook-proxy.](../images/alerts/slack-integration/terminal-add-action-name.png)

   Une confirmation s’affiche indiquant que le modèle a été installé.

## Création des actions de fichier et déploiement {#create-file-actions}

Ajoutez le code proxy, définissez les variables d’environnement, puis déployez. L’action sera alors disponible dans le Developer Console pour enregistrement.

### Implémenter le proxy d’exécution {#runtime-proxy}

>[!NOTE]
>
>La vérification des signatures et la gestion des défis sont automatiques lors de l’utilisation de l’enregistrement de l’action d’exécution.

Accédez au dossier du projet et ouvrez le fichier `actions/webhook-proxy/index.js`. Supprimez le contenu et remplacez par ce qui suit :

```
const fetch = require("node-fetch");
const { Core } = require("@adobe/aio-sdk");
 
/**
 * Adobe I/O Events to Slack Runtime Proxy
 *
 * Receives events from Adobe I/O Events and forwards them to Slack.
 * Signature verification and challenge handling are automatic when
 * using Runtime Action registration (non-web action).
 */
async function main(params) {
  const logger = Core.Logger("runtime-proxy", { level: params.LOG_LEVEL || "info" });
 
  try {
    logger.info(`Event received: ${JSON.stringify(params)}`);
 
    // Forward to Slack
    return forwardToSlack(params, params.SLACK_WEBHOOK_URL, logger);
 
  } catch (error) {
    logger.error(`Error: ${error.message}`);
    return { statusCode: 500, body: { error: "Internal server error" } };
  }
}
 
/**
 * Forwards the event payload to Slack
 */
async function forwardToSlack(payload, webhookUrl, logger) {
  if (!webhookUrl) {
    logger.error("SLACK_WEBHOOK_URL not configured");
    return { statusCode: 500, body: { error: "Server configuration error" } };
  }
 
  // Extract Adobe headers passed to runtime action
  const headers = {
    "x-adobe-event-code": payload["x-adobe-event-code"],
    "x-adobe-event-id": payload["x-adobe-event-id"],
    "x-adobe-provider": payload["x-adobe-provider"]
  };
 
  const slackMessage = buildSlackMessage(payload, headers);
 
  const response = await fetch(webhookUrl, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(slackMessage)
  });
 
  if (!response.ok) {
    const errorText = await response.text();
    logger.error(`Slack API error: ${response.status} - ${errorText}`);
    return { statusCode: response.status, body: { error: errorText } };
  }
 
  logger.info("Event forwarded to Slack");
  return { statusCode: 200, body: { success: true } };
}
 
/**
 * Builds a Slack Block Kit message from the event payload
 */
function buildSlackMessage(payload, headers) {
  // Adobe passes event code as x-adobe-event-code header (available in params for runtime actions)
  const eventType = headers["x-adobe-event-code"] ||
                    payload["x-adobe-event-code"] ||
                    payload.event_code ||
                    payload.type ||
                    payload.event_type ||
                    "Adobe Event";
  const eventId = headers["x-adobe-event-id"] || payload["x-adobe-event-id"] || payload.event_id || payload.id || "N/A";
  const eventData = payload.data || payload.event || payload;
 
  return {
    blocks: [
      {
        type: "header",
        text: { type: "plain_text", text: `Event: ${eventType}`, emoji: true }
      },
      {
        type: "section",
        fields: formatDataFields(eventData)
      },
      { type: "divider" },
      {
        type: "context",
        elements: [{
          type: "mrkdwn",
          text: `*Event ID:* ${eventId}  |  *Time:* ${new Date().toISOString()}`
        }]
      }
    ]
  };
}
 
/**
 * Formats event data as Slack mrkdwn fields
 */
function formatDataFields(data, maxFields = 10) {
  if (typeof data !== "object" || data === null) {
    return [{ type: "mrkdwn", text: `*Payload:*\n${String(data)}` }];
  }
 
  const entries = Object.entries(data);
  if (entries.length === 0) {
    return [{ type: "mrkdwn", text: "_No data provided_" }];
  }
 
  return entries.slice(0, maxFields).map(([key, value]) => ({
    type: "mrkdwn",
    text: `*${key}:*\n${typeof value === "object" ? `\`\`\`${JSON.stringify(value)}\`\`\`` : value}`
  }));
}
 
exports.main = main;
```

### Configurer l’action dans app.config.yaml {#app-config}

>[!IMPORTANT]
>
>La configuration de l’action dans `app.config.yaml` est essentielle. Vous devez utiliser `web: no` pour créer une action non web qui peut être enregistrée en tant qu’action d’exécution dans le Developer Console.

Accédez au dossier du projet et ouvrez-`app.config.yaml`. Remplacez le contenu par le texte suivant :

```
application:
  runtimeManifest:
    packages:
      slack-webhook-proxy:
        license: Apache-2.0
        actions:
          webhook-proxy:
            function: actions/webhook-proxy/index.js
            web: no
            runtime: nodejs:22
            inputs:
              LOG_LEVEL: info
              SLACK_WEBHOOK_URL: $SLACK_WEBHOOK_URL
            annotations:
              require-adobe-auth: false
              final: true
```

### Variables d&#39;environnement {#environment-variables}

>[!IMPORTANT]
>
>L’application ne s’exécute pas sans un fichier .env correctement configuré.

Pour gérer les informations d’identification en toute sécurité, utilisez les variables d’environnement. Modifiez le fichier `.env` à la racine de votre projet et ajoutez les éléments suivants :

```
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL
```

### Déployer l’action {#deploy-action}

Une fois les variables d’environnement définies, déployez l’action. Assurez-vous que vous êtes à la racine de votre projet (`slack-webhook-proxy`) lorsque vous exécutez cette commande dans le terminal :

```bash
aio app deploy
```

Une confirmation s’affiche indiquant que le déploiement a réussi.

>[!IMPORTANT]
>
>Votre action est déployée sur Adobe I/O Runtime. L’action sera désormais disponible dans le Developer Console pour enregistrement.

## Enregistrement de l’action auprès de Adobe I/O Events {#register-events}

Une fois votre action déployée, enregistrez-la en tant que destination de Adobe I/O Events.

Dans le Developer Console, ouvrez votre projet App Builder, puis sélectionnez votre **[!UICONTROL Workspace]**.

Sur la page d’aperçu de Workspace, sélectionnez **[!UICONTROL Add service]** et **[!UICONTROL Event]**.

![Page d’aperçu Workspace mettant en surbrillance Ajouter un service et un événement.](../images/alerts/slack-integration/workspace-service-event.png)

Sur la page Ajouter des événements , sélectionnez **[!UICONTROL Experience Platform]** et **[!UICONTROL Platform notifications]**, puis **[!UICONTROL Next]**.

![Page Ajouter des événements affichant les notifications Experience Platform et Platform sélectionnées.](../images/alerts/slack-integration/add-events.png)

Sélectionnez les événements pour lesquels vous souhaitez recevoir des notifications, puis sélectionnez **[!UICONTROL Next]**.

![Page Ajouter des événements affichant la liste des événements auxquels s’abonner.](../images/alerts/slack-integration/select-events.png)

Sélectionnez vos informations d’authentification serveur à serveur, puis sélectionnez **[!UICONTROL Next]**.

![Page Ajouter des événements affichant la sélection des informations d’authentification de serveur à serveur.](../images/alerts/slack-integration/add-events-credentials.png)

Saisissez un **[!UICONTROL Event registration name]** et un **[!UICONTROL Event registration description]** clair pour l’enregistrement, puis sélectionnez **[!UICONTROL Next]**.

![Page Ajouter des événements affichant les champs Nom d’enregistrement de l’événement et Description de l’enregistrement de l’événement.](../images/alerts/slack-integration/add-events-registration.png)

Sélectionnez **[!UICONTROL Runtime Action]** comme méthode de diffusion et l’action `slack-webhook-proxy/runtime-proxy` que vous avez créée, puis sélectionnez **[!UICONTROL Save configured events]**.

![Page Ajouter des événements affichant la méthode de diffusion Action d’exécution et Enregistrer les événements configurés.](../images/alerts/slack-integration/add-events-runtime.png)

Votre proxy webhook est maintenant configuré. Vous revenez sur la page du proxy Webhook. Vous pouvez tester l’ensemble du flux de bout en bout en sélectionnant l’icône **[!UICONTROL Send sample event]** en regard de n’importe quel événement configuré.

![Page du proxy webhook affichant les événements configurés et l’icône Envoyer un exemple d’événement.](../images/alerts/slack-integration/send-sample.png)
