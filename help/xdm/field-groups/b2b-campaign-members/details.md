---
title: Groupe de champs de schéma des détails des membres de XDM Business Campaign
description: Découvrez le groupe de champs de schéma Détails des membres de XDM Business Campaign .
exl-id: 597629c8-7f41-4c1c-95b6-aed5e16cee72
TQID: https://experienceleague.adobe.com/lVvzXj4pgMtV8L5FS6nIUy-l9Iikc6iX9CJNfH5bbSs
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 74579d9ca311b241313a3d89b564f217cd3476c7
workflow-type: tm+mt
source-wordcount: 369
ht-degree: 5%

---

# [!UICONTROL Détails des membres de XDM Business Campaign] groupe de champs de schéma

[!UICONTROL Détails des membres de XDM Business Campaign] est un groupe de champs de schéma standard pour la classe [[!UICONTROL Membres de XDM Business Campaign]](../../classes/b2b/business-campaign-members.md), qui capture des informations détaillées sur une campagne commerciale.

![&#x200B; Structure du groupe de champs Détails des membres de XDM Business Campaign, tel qu’il apparaît dans l’interface utilisateur](../../images/field-groups/b2b/business-campaign-member-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `acquiredByCampaignKey` | Source B2B[&#128279;](../../data-types/b2b-source.md) | Identifiant composite de la campagne qui a acquis ce membre de campagne. |
| `acquiredByCampaignID` | [!UICONTROL Chaîne] | Identifiant de chaîne de la campagne qui a acquis ce membre de campagne. |
| `firstRespondedDate` | [!UICONTROL DateHeure] | Horodatage [ISO 8601](https://datatracker.ietf.org/doc/html/rfc3339#section-5.6) (`yyyy-MM-dd'T'HH:mm:ssXXX`) du moment où la personne a répondu pour la première fois à la campagne. |
| `hasReachedSuccess` | [!UICONTROL booléen] | Indique si ce membre de la campagne a abouti à une conversion. |
| `hasResponded` | [!UICONTROL booléen] | Indique si ce membre de la campagne a répondu à la campagne. |
| `isDeleted` | [!UICONTROL booléen] | Indique si ce membre de la campagne a été supprimé dans Marketo Engage.<br><br>Lors de l’utilisation du connecteur source [Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tous les enregistrements supprimés dans Marketo sont automatiquement répercutés dans le profil client en temps réel. Cependant, les enregistrements relatifs à ces profils peuvent toujours persister dans le lac de données. En définissant `isDeleted` sur `true`, vous pouvez utiliser le champ pour filtrer les enregistrements qui ont été supprimés de vos sources lors de l’interrogation du lac de données. |
| `isExhausted` | [!UICONTROL booléen] | Indique si ce membre de campagne a épuisé toutes les interactions de campagne. |
| `lastStatus` | [!UICONTROL Chaîne] | Dernier statut du membre de la campagne. |
| `memberStatus` | [!UICONTROL Chaîne] | Statut actuel du membre de la campagne. |
| `memberStatusReason` | [!UICONTROL Chaîne] | Raison du statut actuel du membre de la campagne. |
| `membershipDate` | [!UICONTROL DateHeure] | Raison du statut actuel du membre de la campagne. |
| `nurtureCadence` | [!UICONTROL Chaîne] | Cadence temporelle selon laquelle les informations relatives à la campagne doivent être présentées au membre de la campagne. |
| `nurtureTrackName` | [!UICONTROL Chaîne] | Nom du programme d’éducation auquel ce membre de la campagne est soumis. |
| `reachedSuccessDate` | [!UICONTROL DateHeure] | Horodatage ISO 8601 (`yyyy-MM-dd'T'HH:mm:ssXXX`) indiquant le moment où une conversion réussie a été effectuée pour le membre de la campagne. |
| `webinarConfirmationUrl` | [!UICONTROL Chaîne] | URL de confirmation du webinaire pour le membre de la campagne. |
| `webinarRegistrationID` | [!UICONTROL Chaîne] | ID d’enregistrement du webinaire pour le membre de la campagne. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/campaign-member/campaign-member-details.schema.json)
