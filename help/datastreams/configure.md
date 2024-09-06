---
title: Création et configuration des flux de données
description: Découvrez comment connecter votre intégration SDK Web côté client à d’autres produits Adobe et destinations tierces.
exl-id: 4924cd0f-5ec6-49ab-9b00-ec7c592397c8
source-git-commit: f99370a9bff156b5cf9ecf286a1f8bc09eccc06a
workflow-type: tm+mt
source-wordcount: '2813'
ht-degree: 52%

---


# Création et configuration des flux de données

Ce document décrit les étapes de configuration d’un [flux de données](./overview.md) dans l’interface utilisateur.

## Accéder à l’espace de travail [!UICONTROL Flux de données]

Vous pouvez créer et gérer des flux de données dans l’interface utilisateur de collecte de données ou d’Experience Platform en sélectionnant **[!UICONTROL Flux de données]** dans le volet de navigation de gauche.

![Onglet Flux de données dans l’interface utilisateur de collecte de données](assets/configure/datastreams-tab.png)

L’onglet **[!UICONTROL Flux de données]** affiche une liste des flux de données existants, y compris leur nom convivial, leur identifiant et leur date de dernière modification. Pour [afficher ses détails et configurer les services](#view-details), sélectionnez le nom d’un flux de données.

Pour afficher d’autres options pour un flux de données spécifique, sélectionnez l’icône &quot;plus&quot; (**...**). Pour mettre à jour la [configuration de base](#configure) de la chaîne de données, sélectionnez **[!UICONTROL Modifier]**. Pour supprimer la chaîne de données, sélectionnez **[!UICONTROL Supprimer]**.

![Options de modification ou de suppression d’un flux de données existant](assets/configure/edit-datastream.png)

## Création dʼun flux de données {#create}

Pour créer un flux de données, commencez par sélectionner **[!UICONTROL Nouveau flux de données]**.

![Sélectionner un nouveau flux de données](assets/configure/new-datastream-button.png)

Le processus de création du flux de données s’affiche, en commençant à l’étape de configuration. Ensuite, vous devez fournir un nom et une description facultative pour le flux de données.

Si vous configurez un flux de données à utiliser dans Experience Platform et que vous utilisez également le SDK Web, vous devez également sélectionner un [schéma de modèle de données d’expérience basé sur un événement (XDM)](../xdm/classes/experienceevent.md) pour représenter les données que vous prévoyez d’ingérer.

![Configuration de base d’un flux de données](assets/configure/configure.png)

### Configuration de la géolocalisation et de la recherche réseau {#geolocation-network-lookup}

La géolocalisation et les paramètres de recherche réseau vous aident à définir le niveau de granularité des données géographiques et réseau que vous souhaitez collecter.

Développez la section **[!UICONTROL Géolocalisation et recherche réseau]** pour configurer les paramètres décrits ci-dessous.

![Écran de configuration de la matrice de données avec les paramètres de géolocalisation et de recherche réseau surlignés.](assets/configure/geolookup.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Recherche géographique] | Active les recherches de géolocalisation pour les options sélectionnées en fonction de l’adresse IP du visiteur. Les options disponibles sont les suivantes : <ul><li>**Country** : renseigne `xdm.placeContext.geo.countryCode`</li><li>**Postal Code** : renseigne `xdm.placeContext.geo.postalCode`</li><li>**État/Province** : renseigne `xdm.placeContext.geo.stateProvince`</li><li>**DMA** : renseigne `xdm.placeContext.geo.dmaID`</li><li>**Ville** : renseigne `xdm.placeContext.geo.city`</li><li>**Latitude** : renseigne `xdm.placeContext.geo._schema.latitude`</li><li>**Longitude** : renseigne `xdm.placeContext.geo._schema.longitude`</li></ul>Les options **[!UICONTROL Ville]**, **[!UICONTROL Latitude]** ou **[!UICONTROL Longitude]** fournissent des coordonnées jusqu’à deux décimales, indépendamment des autres options sélectionnées. Il s’agit d’une granularité au niveau de la ville.<br> <br> Si vous ne sélectionnez aucune option, les recherches de géolocalisation sont désactivées. La géolocalisation se produit avant [!UICONTROL l’obscurcissement d’IP], ce qui signifie qu’elle n’est pas affectée par le paramètre [!UICONTROL  d’obscurcissement d’IP]. |
| [!UICONTROL Recherche réseau] | Active les recherches réseau pour les options sélectionnées en fonction de l’adresse IP du visiteur. Les options disponibles sont les suivantes : <ul><li>**Opérateur** : renseigne `xdm.environment.carrier`</li><li>**Domaine** : renseigne `xdm.environment.domain`</li><li>**ISP** : renseigne `xdm.environment.ISP`</li></ul> |

Si vous activez l’un des champs ci-dessus pour la collecte de données, assurez-vous de définir correctement la propriété de tableau [`context`](/help/web-sdk/commands/configure/context.md) lors de la configuration du SDK Web.

Les champs de recherche de géolocalisation utilisent la chaîne de tableau `context` `"placeContext"`, tandis que les champs de recherche réseau utilisent la chaîne de tableau `context` `"environment"`.

Vérifiez également que chaque champ XDM souhaité existe dans votre schéma. Dans le cas contraire, vous pouvez ajouter le groupe de champs `Environment Details` fourni par l’Adobe à votre schéma.

### Configuration de la recherche de périphérique {#geolocation-device-lookup}

Les paramètres de **[!UICONTROL recherche de périphérique]** vous permettent de sélectionner des informations spécifiques à l’appareil que vous souhaitez collecter.

Développez la section **[!UICONTROL Recherche de périphérique]** pour configurer les paramètres décrits ci-dessous.

![Écran de configuration de la banque de données avec les paramètres de recherche d’appareil surlignés.](assets/configure/device-lookup.png)

>[!IMPORTANT]
>
>Les paramètres affichés dans le tableau ci-dessous s’excluent mutuellement. Vous ne pouvez pas sélectionner simultanément les informations de recherche d’agent utilisateur *et les données de recherche d’appareil*.

| Paramètre | Description |
| --- | --- |
| **[!UICONTROL Conserver les en-têtes d’agent utilisateur et d’astuces client]** | Sélectionnez cette option pour ne collecter que les informations stockées dans la chaîne de l’agent utilisateur. Ce paramètre est sélectionné par défaut. Renseigne `xdm.environment.browserDetails.userAgent` |
| **[!UICONTROL Utilisez la recherche de périphérique pour collecter les informations suivantes]** | Sélectionnez cette option si vous souhaitez collecter une ou plusieurs des informations suivantes spécifiques à l’appareil : <ul><li>**[!UICONTROL Device]** information :<ul><li>**Fabricant de l’appareil** : renseigne `xdm.device.manufacturer`</li><li>**Modèle de périphérique** : renseigne `xdm.device.modelNumber`</li><li>**Nom marketing** : renseigne `xdm.device.model`</li></ul></li><li>**[!UICONTROL Matériel]** : <ul><li>**Type de matériel** : renseigne `xdm.device.type`</li><li>**Hauteur d’affichage** : renseigne `xdm.device.screenHeight`</li><li>**Largeur d’affichage** : renseigne `xdm.device.screenWidth`</li><li>**Profondeur d’affichage des couleurs** : renseigne `xdm.device.colorDepth`</li></ul></li><li>**[!UICONTROL Informations sur le navigateur]** : <ul><li>**Fournisseur de navigateur** : renseigne `xdm.environment.browserDetails.vendor`</li><li>**Nom du navigateur** : renseigne `xdm.environment.browserDetails.name`</li><li>**Version du navigateur** : renseigne `xdm.environment.browserDetails.version`</li></ul></li><li>**[!UICONTROL Informations sur le système d’exploitation]** : <ul><li>**Fournisseur du système d’exploitation** : renseigne `xdm.environment.operatingSystemVendor`</li><li>**Nom du système d&#39;exploitation** : renseigne `xdm.environment.operatingSystem`</li><li>**Version du système d&#39;exploitation** : renseigne `xdm.environment.operatingSystemVersion`</li></ul></li></ul>Les informations de recherche de périphérique ne peuvent pas être collectées avec l’agent utilisateur et les conseils client. Si vous choisissez de collecter des informations sur l’appareil, la collecte des indices de l’agent utilisateur et du client est désactivée, et vice versa. |
| **[!UICONTROL Ne collectez aucune information sur l&#39;appareil]** | Sélectionnez cette option si vous ne souhaitez collecter aucune information de recherche de périphérique. Aucune donnée sur l’appareil, le matériel, le navigateur, le système d’exploitation, l’agent utilisateur ou l’indice client n’est collectée. |

Si vous activez l’un des champs ci-dessus pour la collecte de données, assurez-vous de définir correctement la propriété de tableau [`context`](/help/web-sdk/commands/configure/context.md) lors de la configuration du SDK Web.

Les informations sur le périphérique et le matériel utilisent la chaîne de tableau `context` `"device"`, tandis que les informations sur le navigateur et le système d’exploitation utilisent la chaîne de tableau `context` `"environment"`.

Vérifiez également que chaque champ XDM souhaité existe dans votre schéma. Dans le cas contraire, vous pouvez ajouter le groupe de champs `Environment Details` fourni par l’Adobe à votre schéma.

### Configuration des options avancées {#@advanced-options}

Pour afficher les options de configuration avancées, sélectionnez **[!UICONTROL Options avancées]**. Ici, vous pouvez configurer des paramètres de flux de données supplémentaires, tels que l’obscurcissement des adresses IP, les cookies d’ID propriétaires, etc.

![Options de configuration avancées](assets/configure/advanced-settings.png)

>[!IMPORTANT]
>
> Il vous incombe de vous assurer que vous avez obtenu toutes les autorisations, consentements, autorisations et autorisations nécessaires en vertu des lois et réglementations applicables pour collecter, traiter et transmettre des données personnelles, y compris des informations de géolocalisation précises.
> 
> Votre sélection de l’obscurcissement des adresses IP n’a aucune incidence sur le niveau des informations de géolocalisation qui sont dérivées de l’adresse IP et envoyées à vos solutions d’Adobe configurées. Les recherches de géolocalisation doivent être limitées ou désactivées séparément.

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Obscurcissement d’IP] | Indique le type d’obscurcissement d’adresses IP à appliquer au train de données. Tout traitement basé sur l’adresse IP du client est affecté par le paramètre d’obscurcissement de l’adresse IP. Cela inclut tous les services Experience Cloud qui reçoivent des données de votre train de données. <p>Options disponibles :</p> <ul><li>**[!UICONTROL Aucun]** : désactive l’obscurcissement des adresses IP. L’adresse IP complète de l’utilisateur est envoyée via la banque de données.</li><li>**[!UICONTROL Partiel]** : obscurcit le dernier octet de l’adresse IP pour les adresses IPv4. Pour les adresses IPv6, l’obscurcissement masque les 80 derniers bits de l’adresse IP. <p>Exemples :</p> <ul><li>IPv4 : `1.2.3.4` -> `1.2.3.0`</li><li>IPv6 : `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `2001:0db8:1345:0000:0000:0000:0000:0000`</li></ul></li><li>**[!UICONTROL Complet]** : obscurcit l’intégralité de l’adresse IP. <p>Exemples :</p> <ul><li>IPv4 : `1.2.3.4` -> `0.0.0.0`</li><li>IPv6 : `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `0:0:0:0:0:0:0:0`</li></ul></li></ul> Impact de l’obscurcissement des adresses IP sur d’autres produits Adobe : <ul><li>**Adobe Target** : l’obscurcissement de l’adresse IP au niveau du flux de données [!UICONTROL  est appliqué avant l’ [!UICONTROL obscurcissement de l’adresse IP] effectué dans Adobe Target, à toutes les adresses IP présentes dans la requête. ] Par exemple, si l’option [!UICONTROL  d’obscurcissement d’IP ] au niveau de la banque de données est définie sur **[!UICONTROL Full]** et que l’option d’obscurcissement d’IP d’Adobe Target est définie sur **[!UICONTROL Last octet obfuscation]**, Adobe Target reçoit une adresse IP entièrement obscurcie. Si l’option [!UICONTROL  d’obscurcissement d’IP] au niveau du flux de données est définie sur **[!UICONTROL Partial]** et que l’option d’obscurcissement d’IP d’Adobe Target est définie sur **[!UICONTROL Full]**, Adobe Target reçoit une adresse IP partiellement obscurcie, puis applique l’obscurcissement complet sur celle-ci. L’obscurcissement des adresses IP d’Adobe Target est géré indépendamment de celui du flux de données. Pour plus d’informations, consultez la documentation d’Adobe Target sur l’[Obscurcissement d’adresses IP](https://experienceleague.adobe.com/docs/target-dev/developer/implementation/privacy/privacy.html) et sur la [géolocalisation](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html).</li><li>**Audience Manager** : le paramètre [!UICONTROL obscurcissement d’IP] au niveau du flux de données est appliqué avant l’ [!UICONTROL obscurcissement d’IP] effectué en Audience Manager, à toutes les adresses IP présentes dans la requête. Les recherches de géolocalisation effectuées dans Audience Manager sont affectées par l’option [!UICONTROL Obscurcissement d’adresses IP] définie au niveau du train de données. Une recherche de géolocalisation dans l’Audience Manager, basée sur une adresse IP complètement obscurcie, génère une région inconnue et aucun segment basé sur les données de géolocalisation résultantes n’est réalisé. Pour plus d’informations, consultez la documentation d’Audience Manager sur l’[Obscurcissement d’adresses IP](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/ip-obfuscation.html).</li><li>**Adobe Analytics** : si le paramètre d’obscurcissement de l’adresse IP au niveau du flux de données est défini sur **[!UICONTROL Full]**, Adobe Analytics traite l’adresse IP comme vide. Cela affecte tout traitement Analytics qui dépend de l’adresse IP, comme les recherches de géolocalisation et le filtrage IP. Pour qu’Analytics reçoive les adresses IP non obscurcies ou partiellement obscurcies, définissez le paramètre d’obscurcissement d’IP sur **[!UICONTROL Partial]** ou **[!UICONTROL None]**. Dans Analytics, il est possible d’obscurcir davantage les adresses IP partiellement obscurcies et non obscurcies. Pour plus d’informations sur l’activation de l’obscurcissement des adresses IP dans Analytics, reportez-vous à la [documentation](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/general-acct-settings-admin.html?lang=fr) d’Adobe Analytics. Si l’adresse IP est complètement obscurcie et que l’accès à la page ne comporte ni [!DNL ECID] ni [!DNL VisitorID], Analytics abandonne l’accès au lieu de générer un [identifiant de secours](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-ids.html?lang=en), qui est partiellement basé sur l’adresse IP.</li></ul> |
| [!UICONTROL Cookie interne d’identifiant] | Lorsqu’il est activé, ce paramètre indique à Edge Network de se référer à un cookie spécifié lors de la recherche d’un [identifiant d’appareil interne](../web-sdk/identity/first-party-device-ids.md), plutôt que de rechercher cette valeur dans le mappage d’identité.<br><br>Lorsque vous activez ce paramètre, vous devez indiquer le nom du cookie qui doit stocker l’ID. |
| [!UICONTROL Synchronisation des identifiants tiers] | Les synchronisations des identifiants peuvent être regroupées en conteneurs afin de permettre l’exécution de différentes synchronisations d’identifiant à différents moments. Lorsqu’il est activé, ce paramètre vous permet de spécifier le conteneur des synchronisations d’identifiant à exécuter pour ce flux de données. |
| [!UICONTROL ID de conteneur de synchronisation d’identifiants tiers] | L’identifiant numérique du conteneur à utiliser pour la synchronisation des identifiants tiers. |
| [!UICONTROL Remplacements d’identifiants de conteneur] | Dans cette section, vous pouvez définir des identifiants de conteneur de synchronisation d’identifiants tiers supplémentaires que vous pouvez utiliser pour remplacer celui par défaut. |
| [!UICONTROL Type d’accès] | Définit le type d’authentification qu’Edge Network accepte pour le train de données. <ul><li>**[!UICONTROL Authentification mixte]** : lorsque cette option est activée, Edge Network accepte les demandes authentifiées et non authentifiées. Sélectionnez cette option lorsque vous prévoyez d’utiliser le SDK web ou le [SDK mobile](https://developer.adobe.com/client-sdks/home/), ainsi que l’[API Server](../server-api/overview.md). </li><li>**[!UICONTROL Authentifié uniquement]** : lorsque cette option est activée, Edge Network accepte uniquement les demandes authentifiées. électionnez cette option lorsque vous prévoyez d’utiliser uniquement l’API Server et que vous souhaitez empêcher le traitement des demandes non authentifiées par Edge Network.</li></ul> |
| [!UICONTROL Media Analytics] | Active le traitement des données de suivi en continu pour l’intégration des Edge Network via les SDK Experience Platform ou l’ [ API Media Edge](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/getting-started/). Découvrez Media Analytics à partir de la [documentation](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=fr). |

Ensuite, si vous configurez le flux de données d’Experience Platform, suivez le tutoriel sur la [Préparation des données pour la collecte de données](./data-prep.md) afin de mapper les données à un schéma d’événement de Platform avant de revenir à ce guide. Sinon, sélectionnez **[!UICONTROL Enregistrer]** et passez à la section suivante.

## Afficher les détails d’un flux de données {#view-details}

Après avoir configuré un nouveau flux de données ou sélectionné un flux de données existant à afficher, sa page de détails s’affiche. Vous y trouverez des informations supplémentaires sur le flux de données, y compris son identifiant.

![Page des détails du flux de données.](assets/configure/view-details.png)

À partir de l’écran de détails du flux de données, vous pouvez [ajouter des services](#add-services) pour activer les fonctionnalités des produits Adobe Experience Cloud auxquels vous avez accès. Vous pouvez également modifier la [configuration de base](#create) du flux de données, mettre à jour ses [règles de mappage](./data-prep.md), [copier le flux de données](#copy) ou le supprimer entièrement.

## Ajouter des services à un flux de données {#add-services}

Sur la page de détails d’un flux de données, sélectionnez **[!UICONTROL Ajouter un service]** pour commencer à ajouter les services disponibles à ce flux de données.

![Sélectionnez Ajouter un service pour continuer.](assets/configure/add-service.png)

Sur l’écran suivant, utilisez le menu déroulant pour sélectionner un service à configurer pour ce flux de données. Seuls les services auxquels vous avez accès sont répertoriés dans cette liste.

![Sélectionnez un service dans la liste.](assets/configure/service-selection.png)

Sélectionnez le service souhaité, renseignez les options de configuration qui s’affichent, puis sélectionnez **[!UICONTROL Enregistrer]** pour ajouter le service au flux de données. Tous les services ajoutés s’affichent dans la vue des détails du flux de données.

![Services ajoutés à un flux de données](assets/configure/services-added.png)

Les sous-sections ci-dessous décrivent les options de configuration de chaque service.

>[!NOTE]
>
>Chaque configuration de service contient un bouton **[!UICONTROL Activer]** qui est automatiquement activé lorsque le service est sélectionné. Pour désactiver le service sélectionné de ce flux de données, sélectionnez à nouveau le bouton **[!UICONTROL Activer]**.

### Paramètres d’Adobe Analytics {#analytics}

Ce service contrôle si et comment les données sont envoyées à Adobe Analytics. Voir [Envoi de données à Adobe Analytics](/help/web-sdk/use-cases/adobe-analytics.md).

![Paramètres de la banque de données Adobe Analytics.](assets/configure/analytics-config.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Identifiant de suite de rapports] | **(Obligatoire)** L’identifiant de la suite de rapports Analytics à laquelle vous souhaitez envoyer des données. Cet identifiant se trouve dans l’interface utilisateur d’Adobe Analytics sous [!UICONTROL Administration] > [!UICONTROL Suites de rapports]. Si plusieurs suites de rapports sont spécifiées, les données sont copiées dans chaque suite de rapports. |
| [!UICONTROL Espace de noms d’identifiant visiteur] | (Facultatif) L’espace de noms que vous souhaitez utiliser pour Adobe Analytics [visitorID](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html?lang=fr). Lorsque vous envoyez un événement avec une valeur spécifiée pour cet espace de noms, il sera automatiquement utilisé comme `visitorID` dans Analytics. |
| [!UICONTROL Remplacements de suites de rapports] | Dans cette section, vous pouvez ajouter d’autres identifiants de suites de rapports que vous pouvez utiliser pour remplacer celui par défaut. |

### Paramètres d’Adobe Audience Manager {#audience-manager}

Ce service contrôle si et comment les données sont envoyées à Adobe Audience Manager. Il suffit d’activer cette section pour envoyer des données à Audience Manager. Les autres paramètres sont facultatifs, mais recommandés.

![ Adobe Audience Gérer les paramètres de flux de données.](assets/configure/audience-manager-config.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Destinations de cookie activées] | Permet au SDK de partager des informations sur les segments via les [destinations de cookie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html?lang=fr) d’[!DNL Audience Manager]. |
| [!UICONTROL Destinations d’URL activées] | Permet au SDK de partager des informations sur les segments via les [destinations d’URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html?lang=fr) d’[!DNL Audience Manager]. |

### Paramètres d’Adobe Experience Platform {#aep}

>[!IMPORTANT]
>
>Lors de l’activation d’un flux de données pour Platform, notez le sandbox Platform que vous utilisez actuellement, tel qu’affiché dans le ruban supérieur de l’interface utilisateur.
>
>![Sandbox sélectionné](assets/configure/platform-sandbox.png)
>
>Les sandbox sont des partitions virtuelles dans Adobe Experience Platform qui vous permettent d’isoler les données et mises en œuvre des autres membres de l’organisation. Une fois un flux de données créé, le sandbox ne peut plus être modifié. Pour plus d’informations sur le rôle des sandbox dans Experience Platform, consultez la [documentation sur les sandbox](../sandboxes/home.md).

Ce service contrôle si et comment les données sont envoyées à Adobe Experience Platform.

![Paramètres de la transmission de données Adobe Experience Platform.](assets/configure/platform-config.png)

| Paramètre | Description |
|---| --- |
| [!UICONTROL Jeu de données d’événement] | **(Obligatoire)** Sélectionnez le jeu de données de Platform vers lequel les données d’événement client seront diffusées. Ce schéma doit utiliser la [classe XDM ExperienceEvent](../xdm/classes/experienceevent.md). Pour ajouter d’autres jeux de données, sélectionnez **[!UICONTROL Ajouter un jeu de données d’événement]**. |
| [!UICONTROL Jeu de données de profil] | Sélectionnez le jeu de données de Platform auquel les données d’attribut du client seront envoyées. Ce schéma doit utiliser la [classe XDM Individual Profile](../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Permet l’Offer decisioning des mises en oeuvre du SDK Web. Pour plus d’informations sur l’implémentation, consultez le guide sur [l’utilisation d’Offer Decisioning avec SDK Web](../web-sdk/personalization/offer-decisioning/offer-decisioning-overview.md) .<br><br>Pour plus d’informations sur les fonctionnalités d’Offer Decisioning, consultez la [Documentation d’Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/get-started-decision/starting-offer-decisioning.html?lang=fr). |
| [!UICONTROL Segmentation Edge] | Active la [segmentation Edge](../segmentation/ui/edge-segmentation.md) pour ce flux de données. Lorsque le [SDK Web](../web-sdk/home.md) ou l’ [ API de serveur Edge Network](../server-api/overview.md) envoie des données par le biais d’un flux de données avec la segmentation Edge activée, toutes les appartenances d’audience mises à jour pour le profil en question sont renvoyées dans la réponse.<br><br>Vous pouvez utiliser cette option en combinaison avec **[!UICONTROL Destinations Personalization]** pour les cas d’utilisation de personnalisation de la même page et de la page suivante par le biais de [destinations de périphérie](../destinations/ui/activate-edge-personalization-destinations.md) ou [!DNL Offer Decisioning]. |
| [!UICONTROL Destinations de personnalisation] | Lorsque vous activez cette fonction après avoir activé la case à cocher [!UICONTROL Segmentation Edge], cette option permet au flux de données de se connecter aux destinations de personnalisation, telles que [Personnalisation personnalisée](../destinations/catalog/personalization/custom-personalization.md).<br><br>Consultez la documentation des destinations pour obtenir des instructions spécifiques sur la [configuration des destinations de personnalisation](../destinations/ui/activate-edge-personalization-destinations.md). |
| [!UICONTROL Adobe Journey Optimizer] | Active [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=fr) pour ce flux de données. <br><br> L’activation de cette option permet au flux de données de renvoyer du contenu personnalisé à partir de campagnes entrantes web et basées sur des applications dans [!DNL Adobe Journey Optimizer]. Cette option nécessite [!UICONTROL Segmentation Edge] pour être active. Si [!UICONTROL Segmentation Edge] n’est pas cochée, cette option est grisée. |

### Paramètres d’Adobe Target {#target}

Ce service contrôle si et comment les données sont envoyées à Adobe Target.

![Paramètres de la banque de données Adobe Target.](assets/configure/target-config.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Jeton de propriété] | [!DNL Target] permet aux clients de contrôler les autorisations à l’aide de propriétés. Pour plus d’informations sur les propriétés, consultez le guide sur la [configuration des autorisations d’entreprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=fr) dans la documentation de [!DNL Target].<br><br>Le jeton de propriété se trouve dans l’interface utilisateur d’Adobe Target sous [!UICONTROL Configuration] > [!UICONTROL Propriétés]. |
| [!UICONTROL Identifiant d’environnement Target] | Les [environnements dans Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=fr) vous permettent de gérer la mise en œuvre à toutes les étapes de développement. Ce paramètre spécifie l’environnement que vous allez utiliser avec ce flux de données.<br><br>Une bonne pratique consiste à définir ce paramètre différemment pour chacun des environnements de flux de données `dev`, `stage` et `prod` afin de simplifier le processus. Cependant, si des environnements Adobe Target sont déjà définis, vous pouvez les utiliser. |
| [!UICONTROL Espace de noms d’identifiant tiers de Target] | L’espace de noms d’identité du `mbox3rdPartyId` que vous souhaitez utiliser pour ce flux de données. Si vous utilisez une intégration [!DNL Customer Attributes] avec Adobe Target ou `thirdPartyId` pour mettre à jour ou créer des profils via [l&#39;API de profils Adobe Target](https://experienceleague.adobe.com/en/docs/target-dev/developer/api/profile-apis/profiles-api), vous devez fournir une valeur d&#39;espace de noms de votre choix. Vous devez utiliser cet espace de noms dans la section `IdentityMap` de votre schéma XDM pour envoyer les `customerID` ou `thirdPartyId` utilisés dans les téléchargements de fichiers d’attributs du client ou dans vos appels d’API de mise à jour de profil.  Pour plus d’informations, consultez le guide sur la [mise en œuvre de `mbox3rdPartyId` avec le SDK web](../web-sdk/personalization/adobe-target/using-mbox-3rdpartyid.md). |
| [!UICONTROL Remplacements de jetons de propriété] | Dans cette section, vous pouvez définir des jetons de propriété supplémentaires que vous pouvez utiliser pour remplacer celui par défaut. |

### Paramètres [!UICONTROL Transfert d’événement]

Ce service contrôle si et comment les données sont envoyées au [transfert d’événement](../tags/ui/event-forwarding/overview.md).

![Section Transfert d’événement de l’écran de configuration de la chaîne de données.](assets/configure/event-forwarding-config.png)

| Paramètre | Description |
| --- | --- |
| [!UICONTROL Propriété de Launch] | **(Obligatoire)** La propriété de transfert d’événement à laquelle vous souhaitez envoyer des données. |
| [!UICONTROL Environnement Launch] | **(Obligatoire)** L’environnement au sein de la propriété sélectionnée auquel vous souhaitez envoyer des données. |

>[!NOTE]
>
>Vous pouvez sélectionner **[!UICONTROL Saisie manuelle des identifiants]** pour saisir les noms des propriétés et des environnements au lieu d’utiliser les menus déroulants.

## Copier un flux de données {#copy}

Vous pouvez créer une copie d’un flux de données existant et en modifier les détails si nécessaire.

>[!NOTE]
>
>Les flux de données peuvent uniquement être copiés dans le même [sandbox](../sandboxes/home.md). En d’autres termes, vous ne pouvez pas copier un flux de données d’un sandbox vers un autre.

À partir de la page principale de l’espace de travail [!UICONTROL Flux de données], sélectionnez les points de suspension (**....**) pour le flux de données en question, puis sélectionnez **[!UICONTROL Copier]**.

![Image montrant l’option Copier sélectionnée dans la vue de liste de la chaîne de données.](assets/configure/copy-datastream-list.png)

Vous pouvez également sélectionner **[!UICONTROL Copier le flux de données]** dans la vue des détails d’un flux de données particulier.

![Option de copie sélectionnée dans la vue de détails de la banque de données.](assets/configure/copy-datastream-details.png)

Une boîte de dialogue de confirmation s’affiche, vous invitant à fournir un nom unique pour la création du flux de données, ainsi que des détails sur les options de configuration qui seront copiées. Une fois prêt, sélectionnez **[!UICONTROL Copier]**.

![Boîte de dialogue de confirmation pour la copie d’un flux de données.](assets/configure/copy-datastream-confirm.png)

La page principale de l’espace de travail [!UICONTROL Flux de données] réapparaît avec le nouveau flux de données répertorié.

## Étapes suivantes

Ce guide explique comment gérer les flux de données dans l’interface utilisateur de collecte de données. Pour plus d’informations sur l’installation et la configuration du SDK web après la configuration d’un flux de données, consultez le [Guide E2E de collecte de données](../collection/e2e.md#install).
