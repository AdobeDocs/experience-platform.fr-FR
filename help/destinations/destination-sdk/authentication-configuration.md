---
description: Utilisez les configurations d’authentification prises en charge dans le SDK Adobe Experience Platform Destination pour authentifier les utilisateurs et activer les données vers votre point de terminaison de destination.
title: Configuration de l’authentification
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: e6d922800c17312df8529061c56d8a2deac46662
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Configuration de l’authentification {#credentials}

## Types d’authentification pris en charge {#supported-authentication-types}

Le SDK Adobe Experience Platform Destination prend en charge plusieurs types d’authentification :

* Authentification du porteur
* OAuth 2 avec code d’autorisation
* OAUth 2 avec l&#39;octroi du mot de passe
* OAuth 2 avec octroi des informations d’identification client

Vous pouvez configurer les informations d’authentification pour votre destination via le `customerAuthenticationConfigurations` des paramètres `/destinations` point de terminaison . Reportez-vous à la section [section sur les configurations d’authentification du client](./destination-configuration.md#customer-authentication-configurations) dans l’article sur la configuration des destinations et dans les sections ci-dessous pour plus de détails sur les configurations de chaque type d’authentification.

## Authentification du porteur {#bearer}

Pour configurer l’authentification par type de porteur pour vos destinations, vous devez simplement configurer la variable `customerAuthenticationConfigurations` du paramètre `/destinations` point de terminaison comme illustré ci-dessous :

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## Authentification OAuth 2 {#oauth2}

Pour plus d’informations sur la configuration des différents flux OAuth 2 pris en charge, ainsi que sur la prise en charge personnalisée d’OAuth 2, consultez la documentation du SDK de destination sur [Authentification OAuth 2](./oauth2-authentication.md).


## Quand utiliser la variable `/credentials` Point d’entrée API {#when-to-use}

>[!IMPORTANT]
>
>Dans la plupart des cas, vous *ne pas* Vous devez utiliser la variable `/credentials` Point d’entrée de l’API. Au lieu de cela, vous pouvez configurer les informations d’authentification pour votre destination via le `customerAuthenticationConfigurations` des paramètres `/destinations` point de terminaison .

Le `/credentials` Le point de terminaison de l’API est fourni aux développeurs de destination pour les cas où il existe un système d’authentification global entre l’Adobe et votre destination et [!DNL Platform] Les clients n’ont pas besoin de fournir d’informations d’authentification pour se connecter à votre destination.

Dans ce cas, vous devez créer un objet d’identification à l’aide de la fonction `/credentials` Point d’entrée de l’API. Vous devez également sélectionner `PLATFORM_AUTHENTICATION` dans le [configuration de destination](./destination-configuration.md#destination-delivery). Lecture [Opérations du point d’entrée de l’API d’identification](./credentials-configuration-api.md) pour obtenir la liste complète des opérations que vous pouvez effectuer sur la variable `/credentials` point de terminaison .
