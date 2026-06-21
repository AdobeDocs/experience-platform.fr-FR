---
title: Classe d’opportunité commerciale XDM
description: Découvrez la classe XDM Business Opportunity dans le modèle de données d’expérience (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
TQID: https://experienceleague.adobe.com/SYF6sbMhbh56TucygUFbW-dlTB1xJcnlS-fftNHZ-iI
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 314
ht-degree: 3%

---

# Classe [!UICONTROL &#x200B; XDM Business Opportunity &#x200B;]

>[!IMPORTANT]
>
>Cette classe est destinée aux organisations ayant accès à [Adobe Real-Time Customer Data Platform B2B edition](../../../rtcdp/b2b-overview.md). Vous devez avoir accès à Real-Time CDP B2B edition pour que cette classe puisse participer au [profil client en temps réel](../../../profile/home.md).

[!UICONTROL XDM Business Opportunity] est une classe de modèle de données d’expérience (XDM) standard qui capture les propriétés minimales requises d’une opportunité commerciale.

![&#x200B; Structure de la classe d’opportunité commerciale XDM telle qu’elle apparaît dans l’interface utilisateur](../../images/classes/b2b/business-opportunity.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `accountKey` | Source B2B[&#128279;](../../data-types/b2b-source.md) | Identifiant composite du compte auquel cette opportunité est associée. |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système Source externe]](../../data-types/external-source-system-audit-attributes.md) | Si l’opportunité provient d’un système source externe, cet objet capture les attributs d’audit de ce système. |
| `opportunityKey` | Source B2B[&#128279;](../../data-types/b2b-source.md) | Identifiant composite de l’entité d’opportunité. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système et distincte de la `opportunityID`. |
| `accountID` | Chaîne | ID unique du compte auquel cette opportunité est associée. |
| `isDeleted` | Booléen | Indique si cette entité de liste marketing a été supprimée dans Marketo Engage.<br><br>Lors de l’utilisation du connecteur source [Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tous les enregistrements supprimés dans Marketo sont automatiquement répercutés dans le profil client en temps réel. Cependant, les enregistrements relatifs à ces profils peuvent toujours persister dans le lac de données. En définissant `isDeleted` sur `true`, vous pouvez utiliser le champ pour filtrer les enregistrements qui ont été supprimés de vos sources lors de l’interrogation du lac de données. |
| `opportunityDescription` | Chaîne | Description de l’opportunité. |
| `opportunityID` | Chaîne | ID unique de l’entité d’opportunité. |
| `opportunityName` | Chaîne | Nom de l’opportunité. |
| `opportunityStage` | Chaîne | Étape de vente de l’opportunité. |
| `opportunityType` | Chaîne | Type d’opportunité. |

{style="table-layout:auto"}

Consultez le guide sur les [relations de schéma dans Real-Time CDP B2B edition](../../tutorials/relationship-b2b.md) pour savoir comment cette classe est conceptuellement liée aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
