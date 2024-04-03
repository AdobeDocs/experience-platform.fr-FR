---
title: Type de données de collecte des détails du chapitre
description: Découvrez le type de données XDM (Modèle de données d’expérience de collecte de détails de chapitre).
source-git-commit: c6108bb692c80c79e115ac7b1488d95a7039ffcf
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 11%

---

# [!UICONTROL Détails du chapitre] Type de données de collecte

[!UICONTROL Détails du chapitre] Collection est un type de données XDM (Experience Data Model) standard qui décrit divers attributs liés aux chapitres ou aux segments dans le contenu multimédia. Utilisez la variable [!UICONTROL Détails du chapitre] Type de données de collection pour capturer des détails tels que le nom, le décalage, la durée et l’index de chapitre. Les champs de collecte de médias capturent des données et les envoient à d’autres services Adobe en vue d’un traitement ultérieur.

![Schéma du type de données Collection de détails du chapitre.](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>Chaque nom d’affichage contient un lien vers des informations supplémentaires sur ses paramètres audio et vidéo. Les pages liées contiennent des détails sur les données de publicité vidéo collectées par Adobe, les valeurs d’implémentation, les paramètres réseau, la création de rapports et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|----------|---------------------------------------------------|
| [[!UICONTROL Durée Ou Durée Du Chapitre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | Entier | Oui | Durée du chapitre, en secondes. |
| [[!UICONTROL Nom du chapitre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | Chaîne | Non | Nom du chapitre et/ou du segment. |
| [[!UICONTROL Décalage de chapitre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | Entier | Oui | Décalage du chapitre dans le contenu (en secondes) à partir du début. |
| [[!UICONTROL Position du chapitre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | Entier | Oui | Position (index, entier) du chapitre dans le contenu. |

{style="table-layout:auto"}
