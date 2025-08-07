---
title: Présentation du connecteur Source de la base de données Oracle
description: Découvrez comment connecter Oracle à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
last-substantial-update: 2025-08-06T00:00:00Z
exl-id: be422cf8-fb24-48c7-8369-34f0f2ec95fc
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 8%

---

# [!DNL Oracle DB]

[!DNL Oracle DB] est un puissant système de gestion de base de données relationnelle développé par [!DNL Oracle Corporation]. Vous pouvez utiliser [!DNL Oracle DB] pour stocker, gérer et récupérer de grands volumes de données structurées de manière efficace et sécurisée.

Utilisez la source [!DNL Oracle DB] dans le catalogue des sources Adobe Experience Platform pour connecter votre base de données et ingérer des données dans Experience Platform.

## Conditions préalables {#prerequisites}

Lisez les sections suivantes pour terminer la configuration requise avant de connecter votre compte [!DNL Oracle DB] à Experience Platform.

### Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform sur Azure ou Amazon Web Services (AWS). Pour plus d’informations, consultez le guide sur la [liste autorisée des adresses IP pour se connecter à Experience Platform sur Azure et AWS](../../ip-address-allow-list.md).

### S’authentifier auprès d’Experience Platform sur Azure {#azure}

Fournissez une chaîne de connexion pour authentifier et connecter votre compte [!DNL Oracle DB] à Experience Platform sur Azure.

| Informations d’identification | Description |
| --- | --- |
| Chaîne de connexion | Une chaîne de connexion est une chaîne de texte utilisée par les applications pour se connecter à une base de données. Le modèle de chaîne de connexion [!DNL Oracle DB] est : `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| Identifiant de spécification de connexion | L’identifiant de spécification de connexion renvoie les propriétés de connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Oracle] est `d6b52d86-f0f8-475f-89d4-ce54c8527328`. **Remarque** : ces informations d’identification ne sont requises que lors de la connexion via l’API [!DNL Flow Service]. |

### Authentification à Experience Platform sur Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Cette section s’applique aux implémentations d’Experience Platform s’exécutant sur Amazon Web Services (AWS). Experience Platform s’exécutant sur AWS est actuellement disponible pour un nombre limité de clients. Pour en savoir plus sur l’infrastructure Experience Platform prise en charge, consultez la [présentation multi-cloud d’Experience Platform](../../../landing/multi-cloud.md).

Fournissez des valeurs pour les informations d’identification suivantes afin d’authentifier et de connecter votre compte [!DNL Oracle DB] à Experience Platform sur AWS.

| Informations d’identification | Description |
| --- | --- |
| Serveur | L’adresse IP ou le nom d’hôte de votre serveur [!DNL Oracle DB]. |
| Port | Numéro de port du serveur de base de données. Le numéro de port par défaut est `1521`. |
| Nom d’utilisateur | Compte utilisateur [!DNL Oracle DB] utilisé pour authentifier et accéder à la base de données. |
| Mot de passe | Clé secrète associée à votre nom d’utilisateur, utilisée pour l’authentification. |
| Base de données | Instance de base de données [!DNL Oracle] spécifique à laquelle vous souhaitez vous connecter. |
| Schéma | Conteneur des objets de base de données, tels que les tables, les vues ou les procédures. |
| Mode SSL | Valeur booléenne qui contrôle si le protocole SSL est appliqué ou non. Cette configuration dépend de la prise en charge de votre serveur et est définie par défaut sur `false`. |
| Identifiant de spécification de connexion | L’identifiant de spécification de connexion renvoie les propriétés de connecteur d’une source, y compris les spécifications d’authentification liées à la création des connexions de base et source. L’identifiant de spécification de connexion pour [!DNL Oracle] est `d6b52d86-f0f8-475f-89d4-ce54c8527328`. **Remarque** : ces informations d’identification ne sont requises que lors de la connexion via l’API [!DNL Flow Service]. |


## Connecter [!DNL Oracle] à [!DNL Experience Platform] à lʼaide dʼAPI

- [Connecter la base de données Oracle à l’aide de l’API Flow Service](../../tutorials/api/create/databases/oracle.md)
- [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
- [Créer un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

## Connecter [!DNL Oracle] à [!DNL Experience Platform] à lʼaide de l’interface utilisateur

- [Connectez la base de données Oracle à l’aide de l’espace de travail de l’interface utilisateur Experience Platform.](../../tutorials/ui/create/databases/oracle.md)
- [Créer un flux de données pour une connexion source de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)
