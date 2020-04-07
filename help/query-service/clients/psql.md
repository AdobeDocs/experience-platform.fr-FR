---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connexion à PSQL
topic: connect
translation-type: tm+mt
source-git-commit: f5bc9beb59e83b0411d98d901d5055122a124d07

---


# Connexion à PSQL

PSQL est une interface de ligne de commande qui vient lorsque vous installez Postgres sur votre machine. Vous pouvez l’installer en suivant ces instructions.

## Installation de postgres sur un Mac

Ouvrez une fenêtre de terminal et exécutez les trois commandes suivantes :

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
brew install postgres
```

```shell
which psql
```

Après avoir exécuté ces commandes, vous devriez voir ce qui suit :

```shell
/usr/local/bin/psql
```

## Installation de postgres sur un ordinateur

Téléchargez et installez Postgres à partir de cet [emplacement](https://www.postgresql.org/download/windows/).

Modifiez votre variable de chemin d’accès :

![Image](../images/clients/psql/path.png)

Ajouter les deux lignes affichées qui incluent &quot;Postgres&quot;.

Enregistrez vos mises à jour, puis ouvrez une invite de commande et saisissez :

```shell
psql -V
```

Vous devriez voir quelque chose comme ceci :

```shell
psql (PostgreSQL) 9.5.14
```

## Connect PSQL et service de 

Revenez à l’interface utilisateur de la plate-forme sur la page &quot;Connect BI Tools&quot;.

Cliquez sur **Copier** pour &quot;Commande PSQL&quot;.

![Image](../images/clients/psql/connect-bi.png)

>[!IMPORTANT]: Si vous êtes sur un PC, utilisez un éditeur de texte pour supprimer les sauts de ligne dans la chaîne de commande, puis copiez la chaîne.

Collez la chaîne de commande dans un terminal ou une fenêtre de commande et appuyez sur Entrée.

Vous devriez voir un résultat comme suit :

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Si vous ne voyez pas au moins la version 10.5, vous devez télécharger cette version ou une version plus récente.