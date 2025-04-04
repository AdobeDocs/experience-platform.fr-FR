---
keywords: Experience Platform;accueil;rubriques les plus consultées;query service;Query service;Db Visualizer;DbVisualizer;db visualizer;se connecter à query service;
solution: Experience Platform
title: Connexion de DbVisualizer à Query Service
description: Ce document décrit les étapes à suivre pour connecter DbVisualizer à Adobe Experience Platform Query Service.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 3%

---

# Connexion de [!DNL DbVisualizer] à [!DNL Query Service] {#connect-dbvisualizer}

Ce document décrit les étapes à suivre pour connecter l’outil de base de données [!DNL DbVisualizer] à Adobe Experience Platform [!DNL Query Service].

## Prise en main

Ce guide nécessite que vous ayez déjà accès à l’application [!DNL DbVisualizer] Desktop et que vous sachiez comment naviguer dans son interface. Pour télécharger l’application de bureau [!DNL DbVisualizer] ou pour plus d’informations, consultez la [documentation [!DNL DbVisualizer] officielle](https://www.dbvis.com/download/).

Pour acquérir les informations d’identification nécessaires à la connexion de [!DNL  DbVisualizer] à Experience Platform, vous devez avoir accès à l’espace de travail Requêtes dans l’interface utilisateur d’Experience Platform. Contactez l’administrateur ou administratrice de votre organisation si vous n’avez pas actuellement accès à l’espace de travail Requêtes.

## Créer une connexion à la base de données {#connect-database}

Une fois que vous avez installé l&#39;appli de bureau sur votre ordinateur local, suivez les instructions officielles de BDVisualizer pour [créer une nouvelle connexion à la base de données](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

Une fois que vous avez sélectionné **[!DNL PostgreSQL]** dans la liste [!DNL Connections], un onglet [!DNL Object View] pour la nouvelle connexion [!DNL PostgreSQL] s’affiche.

### Définir les propriétés du pilote pour votre connexion {#properties}

Dans l’onglet Affichage de l’objet [!DNL PostgreSQL] , sélectionnez l’onglet **[!DNL Properties]** , suivi de l’**[!DNL Driver Properties]** dans la barre latérale de navigation. Vous trouverez plus d&#39;informations sur [les propriétés du pilote](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) dans la documentation officielle.

Saisissez ensuite les propriétés du pilote décrites dans le tableau ci-dessous.

>[!IMPORTANT]
>
>Pour connecter DBVisualizer à Adobe Experience Platform, vous devez activer l’utilisation de SSL. Consultez la documentation [Modes SSL](./ssl-modes.md) pour en savoir plus sur la prise en charge SSL pour les connexions tierces à Adobe Experience Platform Query Service et comment se connecter à l’aide `verify-full` mode SSL.

| Propriété | Description |
| ------ | ------ |
| `PGHOST` | Nom d’hôte du serveur [!DNL PostgreSQL]. Cette valeur correspond à vos informations d’identification Experience Platform **[!UICONTROL hôte]**. |
| `ssl` | Définissez la valeur SSL `1` pour activer l’utilisation de SSL. |
| `sslmode` | Cela contrôle le niveau de protection SSL. Il est recommandé d’utiliser le mode SSL `require` lors de la connexion de clients tiers à Adobe Experience Platform. Le mode `require` garantit que le chiffrement est requis pour toutes les communications et que le réseau est approuvé pour se connecter au serveur approprié. La validation du certificat SSL du serveur n’est pas requise. |
| `user` | Le nom d’utilisateur connecté à la base de données est votre identifiant d’organisation. Il s’agit d’une chaîne alphanumérique se terminant par `@Adobe.Org`. Cette valeur correspond à vos informations d’identification Experience Platform **[!UICONTROL Nom d’utilisateur]**. |

Utilisez la barre de recherche pour rechercher chaque propriété, puis sélectionnez la cellule correspondante pour la valeur du paramètre. La cellule est mise en surbrillance en bleu. Saisissez vos informations d’identification Experience Platform dans le champ de valeur et sélectionnez **[!DNL Apply]** pour ajouter la propriété du pilote.

>[!NOTE]
>
>Pour ajouter un second profil de `user`, sélectionnez `user` dans la colonne de paramètres, puis sélectionnez l’icône bleue + (plus) pour ajouter des informations d’identification pour chaque utilisateur. Sélectionnez **[!DNL Apply]** pour ajouter la propriété de pilote.

La colonne [!DNL Edited] affiche une coche pour indiquer que la valeur du paramètre a été mise à jour.

### Informations d’identification d’Input Query Service {#query-service-credentials}

Pour obtenir les informations d’identification nécessaires à la connexion de BBVisualizer à Query Service, connectez-vous à l’interface utilisateur d’Experience Platform et sélectionnez **[!UICONTROL Requêtes]** dans le volet de navigation de gauche, suivi de **[!UICONTROL Informations d’identification]**. Pour plus d’informations sur la recherche de vos informations d’identification **hôte**, **port**, **base de données**, **nom d’utilisateur** et **mot de passe**, veuillez lire le guide [](../ui/credentials.md) credentials.

![Page Informations d’identification de l’espace de travail Requêtes Experience Platform avec les Informations d’identification et les Informations d’identification arrivant à expiration en surbrillance.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] propose également des informations d’identification non expirantes pour permettre une configuration unique avec des clients tiers. Consultez la documentation pour obtenir des [instructions complètes sur la génération et l’utilisation d’informations d’identification non expirantes](../ui/credentials.md#non-expiring-credentials). Il est nécessaire de terminer ce processus si vous souhaitez connecter BDVisualizer en une seule configuration. Les valeurs `credential` et `technicalAccountId` acquises comprennent la valeur du paramètre `password` DBVisualizer.

## Authentification {#authentication}

Pour exiger un ID utilisateur et une authentification par mot de passe chaque fois qu’une connexion est établie, accédez à l’onglet [!DNL Properties] et sélectionnez **[!DNL Authentication]** dans la barre latérale de navigation sous [!DNL PostgreSQL].

Dans le panneau Authentification de la connexion , cochez les cases **[!DNL Require Userid]** et **[!DNL Require Password]**, puis sélectionnez **[!DNL Apply]**. Vous trouverez plus d’informations sur la [définition des options d’authentification](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) dans la documentation officielle.

## Connexion à Experience Platform

Vous pouvez établir une connexion à l’aide d’informations d’identification arrivant à expiration ou non. Pour établir une connexion, sélectionnez l’onglet **[!DNL Connection]** dans l’onglet Affichage de l’objet [!DNL PostgreSQL] et saisissez vos informations d’identification Experience Platform pour les paramètres suivants. Des instructions complémentaires pour [configurer une connexion manuelle](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) sont disponibles sur le site officiel de DBVisualizer.

>[!NOTE]
>
>Toutes les informations d’identification requises par BDVisualizer dans le tableau ci-dessous sont identiques pour les informations d’identification expirantes et non expirantes, sauf indication contraire dans la description des paramètres.

| Paramètre de connexion | Description |
|---|---|
| **[!UICONTROL Nom]** | Créez un nom pour votre connexion. Il est recommandé de fournir un nom convivial pour reconnaître la connexion. |
| **[!UICONTROL Serveur de base de données]** | Il s’agit de vos informations d’identification Experience Platform **[!UICONTROL hôte]**. |
| **[!UICONTROL Port de base de données]** | Port de [!DNL Query Service]. Vous devez utiliser le port **80** ou **5432** pour vous connecter à [!DNL Query Service]. |
| **[!UICONTROL Base de données]** | Utilisez votre valeur d’informations d’identification Experience Platform **[!UICONTROL Base de données]** : `prod:all`. |
| **[!UICONTROL Identifiant utilisateur de la base de données]** | Il s’agit de votre identifiant d’organisation Experience Platform. Utilisez votre valeur d’identification Experience Platform **[!UICONTROL Nom d’utilisateur]**. L’ID aura le format `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Mot de passe de la base de données]** | Cette chaîne alphanumérique correspond à vos informations d’identification Experience Platform **[!UICONTROL mot de passe]**. Si vous souhaitez utiliser des informations d’identification non expirantes, cette valeur correspond aux arguments concaténés des `technicalAccountID` et `credential` téléchargés dans le fichier de configuration JSON. La valeur du mot de passe se présente comme suit : {technicalAccountId}:{credential}. Le fichier JSON de configuration pour les informations d’identification non expirantes est un téléchargement unique pendant leur initialisation dont Adobe ne conserve pas de copie. |

Après avoir saisi toutes les informations d’identification pertinentes, sélectionnez **[!DNL Connect]**.

La boîte de dialogue [!DNL Connect] s’affiche à la première occasion de la session. Saisissez votre ID utilisateur et votre Mot de passe, puis sélectionnez **[!DNL Connect]**. Un message s’affiche dans le journal pour confirmer la réussite de la connexion.

## Étapes suivantes

Maintenant que vous avez connecté [!DNL DbVisualizer] à [!DNL Query Service], vous pouvez utiliser [!DNL DbVisualizer] pour écrire des requêtes. Pour plus d’informations sur l’écriture et l’exécution de requêtes, consultez le guide [ sur l’exécution de requêtes](../best-practices/writing-queries.md).
