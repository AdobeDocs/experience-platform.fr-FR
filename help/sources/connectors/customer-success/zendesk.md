---
title: Présentation du connecteur source Zendesk
description: Découvrez comment connecter Zendesk à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 47%

---

# [!DNL Zendesk]

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’une application de succès client tierce. La prise en charge des fournisseurs de succès client inclut [!DNL Zendesk].

Cette Adobe Experience Platform [sources](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=fr) tire parti de la fonction [API de recherche Zendesk > Exporter les résultats de recherche](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) qui renvoie les informations sur les utilisateurs dans Experience Platform à partir de Zendesk pour un traitement ultérieur.

## Liste autorisée d’adresses IP

Une liste d’adresses IP doit être ajoutée à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Authentifiez votre [!DNL Zendesk] account

[!DNL Zendesk] utilise des jetons porteur comme mécanisme d’authentification pour communiquer avec l’API [!DNL Zendesk]

Cette section décrit les étapes préalables à l’authentification [!DNL Zendesk] compte .

* La première étape de l’authentification [!DNL Zendesk] afin de vous assurer que vous avez [!DNL Zendesk] compte d’assistance. Si vous n’en avez pas déjà un, la fonction [[!DNL Zendesk] page d&#39;inscription](https://www.zendesk.fr/register/) pour enregistrer et créer votre compte Zendesk.
* Une fois que vous êtes enregistré, accédez à la [[!DNL Zendesk] site web](https://www.zendesk.com/login/) et fournissez vos **subdomain**.
* Ensuite, sélectionnez **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Enfin, récupérez votre jeton API à partir de la fonction **[!DNL API token]** .

![Jeton d’API Zendesk](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Voir [[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->) pour plus d’informations sur la manière de récupérer votre sous-domaine. Pour plus d’informations sur la génération de votre jeton API, voir [[!DNL Zendesk] guide sur la génération d’un nouveau jeton API](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>).

La documentation ci-dessous fournit des informations sur la connexion d’[!DNL Zendesk] à Platform à l’aide d’API ou de l’interface utilisateur :

## Connecter [!DNL Zendesk] à Platform à l’aide d’API

* [Création d’une connexion source et d’un flux de données pour [!DNL Zendesk] utilisation de l’API Flow Service](../../tutorials/api/create/customer-success/zendesk.md)

## Connecter [!DNL Zendesk] à Platform à l’aide de l’interface utilisateur

* [Créer une connexion source  [!DNL Zendesk ] dans l’interface utilisateur](../../tutorials/ui/create/customer-success/zendesk.md)
* [Création d’un flux de données pour une connexion de source de succès client dans l’interface utilisateur](../../tutorials/ui/dataflow/customer-success.md)
