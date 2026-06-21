---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;ExperienceEvent;champs;schémas;Schémas;Conception de schéma;groupe de champs;groupe de champs;iab;tcf;consentement;
solution: Experience Platform
title: Groupe de champs de consentement IAB TCF 2.0 pour les schémas d’événement
description: Découvrez le groupe de champs de schéma de consentement IAB TCF 2.0 pour la classe XDM ExperienceEvent.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
TQID: https://experienceleague.adobe.com/fGy0-F-1JQuZFhBhMU9A2DFVtcxQfvp9njdb8-fcNXw
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: d095671a-1355-40aa-8b5f-06c33c68080bid: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 260
ht-degree: 1%

---

# Groupe de champs [!UICONTROL Consentement IAB TCF 2.0] pour les schémas d’événement

>[!IMPORTANT]
>
>Ce document couvre le groupe de champs de schéma [!UICONTROL Consentement IAB TCF 2.0] pour la classe XDM ExperienceEvent. Ce groupe de champs ne doit être utilisé que si vous avez l’intention de suivre les événements de changement de consentement au fil du temps.
>
>Notez que les valeurs de consentement enregistrées dans les données d’événement ne sont pas respectées dans les workflows d’application automatiques. Pour que l’application automatique ait lieu, les valeurs de consentement doivent être ingérées dans la classe XDM Individual Profile et activées pour le profil client en temps réel.
>
>Pour le groupe de champs destiné à la classe XDM Individual Profile, reportez-vous plutôt au [document](../profile/iab.md) suivant.

[!UICONTROL Consentement IAB TCF 2.0] est un groupe de champs de schéma standard pour la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilisé pour capturer une série horodatée de chaînes de consentement IAB, afin de suivre les modèles de changement de consentement au fil du temps.

![](../../images/field-groups/iab-event.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `consentStrings` | Tableau de [chaînes de consentement](../../data-types/consent-string.md) | Tableau de valeurs de chaîne de consentement associées à l’événement. |

{style="table-layout:auto"}

Pour plus d’informations sur le cas d’utilisation de ce groupe de champs](../../../landing/governance-privacy-security/consent/iab/overview.md) consultez le guide sur la prise en charge d’[ IAB TCF 2.0 dans Experience Platform . Pour plus d’informations sur le groupe de champs lui-même, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
