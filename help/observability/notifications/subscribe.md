---
keywords: Experience Platform ; accueil ; rubriques populaires ; plage de dates
solution: Experience Platform
title: S'abonner aux notifications de Événement d'Adobe I/O
topic-legacy: developer guide
description: Ce document décrit la procédure à suivre pour s'abonner aux notifications événement Adobe I/O pour les services Adobe Experience Platform. Des informations de référence sur les types d'événement disponibles sont également fournies, ainsi que des liens vers d'autres documents sur la façon d'interpréter les données de événement renvoyées pour chaque  [!DNL Platform] service applicable.
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 4%

---

# S’abonner aux notifications de Événement d’Adobe I/O

[!DNL Observability Insights] vous permet de vous abonner à des notifications Adobe I/O Événement concernant les activités Adobe Experience Platform. Ces événements sont envoyés à un crochet Web configuré pour faciliter l&#39;automatisation efficace de la surveillance des activités.

Ce document décrit la procédure à suivre pour s&#39;abonner aux notifications événement Adobe I/O pour les services Adobe Experience Platform. Des informations de référence sur les types d&#39;événement disponibles sont également fournies, ainsi que des liens vers d&#39;autres documents sur la façon d&#39;interpréter les données de événement renvoyées pour chaque service [!DNL Platform] applicable.

## Prise en main

Ce document nécessite une bonne compréhension des hameçons Web et de la façon de connecter un hameçon Web d&#39;une application à une autre. Consultez la [[!DNL I/O Events] documentation](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) pour une présentation des hameçons Web.

## Création d’un hook Web

Pour recevoir des notifications [!DNL I/O Event], vous devez enregistrer un webhook en spécifiant une URL webhook unique dans les détails d&#39;enregistrement de votre événement.

Vous pouvez configurer votre webhook à l’aide du client de votre choix. Pour utiliser une adresse webhook temporaire dans le cadre de ce didacticiel, visitez [Webhook.site](https://webhook.site/) et copiez l’URL unique fournie.

![](../images/notifications/webhook-url.png)

Au cours du processus de validation initial, [!DNL I/O Events] envoie un paramètre de requête `challenge` dans une demande de GET au hook Web. Vous devez configurer votre webhook pour renvoyer la valeur de ce paramètre dans la charge utile de réponse. Si vous utilisez Webhook.site, sélectionnez **[!DNL Edit]** dans le coin supérieur droit, puis saisissez `$request.query.challenge$` sous **[!DNL Response body]** avant de sélectionner **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## Créer un projet dans la console de développement Adobe

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_fr) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le didacticiel sur la [création d&#39;un projet vide](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) dans la documentation de la Console développeur de l&#39;Adobe.

## S&#39;abonner aux événements

Une fois que vous avez créé un nouveau projet, accédez à l’écran d’aperçu de ce projet. À partir de là, sélectionnez **[!UICONTROL Ajouter le événement]**.

![](../images/notifications/add-event-button.png)

Une boîte de dialogue s’affiche, vous permettant d’ajouter un fournisseur de événement à votre projet :

* Si vous vous abonnez à des notifications [!DNL Experience Platform], sélectionnez **[!UICONTROL Notifications de plateforme]**.
* Si vous vous abonnez à des notifications Adobe Experience Platform [!DNL Privacy Service], sélectionnez **[!UICONTROL Événements Privacy Service]**.

Une fois que vous avez choisi un fournisseur de événement, sélectionnez **[!UICONTROL Suivant]**.

![](../images/notifications/event-provider.png)

L’écran suivant affiche une liste de types d&#39;événement auxquels s’abonner. Sélectionnez les événements auxquels vous souhaitez vous abonner, puis **[!UICONTROL Suivant]**.

>[!NOTE]
>
>Si vous ne savez pas quels événements vous souhaitez vous abonner au service que vous utilisez, consultez la documentation de notification spécifique au service :
>
>* [[!DNL Privacy Service] notifications](../../privacy-service/privacy-events.md)
>* [[!DNL Data Ingestion] notifications](../../ingestion/quality/subscribe-events.md)
>* [[!DNL Flow Service (sources)] notifications](../../sources/notifications.md)


![](../images/notifications/choose-event-subscriptions.png)

L’écran suivant vous invite à créer un JSON Web Token (JWT). Vous avez la possibilité de générer automatiquement une paire de clés ou de télécharger votre propre clé publique générée dans le terminal.

Pour les besoins de ce didacticiel, la première option est suivie. Sélectionnez la zone d’options pour **[!UICONTROL Générer une paire de clés]**, puis sélectionnez le bouton **[!UICONTROL Générer la paire de clés]** dans le coin inférieur droit.

![](../images/notifications/generate-keypair.png)

Lorsque la paire de clés est générée, elle est automatiquement téléchargée par le navigateur. Vous devez stocker ce fichier vous-même, car il n’est pas conservé dans la Console développeur.

L’écran suivant vous permet de vérifier les détails de la paire de clés nouvellement générée. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![](../images/notifications/keypair-generated.png)

Dans l’écran suivant, indiquez le nom et la description de l’enregistrement du événement dans la section [!UICONTROL Détails de l’enregistrement du Événement]. Il est recommandé de créer un nom unique et facilement identifiable afin de différencier cette inscription de événement des autres sur le même projet.

![](../images/notifications/registration-details.png)

Plus loin dans le même écran, sous la section [!UICONTROL Comment recevoir des événements], vous pouvez éventuellement configurer comment recevoir des événements. **** Webhooking vous permet de fournir une adresse webhook personnalisée pour recevoir des événements, tandis que l’ **[!UICONTROL action]** Runtime vous permet de faire de même à l’aide de  [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Pour ce didacticiel, sélectionnez **[!UICONTROL Webhook]** et indiquez l’URL du webhook que vous avez créé précédemment. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Enregistrer les événements configurés]** pour terminer l&#39;enregistrement du événement.

![](../images/notifications/receive-events.png)

La page des détails de l&#39;enregistrement de événement nouvellement créé s&#39;affiche, dans laquelle vous pouvez modifier sa configuration, examiner les événements reçus, effectuer le suivi du débogage et ajouter de nouveaux fournisseurs de événement.

![](../images/notifications/registration-complete.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez enregistré un webhook pour recevoir des notifications [!DNL I/O Event] pour [!DNL Experience Platform] et/ou [!DNL Privacy Service]. Pour plus d’informations sur les événements disponibles et sur la façon d’interpréter les charges utiles de notification pour chaque service, consultez la documentation suivante :

* [[!DNL Privacy Service] notifications](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] notifications](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service (sources)] notifications](../../sources/notifications.md)

Voir [[!DNL Observability Insights] présentation](../home.md) pour plus d&#39;informations sur la façon de surveiller vos activités sur [!DNL Experience Platform] et [!DNL Privacy Service].
