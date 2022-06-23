---
description: Utilisez les configurations d’authentification prises en charge dans Adobe Experience Platform Destination SDK pour authentifier les utilisateurs et activer les données vers votre point d’entrée de destination.
title: Configuration de l’authentification
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 631c0ac02cb7f4f95500897ca224aa532393c109
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 97%

---

# Configuration de l’authentification {#credentials}

## Types d’authentification pris en charge {#supported-authentication-types}

La configuration d’authentification que vous sélectionnez détermine la manière dont Experience Platform s’authentifie auprès de votre destination, et ce dans l’interface utilisateur de Platform.

Adobe Experience Platform Destination SDK prend en charge plusieurs types d’authentification :

* [Authentification du porteur](#bearer)
* [(Version bêta) Authentification Amazon S3](#s3)
* [(Version bêta) Stockage Azure Blob](#blob)
* [(Version bêta) Stockage du lac de données Azure](#adls)
* [(Version bêta) Stockage dans le cloud Google](#gcs)
* [SFTP avec clé SSH (version Beta)](#sftp-ssh)
* [SFTP avec mot de passe (version Beta)](#sftp-password)
* [OAuth 2 avec code d’autorisation](#oauth2)
* [OAUth 2 avec octroi de mot de passe](#oauth2)
* [OAuth 2 avec octroi dʼinformations d’identification du client](#oauth2)

Vous pouvez configurer les informations d’authentification pour votre destination via les paramètres `customerAuthenticationConfigurations` du point d’entrée `/destinations`.

Pour plus d’informations sur la configuration de l’authentification pour chaque type de destination, consultez les sections suivantes :

* [Configurations d’authentification pour les destinations de diffusion en continu](destination-configuration.md#customer-authentication-configurations)
* [Configurations dʼauthentification pour les destinations basées sur des fichiers](file-based-destination-configuration.md#customer-authentication-configurations)

## Authentification du porteur {#bearer}

L’authentification du porteur est prise en charge pour les destinations de diffusion en continu dans Experience Platform.

Pour configurer l’authentification de type porteur pour votre destination, configurez le paramètre `customerAuthenticationConfigurations` dans le point d’entrée `/destinations` comme indiqué ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## (Version bêta) Authentification [!DNL Amazon S3] {#s3}

L’authentification [!DNL Amazon S3] est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

>[!IMPORTANT]
>
>La prise en charge des destinations basées sur des fichiers dans Adobe Experience Platform Destination SDK est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Pour configurer l’authentification Amazon S3 pour votre destination, configurez le paramètre `customerAuthenticationConfigurations` du point d’entrée `/destinations` comme illustré ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## (version bêta) [!DNL Azure Blob Storage] {#blob}

L’authentification [!DNL Azure Blob Storage] est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

>[!IMPORTANT]
>
>La prise en charge des destinations basées sur des fichiers dans Adobe Experience Platform Destination SDK est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Pour configurer l’authentification [!DNL Azure Blob] pour votre destination, configurez le paramètre `customerAuthenticationConfigurations` du point d’entrée `/destinations` comme illustré ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## (version bêta) [!DNL Azure Data Lake Storage] {#adls}

L’authentification [!DNL Azure Data Lake Storage] est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

>[!IMPORTANT]
>
>La prise en charge des destinations basées sur des fichiers dans Adobe Experience Platform Destination SDK est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Pour configurer l’authentification [!DNL Azure Data Lake Storage] (ADLS) de votre destination, configurez le paramètre `customerAuthenticationConfigurations` du point d’entrée `/destinations` comme illustré ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## (version bêta) [!DNL Google Cloud Storage] {#gcs}

L’authentification [!DNL Google Cloud Storage] est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

>[!IMPORTANT]
>
>La prise en charge des destinations basées sur des fichiers dans Adobe Experience Platform Destination SDK est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```


## (Version bêta) Authentification [!DNL SFTP] avec clé [!DNL SSH] {#sftp-ssh}

L’authentification [!DNL SFTP] avec la clé [!DNL SSH] est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

>[!IMPORTANT]
>
>La prise en charge des destinations basées sur des fichiers dans Adobe Experience Platform Destination SDK est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Pour configurer l’authentification SFTP avec la clé SSH pour votre destination, configurez le paramètre `customerAuthenticationConfigurations` du point d’entrée `/destinations` comme illustré ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## (Version bêta) Authentification [!DNL SFTP] avec mot de passe {#sftp-password}

L’authentification [!DNL SFTP] avec mot de passe est prise en charge pour les destinations basées sur des fichiers dans Experience Platform.

>[!IMPORTANT]
>
>La prise en charge des destinations basées sur des fichiers dans Adobe Experience Platform Destination SDK est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Pour configurer l’authentification SFTP avec le mot de passe de votre destination, configurez le paramètre `customerAuthenticationConfigurations` du point d’entrée `/destinations` comme illustré ci-dessous :

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## Authentification [!DNL OAuth 2] {#oauth2}

L’authentification [!DNL OAuth 2] est prise en charge pour les destinations de diffusion en continu dans Experience Platform.

Pour plus d’informations sur la configuration des différents flux OAuth 2 pris en charge, ainsi que sur la prise en charge personnalisée d’OAuth 2, consultez la documentation de Destination SDK sur l’[Authentification OAuth 2](./oauth2-authentication.md).


## Quand utiliser le point d’entrée de l’API `/credentials` ? {#when-to-use}

>[!IMPORTANT]
>
>Dans la plupart des cas, vous *ne devez pas* utiliser le point d’entrée de l’API `/credentials`. Au lieu de cela, vous pouvez configurer les informations d’authentification pour votre destination via les paramètres `customerAuthenticationConfigurations` du point d’entrée `/destinations`.

Le point d’entrée de l’API `/credentials` est fourni aux développeurs de destination pour les cas où il existe un système d’authentification global entre Adobe et votre destination et les clients [!DNL Platform] n’ont pas besoin de fournir d’informations d’authentification pour se connecter à votre destination.

Dans ce cas, vous devez créer un objet d’identification à l’aide du point d’entrée de l’API `/credentials`. Vous devez également sélectionner `PLATFORM_AUTHENTICATION` dans la [configuration de destination](./destination-configuration.md#destination-delivery). Lisez [Opérations du point d’entrée de l’API Credentials](./credentials-configuration-api.md) pour obtenir la liste complète des opérations que vous pouvez effectuer sur le point d’entrée `/credentials`.
