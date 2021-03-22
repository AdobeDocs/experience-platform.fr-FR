---
keywords: Audience Manager DIL extension ; destination audience manager ; dil extension
title: Extension Audience Manager DIL
description: L'extension Audience Manager DIL est une destination DMP (Data Management Platform) à Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 44%

---


# Extension Audience Manager DIL {#aam-dil-extension}

## Présentation {#overview}

Il s’agit de l’extension de la bibliothèque d’intégration des données (mise en œuvre côté client) d’Adobe Audience Manager. Remarque : cette extension n’est pas destinée à être utilisée pour le transfert côté serveur (SSF) des données Adobe Analytics. Pour SSF, utilisez l’extension Adobe Analytics. Important : À partir de la version 8.0, le DIL a une dépendance stricte sur le service d’ID [!DNL Experience Cloud], version 3.3 ou ultérieure. Mettez en oeuvre à la fois le service d’ID [!DNL Experience Cloud] et le DIL pour bénéficier de capacités complètes d’intégration des données [!DNL Audience Manager].

[!DNL Audience Manager] DIL est une extension DMP (Data Management Platform) de Adobe Experience Platform. Pour plus d’informations sur la fonctionnalité de l’extension, consultez la [page de l’extension Audience Manager](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) dans la documentation Experience Platform Launch.

Cette destination est une extension [!DNL Experience Platform Launch]. Pour plus d’informations sur le fonctionnement des extensions de lancement dans Platform, voir [Présentation des extensions Experience Platform Launch](../launch-extensions/overview.md).

![Extension Audience Manager DIL](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Conditions préalables  {#prerequisites}

Cette extension est disponible dans le catalogue [!DNL Destinations] pour tous les clients qui ont acheté Platform.

Pour utiliser cette extension, vous devez accéder à [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] est proposé aux clients de Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse. Contactez l’administrateur de votre organisation pour accéder à [!DNL Platform Launch] et demandez-lui de vous accorder l’autorisation **[!UICONTROL manage_properties]** afin que vous puissiez installer les extensions.

## Installation de l’extension {#install-extension}

Pour installer l&#39;extension de DIL [!DNL Audience Manager] :

Dans l&#39;[interface de plate-forme](http://platform.adobe.com/), accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**.

Sélectionnez l’extension dans le catalogue ou utilisez la barre de recherche.

Cliquez sur la destination pour la mettre en évidence, puis sélectionnez **[!UICONTROL Configurer]** dans le rail de droite. Si le contrôle **[!UICONTROL Configure]** est grisé, l&#39;autorisation **[!UICONTROL manage_properties]** vous manque. Voir les [Conditions préalables](#prerequisites).

Dans la fenêtre **[!UICONTROL Sélectionner la propriété disponible]**, sélectionnez la propriété Launch dans laquelle vous souhaitez installer l’extension. [!DNL Launch] Vous pouvez aussi créer une nouvelle propriété dans Launch. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. Pour en savoir plus sur les propriétés, consultez la [section de la page Propriétés](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) de la documentation de [!DNL Launch]

Le flux de travail vous conduit à [!DNL Launch] pour terminer l&#39;installation.

Pour plus d’informations sur les options de configuration de l’extension, consultez la [page de l’extension Audience Manager](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) dans la documentation [!DNL Experience Launch]

Vous pouvez également installer l&#39;extension directement dans l&#39;[interface Adobe Experience Platform Launch](https://launch.adobe.com/). Consultez la section [Ajout d’une nouvelle extension](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) de la documentation de [!DNL Platform Launch]

## Utilisation de l’extension {#how-to-use}

Une fois que vous avez installé l’extension, vous pouvez commencer à configurer des règles pour cette extension directement dans [!DNL Platform Launch].

Dans [!DNL Platform Launch], vous pouvez configurer des règles pour vos extensions installées afin d&#39;envoyer des données de événement à la destination de l&#39;extension uniquement dans certaines situations. Pour plus d’informations sur la configuration de règles pour vos extensions, consultez la [documentation des règles](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Configuration, mise à niveau et suppression de l’extension {#configure-upgrade-delete}

Vous pouvez configurer, mettre à niveau et supprimer des extensions dans l&#39;interface [!DNL Platform Launch].

>[!TIP]
>
>Si l&#39;extension est déjà installée sur l&#39;une de vos propriétés, l&#39;interface utilisateur de la plate-forme affiche toujours **[!UICONTROL Installer]** pour l&#39;extension. Démarrez le workflow d’installation comme décrit dans [Installer l’extension](#install-extension) pour accéder à et configurer ou supprimer votre extension.[!DNL Platform Launch]

Pour mettre à niveau votre extension, consultez la section [Mise à niveau d’extension](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) dans la documentation de [!DNL Platform Launch]



