---
keywords: bizible;bizible extension;bizible destination
title: Extension Bizible
seo-title: Extension Bizible
description: L’extension Bizible est une destination de courrier électronique dans la plate-forme de données client en temps réel. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
seo-description: L’extension Bizible est une destination de courrier électronique dans la plate-forme de données client en temps réel. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
translation-type: tm+mt
source-git-commit: 80db19822551883da272787affb6f7dc9dc3a745
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 44%

---


# [!DNL Bizible] Extension {#bizible-extension}

## Présentation {#overview}

[!DNL Bizible] est une solution d’attribution B2B de pointe qui vous offre une visibilité inégalée sur les données, afin que vous puissiez prendre des décisions intelligentes pour stimuler la croissance.

[!DNL Bizible] est une extension de courrier électronique dans la plateforme de données client en temps réel. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101055.bizible-analytics.html).

Cette destination est une [!DNL Adobe Experience Platform Launch] extension. For more information about how [!DNL Platform Launch] extensions work in Real-time CDP, see [Experience Platform Launch extensions overview](../launch-extensions/overview.md).

![Extension Bizible](../../assets/catalog/email/bizible/catalog.png)

## Conditions préalables  {#prerequisites}

This extension is available in the [!DNL Destinations] catalog for all customers who have purchased Real-time CDP.

To use this extension, you need access to [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] est proposé aux clients de Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse. Contact your organization administrator to get access to [!DNL Platform Launch] and ask them to grant you the **[!UICONTROL manage_properties]** permission so you can install extensions.

## Installation de l’extension {#install-extension}

Pour installer l’ [!DNL Bizible] extension :

In the [Real-time CDP interface](http://platform.adobe.com/), go to **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Sélectionnez l’extension dans le catalogue ou utilisez la barre de recherche.

Click on the destination to highlight it, then select **[!UICONTROL Configure]** in the right rail. If the **[!UICONTROL Configure]** control is greyed out, you are missing the **[!UICONTROL manage_properties]** permission. Voir les [Conditions préalables](#prerequisites).

In the **[!UICONTROL Select available Platform Launch property]** window, select the [!DNL Platform Launch] property in which you want to install the extension. Vous pouvez aussi créer une nouvelle propriété dans [!DNL Platform Launch]. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. Pour en savoir plus sur les propriétés, consultez la [section de la page Propriétés](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) de la documentation de [!DNL Launch]

The workflow takes you to [!DNL Platform Launch] to complete the installation.

Pour plus d’informations sur les options de configuration d’extension et la prise en charge de l’installation, consultez la [page Bizible sur Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101055.bizible-analytics.html).

You can also install the extension directly in the [Adobe Experience Platform Launch interface](https://launch.adobe.com/). Consultez la section [Ajout d’une nouvelle extension](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) de la documentation de [!DNL Platform Launch]

## Utilisation de l’extension {#how-to-use}

Une fois que vous avez installé l’extension, vous pouvez commencer à configurer des règles pour cette extension directement dans [!DNL Platform Launch].

In [!DNL Platform Launch], you can set up rules for your installed extensions to send event data to the extension destination only in certain situations. Pour plus d’informations sur la configuration de règles pour vos extensions, consultez la [documentation des règles](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Configuration, mise à niveau et suppression de l’extension {#configure-upgrade-delete}

You can configure, upgrade, and delete extensions in the [!DNL Platform Launch] interface.

>[!TIP]
>
>If the extension is already installed on one of your properties, the Real-time CDP UI still displays **[!UICONTROL Install]** for the extension. Démarrez le workflow d’installation comme décrit dans [Installer l’extension](#install-extension) pour accéder à et configurer ou supprimer votre extension.[!DNL Platform Launch]

Pour mettre à niveau votre extension, consultez la section [Mise à niveau d’extension](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) dans la documentation de [!DNL Platform Launch]