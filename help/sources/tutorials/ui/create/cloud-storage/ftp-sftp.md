---
keywords: Experience Platform;home;popular topics;SFTP;FTP;ftp;sftp
solution: Experience Platform
title: Création d’un connecteur source FTP ou SFTP dans l’interface utilisateur
topic: overview
type: Tutorial
description: Ce didacticiel décrit la procédure à suivre pour créer un connecteur source FTP ou SFTP à l’aide de l’interface utilisateur de la plate-forme.
translation-type: tm+mt
source-git-commit: c3352c090ce9e5a89d9285aabdc4851632d4d437
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 9%

---


# Création d’un connecteur source FTP ou SFTP dans l’interface utilisateur

>[!NOTE]
>
>Les connecteurs FTP et SFTP sont en version bêta. Pour plus d’informations sur l’utilisation de connecteurs bêta, consultez l’aperçu [des](../../../../home.md#terms-and-conditions) sources.

Les connecteurs source de Adobe Experience Platform permettent d’importer des données provenant de l’extérieur sur une base planifiée. Ce didacticiel décrit la procédure à suivre pour créer un connecteur source FTP ou SFTP à l’aide de l’interface [!DNL Platform] utilisateur.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [[!DNL Experience Data Model] (XDM) Système](../../../../../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition des schémas](../../../../../xdm/schema/composition.md) : découvrez les blocs de création de base des schémas XDM, y compris les principes clés et les bonnes pratiques en matière de composition de schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [[ !Profil client en temps réel DNL]](../../../../../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion FTP ou SFTP valide, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/batch/cloud-storage.md).

### Formats de fichiers pris en charge

[!DNL Experience Platform] prend en charge les formats de fichier suivants à ingérer à partir de sources externes :

* Valeurs séparées par des délimiteurs (DSV) : La prise en charge des fichiers de données au format DSV est actuellement limitée aux valeurs séparées par des virgules (CSV). La valeur des en-têtes de champ des fichiers au format DSV ne doit être composée que de caractères alphanumériques et de traits de soulignement. Le support de DSV général sera assuré à l&#39;avenir.
* Notation d’objet JavaScript (JSON) : Les fichiers de données au format JSON doivent être compatibles XDM.
* Apache Parquet : Les fichiers de données au format Parquet doivent être conformes à XDM.

### Collecte des informations d’identification requises

Pour accéder à votre serveur FTP ou SFTP sur [!DNL Platform], vous devez indiquer le nom **d’** hôte du serveur, un nom **d’** utilisateur et un **mot de passe**.

## Connexion à votre serveur FTP ou SFTP

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer un compte FTP ou SFTP auquel vous connecter [!DNL Platform].

Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com) , puis sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail **[!UICONTROL Sources]** . L’écran **[!UICONTROL Catalogue]** affiche diverses sources pour lesquelles vous pouvez créer un compte entrant.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous la catégorie **[!UICONTROL Bases de données]** , sélectionnez **[!UICONTROL SFTP]**. Si c’est la première fois que vous utilisez ce connecteur, sélectionnez **[!UICONTROL Configurer]**. Sinon, sélectionnez **[!UICONTROL Ajouter des données]** pour créer un connecteur FTP ou SFTP.

![catalogue](../../../../images/tutorials/create/sftp/catalog.png)

La page **[!UICONTROL Se connecter au protocole SFTP]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Se connecter]** , puis accordez un peu de temps à la nouvelle connexion pour établir.

Le connecteur SFTP fournit différents types d’authentification pour l’accès. Sous Authentification **[!UICONTROL du]** compte, sélectionnez **[!UICONTROL Mot de passe]** pour utiliser des informations d’identification basées sur un mot de passe.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

Vous pouvez également sélectionner la clé **[publique]** SSH et connecter votre compte SFTP à l’aide d’une combinaison de contenu **[!UICONTROL de clé]** privée et de phrase secrète ****.

>[!IMPORTANT]
>
>Le connecteur SFTP prend en charge une clé RSA/DSA OpenSSH. Assurez-vous que le contenu de votre fichier clé s’début `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`. Si le fichier de clé privée est au format PPK, utilisez l&#39;outil PuTTY pour convertir le fichier de clé privée au format OpenSSH.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| Informations d’identification | Description |
| ---------- | ----------- |
| Contenu de clé privée | Contenu de clé privée SSH codée en base 64. La clé privée SSH doit être au format OpenSSH. |
| Passphrase | Indique l’expression de passe ou le mot de passe pour déchiffrer la clé privée si le fichier de clé ou le contenu de la clé est protégé par une expression de passe. Si PrivateKeyContent est protégé par un mot de passe, ce paramètre doit être utilisé avec la phrase secrète de PrivateKeyContent comme valeur. |

### Compte existant

Pour connecter un compte existant, sélectionnez le compte FTP ou SFTP avec lequel vous souhaitez vous connecter, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/sftp/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte FTP ou SFTP. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer [!DNL Platform]](../../dataflow/batch/cloud-storage.md)les données de votre enregistrement cloud.