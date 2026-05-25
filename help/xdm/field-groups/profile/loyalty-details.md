---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;profil individuel;champs;schémas;Schémas;détails de fidélité;conception de schéma;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma des détails de fidélité
description: Découvrez le groupe de champs de schéma Détails de fidélité .
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
TQID: https://experienceleague.adobe.com/ejWOFx2swDsfq7xDXuppY0yaqCFCbgcrH8IxdLHh7AQ
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 302
ht-degree: 10%

---

# [!UICONTROL Loyalty Details] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Loyalty Details] groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le groupe de champs fournit un champ unique de type objet, `loyalty`, qui recueille les informations relatives à l’appartenance d’une personne à un programme de fidélité des clients.

![](../../images/field-groups/loyalty-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `pointsExpiration` | Tableau d’objets | Répertorie tous les points de fidélité (ou groupes de points de fidélité) qui vont expirer, ainsi que les dates d’expiration. Chaque élément de tableau doit être un objet contenant les deux propriétés suivantes : <ul><li>`pointsExpirationDate` : date et heure ISO 8601 indiquant le moment où les points expireront.</li><li>`pointsExpiring` : solde de points arrivant à expiration à compter de la date d&#39;expiration associée.</li></ul> |
| `joinDate` | DateTime | Date et heure ISO 8601 auxquelles la personne a rejoint le programme de fidélité. |
| `loyaltyID` | Tableau de chaînes | Représente le ou les identifiants du programme de fidélité associés au membre du programme de fidélité. |
| `points` | Double | Solde actuel de points de fidélité ou de récompenses pour le membre du programme de fidélité. |
| `pointsRedeemed` | Double | Le nombre de points que le membre du programme de fidélité a appliqués pour un achat ou qu’il a autrement échangés. |
| `program` | Chaîne | Nom du programme de fidélité auquel la personne est inscrite. |
| `status` | Chaîne | Statut actuel de l’abonnement de fidélité de la personne, tel que `active`, `disabled` ou `suspended`. |
| `tier` | Chaîne | Capture le niveau du programme de fidélité auquel la personne est inscrite. |
| `upgradeDate` | Chaîne | Date à laquelle le membre du programme de fidélité a été promu à son niveau le plus récent. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
