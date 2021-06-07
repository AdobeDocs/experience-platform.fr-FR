---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;profil individuel;champs;schémas;schémas;détails de fidélité;conception de schéma;groupe de champs;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma des détails de fidélité
topic-legacy: overview
description: Ce document présente un aperçu du groupe de champs de schéma Détails du programme de fidélité .
source-git-commit: fe49560a69c4c02835f00e4ebc0a5b9dc88eae90
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 4%

---


# [!UICONTROL Groupe de champs ] Loyalty Detailsschema

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document [mises à jour des noms de groupe de champs](../name-updates.md) .

[!UICONTROL Loyalty ] Détaille un groupe de champs de schéma standard pour la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le groupe de champs fournit un champ de type objet unique, `loyalty`, qui capture les informations relatives à l’appartenance d’une personne à un programme de fidélité client.

![](../../images/field-groups/loyalty-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `pointsExpiration` | Tableau d’objets | Répertorie tous les points de fidélité (ou groupes de points de fidélité) qui vont expirer et les dates auxquelles ils vont expirer. Chaque élément du tableau doit être un objet qui contient les deux propriétés suivantes : <ul><li>`pointsExpirationDate`: Date et heure ISO 8601 d’expiration des points.</li><li>`pointsExpiring`: Le solde des points arrivant à expiration à partir de la date d’expiration associée.</li></ul> |
| `joinDate` | DateTime | Date et heure ISO 8601 du moment où la personne a rejoint le programme de fidélité. |
| `loyaltyID` | Tableau de chaînes | Représente le ou les identifiants du programme de fidélité associés au membre du programme de fidélité. |
| `points` | Double | L’équilibre actuel des points de fidélité ou des récompenses pour le membre du programme de fidélité. |
| `pointsRedeemed` | Double | Nombre de points que le membre du programme de fidélité a appliqués à un achat ou qu’il a consommé d’une autre manière. |
| `program` | Chaîne | Nom du programme de fidélité dans lequel la personne est inscrite. |
| `status` | Chaîne | État actuel de l’appartenance à la fidélité de la personne, tel que `active`, `disabled` ou `suspended`. |
| `tier` | Chaîne | Capture le niveau du programme de fidélité dans lequel la personne est inscrite. |
| `upgradeDate` | Chaîne | Date à laquelle le membre du programme de fidélité a été mis à niveau vers son niveau le plus récent. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-loyalty-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-loyalty-details.schema.json)
