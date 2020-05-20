---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d'un connecteur source Microsoft Dynamics ou Salesforce dans l'interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Création d&#39;un connecteur source Microsoft Dynamics ou Salesforce dans l&#39;interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’importer des données de gestion de la relation client de source externe sur une base planifiée. Ce didacticiel décrit les étapes à suivre pour créer un connecteur source Microsoft Dynamics (ci-après appelé &quot;Dynamics&quot;) ou Salesforce à l&#39;aide de l&#39;interface utilisateur de la plate-forme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)des schémas : Découvrez les éléments de base des schémas XDM, y compris les principes clés et les meilleures pratiques en matière de composition des schémas.
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Découvrez comment créer des schémas personnalisés à l’aide de l’interface utilisateur de l’éditeur de Schémas.
* [Profil](../../../../../profile/home.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d&#39;une connexion de base Microsoft Dynamics ou Salesforce, vous pouvez ignorer le reste de ce document et passer au didacticiel sur la [configuration d&#39;un flux de données](../../dataflow/crm.md).

### Collecte des informations d’identification requises

Pour accéder à votre compte Dynamics sur la plateforme, vous devez fournir un URI **de** service, un nom d&#39; **utilisateur** et un **mot de passe**.

De même, l’accès à votre compte Salesforce sur la plate-forme requiert que vous fournissiez une URL **d’** environnement, un nom d’ **utilisateur**, un **mot de passe** et un jeton **de sécurité.**

## Connecter votre compte Dynamics ou Salesforce

Les informations d&#39;identification de votre système CRM étant prêtes, vous pouvez suivre les étapes ci-dessous pour créer une nouvelle connexion de base entrante afin de lier votre compte Dynamics ou Salesforce à la plateforme.

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail sources. L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer des connexions de base entrantes et chaque source affiche le nombre de connexions de base existantes qui lui sont associées.

Sous la catégorie *CRM* , sélectionnez **Microsoft Dynamics** ou **Salesforce** pour afficher une barre d&#39;informations sur la droite de l&#39;écran. La barre d&#39;informations fournit une brève description de la source sélectionnée ainsi que des options permettant de vue de sa documentation ou de se connecter à la source. Pour créer une connexion de base entrante, cliquez sur **Connexion source**.

![](../../../../images/tutorials/create/salesforce/sf_sources_catalog.png)

Dans le formulaire d&#39;entrée, fournissez la connexion de base avec un nom, une description facultative et vos informations d&#39;identification Dynamics ou Salesforce. Enfin, cliquez sur **Se connecter** , puis accordez un certain temps à la nouvelle connexion de base pour établir.

![](../../../../images/tutorials/create/salesforce/sf_credentials.png)

Une fois qu’une connexion de base avec votre système de gestion de la relation client est établie, vous pouvez passer à la section suivante et configurer un flux de données pour importer les données de gestion de la relation client dans la plate-forme.

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion de base à votre compte Dynamics ou Salesforce. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de données pour importer des données dans la plate-forme](../../dataflow/crm.md).