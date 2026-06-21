---
title: Type de données de rapport des détails de chapitre
description: Découvrez le type de données Modèle de données d’expérience de création de rapports (XDM) des détails du chapitre.
exl-id: 73ebfbe3-66c3-4ef9-9944-d9cb5772127b
TQID: https://experienceleague.adobe.com/gVjIGh7CHzfTzgq-XnEzvkBiyospwk9gG8V47rst0hI
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c20d46e7-1c7d-476c-a50e-3961d4dce35fid: daec7ead-f475-492a-a3b3-02ae08565d6f
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 139751142683b9bdfc2e8e4061eec18572d1b182
workflow-type: tm+mt
source-wordcount: 374
ht-degree: 8%

---

# [!UICONTROL Détails du chapitre] Type de données de rapport

[!UICONTROL Détails du chapitre] la création de rapports est un type de données standard du modèle de données d’expérience (XDM) qui décrit divers attributs liés aux chapitres ou aux segments dans le contenu multimédia. Utilisez le type de données de rapport [!UICONTROL Détails du chapitre] pour capturer des informations telles que le nom du chapitre, la durée, la position, l’identifiant, le statut de lecture (commencé/terminé) et le temps passé sur chaque chapitre.

![Diagramme du type de données Rapports sur les détails du chapitre.](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>Ce type de données appartient au schéma `mediaReporting` : champs calculés par le serveur principal des médias en flux continu à partir des données `mediaCollection` envoyées par votre implémentation. Il s’agit des champs qu’Adobe ingère dans les jeux de données Platform. Voir [Schéma de reporting XDM des médias en flux continu](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge/reporting-schema) pour plus d’informations.

Chaque nom d’affichage contient un lien vers des informations supplémentaires sur sa dimension ou sa mesure de reporting. Les pages liées contiennent des détails sur la manière dont Adobe calcule et signale ces données, y compris les répartitions par système de rapports.

| Nom d’affichage | Propriété | Type de données | Description |
|---|---|---|---|
| [[!UICONTROL Chapitre terminé]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/chapter-completes) | `isCompleted` | booléen | Indique si le chapitre est terminé. |
| [[!UICONTROL Identifiant du chapitre]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/dimensions/chapter) | `ID` | chaîne | Identifiant généré automatiquement pour le chapitre. |
| [[!UICONTROL Longueur Ou Durée Du Chapitre]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/dimensions/chapter-length) | `length` | entier | Durée du chapitre, en secondes. |
| [[!UICONTROL Nom du chapitre]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/dimensions/chapter-name) | `friendlyName` | chaîne | Nom du chapitre et/ou du segment. |
| [[!UICONTROL décalage de chapitre]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/dimensions/chapter-offset) | `offset` | entier | Décalage du chapitre à l’intérieur du contenu (en secondes) depuis le début. |
| [[!UICONTROL Position du chapitre]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/dimensions/chapter-position) | `index` | entier | Position (index, entier) du chapitre à l’intérieur du contenu. |
| [[!UICONTROL Chapitre démarré]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/chapter-starts) | `isStarted` | booléen | Indique si le chapitre a commencé ou non. |
| [[!UICONTROL Temps de lecture du chapitre]](https://experienceleague.adobe.com/en/docs/media-analytics/using/reporting/metrics/chapter-time-spent) | `timePlayed` | entier | Temps passé sur le chapitre, en secondes. |

Voir [chapterdetails.schema.json](https://github.com/adobe/xdm/blob/master/components/datatypes/chapterdetails.schema.json) dans le référentiel XDM public pour la définition complète du schéma.
