---
title: Groupe de champs de schéma des détails de l’application
description: Ce document présente un aperçu du groupe de champs de schéma Détails de l’application .
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 5%

---

# [!UICONTROL Détails de l’application] groupe de champs de schéma

[!UICONTROL Détails de l’application] est un groupe de champs de schéma standard pour la variable [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Le groupe de champs fournit une `application` vers un schéma, qui capture les détails liés à l’application tels que les blocages, l’utilisation des fonctionnalités, les lancements et les mises à niveau.

![](../../images/field-groups/application-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `application` | [[!UICONTROL Application]](../../data-types/financial-account.md) | Capture les informations de l’application relatives à un événement, y compris le nom de l’application, la version de l’application, les installations, les lancements, les blocages et les fermetures. Il peut s’agir de l’application ciblée par l’événement (comme la destination d’une notification push envoyée) ou de l’application à l’origine de l’événement (un clic ou une connexion, par exemple). |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous à la section [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
