---
keywords: Experience Platform ; accueil ; rubriques populaires ; Zoho CRM ; zoho crm ; Zoho ; zoho
solution: Experience Platform
title: Présentation du connecteur source Zoho CRM
topic-legacy: overview
description: Découvrez comment connecter Zoho CRM à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
exl-id: fcd7af48-e66a-4313-bbfe-73301d335c67
source-git-commit: 7a15090d8ed2c1016d7dc4d7d3d0656640c4785c
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 3%

---

# (version bêta) [!DNL Zoho CRM]

>[!NOTE]
>
>Le [!DNL Zoho CRM] source est en version bêta. Voir la section [Présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de connecteurs étiquetés bêta.

Adobe Experience Platform permet d’assimiler des données à partir de sources externes tout en vous permettant de structurer, étiqueter et améliorer les données entrantes à l’aide de [!DNL Platform] services. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, des bases de données, etc.

Experience Platform prend en charge l’assimilation de données à partir d’un système CRM tiers. La prise en charge des fournisseurs de CRM inclut [!DNL Zoho CRM].

## Liste d&#39;autorisations d&#39;adresses IP

Une liste d&#39;adresses IP doit être ajoutée à une liste d&#39;autorisations avant d&#39;utiliser des connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à votre région à votre liste d’autorisations, des erreurs ou des performances risquent de se produire lors de l’utilisation de sources. Voir la section [Liste d&#39;autorisations d&#39;adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Récupérez vos informations d’authentification pour [!DNL Zoho CRM]

Avant d’importer des données de votre [!DNL Zoho CRM] sur la plate-forme, vous devez d’abord récupérer vos informations d’identification pour authentifier votre [!DNL Zoho CRM] source. Suivez les étapes ci-dessous pour récupérer votre ID client, votre secret client, votre jeton d’accès et votre jeton d’actualisation.

### Enregistrement de votre application

La première étape de la récupération de vos identifiants d’authentification consiste à enregistrer votre application à l’aide de la [[!DNL Zoho CRM] console développeur](https://accounts.zoho.com/). Pour enregistrer votre demande, vous devez sélectionner votre type de client parmi : Java Script, Web, mobile, non-navigateur, applications mobiles ou autoclient. Indiquez ensuite des valeurs pour le nom de votre application, l’URL de votre page Web et un URI de redirection autorisé qui [!DNL Zoho CRM] peut ensuite vous utiliser pour vous rediriger avec un jeton de subvention.

Une inscription réussie renvoie votre ID client et votre secret client.

### Création d’une demande d’autorisation

Ensuite, vous devez créer un [demande d&#39;autorisation](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) à l’aide d’une application Web ou d’un client autonome. La demande d’autorisation renvoie votre jeton de subvention, ce qui vous permet à son tour de récupérer votre jeton d’accès.

Lors de la création d’une demande d’autorisation, vous devez renseigner les valeurs des deux **domaines** et **type d&#39;accès**. Reportez-vous à [[!DNL Zoho CRM] document](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) pour plus d’informations sur les domaines, tandis que **type d&#39;accès** doit toujours être défini sur `offline`.

### Génération de vos jetons d’accès et actualisation

Une fois que vous avez récupéré votre jeton de subvention, vous pouvez générer votre [accès et actualisation des jetons](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) en adressant une demande de POST à `{ACCOUNTS_URL}/oauth/v2/token` lors de la fourniture de votre ID client, de votre secret client, de votre jeton d’octroi et de votre URI de redirection. Au cours de cette étape, vous devez également inclure `grant_type` en tant que paramètre, puis définissez la valeur comme `"authorization_code"`.

Une demande réussie renvoie vos jetons d’accès et d’actualisation, que vous pouvez ensuite utiliser pour vous authentifier.

Pour connaître les étapes détaillées de l’acquisition de vos identifiants, consultez la section [[!DNL Zoho CRM] guide d’authentification](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connexion [!DNL Zoho CRM] à [!DNL Platform] utilisation d’API

La documentation ci-dessous fournit des informations sur la connexion. [!DNL Zoho CRM] vers la plate-forme à l’aide d’API ou de l’interface utilisateur :

- [Créer un [!DNL Zoho CRM] connexion de base à l’aide de l’API Flow Service](../../tutorials/api/create/crm/zoho.md)
- [Exploration de la structure de données et du contenu d’une source CRM à l’aide de l’API Flow Service](../../tutorials/api/explore/crm.md)
- [Création d’un flux de données pour une source CRM à l’aide de l’API Flow Service](../../tutorials/api/collect/crm.md)

## Connexion [!DNL Zoho CRM] à [!DNL Platform] à l’aide de l’interface utilisateur

- [Créer un [!DNL Zoho CRM] connexion source dans l’interface utilisateur](../../tutorials/ui/create/crm/zoho.md)
- [Création d’un flux de données pour une connexion source CRM dans l’interface utilisateur](../../tutorials/ui/dataflow/crm.md)
