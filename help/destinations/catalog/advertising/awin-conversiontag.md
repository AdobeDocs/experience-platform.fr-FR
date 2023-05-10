---
keywords: Extension Awin Advertiser Conversion Tag;balise de conversion;Awin;awin;AWIN
title: Extension Awin Advertiser Conversion Tag
description: L’extension Awin Advertiser Conversion Tag est une destination publicitaire dans Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
exl-id: 99feb169-acf3-4e68-8785-3f4cf565e5a9
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 63%

---

# Extension Awin Advertiser Conversion Tag {#awin-conversiontag-extension}

## Présentation {#overview}

Conversion Tag est la déclaration de l’objet JavaScript AWIN.Tracking.Sale qui est réalisé sur la page de confirmation pour informer le Mastertag qu’une conversion a eu lieu. À la suite de cela, les requêtes de suivi nécessaires seront réalisées.

Awin Advertiser Conversion Tag est une extension publicitaire de Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html).

Cette destination est une extension de balise. Pour plus d’informations sur le fonctionnement des extensions de balises dans Platform, voir [Présentation des extensions de balise](../launch-extensions/overview.md).

![Extension Awin Advertiser Conversiontag dans l’interface utilisateur](../../assets/catalog/advertising/awin-conversion-tag/catalog.png)

## Conditions préalables  {#prerequisites}

Cette extension est disponible dans le catalogue des destinations pour tous les clients qui ont acheté Platform.

Pour utiliser cette extension, vous devez avoir accès aux balises dans Platform. Les balises sont proposées aux clients Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse. Contactez l’administrateur de votre organisation pour accéder aux fonctionnalités de collecte de données de l’interface utilisateur et demandez-lui de vous accorder la variable **[!UICONTROL manage_properties]** pour pouvoir installer des extensions.

## Installation l’extension {#install-extension}

Pour installer le [!DNL Awin Advertiser Conversion Tag] extension :

Dans l’[interface de Platform](https://platform.adobe.com/), accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**.

Sélectionnez l’extension dans le catalogue ou utilisez la barre de recherche.

Cliquez sur la destination pour la mettre en surbrillance, puis sélectionnez **[!UICONTROL Configurer]** dans le rail droit. Si la commande **[!UICONTROL Configurer]** est grisée, vous ne disposez pas de l’autorisation **[!UICONTROL manage_properties]**. Voir les [Conditions préalables](#prerequisites).

Sélectionnez la propriété de balise dans laquelle vous souhaitez installer l’extension. Vous pouvez aussi créer une propriété. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. En savoir plus sur les propriétés dans [documentation sur les balises](../../../tags/ui/administration/companies-and-properties.md).

Le workflow vous permet d’accéder à l’interface utilisateur de collecte de données pour terminer l’installation.

Pour plus d’informations sur les options de configuration de l’extension et la prise en charge de l’installation, voir la [page Awin Advertiser Conversion Tag sur Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html).

Vous pouvez également installer l’extension directement dans l’[interface utilisateur de la collecte de données](https://experience.adobe.com/#/data-collection/). Consultez le guide sur la [ajout d’une nouvelle extension](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) pour plus d’informations.


## Utilisation de l’extension {#how-to-use}

Une fois que vous avez installé l’extension, vous pouvez commencer à configurer des règles. Dans l’interface utilisateur de collecte de données, vous pouvez configurer des règles pour vos extensions installées afin d’envoyer des données d’événement vers la destination de l’extension uniquement dans certains cas. Pour plus d’informations sur la configuration de règles pour vos extensions, consultez la présentation de [rules](../../../tags/ui/managing-resources/rules.md) dans la documentation sur les balises.

## Configuration, mise à niveau et suppression de l’extension {#configure-upgrade-delete}

Vous pouvez configurer, mettre à niveau et supprimer des extensions dans l’interface utilisateur de collecte de données.

>[!TIP]
>
>Si l’extension est déjà installée sur l’une de vos propriétés, l’interface utilisateur de continue d’afficher **[!UICONTROL Installer]** pour cette extension. Démarrez le workflow d’installation comme décrit dans [Installation de l’extension](#install-extension) pour configurer ou supprimer votre extension.

Pour mettre à niveau votre extension, consultez le guide sur le [processus de mise à niveau d’extension](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) dans la documentation sur les balises.
