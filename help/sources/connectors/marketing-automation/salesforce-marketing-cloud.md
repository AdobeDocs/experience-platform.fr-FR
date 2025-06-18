---
title: Présentation de Salesforce Marketing Cloud Source
description: Découvrez comment connecter Salesforce Marketing Cloud à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-05-17T00:00:00Z
source-git-commit: 0c0a58df4beae499008e52c118b40bed86ff0596
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 8%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>La source [!DNL Salesforce Marketing Cloud] sera abandonnée en janvier 2026. Une nouvelle source sera publiée plus tard cette année comme alternative. Une fois la nouvelle source publiée, vous devez planifier la migration vers la nouvelle source en créant de nouvelles connexions de compte et de nouveaux flux de données avant la fin du mois de janvier 2026.

[!DNL Salesforce Marketing Cloud] vous permet de gérer et d’automatiser l’engagement des clients sur les canaux e-mail, mobiles, les médias sociaux et la publicité, le tout sur une seule plateforme. Grâce à des outils tels qu’Email Studio, Parcours Builder et Audience Builder, vous pouvez créer des campagnes personnalisées et des parcours client adaptés à votre audience.

Vous pouvez utiliser la source de [!DNL Salesforce Marketing Cloud] pour connecter votre compte et importer vos données dans Adobe Experience Platform.

## Conditions préalables

Avant de pouvoir connecter votre source de [!DNL Salesforce Marketing Cloud] à Experience Platform, vous devez vous assurer que les **portées d’autorisation** suivantes sont configurées sur votre combinaison d’identifiant client et de secret client [!DNL Salesforce Marketing Cloud] :

* `campaign_read`
* `list_and_subscribers_read`

Vous pouvez demander des portées en effectuant un appel à la ressource `v2/userinfo` de l’API [!DNL Salesforce Marketing Cloud]. Consultez le document [[!DNL Salesforce Marketing Cloud] Portées des autorisations d’intégration des API](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) pour obtenir des conseils sur la requête et la comparaison des portées.

Pour plus d’informations sur les portées, y compris une liste de leurs autorisations et comportements associés, consultez ce document [[!DNL Salesforce Marketing Cloud] API REST](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>L’ingestion d’objets personnalisés n’est actuellement pas prise en charge par l’intégration source [!DNL Salesforce Marketing Cloud].

### Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform. Placer sur la liste autorisée Pour plus d’informations, consultez le guide sur la [connexion des adresses IP à Experience Platform](../../ip-address-allow-list.md).

>[!WARNING]
>
>Placer sur la liste autorisée Si vous n’ajoutez pas les adresses IP nécessaires à votre, votre compte [!DNL Salesforce Marketing Cloud] ne se connectera pas à Experience Platform.

### S’authentifier auprès d’Experience Platform sur Azure {#azure}

Vous devez fournir des valeurs pour les informations d’identification suivantes afin de [!DNL Salesforce Marketing Cloud] connecter à Experience Platform sur [!DNL Azure].

| Informations d’identification | Description |
| --- | --- |
| Hôte | Serveur hôte de votre application. Il s’agit souvent de votre sous-domaine. **Remarque :** lors de la saisie de votre valeur de `host`, vous devez spécifier la `{subdomain}.rest.marketingcloudapis.com`. Par exemple, si votre URL hôte est `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, vous devez saisir `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` comme valeur d’hôte. |
| Identifiant client | Identifiant client associé à votre application [!DNL Salesforce Marketing Cloud]. |
| Secret client | Secret client associé à votre application [!DNL Salesforce Marketing Cloud]. |
| Identifiant de spécification de connexion | La **spécification de connexion** fournit les propriétés de connecteur d’une source de données. Cela inclut des détails tels que les spécifications d’authentification et les exigences pour la création de connexions **de base** et **source**. Par [!DNL Salesforce Marketing Cloud], l’identifiant de spécification de connexion est : `ea1c2a08-b722-11eb-8529-0242ac130003`. **Remarque :** ces informations d’identification ne sont nécessaires que lors de la connexion via les API. |

### Authentification à Experience Platform sur Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).

Vous devez fournir des valeurs pour les informations d’identification suivantes pour connecter [!DNL Salesforce Marketing Cloud] à Experience Platform sur AWS.

| Informations d’identification | Description |
| --- | --- |
| Sous-domaine | Partie unique de l’URL de votre instance [!DNL Salesforce Marketing Cloud], utilisée pour construire les points d’entrée de l’API. |
| Identifiant client | Identifiant public de votre application, généré lors de la création d’un package installé dans [!DNL Salesforce Marketing Cloud] |
| Secret client | Clé confidentielle associée à votre identifiant client, également générée dans le package installé. |
| Identifiant de spécification de connexion | La **spécification de connexion** fournit les propriétés de connecteur d’une source de données. Cela inclut des détails tels que les spécifications d’authentification et les exigences pour la création de connexions **de base** et **source**. Par [!DNL Salesforce Marketing Cloud], l’identifiant de spécification de connexion est : `ea1c2a08-b722-11eb-8529-0242ac130003`. **Remarque :** ces informations d’identification ne sont nécessaires que lors de la connexion via les API. |

Pour plus d’informations, consultez la [[!DNL Salesforce] documentation sur le jeton d’accès pour les intégrations serveur à serveur](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html).

## Connexion de [!DNL Salesforce Marketing Cloud] à Experience Platform à l’aide d’API

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Salesforce Marketing Cloud] à Experience Platform à l’aide d’API :

* [Connexion  [!DNL Salesforce Marketing Cloud]  Experience Platform à l’aide de l’API Flow Service](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
* [Créer un flux de données pour une source d’automatisation du marketing à l’aide de l’API Flow Service](../../tutorials/api/collect/marketing-automation.md)

## Connexion d’[!DNL Salesforce Marketing Cloud] à Experience Platform à l’aide de l’interface utilisateur

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Salesforce Marketing Cloud] à Experience Platform à l’aide de l’interface utilisateur :

* [Connexion  [!DNL Salesforce Marketing Cloud]  Experience Platform dans l’interface utilisateur](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Créer un flux de données pour une connexion à une source d’automatisation du marketing dans l’interface utilisateur](../../tutorials/ui/dataflow/marketing-automation.md)
