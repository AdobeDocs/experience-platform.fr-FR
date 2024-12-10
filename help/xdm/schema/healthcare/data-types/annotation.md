---
title: Type de données d’annotation
description: Découvrez le type de données du modèle de données d’expérience d’annotation (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: f46b5fb6-d64a-4a37-91f6-b470599d9130
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---

# Type de données [!UICONTROL Annotation]

[!UICONTROL Annotation] est un type de données XDM (Experience Data Model) standard qui contient un noeud de texte avec attribution à l’auteur. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données d’annotation](../../../images/healthcare/data-types/annotation.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Référence de l’auteur] | `authorReference` | [[!UICONTROL Référence]](../data-types/reference.md) | Référence à l’auteur. |
| [!UICONTROL Auteur] | `authorString` | Chaîne | Personne responsable de l’annotation. |
| [!UICONTROL Texte] | `text` | Chaîne | Contenu de l’annotation. |
| [!UICONTROL Heure] | `time` | DateTime | Lorsque l’annotation a été faite. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
