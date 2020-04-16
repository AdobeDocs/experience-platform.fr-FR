---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source FTP ou SFTP dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Création d’un connecteur source FTP ou SFTP dans l’interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’assimiler des données externes sur une base planifiée. Ce didacticiel décrit la procédure à suivre pour créer un connecteur source FTP ou SFTP à l’aide de l’interface utilisateur de la plate-forme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)de l’éditeur de  : Découvrez comment créer des  personnalisées à l’aide de l’interface utilisateur de l’éditeur de  de.
* [](../../../../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion FTP ou SFTP valide, vous pouvez ignorer le reste de ce et accéder au didacticiel sur la [configuration d’un flux de données](../../dataflow/cloud-storage.md).

### Formats de fichiers pris en charge

Experience Platform prend en charge les formats de fichier suivants pour être assimilés à partir de sources externes :

* Valeurs séparées par des délimiteurs (DSV) : La prise en charge des fichiers de données au format DSV est actuellement limitée aux valeurs séparées par des virgules (CSV). La valeur des en-têtes de champ dans les fichiers au format DSV ne doit être composée que de caractères alphanumériques et de traits de soulignement. Le support de DSV général sera fourni à l’avenir.
* Notation d’objet JavaScript (JSON) : Les fichiers de données au format JSON doivent être compatibles XDM.
* Apache Parquet : Les fichiers de données au format Parquet doivent être conformes XDM.

### Collecte des informations d’identification requises

Pour accéder à votre serveur FTP ou SFTP sur la plateforme, vous devez indiquer le nom **d’** hôte du serveur, un nom **d’** utilisateur et un **mot de passe**.

## Connexion à votre serveur

Les informations d’identification de votre serveur étant prêtes, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre serveur FTP ou SFTP à la plateforme.

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail Sources. L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes, et chaque source indique le nombre de connexions de base existantes qui lui sont associées.

Sous le  de *Cloud* , sélectionnez **FTP** ou **SFTP** pour afficher une barre d’informations sur le côté droit de l’écran. La barre d’informations fournit une brève description de la source sélectionnée, ainsi que des options permettant de  sa documentation ou de se connecter à la source. Pour créer une connexion de base entrante, cliquez sur **Connect source**.

![](../../../../images/tutorials/create/sftp/sftp_sources_catalog.png)

Dans le formulaire d’entrée, indiquez un nom, une description facultative et vos informations d’identification FTP ou SFTP pour la connexion de base. Enfin, cliquez sur **Se connecter** , puis accordez un peu de temps pour que la nouvelle connexion de base soit établie.

![](../../../../images/tutorials/create/sftp/sftp_credentials.png)

Une fois qu’une connexion de base avec votre serveur FTP ou SFTP est établie, vous pouvez passer à la section suivante et configurer un flux de données pour importer des données dans la plateforme.

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre serveur FTP ou SFTP. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/cloud-storage.md).
