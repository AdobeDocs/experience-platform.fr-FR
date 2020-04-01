---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' champ de mappage  Gestionnaire de'
topic: overview
translation-type: tm+mt
source-git-commit: 985c450a174712fa4b4185d5a6527962e697b5ba

---


#  champ de mappage  Gestionnaire de

Les tableaux ci-dessous contiennent les mappages entre les champs des données Adobe  Gestionnaire de  de (données en temps réel, intégrées et de) et les champs XDM correspondants.

Consultez le dictionnaire [de champ](../../../xdm/schema/field-dictionary.md) XDM pour plus d’informations sur chaque champ XDM.

## Données en temps réel

Type : Données en temps réel

| Champ de données en temps réel | Champ XDM |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *Uniquement pour   présent dans endUserIds et uniquement la première valeur.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Uniquement pour   présents dans endUserIds et uniquement la première valeur.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>PrimaryHardwareType → type</li><li>fabricant → fabricant</li><li>marketingName → modèle</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_country → countryCode</li><li>d_state → stateProvince</li><li>d_city → ville</li><li>d_postal → postalCode</li><li>d_lat → latitude</li><li>d_longitude → longitude</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_name → nom os </li><li>d_os_version → os_version</li></ul> |
| `Signals` | ExperienceEvent.signaux |

## Données entrantes **(obsolètes)**

Type : ExperienceEvent

| Champ entrant | Champ XDM |
| --- | --- |
| `uuid` | `ExperienceEvent.identityMap[<ID Type>]` |
| `deviceIds` | `ExperienceEvent.identityMap["CORE"] And calculated ECIDs  ExperienceEvent.identityMap["ECID"]` |
| `signals` | `ExperienceEvent.signals` |
| `b_time` | `ExperienceEvent.timeStamp` |
| `overwrite` | `overwriteTraits` |

>[!NOTE] Les champs entrants doivent être abandonnés dans une prochaine version.

## Données 

Type :  XDM

| Champ  | Champ XDM |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
