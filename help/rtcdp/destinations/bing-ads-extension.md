---
keywords: bing;bing ads event tracking;event tracking bing;UET;UET extension
title: Extension Bing Ads Universal Event Tracking (UET)
seo-title: Extension Bing Ads Universal Event Tracking (UET)
description: L’extension Bing Ads Universal Event Tracking (UET) est une destination publicitaire de la plateforme de données clients en temps réel d’Adobe. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
seo-description: L’extension Bing Ads Universal Event Tracking (UET) est une destination publicitaire de la plateforme de données clients en temps réel d’Adobe. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
translation-type: tm+mt
source-git-commit: 0f6939e131a67568e9002fc37e7b15859c6412b4
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 66%

---


# [!DNL Bing Ads Universal Event Tracking] (UET) extension {#bing-ads-extension}

## Présentation {#overview}

[!DNL Bing Ads Universal Event Tracking] (UET) [!DNL Experience Platform Launch] est un moyen utile de suivre ce qui se passe après que quelqu&#39;un a cliqué sur votre publicité de recherche. Utilisez une simple balise UET pour enregistrer ce que font les consommateurs sur votre site web et exploitez ces données pour suivre les conversions et cibler des audiences à l’aide de listes de remarketing.

[!DNL Bing Ads Universal Event Tracking] (UET) est une extension de publicité dans la plateforme de données client en temps réel Adobe. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100154.html).

Cette destination est une [!DNL Experience Platform Launch] extension. For more information about how [!DNL Launch] extensions work in Adobe Real-time CDP, see [Experience Platform Launch extensions overview](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

![Extension Bing Ads](assets/bing-ads-extension.png)


## Conditions préalables  {#prerequisites}

This extension is available in the [!DNL Destinations] catalog for all customers who have purchased Adobe Real-time CDP.

To use this extension, you need access to [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] est proposé aux clients de Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse. Contact your organization administrator to get access to [!DNL Launch] and ask them to grant you the **[!UICONTROL manage_properties]** permission so you can install extensions.

## Installation de l’extension {#install-extension}

To install the [!DNL Bing Ads Universal Event Tracking] (UET) extension:

1. In the [Adobe Real-time CDP interface](http://platform.adobe.com/), go to **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
2. Sélectionnez l’extension dans le catalogue ou utilisez la barre de recherche.
3. Click on the destination to highlight it, then select **[!UICONTROL Configure]** in the right rail. If the **[!UICONTROL Configure]** control is greyed out, you are missing the **[!UICONTROL manage_properties]** permission. Voir les [Conditions préalables](#prerequisites).
4. Dans la fenêtre **[!UICONTROL Sélectionner la propriété disponible]**, sélectionnez la propriété Launch dans laquelle vous souhaitez installer l’extension. [!DNL Launch] Vous pouvez aussi créer une nouvelle propriété dans [!DNL Launch]. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. Pour en savoir plus sur les propriétés, consultez la [section de la page Propriétés](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/admin/companies-and-properties.html#properties-page) de la documentation de [!DNL Launch]
5. The workflow takes you to [!DNL Launch] to complete the installation.

Pour plus d’informations sur les options de configuration de l’extension et sur l’aide à l’installation, consultez la [page Bing Ads Universal Event Tracking (UET) sur Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100154.html).

Vous pouvez aussi installer l’extension directement dans l’[interface d’Experience Platform Launch](https://launch.adobe.com/). Consultez la section [Ajout d’une nouvelle extension](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) de la documentation de [!DNL Launch]


## Utilisation de l’extension {#how-to-use}

Une fois que vous avez installé l’extension, vous pouvez commencer à configurer des règles pour cette extension directement dans [!DNL Launch].

In [!DNL Launch], you can set up rules for your installed extensions to send event data to the extension destination only in certain situations. Pour plus d’informations sur la configuration de règles pour vos extensions, consultez la [documentation des règles](https://docs.adobe.com/help/fr-FR/launch/using/reference/manage-resources/rules.html).

## Configuration, mise à niveau et suppression de l’extension {#configure-upgrade-delete}

You can configure, upgrade, and delete extensions in the [!DNL Launch] interface.

>[!TIP]
>
>Si l’extension est déjà installée sur l’une de vos propriétés, l’interface de la plateforme de données clients en temps réel d’Adobe affiche toujours **[!UICONTROL Install]** pour l’extension. Démarrez le workflow d’installation comme décrit dans [Installer l’extension](#install-extension) pour accéder à et configurer ou supprimer votre extension.[!DNL Launch]

Pour mettre à niveau votre extension, consultez la section [Mise à niveau d’extension](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/manage-resources/extensions/extension-upgrade.html) dans la documentation de [!DNL Launch]
