---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; périphérique ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données du périphérique
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM du périphérique.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 18%

---

# [!UICONTROL Type ] de données Devicedata

[!UICONTROL Le ] périphérique est un type de données XDM standard qui décrit un périphérique identifié. Un périphérique est une application ou une instance de navigateur qui peut faire l’objet d’un suivi entre les sessions, généralement par cookies.

<img src="../images/data-types/device.png" width="450" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `colorDepth` | Entier | Nombre de couleurs que l’affichage peut représenter. |
| `manufacturer` | Chaîne | Nom de l’organisation propriétaire de la conception et de la création du périphérique. |
| `model` | Chaîne | Nom du modèle du périphérique. Il s’agit du nom marketing courant, lisible par l’utilisateur ou du nom marketing du périphérique. Par exemple, &quot;iPhone 6S&quot; est un modèle particulier de téléphone mobile. |
| `modelNumber` | Chaîne | Désignation du numéro de modèle unique attribuée par le fabricant pour ce dispositif. Les numéros de modèle ne sont pas des versions, mais des identifiants uniques qui désignent une configuration de modèle particulière. |
| `screenHeight` | Entier | Nombre de pixels verticaux de l’principal affichage du périphérique dans l’orientation par défaut. |
| `screenOrientation` | Chaîne | Orientation actuelle de l’écran. Les valeurs acceptées sont `portrait` et `landscape`. |
| `screenWidth` | Chaîne | Nombre de pixels horizontaux de l’principal affichage du périphérique dans l’orientation par défaut. |
| `type` | Chaîne | Type de périphérique suivi. Les valeurs acceptées sont les suivantes : <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | Chaîne | Identifiant de l’appareil. Il peut s&#39;agir d&#39;un identifiant de DeviceAtlas ou d&#39;un autre service qui identifie le matériel utilisé. |
| `typeIDService` | Chaîne | Espace de noms du service utilisé pour identifier le type d’appareil. Voir l&#39;[annexe](#typeIDService) pour plus d&#39;informations sur les valeurs acceptées. |

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Annexe

La section suivante contient des informations supplémentaires sur le type de données [!UICONTROL Device].

## Valeurs acceptées pour typeIDService {#typeIDService}

Le tableau suivant décrit les valeurs acceptées pour `typeIDService` et leur signification associée :

| Valeur | Description |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | L&#39;appareil a été identifié à l&#39;aide de DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | L&#39;appareil a été identifié à l&#39;aide d&#39;Adobe Campaign. |
