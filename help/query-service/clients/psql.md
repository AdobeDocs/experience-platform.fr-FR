---
keywords: Experience Platform;home;popular topics;PSQL;psql
solution: Experience Platform
title: Connexion à PSQL
topic: connect
description: 'PSQL est une interface de ligne de commande qui apparaît lorsque vous installez Postgres sur votre machine. Vous pouvez l’installer en suivant ces instructions. '
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 63%

---


# Connexion à PSQL

PSQL is a command-line interface that comes when you install [!DNL Postgres] on your machine. Vous pouvez l’installer en suivant ces instructions.

## Installation de Postgres sur Mac

Ouvrez une fenêtre de terminal et lancez les trois commandes suivantes :

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
brew install postgres
```

```shell
which psql
```

Une fois ces commandes lancées, les éléments suivants devraient apparaître :

```shell
/usr/local/bin/psql
```

## Install [!DNL Postgres] on a PC

Download and install [!DNL Postgres] from this [location](https://www.postgresql.org/download/windows/).

Modifiez votre variable de chemin d’accès :

![Image](../images/clients/psql/path.png)

Add the two lines shown that include &quot;[!DNL Postgres].&quot;

Enregistrez les mises à jour, puis ouvrez une invite de commande et saisissez :

```shell
psql -V
```

Vous devriez voir apparaître une ligne similaire à ceci :

```shell
psql (PostgreSQL) 9.5.14
```

## Connect PSQL and [!DNL Query Service]

Return to the [!DNL Platform] UI on the **[!UICONTROL Connect BI Tools]** page.

Click **[!UICONTROL copy]** for **[!UICONTROL PSQL Command]**.

![Image](../images/clients/psql/connect-bi.png)

>[!IMPORTANT]
>
>Si vous êtes sur un PC, utilisez un éditeur de texte pour supprimer les sauts de ligne dans la chaîne de commande, puis copiez la chaîne.

Collez la chaîne de commande dans une fenêtre de terminal ou de commande et appuyez sur Entrée.

Vous devriez voir apparaître un résultat similaire à ceci :

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Si la version qui s’affiche est antérieure à la version 10.5, vous devez télécharger cette version ou une version plus récente.