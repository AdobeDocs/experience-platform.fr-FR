---
keywords: Experience Platform;accueil;rubriques les plus consultées;SFTP;sftp
solution: Experience Platform
title: Création d’une connexion source SFTP dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Découvrez comment créer une connexion source SFTP à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: ade0da445b18108a7f8720404cc7a65139ed42b1
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 6%

---

# Création d’une connexion source [!DNL SFTP] dans l’interface utilisateur

Ce tutoriel décrit les étapes à suivre pour créer une connexion source [!DNL SFTP] à l’aide de l’interface utilisateur de Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension pratique des composants suivants de Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Tutoriel](../../../../../xdm/tutorials/create-schema-ui.md) de l’éditeur de schémas : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

>[!IMPORTANT]
>
>Il est recommandé d’éviter les nouvelles lignes ou les retours chariot lors de l’ingestion d’objets JSON avec une connexion source [!DNL SFTP]. Pour contourner cette limitation, utilisez un seul objet JSON par ligne et plusieurs lignes pour les fichiers qui s’ensuivent.

Si vous disposez déjà d’une connexion [!DNL SFTP] valide, vous pouvez ignorer le reste de ce document et passer au tutoriel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecte des informations d’identification requises

Pour vous connecter à [!DNL SFTP], vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Credential | Description |
| ---------- | ----------- |
| `host` | Nom ou adresse IP associé à votre serveur [!DNL SFTP]. |
| `port` | Port du serveur [!DNL SFTP] auquel vous vous connectez. Si elle n’est pas fournie, la valeur est définie par défaut sur `22`. |
| `username` | Nom d’utilisateur ayant accès à votre serveur [!DNL SFTP]. |
| `password` | Mot de passe de votre serveur [!DNL SFTP]. |
| `privateKeyContent` | Contenu de clé privée SSH codée en Base64. Le type de clé OpenSSH doit être classé en tant que RSA ou DSA. |
| `passPhrase` | L’expression de passe ou le mot de passe pour déchiffrer la clé privée si le fichier de clé ou le contenu de la clé est protégé par une expression de passe. Si PrivateKeyContent est protégé par mot de passe, ce paramètre doit être utilisé avec comme valeur le mot de passe de PrivateKeyContent. |

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer un nouveau compte [!DNL SFTP] à connecter à Platform.

## Connectez-vous à votre serveur [!DNL SFTP]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte entrant.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Dans la catégorie [!UICONTROL Stockage dans le cloud], sélectionnez **[!UICONTROL SFTP]**, puis **[!UICONTROL Ajouter des données]**.

![catalogue](../../../../images/tutorials/create/sftp/catalog.png)

La page **[!UICONTROL Se connecter à SFTP]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour connecter un compte existant, sélectionnez le compte FTP ou SFTP avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/sftp/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom et une description facultative de votre nouveau compte [!DNL SFTP].

#### Authentification avec mot de passe

[!DNL SFTP] prend en charge différents types d’authentification pour l’accès. Sous **[!UICONTROL Authentification du compte]**, sélectionnez **[!UICONTROL Mot de passe]**, puis indiquez les valeurs d’hôte et de port auxquelles se connecter, ainsi que votre nom d’utilisateur et votre mot de passe.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

#### Authentification à l’aide de la clé publique SSH

Pour utiliser des informations d’identification SSH basées sur des clés publiques, sélectionnez **[!UICONTROL SSH public key]** , puis fournissez les valeurs d’hôte et de port, ainsi que votre combinaison de contenu de clé privée et de mot de passe.

>[!IMPORTANT]
>
>SFTP prend en charge une clé OpenSSH de type RSA ou DSA. Assurez-vous que le contenu de votre fichier clé commence par `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` et se termine par `"-----END [RSA/DSA] PRIVATE KEY-----"`. Si le fichier de clé privée est un fichier au format PPK, utilisez l’outil PuTTY pour effectuer une conversion de PPK au format OpenSSH.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh-public-key.png)

| Credential | Description |
| ---------- | ----------- |
| Contenu de clé privée | Contenu de clé privée SSH codée en Base64. Le type de clé OpenSSH doit être classé en tant que RSA ou DSA. |
| Passphrase | Indique l’expression de passe ou le mot de passe pour déchiffrer la clé privée si le fichier de clé ou le contenu de la clé est protégé par une expression de passe. Si PrivateKeyContent est protégé par mot de passe, ce paramètre doit être utilisé avec le mot de passe de PrivateKeyContent comme valeur. |


## Étapes suivantes

En suivant ce tutoriel, vous avez établi une connexion à votre compte SFTP. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer les données de votre espace de stockage dans le cloud dans Platform](../../dataflow/batch/cloud-storage.md).
