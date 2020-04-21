---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Champ '
topic: overview
translation-type: tm+mt
source-git-commit: 53fb7ea201ed9361584d24c8bd2ad10edd9f3975

---


# Champs de 

Adobe Experience Platform vous permet d’assimiler des données  Adobe par l’intermédiaire du connecteur source . Lors de l’utilisation du connecteur, toutes les données des champs de  du doivent être mises en correspondance avec les champs XDM ( [Experience Data Model)](../../../../xdm/home.md) associés à la classe XDM ExperienceEvent.

Le tableau suivant décrit les champs d’un  d’expérience  de l’ (champ *Expérience* XDM) et les champs d’*événement d’expérience auxquels ils doivent être mappés (champ* Demande dede deXDM). Des notes supplémentaires pour certains mappages sont également fournies.

>[!NOTE] Faites défiler vers la gauche ou vers la droite pour  le contenu complet du tableau.

| Champ XDM ExperienceEvent | Champ de requête  | Notes |
| ------------------------- | -------------------- | ----- |
| **`id`** | Un identifiant de requête unique |
| **`dataSource`** |  | Configuré sur &quot;1&quot; pour tous les clients. |
| `dataSource._id` | Valeur générée par le système qui ne peut pas être transmise avec la requête. | ID unique de cette source de données. Cela serait fourni par la personne ou le système qui a créé la source de données. |
| `dataSource.code` | Valeur générée par le système qui ne peut pas être transmise avec la requête. | Raccourci vers le @id complet. Vous pouvez utiliser au moins un code ou @id. Parfois, ce code est appelé code d’intégration de la source de données. |
| `dataSource.tags` | Valeur générée par le système qui ne peut pas être transmise avec la requête. | Les balises sont utilisées pour indiquer comment les alias représentés par une source de données donnée doivent être interprétés par les applications utilisant ces alias.<br><br>Exemples :<br><ul><li>`isAVID`: Sources de données représentant les ID de Analytics.</li><li>`isCRSKey`: Sources de données représentant des alias qui doivent être utilisés comme clés dans CRS.</li></ul>Les balises sont définies lors de la création de la source de données, mais elles sont également incluses dans les messages de pipeline lors du référencement d’une source de données donnée. |
| **`timestamp`** | Horodatage  |
| **`channel`** | `context.channel` | Fonctionne uniquement avec  . Les options sont &quot;web&quot; et &quot;mobile&quot;, avec &quot;web&quot; comme valeur par défaut. |
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
| `environment.carrier` | Le nom de l’opérateur de téléphonie mobile a été résolu en fonction de l’adresse IP de la requête. |
| `environment.ipV4` | `mboxRequest.ipAddress` (si au format V4) |
| `environment.ipV6` | `mboxRequest.ipAddress` (si au format V6) |
| **`experience`** |
| `experience.target.clientCode` | `mboxRequest.client` |
| `experience.target.mboxName` | `mboxRequest.mboxName` |
| `experience.target.mboxVersion` | `mboxRequest.mboxVersion` |
| `experience.target.sessionId` | `mboxRequest.sessionId` |
| `experience.target.environmentID` | Correspondance interne  pour les  de définis par le client (comme dev, qa ou prod). |
| `experience.target.supplementalDataID` | Identifiant utilisé pour assembler   avec les  Analytics de la |
| `experience.target.pageDetails.pageId` | `mboxRequest.pageId` |
| `experience.target.pageDetails.pageScore` | `mboxRequest.mboxPageValue` |
| `experience.target.activities` |  (tableau) de   le a qualifié pour |
| `experience.target.activities[i].activityID` | ID de tout  donné  le qualifié pour |
| `experience.target.activities[i].version` | La version de tout  donné  le qualifié pour |
| `experience.target.activities[i].activityEvents` | Inclut les détails de    l&#39;utilisateur a atteint avec ce. |
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
| `placeContext.geo.city` | Le nom de la ville a été résolu en fonction de l’adresse IP de la requête. |
| `placeContext.geo.countryCode` | Code pays résolu en fonction de l’adresse IP de la requête. |
| `placeContext.geo.dmaId` | Code de zone de marché désignée résolu en fonction de l’adresse IP de la requête. |
| `placeContext.geo.postalCode` | Code postal résolu en fonction de l’adresse IP de la requête. |
| `placeContext.geo.stateProvince` | Etat ou province résolu en fonction de l’adresse IP de la requête. |
| `placeContext.localTime` | `mboxRequest.offsetTime` + `mboxRequest.currentServerTime` |
| **`commerce`** |  | Défini uniquement si les détails de la commande sont présents dans la requête. |
| `commerce.order.priceTotal` | `mboxRequest.orderTotal` |
| `commerce.order.purchaseOrderNumber` | `mboxRequest.orderId` |
| `commerce.order.purchaseID` | `mboxRequest.orderId` |
| **`web`** |
| `web.withWebPageDetails.url` | `mboxURL.context.address.url` |
| `web.webReferrer.url` | `mboxReferrer.context.address.url` |
| **`identityMap`** |
| `identityMap.TNTID` | `tntId.mboxPC` |
| `identityMap.ECID` | `marketingCloudVisitorId` |
