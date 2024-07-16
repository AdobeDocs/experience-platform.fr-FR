---
solution: Experience Platform
title: Type de données de chaîne de consentement
description: Découvrez le type de données XDM Chaîne de consentement.
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 13%

---

# Type de données [!UICONTROL Consent String]

[!UICONTROL Consent String] est un type de données XDM standard qui décrit une valeur string qui représente le consentement d’un client. Il comprend des informations contextuelles telles que la norme pour la chaîne de consentement (par exemple, le [Transparency and Consent Framework (TCF) IAB 2.0](../field-groups/profile/iab.md)).

![](../images/data-types/consent-string.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `consentStandard` | Chaîne | La norme pour la chaîne de consentement. Cela permet de déterminer le format de la chaîne de consentement telle que définie par les services de gestion du consentement. |
| `consentStandardVersion` | Chaîne | La version de la norme de consentement, utilisée pour définir précisément le format de la chaîne de consentement tel que défini par les services de gestion du consentement. |
| `consentStringValue` | Chaîne | Chaîne de consentement complète fournie par le service de gestion du consentement. `consentStandard` et `consentStandardVersion` aident à définir comment analyser cette chaîne. |
| `containsPersonalData` | Booléen | Lorsque ce champ est défini sur true, cela signifie que cette chaîne de consentement doit être traitée pour l’application du consentement. |
| `gdprApplies` | Booléen | Lorsque ce champ est vrai, cela signifie que le consentement est fourni avec des données personnelles. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
