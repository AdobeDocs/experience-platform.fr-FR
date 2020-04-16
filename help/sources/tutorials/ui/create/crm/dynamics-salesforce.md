---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source Microsoft Dynamics ou Salesforce dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Création d’un connecteur source Microsoft Dynamics ou Salesforce dans l’interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’assimiler des données de gestion de la relation client de source externe sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source Microsoft Dynamics (ci-après dénommé &quot;Dynamics&quot;) ou Salesforce à l’aide de l’interface utilisateur de la plate-forme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)de l’éditeur de  : Découvrez comment créer des  personnalisées à l’aide de l’interface utilisateur de l’éditeur de  de.
* [](../../../../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d&#39;une connexion de base Microsoft Dynamics ou Salesforce, vous pouvez ignorer le reste de ce et passer au didacticiel sur la [configuration d&#39;un flux de données](../../dataflow/crm.md).

### Collecte des informations d’identification requises

Pour accéder à votre compte Dynamics sur la plateforme, vous devez fournir un URI **de** service, un **nom d’utilisateur** et un **mot de passe**.

De même, pour accéder à votre compte Salesforce sur la plateforme, vous devez fournir une URL **de**, un nom d’ **utilisateur**, un **mot de passe** et un jeton de **sécurité.**

## Connectez votre compte Dynamics ou Salesforce.

Les informations d’identification de votre système CRM étant prêtes, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre compte Dynamics ou Salesforce à la plateforme.

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail Sources. L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes, et chaque source indique le nombre de connexions de base existantes qui lui sont associées.

Sous le *CRM* , sélectionnez **Microsoft Dynamics** ou **Salesforce** pour afficher une barre d’informations sur le côté droit de votre écran. La barre d’informations fournit une brève description de la source sélectionnée, ainsi que des options permettant de  sa documentation ou de se connecter à la source. Pour créer une connexion de base entrante, cliquez sur **Connect source**.

![](../../../../images/tutorials/create/salesforce/sf_sources_catalog.png)

Dans le formulaire d’entrée, indiquez un nom, une description facultative et vos informations d’identification Dynamics ou Salesforce pour la connexion de base. Enfin, cliquez sur **Se connecter** , puis accordez un peu de temps pour que la nouvelle connexion de base soit établie.

![](../../../../images/tutorials/create/salesforce/sf_credentials.png)

Une fois qu’une connexion de base avec votre système de gestion de la relation client est établie, vous pouvez passer à la section suivante et configurer un flux de données pour importer les données de gestion de la relation client dans Platform.

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion de base à votre compte Dynamics ou Salesforce. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans Platform](../../dataflow/crm.md).