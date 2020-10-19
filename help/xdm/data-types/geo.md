---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;datatype;data-type;data type;
solution: Experience Platform
title: Type de données géographiques
topic: overview
description: Ce document présente un aperçu du type de données de Géo XDM.
translation-type: tm+mt
source-git-commit: 6a7967ac9e652c7e73fd713e89a9079287cf0ae5
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 39%

---


# [!UICONTROL Type de données géo]

[!UICONTROL Geo] est un type de données XDM standard qui décrit la zone géographique où un événement a été observé.

<img src="../images/data-types/geo.png" width="400" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Coordonnées géographiques]](./geo-coordinates.md) | Décrit les coordonnées géographiques d’un lieu. |
| `_id` | Chaîne | Identifiant unique généré par le système pour les coordonnées. |
| `city` | Chaîne | Nom de la ville. |
| `countryCode` | Chaîne | Code <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> à deux caractères pour le pays. |
| `dmaID` | Entier | La recherche médiatique Nielsen a désigné zone de marché. |
| `msaID` | Entier | Zone statistique métropolitaine aux États-Unis où l&#39;observation s&#39;est produite. |
| `postalCode` | Chaîne | Code postal de l’emplacement. Les codes postaux ne sont pas disponibles pour tous les pays. Dans certains pays, ce champ ne contiendra qu’une partie du code postal. |
| `stateProvince` | Chaîne | Partie de l’état ou de la province de l’observation. Le format est conforme à la norme [ISO 3166-2 (pays et subdivisions)](http://www.unece.org/cefact/locode/subdivisions.html). |

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)