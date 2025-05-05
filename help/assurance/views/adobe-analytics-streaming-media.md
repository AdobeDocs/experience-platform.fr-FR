---
title: Vue Adobe Analytics pour les médias en streaming dans Assurance
description: Ce guide explique comment utiliser Adobe Analytics pour les médias en streaming avec Adobe Experience Platform Assurance.
exl-id: 9a9c2c64-e9ed-4d58-b936-d802f1c3b7d3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Vue Adobe Analytics pour les médias en streaming dans Assurance

Avec l’intégration entre Adobe Analytics pour les médias en streaming et Adobe Experience Platform Assurance, vous pouvez désormais valider la mise en oeuvre de Media Analytics dans votre application mobile. Les vues Media Analytics affichent ce qui est suivi dans la session multimédia, par exemple :

- Événement de début de session contenant toutes les propriétés de base de contenu, les métadonnées standard et les métadonnées personnalisées, ainsi que les événements de fin de session et de fin de session.
- Événements Début de la coupure publicitaire et Début de la publicité avec toutes les propriétés de publicité associées, ainsi que Saut et Fin pour les deux.
- Début du chapitre avec toutes les propriétés jointes, ainsi que les événements Saut de chapitre et Fin du chapitre.
- Tous les événements de changement de lecture (lecture, pause, mémoire tampon, erreurs, changement de débit).
- Tous les événements de suivi de changement d’état du lecteur (début, fin).

Une fois les données traitées dans Analytics, l’état et les données post-traitement, tels que le temps passé sur le média et la durée totale de mise en pause, sont également disponibles dans la vue détaillée de l’événement.

## Commencer

Avant de poursuivre, assurez-vous que vous disposez des services suivants :

- [Interface utilisateur de collecte de données Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Pour savoir comment installer Assurance dans votre application, consultez le [guide d’assurance d’implémentation](../tutorials/implement-assurance.md).

## Utilisation de l’assurance avec Adobe Analytics pour les médias en streaming

Une fois que vous êtes connecté et que vous avez configuré votre application pour Adobe Analytics, vous êtes prêt à la configurer pour Streaming Media Analytics. Au bas du panneau de gauche, sélectionnez **[!UICONTROL Configurer]** pour ajouter la vue Événements Media Analytics et **Enregistrer**.

![Configuration](./images/adobe-analytics-streaming-media/configure.png)

Une fois ajouté, sélectionnez la vue **[!UICONTROL Media Analytics Events]** dans la section **[!UICONTROL Adobe Analytics]** pour valider votre suivi de session.

![Select](./images/adobe-analytics-streaming-media/select.png)

Dans la vue **[!UICONTROL Événements Media Analytics]**, vous pouvez rechercher et filtrer par ID de session (VSID) pour afficher une session multimédia spécifique. Pour afficher des détails d’événement supplémentaires, sélectionnez un événement spécifique.

![Événements de médias](./images/adobe-analytics-streaming-media/media-events.png)

Pour obtenir une vue plus succincte des appels API, vous pouvez également masquer les événements de mise à jour du curseur de lecture en sélectionnant le filtre **[!UICONTROL Masquer les événements de mise à jour du curseur de lecture]** .

![Masquer le curseur de lecture](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>L’affichage des données d’analyse des médias post-traités nécessite l’utilisation des versions du SDK : Android Media 2.1.2 et iOS AEPMedia 3.0.1 (ou version ultérieure)

Pour afficher les données post-traitées, recherchez l’événement de début de session et validez dans la colonne d’état la fin de la session. Si vous avez terminé, cliquez sur l’événement pour afficher un résumé de la session multimédia dans la vue détaillée de l’événement. Pour plus d’informations, faites défiler la page vers le bas pour trouver les détails post-traités.

![ &lbrace;Post-Processed View](./images/adobe-analytics-streaming-media/post-processed-view.png)
