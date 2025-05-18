---
title: Présentation du connecteur MySQL Source
description: Découvrez comment connecter MySQL à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
last-substantial-update: 2025-05-17T00:00:00Z
exl-id: a18e8e69-880f-4bee-b339-726091d6f858
source-git-commit: f758479c37b72752bbb8a371de88bf653b2e6030
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 5%

---

# [!DNL MySQL]

[!DNL MySQL] est un système de gestion de base de données relationnelle open source utilisé pour stocker et gérer des données structurées. Il organise les données en tables et utilise le langage SQL (Structured Query Language) pour interroger et mettre à jour les informations. [!DNL MySQL] est largement utilisé dans les applications web, prend en charge plusieurs plateformes et est connu pour sa vitesse, sa fiabilité et sa facilité d’utilisation.

Vous pouvez utiliser la source de [!DNL MySQL] pour connecter votre compte et ingérer les données de votre base de données [!DNL MySQL] vers Adobe Experience Platform.

## Prérequis {#prerequisites}

Lisez les sections suivantes pour terminer la configuration requise avant de connecter votre compte [!DNL MySQl] à Experience Platform.

### Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform sur Azure ou Amazon Web Services (AWS). Pour plus d’informations, consultez le guide sur la [liste autorisée des adresses IP pour se connecter à Experience Platform sur Azure et AWS](../../ip-address-allow-list.md).

### S’authentifier auprès d’Experience Platform sur Azure {#azure}

Vous pouvez utiliser l’authentification par clé de compte ou l’authentification de base pour connecter votre base de données [!DNL MySQL] à Experience Platform sur Azure.

>[!BEGINTABS]

>[!TAB Authentification de la clé de compte]

Fournissez des valeurs pour les informations d’identification suivantes afin de connecter votre base de données [!DNL MySQL] à Experience Platform à l’aide de l’authentification par clé de compte.

| Informations d’identification | Description |
| --- | --- |
| `connectionString` | Chaîne de connexion [!DNL MySQL] associée à votre compte. Le modèle de chaîne de connexion [!DNL MySQL] est : `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL MySQL] est `26d738e0-8963-47ea-aadf-c60de735468a`. |

Pour plus d’informations, consultez la [[!DNL MySQL] documentation sur les chaînes de connexion](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html).

>[!TAB  Authentification de base ]

Fournissez des valeurs pour les informations d’identification suivantes afin de connecter votre base de données [!DNL MySQL] à Experience Platform à l’aide de l’authentification de base.

| Informations d’identification | Description |
| --- | --- |
| `server` | Nom ou adresse IP de la base de données [!DNL MySQL]. |
| `username` | Nom d’utilisateur associé à l’authentification de la base de données [!DNL MySQL]. |
| `password` | Mot de passe associé à l’authentification de la base de données [!DNL MySQL]. |
| `database` | Nom de la base de données [!DNL MySQL] à laquelle vous souhaitez vous connecter. |
| `sslMode` | Méthode [!DNL Secure Sockets Layer] (SSL) à appliquer à la connexion. Les valeurs disponibles sont les suivantes : <ul><li>`DISABLED` : utilisez cette option pour désactiver SSL. Si votre serveur nécessite une configuration SSL, la connexion échoue</li><li>`PREFERRED` : utilisez cette option pour préférer les connexions SSL, étant donné qu’elles sont prises en charge par le serveur. Cette option permet également les connexions non SSL.</li><li>`REQUIRED` : utilisez cette option pour rendre les connexions SSL obligatoires. Si le serveur ne prend pas en charge SSL, les connexions échouent.</li><li>`Verify-Ca` : utilisez cette option pour vérifier les certificats du serveur lors de l’échec des connexions si le serveur ne prend pas en charge SSL.</li><li>`Verify Identity` : utilisez cette option pour vérifier les certificats de serveur portant le nom de l’hôte lors de l’échec des connexions si le serveur ne prend pas en charge SSL.</li></ul> |

>[!ENDTABS]

### Authentification à Experience Platform sur Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).

Vous devez fournir des valeurs pour les informations d’identification suivantes pour connecter [!DNL MySQL] à Experience Platform sur AWS.

| Informations d’identification | Description |
| --- | --- |
| `server` | Nom ou adresse IP de la base de données [!DNL MySQL]. |
| `username` | Nom de la base de données. |
| `password` | Nom d’utilisateur correspondant à votre base de données. |
| `database` | Mot de passe correspondant à votre base de données. |
| `sslMode` | Méthode [!DNL Secure Sockets Layer] (SSL) à appliquer à la connexion. Les valeurs disponibles sont les suivantes : <ul><li>`DISABLED` : utilisez cette option pour désactiver SSL. Si votre serveur nécessite une configuration SSL, la connexion échoue</li><li>`PREFERRED` : utilisez cette option pour préférer les connexions SSL, étant donné qu’elles sont prises en charge par le serveur. Cette option permet également les connexions non SSL.</li><li>`REQUIRED` : utilisez cette option pour rendre les connexions SSL obligatoires. Si le serveur ne prend pas en charge SSL, les connexions échouent.</li><li>`Verify-Ca` : utilisez cette option pour vérifier les certificats du serveur lors de l’échec des connexions si le serveur ne prend pas en charge SSL.</li><li>`Verify Identity` : utilisez cette option pour vérifier les certificats de serveur portant le nom de l’hôte lors de l’échec des connexions si le serveur ne prend pas en charge SSL.</li></ul> |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL MySQL] est `26d738e0-8963-47ea-aadf-c60de735468a`. **Remarque** : ces informations d’identification ne sont requises que lors de la connexion via l’API [!DNL Flow Service]. |

## Connexion de [!DNL MySQL] à Experience Platform à l’aide d’API

- [Connecter votre base  [!DNL MySQL]  données à l’aide de l’API Flow Service](../../tutorials/api/create/databases/mysql.md)
- [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Créer un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

## Connecter MySQL à Experience Platform à l’aide de l’interface utilisateur

- [Connecter votre base  [!DNL MySQL]  données à Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/databases/mysql.md)
- [Créer un flux de données pour une connexion source de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)
