---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;Query Service;Db Visualizer;DbVisualizer;db Visulaizer;se connecter au service de requête;
solution: Experience Platform
title: Connexion de DbVisualizer à Query Service
description: Ce document décrit les étapes à suivre pour connecter DbVisualizer à Adobe Experience Platform Query Service.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 5%

---

# Connectez [!DNL DbVisualizer] à [!DNL Query Service] {#connect-dbvisualizer}

Ce document décrit les étapes à suivre pour connecter l’outil de base de données [!DNL DbVisualizer] à Adobe Experience Platform [!DNL Query Service].

## Prise en main

Ce guide nécessite que vous ayez déjà accès à l’application [!DNL DbVisualizer] Desktop et que vous sachiez comment naviguer dans son interface. Pour télécharger l’appli de bureau [!DNL DbVisualizer] ou pour plus d’informations, consultez la [documentation officielle [!DNL DbVisualizer] 3}.](https://www.dbvis.com/download/)

Pour acquérir les informations d’identification nécessaires à la connexion de [!DNL  DbVisualizer] à Experience Platform, vous devez avoir accès à l’espace de travail Requêtes dans l’interface utilisateur de Platform. Contactez l’administrateur de votre organisation si vous n’avez pas actuellement accès à l’espace de travail Requêtes .

## Créer une connexion à une base de données {#connect-database}

Une fois que vous avez installé l’appli de bureau sur votre ordinateur local, suivez les instructions officielles de BDVisualizer pour [créer une connexion à la base de données](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

Une fois que vous avez sélectionné **[!DNL PostgreSQL]** dans la liste [!DNL Connections], un onglet [!DNL Object View] pour la nouvelle connexion [!DNL PostgreSQL] s’affiche.

### Définition des propriétés du pilote pour votre connexion {#properties}

Dans l’onglet [!DNL PostgreSQL] object view, sélectionnez l’onglet **[!DNL Properties]**, suivi de **[!DNL Driver Properties]** dans la barre latérale de navigation. Vous trouverez plus d’informations sur les [propriétés du pilote](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) dans la documentation officielle.

Saisissez ensuite les propriétés du pilote décrites dans le tableau ci-dessous.

>[!IMPORTANT]
>
>Pour connecter DBVisualizer à Adobe Experience Platform, vous devez activer l’utilisation de SSL. Consultez la [ documentation sur les modes SSL](./ssl-modes.md) pour en savoir plus sur la prise en charge du protocole SSL pour les connexions tierces à Adobe Experience Platform Query Service et sur la connexion à l’aide du mode SSL `verify-full`.

| Propriété | Description |
| ------ | ------ |
| `PGHOST` | Nom d’hôte du serveur [!DNL PostgreSQL]. Cette valeur est votre identifiant Experience Platform **[!UICONTROL Host] credential**. |
| `ssl` | Définissez la valeur SSL `1` pour activer l’utilisation de SSL. |
| `sslmode` | Cela contrôle le niveau de protection SSL. Il est recommandé d’utiliser le mode SSL `require` lors de la connexion de clients tiers à Adobe Experience Platform. Le mode `require` garantit que le cryptage est requis sur toutes les communications et que le réseau est approuvé pour se connecter au bon serveur. La validation du certificat SSL du serveur n’est pas requise. |
| `user` | Le nom d’utilisateur connecté à la base de données est votre ID d’organisation. Il s’agit d’une chaîne alphanumérique se terminant par `@Adobe.Org`. Cette valeur est votre identifiant Experience Platform **[!UICONTROL Username] credential**. |

Utilisez la barre de recherche pour rechercher chaque propriété, puis sélectionnez la cellule correspondante pour la valeur du paramètre. La cellule est mise en surbrillance en bleu. Saisissez vos informations d’identification Platform dans le champ de valeur et sélectionnez **[!DNL Apply]** pour ajouter la propriété driver.

>[!NOTE]
>
>Pour ajouter un second profil `user`, sélectionnez `user` dans la colonne des paramètres, puis sélectionnez l’icône bleue + (plus) pour ajouter les informations d’identification de chaque utilisateur. Sélectionnez **[!DNL Apply]** pour ajouter la propriété du pilote.

La colonne [!DNL Edited] affiche une coche indiquant que la valeur du paramètre a été mise à jour.

### Informations d’identification de Query Service {#query-service-credentials}

Pour trouver les informations d’identification nécessaires à la connexion de BBVisualizer à Query Service, connectez-vous à l’interface utilisateur de Platform et sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche, suivi de **[!UICONTROL Credentials]**. Pour plus d&#39;informations sur la recherche de vos **identifiants**, **port**, **base de données**, **nom d&#39;utilisateur** et **mot de passe**, consultez le [guide d&#39;identification](../ui/credentials.md).

![La page Informations d’identification de l’espace de travail Requêtes Experience Platform avec les informations d’identification et les informations d’identification arrivant à expiration est mise en surbrillance.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] propose également des informations d’identification non expirantes pour permettre une configuration unique avec des clients tiers. Consultez la documentation de [ instructions complètes sur la génération et l&#39;utilisation des informations d&#39;identification non arrivant à expiration ](../ui/credentials.md#non-expiring-credentials). Il est nécessaire de terminer ce processus si vous souhaitez connecter BDVisualizer en tant que configuration unique. Les valeurs `credential` et `technicalAccountId` acquises constituent la valeur du paramètre DBVisualizer `password`.

## Authentification {#authentication}

Pour avoir besoin d’une authentification par identifiant utilisateur et mot de passe chaque fois qu’une connexion est établie, accédez à l’onglet [!DNL Properties] et sélectionnez **[!DNL Authentication]** dans la barre latérale de navigation sous [!DNL PostgreSQL].

Dans le panneau Connection Authentication, cochez les cases **[!DNL Require Userid]** et **[!DNL Require Password]** , puis sélectionnez **[!DNL Apply]**. Vous trouverez plus d’informations sur la [définition des options d’authentification](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) dans la documentation officielle.

## Connexion à Platform

Vous pouvez établir une connexion à l’aide d’informations d’identification arrivant à expiration ou non arrivant à expiration. Pour établir une connexion, sélectionnez l’onglet **[!DNL Connection]** dans l’onglet [!DNL PostgreSQL] vue d’objet et saisissez vos informations d’identification d’Experience Platform pour les paramètres suivants. Des instructions complémentaires pour [configurer une connexion manuelle](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) sont disponibles sur le site officiel DBVisualizer.

>[!NOTE]
>
>Toutes les informations d’identification requises par BDVisualizer dans le tableau ci-dessous sont les mêmes pour les informations d’identification arrivant à expiration et non arrivant à expiration, sauf indication contraire dans la description du paramètre.

| Paramètre de connexion | Description |
|---|---|
| **[!UICONTROL Nom]** | Créez un nom pour votre connexion. Il est recommandé de fournir un nom convivial pour reconnaître la connexion. |
| **[!UICONTROL Serveur de base de données]** | Il s’agit de vos informations d’identification **[!UICONTROL Host]** d’Experience Platform. |
| **[!UICONTROL Port de base de données]** | Port de [!DNL Query Service]. Vous devez utiliser le port **80** ou **5432** pour vous connecter à [!DNL Query Service]. |
| **[!UICONTROL Base de données]** | Utilisez la valeur d&#39;identification **[!UICONTROL Database]** de votre Experience Platform : `prod:all`. |
| **[!UICONTROL Database Userid]** | Il s’agit de votre ID d’organisation Platform. Utilisez la valeur d’identification **[!UICONTROL Username]** de votre Experience Platform. L’ID sera au format `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Mot de passe de la base de données]** | Cette chaîne alphanumérique est votre identifiant Experience Platform **[!UICONTROL Password]**. Si vous souhaitez utiliser des informations d’identification qui n’expirent pas, cette valeur correspond aux arguments concaténés de `technicalAccountID` et de `credential` téléchargés dans le fichier JSON de configuration. La valeur du mot de passe se présente comme suit : {technicalAccountId}:{credential}. Le fichier de configuration JSON pour les informations d’identification non arrivant à expiration est un téléchargement unique lors de leur initialisation, dont Adobe ne conserve pas de copie. |

Après avoir saisi toutes les informations d’identification pertinentes, sélectionnez **[!DNL Connect]**.

La boîte de dialogue [!DNL Connect] s’affiche à la première occasion de la session. Saisissez votre identifiant utilisateur et votre mot de passe, puis sélectionnez **[!DNL Connect]**. Un message s’affiche dans le journal pour confirmer la connexion.

## Étapes suivantes

Maintenant que vous êtes connecté à [!DNL DbVisualizer] avec [!DNL Query Service], vous pouvez utiliser [!DNL DbVisualizer] pour écrire des requêtes. Pour plus d’informations sur la manière d’écrire et d’exécuter des requêtes, consultez le [guide sur l’exécution de requêtes](../best-practices/writing-queries.md).
