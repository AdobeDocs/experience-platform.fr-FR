---
keywords: Experience Platform;accueil;rubriques les plus consultées;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Présentation du connecteur source Zoho CRM
description: Découvrez comment connecter Zoho CRM à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 96%

---

# [!DNL Zoho CRM]

>[!IMPORTANT]
>
>La source [!DNL Zoho CRM] sera abandonnée fin mai 2025. Vous pouvez également utiliser la source [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md).

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services [!DNL Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’un système tiers de gestion de la relation client (CRM). La prise en charge des fournisseurs de gestion de la relation client inclut [!DNL Zoho CRM].

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Consultez la page relative à la [liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Récupérer vos informations d’authentification pour [!DNL Zoho CRM]

Avant de pouvoir importer des données de votre compte [!DNL Zoho CRM] dans Platform, vous devez d’abord récupérer vos informations d’identification pour authentifier votre source [!DNL Zoho CRM]. Pour récupérer votre identifiant client, secret client, jeton d’accès et jeton d’actualisation, procédez comme suit.

### Enregistrer votre application

La première étape en vue de récupérer vos informations d’authentification consiste à enregistrer votre application à l’aide de [[!DNL Zoho CRM] Developer Console](https://accounts.zoho.com/). Pour enregistrer votre application, vous devez sélectionner votre type de client parmi les valeurs suivantes : applications JavaScript, web, mobiles, mobiles hors navigateur ou client autonome. Indiquez ensuite des valeurs pour le nom de votre application, l’URL de votre page web et un URI de redirection autorisé que [!DNL Zoho CRM] peut ensuite utiliser pour vous rediriger à lʼaide dʼun jeton d’autorisation.

Un enregistrement réussi renvoie votre identifiant et secret client.

### Créer une demande d’autorisation

Vous devez créer ensuite une [demande d’autorisation](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) à l’aide d’une application web ou d’un client autonome. La demande d’autorisation renvoie votre jeton d’autorisation, avec lequel vous pouvez récupérer votre jeton d’accès.

Lors de la création d’une demande d’autorisation, vous devez renseigner les valeurs des **portées** et du **type dʼaccès**. Pour plus d’informations sur les portées, consultez ce [[!DNL Zoho CRM] document](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html). Votre **type dʼaccès** doit toujours être défini sur `offline`.

### Générer les jetons d’accès et d’actualisation

Une fois que vous avez récupéré votre jeton d’autorisation, vous pouvez générer vos [jetons dʼaccès et dʼactualisation](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) en effectuant une requête POST vers `{ACCOUNTS_URL}/oauth/v2/token` tout en fournissant votre identifiant client, votre secret client, votre jeton d’autorisation et votre URI de redirection. Au cours de cette étape, vous devez également inclure `grant_type` en tant que paramètre et définir la valeur sur `"authorization_code"`.

Une requête réussie renvoie vos jetons d’accès et d’actualisation, que vous pouvez ensuite utiliser pour vous authentifier.

Pour obtenir des instructions détaillées sur l’acquisition de vos informations d’identification, consultez le [[!DNL Zoho CRM] guide d’authentification](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connecter [!DNL Zoho CRM] à [!DNL Platform] à lʼaide dʼAPI

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Zoho CRM] à Platform à l’aide d’API ou de l’interface utilisateur :

- [Créer une connexion de base [!DNL Zoho CRM] à l’aide de l’API Flow Service](../../tutorials/api/create/crm/zoho.md)
- [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Créer un flux de données pour une source CRM à l’aide de l’API Flow Service](../../tutorials/api/collect/crm.md)

## Connecter [!DNL Zoho CRM] à [!DNL Platform] à lʼaide de l’interface utilisateur

- [Créer une connexion source  [!DNL Zoho CRM]  dans l’interface utilisateur](../../tutorials/ui/create/crm/zoho.md)
- [Créer un flux de données pour une connexion source CRM dans l’interface utilisateur](../../tutorials/ui/dataflow/crm.md)
