---
description: Découvrez comment configurer les attributs de l’interface utilisateur, tels que le lien de documentation, la catégorie de carte de destination, ainsi que le type et la fréquence de connexion à la destination, pour les destinations créées avec Destination SDK.
title: Attributs de l’interface utilisateur
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 9%

---


# Attributs de l’interface utilisateur

Les attributs de l’interface utilisateur définissent les éléments visuels que l’Adobe doit afficher pour votre carte de destination dans l’interface utilisateur de Adobe Experience Platform, tels que le logo de la plateforme de destination, un lien vers la page de documentation, une description de destination et sa catégorie et son type.

Pour comprendre où ce composant entre dans une intégration créée avec Destination SDK, reportez-vous au diagramme de la section [options de configuration](../configuration-options.md) ou consultez les pages de présentation de la configuration de destination suivantes :

* [Utiliser Destination SDK pour configurer une destination de diffusion en continu](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Utiliser Destination SDK pour configurer une destination basée sur des fichiers](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

When [création d’une destination](../../authoring-api/destination-configuration/create-destination-configuration.md) par Destination SDK, la variable `uiAttributes` définit les propriétés visuelles suivantes de votre carte de destination :

* L’URL de votre page de documentation de destination dans la variable [catalogue de destination](../../../catalog/overview.md).
* URL dans laquelle vous avez hébergé l’icône à afficher dans la carte du catalogue des destinations.
* La catégorie sous laquelle votre destination sera visible dans l’interface utilisateur de Platform.
* Fréquence d’exportation des données pour votre destination.
* Type de connexion de destination, tel qu’Amazon S3, Azure Blob, etc.

Vous pouvez configurer les attributs de l’interface utilisateur à l’aide de l’option `/authoring/destinations` point de terminaison . Consultez les pages de référence d’API suivantes pour obtenir des exemples d’appels d’API détaillés dans lesquels vous pouvez configurer les composants affichés dans cette page.

* [Création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Mise à jour d’une configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md)

Cet article décrit tous les attributs d’interface utilisateur pris en charge que vous pouvez utiliser pour votre destination et indique ce que les clients verront dans l’interface utilisateur de l’Experience Platform.

![Copie d’écran de l’interface utilisateur présentant les attributs de l’interface utilisateur dans l’interface Experience Platform](../../assets/functionality/destination-configuration/ui-attributes.png)

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Reportez-vous au tableau ci-dessous pour plus d’informations sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (diffusion en continu) | Oui |
| Intégrations basées sur des fichiers (par lots) | Oui |

## Paramètres pris en charge {#supported-parameters}

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"cloudStorage",
      "connectionType":"S3",
      "frequency":"batch",
      "isBeta":"true"
   }
```

### `documentationLink` {#documentation-link}

`documentationLink` est un paramètre de chaîne qui fait référence à la page de documentation dans la variable [Catalogue des destinations](../../../catalog/overview.md) pour votre destination. Chaque destination productisée dans Adobe Experience Platform doit avoir une page de documentation correspondante. [Découvrez comment créer une page de documentation de destination](../../docs-framework/documentation-instructions.md) pour votre destination. Notez que cela n’est pas nécessaire pour les destinations privées/personnalisées.

Utilisez le format suivant : `http://www.adobe.com/go/destinations-YOURDESTINATION-en`où `YOURDESTINATION` est le nom de votre destination. Par exemple, pour une destination appelée Moviestar, procédez comme suit : `http://www.adobe.com/go/destinations-moviestar-en`.

Les utilisateurs peuvent afficher et consulter votre lien vers votre documentation à partir de la page de catalogue des destinations de l’interface utilisateur. Ils doivent accéder à votre carte de destination, puis sélectionner **[!UICONTROL Autres actions]**, puis **[!UICONTROL Afficher la documentation]**, comme illustré dans l’image ci-dessous.

![Image de l’interface utilisateur indiquant l’emplacement du lien vers la documentation.](../../assets/functionality/destination-configuration/ui-attributes-doc-link.png)

>[!NOTE]
>
>Ce lien ne fonctionne qu’après que Adobe a défini votre destination et que la documentation a été publiée.

### `category` {#category}

`category` est un paramètre de chaîne qui fait référence à la catégorie affectée à votre destination dans Adobe Experience Platform. Pour plus d’informations, consultez la section [Catégories de destinations](../../../destination-types.md). Utilisez l’une des valeurs suivantes :`adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`.

Les utilisateurs peuvent voir la liste des catégories de destination sur le côté gauche de l’écran dans le catalogue des destinations, comme illustré dans l’image ci-dessous.

![Image de l’interface utilisateur indiquant l’emplacement de la catégorie de destination.](../../assets/functionality/destination-configuration/ui-attributes-category.png)

<!-- ### `iconUrl` {#icon-url}

`iconUrl` is a string parameter that refers to the URL where you hosted the icon to be displayed in the destinations catalog card. For private custom integrations, this is not required. For productized configurations, you need to share an icon with the Adobe team when you [submit the destination for review](../../guides/submit-destination.md#logo).

Users can see the icon on your destination card, as shown in the image below.

![UI image showing the icon location.](../../assets/functionality/destination-configuration/ui-attributes-icon.png) -->

### `connectionType` {#connection-type}

`connectionType` est un paramètre de chaîne qui fait référence au type de connexion, selon la destination. Valeurs prises en charge : <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul>

Les utilisateurs peuvent voir le type de connexion de destination dans la variable [Parcourir](../../../ui/destinations-workspace.md#browse) de l’espace de travail des destinations.

![Image de l’interface utilisateur indiquant l’emplacement du type de connexion dans l’interface utilisateur.](../../assets/functionality/destination-configuration/ui-attributes-connection.png)

### `frequency` {#frequency}

`frequency` est un paramètre de chaîne qui fait référence au type d’exportation de données pris en charge par votre destination. Définissez sur . `Streaming` pour les intégrations basées sur des API, ou `Batch` lorsque vous exportez des fichiers vers vos destinations.

Les utilisateurs peuvent voir le type de fréquence dans la variable **[!UICONTROL Exécutions de flux de données]** de chaque connexion à la destination.

![Image de l’interface utilisateur montrant l’emplacement du type de fréquence dans l’interface utilisateur.](../../assets/functionality/destination-configuration/ui-attributes-frequency.png)

### `isBeta` {#isbeta}

Si la destination que vous créez avec Destination SDK est disponible pour un nombre limité de clients, vous pouvez marquer la carte de destination du catalogue de destination comme étant en version bêta.

Pour ce faire, vous pouvez utiliser la variable `isBeta: "true"` dans la section Attributs de l’interface utilisateur de la configuration de destination afin de marquer la carte de destination de manière appropriée.

![Image de l’interface utilisateur montrant une carte de destination marquée comme bêta.](../../assets/functionality/destination-configuration/ui-attributes-isbeta.png)

## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devriez mieux comprendre les attributs d’interface utilisateur que vous pouvez configurer pour votre destination et où les utilisateurs les verront dans l’interface utilisateur de Platform.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Authentification du client](customer-authentication.md)
* [Authentification OAuth 2](oauth2-authentication.md)
* [Champs de données client](customer-data-fields.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Diffusion de destination](destination-delivery.md)
* [Configuration des métadonnées d’audience](audience-metadata-configuration.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Configuration par lots](batch-configuration.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)