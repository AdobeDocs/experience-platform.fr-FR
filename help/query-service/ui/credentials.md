---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;requête;éditeur de requêtes;éditeur de requêtes;éditeur de requêtes;éditeur de requêtes
solution: Experience Platform
title: Guide de l’interface utilisateur de Query Service
topic-legacy: guide
description: Adobe Experience Platform Query Service fournit une interface utilisateur qui peut être utilisée pour écrire et exécuter des requêtes, afficher des requêtes précédemment exécutées et accéder aux requêtes enregistrées par les utilisateurs au sein de votre organisation IMS.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: aabe89f236bc68a51f14ee1909687982f4fe5973
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---


# Guide d’identification

Adobe Experience Platform Query Service vous permet de vous connecter à des clients externes. Vous pouvez vous connecter à ces clients externes à l’aide d’informations d’identification arrivant à expiration ou d’informations d’identification non arrivant à expiration.

## Expiration des informations d’identification

Vous pouvez utiliser des informations d’identification arrivant à expiration pour configurer rapidement une connexion à un client externe.

![](../images/ui/credentials/expiring-credentials.png)

La section **[!UICONTROL Informations d’identification arrivant à expiration]** fournit les informations suivantes :

- **[!UICONTROL Hôte]** : Nom de l’hôte auquel vous vous connectez. Pour la connexion à Query Service, cela inclut le nom de l’organisation IMS que vous utilisez actuellement.
- **[!UICONTROL Port]** : Numéro de port de l’hôte auquel vous vous connectez.
- **[!UICONTROL Base de données]** : Nom de la base de données à laquelle vous vous connectez.
- **[!UICONTROL Nom d’utilisateur]** : Nom d’utilisateur que vous utiliserez pour vous connecter à Query Service.
- **[!UICONTROL Mot de passe]** : mot de passe que vous utiliserez pour vous connecter à Query Service.
- **[!UICONTROL Commande]** PSQL : Une commande qui a automatiquement inséré toutes les informations pertinentes pour vous connecter à Query Service à l’aide de PSQL sur la ligne de commande.
- **[!UICONTROL Expire]** : Date d’expiration des informations d’identification arrivant à expiration. Les informations d’identification expirent 24 heures après leur génération.

## Informations d’identification non arrivant à expiration

Vous pouvez utiliser des informations d’identification non arrivant à expiration pour configurer une connexion plus permanente à un client externe.

Pour créer un ensemble d’informations d’identification non arrivant à expiration, sélectionnez **[!UICONTROL Générer les informations d’identification]**.

>[!NOTE]
>
>Avant de pouvoir créer des informations d’identification non arrivées à expiration, vous devez disposer des autorisations **Sandbox** et **Gérer l’intégration de Query Service**. Pour savoir comment attribuer ces autorisations, consultez la documentation sur le [contrôle d’accès](../../access-control/home.md).

![](../images/ui/credentials/generate-credentials.png)

La fenêtre modale de génération des informations d’identification s’affiche. Pour créer des informations d’identification non expirantes, vous devez fournir les détails suivants :

- **[!UICONTROL Nom]** : Nom des informations d’identification que vous générez.
- **[!UICONTROL Description]** : (Facultatif) Description des informations d’identification que vous générez.
- **[!UICONTROL Affecté à]** : L’utilisateur auquel les informations d’identification seront attribuées. Cette valeur doit correspondre à l’adresse électronique de l’utilisateur qui crée les informations d’identification.
- **[!UICONTROL Mot de passe]**  (facultatif) Mot de passe facultatif pour vos informations d’identification. Si le mot de passe n’est pas défini, Adobe génère automatiquement un mot de passe.

