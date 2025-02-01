---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;appareil;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données de l’appareil
description: Découvrez le type de données XDM de l’appareil.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 19%

---

# Type de données [!UICONTROL Device]

[!UICONTROL Appareil] est un type de données XDM standard qui décrit un appareil identifié. Un appareil est une instance de navigateur ou d’application pouvant être suivie entre les sessions, généralement par des cookies.

![](../images/data-types/device.png){width=450}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `colorDepth` | Nombre entier | Nombre de couleurs que l’affichage peut représenter. |
| `manufacturer` | Chaîne | Nom de l’organisation propriétaire de la conception et de la création de l’appareil. |
| `model` | Chaîne | Nom du modèle de l’appareil. Il s’agit du nom marketing, du nom lisible par l’utilisateur ou du nom courant de l’appareil. Par exemple, le « iPhone 6S » est un modèle particulier de téléphone mobile. |
| `modelNumber` | Chaîne | Désignation de numéro de modèle unique attribuée par le fabricant pour ce périphérique. Les numéros de modèle ne sont pas des versions, mais des identifiants uniques qui identifient une configuration de modèle particulière. |
| `screenHeight` | Nombre entier | Nombre de pixels verticaux de l’écran actif de l’appareil dans l’orientation par défaut. |
| `screenOrientation` | Chaîne | Orientation actuelle de l’écran. Les valeurs acceptées incluent `portrait` et `landscape`. |
| `screenWidth` | Chaîne | Nombre de pixels horizontaux de l’écran actif de l’appareil dans l’orientation par défaut. |
| `type` | Chaîne | Type d’appareil suivi. Les valeurs acceptées sont les suivantes : <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | Chaîne | Identifiant de l’appareil. Il peut s’agir d’un identifiant de DeviceAtlas ou d’un autre service qui identifie le matériel utilisé. |
| `typeIDService` | Chaîne | Espace de noms du service utilisé pour identifier le type d’appareil. Voir l’[annexe](#typeIDService) pour plus d’informations sur les valeurs acceptées. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [ Exemple renseigné ](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur le type de données [!UICONTROL Appareil].

## Valeurs acceptées pour typeIDService {#typeIDService}

Le tableau suivant décrit les valeurs acceptées pour les `typeIDService` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | L’appareil a été identifié à l’aide de DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | L’appareil a été identifié à l’aide d’Adobe Campaign. |
