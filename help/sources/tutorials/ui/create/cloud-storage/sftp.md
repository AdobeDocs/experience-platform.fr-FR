---
title: Création d’une connexion Source SFTP dans l’interface utilisateur
description: Découvrez comment créer une connexion source SFTP à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: 9cd1232c9257d27b80ed57c26658b1e4058535e8
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 25%

---

# Créer une connexion source [!DNL SFTP] dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion source [!DNL SFTP] à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Commencer

Ce tutoriel nécessite une compréhension pratique des composants suivants de Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel Experience Platform organise les données d’expérience client. 
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel sur l’éditeur de schémas](../../../../../xdm/tutorials/create-schema-ui.md) : découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

>[!IMPORTANT]
>
>Il est recommandé d’éviter les nouvelles lignes ou les retours chariot lors de l’ingestion d’objets JSON avec une connexion source [!DNL SFTP]. Pour contourner cette limitation, utilisez un seul objet JSON par ligne et plusieurs lignes pour les fichiers qui s’ensuivent.

Si vous disposez déjà d’une connexion [!DNL SFTP] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecter les informations d’identification requises

Lisez le [[!DNL SFTP] guide d&#39;authentification](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials) pour obtenir des instructions détaillées sur la manière de récupérer vos informations d&#39;authentification.

## Connexion à votre serveur [!DNL SFTP]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie [!UICONTROL Stockage dans le cloud], sélectionnez **[!UICONTROL SFTP]**, puis sélectionnez **[!UICONTROL Ajouter des données]**.

![Catalogue des sources Experience Platform avec la source SFTP sélectionnée.](../../../../images/tutorials/create/sftp/catalog.png)

La page **[!UICONTROL Se connecter à SFTP]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour connecter un compte existant, sélectionnez le compte FTP ou SFTP avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Liste des comptes SFTP existants sur l’interface utilisateur Experience Platform.](../../../../images/tutorials/create/sftp/existing.png)

### Nouveau compte

>[!TIP]
>
>* Une fois créé, vous ne pouvez pas modifier le type d&#39;authentification d&#39;une connexion de base [!DNL SFTP]. Pour modifier le type d&#39;authentification, vous devez créer une nouvelle connexion de base.
>
>* SFTP prend en charge une clé OpenSSH de type RSA ou DSA. Assurez-vous que le contenu de votre fichier clé commence par `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` et se termine par `"-----END [RSA/DSA] PRIVATE KEY-----"`. Si le fichier de clé privée est un fichier au format PPK, utilisez l’outil PuTTY pour effectuer une conversion de PPK au format OpenSSH.

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description facultative de votre nouveau compte [!DNL SFTP].

![Nouvel écran de compte pour SFTP](../../../../images/tutorials/create/sftp/new.png)

La source [!DNL SFTP] prend en charge l’authentification et l’authentification de base via la clé publique SSH.

>[!BEGINTABS]

>[!TAB Authentification de base]

Pour utiliser une authentification de base, sélectionnez **[!UICONTROL Password]** , puis fournissez les valeurs appropriées pour les informations d’identification suivantes :

* hôte
* port
* username
* password

Au cours de cette étape, vous pouvez également configurer votre nombre maximal de connexions simultanées, définir votre chemin d’accès au dossier et activer ou désactiver le découpage pour votre serveur [!DNL SFTP]. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** et attendez quelques instants pour établir la connexion.

Pour plus d&#39;informations sur l&#39;authentification, consultez le guide sur la [collecte des informations d&#39;identification requises pour [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![Nouvel écran de compte pour la source SFTP à l’aide de l’authentification de base](../../../../images/tutorials/create/sftp/password.png)

>[!TAB Authentification de clé publique SSH]

Pour utiliser des informations d’identification SSH basées sur des clés publiques, sélectionnez **[!UICONTROL SSH public key]** , puis fournissez les valeurs appropriées pour les informations d’identification suivantes :

* hôte
* port
* username
* contenu de clé privée
* passphrase

Au cours de cette étape, vous pouvez également configurer votre nombre maximal de connexions simultanées, définir votre chemin d’accès au dossier et activer ou désactiver le découpage pour votre serveur [!DNL SFTP]. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]** et attendez quelques instants pour établir la connexion.

Pour plus d&#39;informations sur l&#39;authentification, consultez le guide sur la [collecte des informations d&#39;identification requises pour [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![Nouvel écran de compte pour la source SFTP à l’aide de la clé publique SSH.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte SFTP. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données de votre espace de stockage dans le cloud dans Platform](../../dataflow/batch/cloud-storage.md).
