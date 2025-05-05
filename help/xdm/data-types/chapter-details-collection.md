---
title: Type de données de collecte des détails du chapitre
description: Découvrez le type de données XDM (Modèle de données d’expérience de collecte de détails de chapitre).
exl-id: 4f841f5a-3840-4da5-a3a4-ceecde87c684
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 11%

---

# [!UICONTROL Détails du chapitre] Type de données de collection

[!UICONTROL Détails du chapitre] La collection est un type de données XDM (Experience Data Model) standard qui décrit divers attributs liés aux chapitres ou aux segments dans le contenu multimédia. Utilisez le type de données Collection [!UICONTROL Détails du chapitre] pour capturer des détails tels que le nom du chapitre, le décalage, la durée et l’index du chapitre. Les champs de collecte de médias capturent des données et les envoient à d’autres services Adobe en vue d’un traitement ultérieur.

![Schéma du type de données Collecte de détails du chapitre.](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>Chaque nom d’affichage contient un lien vers des informations supplémentaires sur ses paramètres audio et vidéo. Les pages liées contiennent des détails sur les données de publicité vidéo collectées par Adobe, les valeurs d’implémentation, les paramètres réseau, la création de rapports et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|----------|---------------------------------------------------|
| [[!UICONTROL Durée Ou Durée Du Chapitre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=fr#chapter-length) | `length` | Entier | Oui | Durée du chapitre, en secondes. |
| [[!UICONTROL Nom du chapitre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=fr#chapter-name) | `friendlyName` | Chaîne | Non | Nom du chapitre et/ou du segment. |
| [[!UICONTROL Décalage de chapitre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=fr#chapter-offset) | `offset` | Entier | Oui | Décalage du chapitre dans le contenu (en secondes) à partir du début. |
| [[!UICONTROL Position du chapitre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html?lang=fr#chapter-position) | `index` | Entier | Oui | Position (index, entier) du chapitre dans le contenu. |

{style="table-layout:auto"}
