---
title: Extension de Questionnaires Intercept QuestionPro
seo-title: Extension de Questionnaires Intercept QuestionPro
description: L'extension de Questionnaires Intercept QuestionPro est une destination questionnaire dans la plate-forme de données client en temps réel d'Adobe. Pour plus d’informations sur la fonctionnalité d’extension, voir la page d’extension dans Adobe Exchange.
seo-description: L’extension de Questionnaires Intercept QuestionPro est une destination questionnaire dans la plateforme de données clientes en temps réel d’Adobe. Pour plus d’informations sur la fonctionnalité d’extension, voir la page d’extension dans Adobe Exchange.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 4%

---


# Extension de Questionnaires d&#39;ordonnancement QuestionPro {#questionpro-extension}

## Aperçu {#overview}

QuestionPro Intercept Questionnaires est une plateforme permettant de déployer des questionnaires et de collecter des données comportementales au point de la transaction ou lorsque les utilisateurs entrent ou sortent de votre site Web.

QuestionPro Intercept Questionnaires est une extension de questionnaire de la plate-forme de données client en temps réel d’Adobe. Pour plus d’informations sur la fonctionnalité d’extension, voir la page d’extension d’ [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.90096.questionpro-surveys.html).

Cette destination est une extension de lancement de plateforme d’expérience. Pour plus d’informations sur le fonctionnement des extensions de lancement dans Adobe CDP en temps réel, voir Présentation [des extensions de lancement de plateformes](/help/rtcdp/destinations/experience-platform-launch-extensions.md)d’expérience.

![Extension de Questionnaires d&#39;ordonnancement QuestionPro](assets/web-intercept-surveys-extension.png)

## Conditions préalables {#prerequisites}

Cette extension est disponible dans le catalogue Destinations pour tous les clients qui ont acheté Adobe Real-time CDP.

Pour utiliser cette extension, vous devez accéder au lancement de la plate-forme d’expérience. Experience Platform Launch est proposé aux clients d’Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse. Contactez l’administrateur de votre organisation pour accéder à Launch et demandez-lui de vous accorder l’autorisation **[!UICONTROL manage_properties]** afin que vous puissiez installer des extensions.

## Extension d’installation {#install-extension}

Pour installer l&#39;extension de Questionnaires d&#39;ordonnancement Intercept de QuestionPro :

1. Dans l’interface [CDP en temps réel d’](http://platform.adobe.com/)Adobe, accédez à **[!UICONTROL Destinations > Catalogue]**.
2. Sélectionnez l&#39;extension dans le catalogue ou utilisez la barre de recherche.
3. Cliquez sur la destination pour la mettre en surbrillance, puis sélectionnez **[!UICONTROL Installer l’extension]** dans le rail de droite. Si le contrôle **[!UICONTROL Install Extension]** est grisé, l’autorisation **[!UICONTROL manage_properties]** est manquante. Voir [Conditions préalables](#prerequisites).
4. Dans la fenêtre **[!UICONTROL Sélectionner la propriété]** de lancement disponible, sélectionnez la propriété de lancement dans laquelle vous souhaitez installer l’extension. Vous avez également la possibilité de créer une propriété dans Lancement. Une propriété est un ensemble de règles, d’éléments de données, d’extensions configurées, d’environnements et de bibliothèques. Découvrez les propriétés dans la section [de la page](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Propriétés de la documentation sur le lancement.
5. Le processus vous amène au lancement pour terminer l’installation.

Pour plus d&#39;informations sur les options de configuration de l&#39;extension et la prise en charge de l&#39;installation, consultez la page Questionnaires d&#39;interception [QuestionPro dans Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.90096.questionpro-surveys.html).

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