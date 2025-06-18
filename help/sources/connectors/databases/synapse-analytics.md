---
title: Présentation Du Connecteur Source Azure Synapse Analytics
description: Découvrez comment connecter Azure Synapse Analytics à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2025-06-17T00:00:00Z
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 8%

---

# [!DNL Azure Synapse Analytics]

>[!IMPORTANT]
>
>La source [!DNL Azure Synapse Analytics] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.

[!DNL Azure Synapse Analytics] est un service d’analyse basé sur le cloud qui unifie le big data et l’entreposage de données. Vous pouvez ingérer, explorer, préparer et analyser des données à l’aide d’outils SQL, [!DNL Spark] ou en temps réel, le tout sans déplacer vos données.

Vous pouvez utiliser la source de [!DNL Azure Synapse Analytics] pour connecter votre compte et importer vos données dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Lisez les sections suivantes pour terminer la configuration requise avant de connecter votre compte [!DNL Azure Synapse Analytics] à Experience Platform.

### Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform. Placer sur la liste autorisée Pour plus d’informations, consultez le guide sur la [connexion des adresses IP à Experience Platform](../../ip-address-allow-list.md).

### Configuration des autorisations

Pour connecter votre compte source à Experience Platform, les deux autorisations ci-dessous doivent être activées pour votre compte :

* **Affichage des sources**
* **Gestion des sources**

Si vous ne disposez pas de ces autorisations, contactez votre administrateur de produit pour demander l’accès. Pour plus d’informations, consultez le [guide de l’interface utilisateur du contrôle d’accès](../../../access-control/ui/overview.md).

### S’authentifier auprès d’Experience Platform

Vous pouvez utiliser l’authentification par clé de compte ou l’authentification par clé principale de service pour connecter votre [!DNL Azure Synapse Analytics] à Experience Platform.

>[!BEGINTABS]

>[!TAB Authentification de la clé de compte]

Fournissez des valeurs pour les informations d’identification suivantes afin de connecter votre base de données [!DNL Azure Synapse Analytics] à Experience Platform à l’aide de l’authentification par clé de compte.

| Informations d’identification | Description |
| --- | --- |
| Chaîne de connexion | Il s’agit de la **chaîne de connexion** utilisée pour l’authentification avec [!DNL Azure Synapse Analytics]. Le format standard est : `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. Vous devez remplacer les espaces réservés par vos détails de connexion réels. |
| Identifiant de spécification de connexion | La **spécification de connexion** fournit les propriétés de connecteur d’une source de données. Cela inclut des détails tels que les spécifications d’authentification et les exigences pour la création de connexions **de base** et **source**. Par [!DNL Azure Synapse Analytics], l’identifiant de spécification de connexion est : `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. **Remarque :** ces informations d’identification ne sont nécessaires que lors de la connexion via les API. |

>[!TAB Authentification de la clé principale du service]

Pour récupérer vos informations d’identification pour l’authentification de la clé principale du service, accédez à la [[!DNL Microsfot Entra admin center]](https://entra.microsoft.com/#home) et récupérez les valeurs des éléments suivants :

* ID d’application
* Nom d’affichage
* Secret
* ID du client

Ensuite, accédez à votre [[!DNL Azure Synapse Analytics] instance](https://azure.microsoft.com/en-ca/products/synapse-analytics), puis sélectionnez l’option permettant de créer un utilisateur à partir d’un fournisseur externe. À partir de là, indiquez les autorisations appropriées pour le principal de service sur le schéma. **REMARQUE :** : vous devez inclure « SELECT », car il est obligatoire pour la prévisualisation du schéma, comme pour « COPY ». Par exemple, une commande d&#39;exemple peut être :

```SQL
GRANT SELECT ON SCHEMA::dbo TO {APP_ID};
```

Fournissez des valeurs pour les informations d’identification suivantes afin de connecter votre base de données [!DNL Azure Synapse Analytics] à Experience Platform à l’aide de l’authentification par clé principale de service.

| Informations d’identification | Description |
| --- | --- |
| Serveur | Nom de domaine complet de votre point d’entrée SQL [!DNL Azure Synapse Analytics]. |
| Base de données | Nom de la base de données spécifique dans votre espace de travail [!DNL Azure Synapse Analytics]. |
| Locataire | Identifiant client [!DNL Azure Active Directory] associé à votre abonnement [!DNL Azure]. |
| ID de service principal | Identifiant client d’une application [!DNL Azure Active Directory]. |
| Clé de service principale | Secret client ou mot de passe associé au principal de service. |
| Identifiant de spécification de connexion | La **spécification de connexion** fournit les propriétés de connecteur d’une source de données. Cela inclut des détails tels que les spécifications d’authentification et les exigences pour la création de connexions **de base** et **source**. Par [!DNL Azure Synapse Analytics], l’identifiant de spécification de connexion est : `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`. **Remarque :** ces informations d’identification ne sont nécessaires que lors de la connexion via les API. |

Pour plus d’informations, consultez la documentation [[!DNL Azure]  sur la gestion des identités pour  [!DNL Azure Synapse Analytics]](https://learn.microsoft.com/en-us/azure/synapse-analytics/synapse-service-identity).

>[!ENDTABS]

## Connexion de [!DNL Azure Synapse Analytics] à Experience Platform à l’aide d’API

* [Connexion  [!DNL Azure Synapse Analytics]  Experience Platform à l’aide de l’API Flow Service](../../tutorials/api/create/databases/synapse-analytics.md)
* [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
* [Créer un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

## Connexion d’[!DNL Azure Synapse Analytics] à Experience Platform à l’aide de l’interface utilisateur

* [Connexion  [!DNL Azure Synapse Analytics]  Experience Platform dans l’interface utilisateur](../../tutorials/ui/create/databases/synapse-analytics.md)
* [Créer un flux de données pour une connexion source de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)

