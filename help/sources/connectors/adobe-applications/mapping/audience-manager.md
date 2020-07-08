---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Champ de mappage Audience Manager
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 97%

---


# Champs de mappage des Audiences Manager

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
| `Signals` | ExperienceEvent.signals |

## Données entrantes **(obsolètes)**

Type : ExperienceEvent

| Champ entrant | Champ XDM |
| --- | --- |
| `uuid` | `ExperienceEvent.identityMap[<ID Type>]` |
| `deviceIds` | `ExperienceEvent.identityMap["CORE"] And calculated ECIDs  ExperienceEvent.identityMap["ECID"]` |
| `signals` | `ExperienceEvent.signals` |
| `b_time` | `ExperienceEvent.timeStamp` |
| `overwrite` | `overwriteTraits` |

>[!NOTE]
>
>Il est prévu que les champs entrants seront obsolètes dans une prochaine version.

## Données de profil

Type : profil

| Champ de profil | Champ XDM |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
