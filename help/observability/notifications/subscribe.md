---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: S'abonner aux notifications de Événement d'E/S d'Adobe
topic: developer guide
description: Ce document décrit la procédure à suivre pour s'abonner aux notifications événement E/S Adobe pour les services Adobe Experience Platform. Des informations de référence sur les types d'événement disponibles sont également fournies, ainsi que des liens vers d'autres documents sur la façon d'interpréter les données de événement renvoyées pour chaque service [!DNL Platform] applicable.
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 3%

---


# S&#39;abonner aux notifications de Événement d&#39;E/S d&#39;Adobe

[!DNL Observability Insights] vous permet de vous abonner aux notifications de Événement d&#39;E/S d&#39;Adobe concernant les activités Adobe Experience Platform. Ces événements sont envoyés à un crochet Web configuré pour faciliter l&#39;automatisation efficace de la surveillance des activités.

Ce document décrit la procédure à suivre pour s&#39;abonner aux notifications événement E/S Adobe pour les services Adobe Experience Platform. Des informations de référence sur les types d&#39;événement disponibles sont également fournies, ainsi que des liens vers d&#39;autres documents sur la façon d&#39;interpréter les données de événement renvoyées pour chaque [!DNL Platform] service concerné.

## Prise en main

Ce document nécessite une bonne compréhension des hameçons Web et de la façon de connecter un hameçon Web d&#39;une application à une autre. Reportez-vous à la [[!DNL I/O Events] documentation](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) pour une introduction aux hameçons Web.

## Création d’un hook Web

Pour recevoir [!DNL I/O Event] des notifications, vous devez enregistrer un webhook en spécifiant une URL webhook unique dans les détails d’enregistrement de votre événement.

Vous pouvez configurer votre webhook à l’aide du client de votre choix. Pour utiliser une adresse webhook temporaire dans le cadre de ce didacticiel, visitez [Webhook.site](https://webhook.site/) et copiez l’URL unique fournie.

![](../images/notifications/webhook-url.png)

Au cours du processus de validation initial, [!DNL I/O Events] envoie un paramètre de `challenge` requête dans une demande de GET au webhook. Vous devez configurer votre webhook pour renvoyer la valeur de ce paramètre dans la charge utile de réponse. Si vous utilisez Webhook.site, sélectionnez **[!DNL Edit]** dans le coin supérieur droit, puis entrez `$request.query.challenge$` sous **[!DNL Response body]** avant de sélectionner **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## Créer un projet dans la console de développement Adobe

Go to [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_fr) and sign in with your Adobe ID. Suivez ensuite les étapes décrites dans le didacticiel sur la [création d&#39;un projet](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vide dans la documentation de la Console développeur d&#39;Adobes.

## S&#39;abonner aux événements

Une fois que vous avez créé un nouveau projet, accédez à l’écran d’aperçu de ce projet. Sélectionnez **[!UICONTROL Ajouter le événement]**.

![](../images/notifications/add-event-button.png)

Une boîte de dialogue s’affiche, vous permettant d’ajouter un fournisseur de événement à votre projet :

* Si vous vous abonnez à [!DNL Experience Platform] des notifications, sélectionnez Notifications **[!UICONTROL de plateforme.]**
* Si vous vous abonnez à des notifications Adobe Experience Platform [!DNL Privacy Service] , sélectionnez Événements **[!UICONTROL Privacy Service.]**

Une fois que vous avez choisi un fournisseur de événements, sélectionnez **[!UICONTROL Suivant]**.

![](../images/notifications/event-provider.png)

L’écran suivant affiche une liste de types d&#39;événement auxquels s’abonner. Sélectionnez les événements auxquels vous souhaitez vous abonner, puis sélectionnez **[!UICONTROL Suivant]**.

>[!NOTE]
>
>Si vous ne savez pas quels événements vous souhaitez vous abonner au service que vous utilisez, consultez la documentation de notification spécifique au service :
>
>* [[!DNL Privacy Service] notifications](../../privacy-service/privacy-events.md)
>* [[!DNL Data Ingestion] notifications](../../ingestion/quality/subscribe-events.md)
>* [[!DNL Flow Service] (sources) notifications](../../sources/notifications.md)


![](../images/notifications/choose-event-subscriptions.png)

L’écran suivant vous invite à créer un JSON Web Token (JWT). Vous avez la possibilité de générer automatiquement une paire de clés ou de télécharger votre propre clé publique générée dans le terminal.

Pour les besoins de ce didacticiel, la première option est suivie. Sélectionnez la zone d’options **[!UICONTROL Générer une paire]** de clés, puis sélectionnez le bouton **[!UICONTROL Générer la paire de clés]** dans le coin inférieur droit.

![](../images/notifications/generate-keypair.png)

Lorsque la paire de clés est générée, elle est automatiquement téléchargée par le navigateur. Vous devez stocker ce fichier vous-même, car il n’est pas conservé dans la Console développeur.

L’écran suivant vous permet de vérifier les détails de la paire de clés nouvellement générée. Select **[!UICONTROL Next]** to continue.

![](../images/notifications/keypair-generated.png)

Dans l’écran suivant, indiquez le nom et la description de l’enregistrement du événement dans la section des détails [!UICONTROL d’enregistrement du] Événement. Il est recommandé de créer un nom unique et facilement identifiable afin de différencier cette inscription de événement des autres sur le même projet.

![](../images/notifications/registration-details.png)

Plus loin dans le même écran, sous la section [!UICONTROL Comment recevoir des événements] , vous pouvez éventuellement configurer la manière de recevoir des événements. **[!UICONTROL Webhook]** vous permet de fournir une adresse webhook personnalisée pour recevoir des événements, tandis que l’action **** Runtime vous permet de faire de même à l’aide de [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Pour ce didacticiel, sélectionnez **[!UICONTROL Webhook]** et indiquez l’URL du webhook que vous avez créé précédemment. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Enregistrer les événements]** configurés pour terminer l’enregistrement du événement.

![](../images/notifications/receive-events.png)

La page des détails de l&#39;enregistrement de événement nouvellement créé s&#39;affiche, dans laquelle vous pouvez modifier sa configuration, examiner les événements reçus, effectuer le suivi du débogage et ajouter de nouveaux fournisseurs de événement.

![](../images/notifications/registration-complete.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez enregistré un webhook pour recevoir [!DNL I/O Event] des notifications pour [!DNL Experience Platform] et/ou [!DNL Privacy Service]. Pour plus d’informations sur les événements disponibles et sur la façon d’interpréter les charges utiles de notification pour chaque service, consultez la documentation suivante :

* [[!DNL Privacy Service] notifications](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] notifications](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] (sources) notifications](../../sources/notifications.md)

Consultez la [[!DNL Observability Insights] présentation](../home.md) pour en savoir plus sur la manière de surveiller vos activités sur [!DNL Experience Platform] et [!DNL Privacy Service].