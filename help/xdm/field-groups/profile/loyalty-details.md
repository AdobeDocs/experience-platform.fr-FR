---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;profil individuel;champs;schémas;schémas;détails de fidélité;conception de schéma;groupe de champs;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma des détails de fidélité
topic-legacy: overview
description: Ce document présente un aperçu du groupe de champs de schéma Détails du programme de fidélité .
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 4%

---


# [!UICONTROL Loyalty Details] schema field group

>[!NOTE]
>
>The names of several schema field groups have changed. See the document on [field group name updates](../name-updates.md) for more information.

[!UICONTROL Loyalty ] Détaille un groupe de champs de schéma standard pour la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). The field group provides a single object-type field, `loyalty`, which captures information related to a person&#39;s membership in a customer loyalty program.

![](../../images/field-groups/loyalty-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `pointsExpiration` | Array of objects | Lists any loyalty points (or groups of loyalty points) that are going to expire, and the dates they will expire on. Each array item must be an object that contains the following two properties: <ul><li>`pointsExpirationDate`: Date et heure ISO 8601 d’expiration des points.</li><li>`pointsExpiring`: Le solde des points arrivant à expiration à partir de la date d’expiration associée.</li></ul> |
| `joinDate` | DateTime | An ISO 8601 datetime of when the person joined the loyalty program. |
| `loyaltyID` | Tableau de chaînes | Represents the loyalty program ID(s) associated with the loyalty program member. |
| `points` | Double | L’équilibre actuel des points de fidélité ou des récompenses pour le membre du programme de fidélité. |
| `pointsRedeemed` | Double | Nombre de points que le membre du programme de fidélité a appliqués à un achat ou qu’il a consommé d’une autre manière. |
| `program` | Chaîne | Nom du programme de fidélité dans lequel la personne est inscrite. |
| `status` | Chaîne | État actuel de l’appartenance à la fidélité de la personne, tel que `active`, `disabled` ou `suspended`. |
| `tier` | Chaîne | Capture le niveau du programme de fidélité dans lequel la personne est inscrite. |
| `upgradeDate` | Chaîne | Date à laquelle le membre du programme de fidélité a été mis à niveau vers son niveau le plus récent. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Populated example](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Full schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
