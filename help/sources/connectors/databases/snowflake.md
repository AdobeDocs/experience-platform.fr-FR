---
title: Présentation du connecteur Source de Snowflake
description: Découvrez comment connecter Snowflake à Adobe Experience Platform à l’aide d’API ou de l’interface utilisateur.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 687363ab664e43cc854b535760dfbfc55acefd2c
workflow-type: tm+mt
source-wordcount: '1570'
ht-degree: 3%

---

# Source [!DNL Snowflake]

>[!IMPORTANT]
>
>* La source [!DNL Snowflake] est disponible dans le catalogue des sources pour les utilisateurs qui ont acheté Real-Time Customer Data Platform Ultimate.
>* Par défaut, la source de [!DNL Snowflake] interprète `null` comme une chaîne vide. Contactez votre représentant Adobe pour vous assurer que vos valeurs `null` sont correctement écrites comme `null` dans Adobe Experience Platform.
>* Pour qu’Experience Platform ingère des données, les fuseaux horaires de toutes les sources de lots basées sur un tableau doivent être configurés au format UTC. Le seul horodatage pris en charge pour la source [!DNL Snowflake] est TIMESTAMP_NTZ avec l’heure UTC.

[!DNL Snowflake] est une plateforme d’entrepôt de données cloud conçue pour permettre aux entreprises de stocker, de traiter et d’analyser efficacement de grands volumes de données. Conçu pour tirer parti de l’évolutivité et de la flexibilité du cloud, [!DNL Snowflake] prend en charge l’intégration des données, les analyses avancées et le partage transparent entre les équipes. En tant que service entièrement géré, [!DNL Snowflake] élimine la complexité de maintenance commune aux bases de données traditionnelles, ce qui vous permet de vous concentrer sur l’obtention d’informations et de valeur à partir de vos données.

Vous pouvez utiliser la source de [!DNL Snowflake] pour vous connecter et importer vos données de [!DNL Snowflake] vers Adobe Experience Platform. Lisez la documentation ci-dessous pour savoir comment configurer votre source [!DNL Snowflake] et vous connecter à Experience Platform.

## Conditions préalables {#prerequisites}

Cette section décrit les tâches de configuration que vous devez effectuer avant de connecter votre source [!DNL Snowflake] à Experience Platform.

### Liste autorisée d’adresses IP

Vous devez ajouter à votre place sur la liste autorisée des adresses IP spécifiques à une région avant de connecter vos sources à Experience Platform. Placer sur la liste autorisée Pour plus d’informations, consultez le guide sur la [connexion des adresses IP à Experience Platform](../../ip-address-allow-list.md).

### Collecter les informations d’identification requises

Vous devez fournir des valeurs pour les propriétés d’identification suivantes afin d’authentifier votre source [!DNL Snowflake].

>[!BEGINTABS]

>[!TAB Authentification par clé de compte (Azure)]

Fournissez des valeurs pour les informations d’identification suivantes pour connecter [!DNL Snowflake] à Experience Platform sur Azure à l’aide de l’authentification par clé de compte.

