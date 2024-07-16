---
Keywords: ECID;ecid
title: Extension du service Experience Cloud ID
description: L’extension du service d’ID Experience Cloud est une destination de personnalisation dans Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
exl-id: 4cc49c14-66ec-43e0-a106-70d9c3646d87
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 40%

---

# Extension [!DNL Experience Cloud] ID Service {#adobe-ecid-extension}

## Vue d’ensemble {#overview}

Cette extension met en oeuvre le service [!DNL Experience Cloud] ID, qui identifie les visiteurs sur toutes les solutions [!DNL Experience Cloud].

[!DNL Experience Cloud] ID Le service est une extension de personnalisation dans Adobe Experience Platform. Pour plus d’informations sur la fonctionnalité de l’extension, consultez la [page d’extension du service d’ID Experience Cloud](../../../tags/extensions/client/id-service/overview.md) dans la documentation sur les balises.

Cette destination est une extension de balise. Pour plus d’informations sur le fonctionnement des extensions de balises dans Platform, consultez la [présentation des extensions de balises](../launch-extensions/overview.md).

![Extension Adobe ECID](../../assets/catalog/personalization/adobe-ecid/catalog.png)

## Conditions préalables  {#prerequisites}

Cette extension est disponible dans le catalogue des destinations pour tous les clients qui ont acheté Platform.

Pour utiliser cette extension, vous devez accéder aux balises dans Platform. Les balises sont proposées aux clients Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse. Contactez l’administrateur de votre organisation pour accéder à l’interface utilisateur de la collecte de données et demandez-lui de vous accorder l’autorisation **[!UICONTROL manage_properties]** afin que vous puissiez installer des extensions.

## Installation l’extension {#install-extension}

Pour installer l’extension [!DNL Experience Cloud] ID Service :

Dans l’[interface de Platform](https://platform.adobe.com/), accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**.

Sélectionnez l’extension dans le catalogue ou utilisez la barre de recherche.

Cliquez sur la destination pour la mettre en surbrillance, puis sélectionnez **[!UICONTROL Configurer]** dans le rail droit. Si la commande **[!UICONTROL Configurer]** est grisée, vous ne disposez pas de l’autorisation **[!UICONTROL manage_properties]**. Voir les [Conditions préalables](#prerequisites).

Sélectionnez la propriété de balise dans laquelle vous souhaitez installer l’extension. Vous pouvez aussi créer une propriété. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. Découvrez les propriétés dans la [documentation sur les balises](../../../tags/ui/administration/companies-and-properties.md).

Le workflow vous permet d’accéder à l’interface utilisateur de collecte de données pour terminer l’installation.

Pour plus d’informations sur les options de configuration de l’extension et la prise en charge de l’installation, consultez la [page d’extension du service d’ID Experience Cloud](../../../tags/extensions/client/id-service/overview.md) dans la documentation des balises.

Vous pouvez également installer l’extension directement dans l’[interface utilisateur de la collecte de données](https://experience.adobe.com/#/data-collection/). Pour plus d’informations, consultez le guide sur l’ [ajout d’une nouvelle extension](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) .

## Utilisation de l’extension {#how-to-use}

Une fois que vous avez installé l’extension, vous pouvez commencer à configurer des règles. Dans l’interface utilisateur de collecte de données, vous pouvez configurer des règles pour vos extensions installées afin d’envoyer des données d’événement vers la destination de l’extension uniquement dans certains cas. Pour plus d’informations sur la configuration des règles pour vos extensions, consultez la présentation des [règles](../../../tags/ui/managing-resources/rules.md) dans la documentation sur les balises.

## Configuration, mise à niveau et suppression de l’extension {#configure-upgrade-delete}

Vous pouvez configurer, mettre à niveau et supprimer des extensions dans l’interface utilisateur de collecte de données.

>[!TIP]
>
>Si l’extension est déjà installée sur l’une de vos propriétés, l’interface utilisateur affiche toujours **[!UICONTROL Install]** pour l’extension. Démarrez le workflow d’installation comme décrit dans [Installation de l’extension](#install-extension) pour configurer ou supprimer votre extension.

Pour mettre à niveau votre extension, consultez le guide sur le [processus de mise à niveau d’extension](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) dans la documentation sur les balises.
