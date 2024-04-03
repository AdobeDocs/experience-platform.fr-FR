---
title: Type de données de collecte de détails sur la qualité de l’expérience (QoE)
description: Découvrez le type de données Modèle de données d’expérience (XDM) de détails sur la qualité de l’expérience (QoE).
source-git-commit: e1c94635b691c68de6154d19e974bfdf2e250923
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 6%

---

# Type de données de collecte de données QoE (Qualité de l’expérience)

[!UICONTROL Détails des données QoE] La collecte est un type de données XDM (Experience Data Model) standard qui fournit des mesures détaillées liées à la qualité de l’expérience (QoE) pendant la lecture multimédia. Utilisez la variable [!UICONTROL Détails des données QoE] Type de données de collection pour capturer des détails tels que les informations de débit binaire, les taux d’images, les événements de mise en mémoire tampon, les images perdues, etc. Les champs de collecte de médias capturent des données et les envoient à d’autres services Adobe en vue d’un traitement ultérieur. Ce type de données permet d’analyser la qualité de lecture, ce qui permet d’obtenir des informations sur les performances de diffusion en continu, l’expérience utilisateur et les problèmes potentiels rencontrés lors des sessions de lecture.

+++Sélectionnez cette option pour afficher le type de données Détails des données QoE .
![Schéma du type de données de collecte des détails sur la qualité de l’expérience (QoE).](../images/data-types/qoe-data-details-collection.png)
+++

>[!NOTE]
>
>Chaque nom d’affichage contient un lien vers des informations supplémentaires sur ses paramètres audio et vidéo. Les pages liées contiennent des détails sur les données de publicité vidéo collectées par Adobe, les valeurs d’implémentation, les paramètres réseau, la création de rapports et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|-----------|---------------------------------------------------------------------------------------|
| [[!UICONTROL Débit binaire]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | Entier | Non | Valeur de débit binaire (en Kbits/s). |
| [[!UICONTROL Perte d’images]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames) | `droppedFrames` | Entier | Non | Nombre total d’images perdues pendant la lecture. |
| [[!UICONTROL Images par seconde]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | Entier | Non | Vitesse d’image de la diffusion en cours (en images par seconde). |
| [[!UICONTROL Temps jusqu’au début]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | Entier | Non | Durée (en secondes) entre le chargement de la vidéo et le démarrage. |

{style="table-layout:auto"}
