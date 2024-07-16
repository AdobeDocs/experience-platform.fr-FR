---
title: Type de données de liste de demandes
description: Découvrez le type de données XDM (modèle de données d’expérience de liste de demandes).
exl-id: cbea6b08-9d4d-4cbe-b0c5-506bccc6df67
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 7%

---

# Type de données [!UICONTROL Liste des demandes]

[!UICONTROL Liste des demandes] est un type de données XDM (Experience Data Model) standard qui décrit une collection organisée d’articles à acheter ou à acheter. Utilisez le type de données [!UICONTROL Liste des demandes] pour identifier et décrire les listes de demandes.

![Schéma du type de données [!UICONTROL Liste de demandes].](../images/data-types/requisition-list.png)

| Nom d’affichage | Propriété | Type de données | Description |
|---------------------------|-------------------|-----------|--------------------------------------------------|
| [!UICONTROL ID de liste de demandes] | `ID` | Chaîne | Identifiant unique de la liste des demandes. |
| [!UICONTROL Nom de liste de demandes] | `name` | Chaîne | Nom de la liste des demandes spécifiée par le client. |
| [!UICONTROL Description de la liste de demandes] | `description` | Chaîne | Description de la liste des demandes spécifiée par le client. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.schema.json)
