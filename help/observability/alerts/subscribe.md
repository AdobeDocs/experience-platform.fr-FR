---
keywords: Experience Platform;accueil;rubriques populaires;période
title: S’abonner aux notifications d’événement d’Adobe I/O
description: Ce document décrit les étapes à suivre pour s’abonner aux notifications d’événement d’Adobe I/O pour les services Adobe Experience Platform. Des informations de référence sur les types d’événement disponibles sont également fournies, ainsi que des liens vers d’autres documents sur la manière d’interpréter les données d’événement renvoyées pour chaque service [!DNL Platform] applicable.
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: d82487f34c0879ed27ac55e42d70346f45806131
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 8%

---

# S’abonner aux notifications d’événement d’Adobe I/O

[!DNL Observability Insights] vous permet de vous abonner à des notifications d’événement d’Adobe I/O concernant les activités Adobe Experience Platform. Ces événements sont envoyés à un webhook configuré pour faciliter l’automatisation efficace de la surveillance des activités.

Ce document décrit les étapes à suivre pour s’abonner aux notifications d’événement d’Adobe I/O pour les services Adobe Experience Platform. Des informations de référence sur les types d’événement disponibles sont également fournies, ainsi que des liens vers d’autres documents sur la manière d’interpréter les données d’événement renvoyées pour chaque service [!DNL Platform] applicable.

## Prise en main

Ce document nécessite une compréhension pratique des webhooks et de la manière dont connecter un webhook d’une application à une autre. Consultez la [[!DNL I/O Events] documentation](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) pour une présentation des webhooks.

## Création d’un webhook

Pour recevoir des notifications [!DNL I/O Event], vous devez enregistrer un webhook en spécifiant une URL webhook unique dans les détails d’enregistrement de votre événement.

Vous pouvez configurer votre webhook à l’aide du client de votre choix. Pour obtenir une adresse webhook temporaire à utiliser dans le cadre de ce tutoriel, rendez-vous sur [Webhook.site](https://webhook.site/) et copiez l’URL unique fournie.

![](../images/notifications/webhook-url.png)

Au cours du processus de validation initial, [!DNL I/O Events] envoie un paramètre de requête `challenge` dans une demande de GET au webhook. Vous devez configurer votre webhook pour renvoyer la valeur de ce paramètre dans le payload de réponse. Si vous utilisez Webhook.site, sélectionnez **[!DNL Edit]** dans le coin supérieur droit, puis saisissez `$request.query.challenge$` sous **[!DNL Response body]** avant de sélectionner **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## Création d’un projet dans Adobe Developer Console

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le tutoriel sur la [création d’un projet vide](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) dans la documentation d’Adobe Developer Console.

## Abonnement aux événements

Une fois que vous avez créé un projet, accédez à l’écran d’aperçu de ce projet. À partir de là, sélectionnez **[!UICONTROL Ajouter un événement]**.

![](../images/notifications/add-event-button.png)

Une boîte de dialogue s’affiche, vous permettant d’ajouter un fournisseur d’événements à votre projet :

* Si vous vous abonnez à des alertes Experience Platform, sélectionnez **[!UICONTROL Notifications de la plateforme]**
* Si vous vous abonnez à des notifications Adobe Experience Platform [!DNL Privacy Service], sélectionnez **[!UICONTROL Événements de Privacy Service]**

Une fois que vous avez choisi un fournisseur d’événements, sélectionnez **[!UICONTROL Suivant]**.

![](../images/notifications/event-provider.png)

L’écran suivant affiche une liste des types d’événements auxquels s’abonner. Sélectionnez les événements auxquels vous souhaitez vous abonner, puis cliquez sur **[!UICONTROL Suivant]**.

>[!NOTE]
>
>Si vous ne savez pas à quels événements vous abonner pour le service que vous utilisez, consultez la documentation de notification spécifique au service :
>
>* [[!DNL Privacy Service] notifications](../../privacy-service/privacy-events.md)
>* [[!DNL Data Ingestion] notifications](../../ingestion/quality/subscribe-events.md)
>* [[!DNL Flow Service (sources)] notifications](../../sources/notifications.md)


![](../images/notifications/choose-event-subscriptions.png)

L’écran suivant vous invite à créer un jeton Web JSON (JWT). Vous avez la possibilité de générer automatiquement une paire de clés ou de télécharger votre propre clé publique générée dans le terminal.

Pour les besoins de ce tutoriel, la première option est suivie. Sélectionnez la zone d’option **[!UICONTROL Générer une paire de clés]**, puis cliquez sur le bouton **[!UICONTROL Générer la paire de clés]** dans le coin inférieur droit.

![](../images/notifications/generate-keypair.png)

Lorsque la paire de clés est générée, elle est automatiquement téléchargée par le navigateur. Vous devez stocker ce fichier vous-même, car il n’est pas conservé dans Developer Console.

L’écran suivant vous permet de consulter les détails de la paire de clés nouvellement générée. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../images/notifications/keypair-generated.png)

Dans l’écran suivant, indiquez le nom et la description de l’enregistrement de l’événement dans la section [!UICONTROL Détails de l’enregistrement de l’événement] . La bonne pratique consiste à créer un nom unique et facilement identifiable afin de différencier cette enregistrement d’événement des autres sur le même projet.

![](../images/notifications/registration-details.png)

Plus bas sur le même écran, sous la section [!UICONTROL Comment recevoir des événements] , vous pouvez éventuellement configurer comment recevoir des événements. **** Webhookie vous permet de fournir une adresse webhook personnalisée pour recevoir les événements, tandis que l’ **[!UICONTROL action]** Runtime vous permet de faire de même à l’aide de  [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Pour ce tutoriel, sélectionnez **[!UICONTROL Webhook]** et fournissez l’URL du webhook que vous avez créé précédemment. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Enregistrer les événements configurés]** pour terminer l’enregistrement de l’événement.

![](../images/notifications/receive-events.png)

La page de détails de l’enregistrement d’événement nouvellement créé s’affiche, dans laquelle vous pouvez modifier sa configuration, revoir les événements reçus, effectuer le suivi de débogage et ajouter de nouveaux fournisseurs d’événements.

![](../images/notifications/registration-complete.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez enregistré un webhook pour recevoir des [!DNL I/O Event] notifications pour [!DNL Experience Platform] et/ou [!DNL Privacy Service]. Pour plus d’informations sur les événements disponibles et sur la façon d’interpréter les payloads des notifications pour chaque service, reportez-vous à la documentation suivante :

* [[!DNL Privacy Service] notifications](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] notifications](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] Notifications (sources)](../../sources/notifications.md)

Pour plus d’informations sur la façon de surveiller vos activités sur [!DNL Experience Platform] et [!DNL Privacy Service], consultez la [[!DNL Observability Insights] présentation](../home.md) .
