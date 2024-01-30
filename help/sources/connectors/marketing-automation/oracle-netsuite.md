---
title: Présentation de la source Oracle NetSuite
description: Découvrez comment connecter Oracle NetSuite à Adobe Experience Platform à l’aide des API ou de l’interface utilisateur.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Version Beta
source-git-commit: 632cff3ee4ca82d391e9a1df0cb38d903e8a5428
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 21%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>La source [!DNL Oracle NetSuite] est en version Beta. Veuillez lire la [présentation des sources](../../home.md#terms-and-conditions) pour plus d’informations sur l’utilisation de sources étiquetées bêta.

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données dans un système tiers d’automatisation du marketing. La prise en charge des fournisseurs d’automatisation marketing inclut [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) est une suite de gestion d’entreprise dans le cloud qui englobe les solutions de gestion de la relation client, de gestion de la relation client et de commerce électronique.

Vous pouvez utiliser deux sources différentes pour ingérer des données à partir de [!DNL Oracle NetSuite] à l’Experience Platform :

* Utilisez la variable [!DNL Oracle NetSuite Activities] source pour ingérer des données d’événements.
* Utilisez la variable [!DNL Oracle NetSuite Entities] source pour ingérer les données client et contact.

Pour plus d’informations sur les deux [!DNL Oracle NetSuite] sources.

| Source | Type | Description |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Événement | Récupérez les activités planifiées ajoutées à votre calendrier. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Client | Récupérez des données client spécifiques, notamment des détails tels que les noms de client, les adresses et les identifiants clés. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Contact | Récupérez les noms de contact, les e-mails, les numéros de téléphone et tous les champs personnalisés liés aux contacts associés aux clients. |

## Liste autorisée d’adresses IP {#ip-allow-list}

Il peut être nécessaire d’ajouter une liste d’adresses IP à une liste autorisée avant d’utiliser les connecteurs source. Si vous n’ajoutez pas vos adresses IP spécifiques à une région à votre liste autorisée, des erreurs ou une absence de performances peuvent se produire lors de l’utilisation de sources. Voir la page [Liste autorisée d’adresses IP](../../ip-address-allow-list.md) pour plus d’informations.

## Conditions préalables {#prerequisites}

Avant d’apporter votre [!DNL Oracle NetSuite] pour Experience Platform, vous devez d’abord vous assurer que vous disposez des éléments suivants :

* **Un [!DNL Oracle NetSuite] account**.
   * Contact [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) si vous ne disposez pas déjà d’un compte valide.
* Un **abonnement actif** à tout [!DNL Oracle NetSuite] produit.
* Un **ID de compte**.
   * La variable [!DNL Oracle NetSuite] La source utilise OAuth 2.0 pour communiquer avec le [!DNL Oracle NetSuite] API. Si vous ne disposez pas de votre ID de compte, rendez-vous sur la page [!DNL Oracle] documentation sur [comment récupérer votre ID de compte](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* A **ID client** et **secret client** combinaison
   * L’ID client et le secret client sont requis pour accéder à [!DNL Oracle NetSuite] API. Au cours de cette étape, vous devez également vous assurer que votre administrateur dispose des éléments suivants :
      * Activation de la fonction OAuth 2.0 et configuration des rôles OAuth 2.0 appropriés.
      * Affectez des utilisateurs aux rôles OAuth 2.0 et créez les enregistrements d’intégration nécessaires.
* Un **jeton d’accès** et un **jeton d’actualisation**.
   * Voir [!DNL Oracle] guide on [Flux d’octroi du code d’autorisation OAuth 2.0](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) pour plus d’informations sur la génération de vos jetons d’accès et d’actualisation.

### Collecter les informations d’identification requises {#gather-credentials}

Pour connecter [!DNL Oracle NetSuite] à Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| Identifiant client | La valeur de l’ID client générée lors de la création de l’enregistrement d’intégration dans [!DNL Oracle NetSuite]. Lisez la section [!DNL Oracle] guide sur la manière de procéder [création d’enregistrements d’intégration](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) pour plus d’informations. | `7fce.....b42f`<br>La valeur est une chaîne de 64 caractères. |
| Secret client | La valeur du secret client générée lors de la création de l’enregistrement d’intégration. Lisez la section [!DNL Oracle] guide sur la manière de procéder [création d’enregistrements d’intégration](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) pour plus d’informations. | `5c98.....1b46`<br>La valeur est une chaîne de 64 caractères. |
| URL de test d’autorisation | (Facultatif) Votre [!DNL NetSuite] URL du test d’autorisation. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Jeton d’accès | Le jeton d’accès est au format JSON Web Token (JWT) et n’est valide que pendant 60 minutes. Pour plus d’informations sur la manière de récupérer votre jeton d’accès, consultez la section [!DNL Oracle] guide on [Autorisation OAuth 2.0 pour NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> La valeur est une chaîne de 1 024 caractères au format JSON Web Token (JWT). |
| Jeton d’actualisation | Utilisez l’actualisation pour générer un nouveau jeton d’accès, une fois votre jeton d’accès expiré. Le jeton d’actualisation est valide pendant sept jours. Pour plus d’informations sur la manière de récupérer votre jeton d’accès, consultez la section [!DNL Oracle] guide on [Autorisation OAuth 2.0 pour NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> La valeur est une chaîne de 1 024 caractères au format JSON Web Token (JWT). |
| URL du jeton d’accès | Point de terminaison de jeton vers lequel l’application envoie les demandes du POST. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>Après l’expiration d’un jeton d’actualisation, vous devez créer un nouveau compte en Experience Platform avec vos jetons mis à jour.

## Connecter [!DNL Oracle NetSuite Activities] à Platform {#oracle-netsuite-activities}

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Oracle NetSuite Activities] à Platform à l’aide d’API ou de l’interface utilisateur :

* [Créer une connexion source et un flux de données à importer [!DNL Oracle NetSuite Activities] données vers Platform à l’aide d’API](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [Connectez-vous à [!DNL Oracle NetSuite Activities] compte à Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [Créer un flux de données pour une connexion source à l’aide de l’interface utilisateur](../../tutorials/ui/dataflow/marketing-automation.md).

## Connecter [!DNL Oracle NetSuite Entities] à Platform {#oracle-netsuite-entities}

La documentation ci-dessous fournit des informations sur la connexion de [!DNL Oracle NetSuite Entities] à Platform à l’aide d’API ou de l’interface utilisateur :

* [Créer une connexion source et un flux de données à importer [!DNL Oracle NetSuite Entities] données vers Platform à l’aide d’API](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [Connectez-vous à [!DNL Oracle NetSuite Entities] compte à Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [Créer un flux de données pour une connexion source à l’aide de l’interface utilisateur](../../tutorials/ui/dataflow/marketing-automation.md).
