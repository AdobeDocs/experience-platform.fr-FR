---
title: Extension de Medallia
seo-title: Extension de Medallia
description: L’extension Medallia est une voix de la destination du client dans la plate-forme de données client en temps réel d’Adobe. Pour plus d’informations sur la fonctionnalité d’extension, voir la page d’extension dans Adobe Exchange.
seo-description: L’extension Medallia est une voix de la destination du client dans la plate-forme de données client en temps réel d’Adobe. Pour plus d’informations sur la fonctionnalité d’extension, voir la page d’extension dans Adobe Exchange.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 4%

---


# Extension Medallia {#medallia-extension}

## Aperçu {#overview}

Déployez Medallia rapidement et facilement sur vos propriétés web. L’extension vous permet également de détecter des événements de questionnaire, de capturer les commentaires des clients en temps réel au moyen d’éléments de données, de les utiliser dans des règles pour personnaliser l’expérience de vos clients et de partager des données avec Adobe Analytics.

Medallia est la voix de l’extension client dans la plate-forme de données client en temps réel d’Adobe. Pour plus d’informations sur la fonctionnalité d’extension, voir la page d’extension d’ [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103279.medallia-for-adobe-launch.html).

Cette destination est une extension de lancement de plateforme d’expérience. Pour plus d’informations sur le fonctionnement des extensions de lancement dans Adobe CDP en temps réel, voir Présentation [des extensions de lancement de plateformes](/help/rtcdp/destinations/experience-platform-launch-extensions.md)d’expérience.

![Extension Medallia](assets/medallia-extension.png)

## Conditions préalables {#prerequisites}

Cette extension est disponible dans le catalogue Destinations pour tous les clients qui ont acheté Adobe Real-time CDP.

Pour utiliser cette extension, vous devez accéder au lancement de la plate-forme d’expérience. Experience Platform Launch est proposé aux clients d’Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse. Contactez l’administrateur de votre organisation pour accéder à Launch et demandez-lui de vous accorder l’autorisation **[!UICONTROL manage_properties]** afin que vous puissiez installer des extensions.

## Extension d’installation {#install-extension}

Pour installer l&#39;extension Medallia :

1. Dans l’interface [CDP en temps réel d’](http://platform.adobe.com/)Adobe, accédez à **[!UICONTROL Destinations > Catalogue]**.
2. Sélectionnez l&#39;extension dans le catalogue ou utilisez la barre de recherche.
3. Cliquez sur la destination pour la mettre en surbrillance, puis sélectionnez **[!UICONTROL Installer l’extension]** dans le rail de droite. Si le contrôle **[!UICONTROL Install Extension]** est grisé, l’autorisation **[!UICONTROL manage_properties]** est manquante. Voir [Conditions préalables](#prerequisites).
4. Dans la fenêtre **[!UICONTROL Sélectionner la propriété]** de lancement disponible, sélectionnez la propriété de lancement dans laquelle vous souhaitez installer l’extension. Vous avez également la possibilité de créer une propriété dans Lancement. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. Découvrez les propriétés dans la section [de la page](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Propriétés de la documentation sur le lancement.
5. Le processus vous amène au lancement pour terminer l’installation.

Pour plus d’informations sur les options de configuration de l’extension et la prise en charge de l’installation, voir la page [Medallia sur Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103279.medallia-for-adobe-launch.html).

Vous pouvez également installer l’extension directement dans l’interface [de lancement de la plateforme](https://launch.adobe.com/)d’expérience. Reportez-vous à [Ajouter une nouvelle extension](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) dans la documentation de lancement.

## Utilisation de l&#39;extension {#how-to-use}

Une fois que vous avez installé l&#39;extension, vous pouvez début la configuration de règles pour celle-ci directement dans Lancement.

Dans Lancement, vous pouvez configurer des règles pour vos extensions installées afin d’envoyer des données de événement à la destination de l’extension uniquement dans certaines situations. Pour plus d’informations sur la configuration de règles pour vos extensions, voir la documentation [sur les](https://docs.adobe.com/help/fr-FR/launch/using/reference/manage-resources/rules.translate.html)règles.

## Configuration, mise à niveau et suppression de l’extension {#configure-upgrade-delete}

Vous pouvez configurer, mettre à niveau et supprimer des extensions dans l’interface de lancement.

>[!TIP]
>
>Si l’extension est déjà installée sur l’une de vos propriétés, l’interface utilisateur CDP en temps réel d’Adobe affiche toujours **[!UICONTROL Install]** pour l’extension. Lancez le processus d’installation comme décrit dans [Installer l’extension](#install-extension) pour accéder à Lancer et configurer ou supprimer votre extension.

Pour mettre à niveau votre extension, reportez-vous à la section Mise à niveau [de l’](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) extension dans la documentation relative au lancement.