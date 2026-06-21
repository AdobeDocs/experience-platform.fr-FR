---
solution: Experience Platform
title: Type de données de chaîne de consentement
description: Découvrez le type de données XDM de chaîne de consentement.
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
TQID: https://experienceleague.adobe.com/2HaTtDeP-lJSF25z7wqRfUjPSHhXPEZV9vD9gPBhGvk
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 196
ht-degree: 4%

---

# [!UICONTROL Chaîne de consentement] type de données

[!UICONTROL &#x200B; Chaîne de consentement &#x200B;] est un type de données XDM standard qui décrit une valeur de chaîne représentant le consentement d’un client. Il comprend des informations contextuelles telles que la norme pour la chaîne de consentement (par exemple, le [&#x200B; IAB Transparency and Consent Framework (TCF) 2.0](../field-groups/profile/iab.md)).

![](../images/data-types/consent-string.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `consentStandard` | Chaîne | Norme de la chaîne de consentement. Cela permet de déterminer le format de la chaîne de consentement telle que définie par les services de gestion du consentement. |
| `consentStandardVersion` | Chaîne | Version de la norme de consentement utilisée pour définir précisément le format de la chaîne de consentement telle qu’elle est définie par les services de gestion du consentement. |
| `consentStringValue` | Chaîne | Chaîne de consentement complète fournie par le service de gestion du consentement. `consentStandard` et `consentStandardVersion` permettent de définir comment analyser cette chaîne. |
| `containsPersonalData` | Booléen | Lorsque ce champ est défini sur « true », cela signifie que cette chaîne de consentement doit être traitée pour l’application du consentement. |
| `gdprApplies` | Booléen | Lorsque ce champ est défini sur « vrai », cela signifie que le consentement s’accompagne de données personnelles. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
