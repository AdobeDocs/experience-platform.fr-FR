---
title: Type de données de liste de demandes
description: Découvrez le type de données XDM (modèle de données d’expérience de liste de demandes).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 7%

---

# [!UICONTROL Liste des demandes] type de données

[!UICONTROL Liste des demandes] est un type de données XDM (Experience Data Model) standard qui décrit une collection organisée d’articles à des fins d’achat ou d’achat. Utilisez la variable [!UICONTROL Liste des demandes] type de données pour identifier et décrire les listes de demandes d’acquisition.

![Un diagramme de [!UICONTROL Liste des demandes] type de données.](../images/data-types/requisition-list.png)

| Nom d’affichage | Propriété | Type de données | Description |
|---------------------------|-------------------|-----------|--------------------------------------------------|
| [!UICONTROL Identifiant de liste de demandes] | `ID` | chaîne | Identifiant unique de la liste des demandes. |
| [!UICONTROL Nom de la liste de demandes] | `name` | chaîne | Nom de la liste des demandes spécifiée par le client. |
| [!UICONTROL Description de la liste de demandes] | `description` | chaîne | Description de la liste des demandes spécifiée par le client. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.schema.json)
