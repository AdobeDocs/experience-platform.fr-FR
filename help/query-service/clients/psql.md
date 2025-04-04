---
keywords: Experience Platform;accueil;rubriques les plus consultées;PSQL;psqlconnect à query service;Query service;query service;
solution: Experience Platform
title: Connecter PSQL à Query Service
description: PSQL est une interface de ligne de commande qui s’affiche lorsque vous installez PostgreSQL sur votre ordinateur. Vous pouvez l’installer en suivant ces instructions.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 11%

---

# Connecter PSQL à Query Service

PSQL est une interface de ligne de commande qui est installée lorsque vous installez [!DNL PostgreSQL] sur votre ordinateur. Ce document décrit les étapes à suivre pour connecter PSQL à Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Ce guide suppose que vous avez déjà accès à [!DNL PSQL] et que vous savez comment l’utiliser. Vous trouverez plus d’informations sur les [!DNL PSQL] dans la [documentation [!DNL PSQL] officielle](https://www.postgresql.org/docs/current/app-psql.html).

Après avoir installé PSQL sur votre ordinateur, vous êtes prêt à connecter PSQL à Query Service. Revenez à l’interface utilisateur d’[!DNL Experience Platform], puis sélectionnez **[!UICONTROL Requêtes]** et **[!UICONTROL Informations d’identification]**.

Sous la section **[!UICONTROL Commande PSQL]**, sélectionnez l’icône **[!UICONTROL Copier dans le presse-papiers]** (![Icône Copier](/help/images/icons/copy.png)) pour copier la chaîne de commande.

![Onglet Informations d’identification du tableau de bord Requêtes avec l’icône de copie mise en surbrillance.](../images/clients/psql/connect-bi.png)

Collez la chaîne de commande dans un terminal ou une fenêtre de ligne de commande et appuyez sur **Entrée** sur le clavier.

>[!IMPORTANT]
>
>Si vous êtes sur un PC, utilisez un éditeur de texte pour supprimer les sauts de ligne dans la chaîne de commande, puis copiez la chaîne. Si vous utilisez la version 12.0 ou une version ultérieure, vous devez ajouter `PGGSSENCMODE=disable` à votre chaîne de connexion. En outre, si vous utilisez des informations d’identification non expirantes, veillez à remplacer le champ du mot de passe par le mot de passe des informations d’identification non expirantes. Pour en savoir plus sur les informations d’identification non expirantes, consultez le [guide des informations d’identification](../ui/credentials.md).

Vous devriez voir apparaître un résultat similaire à ceci :

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Si la version qui s’affiche est antérieure à la version 10.5, vous devez télécharger cette version ou une version plus récente.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL Query Service], vous pouvez utiliser PSQL pour écrire des requêtes. Pour plus d’informations sur l’écriture et l’exécution de requêtes, consultez le guide sur l’[exécution de requêtes](../best-practices/writing-queries.md).
