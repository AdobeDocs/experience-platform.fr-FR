---
title: Type de données de collecte de détails sur la qualité de l’expérience (QoE)
description: Découvrez le type de données Modèle de données d’expérience (XDM) de détails sur la qualité de l’expérience (QoE).
exl-id: d99816d9-e207-434a-9a40-ee9ded46c4d2
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 6%

---

# Type de données de collecte de données QoE (Qualité de l’expérience)

[!UICONTROL Détails des données QoE] La collection est un type de données XDM (Experience Data Model) standard qui fournit des mesures détaillées liées à la qualité de l’expérience (QoE) pendant la lecture multimédia. Utilisez le type de données de collection [!UICONTROL Détails de données QoE] pour capturer des détails tels que des informations de débit binaire, des taux d’images, des événements de mise en mémoire tampon, des images perdues, etc. Les champs de collecte de médias capturent des données et les envoient à d’autres services Adobe en vue d’un traitement ultérieur. Ce type de données permet d’analyser la qualité de lecture, ce qui permet d’obtenir des informations sur les performances de diffusion en continu, l’expérience utilisateur et les problèmes potentiels rencontrés lors des sessions de lecture.

+++Sélectionnez cette option pour afficher le type de données Détails des données QoE .
![ Diagramme du type de données de collecte de détails sur la qualité de l’expérience.](../images/data-types/qoe-data-details-collection.png)
+++

>[!NOTE]
>
>Chaque nom d’affichage contient un lien vers des informations supplémentaires sur ses paramètres audio et vidéo. Les pages liées contiennent des détails sur les données de publicité vidéo collectées par Adobe, les valeurs d’implémentation, les paramètres réseau, la création de rapports et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|-----------|---------------------------------------------------------------------------------------|
| [[!UICONTROL Débit ]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | Entier | Non | Valeur de débit binaire (en Kbits/s). |
| [[!UICONTROL Images perdues]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames) | `droppedFrames` | Entier | Non | Nombre total d’images perdues pendant la lecture. |
| [[!UICONTROL Images Par Seconde]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | Entier | Non | Vitesse d’image de la diffusion en cours (en images par seconde). |
| [[!UICONTROL Temps De Démarrage]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | Entier | Non | Durée (en secondes) entre le chargement de la vidéo et le démarrage. |

{style="table-layout:auto"}
