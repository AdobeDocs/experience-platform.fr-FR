---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;champs;schémas;Schémas;géo;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données géographiques
description: En savoir plus sur le type de données XDM géographique.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
TQID: https://experienceleague.adobe.com/bGa6QY2Nq5M6BOEv8bApFPD8zwFlW5UhG9sAZ6Nm0-Y
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 205
ht-degree: 32%

---

# Type de données [!UICONTROL Geo]

[!UICONTROL Géo] est un type de données XDM standard qui décrit la zone géographique dans laquelle un événement a été observé.

![](../images/data-types/geo.png){width=400}

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Coordonnées géographiques]](./geo-coordinates.md) | Décrit les coordonnées géographiques d’un emplacement. |
| `_id` | Chaîne | Identifiant unique généré par le système pour les coordonnées. |
| `city` | Chaîne | Nom de la ville. |
| `countryCode` | Chaîne | Code <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> à deux caractères pour le pays. |
| `dmaID` | Entier | Zone de marché désignée par Nielsen Media Research. |
| `msaID` | Entier | Région métropolitaine des États-Unis dans laquelle l’observation a été effectuée. |
| `postalCode` | Chaîne | Code postal de l’emplacement. Les codes postaux ne sont pas disponibles pour tous les pays. Dans certains pays, ce champ ne contiendra qu’une partie du code postal. |
| `stateProvince` | Chaîne | Partie de l’état ou de la province de l’observation. Le format suit la norme [ISO 3166-2 (pays et subdivisions)](https://www.unece.org/cefact/locode/subdivisions.html). |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
