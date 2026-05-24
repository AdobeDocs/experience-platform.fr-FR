---
title: Type de données de collecte des détails de données QoE (qualité de l’expérience)
description: Découvrez le type de données de modèle de données d’expérience (XDM) du type de collecte de données Détails de la qualité de l’expérience (QoE).
exl-id: d99816d9-e207-434a-9a40-ee9ded46c4d2
TQID: https://experienceleague.adobe.com/2FE97ebiyqzEd2NKqoiJ5pNoR6hXezVbK1p6SftHOzc
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c20d46e7-1c7d-476c-a50e-3961d4dce35fid: daec7ead-f475-492a-a3b3-02ae08565d6fid: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6id: de9975b2-c43a-4287-9698-4f4cad92b83f
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 273
ht-degree: 5%

---

# Type de données de collecte des détails de données QoE (qualité de l’expérience)

[!UICONTROL QoE Data Details] collecte de données d’expérience est un type de données standard des modèles de données d’expérience (XDM) qui fournit des mesures détaillées liées à la qualité de l’expérience (QoE) pendant la lecture multimédia. Utilisez le type de données [!UICONTROL QoE Data Details] Collection pour capturer des informations telles que les informations sur le débit binaire, les débits d’images, les événements de mise en mémoire tampon, les images perdues, etc. Les champs de collecte de médias capturent des données et les envoient à d’autres services Adobe en vue d’un traitement ultérieur. Ce type de données permet d’analyser la qualité de la lecture, ce qui permet d’obtenir des informations sur les performances de diffusion en continu, l’expérience utilisateur et les problèmes potentiels rencontrés lors des sessions de lecture.

+++Sélectionnez cette option pour afficher le type de données Détails des données QoE .
![Diagramme du type de données de collecte de détails sur la qualité de l’expérience (QoE).](../images/data-types/qoe-data-details-collection.png)
+++

>[!NOTE]
>
>Chaque nom d’affichage contient un lien vers des informations supplémentaires sur ses paramètres audio et vidéo. Les pages liées contiennent des détails sur la vidéo et les données collectées par Adobe, les valeurs d’implémentation, les paramètres réseau, les rapports et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|-----------|---------------------------------------------------------------------------------------|
| [[!UICONTROL Bitrate]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | Entier | Non | Valeur du débit (en Kbits/s). |
| [[!UICONTROL Dropped Frames]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames) | `droppedFrames` | Entier | Non | Nombre total d’images perdues lors de la lecture. |
| [[!UICONTROL Frames Per Second]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | Entier | Non | Débit d&#39;images du flux actuel (en images par seconde). |
| [[!UICONTROL Time To Start]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | Entier | Non | Durée (en secondes) entre le chargement et le démarrage de la vidéo. |

{style="table-layout:auto"}
