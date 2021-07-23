---
keywords: Experience Platform;accueil;rubriques populaires;schéma;schéma;XDM;champs;schémas;schémas;fullName;xdm:fullName;nom de personne;nom;type de données;type de données;type de données;type de données
solution: Experience Platform
title: Type de données du nom de personne
topic-legacy: overview
description: Ce document fournit un aperçu du type de données XDM du nom de personne.
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 7f694310b17ab257eae459003bb820f7221bb55e
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 21%

---

# [!UICONTROL Type de ] données de nom de personne

[!UICONTROL Le ] nom de personne est un type de données XDM standard qui décrit le nom complet d’une personne. Comme les conventions pour les structures de noms diffèrent largement selon les langues et les cultures, les noms doivent toujours être modélisés à l’aide de ce type de données.

En outre, le type de données fournit un certain nombre de propriétés facultatives qui peuvent être utilisées dans les situations qui nécessitent l’utilisation d’un fragment seulement du nom complet, comme la création d’un message de bienvenue formel ou informel.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Propriété | Description |
| --- | --- |
| `courtesyTitle` | Abréviation du titre, de l’honneur ou de la formule de salutation d’une personne (par exemple `Mr.`, `Miss.` ou `Dr.`). |
| `firstName` | Premier segment du nom dans l’ordre d’écriture et le plus communément accepté dans la langue du nom. |
| `fullName` | Nom complet de la personne, dans l’ordre d’écriture le plus communément accepté dans la langue du nom. |
| `lastName` | Dernier segment du nom dans l’ordre d’écriture et le plus communément accepté dans la langue du nom. |
| `middleName` | Nom intermédiaire, nom alternatif ou noms supplémentaires présents entre le prénom et le nom. |
| `suffix` | Groupe de lettres fourni après le nom d’une personne afin de fournir des informations supplémentaires (par exemple `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`, etc.). |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données du nom de la personne, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
