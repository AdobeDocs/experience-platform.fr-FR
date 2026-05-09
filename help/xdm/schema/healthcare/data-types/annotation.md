---
title: Type de données d’annotation
description: Découvrez le type de données du modèle de données d’expérience (XDM) d’annotation.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: f46b5fb6-d64a-4a37-91f6-b470599d9130
source-git-commit: 0e902b50cce148e0fbbb8e33c227165942b08832
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 8%

---

# Type de données [!UICONTROL Annotation]

[!UICONTROL Annotation] est un type de données standard du modèle de données d’expérience (XDM) qui contient un nœud de texte avec attribution à l’auteur. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données d’annotation](../../../images/healthcare/data-types/annotation.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Author Reference] | `authorReference` | [[!UICONTROL Reference]](../data-types/reference.md) | Référence à l’auteur. |
| [!UICONTROL Author] | `authorString` | Chaîne | Personne responsable de l’annotation. |
| [!UICONTROL Text] | `text` | Chaîne | Contenu de l’annotation. |
| [!UICONTROL Time] | `time` | DateTime | Date à laquelle l’annotation a été créée. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/annotation.schema.json)
