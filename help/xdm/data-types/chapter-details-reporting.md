---
title: Type de données de rapport sur les détails du chapitre
description: Découvrez le type de données XDM (Modèle de données d’expérience de création de rapports de détails du chapitre).
exl-id: 73ebfbe3-66c3-4ef9-9944-d9cb5772127b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 8%

---

# [!UICONTROL Détails du chapitre] Type de données de rapport

[!UICONTROL Détails du chapitre] La création de rapports est un type de données XDM (Experience Data Model) standard qui décrit divers attributs liés aux chapitres ou aux segments dans le contenu multimédia. Utilisez le type de données de rapport [!UICONTROL Détails du chapitre] pour capturer des détails tels que le nom, la durée, la position, l’identifiant, l’état de lecture (démarré/terminé) et la durée passée sur chaque chapitre. Les champs de création de rapports multimédia sont utilisés par les services Adobe pour analyser les champs Media Collection envoyés par les utilisateurs. Ces données, ainsi que d’autres mesures utilisateur spécifiques, sont calculées et font l’objet de rapports.

![ Diagramme du type de données de rapport Détails du chapitre.](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>Chaque nom d’affichage contient un lien vers des informations supplémentaires sur ses paramètres audio et vidéo. Les pages liées contiennent des détails sur les données de publicité vidéo collectées par Adobe, les valeurs d’implémentation, les paramètres réseau, la création de rapports et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Description |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|--------------------------------------------------------------|
| [[!UICONTROL Chapitre terminé]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-complete) | `isCompleted` | Booléen | Indique si le chapitre est terminé ou non. |
| [[!UICONTROL ID de chapitre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter) | `ID` | Chaîne | Identifiant généré automatiquement du chapitre. |
| [[!UICONTROL Durée Ou Durée Du Chapitre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | Entier | Durée du chapitre, en secondes. |
| [[!UICONTROL Nom du chapitre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | Chaîne | Nom du chapitre et/ou du segment. |
| [[!UICONTROL Décalage de chapitre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | Entier | Décalage du chapitre dans le contenu (en secondes) à partir du début. |
| [[!UICONTROL Position du chapitre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | Entier | Position (index, entier) du chapitre dans le contenu. |
| [[!UICONTROL Chapitre commencé]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-start) | `isStarted` | Booléen | Indique si le chapitre a commencé ou non. |
| [[!UICONTROL Durée de lecture du chapitre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-time-spent) | `timePlayed` | Entier | Temps passé sur le chapitre, en secondes. |
