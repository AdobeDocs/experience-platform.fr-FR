---
title: Données QoE (Qualité de l’expérience) Détails Type de données de rapport
description: Découvrez le type de données du modèle de données d’expérience (XDM) de rapport sur les détails de la qualité de l’expérience (QoE).
exl-id: 608baa9b-12ca-466c-a962-1401abc0344e
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 4%

---

# Données QoE (Qualité de l’expérience) Détails Type de données de rapport

[!UICONTROL Détails des données QoE] La création de rapports est un type de données XDM (Experience Data Model) standard qui fournit des mesures détaillées liées à la qualité de l’expérience (QoE) pendant la lecture multimédia. Utilisez le type de données de rapport [!UICONTROL Détails des données QoE] pour capturer des détails tels que des informations de débit binaire, des taux d’images, des événements de mise en mémoire tampon, des images perdues, etc. Les champs de création de rapports multimédia sont utilisés par les services Adobe pour analyser les champs Media Collection envoyés par les utilisateurs. Ces données, ainsi que d’autres mesures utilisateur spécifiques, sont calculées et font l’objet de rapports. Ce type de données permet d’analyser la qualité de lecture, ce qui permet d’obtenir des informations sur les performances de diffusion en continu, l’expérience utilisateur et les problèmes potentiels rencontrés lors des sessions de lecture.

+++Sélectionnez cette option pour afficher le type de données de rapport Détails de données QoE.
![Schéma du type de données de rapport de détails de la qualité de l’expérience (QoE).](../images/data-types/qoe-data-details-reporting.png)
+++

>[!NOTE]
>
>Chaque nom d’affichage contient un lien vers des informations supplémentaires sur ses paramètres audio et vidéo. Les pages liées contiennent des détails sur les données de publicité vidéo collectées par Adobe, les valeurs d’implémentation, les paramètres réseau, la création de rapports et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|---------------------------------------------------------------------------------------------------|
| [[!UICONTROL Débit moyen]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate-1) | `bitrateAverage` | nombre | Débit moyen (en Kbits/s, nombre entier). Calculé en tant que moyenne pondérée des valeurs de débit binaire. |
| [[!UICONTROL Intervalle de débit moyen]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrateAverageBucket` | Chaîne | Débit moyen (en Kbits/s) catégorisé dans des intervalles prédéfinis à des intervalles de 100 Kbits/s. |
| [[!UICONTROL Débit ]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | Entier | Valeur de débit binaire (en Kbits/s). |
| [[!UICONTROL Diffusions touchées par les changements de débit]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#bitrate-change-impacted-streams) | `hasBitrateChangeImpactedStreams` | Booléen | Indique si les flux ont été affectés par les changements de débit au cours de la lecture. |
| [[!UICONTROL Changements de débit binaire]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#bitrate-changes) | `bitrateChangeCount` | Entier | Le nombre total de changements de débit binaire au cours de la lecture. |
| [[!UICONTROL Événements de mémoire tampon]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#buffer-events) | `bufferCount` | Entier | Nombre d’états de mémoire tampon différents pendant la lecture. |
| [[!UICONTROL Flux touchés par la mémoire tampon]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#buffer-impacted-streams) | `hasBufferImpactedStreams` | Booléen | Indique si les diffusions ont été affectées par la mise en mémoire tampon pendant la lecture. |
| [[!UICONTROL Flux touchés par la perte d’images]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frame-impacted-streams) | `hasDroppedFrameImpactedStreams` | Booléen | Indique si les diffusions ont été affectées par les pertes d’images au cours de la lecture. |
| [[!UICONTROL Images perdues]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames-1) | `droppedFrames` | Entier | Nombre total d’images perdues pendant la lecture. |
| [[!UICONTROL Pertes avant le début]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#drops-before-start) | `isDroppedBeforeStart` | Booléen | Indique si les utilisateurs quittent la vidéo avant de la démarrer, quelles que soient les publicités. |
| [[!UICONTROL Diffusions touchées par les erreurs]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#error-impacted-streams) | `hasErrorImpactedStreams` | Booléen | Indique si les flux ont rencontré des erreurs au cours de la lecture. |
| [[!UICONTROL Erreurs]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#errors-%2F-error-events) | `errorCount` | Entier | Nombre total d’erreurs qui se sont produites au cours de la lecture. |
| [[!UICONTROL ID d’erreur externe]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#external-error-ids) | `externalErrors` | tableau de chaînes | Les identifiants d’erreur uniques provenant de sources externes, par exemple les erreurs CDN. |
| [[!UICONTROL Images Par Seconde]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | Entier | Vitesse d’image de la diffusion en cours (en images par seconde). |
| [[!UICONTROL ID d’erreur du SDK Media]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#media-sdk-error-ids) | `mediaSdkErrors` | tableau de chaînes | Identifiants d’erreur uniques générés par le SDK Media pendant la lecture. |
| [[!UICONTROL ID d’erreur du SDK du lecteur]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#player-sdk-error-ids) | `playerSdkErrors` | tableau de chaînes | Identifiants d’erreur uniques générés par le SDK du lecteur lors de la lecture. |
| [[!UICONTROL Événements de blocage]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#stalling-events) | `stallCount` | Entier | Nombre d’événements de blocage pendant la lecture. |
| [[!UICONTROL Flux touchés par un blocage]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#stalling-impacted-streams) | `hasStallImpactedStreams` | Booléen | Indique si les flux ont subi un blocage pendant la lecture. |
| [[!UICONTROL Temps De Démarrage]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | Entier | Durée (en secondes) entre le chargement de la vidéo et le démarrage. |
| [[!UICONTROL Durée totale de la mémoire tampon]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#total-buffer-duration-1) | `bufferTime` | Entier | Durée totale (en secondes) de mise en mémoire tampon pendant la lecture. |
| [[!UICONTROL Durée totale de blocage]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#total-stalling-duration) | `stallTime` | Entier | Durée totale (en secondes) pendant laquelle la lecture a été bloquée. |

{style="table-layout:auto"}
