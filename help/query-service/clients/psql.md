---
keywords: Experience Platform;accueil;rubriques les plus consultées;PSQL;psqlconnect à query service;Query service;query service;
solution: Experience Platform
title: Connecter PSQL à Query Service
description: Découvrez comment connecter le client PSQL à Adobe Experience Platform Query Service, y compris les versions de PostgreSQL prises en charge et les instructions de configuration.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: f75ea97e8631984dcd1d4a7f8aff3c10cba7b11f
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 2%

---

# Connecter PSQL à Query Service

PSQL est une interface de ligne de commande installée avec PostgreSQL sur votre ordinateur. Ce document décrit les étapes à suivre pour connecter PSQL à Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>Query Service prend uniquement en charge la connexion avec PSQL version 14.x. Les versions antérieures à 14.x (telles que 10.x à 13.x) et les versions ultérieures (15.x et ultérieures) ne sont pas officiellement prises en charge. Assurez-vous d’avoir installé une version cliente compatible. Pour référence, reportez-vous à la section [ Dates de fin de vie de PostgreSQL ](https://endoflife.date/postgresql).

Avant de commencer, vérifiez que vous avez accès à PSQL et que vous connaissez les bases de l’utilisation du client. Vous trouverez plus d’informations sur PSQL dans la [documentation officielle de PSQL](https://www.postgresql.org/docs/current/app-psql.html).

>[!IMPORTANT]
>
>Lors du téléchargement de PostgreSQL, veillez à sélectionner la version 14.x. Par défaut, le site web PostgreSQL propose la dernière version, qui peut ne pas être compatible avec Query Service.

Une fois PSQL installé, vous pouvez le connecter à Query Service. Revenez à l’interface utilisateur d’Experience Platform, puis sélectionnez **[!UICONTROL Requêtes]** et **[!UICONTROL Informations d’identification]**.

Sous la section **[!UICONTROL Commande PSQL]**, sélectionnez l’icône **[!UICONTROL Copier dans le presse-papiers]** (![Icône Copier](/help/images/icons/copy.png)) pour copier la chaîne de commande.

![Onglet Informations d’identification du tableau de bord Requêtes avec l’icône de copie mise en surbrillance.](../images/clients/psql/copy-credentials.png)

Collez la chaîne de commande dans votre terminal et appuyez sur **Entrée** sur votre clavier.

>[!IMPORTANT]
>
>Si vous êtes sur un PC, utilisez un éditeur de texte pour supprimer les sauts de ligne dans la chaîne de commande, puis copiez la chaîne. Si vous utilisez la version 12.0 ou une version ultérieure, vous devez ajouter `PGGSSENCMODE=disable` à votre chaîne de connexion. Ce paramètre désactive le chiffrement GSSAPI, qui est inutile pour les connexions à Query Service et peut entraîner des erreurs de connexion.<br>En outre, si vous utilisez des informations d’identification non expirantes, veillez à remplacer le champ du mot de passe par le mot de passe des informations d’identification non expirantes. Pour en savoir plus sur les informations d’identification non expirantes, consultez le [guide des informations d’identification](../ui/credentials.md).

Vous devriez voir apparaître un résultat similaire à ceci :

```shell
psql (14.4, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Si vous ne voyez pas la version 14.x, téléchargez et installez une version 14.x prise en charge de PSQL depuis la page [ Téléchargements officiels PostgreSQL ](https://www.postgresql.org/download/).

>[!NOTE]
>
>Suivez les instructions d’installation de votre système d’exploitation, puis vérifiez la version PSQL installée en exécutant `psql --version` dans votre terminal.

## Étapes suivantes

Maintenant que vous êtes connecté à Query Service, vous pouvez utiliser PSQL pour écrire des requêtes. Pour plus d’informations, consultez le guide sur l’[exécution de requêtes](../best-practices/writing-queries.md).
