---
title: Groupe de champs de schéma Détails du site
description: Ce document présente un aperçu du groupe de champs de schéma Détails du site.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 13%

---

# [!UICONTROL Détails du site] groupe de champs de schéma

[!UICONTROL Détails du site] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Le groupe de champs fournit une `sitetool` vers un schéma, qui capture les informations collectées par un outil de site.

![Structure du groupe de champs](../../images/field-groups/sitetool-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `dataGatheringEvent` | Objet | Indique si cet événement est un événement de collecte de données, ainsi que d’autres détails connexes. Contient les propriétés suivantes :<ul><li>`data`: (Carte) Contient les données JSON qui sont collectées et envoyées dans le cadre d’un événement d’envoi de questionnaire, d’enquête ou de sondage.</li><li>`isTrue`: (Booléen) Indique s’il s’agit d’un événement de collecte de données comme un questionnaire, une enquête ou un sondage.</li><li>`score`: (Entier) Score obtenu par l’acteur en fonction des réponses de l’événement.</li></ul> |
| `actor` | Chaîne | Personne/membre ayant effectué l’action. |
| `actorID` | Chaîne | Identifiant unique de la personne/du membre qui a effectué l’action. |
| `isKeyEvent` | Booléen | Indique si cet événement est un événement clé. |
| `name` | Chaîne | Nom du site (chatbot, enquête, etc.). |
| `section` | Chaîne | La section appropriée de l’outil de site, comme principal ou sous-site. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous à la section [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
