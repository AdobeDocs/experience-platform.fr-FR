---
title: Type de données de collection des détails du chapitre
description: Découvrez le type de données du modèle de données d’expérience (XDM) de la collecte de détails du chapitre.
exl-id: 4f841f5a-3840-4da5-a3a4-ceecde87c684
TQID: https://experienceleague.adobe.com/AYGm5Fukn217Iy-VFH3eElGipFWVdJSxqKctxth7API
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 139751142683b9bdfc2e8e4061eec18572d1b182
workflow-type: tm+mt
source-wordcount: 268
ht-degree: 8%

---

# [!UICONTROL Détails du chapitre] Type de données de collection

[!UICONTROL Détails du chapitre] la collection est un type de données standard du modèle de données d’expérience (XDM) qui décrit divers attributs liés aux chapitres ou aux segments dans le contenu multimédia. Utilisez le type de données de collection [!UICONTROL Détails du chapitre] pour capturer des informations telles que le nom du chapitre, le décalage, la durée et l’index de chapitre.

![Diagramme du type de données de collection Détails du chapitre.](../images/data-types/chapter-details-collection.png)

>[!NOTE]
>
>Ce type de données appartient au schéma `mediaCollection`, à savoir les champs que votre implémentation envoie au serveur principal des médias en flux continu. Adobe traite ces données et génère les champs de `mediaReporting` correspondants, qui sont ingérés dans les jeux de données Platform. Voir [Schéma de reporting XDM des médias en flux continu](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge/reporting-schema) pour plus d’informations.

Chaque nom d’affichage contient un lien vers des informations supplémentaires sur sa variable d’implémentation. Les pages liées contiennent des détails sur les données collectées par Adobe, les valeurs d’implémentation, les paramètres réseau et des considérations importantes.

| Nom d’affichage | Propriété | Type de données | Obligatoire | Description |
|---|---|---|---|---|
| [[!UICONTROL Longueur Ou Durée Du Chapitre]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/chapters/chapter-length) | `length` | Entier | Oui | Durée du chapitre, en secondes. |
| [[!UICONTROL Nom du chapitre]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/chapters/chapter-name) | `friendlyName` | string | Non | Nom du chapitre et/ou du segment. |
| [[!UICONTROL décalage de chapitre]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/chapters/chapter-offset) | `offset` | Entier | Oui | Décalage du chapitre à l’intérieur du contenu (en secondes) depuis le début. |
| [[!UICONTROL Position du chapitre]](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/variables/chapters/chapter-position) | `index` | Entier | Oui | Position (index, entier) du chapitre à l’intérieur du contenu. |
