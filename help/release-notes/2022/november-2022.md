---
title: Notes de mise à jour d’Adobe Experience Platform – Novembre 2022
description: Les notes de mise à jour de novembre 2022 pour Adobe Experience Platform.
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
TQID: https://experienceleague.adobe.com/4-QrsXu0gw7qLUx0PR8vdvWFV2TojviqvqL6lFETKJs
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: abc02dd6-664f-446a-9aaa-675bc0f2fe4a
  - id: acc16deb-1d7f-4ec9-9ce3-6cdf355afde6
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: dc6ebdf7-9a94-43eb-9184-759cfdd0cf1c
  - id: de9975b2-c43a-4287-9698-4f4cad92b83f
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 317
ht-degree: 95%

---

# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 23 novembre 2022.**

Mises à jour des fonctionnalités existantes dans Adobe Experience Platform :

- [Collecte de données](#data-collection)
- [Modèle de données d’expérience (XDM)](#xdm)
- [Sources](#sources)

## Collecte de données {#data-collection}

Adobe Experience Platform fournit une suite de technologies qui vous permettent de collecter des données d’expérience client côté client. Vous pouvez ensuite les envoyer à Adobe Experience Platform Edge Network pour les enrichir, les transformer et les distribuer vers des destinations Adobe ou autres qu’Adobe.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Extension [!DNL AWS] pour le transfert d’événement | Vous pouvez désormais envoyer des données à [!DNL Amazon Web Services] ([!DNL AWS]) à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations, consultez la présentation de l’extension [[!DNL AWS] &#x200B;](../../tags/extensions/server/aws/overview.md). |
| Extension [!DNL Google Ads Enhanced Conversions] pour le transfert d’événement | Vous pouvez désormais envoyer des données de conversion à [!DNL Google Ads] à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations, consultez la présentation de l’extension [[!DNL Google Ads Enhanced Conversions] &#x200B;](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md). |
| Extension [!DNL Microsoft Azure] pour le transfert d’événement | Vous pouvez désormais envoyer des données à [!DNL Microsoft Azure] à l’aide d’une extension de [transfert d’événement](../../tags/ui/event-forwarding/overview.md). Pour plus d’informations, consultez la présentation de l’extension [[!DNL Microsoft Azure] &#x200B;](../../tags/extensions/server/azure/overview.md). |

Pour plus d’informations sur les fonctionnalités de collecte de données d’Experience Platform, consultez la [présentation de la collecte de données](../../collection/home.md).

## Modèle de données d’expérience (XDM) {#xdm}

XDM est une spécification Open Source qui fournit des structures et des définitions communes (schémas) pour les données introduites dans Adobe Experience Platform. En adhérant aux normes XDM, toutes les données d’expérience client peuvent être intégrées dans une représentation commune afin de fournir des informations plus rapidement et de manière plus intégrée. Vous pouvez obtenir des informations précieuses à partir des actions des clients, définir des types d’audiences clientes par le biais de segments et utiliser les attributs du client à des fins de personnalisation.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Attribuer des champs à des classes personnalisées lors de l’ajout direct à un schéma | Auparavant, lorsque vous [ajoutiez directement un champ individuel à un schéma](../../xdm/ui/resources/schemas.md#add-individual-fields), vous ne pouviez attribuer le champ qu’à un groupe de champs en tant que sa ressource parente. Désormais, en plus des groupes de champs, vous pouvez [attribuer le champ à une classe personnalisée](../../xdm/ui/resources/schemas.md#add-to-class) en tant que sa ressource parente. |

{style="table-layout:auto"}

Pour plus d’informations sur XDM dans Experience Platform, consultez la [vue d’ensemble du système XDM](../../xdm/home.md).
