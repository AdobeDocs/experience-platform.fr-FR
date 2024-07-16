---
title: Groupe de champs de schéma Détails du site
description: Découvrez le groupe de champs de schéma Détails du site.
exl-id: 472c0a3f-efda-49af-9490-f2de90b348c0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 6%

---

# [!UICONTROL Détails du site] groupe de champs de schéma

[!UICONTROL Sitetool Details] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Le groupe de champs fournit un seul objet `sitetool` à un schéma, qui capture les informations collectées par un outil de site.

![Structure de groupe de champs](../../images/field-groups/sitetool-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `dataGatheringEvent` | Objet | Indique si cet événement est un événement de collecte de données, ainsi que d’autres détails connexes. Contient les propriétés suivantes :<ul><li>`data` : (carte) contient les données JSON collectées et envoyées dans le cadre d’un événement d’envoi de questionnaire, d’enquête ou de sondage.</li><li>`isTrue` : (booléen). Indique s’il s’agit d’un événement de collecte de données comme un questionnaire, une enquête ou un sondage.</li><li>`score` : (entier) score obtenu par l’acteur en fonction des réponses de l’événement.</li></ul> |
| `actor` | Chaîne | Personne/membre ayant effectué l’action. |
| `actorID` | Chaîne | Identifiant unique de la personne/du membre qui a effectué l’action. |
| `isKeyEvent` | Booléen | Indique si cet événement est un événement clé. |
| `name` | Chaîne | Nom du site (chatbot, enquête, etc.). |
| `section` | Chaîne | La section appropriée de l’outil de site, comme principal ou sous-site. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json).
