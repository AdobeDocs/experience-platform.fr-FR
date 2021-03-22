---
Keywords: ECID;ecid
title: Extension du service Experience Cloud ID
description: L’extension Experience Cloud ID Service est une destination de personnalisation à Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 38%

---


# [!DNL Experience Cloud] Extension du service d’ID  {#adobe-ecid-extension}

## Présentation {#overview}

Cette extension implémente le service d’ID [!DNL Experience Cloud], qui identifie les visiteurs dans toutes les solutions [!DNL Experience Cloud].

[!DNL Experience Cloud] Le service d’ID est une extension de personnalisation dans Adobe Experience Platform. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la [page d’extension du service Experience Cloud ID](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html) dans la documentation [!DNL Experience Platform Launch]

Cette destination est une extension [!DNL Adobe Experience Platform Launch]. Pour plus d&#39;informations sur le fonctionnement des extensions [!DNL Platform Launch] dans Platform, voir [Présentation des extensions Experience Platform Launch](../launch-extensions/overview.md).

![Extension Adobe ECID](../../assets/catalog/personalization/adobe-ecid/catalog.png)

## Conditions préalables  {#prerequisites}

Cette extension est disponible dans le catalogue Destinations pour tous les clients qui ont acheté Platform.

Pour utiliser cette extension, vous devez accéder à [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] est proposé aux clients de Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse. Contactez l’administrateur de votre organisation pour accéder à [!DNL Launch] et demandez-lui de vous accorder l’autorisation **[!UICONTROL manage_properties]** afin que vous puissiez installer les extensions.

## Installation de l’extension {#install-extension}

Pour installer l&#39;extension de service d&#39;ID [!DNL Experience Cloud] :

Dans l&#39;[interface de plate-forme](http://platform.adobe.com/), accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**.

Sélectionnez l’extension dans le catalogue ou utilisez la barre de recherche.

Cliquez sur la destination pour la mettre en évidence, puis sélectionnez **[!UICONTROL Configurer]** dans le rail de droite. Si le contrôle **[!UICONTROL Configure]** est grisé, l&#39;autorisation **[!UICONTROL manage_properties]** vous manque. Voir les [Conditions préalables](#prerequisites).

Dans la fenêtre **[!UICONTROL Sélectionner la propriété de Platform launch disponible]**, sélectionnez la propriété [!DNL Platform Launch] dans laquelle vous souhaitez installer l&#39;extension. Vous pouvez aussi créer une nouvelle propriété dans [!DNL Platform Launch]. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. Pour en savoir plus sur les propriétés, consultez la [section de la page Propriétés](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) de la documentation de [!DNL Launch]

Le flux de travail vous conduit à [!DNL Platform Launch] pour terminer l&#39;installation.

Pour plus d’informations sur les options de configuration de l’extension et sur l’aide à l’installation, consultez la [page d’extension du service Experience Cloud ID](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/id-service-extension/overview.html) dans la documentation [!DNL Experience Launch]

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