| Informations d’identification | Description |
| ---------- | ----------- |
| `account` | Un nom de compte identifie de manière unique un compte de votre organisation. Dans ce cas, vous devez identifier de manière unique un compte dans différentes organisations [!DNL Snowflake]. Pour ce faire, vous devez ajouter le nom de votre organisation au nom du compte. Par exemple : `myorg-myaccount.snowflakecomputing.com`. Lisez la section sur la [récupération de l’identifiant  [!DNL Snowflake]  compte](#retrieve-your-account-identifier) pour plus d’informations. Pour plus d’informations, consultez la [[!DNL Snowflake] documentation](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `warehouse` | L’entrepôt de [!DNL Snowflake] gère le processus d’exécution de la requête pour l’application. Chaque entrepôt de [!DNL Snowflake] est indépendant les uns des autres et doit être accessible individuellement lors de l’importation de données dans Experience Platform. |
| `database` | La base de données [!DNL Snowflake] contient les données que vous souhaitez importer dans Experience Platform. |
| `username` | Nom d’utilisateur du compte [!DNL Snowflake]. |
| `password` | Mot de passe du compte utilisateur [!DNL Snowflake]. |
| `role` | Rôle de contrôle d’accès par défaut à utiliser dans la session [!DNL Snowflake]. Le rôle doit être un rôle existant qui a déjà été attribué à l’utilisateur spécifié. Le rôle par défaut est `PUBLIC`. |
| `connectionString` | Chaîne de connexion utilisée pour la connexion à votre instance [!DNL Snowflake]. Le modèle de chaîne de connexion pour [!DNL Snowflake] est `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |

>[!TAB Authentification par paire de clés (Azure)]

Pour utiliser l’authentification par paire de clés, générez d’abord une paire de clés RSA 2 048 bits. Indiquez ensuite les valeurs des informations d’identification suivantes pour vous connecter à Experience Platform sur Azure à l’aide de l’authentification par paire de clés.

| Informations d’identification | Description |
| --- | --- |
| `account` | Un nom de compte identifie de manière unique un compte de votre organisation. Dans ce cas, vous devez identifier de manière unique un compte dans différentes organisations [!DNL Snowflake]. Pour ce faire, vous devez ajouter le nom de votre organisation au nom du compte. Par exemple : `myorg-myaccount.snowflakecomputing.com`. Lisez la section sur la [récupération de l’identifiant  [!DNL Snowflake]  compte](#retrieve-your-account-identifier) pour plus d’informations. Pour plus d’informations, consultez la [[!DNL Snowflake] documentation](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Nom d’utilisateur de votre compte [!DNL Snowflake]. |
| `privateKey` | Clé privée [!DNL Base64-]encodée) de votre compte [!DNL Snowflake]. Vous pouvez générer des clés privées chiffrées ou non chiffrées. Si vous utilisez une clé privée chiffrée, vous devez également fournir une phrase secrète de clé privée lors de l’authentification auprès d’Experience Platform. Pour plus d’informations, consultez la section relative à la [récupération de votre clé privée](#retrieve-your-private-key). |
| `privateKeyPassphrase` | La phrase secrète de la clé privée est une couche de sécurité supplémentaire que vous devez utiliser lors de l’authentification avec une clé privée chiffrée. Vous n’êtes pas tenu de fournir la phrase secrète si vous utilisez une clé privée non chiffrée. |
| `port` | Numéro de port utilisé par [!DNL Snowflake] lors de la connexion à un serveur via Internet. |
| `database` | Base de données [!DNL Snowflake] contenant les données à ingérer dans Experience Platform. |
| `warehouse` | L’entrepôt de [!DNL Snowflake] gère le processus d’exécution de la requête pour l’application. Chaque entrepôt de [!DNL Snowflake] est indépendant les uns des autres et doit être accessible individuellement lors de l’importation de données dans Experience Platform. |

Pour plus d’informations sur ces valeurs, consultez le [[!DNL Snowflake] guide d’authentification par paire de clés](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!TAB Authentification de base (AWS)]

Fournissez des valeurs pour les informations d’identification suivantes pour connecter [!DNL Snowflake] à Experience Platform sur AWS à l’aide de l’authentification de base.

>[!WARNING]
>
>L’authentification de base (ou authentification par clé de compte) de la source [!DNL Snowflake] sera abandonnée en novembre 2025. Vous devez passer à l’authentification par paire de clés pour continuer à utiliser la source et à ingérer des données de votre base de données vers Experience Platform. Pour plus d’informations sur l’obsolescence, consultez le [[!DNL Snowflake] guide des bonnes pratiques sur la réduction des risques liés à la compromission des informations d’identification](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

| Informations d’identification | Description |
| --- | --- |
| `host` | URL hôte à laquelle votre compte [!DNL Snowflake] se connecte. |
| `port` | Numéro de port utilisé par [!DNL Snowflake] lors de la connexion à un serveur via Internet. |
| `username` | Nom d’utilisateur associé à votre compte [!DNL Snowflake]. |
| `password` | Mot de passe associé à votre compte [!DNL Snowflake]. |
| `database` | Base de données [!DNL Snowflake] à partir de laquelle les données seront extraites. |
| `schema` | Nom du schéma associé à votre base de données [!DNL Snowflake]. Vous devez vous assurer que l’utilisateur auquel vous souhaitez accorder l’accès à la base de données a également accès à ce schéma. |
| `warehouse` | Entrepôt de [!DNL Snowflake] utilisé. |

>[!TAB Authentification par paire de clés (AWS)]

Pour utiliser l’authentification par paire de clés, générez d’abord une paire de clés RSA 2 048 bits. Indiquez ensuite les valeurs des informations d’identification suivantes pour vous connecter à Experience Platform sur AWS à l’aide de l’authentification par paire de clés.

| Informations d’identification | Description |
| --- | --- |
| `account` | Un nom de compte identifie de manière unique un compte de votre organisation. Dans ce cas, vous devez identifier de manière unique un compte dans différentes organisations [!DNL Snowflake]. Pour ce faire, vous devez ajouter le nom de votre organisation au nom du compte. Par exemple : `http://myorg-myaccount.snowflakecomputing.com/`. Lisez le guide sur la [récupération de l’identifiant  [!DNL Snowflake]  compte](#etrieve-your-account-identifier) pour obtenir des conseils supplémentaires. Pour plus d’informations, consultez la [[!DNL Snowflake] documentation](https://docs.snowflake.com/en/user-guide/admin-account-identifier#format-1-preferred-account-name-in-your-organization). |
| `username` | Nom d’utilisateur de votre compte [!DNL Snowflake]. |
| `privateKey` | Clé privée de votre utilisateur [!DNL Snowflake], codée en base64 sur une seule ligne, sans en-têtes ni sauts de ligne. Pour le préparer, copiez le contenu de votre fichier PEM, supprimez les lignes `BEGIN`/`END` et tous les sauts de ligne, puis codez le résultat en base64. Pour plus d’informations, consultez la section relative à la [récupération de votre clé privée](#retrieve-your-private-key). **Remarque :** les clés privées chiffrées ne sont actuellement pas prises en charge pour une connexion AWS. |
| `port` | Numéro de port utilisé par [!DNL Snowflake] lors de la connexion à un serveur via Internet. |
| `database` | Base de données [!DNL Snowflake] contenant les données à ingérer dans Experience Platform. |
| `warehouse` | L’entrepôt de [!DNL Snowflake] gère le processus d’exécution de la requête pour l’application. Chaque entrepôt de [!DNL Snowflake] est indépendant les uns des autres et doit être accessible individuellement lors de l’importation de données dans Experience Platform. |

Pour plus d’informations sur ces valeurs, consultez le [[!DNL Snowflake] guide d’authentification par paire de clés](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

>[!ENDTABS]

### Récupérer l’identifiant de votre compte {#retrieve-your-account-identifier}

Vous devez récupérer l’identifiant de votre compte depuis le tableau de bord de l’interface utilisateur [!DNL Snowflake], car vous l’utiliserez pour authentifier votre instance [!DNL Snowflake] sur Experience Platform.

Pour récupérer l’identifiant de votre compte :

* Utilisez le tableau de bord [[!DNL Snowflake] interface utilisateur de l’application](https://app.snowflake.com/) pour accéder à votre compte.
* Dans le volet de navigation de gauche, sélectionnez **[!DNL Accounts]** , puis **[!DNL Active Accounts]** dans l’en-tête.
* Sélectionnez ensuite l’icône d’information, puis sélectionnez et copiez le nom de domaine de l’URL active.

![Tableau de bord de l’interface utilisateur de Snowflake avec le nom de domaine sélectionné.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Générer votre paire de clés RSA

Utilisez OpenSSL dans l’interface de ligne de commande pour générer une paire de clés RSA 2 048 bits au format PKCS#8. Il est recommandé de créer une clé privée chiffrée à des fins de sécurité, qui nécessitera une phrase secrète.

>[!BEGINTABS]

>[!TAB Générer une clé privée chiffrée]

Pour générer votre clé privée [!DNL Snowflake] chiffrée, exécutez la commande suivante sur votre terminal :

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8# You will be prompted to enter a passphrase. Store this securely!
```

>[!TAB Générer une clé privée non chiffrée]

Pour générer votre clé privée [!DNL Snowflake] non chiffrée, exécutez la commande suivante sur votre terminal :

```bash
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

>[!ENDTABS]

### Générer une clé publique à partir de votre clé privée

Exécutez ensuite la commande suivante dans votre interface de ligne de commande pour créer une clé publique basée sur votre clé privée.

```bash
openssl rsa -in rsa_key.p8 -pubout -out rsa_key.pub# You will be prompted to enter the passphrase if the private key is encrypted.
```

### Attribuer la clé publique à l’utilisateur [!DNL Snowflake]

Vous devez utiliser un rôle d’administrateur [!DNL Snowflake] (tel que **SECURITYADMIN**) pour associer la clé publique générée à l’utilisateur du service [!DNL Snowflake] qu’Experience Platform utilisera. Pour récupérer le contenu de la clé publique, ouvrez le fichier `rsa_key.pub` et copiez le contenu entier, à l’exception des lignes `-----BEGIN PUBLIC KEY----- and -----END PUBLIC KEY-----`. Exécutez ensuite le code SQL suivant dans [!DNL Snowflake] :

```sql
ALTER USER {YOUR_SNOWFLAKE_USERNAME}>SET RSA_PUBLIC_KEY='{PUBLIC_KEY_CONTENT}';
```

### Encoder la clé privée en [!DNL Base64]

Experience Platform nécessite que la clé privée soit codée en [!DNL Base64] et fournie sous la forme d’une chaîne lors de la configuration de la connexion. Utilisez un outil ou un script approprié pour coder le contenu du fichier `rsa_key.p8` en une seule chaîne [!DNL Base64].

>[!TIP]
>
>Assurez-vous qu’il n’y a pas d’espaces ou de sauts de ligne supplémentaires, y compris les lignes d’en-tête/de pied de page `(-----BEGIN ENCRYPTED PRIVATE KEY----- and -----END ENCRYPTED PRIVATE KEY-----)`, avant ou après le processus de codage, car cela peut entraîner des erreurs d’authentification.

### Vérifier les configurations

Avant de créer la connexion source [!DNL Snowflake] dans Experience Platform, vous devez vous assurer que l’**[!DNL Default Role]** et la **[!DNL Default Warehouse]** de l’utilisateur correspondent aux valeurs que vous fournissez dans Experience Platform. Vous pouvez vérifier ces paramètres dans l’interface utilisateur de [!DNL Snowflake] à l’aide de la commande SQL `DESCRIBE USER {USERNAME}`.

Vous pouvez également suivre les étapes ci-dessous pour vérifier vos paramètres :

* Sélectionnez **[!DNL Admin]** dans le volet de navigation de gauche, puis sélectionnez **[!DNL Users & Roles]**.
* Sélectionnez l’utilisateur approprié, puis sélectionnez les points de suspension (`...`) dans le coin supérieur droit.
* Dans la fenêtre de [!DNL Edit user] qui s’affiche, accédez à [!DNL Default Role] pour afficher le rôle associé à l’utilisateur donné.
* Dans la même fenêtre, accédez à [!DNL Default Warehouse] pour afficher l&#39;entrepôt associé à l&#39;utilisateur donné.

![Interface utilisateur de Snowflake dans laquelle vous pouvez vérifier votre rôle et votre entrepôt de données.](../../images/tutorials/create/snowflake/snowflake-configs.png)

## Étapes suivantes

Une fois la configuration terminée, vous pouvez procéder à la connexion de votre compte [!DNL Snowflake] à Experience Platform. Pour plus d’informations, consultez la documentation suivante :

### Connexion de [!DNL Snowflake] à Experience Platform à l’aide d’API

* [Connexion  [!DNL Snowflake]  Experience Platform à l’aide de l’API](../../tutorials/api/create/databases/snowflake.md)
* [Explorer des tableaux de données à l’aide de l’API Flow Service](../../tutorials/api/explore/tabular.md)
* [Créer un flux de données pour une source de base de données à l’aide de l’API Flow Service](../../tutorials/api/collect/database-nosql.md)

### Connexion d’[!DNL Snowflake] à Experience Platform à l’aide de l’interface utilisateur

* [Connexion  [!DNL Snowflake]  Experience Platform à l’aide de l’interface utilisateur](../../tutorials/ui/create/databases/snowflake.md)
* [Créer un flux de données pour une connexion source de base de données dans l’interface utilisateur](../../tutorials/ui/dataflow/databases.md)
