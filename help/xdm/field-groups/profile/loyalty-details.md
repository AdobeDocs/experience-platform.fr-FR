---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;profil individuel;champs;schémas;schémas;détails de fidélité;conception de schéma;groupe de champs;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma des détails de fidélité
description: En savoir plus sur le groupe de champs de schéma Loyalty Details .
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 11%

---

# [!UICONTROL Groupe de champs de schéma Loyalty Details]

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Loyalty Details] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le groupe de champs fournit un champ de type objet unique, `loyalty`, qui capture les informations relatives à l’appartenance d’une personne à un programme de fidélité client.

![](../../images/field-groups/loyalty-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `pointsExpiration` | Tableau d’objets | Répertorie tous les points (ou groupes de points de fidélité) qui vont expirer et les dates auxquelles ils vont expirer. Chaque élément du tableau doit être un objet qui contient les deux propriétés suivantes : <ul><li>`pointsExpirationDate` : date et heure ISO 8601 d’expiration des points.</li><li>`pointsExpiring` : le solde des points expirant à compter de la date d’expiration associée.</li></ul> |
| `joinDate` | DateTime | Date et heure ISO 8601 du moment où la personne a rejoint le programme de fidélité. |
| `loyaltyID` | Tableau de chaînes | Représente le ou les identifiants du programme de fidélité associés au membre du programme de fidélité. |
| `points` | Double | L’équilibre actuel des points de fidélité ou des récompenses pour le membre du programme de fidélité. |
| `pointsRedeemed` | Double | Nombre de points que le membre du programme de fidélité a appliqués à un achat ou qu’il a consommé d’une autre manière. |
| `program` | Chaîne | Nom du programme de fidélité dans lequel la personne est inscrite. |
| `status` | Chaîne | État actuel de l’appartenance à la fidélité de la personne, par exemple `active`, `disabled` ou `suspended`. |
| `tier` | Chaîne | Capture le niveau du programme de fidélité dans lequel la personne est inscrite. |
| `upgradeDate` | Chaîne | Date à laquelle le membre du programme de fidélité a été mis à niveau vers son niveau le plus récent. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
