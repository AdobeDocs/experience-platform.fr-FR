---
title: Type de données des informations sur les détails de l’erreur
description: Découvrez le type de données du modèle de données d’expérience (XDM) Détails de l’erreur.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 7%

---

# [!UICONTROL Informations sur les erreurs] type de données

[!UICONTROL Informations sur les erreurs] est un type de données XDM (Experience Data Model) standard qui décrit les détails d’erreur. Utilisez la variable [!UICONTROL Informations sur les erreurs] type de données pour capturer les détails de la source et de l’identification de l’erreur. L’ID d’erreur identifie l’erreur et la source de l’erreur indique si elle provient du lecteur ou d’une source externe.

![Schéma du type de données Error Details Information .](../images/data-types/error-details-information.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Identifiant d’erreur] | `name` | chaîne | ID d’erreur. |
| [!UICONTROL Source de l’erreur] | `source` | chaîne | Source de l’erreur. Énuméré : &quot;joueur&quot;, &quot;externe&quot; avec leurs significations respectives. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json)
