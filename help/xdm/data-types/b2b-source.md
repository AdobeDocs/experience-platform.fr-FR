---
title: Type de données Source B2B
description: Découvrez le type de données du modèle de données d’expérience (XDM) Source B2B.
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# Type de données [!UICONTROL Source B2B]

[!UICONTROL Source B2B] est un type de données standard du modèle de données d’expérience (XDM) qui représente un identifiant composite pour une entité B2B (telle qu’un [compte](../classes/b2b/business-account.md), une [opportunité](../classes/b2b/business-opportunity.md) ou une [campagne](../classes/b2b/business-campaign.md)).

Lorsque l’on se fie uniquement aux identifiants basés sur des chaînes, il peut y avoir des chevauchements entre les identifiants de plusieurs systèmes (par exemple, un identifiant de chaîne peut être attribué à une opportunité sur un système CRM, mais ce même identifiant peut renvoyer à une opportunité complètement différente). Cela peut entraîner des conflits de données lors de la fusion de données dans [Real-Time Customer Profile](../../profile/home.md).

Le type de données [!UICONTROL Source B2B] vous permet d’utiliser l’identifiant de chaîne d’origine d’une entité et de le combiner avec des informations contextuelles spécifiques à la source afin de vous assurer qu’il reste entièrement unique dans le système Experience Platform, quelle que soit la source d’où il provient.

![ Structure Source B2B ](../images/data-types/b2b-source.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `sourceID` | Chaîne | ID unique de l’enregistrement source. |
| `sourceInstanceID` | Chaîne | Identifiant d’instance ou d’organisation des données sources. |
| `sourceKey` | Chaîne | Identifiant unique composé des `sourceId`, `sourceInstanceId` et `sourceType` concaténés ensemble au format suivant : `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>Certains connecteurs source tels que Marketo concaténent automatiquement cette valeur pour certains identifiants. D’autres doivent être concaténés manuellement à l’aide de la fonction [`concat` de la préparation des données](../../data-prep/functions.md#string) par exemple : `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | Chaîne | Nom de la plateforme qui fournit les données sources. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [ Exemple renseigné ](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
