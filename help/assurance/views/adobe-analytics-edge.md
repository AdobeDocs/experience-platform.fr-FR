---
title: Événements Analytics 2.0 dans Assurance
description: Ce guide explique comment utiliser la vue Adobe Analytics et Analytics Edge avec Adobe Experience Platform Assurance.
badgeBeta: label="Version Beta" type="Informative"
source-git-commit: f707554ea89731fbd3f013d6065fde27ba7fa811
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---

# Événements Analytics 2.0 dans Assurance

Les événements Analytics 2.0 offrent une vue plus riche des événements de SDK aux utilisateurs qui déboguent et valident leur mise en oeuvre Adobe Analytics. La vue affiche les événements envoyés à Adobe Analytics à partir du [SDK Adobe Experience Platform Mobile](https://developer.adobe.com/client-sdks/solution/adobe-analytics/) ainsi que la variable [SDK réseau Adobe Experience Platform Edge](https://developer.adobe.com/client-sdks/edge/edge-network/). La vue comprend également un panneau de détails, qui fournit un contexte sur la manière dont l’événement a été traité par le SDK client, ainsi que par les services en amont une fois qu’il a quitté l’appareil.

## Prise en main

Pour utiliser cette vue, procédez comme suit :

1. [Configuration de Adobe Experience Platform Assurance](../tutorials/implement-assurance.md).
2. [Création et connexion à une session Assurance](../tutorials/using-assurance.md).
3. Dans l’interface utilisateur d’assurance à partir du volet de navigation de gauche **Accueil** menu d’affichage, sélectionnez **Analytics Events 2.0 (bêta)**. Si vous ne voyez pas cette option, sélectionnez **Configurer** dans le coin inférieur gauche de la fenêtre, ajoutez le **Analytics Events 2.0 (bêta)**, puis sélectionnez **Enregistrer**.

## Vue Événements Analytics

Utilisez la vue d’événement Analytics si vous utilisez la variable **Adobe Analytics** extension mobile. Cette vue vous permet d’afficher facilement les événements Analytics envoyés à partir de votre client connecté, y compris les événements d’action de suivi, d’état de suivi et de cycle de vie. Si vous sélectionnez l’un des événements Analytics dans le tableau, vous pouvez afficher les détails sur le traitement de l’événement dans le panneau de droite.

![Image présentant différents composants dans la vue Événements Analytics.](./images/adobe-analytics-edge/analytics-events.png)

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
| `Unavailable` | La requête Adobe Analytics ne comporte pas de `AnalyticsResponse` . |
| `No Debug Flag` | La version actuelle du SDK Adobe Analytics ou Assurance peut ne pas prendre en charge la fonctionnalité de débogage Analytics. Pour plus d’informations, veuillez lire la [Guide de dépannage](../troubleshooting.md). |
| `Expired` | La variable `AnalyticsTrack` ou `LifecycleStart` a plus de 24 heures. |

### Affichage des détails de l’événement

Pour un événement de suivi Analytics, la vue détaillée contient les parties suivantes :

- Événement de demande d’Analytics du SDK d’origine.
- Métadonnées et données contextuelles provenant de la requête, telles que l’identifiant de la suite de rapports, les versions de l’extension du SDK et les données contextuelles.
- Informations post-traitées sur l’événement Analytics qui contient le mappage des variables, evars et props.

### Validation de la vue Analytics

La vue de validation vous permet d’afficher facilement les résultats sur les scripts de validation liés à Analytics. Les erreurs affichées par les validateurs peuvent contenir des liens vers l’emplacement où elles doivent être corrigées ou afficher les événements qui se trouvent dans un état d’erreur.

![Image qui affiche l’onglet Validateurs dans la vue Analytics.](./images/adobe-analytics-edge/analytics-validation-view.png)

## Vue Edge Analytics

Utilisez la vue Analytics Edge si vous utilisez **Edge Network** ou **Edge Bridge** extensions mobiles. Pour activer cette vue, sélectionnez la bascule &quot;Analytics Edge (Beta)&quot; en haut à droite pour afficher les événements Analytics envoyés via le réseau Edge dans votre session en cours. Cela inclut tous les événements qui ont été déclenchés par l’extension de cycle de vie, les requêtes Edge et/ou les événements Edge Bridge basés sur l’action de suivi et l’état de suivi.

![Image qui affiche le bouton d’activation/désactivation utilisé pour basculer entre la vue Analytics et la vue Edge Analytics.](./images/adobe-analytics-edge/analytics-view-toggle.png)

La vue Edge Analytics contient des informations sur les requêtes Edge liées à Analytics et les méthodes de cycle de vie distribuées par le client. En choisissant un événement dans la liste, le panneau de droite affiche les événements qui ont été traités par le SDK client, ainsi que par le service en amont après qu’ils aient quitté l’appareil, afin que vous puissiez facilement afficher la chaîne des événements qui ont résulté d’un appel .

![Image présentant différents composants dans la vue Edge Analytics.](./images/adobe-analytics-edge/edge-analytics-events.png)

### Validation d’Analytics Edge

La vue de validation d’Analytics Edge vous permet d’afficher facilement les résultats sur les scripts de validation liés à Analytics Edge. Les erreurs affichées par les validateurs peuvent contenir des liens vers l’emplacement où elles doivent être corrigées ou afficher les événements qui se trouvent dans un état d’erreur.

![Image qui affiche l’onglet Validateurs dans la vue Edge Analytics.](./images/adobe-analytics-edge/edge-analytics-validation-view.png)
