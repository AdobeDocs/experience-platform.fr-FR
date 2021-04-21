---
keywords: Experience Platform ; accueil ; rubriques populaires ; PSQL ; psqlconnect to requête service ; Requête service ; requête service ;
solution: Experience Platform
title: Connecter PSQL à Requête Service
topic-legacy: connect
description: PSQL est une interface de ligne de commande qui vient lorsque vous installez PostgreSQL sur votre machine. Vous pouvez l’installer en suivant ces instructions.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 13%

---

# Connecter PSQL à Requête Service

PSQL est une interface de ligne de commande qui s&#39;installe lorsque vous installez [!DNL PostgreSQL] sur votre machine. Ce document décrit les étapes de connexion de PSQL à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL PSQL] et que vous savez comment l&#39;utiliser. Pour plus d&#39;informations sur [!DNL PSQL], consultez la [documentation officielle [!DNL PSQL]] (https://www.postgresql.org/docs/current/app-psql.html).

Après avoir installé PSQL sur votre ordinateur, vous êtes prêt à connecter PSQL à Requête Service. Revenez à l&#39;interface utilisateur [!DNL Platform], puis sélectionnez **[!UICONTROL Requêtes]**, puis **[!UICONTROL Informations d&#39;identification]**.

![Image](../images/clients/psql/connect-bi.png)

Sélectionnez l&#39;icône pour copier la section intitulée **[!UICONTROL Commande PSQL]**, puis collez la chaîne de commande dans un terminal ou une fenêtre de ligne de commande avant d&#39;appuyer sur Entrée.

>[!IMPORTANT]
>
>Si vous êtes sur un PC, utilisez un éditeur de texte pour supprimer les sauts de ligne dans la chaîne de commande, puis copiez la chaîne. De plus, si vous utilisez la version 12.0 ou supérieure, vous devrez ajouter `PGGSSENCMODE=disable` à votre chaîne de connexion.

Vous devriez voir apparaître un résultat similaire à ceci :

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Si la version qui s’affiche est antérieure à la version 10.5, vous devez télécharger cette version ou une version plus récente.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser PSQL pour écrire des requêtes. Pour plus d&#39;informations sur la façon d&#39;écrire et d&#39;exécuter des requêtes, veuillez lire le guide sur les [requêtes en cours d&#39;exécution](../best-practices/writing-queries.md).
