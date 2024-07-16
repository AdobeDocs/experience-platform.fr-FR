---
keywords: Experience Platform;accueil;rubriques populaires;schéma;schéma;XDM;champs;schémas;schémas;fullName;xdm:fullName;nom de personne;nom;type de données;type de données;type de données;type de données
solution: Experience Platform
title: Type de données du nom de personne
description: Découvrez le type de données XDM du nom de la personne.
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 6%

---

# Type de données [!UICONTROL Person name]

[!UICONTROL Person name] est un type de données XDM standard qui décrit le nom complet d’une personne. Comme les conventions pour les structures de noms diffèrent largement selon les langues et les cultures, les noms doivent toujours être modélisés à l’aide de ce type de données.

En outre, le type de données fournit un certain nombre de propriétés facultatives qui peuvent être utilisées dans les situations qui nécessitent l’utilisation d’un fragment seulement du nom complet, comme la création d’un message de bienvenue formel ou informel.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Propriété | Description |
| --- | --- |
| `courtesyTitle` | Abréviation du titre, de l’honneur ou de la formule de salutation d’une personne (par exemple, `Mr.`, `Miss.` ou `Dr.`). |
| `firstName` | Premier segment du nom dans l’ordre d’écriture le plus communément accepté dans la langue du nom. |
| `fullName` | Nom complet de la personne, dans l’ordre d’écriture le plus communément accepté dans la langue du nom. |
| `lastName` | Dernier segment du nom dans l’ordre d’écriture le plus communément accepté dans la langue du nom. |
| `middleName` | Nom intermédiaire, nom alternatif ou noms supplémentaires présents entre le prénom et le nom. |
| `suffix` | Groupe de lettres fournies après le nom d’une personne pour fournir des informations supplémentaires (telles que `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`, etc.). |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données du nom de la personne, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
