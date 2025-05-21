---
title: Présentation du connecteur Source PostgreSQL
description: Découvrez la source PostgreSQL sur Adobe Experience Platform.
last-substantial-update: 2025-05-20T00:00:00Z
exl-id: 27b891c5-5fc5-4539-8f98-e3a53e2eefe3
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 13%

---

# [!DNL PostgreSQL]

Lisez ce document pour découvrir les étapes préalables à suivre avant de pouvoir connecter votre base de données [!DNL PostgreSQL] à Adobe Experience Platform.

## Prérequis {#prerequisites}

Lisez les sections suivantes pour terminer la configuration requise avant de connecter votre base de données [!DNL PostgreSQL] à Experience Platform.

### Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform sur Azure ou Amazon Web Services (AWS). Pour plus d’informations, consultez le guide sur la [liste autorisée des adresses IP pour se connecter à Experience Platform sur Azure et AWS](../../ip-address-allow-list.md).

### S’authentifier auprès d’Experience Platform sur Azure {#azure}

Vous devez fournir des valeurs pour les informations d’authentification suivantes pour connecter [!DNL PostgreSQL] à Experience Platform sur Azure.

>[!BEGINTABS]

>[!TAB Authentification de la clé de compte]

Fournissez des valeurs pour les informations d’identification suivantes afin de connecter votre base de données [!DNL PostgreSQL] à Experience Platform sur Azure à l’aide de l’authentification par clé de compte.

| Informations d’identification | Description |
| --- | --- |
| `connectionString` | Chaîne de connexion associée à votre compte [!DNL PostgreSQL]. Le modèle de chaîne de connexion [!DNL PostgreSQL] est : `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL PostgreSQL] est `74a1c565-4e59-48d7-9d67-7c03b8a13137`. Ces informations d’identification ne sont requises que lors de la connexion via l’API [!DNL Flow Service]. |

Pour plus d’informations, consultez la [[!DNL PostgreSQL] documentation](https://www.postgresql.org/docs/current/) .

>[!TAB  Authentification de base ]

Fournissez des valeurs pour les informations d’identification suivantes afin de connecter votre base de données [!DNL PostgreSQL] à Experience Platform sur Azure à l’aide de l’authentification de base.

| Informations d’identification | Description |
| --- | --- |
| `server` | Nom ou adresse IP de la base de données [!DNL PostgreSQL]. |
| `port` | Port TCP du serveur [!DNL PostgreSQL]. |
| `username` | Nom d’utilisateur associé à l’authentification de la base de données [!DNL PostgreSQL]. |
| `password` | Mot de passe associé à l’authentification de la base de données [!DNL PostgreSQL]. |
| `database` | Nom de la base de données [!DNL PostgreSQL] à laquelle vous souhaitez vous connecter. |
| `sslMode` | Méthode [!DNL Secure Sockets Layer] (SSL) à appliquer à la connexion. Les valeurs disponibles sont les suivantes : <ul><li>`Disable` : utilisez cette option pour désactiver SSL. Si votre serveur nécessite une configuration SSL, la connexion échoue.</li><li>`Allow` : utilisez cette option pour autoriser les connexions SSL. Les connexions non SSL peuvent toujours être utilisées si le serveur les prend en charge.</li><li>`Prefer` : utilisez cette option pour préférer les connexions SSL, étant donné qu’elles sont prises en charge par le serveur. Cette option permet également les connexions non SSL.</li><li>`Require` : utilisez cette option pour rendre les connexions SSL obligatoires. Si le serveur ne prend pas en charge SSL, les connexions échouent.</li><li>`Verify-Ca` : utilisez cette option pour vérifier les certificats du serveur lors de l’échec des connexions si le serveur ne prend pas en charge SSL.</li><li>`Verify-Full` : utilisez cette option pour vérifier les certificats de serveur portant le nom de l’hôte lors de l’échec des connexions si le serveur ne prend pas en charge SSL.</li></ul> |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL PostgreSQL] est `74a1c565-4e59-48d7-9d67-7c03b8a13137`. Ces informations d’identification ne sont requises que lors de la connexion via l’API [!DNL Flow Service]. |

Pour plus d’informations, consultez la [[!DNL PostgreSQL] documentation](https://www.postgresql.org/docs/current/) .

>[!ENDTABS]

### Authentification à Experience Platform sur Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).

Fournissez des valeurs pour les informations d’identification suivantes afin de connecter votre base de données [!DNL PostgreSQL] à Experience Platform sur AWS à l’aide de l’authentification de base.

| Informations d’identification | Description |
| --- | --- |
| `server` | Nom ou adresse IP de la base de données [!DNL PostgreSQL]. |
| `port` | Port TCP du serveur [!DNL PostgreSQL]. |
| `username` | Nom d’utilisateur associé à l’authentification de la base de données [!DNL PostgreSQL]. |
| `password` | Mot de passe associé à l’authentification de la base de données [!DNL PostgreSQL]. |
| `database` | Nom de la base de données [!DNL PostgreSQL] à laquelle vous souhaitez vous connecter. |
| `sslMode` | Valeur booléenne qui contrôle l’application ou non du protocole SSL, selon la prise en charge de votre serveur. Cette configuration est définie par défaut sur `false`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL PostgreSQL] est `74a1c565-4e59-48d7-9d67-7c03b8a13137`. Ces informations d’identification ne sont requises que lors de la connexion via l’API [!DNL Flow Service]. |

Pour plus d’informations, consultez la [[!DNL PostgreSQL] documentation](https://www.postgresql.org/docs/current/) .

## Connexion de [!DNL PostgreSQL] à Experience Platform à l’aide d’API

* [Créer une connexion de base [!DNL PostgreSQL] à l’aide de l’API Flow Service](../../tutorials/api/create/databases/postgres.md)
* [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
* [Créer un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

## Connexion d’[!DNL PostgreSQL] à Experience Platform à l’aide de l’interface utilisateur

* [Créer une connexion source  [!DNL PostgreSQL]  dans l’interface utilisateur](../../tutorials/ui/create/databases/postgres.md)
* [Créer un flux de données pour une connexion source de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)
