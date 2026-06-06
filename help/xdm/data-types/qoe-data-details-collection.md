---
title: Type de données de collecte des détails de données QoE (qualité de l’expérience)
description: Découvrez le type de données de modèle de données d’expérience (XDM) du type de collecte de données Détails de la qualité de l’expérience (QoE).
exl-id: d99816d9-e207-434a-9a40-ee9ded46c4d2
TQID: https://experienceleague.adobe.com/2FE97ebiyqzEd2NKqoiJ5pNoR6hXezVbK1p6SftHOzc
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6
  - id: de9975b2-c43a-4287-9698-4f4cad92b83f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 139751142683b9bdfc2e8e4061eec18572d1b182
workflow-type: tm+mt
source-wordcount: 352
ht-degree: 4%

---

# Type de données de collecte des détails de données QoE (qualité de l’expérience)

La collecte de [!UICONTROL QoE Data Details] est un type de données standard du modèle de données d’expérience (XDM) qui fournit des mesures détaillées liées à la qualité de l’expérience (QoE) pendant la lecture de médias. Utilisez le type de données [!UICONTROL QoE Data Details] Collection pour capturer des informations telles que les informations sur le débit binaire, les débits d’images, les événements de mise en mémoire tampon, les images perdues, etc. Ce type de données permet d’analyser la qualité de la lecture, ce qui permet d’obtenir des informations sur les performances de diffusion en continu, l’expérience utilisateur et les problèmes potentiels rencontrés lors des sessions de lecture.

>[!NOTE]
>
>Ce type de données appartient au schéma `mediaCollection`, à savoir les champs que votre implémentation envoie au serveur principal des médias en flux continu. Adobe traite ces données et génère les champs de `mediaReporting` correspondants, qui sont ingérés dans les jeux de données Platform. Voir [Schéma de reporting XDM des médias en flux continu](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/edge/reporting-schema) pour plus d’informations.

>[!NOTE]
>
>Ce type de données capture uniquement les quatre champs envoyés par l’implémenteur. Adobe calcule des agrégats QoE supplémentaires (notamment le débit moyen, le nombre de tampons, les événements de blocage, le nombre d’erreurs et les mesures de flux affectées) à partir des données d’événement au cours de la session. Ces champs calculés sont disponibles dans le type de données [Rapports sur les détails des données QoE](./qoe-data-details-reporting.md).

+++Sélectionnez cette option pour afficher le type de données Détails des données QoE .
![Diagramme du type de données de collecte de détails sur la qualité de l’expérience (QoE).](../images/data-types/qoe-data-details-collection.png)
+++

Chaque nom d’affichage contient un lien vers des informations supplémentaires sur sa variable d’implémentation. Les pages liées contiennent des détails sur les données collectées par Adobe, les valeurs d’implémentation, les paramètres réseau et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|---|---|---|---|---|
| [[!UICONTROL Bitrate]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/variables/quality/bitrate) | `bitrate` | entier | Non | Valeur du débit (en Kbits/s). |
| [[!UICONTROL Dropped Frames]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/variables/quality/dropped-frames) | `droppedFrames` | entier | Non | Nombre total d’images perdues lors de la lecture. |
| [[!UICONTROL Frames Per Second]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/variables/quality/frames-per-second) | `framesPerSecond` | entier | Non | Débit d&#39;images du flux actuel (en images par seconde). |
| [[!UICONTROL Time To Start]](https://experienceleague.adobe.com/fr/docs/media-analytics/using/implementation/variables/quality/time-to-start) | `timeToStart` | entier | Non | Durée (en secondes) entre le chargement et le démarrage de la vidéo. |
