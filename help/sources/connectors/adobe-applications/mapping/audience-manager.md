---
keywords: Experience Platform ; accueil ; rubriques populaires ; mappage des Audiences Manager ; mappage du gestionnaire d’audiences
solution: Experience Platform
title: Mappage de champs pour le connecteur source Adobe Audience Manager
topic: overview
description: Découvrez comment mapper les données Adobe Audience Manager (en temps réel, intégrées et de Profil) aux champs correspondants du modèle de données d’expérience (XDM) pour le connecteur de source d’Audience Manager.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 70%

---


# Mappages des champs d’Audience Manager

Les tableaux ci-dessous contiennent les mappages entre les champs des données Adobe Audience Manager (données en temps réel, intégrées et de profil) et les champs XDM correspondants.

Pour plus d’informations sur chaque champ XDM, consultez le [dictionnaire des champs XDM](../../../../xdm/schema/field-dictionary.md).

## Données en temps réel

Type : données en temps réel

| Champ de données en temps réel | Champ XDM |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *Uniquement pour les espaces de noms présents dans endUserIds et uniquement la première valeur.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Uniquement pour les espaces de noms présents dans endUserIds et uniquement la première valeur.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType → type</li><li>manufacturer → manufacturer</li><li>marketingName → model</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvince</li><li>d_city → city</li><li>d_postal → postalCode</li><li>d_lat → latitude</li><li>d_longitude → longitude</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → os name </li><li>d_os_version → os_version</li></ul> |

## Données de profil

Type : profil

| Champ de profil | Champ XDM |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
