---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’un connecteur source OData générique dans l’interface utilisateur
topic: overview
translation-type: tm+mt
source-git-commit: 8c67ba710b486501374020ab505b04931f327c0f

---


# Création d’un connecteur source OData générique dans l’interface utilisateur

Les connecteurs source d’Adobe Experience Platform permettent d’assimiler des données externes sur une base planifiée. Ce didacticiel décrit la procédure à suivre pour créer un connecteur source Open Data Protocol générique (ci-après dénommé &quot;OData&quot;) à l’aide de l’interface utilisateur de la plate-forme.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des composants suivants d’Adobe Experience Platform :

* [Système](../../../../../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plateforme d’expérience organise les données d’expérience client.
   * [Principes de base de la composition](../../../../../xdm/schema/composition.md)de  : Découvrez les éléments de base des  XDM, y compris les principes clés et les bonnes pratiques en matière de composition de .
   * [Didacticiel](../../../../../xdm/tutorials/create-schema-ui.md)de l’éditeur de  : Découvrez comment créer des  personnalisées à l’aide de l’interface utilisateur de l’éditeur de  de.
* [](../../../../../profile/home.md)du client en temps réel : Fournit un client en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.

Si vous disposez déjà d’une connexion OData valide, vous pouvez ignorer le reste de ce et passer au didacticiel sur la [configuration d’un flux de données de jeu de protocoles.](../../dataflow/protocols.md)

### Collecte des informations d’identification requises

Pour accéder à votre compte OData dans Platform, vous devez fournir les valeurs suivantes :

| Informations d’identification | Description |
| ---------- | ----------- |
| `url` | URL racine du service OData. |

Pour plus d’informations sur la prise en main, reportez-vous à [cette](https://www.odata.org/getting-started/basic-tutorial/)OData.

## Connectez votre compte OData

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes ci-dessous pour créer un compte OData afin de vous connecter à la plateforme.

Connectez-vous à <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , puis sélectionnez **Sources** dans la barre de navigation de gauche pour accéder à l’espace de travail *Sources* . L’écran *Catalogue* affiche diverses sources pour lesquelles vous pouvez créer un compte entrant. Chaque source affiche le nombre de comptes et de flux de jeux de données existants qui leur sont associés.

Vous pouvez sélectionner le  approprié dans le catalogue sur le côté gauche de l’écran. Vous pouvez également trouver la source spécifique avec laquelle vous souhaitez travailler à l’aide de l’option de recherche.

Sous le  *Protocoles* , sélectionnez **Générique OData** pour afficher une barre d’informations sur le côté droit de votre écran. La barre d’informations fournit une brève description de la source sélectionnée ainsi que des options permettant de se connecter à la source ou au  sa documentation. Pour créer une connexion entrante, sélectionnez **Connexion source**.

![catalogue](../../../../images/tutorials/create/odata/catalog.png)

La page *Se connecter à OData* générique s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Nouveau compte

Si vous utilisez de nouvelles informations d’identification, sélectionnez **Nouveau compte**. Dans le formulaire d’entrée qui s’affiche, indiquez un nom, une description facultative et vos informations d’identification OData pour la connexion. Lorsque vous avez terminé, sélectionnez **Se connecter** , puis accordez du temps au nouveau compte pour l’établir.

![connecter](../../../../images/tutorials/create/odata/connect.png)

### Compte existant

Pour connecter un compte existant, sélectionnez le compte OData auquel vous souhaitez vous connecter, puis sélectionnez **Suivant** pour continuer.

![existant](../../../../images/tutorials/create/odata/existing.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez établi une connexion à votre compte OData. Vous pouvez maintenant passer au didacticiel suivant et [configurer un flux de jeux de données pour importer les données de protocoles dans Platform](../../dataflow/protocols.md).