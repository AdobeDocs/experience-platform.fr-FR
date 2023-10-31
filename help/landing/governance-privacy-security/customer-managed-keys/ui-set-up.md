---
title: Configuration et configuration des clés gérées par le client à l’aide de l’interface utilisateur de Platform
description: Découvrez comment configurer votre application CMK avec votre client Azure et envoyer votre ID de clé de chiffrement à Adobe Experience Platform.
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 22%

---

# Configuration et configuration des clés gérées par le client à l’aide de l’interface utilisateur de Platform

Ce document couvre le processus d’activation de la fonctionnalité de clés gérées par le client (CMK) dans Platform à l’aide de l’interface utilisateur. Pour obtenir des instructions sur la façon d’effectuer ce processus à l’aide de l’API, reportez-vous à la section [Document de configuration du CMK de l’API](./api-set-up.md).

## Conditions préalables

Pour afficher et consulter la variable [!UICONTROL Chiffrement] dans Adobe Experience Platform, vous devez avoir créé un rôle et affecté la fonction [!UICONTROL Gestion de la clé gérée par le client] autorisation de ce rôle. Tout utilisateur qui possède la variable [!UICONTROL Gestion de la clé gérée par le client] La permission peut activer le CMK pour leur organisation.

Pour plus d’informations sur l’affectation de rôles et d’autorisations dans Experience Platform, reportez-vous à la section [configuration de la documentation sur les autorisations](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Pour activer le CMK, votre [[!DNL Azure] Key Vault doit être configuré](./azure-key-vault-config.md) avec les paramètres suivants :

* [Activer la protection contre le vidage](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Activation de la suppression progressive](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurer l’accès à l’aide de [!DNL Azure] contrôle d’accès en fonction du rôle](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Configurer un coffre  [!DNL Azure]  Key Vault](./azure-key-vault-config.md)

## Configurer l’application CMK {#register-app}

Une fois que votre coffre-fort de clé est configuré, l’étape suivante consiste à enregistrer l’application CMK qui se connectera à votre [!DNL Azure] client.

### Prise en main

Pour afficher la variable [!UICONTROL Configurations du chiffrement] tableau de bord, sélectionnez **[!UICONTROL Chiffrement]** sous le [!UICONTROL Administration] en-tête de la barre de navigation gauche.

![Le tableau de bord de configuration Chiffrement avec Encryption et la carte Clés gérées par le client sont mis en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

Sélectionner **[!UICONTROL Configurer]** pour ouvrir le [!UICONTROL Configuration des clés gérées par le client] vue. Cet espace de travail contient toutes les valeurs nécessaires pour effectuer les étapes décrites ci-dessous et effectuer l’intégration avec votre coffre de clés Azure.

### Copie de l’URL d’authentification {#copy-authentication-url}

Pour lancer le processus d’enregistrement, copiez l’URL d’authentification de l’application pour votre organisation à partir de la page [!UICONTROL Configuration des clés gérées par le client] affichez-la et collez-la dans votre [!DNL Azure] environnement **[!DNL Key Vault Crypto Service Encryption User]**. Détails sur la manière de procéder [affecter un rôle](#assign-to-role) sont fournies dans la section suivante.

Sélectionnez l’icône de copie (![Icône Copier.](../../images/governance-privacy-security/customer-managed-keys/copy-icon.png)) par le [!UICONTROL URL d’authentification de l’application].

![La variable [!UICONTROL Configuration des clés gérées par le client] avec la section URL d’authentification de l’application mise en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

Copiez et collez le [!UICONTROL URL d’authentification de l’application] dans un navigateur pour ouvrir une boîte de dialogue d’authentification. Sélectionnez **[!DNL Accept]** pour ajouter le principal de service de l’application CMK à votre client [!DNL Azure]. Confirmer l’authentification vous redirige vers la page d’entrée de l’Experience Cloud.

![Boîte de dialogue de demande d’autorisation Microsoft avec [!UICONTROL Accepter] surlignée.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>Si vous avez plusieurs [!DNL Microsoft Azure] abonnements, vous pouvez alors potentiellement connecter votre instance Platform à un coffre de clé incorrect. Dans ce cas, vous devez échanger les `common` section du nom de l’URL d’authentification de l’application pour l’ID de répertoire de CMK.<br>Copiez l’ID de répertoire CMK à partir de la page Paramètres du portail, Répertoires et Abonnements de [!DNL Microsoft Azure] application<br>![La variable [!DNL Microsoft Azure] Paramètres du portail d’application, Répertoires et abonnements , avec l’ID d’annuaire en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>Ensuite, collez-le dans la barre d’adresse de votre navigateur.<br>![Une page de navigateur Google avec la section &quot;commune&quot; de l’URL d’authentification de l’application mise en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### Attribuer l’application CMK à un rôle {#assign-to-role}

Une fois le processus d’authentification terminé, revenez au coffre de clés [!DNL Azure] et sélectionnez **[!DNL Access control]** dans le volet de navigation de gauche. À partir de là, sélectionnez **[!DNL Add]**, puis **[!DNL Add role assignment]**.

![La variable [!DNL Microsoft Azure] tableau de bord avec [!DNL Add] et [!DNL Add role assignment] surlignée.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

L’écran suivant vous invite à choisir un rôle pour cette affectation. Sélectionnez **[!DNL Key Vault Crypto Service Encryption User]** avant de sélectionner **[!DNL Next]** pour continuer.

![La variable [!DNL Microsoft Azure] tableau de bord avec la variable [!DNL Key Vault Crypto Service Encryption User] surlignée.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Dans l’écran suivant, choisissez **[!DNL Select members]** pour ouvrir une boîte de dialogue dans le rail de droite. Utilisez la barre de recherche pour localiser le principal de service de l’application CMK et sélectionnez-le dans la liste. Lorsque vous avez terminé, sélectionnez **[!DNL Save]**.

>[!NOTE]
>
>Si vous ne trouvez pas votre application dans la liste, votre principal de service n’a pas été accepté dans votre client. Pour vous assurer que vous disposez des privilèges appropriés, utilisez votre [!DNL Azure] administrateur ou représentant.

Vous pouvez vérifier l’application en comparant la variable [!UICONTROL ID de l’application] fourni dans la variable [!UICONTROL Configuration des clés gérées par le client] avec la vue [!DNL Application ID] fourni dans la variable [!DNL Microsoft Azure] présentation des applications.

![La variable [!UICONTROL Configuration des clés gérées par le client] avec la vue [!UICONTROL ID de l’application] surlignée.](../../images/governance-privacy-security/customer-managed-keys/application-id.png)

Tous les détails nécessaires pour vérifier les outils Azure sont inclus dans l’interface utilisateur de Platform. Ce niveau de granularité est fourni lorsque de nombreux utilisateurs souhaitent utiliser d’autres outils Azure afin d’améliorer leur capacité à surveiller et consigner l’accès de ces applications à leur coffre-fort clé. Pour ce faire, il est essentiel de comprendre ces identifiants et d’aider les services Adobe à accéder à la clé.

## Activer la configuration de la clé de chiffrement sur Experience Platform {#send-to-adobe}

Après l’installation de l’application CMK sur [!DNL Azure], vous pouvez envoyer votre identifiant de la clé de chiffrement à Adobe. Sélectionnez **[!DNL Keys]** dans le volet de navigation de gauche, suivi du nom de la clé à envoyer.

![Le tableau de bord Azure de Microsoft avec la variable [!DNL Keys] et le nom de la clé mis en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Sélectionnez la dernière version de la clé et sa page de détails s’affiche. À partir de là, vous pouvez éventuellement configurer les opérations autorisées pour la clé.

>[!IMPORTANT]
>
>Les opérations minimales requises autorisées pour la clé sont les suivantes : **[!DNL Wrap Key]** et **[!DNL Unwrap Key]** autorisations. Vous pouvez inclure [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign], et [!DNL Verify] devrais-tu vouloir.

Le champ **[!UICONTROL Identifiant de clé]** affiche l’identifiant d’URI de la clé. Copiez cette valeur d’URI à utiliser à l’étape suivante.

![La clé du tableau de bord Azure de Microsoft contient les informations suivantes : [!DNL Permitted operations] et les sections Copier la clé URL sont mises en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Une fois que vous avez obtenu la variable [!DNL Key vault URI], revenez à la variable [!UICONTROL Configuration des clés gérées par le client] afficher et saisir une description ; **[!UICONTROL Nom de la configuration]**. Ajoutez ensuite le [!DNL Key Identifier] extrait de la page de détails de la clé Azure dans la variable **[!UICONTROL Identifiant de clé Vault]** et sélectionnez **[!UICONTROL Enregistrer]**.

![La variable [!UICONTROL Configuration des clés gérées par le client] avec la vue [!UICONTROL Nom de la configuration] et la variable [!UICONTROL Identifiant de clé Vault] en surbrillance.](../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

Vous revenez alors à la variable [!UICONTROL Tableau de bord des configurations de chiffrement]. L’état de la variable [!UICONTROL Clés gérées par le client] La configuration s’affiche sous [!UICONTROL Traitement].

![La variable [!UICONTROL Configurations du chiffrement] tableau de bord avec [!UICONTROL Traitement] mis en surbrillance sur la [!UICONTROL Clés gérées par le client] carte.](../../images/governance-privacy-security/customer-managed-keys/processing.png)

## Vérifiez le statut de la configuration {#check-status}

Laps de temps important pour le traitement. Pour vérifier le statut de la configuration, revenez à la [!UICONTROL Configuration des clés gérées par le client] afficher et faire défiler l’écran vers le bas jusqu’à [!UICONTROL Statut de la configuration]. La barre de progression est passée à l’étape 1 de 3 et explique que le système valide que Platform a accès à la clé et au coffre-fort.

Il existe quatre états potentiels de la configuration du CMK. En voici la liste :

* Étape 1 : valide la capacité de Platform à accéder à la clé et au coffre-fort de la clé.
* Étape 2 : le coffre-fort et le nom de la clé sont en train d’être ajoutés à tous les entrepôts de données de votre organisation.
* Étape 3 : la coffre-fort de la clé et le nom de la clé ont été ajoutés avec succès aux banques de données.
* `FAILED` : un problème s’est produit, principalement lié à la configuration de la clé, du coffre de clés ou de l’application multi-utilisateur.

## Étapes suivantes

En suivant les étapes ci-dessus, vous avez activé le CMK pour votre entreprise. Les données ingérées dans les entrepôts de données principaux seront désormais chiffrées et déchiffrées à l’aide des clés de votre [!DNL Azure] Key Vault.
