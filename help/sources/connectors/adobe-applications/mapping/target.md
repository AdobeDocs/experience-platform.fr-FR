---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Champ Mapping de ciblage
topic: overview
translation-type: tm+mt
source-git-commit: 53fb7ea201ed9361584d24c8bd2ad10edd9f3975
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# Champs de Mapping de ciblage

Adobe Experience Platform vous permet d’assimiler des données de Cible Adobe par le biais du connecteur source de la Cible. Lors de l’utilisation du connecteur, toutes les données des champs de Cible doivent être mises en correspondance avec les champs du modèle de données d’ [expérience (XDM)](../../../../xdm/home.md) associés à la classe XDM ExperienceEvent.

Le tableau suivant décrit les champs d’un schéma de Événement d’expérience (champ *ExpérienceXDM) et les champs de Cible correspondants auxquels ils doivent être associés (champ* Demande de ** Cible). Des notes supplémentaires pour certains mappages sont également fournies.

>[!NOTE] Veuillez faire défiler la page vers la gauche/vers la droite pour vue du contenu complet du tableau.

| Champ XDM ExperienceEvent | Champ Demande de Cible | Notes |
| ------------------------- | -------------------- | ----- |
| **`id`** | Un identifiant de demande unique |
| **`dataSource`** |  | Configuré sur &quot;1&quot; pour tous les clients. |
| `dataSource._id` | Valeur générée par le système qui ne peut pas être transmise avec la requête. | ID unique de cette source de données. Cela serait fourni par la personne ou le système qui a créé la source de données. |
| `dataSource.code` | Valeur générée par le système qui ne peut pas être transmise avec la requête. | raccourci vers le @id complet. Au moins un des codes ou @id peut être utilisé. Il arrive que ce code soit appelé code d’intégration de la source de données. |
| `dataSource.tags` | Valeur générée par le système qui ne peut pas être transmise avec la requête. | Les balises sont utilisées pour indiquer comment les alias représentés par une source de données donnée doivent être interprétés par les applications utilisant ces alias.<br><br>Exemples :<br><ul><li>`isAVID`: Sources de données représentant les identifiants des visiteurs Analytics.</li><li>`isCRSKey`: Sources de données représentant des alias qui doivent être utilisés comme clés dans CRS.</li></ul>Les balises sont définies lors de la création de la source de données, mais elles sont également incluses dans les messages de pipeline lors du référencement d’une source de données donnée. |
| **`timestamp`** | Horodatage Événement |
| **`channel`** | `context.channel` | Fonctionne uniquement avec la diffusion de vue. Les options sont &quot;web&quot; et &quot;mobile&quot;, &quot;web&quot; étant la valeur par défaut. |
| **`endUserIds`** |
| `endUserIds.experience.tntId` | `tntId/mboxPC` |
| `endUserIds.experience.mcId` | `marketingCloudVisitorId` |
| **`environment`** |
| `environment.browserDetails.userAgent` | `mboxRequest.userAgent` |
| `environment.browserDetails.viewPortHeight` | `mboxRequest.browserHeight` |
| `environment.browserDetails.viewPortWidth` | `mboxRequest.browserWidth` |
| `environment.operatingSystem` | `deviceAtlas.osName` |
| `environment.operatingSystemVersion` | `deviceAtlas.osVersion` |
| `environment.viewportHeight` | `mboxRequest.screenHeight` |
| `environment.viewportWidth` | `mboxRequest.screenWidth` |
| `environment.colorDepth` | `mboxRequest.colorDepth` |
| `environment.carrier` | Le nom de l’opérateur de téléphonie mobile a été résolu en fonction de l’adresse IP de la demande. |
| `environment.ipV4` | `mboxRequest.ipAddress` (si au format V4) |
| `environment.ipV6` | `mboxRequest.ipAddress` (si au format V6) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Mappage interne des Cibles pour les environnements définis par le client (tels que dev, qa ou prod). |
| `experience.target.supplementalDataID` | Identifiant utilisé pour associer des événements de Cible à des événements Analytics |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` | Liste (tableau) des activités pour lesquelles le visiteur a été qualifié |
| `experience.target.activities[i].activityID` | ID d’une activité donnée pour laquelle le visiteur s’est qualifié |
| `experience.target.activities[i].version` | La version de toute activité donnée pour laquelle le visiteur s’est qualifié |
| `experience.target.activities[i].activityEvents` | Inclut les détails des événements d’activité que l’utilisateur a atteints avec ce événement. |
| **`device`** |
| `device.typeIDService` | `XDMDevice.Device.TypeIDService.typeIDService_deviceatlas` |
| `device.type` | L’une des propriétés suivantes de `deviceAtlas` (ou NULL) : <ul><li>`type_mobile`</li><li>`type_tablet`</li><li>`type_desktop`</li><li>`type_ereader`</li><li>`type_television`</li><li>`type_settop`</li><li>`type_mediaplayer`</li></ul> |
| `device.typeID` | (chaîne vide) |
| `device.manufacturer` | `deviceAtlas.manufacturer` |
| `device.model` | `deviceAtlas.model` |
| `device.modelNumber` | (chaîne vide) |
| `device.screenHeight` | `deviceAtlas.displayHeight` |
| `device.screenWidth` | `deviceAtlas.displayWidth` |
| `device.colorDepth` | `deviceAtlas.displayColorDepth` |
| **`placeContext`** |
| `placeContext.geo.id` | UUID aléatoire (obligatoire) |
| `placeContext.geo.city` | Le nom de la ville a été résolu en fonction de l’adresse IP de la demande. |
| `placeContext.geo.countryCode` | Code de pays résolu en fonction de l’adresse IP de la demande. |
| `placeContext.geo.dmaId` | Code de zone de marché désignée résolu en fonction de l’adresse IP de la demande. |
| `placeContext.geo.postalCode` | Le code postal a été résolu en fonction de l’adresse IP de la requête. |
| `placeContext.geo.stateProvince` | Etat ou province résolu en fonction de l’adresse IP de la demande. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | Défini uniquement si les détails de la commande sont présents dans la demande. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |
