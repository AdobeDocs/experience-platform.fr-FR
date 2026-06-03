---
title: Type de données de rapport sur les détails des données de qualité de l’expérience (QoE)
description: Découvrez le type de données Modèle de données d’expérience (XDM) des rapports sur les détails des données de qualité de l’expérience.
exl-id: 608baa9b-12ca-466c-a962-1401abc0344e
TQID: https://experienceleague.adobe.com/PjP7J9X7NTxgltIBhKgxNVJgwVGYR76PgUe6wWOw8kA
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 139751142683b9bdfc2e8e4061eec18572d1b182
workflow-type: tm+mt
source-wordcount: 705
ht-degree: 4%

---

# Détails des données QoE (qualité de l’expérience) Type de données de rapport

[!UICONTROL QoE Data Details] Reporting est un type de données XDM (Modèle de données d’expérience) standard qui fournit des mesures détaillées liées à la qualité de l’expérience (QoE) pendant la lecture de médias. Utilisez le type de données [!UICONTROL QoE Data Details] Reporting pour capturer des informations telles que les informations de débit binaire, les débits d’images, les événements de mise en mémoire tampon, les images perdues, etc. Ce type de données permet d’analyser la qualité de la lecture, ce qui permet d’obtenir des informations sur les performances de diffusion en continu, l’expérience utilisateur et les problèmes potentiels rencontrés lors des sessions de lecture.

+++Sélectionnez cette option pour afficher le type de données Rapports sur les détails des données QoE .
![Diagramme du type de données de rapport Détails des données QoE (qualité de l’expérience).](../images/data-types/qoe-data-details-reporting.png)
+++

>[!NOTE]
>
>Ce type de données appartient au schéma `mediaReporting` : champs calculés par le serveur principal des médias en flux continu à partir des données `mediaCollection` envoyées par votre implémentation. Il s’agit des champs qu’Adobe ingère dans les jeux de données Platform. Voir [Schéma de reporting XDM des médias en flux continu](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge/reporting-schema) pour plus d’informations.

Chaque nom d’affichage contient un lien vers des informations supplémentaires sur sa dimension ou sa mesure de reporting. Les pages liées contiennent des détails sur la manière dont Adobe calcule et signale ces données, y compris les répartitions par système de rapports.

| Nom d’affichage | Propriété | Type de données | Description |
|---|---|---|---|
| [[!UICONTROL Average Bitrate]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/average-bitrate) | `bitrateAverage` | nombre | Débit moyen (en Kbits/s, entier). Calculé en tant que moyenne pondérée des valeurs de débit. |
| [[!UICONTROL Average Bitrate Bucket]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/dimensions/average-bitrate) | `bitrateAverageBucket` | chaîne | Débit moyen (en Kbits/s) classé par intervalles prédéfinis à 100 Kbits/s. |
| [[!UICONTROL Bitrate]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/quality/bitrate) | `bitrate` | entier | Valeur du débit (en Kbits/s). |
| [[!UICONTROL Bitrate Change Impacted Streams]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/bitrate-change-impacted-streams) | `hasBitrateChangeImpactedStreams` | booléen | Indique si les flux ont été affectés par les modifications de débit lors de la lecture. |
| [[!UICONTROL Bitrate Changes]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/bitrate-changes) | `bitrateChangeCount` | entier | Nombre total de modifications du débit au cours de la lecture. |
| [[!UICONTROL Buffer Events]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/buffer-events) | `bufferCount` | entier | Nombre de différents états de mémoire tampon pendant la lecture. |
| [[!UICONTROL Buffer Impacted Streams]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/buffer-impacted-streams) | `hasBufferImpactedStreams` | booléen | Indique si les flux ont été affectés par la mise en mémoire tampon lors de la lecture. |
| [[!UICONTROL Dropped Frame Impacted Streams]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/dropped-frame-impacted-streams) | `hasDroppedFrameImpactedStreams` | booléen | Indique si les flux ont été impactés par des images perdues lors de la lecture. |
| [[!UICONTROL Dropped Frames]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/dropped-frames) | `droppedFrames` | entier | Nombre total d’images perdues lors de la lecture. |
| [[!UICONTROL Drops Before Starts]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/drops-before-start) | `isDroppedBeforeStart` | booléen | Indique si les utilisateurs quittent la vidéo avant son démarrage, quelles que soient les publicités. |
| [[!UICONTROL Error Impacted Streams]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/error-impacted-streams) | `hasErrorImpactedStreams` | booléen | Indique si des flux ont rencontré des erreurs lors de la lecture. |
| [[!UICONTROL Errors]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/error-events) | `errorCount` | entier | Nombre total d’erreurs qui se sont produites lors de la lecture. |
| [[!UICONTROL External Error IDs]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/dimensions/external-error-ids) | `externalErrors` | tableau de chaînes | ID d’erreur uniques provenant de sources externes, par exemple, erreurs CDN. |
| [[!UICONTROL Frames Per Second]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/quality/frames-per-second) | `framesPerSecond` | entier | Débit d&#39;images du flux actuel (en images par seconde). |
| [!UICONTROL Media SDK Error IDs] | `mediaSdkErrors` | tableau de chaînes | ID d’erreur uniques générés en interne par l’ancien Heartbeat SDK (Media SDK 1.x-2.x) lors de la lecture. Elles ne sont plus collectées par les implémentations actuelles. |
| [[!UICONTROL Player SDK Error IDs]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/dimensions/player-sdk-error-ids) | `playerSdkErrors` | tableau de chaînes | ID d’erreur uniques générés par le SDK du lecteur lors de la lecture. |
| [[!UICONTROL Stalling Events]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/stall-events) | `stallCount` | entier | Nombre d’événements qui bloquent la lecture. |
| [[!UICONTROL Stalling Impacted Streams]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/stall-impacted-streams) | `hasStallImpactedStreams` | booléen | Indique si des flux ont été bloqués lors de la lecture. |
| [[!UICONTROL Time To Start]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/time-to-start) | `timeToStart` | entier | Durée (en secondes) entre le chargement et le démarrage de la vidéo. |
| [[!UICONTROL Total Buffer Duration]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/total-buffer-duration) | `bufferTime` | entier | Temps total (en secondes) passé à mettre en mémoire tampon pendant la lecture. |
| [[!UICONTROL Total Stalling Duration]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/total-stalling-duration) | `stallTime` | entier | Durée totale (en secondes) pendant laquelle la lecture a été bloquée. |

Voir [qoedatadetails.schema.json](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) dans le référentiel XDM public pour la définition complète du schéma.
