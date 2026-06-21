---
title: Type de données de collection des détails des métadonnées personnalisées
description: Découvrez le type de données Modèle de données d’expérience (XDM) de la collecte de détails de métadonnées personnalisées.
exl-id: e2fa65ea-b738-43c6-90f1-1968dd83b963
TQID: https://experienceleague.adobe.com/hYfRmp81jY1jrSqnXT9yEh-bXRHl6ordf3HtU25emuM
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 139751142683b9bdfc2e8e4061eec18572d1b182
workflow-type: tm+mt
source-wordcount: 176
ht-degree: 9%

---

# [!UICONTROL Détails des métadonnées personnalisées] Type de données de collection

[!UICONTROL Détails des métadonnées personnalisées] la collecte est un type de données standard du modèle de données d’expérience (XDM) qui définit une structure de stockage des métadonnées personnalisées. Utilisez le type de données de collection [!UICONTROL Détails de métadonnées personnalisés] pour capturer des informations telles que le nom et la valeur des métadonnées personnalisées associées au contenu ou aux interactions.

+++Sélectionnez cette option pour afficher un diagramme du type de données Collection [!UICONTROL Détails des métadonnées personnalisées].
![Diagramme du type de données Collection de détails de métadonnées personnalisées.](../images/data-types/the-custom-metadata-collection.png)
+++

>[!NOTE]
>
>Ce type de données appartient au schéma `mediaCollection`, à savoir les champs que votre implémentation envoie au serveur principal des médias en flux continu. Adobe traite ces données et génère les champs de `mediaReporting` correspondants, qui sont ingérés dans les jeux de données Platform. Voir [Schéma de reporting XDM des médias en flux continu](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge/reporting-schema) pour plus d’informations.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|---|---|---|---|---|
| [!UICONTROL Nom de champ de métadonnées personnalisé] | `name` | string | Non | Nom du champ personnalisé. |
| [!UICONTROL Valeur de champ de métadonnées personnalisé] | `value` | string | Non | Valeur du champ personnalisé. |
