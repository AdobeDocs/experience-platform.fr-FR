---
title: Présentation du connecteur Source Zendesk
description: Découvrez comment connecter Zendesk à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 22%

---

# [!DNL Zendesk]

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’une application de succès client tierce. La prise en charge des fournisseurs de succès client inclut [!DNL Zendesk].

Ce Adobe Experience Platform [sources](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=fr) tire parti de l’[API de recherche Zendesk > Exporter les résultats de recherche](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) qui renvoie les informations des utilisateurs vers Experience Platform à partir de Zendesk pour un traitement ultérieur.

## Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform. Placer sur la liste autorisée Pour plus d’informations, consultez le guide sur la [connexion des adresses IP à Experience Platform](../../ip-address-allow-list.md).

## Authentification de votre compte [!DNL Zendesk]

[!DNL Zendesk] utilise des jetons porteur comme mécanisme d’authentification pour communiquer avec l’API [!DNL Zendesk].

Cette section décrit les étapes préalables à suivre pour authentifier votre compte [!DNL Zendesk].

* La première étape de l’authentification de votre compte [!DNL Zendesk] consiste à vérifier que vous disposez d’[!DNL Zendesk] compte d’assistance. Si vous n’en avez pas encore, consultez la [[!DNL Zendesk] page d’enregistrement](https://www.zendesk.fr/register/) pour vous enregistrer et créer votre compte Zendesk.
* Une fois l’enregistrement effectué, accédez au [[!DNL Zendesk] site web](https://www.zendesk.com/login/) et indiquez votre **sous-domaine**.
* Sélectionnez ensuite **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Enfin, récupérez votre jeton API dans la section **[!DNL API token]** .

![&#x200B; Jeton API Zendesk &#x200B;](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Voir la [[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->) pour plus d’informations sur la récupération de votre sous-domaine. Pour plus d’informations sur la génération de votre jeton API, consultez le guide [[!DNL Zendesk]  sur la génération d’un nouveau jeton API](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>).

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Zendesk] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

## Connexion de [!DNL Zendesk] à Experience Platform à l’aide d’API

* [Créer une connexion source et un flux de données pour à l’aide  [!DNL Zendesk]  l’API Flow Service](../../tutorials/api/create/customer-success/zendesk.md)

## Connexion d’[!DNL Zendesk] à Experience Platform à l’aide de l’interface utilisateur

* [Créer une connexion source  [!DNL Zendesk &#x200B;] dans l’interface utilisateur](../../tutorials/ui/create/customer-success/zendesk.md)
* [Créer un flux de données pour une connexion source de succès client dans l’interface utilisateur](../../tutorials/ui/dataflow/customer-success.md)
