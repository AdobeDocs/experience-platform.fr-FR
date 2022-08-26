---
keywords: Experience Platform;accueil;rubriques les plus consultées;service de requête;Query Service;Db Visualizer;DbVisualizer;db Visulaizer;se connecter au service de requête;
solution: Experience Platform
title: Connexion de DbVisualizer à Query Service
topic-legacy: connect
description: Ce document décrit les étapes à suivre pour connecter DbVisualizer à Adobe Experience Platform Query Service.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: 9c272cc5b879e38f6b6113542ec7bdfd4f11fa8a
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 1%

---

# Connexion [!DNL DbVisualizer] to [!DNL Query Service] {#connect-dbvisualizer}

Ce document décrit les étapes à suivre pour connecter la variable [!DNL DbVisualizer] outil de base de données avec Adobe Experience Platform [!DNL Query Service].

## Prise en main

Ce guide nécessite que vous ayez déjà accès à la fonction [!DNL DbVisualizer] de l’appli de bureau et connaissent comment naviguer dans son interface. Pour télécharger le [!DNL DbVisualizer] pour plus d’informations, voir [officiel [!DNL DbVisualizer] documentation](https://www.dbvis.com/download/).

>[!NOTE]
>
>Il y a [!DNL Windows], [!DNL macOS], et [!DNL Linux] versions de [!DNL DbVisualizer]. Les captures d’écran de ce guide ont été réalisées à l’aide de la méthode [!DNL macOS] application de bureau . Il peut y avoir des incohérences mineures dans l’interface utilisateur entre les versions.

Pour acquérir les informations d’identification nécessaires à la connexion [!DNL  DbVisualizer] pour Experience Platform, vous devez avoir accès à l’espace de travail Requêtes dans l’interface utilisateur de Platform. Contactez votre administrateur de l’organisation IMS si vous n’avez pas actuellement accès à l’espace de travail Requêtes .

## Création d’une connexion à une base de données {#connect-database}

Une fois que vous avez installé l’appli de bureau sur votre ordinateur local, démarrez l’application et sélectionnez **[!DNL Create a Database Connection]** à partir de la [!DNL DbVisualizer] . Sélectionnez **[!DNL Create a Connection]** dans le panneau situé à droite.

![Le [!DNL DbVisualizer] menu principal avec &quot;Créer une connexion à la base de données&quot; en surbrillance.](../images/clients/dbvisualizer/create-db-connection.png)

Utilisez la barre de recherche ou sélectionnez [!DNL PostgreSQL] dans la liste déroulante nom du pilote. L’espace de travail Connexion à la base de données s’affiche.

![menu déroulant du nom du pilote avec [!DNL PostgreSQL] surlignée.](../images/clients/dbvisualizer/driver-name.png)

Dans l&#39;espace de travail Connexion à la base de données , sélectionnez le **[!DNL Properties]** , suivie de la fonction **[!DNL Driver Properties]** dans la barre latérale de navigation.

![Espace de travail Connexion à la base de données avec l’onglet Propriétés surligné.](../images/clients/dbvisualizer/driver-properties.png)

Les trois propriétés de pilote requises sont présentées dans le tableau ci-dessous.

| Propriété | Description |
| ------ | ------ |
| `PGHOST` | Le nom d’hôte de la variable [!DNL PostgreSQL] serveur. Cette valeur est votre Experience Platform [!UICONTROL Hôte] informations d’identification. |
| `SSL` | Cela contrôle l’utilisation des exigences SSL. You **must** utiliser la valeur `require` pour activer cette exigence. |
| `user` | Le nom d’utilisateur connecté à la base de données est votre ID d’organisation. Il s’agit d’une chaîne alphanumérique se terminant par `@adobe.org` |

>[!IMPORTANT]
>
>Voir [[!DNL Query Service] Documentation SSL](./ssl-modes.md) pour en savoir plus sur la prise en charge du protocole SSL pour les connexions tierces à Adobe Experience Platform Query Service et sur la connexion à l’aide de `verify-full` Mode SSL.

### [!DNL Query Service] informations

Le `PGHOST` et `user` sont extraites de vos informations d’identification Adobe Experience Platform. Pour trouver vos informations d’identification, connectez-vous à l’interface utilisateur de Platform et sélectionnez **[!UICONTROL Requêtes]** à partir du volet de navigation de gauche, suivi de **[!UICONTROL Informations d’identification]**. Pour plus d’informations sur la recherche du nom de la base de données, de l’hôte, du port et des informations de connexion, consultez la section [guide des informations d’identification](../ui/credentials.md).

![Tableau de bord des informations d’identification des requêtes Experience Platform avec les informations d’identification mises en surbrillance.](../images/clients/dbvisualizer/query-service-credentials-page.png)

[!DNL Query Service] propose également des informations d’identification non expirantes pour permettre une configuration unique avec des clients tiers. Consultez la documentation pour [instructions complètes sur la génération et l’utilisation des informations d’identification non arrivant à expiration](../ui/credentials.md#non-expiring-credentials).

Utilisez la barre de recherche pour rechercher chaque propriété, puis sélectionnez la cellule correspondante pour la valeur du paramètre. La cellule est mise en surbrillance en bleu. Saisissez vos informations d’identification Platform dans le champ de valeur et sélectionnez **[!DNL Apply]** pour ajouter la propriété driver.

>[!NOTE]
>
>Pour ajouter une seconde `user` profil, sélectionnez `user` dans la colonne paramètre , sélectionnez l’icône bleue + (plus) pour ajouter les informations d’identification de chaque utilisateur. Sélectionner **[!DNL Apply]** pour ajouter la propriété driver.

Le [!DNL Edited] affiche une coche pour indiquer que la valeur du paramètre a été mise à jour.

## Authentification

Pour exiger une authentification par identifiant utilisateur et mot de passe chaque fois qu’une connexion est établie, sélectionnez **[!DNL Authentication]** de la barre latérale de navigation sous [!DNL PostgreSQL].

Dans le panneau Authentification de connexion , cochez les deux options **[!DNL Require Userid]** et **[!DNL Require Password]** , puis sélectionnez **[!DNL Apply]**.

![Panneau Authentification de connexion avec les cases à cocher Userid et Mot de passe mises en surbrillance.](../images/clients/dbvisualizer/connection-authentication.png)

## Connecter  à Platform

Pour établir une connexion, sélectionnez la variable **[!DNL Connection]** dans l’espace de travail Connexion à la base de données et saisissez les informations d’identification de votre Experience Platform pour les paramètres suivants.

- **Nom**: Il est recommandé de fournir un nom convivial pour reconnaître la connexion.
- **Serveur de base de données**: C’est votre Experience Platform. [!UICONTROL Hôte] informations d’identification.
- **Port de la base de données**: Le port pour [!DNL Query Service]. Vous devez utiliser le port 80 pour vous connecter à [!DNL Query Service].
- **Base**: Utilisation des informations d’identification `dbname` value `prod:all`.
- **Database Userid**: Il s’agit de votre ID d’organisation Platform. L’Userid sera au format de `ORG_ID@AdobeOrg`.
- **Mot de passe de la base de données**: Chaîne alphanumérique figurant sur la variable [!DNL Query Service] tableau de bord des informations d’identification.

Après avoir saisi toutes les informations d’identification pertinentes, sélectionnez **[!DNL Connect]**.

![L&#39;espace de travail Connexion à la base de données avec l&#39;onglet Connexion et le bouton Connexion mis en surbrillance.](../images/clients/dbvisualizer/connect.png)

Le [!DNL Connect] s’affiche à la première occasion de la session.

![La boîte de dialogue Se connecter avec les champs de texte Identifiant utilisateur de la base de données et Mot de passe de la base de données est mise en surbrillance.](../images/clients/dbvisualizer/connect-dialog.png)

Saisissez votre identifiant utilisateur et votre mot de passe, puis sélectionnez **[!DNL Connect]**. Un message s’affiche dans le journal pour confirmer la connexion.

## Étapes suivantes

Maintenant que vous êtes connecté [!DNL DbVisualizer] avec [!DNL Query Service], vous pouvez utiliser [!DNL DbVisualizer] pour écrire des requêtes. Pour plus d’informations sur la manière d’écrire et d’exécuter des requêtes, veuillez lire la section [guide sur l&#39;exécution des requêtes](../best-practices/writing-queries.md).
