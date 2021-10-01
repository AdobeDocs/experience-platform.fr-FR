---
description: Cette configuration détermine la manière dont les utilisateurs de Adobe Experience Platform s’authentifient auprès de votre point de terminaison de destination pour activer les données.
title: Options de configuration des informations d’identification dans le SDK de destination
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 6ff5fd0e80f7ca1015969e91cc23c88251509b61
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 0%

---

# Configuration de l’authentification {#credentials}

## Types d’authentification pris en charge {#supported-authentication-types}

Adobe Experience Platform prend en charge plusieurs types d’authentification :

* Authentification du porteur
* OAuth 2 avec code d’autorisation
* OAUth 2 avec l&#39;octroi du mot de passe
* OAuth 2 avec octroi des informations d’identification client

Pour les différents flux OAuth 2 pris en charge, ainsi que pour la prise en charge personnalisée d’OAuth 2, consultez la documentation du SDK de destination sur [l’authentification OAuth 2](./oauth2-authentication.md).

Vous pouvez configurer les informations d’authentification pour votre destination via les paramètres `customerAuthenticationConfigurations` du point de terminaison `/destinations`. Reportez-vous à la [section Configurations de l’authentification du client](./destination-configuration.md#customer-authentication-configurations) dans l’article Configuration de la destination .

## Quand utiliser le point d’entrée de l’API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Dans la plupart des cas, vous *ne devez pas* utiliser le point d’entrée de l’API `/credentials`. Vous pouvez plutôt configurer les informations d’authentification pour votre destination via les paramètres `customerAuthenticationConfigurations` du point de terminaison `/destinations`.

Utilisez le point d’entrée de l’API `activation/authoring/credentials` et sélectionnez `PLATFORM_AUTHENTICATION` dans la [configuration de destination](./destination-configuration.md#destination-delivery) s’il existe un système d’authentification global entre l’Adobe et votre destination, et que le client [!DNL Platform] n’a pas besoin de fournir d’informations d’identification d’authentification pour se connecter à votre destination. Dans ce cas, vous devez créer un objet d’identification à l’aide du point de terminaison de l’API `/credentials`. Lisez [Opérations de point d’entrée de l’API d’identification](./credentials-configuration-api.md) pour obtenir la liste complète des opérations que vous pouvez effectuer sur le point d’entrée `/credentials`.
