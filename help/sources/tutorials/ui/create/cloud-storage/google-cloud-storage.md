---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur  source de Google Cloud  dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Création d’un connecteur  source de Google Cloud  dans l’interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’assimiler des données externes sur une base planifiée. Ce didacticiel décrit la procédure à suivre pour créer un connecteur source  Google Cloud (ci-après dénommé &quot;connecteur GCS&quot;) à l’aide de l’interface utilisateur de la plateforme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)de l’éditeur de  : Découvrez comment créer des  personnalisées à l’aide de l’interface utilisateur de l’éditeur de  de.
* [](../../../../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion de base GCS, vous pouvez ignorer le reste de ce et passer au didacticiel sur la [configuration d’un flux de données](../../dataflow/cloud-storage.md).

### Formats de fichiers pris en charge

Experience Platform prend en charge les formats de fichier suivants pour être assimilés à partir d’un  externe  :

* Valeurs séparées par des délimiteurs (DSV) : La prise en charge des fichiers de données au format DSV est actuellement limitée aux valeurs séparées par des virgules. La valeur des en-têtes de champ dans les fichiers au format DSV ne doit être composée que de caractères alphanumériques et de traits de soulignement. La prise en charge des fichiers DSV généraux sera assurée à l’avenir.
* Notation d’objet JavaScript (JSON) : Les fichiers de données au format JSON doivent être compatibles XDM.
* Apache Parquet : Les fichiers de données au format Parquet doivent être conformes XDM.

### Collecte des informations d’identification requises

Pour accéder à vos données GCS sur la plateforme, vous devez fournir un ID **de clé d&#39;** accès GCS valide et un **secret**. Pour en savoir plus sur la manière d’obtenir ces valeurs, consultez le guide <a href="https://cloud.google.com/docs/authentication/production" target="_blank">d’authentification</a> serveur à serveur pour Google Cloud.

## Connectez votre compte GCS

Une fois que vous avez rassemblé vos informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre compte GCS à la plateforme.

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes, et chaque source indique le nombre de connexions de base existantes qui lui sont associées.

Sous l’ de *Cloud* , sélectionnez le **** Google Cloud pour exposer une barre d’informations sur le côté droit de votre écran. La barre d’informations fournit une brève description de la source sélectionnée, ainsi que des options permettant de se connecter au source  sa documentation ou de se connecter à la source. Pour créer une connexion de base entrante, cliquez sur **Connect source**.

![](../../../../images/tutorials/create/google-cloud-storage/sources-catalog.png)

La boîte de dialogue _Se connecter à Google Cloud_ s’affiche. Dans le formulaire d’entrée, indiquez un nom, une description facultative et vos informations d’identification GCS pour la connexion de base. Lorsque vous avez terminé, cliquez sur **Se connecter** , puis accordez un peu de temps pour que la nouvelle connexion de base soit établie.

![](../../../../images/tutorials/create/google-cloud-storage/gcs-credentials.png)

Une fois une connexion de base établie, vous pouvez passer à la section suivante et configurer un flux de données pour importer des données dans Platform.

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion de base à votre compte GCS. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/cloud-storage.md).