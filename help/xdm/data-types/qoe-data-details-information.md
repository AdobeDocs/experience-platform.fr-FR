---
title: Données QoE (Qualité de l’expérience) Détails Type de données
description: Découvrez le type de données QoE (Qualité de l’expérience) Détails Informations Type de données Modèle de données d’expérience (XDM) .
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 6%

---

# Données QoE (Qualité de l’expérience) Détails Type de données Informations

[!UICONTROL Informations détaillées sur les données QoE] est un type de données XDM (Experience Data Model) standard qui fournit des mesures détaillées liées à la qualité de l’expérience (QoE) pendant la lecture multimédia. Utilisez la variable [!UICONTROL Informations détaillées sur les données QoE] type de données pour capturer des détails tels que les informations de débit binaire, les taux d’images, les événements de mise en mémoire tampon, les images perdues, etc. Ce type de données permet d’analyser la qualité de lecture, ce qui permet d’obtenir des informations sur les performances de diffusion en continu, l’expérience utilisateur et les problèmes potentiels rencontrés lors des sessions de lecture.

+++Sélectionnez cette option pour afficher le type de données Informations sur les détails des données QoE.
![Schéma du type de données Informations sur les détails de la qualité de l’expérience (QoE).](../images/data-types/qoe-data-details-information.png)
+++

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------------------------|----------------------------|-----------|--------------------------------------------------------------------------------------------------|
| [!UICONTROL Intervalle de débit moyen] | `bitrateAverageBucket` | chaîne | Débit moyen (en Kbits/s) catégorisé dans des intervalles prédéfinis à des intervalles de 100 Kbits/s. |
| [!UICONTROL Débit binaire] | `bitrate` | nombre entier | Valeur de débit binaire (en Kbits/s). |
| [!UICONTROL Débit moyen] | `bitrateAverage` | nombre | Débit moyen (en Kbits/s, nombre entier). Calculé en tant que moyenne pondérée des valeurs de débit binaire. |
| [!UICONTROL Flux touchés par les changements de débit] | `hasBitrateChangeImpactedStreams` | booléen | Indique si les flux ont été affectés par les changements de débit au cours de la lecture. |
| [!UICONTROL Changements de débit] | `bitrateChangeCount` | nombre entier | Le nombre total de changements de débit binaire au cours de la lecture. |
| [!UICONTROL Flux touchés par la perte d’images] | `hasDroppedFrameImpactedStreams` | booléen | Indique si les diffusions ont été affectées par les pertes d’images au cours de la lecture. |
| [!UICONTROL Perte d’images] | `droppedFrames` | nombre entier | Nombre total d’images perdues pendant la lecture. |
| [!UICONTROL Pertes avant le début] | `isDroppedBeforeStart` | booléen | Indique si les utilisateurs quittent la vidéo avant de la démarrer, quelles que soient les publicités. |
| [!UICONTROL Images par seconde] | `framesPerSecond` | nombre entier | Vitesse d’image de la diffusion en cours (en images par seconde). |
| [!UICONTROL Temps jusqu’au début] | `timeToStart` | nombre entier | Durée (en secondes) entre le chargement de la vidéo et le démarrage. |
| [!UICONTROL Flux touchés par la mémoire tampon] | `hasBufferImpactedStreams` | booléen | Indique si les diffusions ont été affectées par la mise en mémoire tampon pendant la lecture. |
| [!UICONTROL Événements de mémoire tampon] | `bufferCount` | nombre entier | Nombre d’états de mémoire tampon différents pendant la lecture. |
| [!UICONTROL Durée totale de la mémoire tampon] | `bufferTime` | nombre entier | Durée totale (en secondes) de mise en mémoire tampon pendant la lecture. |
| [!UICONTROL Flux touchés par les erreurs] | `hasErrorImpactedStreams` | booléen | Indique si les flux ont rencontré des erreurs au cours de la lecture. |
| [!UICONTROL Erreurs] | `errorCount` | nombre entier | Nombre total d’erreurs qui se sont produites au cours de la lecture. |
| [!UICONTROL Flux touchés par un blocage] | `hasStallImpactedStreams` | booléen | Indique si les flux ont subi un blocage pendant la lecture. |
| [!UICONTROL Événements de blocage] | `stallCount` | nombre entier | Nombre d’événements de blocage pendant la lecture. |
| [!UICONTROL Durée totale de blocage] | `stallTime` | nombre entier | Durée totale (en secondes) pendant laquelle la lecture a été bloquée. |
| [!UICONTROL ID d’erreur du SDK du lecteur] | `playerSdkErrors` | tableau de chaînes | Identifiants d’erreur uniques générés par le SDK du lecteur lors de la lecture. |
| [!UICONTROL ID d’erreur externe] | `externalErrors` | tableau de chaînes | Les identifiants d’erreur uniques provenant de sources externes, par exemple les erreurs CDN. |
| [!UICONTROL ID d’erreur du SDK Media] | `mediaSdkErrors` | tableau de chaînes | Identifiants d’erreur uniques générés par le SDK Media pendant la lecture. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json).

