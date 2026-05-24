---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;profil individuel;champs;schémas;Schémas;identityMap;mappage d’identités;Mappage d’identités;conception de schéma;mappage;Mappage;schéma d’union;union
title: Groupe de champs de schéma IdentityMap
description: En savoir plus sur la classe XDM Individual Profile.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
TQID: https://experienceleague.adobe.com/-NasT5qGLXk1qJ0HKOROQM-tv1QOZS8vWOw5FCg6TpY
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 153
ht-degree: 60%

---

# [!UICONTROL IdentityMap] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL IdentityMap] est un groupe de champs de schéma standard pour la classe [[!UICONTROL XDM ExperienceEvent] et un groupe de champs compatible ](../../classes/experienceevent.md) la classe [[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md). Le groupe de champs fournit un champ de mappage unique, qui contient un ensemble d’identités utilisateur saisies par espace de noms.

![Diagramme du groupe de champs de schéma [!UICONTROL IdentityMap]](../../images/field-groups/identitymap.png)

Pour plus d’informations sur les cas d’utilisation des mappages dʼidentités et leurs avantages et inconvénients, consultez la section correspondante sur la page consacrée aux [principes de base de la composition des schémas](../../schema/composition.md#identityMap).

**exemple**

```JSON
{
    "identityMap":{
        "ECID":[
            {
                "id":"83238819066235616291057085344313877718",
                "authenticatedState":"ambiguous",
                "primary":true
            }
        ]
    }
}
```

Pour plus d’informations sur le groupe de champs, reportez-vous au [schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/identitymap.schema.json) dans le référentiel XDM public.
