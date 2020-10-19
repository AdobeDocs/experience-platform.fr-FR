---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;device;datatype;data-type;data type;
solution: Experience Platform
title: Type de données du périphérique
topic: overview
description: Ce document présente un aperçu du type de données XDM du périphérique.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 19%

---


# [!UICONTROL Type de données du périphérique]

[!UICONTROL Le périphérique] est un type de données XDM standard qui décrit un périphérique identifié. Un périphérique est une application ou une instance de navigateur qui peut faire l’objet d’un suivi entre les sessions, généralement par cookies.

<img src="../images/data-types/device.png" width="450" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `colorDepth` | Entier | Nombre de couleurs que l’affichage peut représenter. |
| `manufacturer` | Chaîne | Nom de l’organisation propriétaire de la conception et de la création du périphérique. |
| `model` | Chaîne | Nom du modèle du périphérique. Il s’agit du nom marketing courant, lisible par l’utilisateur ou du nom marketing du périphérique. Par exemple, &quot;iPhone 6S&quot; est un modèle particulier de téléphone mobile. |
| `modelNumber` | Chaîne | Désignation du numéro de modèle unique attribuée par le fabricant pour ce dispositif. Les numéros de modèle ne sont pas des versions, mais des identifiants uniques qui désignent une configuration de modèle particulière. |
| `screenHeight` | Entier | Nombre de pixels verticaux de l’principal affichage du périphérique dans l’orientation par défaut. |
| `screenOrientation` | Chaîne | Orientation actuelle de l’écran. Accepted values include `portrait` and `landscape`. |
| `screenWidth` | Chaîne | Nombre de pixels horizontaux de l’principal affichage du périphérique dans l’orientation par défaut. |
| `type` | Chaîne | Type de périphérique suivi. Les valeurs acceptées sont les suivantes : <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | Chaîne | Identifiant de l’appareil. Il peut s&#39;agir d&#39;un identifiant de DeviceAtlas ou d&#39;un autre service qui identifie le matériel utilisé. |
| `typeIDService` | Chaîne | Espace de noms du service utilisé pour identifier le type d’appareil. Consultez l’ [annexe](#typeIDService) pour plus d’informations sur les valeurs acceptées. |

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur le type de données [!UICONTROL Device] .

## Valeurs acceptées pour typeIDService {#typeIDService}

Le tableau suivant présente les valeurs acceptées pour `typeIDService` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | L&#39;appareil a été identifié à l&#39;aide de DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | L&#39;appareil a été identifié à l&#39;aide d&#39;Adobe Campaign. |