---
title: Présentation Du Connecteur Source Salesforce Service Cloud
description: Découvrez comment connecter Salesforce Service Cloud à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: 9bebbc00-55b3-4aec-9357-4127c05844e2
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 10%

---

# [!DNL Salesforce Service Cloud]

[!DNL Salesforce Service Cloud] est une plateforme de succès client conçue pour automatiser les workflows de service et rationaliser la communication entre les entreprises et leurs clients. Il regroupe les demandes provenant de divers canaux (tels que les e-mails, le téléphone, les médias sociaux et le chat en direct) dans une console d’agent unifiée. Cela permet aux équipes d’assistance de gérer les « cas » avec une vue à 360 degrés de l’historique du client, en veillant à ce que les réponses soient personnalisées et efficaces, quelle que soit la manière dont le client les contacte.

Vous pouvez utiliser le connecteur source [!DNL Salesforce Service Cloud] dans Sources Adobe Experience Platform pour connecter votre compte [!DNL Salesforce Service Cloud] et importer vos données pour les utiliser dans les services Experience Platform.

Lisez ce document pour découvrir comment configurer votre compte [!DNL Salesforce Service Cloud] et le connecter à Experience Platform.

## Conditions préalables {#prerequisites}

Lisez cette section pour connaître les conditions préalables à la configuration que vous devez remplir avant de pouvoir vous connecter à Experience Platform.

### Liste autorisée d’adresses IP {#allowlist}

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform. Pour plus d’informations, consultez le guide sur la [connexion des adresses IP à &#x200B;](../../ip-address-allow-list.md).

### Collecter les informations d’identification requises {#credentials}

Vous devez fournir des valeurs pour les informations d’identification suivantes afin de connecter votre compte [!DNL Salesforce Service Cloud] à l’aide des informations d’identification du client OAuth2.

| Informations d’identification | Description |
| --- | --- |
| URL de l’environnement | URL de l’instance source de la [!DNL Salesforce Service Cloud]. |
| Identifiant client | L’identifiant client est utilisé conjointement avec le secret client dans le cadre de l’authentification OAuth2. Ensemble, l’identifiant client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application à [!DNL Salesforce Service Cloud]. |
| Secret client | Le secret client est utilisé conjointement avec l’identifiant client dans le cadre de l’authentification OAuth2. Ensemble, l’identifiant client et le secret client permettent à votre application d’opérer pour le compte de votre compte en identifiant votre application à [!DNL Salesforce Service Cloud]. |
| Version de l’API | Version de l’API REST de l’instance [!DNL Salesforce Service Cloud] que vous utilisez. La valeur de la version de l’API doit être formatée avec une décimale. Par exemple, si vous utilisez la version `52` de l’API, vous devez saisir la valeur comme `52.0`. Si ce champ n’est pas renseigné, Experience Platform utilise automatiquement la dernière version disponible. |

Pour plus d’informations sur l’utilisation d’OAuth pour [!DNL Salesforce Service Cloud], consultez le guide [[!DNL Salesforce Service Cloud]  sur les flux d’autorisation OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

## Connexion [!DNL Salesforce Service Cloud]à Experience Platform à l’aide d’API

- [Créer une connexion de base Salesforce Service Cloud à l’aide de l’API Flow Service](../../tutorials/api/create/customer-success/salesforce-service-cloud.md)
- [Explorer des tables de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Créer un flux de données pour une source de succès client à l’aide de l’API Flow Service](../../tutorials/api/collect/customer-success.md)

## Connexion d’[!DNL Salesforce Service Cloud] à Experience Platform à l’aide de l’interface utilisateur

- [Créer une connexion source Salesforce Service Cloud dans l’interface utilisateur](../../tutorials/ui/create/customer-success/salesforce-service-cloud.md)
- [Créer un flux de données pour une connexion source succès client dans l’interface utilisateur](../../tutorials/ui/dataflow/customer-success.md)
