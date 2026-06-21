---
title: Classe de compte professionnel XDM
description: Découvrez la classe Compte professionnel XDM dans le modèle de données d’expérience (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
TQID: https://experienceleague.adobe.com/lBNwtc9uiwXWnRKxbCCUmU67oQxpi4Tdal6QZYryKY8
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 257
ht-degree: 2%

---

# Classe [!UICONTROL Compte professionnel XDM]

>[!IMPORTANT]
>
>Cette classe est destinée aux organisations ayant accès à [Adobe Real-Time Customer Data Platform B2B edition](../../../rtcdp/b2b-overview.md). Vous devez avoir accès à Real-Time CDP B2B edition pour que cette classe puisse participer au [profil client en temps réel](../../../profile/home.md).

[!UICONTROL Compte professionnel XDM] est une classe XDM (modèle de données d’expérience) standard qui capture les propriétés minimales requises d’un compte professionnel.

![&#x200B; Structure de la classe XDM Business Account telle qu’elle apparaît dans l’interface utilisateur](../../images/classes/b2b/business-account.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `accountKey` | Source B2B[&#128279;](../../data-types/b2b-source.md) | Identifiant composite de l’entité de compte. |
| `extSourceSystemAudit` | [[!UICONTROL Attributs d’audit du système Source externe]](../../data-types/external-source-system-audit-attributes.md) | Si le compte provient d’un système source externe, cet objet capture les attributs d’audit de ce système. |
| `_id` | Chaîne | Identifiant unique de l’enregistrement. Il s’agit d’une valeur générée par le système qui est distincte de l’identifiant `accountKey`. |
| `isDeleted` | Booléen | Indique si cette entité de compte a été supprimée dans Marketo Engage.<br><br>Lors de l’utilisation du connecteur source [Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), tous les enregistrements supprimés dans Marketo sont automatiquement répercutés dans le profil client en temps réel. Cependant, les enregistrements relatifs à ces profils peuvent toujours persister dans le lac de données. En définissant `isDeleted` sur `true`, vous pouvez utiliser le champ pour filtrer les enregistrements qui ont été supprimés de vos sources lors de l’interrogation du lac de données. |

{style="table-layout:auto"}

Consultez le guide sur les [relations de schéma dans Real-Time CDP B2B edition](../../tutorials/relationship-b2b.md) pour savoir comment cette classe est conceptuellement liée aux autres classes B2B et comment vous pouvez établir ces relations dans l’interface utilisateur de Adobe Experience Platform.
