---
title: Groupe de champs de schéma des détails de l’application
description: Découvrez le groupe de champs de schéma Détails de l’application .
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
TQID: https://experienceleague.adobe.com/LRyLsquiVHsY8HDAUGoOimEhs1lTJ9pYLdOm7-sgptM
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 131
ht-degree: 3%

---

# [!UICONTROL Application Details] groupe de champs de schéma

[!UICONTROL Application Details] groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). Le groupe de champs fournit un seul objet `application` à un schéma, qui capture les détails liés à l’application, tels que les blocages, l’utilisation des fonctionnalités, les lancements et les mises à niveau.

![](../../images/field-groups/application-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `application` | [[!UICONTROL Application]](../../data-types/financial-account.md) | Capture les informations sur l’application associées à un événement, y compris le nom de l’application, sa version, les installations, les lancements, les blocages et les fermetures. Il peut s’agir de l’application ciblée par l’événement (comme la destination d’une notification push envoyée) ou de l’application d’où provient l’événement (comme un clic ou une connexion). |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
