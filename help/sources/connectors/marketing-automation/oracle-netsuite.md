---
title: Présentation d’Oracle NetSuite Source
description: Découvrez comment connecter Oracle NetSuite à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
last-substantial-update: 2024-01-30T00:00:00Z
exl-id: 1dd30660-c990-4d3f-a64f-2a17e426f56d
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 14%

---

# [!DNL Oracle NetSuite]

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données dans un système d’automatisation marketing tiers. La prise en charge des fournisseurs d’automatisation marketing inclut [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) est une suite de gestion d’entreprise cloud regroupant des solutions ERP/financières, CRM et e-commerce.

Vous pouvez utiliser deux sources différentes pour ingérer des données de [!DNL Oracle NetSuite] vers Experience Platform :

* Utilisez la source de [!DNL Oracle NetSuite Activities] pour ingérer des données d’événements.
* Utilisez la source de [!DNL Oracle NetSuite Entities] pour ingérer les données des clients et des contacts.

Consultez le tableau suivant pour plus d’informations sur les deux sources de [!DNL Oracle NetSuite].

| Source | Type | Description |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Événement | Récupérez les activités planifiées ajoutées à votre calendrier. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Client | Récupérez des données client spécifiques, y compris des détails tels que les noms, adresses et identifiants clés du client. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Contact | Récupérez les noms de contacts, les e-mails, les numéros de téléphone et tout champ personnalisé associé aux contacts associé aux clients. |

## Liste autorisée d’adresses IP {#ip-allow-list}

Il peut être nécessaire d’ajouter une liste d’adresses IP à une liste autorisée de données avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Conditions préalables {#prerequisites}

Avant de pouvoir importer vos données [!DNL Oracle NetSuite] dans Experience Platform, vous devez d’abord vous assurer que vous disposez des éléments suivants :

* **Un compte [!DNL Oracle NetSuite]**.
   * Contactez [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) si vous ne disposez pas déjà d’un compte valide.
* Un **abonnement actif** à n’importe quel produit [!DNL Oracle NetSuite].
* Un **ID de compte**.
   * La source [!DNL Oracle NetSuite] utilise OAuth 2.0 pour communiquer avec les API [!DNL Oracle NetSuite]. Si vous ne disposez pas de votre identifiant de compte, consultez la documentation [!DNL Oracle] sur [comment récupérer votre identifiant de compte](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* Une combinaison **identifiant client** et **secret client**.
   * L’identifiant client et le secret client sont requis pour accéder aux API [!DNL Oracle NetSuite]. Au cours de cette étape, vous devez également vous assurer que votre administrateur dispose des éléments suivants :
      * Activation de la fonctionnalité OAuth 2.0 et configuration des rôles OAuth 2.0 appropriés.
      * Affectation des utilisateurs aux rôles OAuth 2.0 et création des enregistrements d’intégration nécessaires.
* Un **jeton d’accès** et un **jeton d’actualisation**.
   * Pour plus d’informations sur la génération de vos jetons d’accès et d’actualisation[!DNL Oracle] reportez-vous au guide de [&#x200B; sur le &#x200B;](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow)flux d’octroi de code d’autorisation OAuth 2.0.

### Collecter les informations d’identification requises {#gather-credentials}

Pour connecter [!DNL Oracle NetSuite] à Experience Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Identifiant client | Valeur de l’identifiant client générée lors de la création de l’enregistrement d’intégration dans [!DNL Oracle NetSuite]. Pour plus d’informations, consultez le guide [!DNL Oracle] sur la [création d’enregistrements d’intégration](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981). | `7fce.....b42f`<br>La valeur est une chaîne de 64 caractères. |
| Secret client | Valeur du secret client générée lors de la création de l’enregistrement d’intégration. Pour plus d’informations, consultez le guide [!DNL Oracle] sur la [création d’enregistrements d’intégration](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981). | `5c98.....1b46`<br>La valeur est une chaîne de 64 caractères. |
| URL du test d’autorisation | (Facultatif) Votre URL de test d’autorisation [!DNL NetSuite]. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Jeton d’accès | Le jeton d’accès est au format JSON Web Token (JWT) et n’est valide que pendant 60 minutes. Pour plus d’informations sur la manière de récupérer votre jeton d’accès, consultez le guide [!DNL Oracle] sur l’autorisation [OAuth 2.0 pour NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> La valeur est une chaîne de 1 024 caractères formatée en jeton JSON Web Token (JWT). |
| Actualiser le jeton | Utilisez l’actualisation pour générer un nouveau jeton d’accès, après l’expiration de votre jeton d’accès. Le jeton d’actualisation est valide pendant sept jours. Pour plus d’informations sur la manière de récupérer votre jeton d’accès, consultez le guide [!DNL Oracle] sur l’autorisation [OAuth 2.0 pour NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> La valeur est une chaîne de 1 024 caractères formatée en jeton JSON Web Token (JWT). |
| URL du jeton d’accès | Point d’entrée du jeton vers lequel l’application envoie les requêtes POST. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>Après l’expiration d’un jeton d’actualisation, vous devez créer un compte dans Experience Platform avec vos jetons mis à jour.

## Connexion de [!DNL Oracle NetSuite Activities] à Experience Platform {#oracle-netsuite-activities}

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Oracle NetSuite Activities] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

* [Créez une connexion source et un flux de données pour importer  [!DNL Oracle NetSuite Activities]  données dans Experience Platform à l’aide d’API](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [Connectez votre compte  [!DNL Oracle NetSuite Activities]  Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [Créez un flux de données pour une connexion source à l’aide de l’interface utilisateur](../../tutorials/ui/dataflow/marketing-automation.md).

## Connexion de [!DNL Oracle NetSuite Entities] à Experience Platform {#oracle-netsuite-entities}

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Oracle NetSuite Entities] à Experience Platform à l’aide d’API ou de l’interface utilisateur :

* [Créez une connexion source et un flux de données pour importer  [!DNL Oracle NetSuite Entities]  données dans Experience Platform à l’aide d’API](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [Connectez votre compte  [!DNL Oracle NetSuite Entities]  Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [Créez un flux de données pour une connexion source à l’aide de l’interface utilisateur](../../tutorials/ui/dataflow/marketing-automation.md).
