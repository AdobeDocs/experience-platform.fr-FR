---
title: Type De Données De Collecte Des Détails D’Erreur
description: Découvrez le type de données Modèle de données d’expérience (XDM) de la collecte de détails d’erreur .
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
TQID: https://experienceleague.adobe.com/KtHPa-G4F0I0GXeTg7XfgRdwQv33y8Yy2xSlTh0fjwE
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 139751142683b9bdfc2e8e4061eec18572d1b182
workflow-type: tm+mt
source-wordcount: 237
ht-degree: 8%

---

# [!UICONTROL Détails de l’erreur] Type de données de collection

[!UICONTROL Détails de l’erreur] la collecte est un type de données standard du modèle de données d’expérience (XDM) qui décrit les détails de l’erreur. Utilisez le type de données de collection [!UICONTROL Détails de l’erreur] pour capturer les détails de la source de l’erreur et de l’identification. L’ID d’erreur identifie l’erreur et la source de l’erreur indique si elle provient du lecteur ou d’une source externe (telle qu’un réseau CDN). Les agrégats d’erreurs calculés, notamment le nombre d’erreurs, les flux impactés et les tableaux d’ID d’erreur, sont disponibles dans le type de données [Rapports sur les détails des données de la qualité de service](./qoe-data-details-reporting.md).

+++Sélectionnez cette option pour afficher un diagramme du type de données Collection [!UICONTROL Détails de l’erreur].
![Diagramme du type de données de collecte des détails de l’erreur.](../images/data-types/error-details-collection.png)
+++

>[!NOTE]
>
>Ce type de données appartient au schéma `mediaCollection`, à savoir les champs que votre implémentation envoie au serveur principal des médias en flux continu. Adobe traite ces données et génère les champs de `mediaReporting` correspondants, qui sont ingérés dans les jeux de données Platform. Voir [Schéma de reporting XDM des médias en flux continu](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge/reporting-schema) pour plus d’informations.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|---|---|---|---|---|
| [!UICONTROL ID d’erreur] | `name` | string | Non | ID de l’erreur. |
| [!UICONTROL Erreur Source] | `source` | string | Non | Source de l’erreur. Utilisez « lecteur » pour les erreurs générées par le lecteur multimédia lui-même et « externe » pour les erreurs provenant de l’extérieur du lecteur, telles que les erreurs CDN. |

Voir [errordetails.schema.json](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) dans le référentiel XDM public pour la définition complète du schéma.
