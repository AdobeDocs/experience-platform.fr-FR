---
description: Utilisez les configurations d’authentification prises en charge en Adobe Experience Platform Destination SDK pour authentifier les utilisateurs et activer les données vers votre point de terminaison de destination.
title: Configuration de l’authentification
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 92bca3600d854540fd2badd925e453fba41601a7
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 7%

---

# Configuration de l’authentification {#credentials}

## Types d’authentification pris en charge {#supported-authentication-types}

La configuration d’authentification que vous sélectionnez détermine la manière dont l’Experience Platform s’authentifie à votre destination, dans l’interface utilisateur de Platform.

L’Adobe Experience Platform Destination SDK prend en charge plusieurs types d’authentification :

* Authentification du porteur
* (Version bêta) Authentification Amazon S3
* (Version bêta) Chaîne de connexion Azure
* (Version bêta) Entité principale du service Azure
* (Version bêta) SFTP avec clé SSH
* (Version bêta) SFTP avec mot de passe
* OAuth 2 avec code d’autorisation
* OAUth 2 avec l&#39;octroi du mot de passe
* OAuth 2 avec octroi des informations d’identification client

Vous pouvez configurer les informations d’authentification pour votre destination via le `customerAuthenticationConfigurations` des paramètres `/destinations` point de terminaison .

Pour plus d’informations sur la configuration de l’authentification pour chaque type de destination, reportez-vous aux sections suivantes :

* [Configurations d’authentification pour les destinations de diffusion en continu](destination-configuration.md#customer-authentication-configurations)
* [Configurations de l’authentification pour les destinations basées sur des fichiers](file-based-destination-configuration.md#customer-authentication-configurations)

## Authentification du porteur {#bearer}

L’authentification du porteur est prise en charge pour les destinations de diffusion en continu dans Experience Platform.

Pour configurer l’authentification par type de porteur pour votre destination, configurez la variable `customerAuthenticationConfigurations` du paramètre `/destinations` point de terminaison comme illustré ci-dessous :

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## (Version bêta) [!DNL Amazon S3] authentication {#s3}

[!DNL Amazon S3] l’authentification est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

>[!IMPORTANT]
>
>La prise en charge des destinations basées sur des fichiers en Adobe Experience Platform Destination SDK est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Pour configurer l’authentification Amazon S3 pour votre destination, configurez la variable `customerAuthenticationConfigurations` du paramètre `/destinations` point de terminaison comme illustré ci-dessous :

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ]
```

## (version bêta) [!DNL Azure Blob Storage] {#blob}

[!DNL Azure Blob Storage] l’authentification est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

>[!IMPORTANT]
>
>La prise en charge des destinations basées sur des fichiers en Adobe Experience Platform Destination SDK est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Pour configurer [!DNL Azure Blob] l’authentification pour votre destination, configurez la variable `customerAuthenticationConfigurations` du paramètre `/destinations` point de terminaison comme illustré ci-dessous :

```json
   "customerAuthenticationConfigurations":[
     {
        "authType":"AZURE_CONNECTION_STRING"
     }
  ]
```

## (version bêta) [!DNL Azure Data Lake Storage] {#adls}

[!DNL Azure Data Lake Storage] l’authentification est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

>[!IMPORTANT]
>
>La prise en charge des destinations basées sur des fichiers en Adobe Experience Platform Destination SDK est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Pour configurer [!DNL Azure Data Lake Storage] (ADLS) pour l’authentification de votre destination, configurez la variable `customerAuthenticationConfigurations` du paramètre `/destinations` point de terminaison comme illustré ci-dessous :

```json
   "customerAuthenticationConfigurations":[
     {
        "authType":"AZURE_SERVICE_PRINCIPAL"
     }
  ]
```

## (Version bêta) [!DNL SFTP] authentification avec [!DNL SSH] key {#sftp-ssh}

[!DNL SFTP] authentification avec [!DNL SSH] est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

>[!IMPORTANT]
>
>La prise en charge des destinations basées sur des fichiers en Adobe Experience Platform Destination SDK est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Pour configurer l’authentification SFTP avec la clé SSH pour votre destination, configurez la variable `customerAuthenticationConfigurations` du paramètre `/destinations` point de terminaison comme illustré ci-dessous :

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_SSH_KEY"
      }
   ]
```

## (Version bêta) [!DNL SFTP] authentification avec mot de passe {#sftp-password}

[!DNL SFTP] l’authentification avec mot de passe est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

>[!IMPORTANT]
>
>La prise en charge des destinations basées sur des fichiers en Adobe Experience Platform Destination SDK est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Pour configurer l’authentification SFTP avec le mot de passe de votre destination, configurez la variable `customerAuthenticationConfigurations` du paramètre `/destinations` point de terminaison comme illustré ci-dessous :

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_PASSWORD"
      }
   ]
```

## [!DNL OAuth 2] authentication {#oauth2}

[!DNL OAuth 2] l’authentification est prise en charge pour les destinations de diffusion en continu dans Experience Platform.

Pour plus d’informations sur la configuration des différents flux OAuth 2 pris en charge, ainsi que sur la prise en charge personnalisée d’OAuth 2, consultez la documentation de Destination SDK sur [Authentification OAuth 2](./oauth2-authentication.md).


## Quand utiliser la variable `/credentials` Point d’entrée API {#when-to-use}

>[!IMPORTANT]
>
>Dans la plupart des cas, vous *ne pas* Vous devez utiliser la variable `/credentials` Point d’entrée de l’API. Au lieu de cela, vous pouvez configurer les informations d’authentification pour votre destination via le `customerAuthenticationConfigurations` des paramètres `/destinations` point de terminaison .

Le `/credentials` Le point de terminaison de l’API est fourni aux développeurs de destination pour les cas où il existe un système d’authentification global entre l’Adobe et votre destination et [!DNL Platform] Les clients n’ont pas besoin de fournir d’informations d’authentification pour se connecter à votre destination.

Dans ce cas, vous devez créer un objet d’identification à l’aide de la fonction `/credentials` Point d’entrée de l’API. Vous devez également sélectionner `PLATFORM_AUTHENTICATION` dans le [configuration de destination](./destination-configuration.md#destination-delivery). Lecture [Opérations du point d’entrée de l’API d’identification](./credentials-configuration-api.md) pour obtenir la liste complète des opérations que vous pouvez effectuer sur la variable `/credentials` point de terminaison .
