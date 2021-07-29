---
Keywords: ECID;ecid
title: Extension du service Experience Cloud ID
description: L’extension du service d’ID Experience Cloud est une destination de personnalisation dans Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
exl-id: 4cc49c14-66ec-43e0-a106-70d9c3646d87
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 14%

---

# [!DNL Experience Cloud] Extension du service d’ID {#adobe-ecid-extension}

## Présentation {#overview}

Cette extension met en oeuvre le service [!DNL Experience Cloud] ID qui identifie les visiteurs à l’échelle de toutes les solutions [!DNL Experience Cloud].

[!DNL Experience Cloud] Le service d’ID est une extension de personnalisation de Adobe Experience Platform. Pour plus d’informations sur la fonctionnalité de l’extension, consultez la [page de l’extension du service d’ID Experience Cloud](../../../tags/extensions/web/id-service/overview.md) dans la documentation des balises.

Cette destination est une extension de balise. Pour plus d’informations sur le fonctionnement des extensions de balises dans Platform, consultez la [présentation des extensions de balise](../launch-extensions/overview.md).

![Extension Adobe ECID](../../assets/catalog/personalization/adobe-ecid/catalog.png)

## Conditions préalables  {#prerequisites}

Cette extension est disponible dans le catalogue des destinations pour tous les clients qui ont acheté Platform.

Pour utiliser cette extension, vous devez accéder aux balises dans Platform. Les balises sont proposées aux clients Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse. Contactez l’administrateur de votre organisation pour accéder à l’interface utilisateur de la collecte de données et demandez-lui de vous accorder l’autorisation **[!UICONTROL manage_properties]** afin que vous puissiez installer des extensions.

## Installation de l’extension {#install-extension}

Pour installer l’extension du service d’ID [!DNL Experience Cloud] :

Dans l’ [interface de Platform](http://platform.adobe.com/), accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**.

Sélectionnez l’extension dans le catalogue ou utilisez la barre de recherche.

Cliquez sur la destination pour la mettre en surbrillance, puis sélectionnez **[!UICONTROL Configurer]** dans le rail de droite. Si le contrôle **[!UICONTROL Configure]** est grisé, vous ne disposez pas de l’autorisation **[!UICONTROL manage_properties]**. Voir les [Conditions préalables](#prerequisites).

Sélectionnez la propriété de balise dans laquelle vous souhaitez installer l’extension. Vous avez également la possibilité de créer une propriété. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. Découvrez les propriétés dans la [documentation sur les balises](../../../tags/ui/administration/companies-and-properties.md).

Le workflow vous permet d’accéder à l’interface utilisateur de collecte de données pour terminer l’installation.

Pour plus d’informations sur les options de configuration de l’extension et la prise en charge de l’installation, consultez la [page de l’extension du service d’ID Experience Cloud](../../../tags/extensions/web/id-service/overview.md) dans la documentation des balises.

Vous pouvez également installer l’extension directement dans l’ [interface utilisateur de collecte de données](https://experience.adobe.com/#/data-collection/). Pour plus d’informations, consultez le guide sur l’[ajout d’une nouvelle extension](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) .

## Utilisation de l’extension {#how-to-use}

Une fois que vous avez installé l’extension, vous pouvez commencer à configurer des règles. Dans l’interface utilisateur de collecte de données, vous pouvez configurer des règles pour vos extensions installées afin d’envoyer des données d’événement vers la destination de l’extension uniquement dans certains cas. Pour plus d’informations sur la configuration des règles pour vos extensions, consultez la présentation des [règles](../../../tags/ui/managing-resources/rules.md) dans la documentation des balises.

## Configuration, mise à niveau et suppression de l’extension {#configure-upgrade-delete}

Vous pouvez configurer, mettre à niveau et supprimer des extensions dans l’interface utilisateur de la collecte de données.

>[!TIP]
>
>Si l’extension est déjà installée sur l’une de vos propriétés, l’interface utilisateur affiche toujours **[!UICONTROL Install]** pour l’extension. Lancez le workflow d’installation comme décrit dans la section [Installer l’extension](#install-extension) pour configurer ou supprimer votre extension.

Pour mettre à niveau votre extension, consultez le guide sur le [processus de mise à niveau de l’extension](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) dans la documentation sur les balises.
