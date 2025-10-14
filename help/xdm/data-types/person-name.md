---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;Schéma;XDM;champs;schémas;Schémas;fullName;xdm:fullName;nom de personne;nom;type de données;type de données;
solution: Experience Platform
title: Type de données de nom de personne
description: Découvrez le type de données XDM Nom de la personne.
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 6%

---

# [!UICONTROL Nom de la personne] type de données

[!UICONTROL Nom de la personne] est un type de données XDM standard qui décrit le nom complet d’une personne. Les conventions relatives aux structures de noms variant considérablement selon les langues et les cultures, les noms doivent toujours être modélisés à l’aide de ce type de données.

En outre, le type de données fournit un certain nombre de propriétés facultatives qui peuvent être utilisées dans les situations qui nécessitent uniquement un fragment du nom complet, comme la création d’un message d’accueil formel ou informel.

![](../images/data-types/person-name.png){width=500}

| Propriété | Description |
| --- | --- |
| `courtesyTitle` | Abréviation du titre, du titre honorifique ou de la qualification d’une personne (par exemple `Mr.`, `Miss.` ou `Dr.`). |
| `firstName` | Premier segment du nom dans l’ordre d’écriture le plus couramment accepté dans la langue du nom. |
| `fullName` | Nom complet de la personne, dans l’ordre d’écriture le plus couramment accepté dans la langue du nom. |
| `lastName` | Dernier segment du nom dans l’ordre d’écriture le plus couramment accepté dans la langue du nom. |
| `middleName` | Nom intermédiaire, nom alternatif ou noms supplémentaires présents entre le prénom et le nom. |
| `suffix` | Groupe de lettres fourni après le nom d’une personne pour fournir des informations supplémentaires (telles que `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`, etc.). |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données de nom de personne, reportez-vous au référentiel XDM public :

* [&#x200B; Exemple renseigné &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
