---
keywords: Experience Platform ; accueil ; rubriques populaires ; SFTP ; sftp
solution: Experience Platform
title: Création d’une connexion à la source SFTP dans l’interface utilisateur
topic: aperçu
type: Tutoriel
description: Découvrez comment créer une connexion source SFTP à l’aide de l’interface utilisateur Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 0e11acc4a599d360cb3048445003f61848ad23d3
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 8%

---


# Création d’une connexion source SFTP dans l’interface utilisateur

Ce didacticiel décrit les étapes à suivre pour créer une connexion source SFTP à l’aide de l’interface utilisateur de Adobe Experience Platform.

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
| `privateKeyContent` | Le contenu de la clé privée SSH codée en Base64. Le type de clé OpenSSH doit être classé RSA ou DSA. |
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
>Le connecteur SFTP prend en charge une clé OpenSSH de type RSA ou DSA. Assurez-vous que le contenu de votre fichier clé est début avec `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` et se termine par `"-----END [RSA/DSA] PRIVATE KEY-----"`. Si le fichier de clé privée est au format PPK, utilisez l&#39;outil PuTTY pour convertir le fichier de clé privée au format OpenSSH.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| Informations d’identification | Description |
| ---------- | ----------- |
| Contenu de clé privée | Le contenu de la clé privée SSH codée en Base64. Le type de clé OpenSSH doit être classé RSA ou DSA. |
| Passphrase | Indique l’expression de passe ou le mot de passe pour déchiffrer la clé privée si le fichier de clé ou le contenu de la clé est protégé par une expression de passe. Si PrivateKeyContent est protégé par un mot de passe, ce paramètre doit être utilisé avec la phrase secrète de PrivateKeyContent comme valeur. |

### Compte existant

Pour connecter un compte existant, sélectionnez le compte FTP ou SFTP avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/sftp/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte FTP ou SFTP. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer les données de votre enregistrement cloud dans Platform](../../dataflow/batch/cloud-storage.md).