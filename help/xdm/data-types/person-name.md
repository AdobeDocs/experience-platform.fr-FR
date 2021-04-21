---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; fullName ; xdm:fullName ; nom de la personne ; nom ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données du nom de personne
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM du nom de personne.
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 21%

---

# [!UICONTROL Type de données de ] nom de personne

[!UICONTROL Le ] nom de personne est un type de données XDM standard qui décrit le nom complet d’une personne. Comme les conventions relatives aux structures de noms diffèrent considérablement d’une langue ou d’une culture à l’autre, les noms doivent toujours être modélisés à l’aide de ce type de données.

En outre, le type de données fournit un certain nombre de propriétés facultatives qui peuvent être utilisées dans les situations qui nécessitent l’utilisation d’un fragment du nom complet, comme la création d’un message d’accueil formel ou informel.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Propriété | Description |
| --- | --- |
| `courtesyTitle` | Abréviation du titre, de l&#39;honneur ou de la formule de politesse d&#39;une personne (par exemple `Mr.`, `Miss.` ou `Dr.`). |
| `firstName` | Premier segment du nom dans l’ordre d’écriture et le plus communément accepté dans la langue du nom. |
| `fullName` | Le nom complet de la personne, dans l&#39;ordre écrit le plus communément accepté dans la langue du nom. |
| `lastName` | Dernier segment du nom dans l’ordre d’écriture et le plus communément accepté dans la langue du nom. |
| `middleName` | Nom intermédiaire, nom alternatif ou noms supplémentaires présents entre le prénom et le nom. |
| `suffix` | Groupe de lettres fournies après le nom d&#39;une personne pour fournir des informations supplémentaires (par exemple `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`, etc.). |

Pour plus d&#39;informations sur le type de données de nom de personne, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.schema.json)
