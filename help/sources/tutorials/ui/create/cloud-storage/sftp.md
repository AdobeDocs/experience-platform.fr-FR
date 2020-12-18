---
keywords: Experience Platform;home;popular topics;SFTP;sftp
solution: Experience Platform
title: Création d’un connecteur source SFTP dans l’interface utilisateur
topic: overview
type: Tutorial
description: Ce didacticiel décrit la procédure à suivre pour créer un connecteur source SFTP à l’aide de l’interface utilisateur de la plate-forme.
translation-type: tm+mt
source-git-commit: 0d0d3aa4213f3a8252de82c47eef6e9caa4d3e9e
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 8%

---


# Création d’un connecteur source SFTP dans l’interface utilisateur

>[!NOTE]
>
>Le connecteur SFTP est en version bêta. Pour plus d&#39;informations sur l&#39;utilisation de connecteurs bêta, consultez l&#39;[Présentation des sources](../../../../home.md#terms-and-conditions).

Ce didacticiel décrit la procédure à suivre pour créer un connecteur source SFTP à l’aide de l’interface utilisateur de la plate-forme.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model (XDM)] Système](../../../../../xdm/home.md) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

>[!IMPORTANT]
>
>Il est recommandé d’éviter les nouvelles lignes ou les retours chariot lors de l’assimilation d’objets JSON avec une connexion source SFTP. Pour contourner cette restriction, utilisez un seul objet JSON par ligne et plusieurs lignes pour les fichiers suivants.

Si vous disposez déjà d’une connexion SFTP valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur [la configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Collecte des informations d’identification requises

Pour vous connecter au protocole SFTP, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `host` | Nom ou adresse IP associé à votre serveur SFTP. |
| `username` | Nom d’utilisateur ayant accès à votre serveur SFTP. |
| `password` | Mot de passe de votre serveur SFTP. |
| `privateKeyContent` | Le contenu de la clé privée SSH codée en Base64. Le format de la clé privée SSH OpenSSH (RSA/DSA). |
| `passPhrase` | Expression de passe ou mot de passe pour déchiffrer la clé privée si le fichier de clé ou le contenu de la clé est protégé par une expression de passe. Si PrivateKeyContent est protégé par un mot de passe, ce paramètre doit être utilisé avec la phrase secrète de PrivateKeyContent comme valeur. |

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer un nouveau compte SFTP pour vous connecter à la plate-forme.

## Connexion à votre serveur SFTP

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com), puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l&#39;espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte entrant.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie [!UICONTROL enregistrement du cloud], sélectionnez **[!UICONTROL SFTP]**. Si vous utilisez ce connecteur pour la première fois, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter les données]** pour créer une nouvelle connexion SFTP.

![catalogue](../../../../images/tutorials/create/sftp/catalog.png)

La page **[!UICONTROL Se connecter à SFTP]** s&#39;affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification. Une fois terminé, sélectionnez **[!UICONTROL Se connecter]**, puis accordez un certain temps à la nouvelle connexion pour établir.

Le connecteur SFTP fournit différents types d’authentification pour l’accès. Sous **[!UICONTROL Authentification du compte]**, sélectionnez **[!UICONTROL Mot de passe]** pour utiliser des informations d’identification basées sur un mot de passe.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

Vous pouvez également sélectionner **[SSH clé publique]** et connecter votre compte SFTP en utilisant une combinaison de [!UICONTROL contenu de clé privée] et [!UICONTROL phrase secrète].

>[!IMPORTANT]
>
>Le connecteur SFTP prend en charge une clé RSA/DSA OpenSSH. Assurez-vous que le contenu de votre fichier clé est début avec `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`. Si le fichier de clé privée est au format PPK, utilisez l&#39;outil PuTTY pour convertir le fichier de clé privée au format OpenSSH.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| Informations d’identification | Description |
| ---------- | ----------- |
| Contenu de clé privée | Contenu de clé privée SSH codée en base 64. La clé privée SSH doit être au format OpenSSH. |
| Passphrase | Indique l’expression de passe ou le mot de passe pour déchiffrer la clé privée si le fichier de clé ou le contenu de la clé est protégé par une expression de passe. Si PrivateKeyContent est protégé par un mot de passe, ce paramètre doit être utilisé avec la phrase secrète de PrivateKeyContent comme valeur. |

### Compte existant

Pour connecter un compte existant, sélectionnez le compte FTP ou SFTP avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/sftp/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte FTP ou SFTP. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer les données de votre enregistrement cloud dans Platform](../../dataflow/batch/cloud-storage.md).