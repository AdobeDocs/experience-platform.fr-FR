---
solution: Experience Platform
title: Mappage des données d’événement Adobe Target avec XDM
description: Découvrez comment mapper des champs d’événement Adobe Target à un schéma de modèle de données d’expérience (XDM) pour une utilisation dans Adobe Experience Platform.
exl-id: dab08ab6-6c1c-460a-bb52-8dcdb5709a34
source-git-commit: 81412493b096264ce7a89e3ca2348edb2dcd1798
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 79%

---

# Mappages des champs de mapping de ciblage

Le tableau suivant décrit les champs d’un schéma d’événement d’expérience de modèle de données d’expérience (XDM) et les champs correspondants d’Adobe Target vers lesquels ils doivent être mappés. Des notes supplémentaires pour certains mappages sont également fournies.

>[!NOTE]
>
>Faites défiler vers la gauche ou vers la droite pour afficher l’intégralité du tableau.

| Champ XDM ExperienceEvent | Champ de requête cible | Notes |
| ------------------------- | -------------------- | ----- |
| **`id`** | Un identifiant de requête unique |
| **`dataSource`** | | Configuré sur « 1 » pour tous les clients. |
| `dataSource._id` | Une valeur générée par le système qui ne peut pas être transmise avec la requête. | L’ID unique de cette source de données. Fourni par la personne ou le système qui a créé la source de données. |
| `dataSource.code` | Une valeur générée par le système qui ne peut pas être transmise avec la requête. | Un raccourci vers la valeur @id complète. Vous pouvez utiliser au moins un code ou une valeur @id. Parfois, ce code est appelé code d’intégration de la source de données. |
| `dataSource.tags` | Une valeur générée par le système qui ne peut pas être transmise avec la requête. | Les balises servent à indiquer la façon dont les alias représentés par une source de données spécifique doivent être interprétés par les applications utilisant ces alias.<br><br>Exemples :<br><ul><li>`isAVID` : sources de données représentant les identifiants de visiteurs Analytics.</li><li>`isCRSKey` : sources de données représentant des alias qui doivent être utilisés comme clés dans CRS.</li></ul>Les balises sont définies lors de la création de la source de données, mais elles sont également incluses dans les messages de pipeline lors du référencement d’une source de données spécifique. |
| **`timestamp`** | Date et heure d’événement |
| **`channel`** | `context.channel` | Fonctionne uniquement avec la diffusion de l’affichage. « web » et « mobile » sont les options disponibles, « web » étant la valeur par défaut. |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` | L’identifiant Experience Cloud (ECID) est également connu sous le nom de MCID et continue à être utilisé dans les espaces de noms. |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | Le nom de l’opérateur de téléphonie mobile résolu en fonction de l’adresse IP de la requête. |
| `environment.ipV4` | `mboxRequest.ipAddress` (si au format V4) |
| `environment.ipV6` | `mboxRequest.ipAddress` (si au format V6) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Mappage interne de la cible pour les environnements définis par le client (de développement, de contrôle qualité ou de production, par exemple). |
| `experience.target.supplementalDataID` | Identifiant utilisé pour rassembler les événements cibles et les événements Analytics |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | Liste (tableau) des activités pour lesquelles le visiteur a rempli les critères |
| `experience.target.activities[i].activityID` | L’identifiant d’une activité pour laquelle le visiteur a rempli les critères |
| `experience.target.activities[i].version` | La version d’une activité pour laquelle le visiteur a rempli les critères |
| `experience.target.activities[i].activityEvents` | Inclut les détails des événements d’activité auxquels l’utilisateur a accédé grâce à cet événement. |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | L’une des propriétés suivantes de `deviceAtlas` (ou valeur nulle) : <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | (chaîne vide) |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | (chaîne vide) |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | UUID aléatoire (obligatoire) |
| `placeContext.geo.city` | Le nom de la ville résolu en fonction de l’adresse IP de la requête. |
| `placeContext.geo.countryCode` | Le code pays résolu en fonction de l’adresse IP de la requête. |
| `placeContext.geo.dmaId` | Le code régional du marché désigné résolu en fonction de l’adresse IP de la requête. |
| `placeContext.geo.postalCode` | Le code postal résolu en fonction de l’adresse IP de la requête. |
| `placeContext.geo.stateProvince` | La province ou l’État résolu en fonction de l’adresse IP de la requête. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** | | Défini uniquement si les informations sur la commande sont présentes dans la requête. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |

{style="table-layout:auto"}
