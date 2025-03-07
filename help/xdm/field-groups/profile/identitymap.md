---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;profil individuel;champs;schémas;Schémas;identityMap;mappage d’identités;Mappage d’identités;conception de schéma;mappage;Mappage;schéma d’union;union
title: Groupe de champs de schéma IdentityMap
description: En savoir plus sur la classe XDM Individual Profile.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
source-git-commit: cfa3e5c6811f148376a2d2012f5687be6fad2299
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 63%

---

# Groupe de champs de schéma [!UICONTROL IdentityMap]

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL IdentityMap] est un groupe de champs de schéma standard pour la classe [[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md) et un groupe de champs compatible pour la classe [[!UICONTROL XDM Individual Profile]](../../classes/individual-profile.md). Le groupe de champs fournit un champ de mappage unique, qui contient un ensemble d’identités utilisateur saisies par espace de noms.

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
