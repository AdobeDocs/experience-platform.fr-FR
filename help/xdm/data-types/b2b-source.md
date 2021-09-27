---
title: Type de données source B2B
description: Ce document présente un aperçu du type de données XDM (Source Experience Data Model) B2B.
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 3%

---

# [!UICONTROL Type ] de données source B2B

>[!NOTE]
>
>Ce type de données est uniquement disponible pour les organisations qui ont accès à l’édition B2B de la plateforme de données clients en temps réel.

[!UICONTROL La source B2B ] est un type de données XDM (Experience Data Model) standard qui représente un identifiant composite pour une entité B2B (un  [compte](../classes/b2b/business-account.md), une  [opportunité](../classes/b2b/business-opportunity.md) ou une  [campagne](../classes/b2b/business-campaign.md), par exemple).

Lorsque vous vous fiez uniquement aux identifiants basés sur des chaînes, il peut y avoir des chevauchements entre les identifiants sur plusieurs systèmes (par exemple, une opportunité peut se voir attribuer un identifiant de chaîne sur un système CRM, mais ce même identifiant peut faire référence à une opportunité complètement différente). Cela peut entraîner des conflits de données lors de la fusion de données dans [Real-time Customer Profile](../../profile/home.md).

Le type de données [!UICONTROL Source B2B] vous permet d’utiliser l’ID de chaîne d’origine d’une entité et de le combiner avec des informations contextuelles spécifiques à la source afin de vous assurer qu’il reste entièrement unique dans le système Platform, quelle que soit la source d’où il provient.

![Structure de la source B2B](../images/data-types/b2b-source.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `sourceID` | Chaîne | Identifiant unique de l’enregistrement source. |
| `sourceInstanceID` | Chaîne | ID d’instance ou d’organisation des données source. |
| `sourceKey` | Chaîne | Identifiant unique composé de `sourceId`, `sourceInstanceId` et `sourceType` concaténés au format suivant : `[sourceID]@$[sourceInstanceID].[sourceType]`.<br><br>Certains connecteurs source tels que Marketo concaténent automatiquement cette valeur pour certains identifiants. D’autres doivent être concaténés manuellement à l’aide de la fonction [Préparation de données `concat`](../../data-prep/functions.md#string), par exemple : `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | Chaîne | Nom de la plateforme qui fournit les données source. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
