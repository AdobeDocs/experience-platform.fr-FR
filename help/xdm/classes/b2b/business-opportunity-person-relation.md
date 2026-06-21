---
title: Classe de relation de la personne avec l’opportunité commerciale XDM
description: Découvrez la classe de relation entre la personne et l’opportunité commerciale XDM dans le modèle de données d’expérience (XDM).
exl-id: 7be193d2-52eb-4b28-953b-5e0fc21d8f93
TQID: https://experienceleague.adobe.com/CZjEhevT7rql7WYWlHypeXBecAnOa6b9IUyvur3iF2U
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 366
ht-degree: 3%

---

# Classe [!UICONTROL Relation de la personne avec l’opportunité commerciale XDM]

>[!IMPORTANT]
>
>Cette classe est destinée aux organisations ayant accès à [Adobe Real-Time Customer Data Platform B2B edition](../../../rtcdp/b2b-overview.md). Vous devez avoir accès à Real-Time CDP B2B edition pour que cette classe puisse participer au [profil client en temps réel](../../../profile/home.md).

[!UICONTROL Relation de la personne avec l’opportunité commerciale XDM] est une classe XDM (modèle de données d’expérience) standard qui capture les propriétés minimales requises d’une personne associée à une opportunité commerciale.

![ Structure de la classe de personne XDM Business Opportunity telle qu’elle apparaît dans l’interface utilisateur](../../images/classes/b2b/business-opportunity-person-relation.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système Source externe]](../../data-types/external-source-system-audit-attributes.md) | Si la relation de l&#39;entrepreneur provient d&#39;un système source externe, cet objet capture les attributs d&#39;audit de ce système. |
| `opportunityKey` | Source B2B]](../../data-types/b2b-source.md)[[!UICONTROL  | Identifiant composite de l’opportunité dans la relation opportunité-personne. |
| `opportunityPersonKey` | Source B2B]](../../data-types/b2b-source.md)[[!UICONTROL  | Identifiant composite de l’entité de relation opportunité-personne. |
| `personKey` | Source B2B]](../../data-types/b2b-source.md)[[!UICONTROL  | Identifiant composite de la personne dans la relation opportunité-personne. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte des autres champs d’identification capturés par la classe . |
| `isDeleted` | Booléen | Indique si cette entité de liste marketing a été supprimée dans Marketo Engage.<br><br>Lors de l’utilisation du connecteur source [Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tous les enregistrements supprimés dans Marketo sont automatiquement répercutés dans le profil client en temps réel. Cependant, les enregistrements relatifs à ces profils peuvent toujours persister dans le lac de données. En définissant `isDeleted` sur `true`, vous pouvez utiliser le champ pour filtrer les enregistrements qui ont été supprimés de vos sources lors de l’interrogation du lac de données. |
| `isPrimary` | Booléen | Indique si la personne est le contact principal pour cette opportunité. |
| `opportunityID` | Chaîne | Identifiant unique de l’opportunité dans la relation opportunité-personne. |
| `opportunityPersonID` | Chaîne | Identifiant unique de l’entité de relation opportunité-personne |
| `personID` | Chaîne | Identifiant unique de la personne dans la relation opportunité-personne. |
| `personRole` | Chaîne | Rôle de la personne dans la relation opportunité-personne. |

{style="table-layout:auto"}

Consultez le guide sur les [relations de schéma dans Real-Time CDP B2B edition](../../tutorials/relationship-b2b.md) pour savoir comment cette classe est conceptuellement liée aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
