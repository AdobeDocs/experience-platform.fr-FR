---
title: Présentation du connecteur Source MariaDB
description: Découvrez comment connecter MariaDB à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
last-substantial-update: 2025-04-29T00:00:00.000Z
exl-id: 37b8f991-dca9-4f85-9bdd-4927a015e4c0
TQID: https://experienceleague.adobe.com/cgQAa-boyziU0EYaaAFJkNCpEXiZGmdQAbIHPoaF1Ps
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 437
ht-degree: 25%

---

# [!DNL MariaDB]

Adobe Experience Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services [!DNL Experience Platform]. Vous pouvez ingérer des données provenant de diverses sources telles que les applications Adobe, le stockage dans le cloud, les bases de données, etc.

Experience Platform prend en charge l’ingestion de données provenant d’une base de données tierce. [!DNL Experience Platform] pouvez vous connecter à différents types de bases de données, telles que Relational, NoSQL ou Data Warehouse. La prise en charge des fournisseurs de base de données inclut [!DNL MariaDB].

## Conditions préalables {#prerequisites}

Lisez les sections suivantes pour terminer la configuration requise avant de connecter votre compte [!DNL MariaDB] à Experience Platform.

### Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform. Pour plus d’informations, consultez le guide sur la [connexion des adresses IP à &#x200B;](../../ip-address-allow-list.md).

### S’authentifier auprès d’Experience Platform

Vous devez fournir des valeurs pour les informations d’identification suivantes afin de [!DNL MariaDB] connecter à Experience Platform.

>[!BEGINTABS]

>[!TAB Authentification de la clé de compte]

Pour utiliser l’authentification par clé de compte, saisissez les valeurs appropriées pour les informations d’identification suivantes.

| Informations d’identification | Description |
| --- | --- |
| `connectionString` | Chaîne de connexion associée à votre authentification [!DNL MariaDB]. Le modèle de chaîne de connexion [!DNL MariaDB] est : `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL MariaDB] est `3000eb99-cd47-43f3-827c-43caf170f015`. **Remarque** : ces informations d’identification ne sont requises que lors de la connexion via l’API [!DNL Flow Service]. |

Pour plus d’informations sur l’obtention d’une chaîne de connexion, reportez-vous à ce [[!DNL MariaDB] document](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!TAB  Authentification de base ]

Pour utiliser l’authentification de base, saisissez les valeurs appropriées pour les informations d’identification suivantes.

| Informations d’identification | Description |
| --- | --- |
| `server` | Nom ou adresse IP de la base de données [!DNL MariaDB]. |
| `username` | Nom de la base de données. |
| `port` | Numéro de port du point d’entrée de communication auquel vous vous connectez. |
| `password` | Nom d’utilisateur correspondant à votre base de données. |
| `database` | Mot de passe correspondant à votre base de données. |
| `sslMode` | Méthode de chiffrement des données lors du transfert de données. |
| `connectionSpec.id` | La spécification de connexion renvoie les propriétés du connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL MariaDB] est `3000eb99-cd47-43f3-827c-43caf170f015`. **Remarque** : ces informations d’identification ne sont requises que lors de la connexion via l’API [!DNL Flow Service]. |

Pour plus d’informations sur l’obtention d’une chaîne de connexion, reportez-vous à ce [[!DNL MariaDB] document](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

>[!ENDTABS]

## Connexion de [!DNL MariaDB] à Experience Platform à l’aide d’API

- [Créer une connexion de base MariaDB à l’aide de l’API Flow Service](../../tutorials/api/create/databases/mariadb.md)
- [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Créer un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

## Connexion d’[!DNL MariaDB] à Experience Platform à l’aide de l’interface utilisateur

- [Créer une connexion source MariaDB dans l’interface utilisateur](../../tutorials/ui/create/databases/mariadb.md)
- [Créer un flux de données pour une connexion source de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)
