---
keywords: Google Global Site Tag;gtag;google gtag;extension google;extension google gtag;GTAG
title: Extension Google Global Site Tag
description: L’extension Google Global Site Tag est une destination d’analyse de Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
exl-id: 9643adc5-997d-45b3-a2b6-e365164022b8
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 28%

---

# [!DNL Google Global Site Tag] Extension {#gtag-analytics-extension}

## Présentation {#overview}

Envoyez des données à [!DNL Google Analytics], [!DNL Google Ads] et à [!DNL Google Marketing Platform] par l’intermédiaire de [!DNL Google's Global Site Tag] ou de gtag.js. Il est possible de configurer plusieurs comptes par produit.

[!DNL Google Global Site Tag] est une extension d’analyse dans Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101437.google-global-site-tag-gtag.html).

Cette destination est une extension Adobe Experience Platform Launch. Pour plus d’informations sur le fonctionnement des extensions de Platform launch dans Platform, voir [Présentation des extensions Adobe Experience Platform Launch](../launch-extensions/overview.md).

![Extension Google Global Site Tag](../../assets/catalog/analytics/gtag-analytics/catalog.png)

## Conditions préalables  {#prerequisites}

Cette extension est disponible dans le catalogue [!DNL Destinations] pour tous les clients qui ont acheté Platform.

Pour utiliser cette extension, vous devez accéder à Adobe Experience Platform Launch.  Platform Launch est une fonctionnalité gratuite intégrée à Adobe Experience Cloud. Contactez l’administrateur de votre organisation pour accéder à Platform launch et demandez-lui de vous accorder l’autorisation **[!UICONTROL manage_properties]** afin que vous puissiez installer les extensions.

## Installation de l’extension {#install-extension}

Pour installer l’extension [!DNL Google Global Site Tag] :

Dans l’ [interface de Platform](http://platform.adobe.com/), accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**.

Sélectionnez l’extension dans le catalogue ou utilisez la barre de recherche.

Cliquez sur la destination pour la mettre en surbrillance, puis sélectionnez **[!UICONTROL Configurer]** dans le rail de droite. Si le contrôle **[!UICONTROL Configure]** est grisé, vous ne disposez pas de l’autorisation **[!UICONTROL manage_properties]**. Voir les [Conditions préalables](#prerequisites).

Dans la fenêtre **[!UICONTROL Sélectionner la propriété de Platform launch disponible]** , sélectionnez la propriété de Platform launch dans laquelle vous souhaitez installer l’extension. Vous avez également la possibilité de créer une propriété dans Platform launch. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. Découvrez les propriétés dans la [section de la page Propriétés](../../../tags/ui/administration/companies-and-properties.md#properties-page) de la documentation du Platform launch.

Le workflow vous permet de réaliser l’installation par Platform launch.

Pour plus d’informations sur les options de configuration de l’extension, consultez la page [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101437.google-global-site-tag-gtag.html) concernant l’extension.

Vous pouvez également installer l’extension directement dans l’[interface Adobe Experience Platform Launch](https://launch.adobe.com/). Voir [Ajouter une nouvelle extension](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) dans la documentation du Platform launch.

## Utilisation de l’extension {#how-to-use}

Une fois que vous avez installé l’extension, vous pouvez commencer à configurer des règles pour celle-ci directement dans Platform launch.

Dans Platform launch, vous pouvez configurer des règles pour vos extensions installées afin d’envoyer des données d’événement vers la destination de l’extension uniquement dans certains cas. Pour plus d’informations sur la configuration de règles pour vos extensions, consultez la [documentation des règles](../../../tags/ui/managing-resources/rules.md).

## Configuration, mise à niveau et suppression de l’extension {#configure-upgrade-delete}

Vous pouvez configurer, mettre à niveau et supprimer des extensions dans l’interface de Platform launch.

>[!TIP]
>
>Si l’extension est déjà installée sur l’une de vos propriétés, l’interface utilisateur de Platform affiche toujours **[!UICONTROL Install]** pour l’extension. Lancez le workflow d’installation comme décrit dans la section [Installer l’extension](#install-extension) pour accéder au Platform launch et configurer ou supprimer votre extension.

Pour mettre à niveau votre extension, voir [Mise à niveau de l’extension](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) dans la documentation du Platform launch.
