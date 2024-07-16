---
title: Groupe de champs de schéma des détails de l’application
description: Découvrez le groupe de champs de schéma Détails de l’application .
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 3%

---

# [!UICONTROL Détails de l’application] groupe de champs de schéma

[!UICONTROL Détails de l’application] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Le groupe de champs fournit un seul objet `application` à un schéma, qui capture les détails liés à l’application tels que les blocages, l’utilisation des fonctionnalités, les lancements et les mises à niveau.

![](../../images/field-groups/application-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `application` | [[!UICONTROL Application]](../../data-types/financial-account.md) | Capture les informations de l’application relatives à un événement, y compris le nom de l’application, la version de l’application, les installations, les lancements, les blocages et les fermetures. Il peut s’agir de l’application ciblée par l’événement (comme la destination d’une notification push envoyée) ou de l’application à l’origine de l’événement (un clic ou une connexion, par exemple). |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
