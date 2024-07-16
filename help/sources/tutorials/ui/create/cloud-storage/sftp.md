---
title: Création d’une connexion Source SFTP dans l’interface utilisateur
description: Découvrez comment créer une connexion source SFTP à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: f6d1cc811378f2f37968bf0a42b428249e52efd8
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 21%

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

Pour vous connecter à [!DNL SFTP], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Nom ou adresse IP associé à votre serveur [!DNL SFTP]. |
| `port` | Port du serveur [!DNL SFTP] auquel vous vous connectez. Si elle n’est pas fournie, la valeur par défaut est `22`. |
| `username` | Nom d’utilisateur ayant accès à votre serveur [!DNL SFTP]. |
| `password` | Mot de passe de votre serveur [!DNL SFTP]. |
| `privateKeyContent` | Contenu de clé privée SSH codée en Base64. Le type de clé OpenSSH doit être classé en tant que RSA ou DSA. |
| `passPhrase` | L’expression de passe ou le mot de passe pour déchiffrer la clé privée si le fichier de clé ou le contenu de la clé est protégé par une expression de passe. Si PrivateKeyContent est protégé par mot de passe, ce paramètre doit être utilisé avec comme valeur le mot de passe de PrivateKeyContent. |
| `maxConcurrentConnections` | Ce paramètre vous permet de spécifier une limite maximale pour le nombre de connexions simultanées que Platform va créer lors de la connexion à votre serveur SFTP. Vous devez définir cette valeur sur une valeur inférieure à la limite définie par SFTP. **Remarque** : lorsque ce paramètre est activé pour un compte SFTP existant, il n’affecte que les flux de données futurs et non les flux de données existants. |
| Chemin du dossier | Chemin d’accès au dossier auquel vous souhaitez accorder l’accès. [!DNL SFTP] source, vous pouvez fournir le chemin du dossier pour spécifier l’accès de l’utilisateur au sous-dossier de votre choix. |

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer un compte [!DNL SFTP] à connecter à Platform.

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

Pour utiliser une authentification de base, sélectionnez **[!UICONTROL Password]** , puis fournissez les valeurs d’hôte et de port auxquelles se connecter, ainsi que votre nom d’utilisateur et votre mot de passe. Au cours de cette étape, vous pouvez également désigner le chemin d’accès au sous-dossier auquel vous souhaitez accorder l’accès. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]**.

![Nouvel écran de compte pour la source SFTP à l’aide de l’authentification de base](../../../../images/tutorials/create/sftp/password.png)

>[!TAB Authentification de clé publique SSH]

Pour utiliser des informations d’identification SSH basées sur des clés publiques, sélectionnez **[!UICONTROL SSH public key]** , puis fournissez vos valeurs d’hôte et de port, ainsi que votre combinaison de contenu de clé privée et de mot de passe. Au cours de cette étape, vous pouvez également désigner le chemin d’accès au sous-dossier auquel vous souhaitez accorder l’accès. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]**.

![Nouvel écran de compte pour la source SFTP à l’aide de la clé publique SSH.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte SFTP. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données de votre espace de stockage dans le cloud dans Platform](../../dataflow/batch/cloud-storage.md).
