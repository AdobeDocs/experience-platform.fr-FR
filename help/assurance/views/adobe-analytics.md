---
title: Vue Adobe Analytics dans Assurance
description: Ce guide explique comment utiliser Adobe Analytics avec Adobe Experience Platform Assurance.
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 66c9b8c1489b86b0b928fc37380f2187a7d237cf
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Vue Événements Adobe Analytics dans Assurance

Les événements Analytics offrent une vue plus riche des événements SDK aux utilisateurs qui déboguent et valident leur mise en oeuvre Adobe Analytics. La vue affiche les événements envoyés à Adobe Analytics à partir du [ SDK Edge Network Adobe Experience Platform ](https://developer.adobe.com/client-sdks/edge/edge-network/) ainsi que le [ SDK Mobile Adobe Experience Platform ](https://developer.adobe.com/client-sdks/solution/adobe-analytics/). La vue comprend également un panneau de détails, qui fournit un contexte sur la manière dont l’événement a été traité par le SDK client et par les services en amont une fois qu’il a quitté l’appareil.

## Commencer

Pour utiliser cette vue, procédez comme suit :

1. [Configurez Adobe Experience Platform Assurance](../tutorials/implement-assurance.md).
2. [Créez une session d’assurance et connectez-vous à une session](../tutorials/using-assurance.md).
3. Dans l’interface utilisateur d’assurance du menu de navigation de gauche **Home**, sélectionnez **Analytics Events**. Si vous ne voyez pas cette option, sélectionnez **Configurer** dans le coin inférieur gauche de la fenêtre, ajoutez les **Événements Analytics** et sélectionnez **Enregistrer**.

## Vue Analytics Edge

Utilisez la vue Analytics Edge si vous utilisez des extensions mobiles **Edge Network** ou **Edge Bridge**. Cette vue est activée lorsque le bouton bascule &quot;Vue Analytics Edge&quot; dans le coin supérieur droit est activé, affichant les événements Analytics envoyés via le réseau Edge dans votre session en cours. Cela inclut tous les événements qui ont été déclenchés par l’extension Lifecycle, l’extension Edge et/ou l’extension Edge Bridge.

![Image qui affiche le bouton d’activation/désactivation qui est passé à la vue Analytics Edge.](./images/adobe-analytics/edge-analytics-view-toggle.png)

La vue Analytics Edge contient des informations sur les événements Edge liés à Analytics et les événements de cycle de vie distribués par le client. En choisissant un événement dans la liste, le panneau d’affichage des détails de l’événement à droite affiche les événements qui ont été traités par le SDK client et par le service en amont après avoir quitté l’appareil. Cela vous permet d’afficher facilement la chaîne d’événements résultant d’un appel .

![Image présentant différents composants dans la vue Analytics Edge pour le scénario Bridge Edge.](./images/adobe-analytics/edgebridge-analytics-events.png)

L’événement **Données post-traitées** de la liste confirme que les données ont été traitées avec succès et envoyées à Adobe Analytics. Si cet événement ou toute donnée traitée est manquante, les utilisateurs peuvent développer chaque événement de la liste pour afficher des informations de débogage détaillées.

### Vue Détails de l’événement Analytics Edge

Pour un événement de demande Edge ou un événement de suivi Analytics, la vue détaillée contient les informations suivantes :

* Détails de l’événement : un événement de requête Edge du SDK d’origine.
* Requête Bridge Edge : événement destiné exclusivement au processus d’extension Bridge Edge.
* Datastream : un événement représenté pour le flux de données de cette session.
* Accès Edge reçu : représente l’accès reçu d’Edge.
* Edge Accès traité : représente l’accès traité dans Edge.
* Accès Analytics : représente l’accès reçu d’Analytics.
* Mappage Analytics : représente l’état du mappage de données dans Analytics.
* Analytics Répondu : état de la réponse d’Analytics.
* Données de post-traitement : informations sur l’événement contenant le mappage des variables, evars et props.

### Validation d’Analytics Edge

La vue de validation d’Analytics Edge vous permet d’afficher facilement les résultats des scripts de validation liés à la session Analytics Edge. Les erreurs affichées par les validateurs peuvent contenir des liens vers l’emplacement où elles doivent être corrigées ou afficher les événements qui se trouvent dans un état d’erreur.

![Image qui affiche l’onglet Validateurs dans la vue Analytics Edge.](./images/adobe-analytics/edge-analytics-validation-view.png)

## Vue Événements Analytics

Utilisez la vue d’événement Analytics si vous utilisez l’extension mobile **Adobe Analytics**. Cette vue vous permet d’afficher facilement les événements Analytics envoyés à partir de votre client connecté, y compris les événements d’action de suivi, d’état de suivi et de cycle de vie. Cette vue est active lorsque la bascule &quot;Vue Analytics Edge&quot; en haut à droite est désactivée.

![Image qui affiche le bouton bascule qui est passé à la vue Analytics.](./images/adobe-analytics/direct-analytics-view-toggle-button.png)

En sélectionnant l’un des événements Analytics dans le tableau d’événement, vous pouvez afficher les détails sur le traitement de l’événement dans le panneau de droite.

![Image présentant différents composants dans la vue Événements Analytics.](./images/adobe-analytics/analytics-events.png)

### Etat post-traitement

Une fois que le SDK a effectué une requête réseau avec Adobe Analytics, l’état vous indique si Assurance a été en mesure de récupérer les informations de post-traitement pour la requête Adobe Analytics. La vue Événements Analytics doit rester active pendant que l’état de post-traitement est en cours d’exécution une fois la requête déclenchée.

Pour récupérer les informations de post-traitement, l’utilisateur connecté doit avoir accès à la suite de rapports correspondante.

| État | Description |
| :----- | :---------- |
| `Queued` | La requête réseau récupère les informations de post-traitement. |
| `Processed` | La requête réseau a réussi et les informations de post-traitement sont reçues. |
| `Delayed` | Le nombre maximal de tentatives de récupération des informations de post-traitement a été dépassé. |
| `Error` | Une erreur provoquait l’échec de la requête réseau. Des informations supplémentaires sur l’erreur s’affichent dans la vue des détails de l’événement. |
| `Unauthorized` | L’utilisateur n’a pas accès à la suite de rapports Adobe Analytics. |
| `Unavailable` | La requête Adobe Analytics ne comporte pas d’événement `AnalyticsResponse` correspondant. |
| `No Debug Flag` | La version actuelle du SDK Adobe Analytics ou Assurance peut ne pas prendre en charge la fonctionnalité de débogage Analytics. Pour plus d’informations, consultez le [guide de dépannage](../troubleshooting.md). |
| `Expired` | L’événement `AnalyticsTrack` ou `LifecycleStart` a plus de 24 heures. |

### Affichage des détails de l’événement

Pour un événement de suivi Analytics, la vue détaillée contient les parties suivantes :

* Événement de demande d’Analytics du SDK d’origine.
* Métadonnées et données contextuelles provenant de la requête, telles que l’identifiant de la suite de rapports, les versions de l’extension du SDK et les données contextuelles.
* Informations post-traitées sur l’événement Analytics qui contient le mappage des variables, evars et props.

### Validation de la vue Analytics

La vue de validation vous permet d’afficher facilement les résultats des scripts de validation liés à Analytics. Les erreurs affichées par les validateurs peuvent contenir des liens vers l’emplacement où elles doivent être corrigées ou afficher les événements qui se trouvent dans un état d’erreur.

![Image qui affiche l’onglet Validateurs dans la vue Analytics.](./images/adobe-analytics/analytics-validation-view.png)