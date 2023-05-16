---
description: Découvrez comment configurer un mécanisme d’authentification pour votre destination et déterminer ce que les utilisateurs verront dans l’interface utilisateur en fonction de la méthode d’authentification que vous sélectionnez.
title: Configuration de l’authentification du client
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 35%

---


# Configuration de l’authentification du client

Experience Platform offre une grande flexibilité dans les protocoles d’authentification disponibles pour les partenaires et les clients. Vous pouvez configurer votre destination pour qu’elle prenne en charge l’une des méthodes d’authentification standard du secteur, telles que [!DNL OAuth2], authentification par jeton porteur, authentification par mot de passe, etc.

Cette page explique comment configurer votre destination à l’aide de votre méthode d’authentification préférée. En fonction de la configuration d’authentification que vous utilisez lors de la création de votre destination, les clients voient différents types de pages d’authentification lors de la connexion à la destination dans l’interface utilisateur de l’Experience Platform.

Pour comprendre où ce composant entre dans une intégration créée avec Destination SDK, reportez-vous au diagramme de la section [options de configuration](../configuration-options.md) ou consultez les pages de présentation de la configuration de destination suivantes :

* [Utiliser Destination SDK pour configurer une destination de diffusion en continu](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Utiliser Destination SDK pour configurer une destination basée sur des fichiers](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Avant que les clients puissent exporter des données de Platform vers votre destination, ils doivent créer une nouvelle connexion entre l’Experience Platform et votre destination, en suivant les étapes décrites dans la section [connexion à la destination](../../../ui/connect-destination.md) tutoriel .

When [création d’une destination](../../authoring-api/destination-configuration/create-destination-configuration.md) par Destination SDK, la variable `customerAuthenticationConfigurations` définit ce que voient les clients dans la section [écran d&#39;authentification](../../../ui/connect-destination.md#authenticate). Selon le type d’authentification de destination, les clients doivent fournir divers détails d’authentification, tels que :

* Pour les destinations qui utilisent [authentification de base](#basic), les utilisateurs doivent fournir un nom d’utilisateur et un mot de passe directement dans la page d’authentification de l’interface utilisateur Experience Platform.
* Pour les destinations qui utilisent [authentification du porteur](#bearer), les utilisateurs doivent fournir un jeton porteur.
* Pour les destinations qui utilisent [Authentification OAuth2](#oauth2), les utilisateurs sont redirigés vers la page de connexion de votre destination, où ils peuvent se connecter à l’aide de leurs informations d’identification.
* Pour [Amazon S3](#s3) destinations, les utilisateurs doivent fournir leurs [!DNL Amazon S3] clé d’accès et clé secrète.
* Pour [Azure Blob](#blob) destinations, les utilisateurs doivent fournir leurs [!DNL Azure Blob] Chaîne de connexion.

Vous pouvez configurer les détails de l’authentification du client via le `/authoring/destinations` point de terminaison . Consultez les pages de référence d’API suivantes pour obtenir des exemples d’appels d’API détaillés dans lesquels vous pouvez configurer les composants affichés dans cette page.

* [Création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Mise à jour d’une configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md)

Cet article décrit toutes les configurations d’authentification du client prises en charge que vous pouvez utiliser pour votre destination et indique ce que les clients verront dans l’interface utilisateur de l’Experience Platform en fonction de la méthode d’authentification que vous avez configurée pour votre destination.

>[!IMPORTANT]
>
>La configuration de l’authentification du client n’exige pas que vous configuriez des paramètres. Vous pouvez copier et coller les fragments de code affichés sur cette page dans vos appels API lors de la [création](../../authoring-api/destination-configuration/create-destination-configuration.md) ou [mise à jour](../../authoring-api/destination-configuration/update-destination-configuration.md) une configuration de destination, et vos utilisateurs verront l’écran d’authentification correspondant dans l’interface utilisateur de Platform.

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Reportez-vous au tableau ci-dessous pour plus d’informations sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (diffusion en continu) | Oui |
| Intégrations basées sur des fichiers (par lots) | Oui |

## Configuration des règles d’authentification {#authentication-rule}

Lors de l’utilisation de l’une des configurations d’authentification du client décrites dans cette page, définissez toujours la variable `authenticationRule` du paramètre [diffusion de destination](destination-delivery.md) to `"CUSTOMER_AUTHENTICATION"`, comme illustré ci-dessous.

```json {line-numbers="true" highlight="4"
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

## Authentification de base {#basic}

L’authentification de base est prise en charge pour les intégrations en temps réel (flux) dans Experience Platform.

Lorsque vous configurez le type d’authentification de base, les utilisateurs doivent saisir un nom d’utilisateur et un mot de passe pour se connecter à votre destination.

![Rendu de l’interface utilisateur avec authentification de base](../../assets/functionality/destination-configuration/basic-authentication-ui.png)

Pour configurer l’authentification de base pour votre destination, configurez la variable `customerAuthenticationConfigurations` via la section `/destinations` point de terminaison comme illustré ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## Authentification du porteur {#bearer}

Lorsque vous configurez le type d’authentification du porteur, les utilisateurs doivent saisir le jeton du porteur qu’ils obtiennent de votre destination.

![Rendu de l’interface utilisateur avec authentification du porteur](../../assets/functionality/destination-configuration/bearer-authentication-ui.png)

Pour configurer l’authentification par type de porteur pour votre destination, configurez la variable `customerAuthenticationConfigurations` via la section `/destinations` point de terminaison comme illustré ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## Authentification OAuth 2 {#oauth2}

Les utilisateurs sélectionnent **[!UICONTROL Se connecter à la destination]** pour déclencher le flux d’authentification OAuth 2 vers votre destination, comme illustré dans l’exemple ci-dessous pour la destination Audiences personnalisées de Twitter. Pour plus d’informations sur la configuration de l’authentification OAuth 2 à votre point d’entrée de destination, consultez la page [Authentification OAuth 2 de Destination SDK](oauth2-authentication.md).

![Rendu de l’interface utilisateur avec authentification OAuth 2](../../assets/functionality/destination-configuration/oauth2-authentication-ui.png)

Pour configurer [!DNL OAuth2] l’authentification pour votre destination, configurez la variable `customerAuthenticationConfigurations` via la section `/destinations` point de terminaison comme illustré ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"OAUTH2"
   }
]
```

## Authentification Amazon S3 {#s3}

L’authentification [!DNL Amazon S3] est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

Lorsque vous configurez le type d’authentification Amazon S3, les utilisateurs doivent saisir leurs informations d’identification S3.

![Rendu de l’interface utilisateur avec authentification S3](../../assets/functionality/destination-configuration/s3-authentication-ui.png)

Pour configurer [!DNL Amazon S3] l’authentification pour votre destination, configurez la variable `customerAuthenticationConfigurations` via la section `/destinations` point de terminaison comme illustré ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## Authentification Azure Blob  {#blob}

L’authentification [!DNL Azure Blob Storage] est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

Lorsque vous configurez le type d’authentification Azure Blob, les utilisateurs doivent saisir la chaîne de connexion.

![Rendu de l’interface utilisateur avec authentification Blob](../../assets/functionality/destination-configuration/blob-authentication-ui.png)

Pour configurer l’authentification [!DNL Azure Blob] pour votre destination, configurez le paramètre `customerAuthenticationConfigurations` du point d’entrée `/destinations` comme illustré ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## Authentification [!DNL Azure Data Lake Storage] {#adls}

L’authentification [!DNL Azure Data Lake Storage] est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

Lorsque vous configurez la variable [!DNL Azure Data Lake Storage] type d’authentification, les utilisateurs doivent saisir les informations d’identification de l’entité de sécurité Azure Service et leurs informations de client.

![[!DNL Azure Data Lake Storage]Rendu de l’interface utilisateur avec authentification ](../../assets/functionality/destination-configuration/adls-authentication-ui.png)

Pour configurer l’authentification [!DNL Azure Data Lake Storage] (ADLS) de votre destination, configurez le paramètre `customerAuthenticationConfigurations` du point d’entrée `/destinations` comme illustré ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## SFTP avec authentification par mot de passe

L’authentification [!DNL SFTP] avec mot de passe est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

Lorsque vous configurez le SFTP avec le type d’authentification par mot de passe, les utilisateurs doivent saisir le nom d’utilisateur et le mot de passe SFTP, ainsi que le domaine et le port SFTP (le port par défaut est 22).

![Rendu de l’interface utilisateur avec authentification par mot de passe](../../assets/functionality/destination-configuration/sftp-password-authentication-ui.png)

Pour configurer l’authentification SFTP avec le mot de passe de votre destination, configurez le paramètre `customerAuthenticationConfigurations` du point d’entrée `/destinations` comme illustré ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## SFTP avec authentification par clé SSH

L’authentification [!DNL SFTP] avec la clé [!DNL SSH] est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

Lorsque vous configurez le SFTP avec le type d’authentification par clé SSH, les utilisateurs doivent saisir le nom d’utilisateur SFTP et la clé SSH, ainsi que le domaine et le port SFTP (le port par défaut est 22).

![Rendu de l’interface utilisateur avec SFTP avec authentification par clé SSH](../../assets/functionality/destination-configuration/sftp-key-authentication-ui.png)

Pour configurer l’authentification SFTP avec la clé SSH pour votre destination, configurez le paramètre `customerAuthenticationConfigurations` du point d’entrée `/destinations` comme illustré ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## Authentification [!DNL Google Cloud Storage] {#gcs}

L’authentification [!DNL Google Cloud Storage] est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

Lorsque vous configurez la variable [!DNL Google Cloud Storage] type d’authentification, les utilisateurs doivent saisir leur [!DNL Google Cloud Storage] [!UICONTROL ID de clé d’accès] et [!UICONTROL clé d&#39;accès secrète].

![Rendu de l’interface utilisateur avec l’authentification Google Cloud Storage](../../assets/functionality/destination-configuration/google-cloud-storage-ui.png)

Pour configurer l’authentification [!DNL Google Cloud Storage] pour votre destination, configurez le paramètre `customerAuthenticationConfigurations` du point d’entrée `/destinations` comme illustré ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```

## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devriez mieux comprendre comment configurer l’authentification des utilisateurs sur votre plateforme de destination.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Authentification OAuth 2](oauth2-authentication.md)
* [Champs de données client](customer-data-fields.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Diffusion de destination](destination-delivery.md)
* [Configuration des métadonnées d’audience](audience-metadata-configuration.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Configuration par lots](batch-configuration.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)