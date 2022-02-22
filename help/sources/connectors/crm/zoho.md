---
keywords: Experience Platform;accueil;rubriques les plus consultées;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Présentation du connecteur source CRM Zoho
topic-legacy: overview
description: Découvrez comment connecter Zoho CRM à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 46b2fd6bc715bf1d8ccfeed576a2a2d193f92edd
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 3%

---

# [!DNL Zoho CRM]

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

Experience Platform prend en charge l’ingestion de données à partir d’un système de gestion de la relation client tiers. La prise en charge des fournisseurs de gestion de la relation client inclut [!DNL Zoho CRM].

## LISTE AUTORISÉE d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou des performances peuvent se produire lors de l’utilisation de sources. Voir [LISTE AUTORISÉE d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Récupérer vos informations d’authentification pour [!DNL Zoho CRM]

Avant d’importer des données de [!DNL Zoho CRM] à Platform, vous devez d’abord récupérer vos informations d’identification pour authentifier votre [!DNL Zoho CRM] source. Suivez les étapes ci-dessous pour récupérer votre ID client, votre secret client, votre jeton d’accès et votre jeton d’actualisation.

### Enregistrement de votre application

La première étape de la récupération de vos informations d’authentification consiste à enregistrer votre application à l’aide de la méthode [[!DNL Zoho CRM] console de développement](https://accounts.zoho.com/). Pour enregistrer votre application, vous devez sélectionner votre type de client parmi : JavaScript, web, applications mobiles, non-navigateurs ou auto-client. Indiquez ensuite des valeurs pour le nom de votre application, l’URL de votre page web et un URI de redirection autorisé qui [!DNL Zoho CRM] peut ensuite utiliser pour vous rediriger avec un jeton d’octroi.

Un enregistrement réussi renvoie votre ID client et votre secret client.

### Créer une demande d’autorisation

Ensuite, vous devez créer une [demande d’autorisation](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) à l’aide d’une application web ou d’un client autonome. La demande d’autorisation renvoie votre jeton d’autorisation, qui vous permet à son tour de récupérer votre jeton d’accès.

Lors de la création d’une demande d’autorisation, vous devez renseigner les valeurs des deux **portées** et **type d&#39;accès**. Consultez cette section [[!DNL Zoho CRM] document](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) pour plus d’informations sur les portées, pendant que **type d&#39;accès** doit toujours être défini sur `offline`.

### Générer vos jetons d’accès et d’actualisation

Une fois que vous avez récupéré votre jeton d’octroi, vous pouvez générer votre [accès et actualisation des jetons](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) en effectuant une requête de POST vers `{ACCOUNTS_URL}/oauth/v2/token` tout en fournissant votre ID client, votre secret client, votre jeton d’octroi et votre URI de redirection. Au cours de cette étape, vous devez également inclure `grant_type` en tant que paramètre, puis définissez la valeur comme `"authorization_code"`.

Une requête réussie renvoie vos jetons d’accès et d’actualisation, que vous pouvez ensuite utiliser pour vous authentifier.

Pour obtenir des instructions détaillées sur l’acquisition de vos informations d’identification, reportez-vous à la section [[!DNL Zoho CRM] guide d&#39;authentification](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connexion [!DNL Zoho CRM] to [!DNL Platform] utilisation des API

La documentation ci-dessous fournit des informations sur la connexion. [!DNL Zoho CRM] vers Platform à l’aide d’API ou de l’interface utilisateur :

- [Créez un [!DNL Zoho CRM] connexion de base à l’aide de l’API Flow Service](../../tutorials/api/create/crm/zoho.md)
- [Explorer la structure et le contenu des données d’une source CRM à l’aide de l’API Flow Service](../../tutorials/api/explore/crm.md)
- [Création d’un flux de données pour une source CRM à l’aide de l’API Flow Service](../../tutorials/api/collect/crm.md)

## Connexion [!DNL Zoho CRM] to [!DNL Platform] utilisation de l’interface utilisateur

- [Créez un [!DNL Zoho CRM] connexion source dans l’interface utilisateur](../../tutorials/ui/create/crm/zoho.md)
- [Création d’un flux de données pour une connexion source CRM dans l’interface utilisateur](../../tutorials/ui/dataflow/crm.md)
