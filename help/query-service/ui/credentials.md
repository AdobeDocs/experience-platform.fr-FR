---
keywords: Experience Platform;accueil;rubriques populaires;service de requête;service de requête;requête;éditeur de requêtes;éditeur de requêtes;éditeur de requêtes;éditeur de requêtes
solution: Experience Platform
title: Guide de l’interface utilisateur de Query Service
topic-legacy: guide
description: Adobe Experience Platform Query Service fournit une interface utilisateur qui peut être utilisée pour écrire et exécuter des requêtes, afficher des requêtes précédemment exécutées et accéder aux requêtes enregistrées par les utilisateurs au sein de votre organisation IMS.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: af122e5064fc5618266948d46c438d1776cdd0cf
workflow-type: tm+mt
source-wordcount: '1310'
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

Avant de pouvoir créer des informations d’identification non arrivées à expiration, vous devez configurer les autorisations **Sandbox** et **Gérer l’intégration de Query Service** pour votre organisation dans Adobe Admin Console.

Connectez-vous à [Adobe Admin Console](https://adminconsole.adobe.com/) et sélectionnez l’organisation appropriée dans la barre de navigation supérieure.

Dans la section [!UICONTROL Produits et services] de [!UICONTROL Aperçu], sélectionnez **Adobe Experience Platform**.

![Tableau de bord Adobe Admin Console](../images/ui/credentials/adobe-admin-console-dashboard.png)

La page Détails de Adobe Experience Platform s’affiche. Créez ensuite un profil. Sélectionnez [!UICONTROL **Nouveau profil**].

![Page Détails du Adobe Experience Platform](../images/ui/credentials/aep-details.png)

Une boîte de dialogue de création de profil s’affiche. Saisissez un nom explicite pour le nouveau profil et sélectionnez [!UICONTROL **Enregistrer**]. La page [!UICONTROL Paramètres] de votre nouveau profil s’affiche. Sélectionnez l’onglet [!UICONTROL **Autorisations**] dans les options disponibles.

### Activation des autorisations de Query Service

Pour vous assurer que les autorisations Query Service correctes sont activées pour votre organisation, recherchez et sélectionnez la catégorie [!UICONTROL **Query Service**] dans la liste.

![Catégorie de service de requête de l’onglet Autorisations mise en surbrillance](../images/ui/credentials/permissions-tab-query-service-category.png)

L’espace de travail [!UICONTROL Modifier les autorisations] pour Query Service s’affiche. Sélectionnez l’icône plus (**+**) pour [!UICONTROL **Gérer les requêtes**] et [!UICONTROL **Gérer l’intégration de Query Service**] pour les ajouter à la colonne [!UICONTROL Éléments d’autorisation inclus]. Sélectionnez ensuite [!UICONTROL **Enregistrer**] pour confirmer vos modifications.

![Enregistrer les éléments d’autorisation inclus](../images/ui/credentials/edit-permissions-for-query-service-profile.png)

Vous revenez alors à l’onglet Paramètres > Autorisations .

### Activation des autorisations Sandbox

Pour vous assurer que l’environnement de test approprié est sélectionné pour votre organisation, recherchez et sélectionnez la catégorie [!UICONTROL **Environnements de test**] dans la liste.

![Catégorie Environnements de test de l’onglet Autorisations mise en surbrillance](../images/ui/credentials/permissions-tab-sandboxes-category.png)

L’espace de travail Environnements de test s’affiche. À partir des [!UICONTROL Éléments d’autorisation disponibles], recherchez l’environnement de test approprié. Dans cette image, il s’agit de l’environnement de test de production. Sélectionnez l’icône plus (**+**) pour l’ajouter aux [!UICONTROL Éléments d’autorisation inclus]. Sélectionnez ensuite [!UICONTROL **Enregistrer**] pour confirmer vos modifications.

![Autorisation Ajouter un environnement de test de production](../images/ui/credentials/prod-sandbox.png)

Vous revenez alors à l’onglet Paramètres > Autorisations .

Trois autres étapes sont nécessaires pour permettre à un utilisateur d’accéder à la fonction de compte non arrivant à expiration.

- Ajoutez un nouvel utilisateur auquel accorder les autorisations nouvellement créées. Sélectionnez l’onglet [!UICONTROL **Utilisateurs**], suivi de [!UICONTROL **Ajouter un utilisateur**].

![Bouton Ajouter un utilisateur surligné](../images/ui/credentials/users-tab-new-user.png)

La boîte de dialogue Créer un utilisateur s’affiche. Saisissez un nom et un email pour le nouvel utilisateur et sélectionnez [!UICONTROL **Enregistrer**].

- L’utilisateur doit ensuite être ajouté en tant qu’administrateur pour permettre la création d’un compte pour tout profil de produit principal. Ajout de l’utilisateur nouvellement créé en tant qu’administrateur. sélectionnez l’onglet [!UICONTROL **Admins**], suivi de [!UICONTROL **Ajouter des administrateurs**].

![Bouton Ajouter un administrateur surligné dans l’onglet Admin](../images/ui/credentials/admins-tab-add-admin.png)

La boîte de dialogue d’ajout d’administrateur s’affiche. Saisissez les détails du nouvel administrateur dans les champs de texte et sélectionnez [!UICONTROL **Enregistrer**].

- L’utilisateur doit ensuite être ajouté en tant que développeur pour qu’une intégration soit créée. Sélectionnez l’onglet **Développeurs**, suivi de **Ajouter développeur**.

![Bouton Ajouter un développeur de l’onglet Développeur surligné](../images/ui/credentials/developers-tab-add-developer.png)

La boîte de dialogue d’ajout de développeur s’affiche. Saisissez les détails du nouveau développeur dans les champs de texte et sélectionnez **Enregistrer**.

Pour en savoir plus sur l’affectation d’autorisations, consultez la documentation sur le [contrôle d’accès](../../access-control/home.md).

Toutes les autorisations requises sont maintenant configurées dans la console du développeur Adobe pour que l’utilisateur puisse utiliser la fonction des informations d’identification arrivant à expiration.

Pour créer un ensemble d’informations d’identification non arrivant à expiration, dans l’espace de travail des informations d’identification des requêtes, sélectionnez **[!UICONTROL Générer les informations d’identification]**.

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
>Une fois le bouton **[!UICONTROL Générer les informations d’identification]** sélectionné, un fichier de configuration JSON est téléchargé sur votre ordinateur local. Comme Adobe n’enregistre pas **les informations d’identification générées, vous** devez **stocker le fichier téléchargé en toute sécurité et conserver un enregistrement des informations d’identification.**
>
>De plus, si les informations d’identification ne sont pas utilisées pendant 90 jours, les informations d’identification sont supprimées.

Le fichier de configuration JSON contient des informations telles que le nom du compte technique, l’identifiant de compte technique et les informations d’identification. Il est fourni au format suivant.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

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

Le tableau ci-dessous contient la liste des paramètres et leur description, généralement nécessaires pour se connecter à des clients externes.

>[!NOTE]
>
>Lors de la connexion à un hôte à l’aide d’informations d’identification non arrivant à expiration, il est toujours nécessaire d’utiliser tous les paramètres répertoriés dans la section [!UICONTROL EXPIRING CREDENTIALS] , à l’exception du mot de passe.

| Paramètre | Description |
|---|---|
| **Serveur/hôte** | Nom du serveur/hôte auquel vous vous connectez. Cette valeur prend la forme `server.adobe.io` et se trouve sous **[!UICONTROL Host]**. |
| **Port** | port du serveur/hôte auquel vous vous connectez. Cette valeur se trouve sous **[!UICONTROL Port]**. Un exemple de valeur pour le port serait `80`. |
| **Base de données** | La base de données à laquelle vous vous connectez. Cette valeur se trouve sous **[!UICONTROL Base de données]**. Un exemple de valeur pour la base de données serait `prod:all`. |
| **Nom d’utilisateur** | Nom d’utilisateur de l’utilisateur qui se connecte au client externe. Il s’agit d’une chaîne alphanumérique devant `@AdobeOrg`. Cette valeur se trouve sous **[!UICONTROL Nom d’utilisateur]**. |
| **Mot de passe** | Mot de passe de l’utilisateur qui se connecte au client externe. <ul><li>Si vous utilisez des informations d’identification arrivant à expiration, vous pouvez le trouver sous **[!UICONTROL Mot de passe]** dans la section Informations d’identification arrivant à expiration.</li><li>Si vous utilisez des informations d’identification qui n’expirent pas, cette valeur est composée des arguments de l’ID de compte technique et des informations d’identification extraites du fichier JSON de configuration. La valeur du mot de passe se présente comme suit : `{technicalAccountId}:{credential}`.</li></ul> |

## Étapes suivantes

Maintenant que vous comprenez le fonctionnement des informations d’identification arrivant à expiration et non arrivant à expiration, vous pouvez utiliser ces informations d’identification pour vous connecter à des clients externes. Pour plus d’informations sur les clients externes, consultez le [guide de connexion des clients à Query Service](../clients/overview.md).
