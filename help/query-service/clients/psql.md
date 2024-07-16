---
keywords: Experience Platform;accueil;rubriques les plus consultées;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: Connexion de PSQL à Query Service
description: PSQL est une interface de ligne de commande qui s’affiche lorsque vous installez PostgreSQL sur votre machine. Vous pouvez l’installer en suivant ces instructions.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 11%

---

# Connexion de PSQL à Query Service

PSQL est une interface de ligne de commande installée lorsque vous installez [!DNL PostgreSQL] sur votre machine. Ce document décrit les étapes de connexion de PSQL à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL PSQL] et que vous savez l&#39;utiliser. Vous trouverez plus d&#39;informations sur [!DNL PSQL] dans la [documentation officielle [!DNL PSQL] 3}.](https://www.postgresql.org/docs/current/app-psql.html)

Après avoir installé PSQL sur votre ordinateur, vous êtes prêt à connecter PSQL à Query Service. Revenez à l’interface utilisateur [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, suivie de **[!UICONTROL Credentials]**.

Sous la section **[!UICONTROL Commande PSQL]**, sélectionnez l’icône **[!UICONTROL Copier dans le presse-papiers]** (![Copier l’icône](../images/clients/psql/copy-icon.png)) pour copier la chaîne de commande.

![Onglet Informations d’identification du tableau de bord Requêtes avec l’icône de copie mise en surbrillance.](../images/clients/psql/connect-bi.png)

Collez la chaîne de commande dans une fenêtre de terminal ou de ligne de commande et appuyez sur **Entrée** sur votre clavier.

>[!IMPORTANT]
>
>Si vous utilisez un PC, utilisez un éditeur de texte pour supprimer les sauts de ligne dans la chaîne de commande, puis copiez la chaîne. Si vous utilisez la version 12.0 ou ultérieure, vous devrez ajouter `PGGSSENCMODE=disable` à votre chaîne de connexion. De plus, si vous utilisez des informations d’identification non arrivant à expiration, veillez à remplacer le champ du mot de passe par le mot de passe des informations d’identification non arrivant à expiration. Pour en savoir plus sur les informations d’identification non arrivant à expiration, consultez le [guide d’identification](../ui/credentials.md).

Vous devriez voir apparaître un résultat similaire à ceci :

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Si la version qui s’affiche est antérieure à la version 10.5, vous devez télécharger cette version ou une version plus récente.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser PSQL pour écrire des requêtes. Pour plus d’informations sur la façon d’écrire et d’exécuter des requêtes, consultez le guide sur l’ [exécution de requêtes](../best-practices/writing-queries.md).
