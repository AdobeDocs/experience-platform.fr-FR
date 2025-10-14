---
keywords: Advertising Cloud;extension advertising cloud;destination advertising cloud
title: Extension Adobe Advertising Cloud
description: L’extension Adobe Advertising Cloud est une destination publicitaire dans Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
exl-id: 3415a85f-5678-4f5b-b7cf-e185a66d084f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 42%

---

# Extension Adobe Advertising Cloud {#adobe-advertising-cloud-extension}

## Vue d’ensemble {#overview}

Il s’agit de l’extension [!DNL Advertising Cloud] pour l’implémentation de [!DNL Advertising Cloud] balises de conversion et d’audience pour DSP et Search (DCO n’est actuellement pas pris en charge).

Adobe Advertising Cloud est une extension publicitaire dans Adobe Experience Platform.

Cette destination est une extension de balise. Pour plus d’informations sur le fonctionnement des extensions de balises dans Experience Platform, consultez la [&#x200B; présentation des extensions de balises](../launch-extensions/overview.md).

![Extension Adobe Advertising Cloud](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## Conditions préalables  {#prerequisites}

Cette extension est disponible dans le catalogue des destinations pour tous les clients qui ont acheté Experience Platform.

Pour utiliser cette extension, vous devez accéder aux balises dans Experience Platform. Les balises sont proposées aux clients Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse. Contactez l’administrateur ou l’administratrice de votre organisation pour accéder aux fonctionnalités de collecte de données dans l’interface utilisateur et demandez-lui de vous accorder l’autorisation **[!UICONTROL manage_properties]** afin que vous puissiez installer les extensions.

## Installation l’extension {#install-extension}

Pour installer l’extension Adobe Advertising Cloud :

Dans l’interface [Experience Platform](https://platform.adobe.com/), accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**.

Sélectionnez l’extension dans le catalogue ou utilisez la barre de recherche.

Cliquez sur la destination pour la mettre en surbrillance, puis sélectionnez **[!UICONTROL Configurer]** dans le rail droit. Si la commande **[!UICONTROL Configurer]** est grisée, vous ne disposez pas de l’autorisation **[!UICONTROL manage_properties]**. Voir les [Conditions préalables](#prerequisites).

Sélectionnez la propriété de balise dans laquelle vous souhaitez installer l’extension. Vous pouvez aussi créer une propriété. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. Pour en savoir plus sur les propriétés, consultez la [documentation sur les balises](../../../tags/ui/administration/companies-and-properties.md).

Le workflow vous mène à l’interface utilisateur de la collecte de données pour terminer l’installation.

Vous pouvez également installer l’extension directement dans l’[interface utilisateur de la collecte de données](https://experience.adobe.com/#/data-collection/). Pour plus d’informations, consultez le guide sur [l’ajout d’une nouvelle extension](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension).

## Utilisation de l’extension {#how-to-use}

Une fois l’extension installée, vous pouvez commencer à configurer des règles. Dans l’interface utilisateur de la collecte de données, vous pouvez configurer des règles pour vos extensions installées afin d’envoyer des données d’événement vers la destination de l’extension uniquement dans certains cas. Pour plus d’informations sur la configuration de règles pour vos extensions, consultez la présentation de [rules](../../../tags/ui/managing-resources/rules.md) dans la documentation sur les balises.

## Configuration, mise à niveau et suppression de l’extension {#configure-upgrade-delete}

Vous pouvez configurer, mettre à niveau et supprimer des extensions dans l’interface utilisateur de collecte de données.

>[!TIP]
>
>Si l’extension est déjà installée sur l’une de vos propriétés, l’interface utilisateur affiche toujours **[!UICONTROL Installer]** pour l’extension. Démarrez le workflow d’installation comme décrit dans [Installation de l’extension](#install-extension) pour configurer ou supprimer votre extension.

Pour mettre à niveau votre extension, consultez le guide sur le [processus de mise à niveau d’extension](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) dans la documentation sur les balises.
