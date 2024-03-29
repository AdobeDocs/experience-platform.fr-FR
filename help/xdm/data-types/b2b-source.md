---
title: Type de données source B2B
description: Découvrez le type de données du modèle de données d’expérience source (XDM) B2B.
exl-id: 01b7d41c-1ab6-4cbc-b9b3-77b6af69faf3
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 3%

---

# [!UICONTROL Source B2B] type de données

[!UICONTROL Source B2B] est un type de données XDM (Experience Data Model) standard qui représente un identifiant composite pour une entité B2B (telle qu’une [account](../classes/b2b/business-account.md), un [occasion](../classes/b2b/business-opportunity.md)ou un [campaign](../classes/b2b/business-campaign.md)).

Lorsque vous vous fiez uniquement aux identifiants basés sur des chaînes, il peut y avoir des chevauchements entre les identifiants sur plusieurs systèmes (par exemple, une opportunité peut se voir attribuer un identifiant de chaîne sur un système de gestion de la relation client, mais ce même identifiant peut faire référence à une opportunité complètement différente). Cela peut entraîner des conflits de données lors de la fusion des données dans [Profil client en temps réel](../../profile/home.md).

La variable [!UICONTROL Source B2B] Le type de données vous permet d’utiliser l’identifiant de chaîne d’origine d’une entité et de le combiner avec des informations contextuelles spécifiques à la source afin de vous assurer qu’il reste entièrement unique dans le système Platform, quelle que soit la source d’où il provient.

![Structure de la source B2B](../images/data-types/b2b-source.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `sourceID` | Chaîne | Identifiant unique de l’enregistrement source. |
| `sourceInstanceID` | Chaîne | ID d’instance ou d’organisation des données source. |
| `sourceKey` | Chaîne | Un identifiant unique composé de la variable `sourceId`, `sourceInstanceId`, et `sourceType` concaténé ensemble au format suivant : `[sourceID]@[sourceInstanceID].[sourceType]`.<br><br>Certains connecteurs source tels que Marketo concaténent automatiquement cette valeur pour certains identifiants. Les autres doivent être concaténés manuellement à l’aide de la variable [Préparation de données `concat` function](../../data-prep/functions.md#string), par exemple : `concat(id,"@${ORG_ID}.Marketo")` |
| `sourceType` | Chaîne | Nom de la plateforme qui fournit les données source. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/b2b-source.schema.json)
