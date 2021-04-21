---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; ExperienceEvent ; champs ; schémas ; Schémas ; conception de Schéma ; mixin ; mixin ; enduserids ; utilisateur final ; ids ; id ;
solution: Experience Platform
title: Mélange de détails d’ID d’utilisateur final
topic-legacy: overview
description: Ce document présente un aperçu du mixin Détails de l’ID d’utilisateur final.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 6%

---

# [!UICONTROL ID utilisateur final ] Détailsmixin

>[!NOTE]
>
>Les noms de plusieurs mixins ont changé. Pour plus d’informations, consultez le document [Mises à jour du nom de mixin](../name-updates.md).

[!UICONTROL ID utilisateur final ] Détail d&#39;un mixin standard pour la  [[!DNL XDM ExperienceEvent] classe](../../classes/individual-profile.md), utilisé pour décrire les informations d&#39;identité d&#39;une personne dans plusieurs applications d&#39;Adobe. Le mixin fournit un objet de niveau racine `endUserIDs`, qui contient lui-même un champ `_experience` en lecture seule dont les valeurs sont automatiquement mises à jour au fur et à mesure que les données sont ingérées.

<img src="../../images/mixins/enduserids.png" width="700" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `aacustomid` | [Identité](../../data-types/identity.md) | Identifiants d’utilisateur final personnalisés pour Adobe Analytics Cloud. |
| `aaid` | [Identité](../../data-types/identity.md) | ID d’utilisateur final pour Adobe Analytics Cloud. |
| `acid` | [Identité](../../data-types/identity.md) | ID d’utilisateur final pour Adobe Campaign. |
| `adcloud` | [Identité](../../data-types/identity.md) | ID d’utilisateur final pour Adobe Advertising Cloud. |
| `emailid` | [Identité](../../data-types/identity.md) | ID d’adresse électronique. |
| `mcid` | [Identité](../../data-types/identity.md) | ID Adobe Marketing Cloud. |
| `phonenumberid` | [Identité](../../data-types/identity.md) | ID de numéro de téléphone. |
| `tntid` | [Identité](../../data-types/identity.md) | ID d’utilisateur final pour Adobe Target. |

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