Une fois que vous avez fourni tous les détails requis, sélectionnez **[!UICONTROL Générer les informations d’identification]** pour générer vos informations d’identification.

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Une fois le bouton **[!UICONTROL Générer les informations d’identification]** sélectionné, un fichier de configuration contenant des informations telles que le nom du compte technique, l’identifiant du compte technique et les informations d’identification. Comme Adobe n’enregistre pas **les informations d’identification générées, vous** devez **stocker le fichier téléchargé en toute sécurité et conserver un enregistrement des informations d’identification.**
>
>De plus, si les informations d’identification ne sont pas utilisées pendant 90 jours, les informations d’identification sont supprimées.

Maintenant que vous avez enregistré vos informations d’identification générées, sélectionnez **[!UICONTROL Fermer]**. Vous pouvez maintenant voir une liste de toutes vos informations d’identification qui ne expirent pas.

![](../images/ui/credentials/list-credentials.png)

Vous pouvez modifier ou supprimer vos informations d’identification non arrivant à expiration. Pour modifier des informations d’identification non expirantes, sélectionnez l’icône représentant un crayon (![](../images/ui/credentials/edit-icon.png)). Pour supprimer des informations d’identification non arrivant à expiration, sélectionnez l’icône de suppression (![](../images/ui/credentials/delete-icon.png)).

Lors de la modification d’informations d’identification non expirantes, un modal s’affiche. Vous pouvez fournir les détails suivants à mettre à jour :

- **[!UICONTROL Nom]** : Nom des informations d’identification que vous générez.
- **[!UICONTROL Description]** : (Facultatif) Description des informations d’identification que vous générez.
- **[!UICONTROL Affecté à]** : L’utilisateur auquel les informations d’identification seront attribuées. Cette valeur doit correspondre à l’adresse électronique de l’utilisateur qui crée les informations d’identification.

![](../images/ui/credentials/update-credentials.png)

Une fois que vous avez fourni tous les détails requis, sélectionnez **[!UICONTROL Mettre à jour le compte]** pour terminer la mise à jour de vos informations d’identification.

## Utilisation des informations d’identification pour se connecter à des clients externes

Vous pouvez utiliser les informations d’identification arrivant à expiration ou non pour vous connecter à des clients externes, tels qu’Aqua Data Studio, Looker ou Power BI.

Lors de la connexion à ces clients externes, vous devrez généralement inclure les informations suivantes :

- **Serveur/hôte** : Nom du serveur/hôte auquel vous vous connectez. Cette valeur prend la forme `server.adobe.io` et se trouve sous **[!UICONTROL Host]** dans la section des informations d’identification arrivant à expiration.
- **Port** : port du serveur/hôte auquel vous vous connectez. Cette valeur se trouve sous **[!UICONTROL Port]** dans la section Informations d’identification arrivant à expiration. Un exemple de valeur pour le port serait `80`.
- **Nom d’utilisateur** : Nom d’utilisateur de l’utilisateur qui se connecte au client externe. Celui-ci prend la forme `ID@AdobeOrg` et se trouve sous **[!UICONTROL Nom d’utilisateur]** dans la section des informations d’identification arrivant à expiration.
- **Mot de passe** : Mot de passe de l’utilisateur qui se connecte au client externe. Si vous utilisez des informations d’identification arrivant à expiration, vous pouvez le trouver sous **[!UICONTROL Mot de passe]** dans la section Informations d’identification arrivant à expiration. Si vous utilisez des informations d’identification qui ne expirent pas, cette valeur est composée à la fois de l’identifiant de compte technique et des informations d’identification dans le formulaire : `technicalAccountId:credential`.
- **Base de données** : La base de données à laquelle vous vous connectez. Cette valeur se trouve sous **[!UICONTROL Base de données]** dans la section Informations d’identification arrivant à expiration. Un exemple de valeur pour la base de données serait `prod:all`.

## Étapes suivantes

Maintenant que vous comprenez le fonctionnement des informations d’identification arrivant à expiration et non arrivant à expiration, vous pouvez utiliser ces informations d’identification pour vous connecter à des clients externes. Pour plus d’informations sur les clients externes, consultez le [guide de connexion des clients à Query Service](../clients/overview.md).