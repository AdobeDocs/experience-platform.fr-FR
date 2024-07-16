---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;appareil;type de données;type de données;type de données
solution: Experience Platform
title: Type de données du périphérique
description: Découvrez le type de données XDM du périphérique.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 19%

---

# Type de données [!UICONTROL Device]

[!UICONTROL Device] est un type de données XDM standard qui décrit un appareil identifié. Un périphérique est une instance d’application ou de navigateur qui peut faire l’objet d’un suivi entre plusieurs sessions, généralement par des cookies.

<img src="../images/data-types/device.png" width="450" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `colorDepth` | Nombre entier | Nombre de couleurs que l’affichage peut représenter. |
| `manufacturer` | Chaîne | Nom de l’organisation propriétaire de la conception et de la création de l’appareil. |
| `model` | Chaîne | Nom du modèle de l’appareil. Il s’agit du nom courant, lisible par l’utilisateur ou du nom marketing de l’appareil. Par exemple, &quot;iPhone 6S&quot; est un modèle particulier de téléphone mobile. |
| `modelNumber` | Chaîne | Numéro de modèle unique attribué par le fabricant pour cet appareil. Les numéros de modèle ne sont pas des versions, mais des identifiants uniques qui identifient une configuration de modèle spécifique. |
| `screenHeight` | Nombre entier | Nombre de pixels verticaux de l’écran actif de l’appareil dans l’orientation par défaut. |
| `screenOrientation` | Chaîne | Orientation de l’écran actuelle. Les valeurs acceptées sont `portrait` et `landscape`. |
| `screenWidth` | Chaîne | Nombre de pixels horizontaux de l’écran actif de l’appareil dans l’orientation par défaut. |
| `type` | Chaîne | Type d’appareil suivi. Les valeurs acceptées sont les suivantes : <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | Chaîne | Identifiant de l’appareil. Il peut s’agir d’un identifiant de DeviceAtlas ou d’un autre service qui identifie le matériel utilisé. |
| `typeIDService` | Chaîne | L’espace de noms du service utilisé pour identifier le type d’appareil. Consultez l’ [annexe](#typeIDService) pour plus d’informations sur les valeurs acceptées. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur le type de données [!UICONTROL Device].

## Valeurs acceptées pour typeIDService {#typeIDService}

Le tableau suivant décrit les valeurs acceptées pour `typeIDService` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | L’appareil a été identifié à l’aide de DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | Le périphérique a été identifié à l’aide d’Adobe Campaign. |
