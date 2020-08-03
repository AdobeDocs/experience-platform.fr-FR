---
title: Extension Nielsen VideoJS Player Handler
seo-title: Extension Nielsen VideoJS Player Handler
description: L’extension Nielsen VideoJS Player Handler est une destination d’analyse de la plateforme de données clients en temps réel d’Adobe. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
seo-description: L’extension Nielsen VideoJS Player Handler est une destination d’analyse de la plateforme de données clients en temps réel d’Adobe. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans Adobe Exchange.
translation-type: tm+mt
source-git-commit: be4cf64c89a189a09a4a7774c8fadc76c6ee8458
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 93%

---


# [!DNL Nielsen VideoJS Player Handler] Extension {#nielsen-vjs-extension}

## Présentation {#overview}

[!DNL Nielsen Digital SDK] offres d&#39;extension de lancement  la mesure des audiences via les produits de mesure numériques suivants :

DCR : une solution de mesure qui permet de mesurer quotidiennement le contenu numérique non linéaire, y compris le contenu comportant des publicités, et d’obtenir une vue exhaustive de la consommation du contenu numérique par l’audience sur les ordinateurs de bureau, les téléphones portables, les tablettes et les appareils connectés.

DTVR : cette solution tient compte du visionnage linéaire de la télévision sur les ordinateurs de bureau et les appareils mobiles pour les sources de programmation participantes. Il s’agit de la première solution ayant obtenu une accréditation du MRC pour sa contribution à la mesure de l’audience télévisuelle pour les programmes visionnés sur des ordinateurs et des appareils mobiles.

[!DNL Nielsen VideoJS Player Handler] est une extension d’analyse de la plateforme de données clients en temps réel d’Adobe. Pour plus d’informations sur les fonctionnalités de l’extension, consultez la page de l’extension dans [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101361.nielsen-digital-sdk-extension.html).

Cette destination est une extension d’Experience Platform Launch. Pour plus d’informations sur le fonctionnement des extensions de Launch dans la plateforme de données clients en temps réel d’Adobe, consultez la [présentation des extensions d’Experience Platform Launch](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

![Extension Nielsen VideoJS Player Handler](assets/nielsen-videojs-extension.png)

## Conditions préalables  {#prerequisites}

This extension is available in the [!DNL Destinations] catalog for all customers who have purchased Adobe Real-time CDP.

Pour utiliser cette extension, vous devez accéder à Experience Platform Launch. Experience Platform Launch est une fonctionnalité gratuite intégrée à Adobe Experience Cloud. Contactez l’administrateur de votre organisation pour accéder à Launch et demandez-lui de vous accorder l’autorisation **[!UICONTROL manage_properties]** afin que vous puissiez installer les extensions.

## Installation de l’extension {#install-extension}

Pour installer l’ [!DNL Nielsen VideoJS Player Handler] extension :

1. In the [Adobe Real-time CDP interface](http://platform.adobe.com/), go to **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.
2. Sélectionnez l’extension dans le catalogue ou utilisez la barre de recherche.
3. Cliquez sur la destination pour la mettre en surbrillance, puis sélectionnez **[!UICONTROL Installer l’extension]** dans le rail droit. Si la commande **[!UICONTROL Installer l’extension]** est grisée, vous ne disposez pas de l’autorisation **[!UICONTROL manage_properties]**. Voir les [Conditions préalables](#prerequisites).
4. Dans la fenêtre **[!UICONTROL Sélectionner la propriété Launch disponible]**, sélectionnez la propriété Launch dans laquelle vous souhaitez installer l’extension. Vous pouvez aussi créer une nouvelle propriété dans Launch. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. Pour en savoir plus sur les propriétés, consultez la [section de la page Propriétés](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/admin/companies-and-properties.html#properties-page) de la documentation de Launch.
5. Le workflow vous redirige vers Launch pour terminer l’installation.

Pour plus d’informations sur les options de configuration de l’extension et sur l’aide à l’installation, consultez la [page SDK Nielsen Digital sur Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101361.nielsen-digital-sdk-extension.html).

Vous pouvez aussi installer l’extension directement dans l’[interface d’Experience Platform Launch](https://launch.adobe.com/). Consultez la section [Ajout d’une nouvelle extension](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) de la documentation de Launch.

## Utilisation de l’extension {#how-to-use}

Une fois que vous avez installé l’extension, vous pouvez commencer à configurer des règles pour cette extension directement dans Launch.

Dans Launch, vous pouvez configurer des règles pour vos extensions installées afin d’envoyer des données d’événement vers la destination de l’extension uniquement dans certains cas. Pour plus d’informations sur la configuration de règles pour vos extensions, consultez la [documentation des règles](https://docs.adobe.com/help/fr-FR/launch/using/reference/manage-resources/rules.html).

## Configuration, mise à niveau et suppression de l’extension {#configure-upgrade-delete}

Vous pouvez configurer, mettre à niveau et supprimer des extensions dans l’interface de Launch.

>[!TIP]
>
>Si l’extension est déjà installée sur l’une de vos propriétés, l’interface de la plateforme de données clients en temps réel d’Adobe affiche toujours **[!UICONTROL Install]** pour l’extension. Démarrez le workflow d’installation comme décrit dans [Installer l’extension](#install-extension) pour accéder à Launch et configurer ou supprimer votre extension.

Pour mettre à niveau votre extension, consultez la section [Mise à niveau d’extension](https://docs.adobe.com/content/help/fr-FR/launch/using/reference/manage-resources/extensions/extension-upgrade.html) dans la documentation de Launch.