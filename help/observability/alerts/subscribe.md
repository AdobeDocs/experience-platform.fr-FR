---
keywords: Experience Platform;accueil;rubriques populaires;période
title: Abonnement aux notifications dʼévénement Adobe I/O
description: Ce document décrit la procédure à suivre pour sʼabonner aux notifications dʼévénement Adobe I/O pour les services Adobe Experience Platform. Des informations de référence concernant les types dʼévénement disponibles sont également fournies, ainsi que des liens vers la documentation supplémentaire sur la manière dʼinterpréter les données dʼévénement renvoyées pour chaque service  [!DNL Experience Platform]  applicable.
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
TQID: https://experienceleague.adobe.com/YbSl4WsK5jaiQOq3bWBBBYX4AKA9WDTSI0Ss0CkEamU
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 780
ht-degree: 70%

---

# Abonnement aux notifications dʼévénement Adobe I/O

[!DNL Observability Insights] vous permet de vous abonner à des notifications dʼévénement Adobe I/O concernant les activités dʼAdobe Experience Platform. Ces événements sont envoyés à un Webhook configuré afin de faciliter lʼautomatisation efficace de la surveillance des activités.

Ce document décrit la procédure à suivre pour vous abonner aux notifications d’événement Adobe I/O pour les services Adobe Experience Platform. Des informations de référence sur les types d’événements disponibles sont également fournies, ainsi que des liens vers d’autres documents sur la façon dont vous pouvez interpréter les données d’événement renvoyées pour chaque service [!DNL Experience Platform] applicable.

## Prise en main

Ce document nécessite une compréhension pratique des Webhooks et de la manière de connecter un Webhook dʼune application à une autre. Pour en savoir plus sur les Webhooks, consultez la [[!DNL I/O Events] documentation](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md).

## Création dʼun Webhook

Pour recevoir des notifications [!DNL I/O Event], vous devez enregistrer un Webhook en indiquant une URL Webhook unique dans les détails dʼenregistrement de votre événement.

Vous pouvez configurer votre Webhook à lʼaide du client de votre choix. Pour obtenir une adresse Webhook temporaire à utiliser dans le cadre de ce tutoriel, rendez-vous sur [Webhook.site](https://webhook.site/) et copiez lʼURL unique fournie.

![](../images/notifications/webhook-url.png)

Au cours du processus de validation initial, [!DNL I/O Events] envoie un paramètre de requête `challenge` dans une requête GET vers le Webhook. Vous devez configurer votre Webhook pour renvoyer la valeur de ce paramètre dans le payload de réponse. Si vous utilisez Webhook.site, sélectionnez **[!DNL Edit]** dans le coin supérieur droit, puis saisissez `$request.query.challenge$` sous **[!DNL Response body]** avant de sélectionner **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## Création dʼun projet dans Adobe Developer Console

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le tutoriel sur la [création dʼun projet vide](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) disponible dans la documentation dʼAdobe Developer Console.

## Abonnement aux événements

>[!NOTE]
>
>L’événement de notification d’ingestion de données est obsolète dans Adobe I/O. Utilisez plutôt l’événement d’E/S **Informations d’exécution du flux de sources**.

Une fois que vous avez créé un projet, accédez à lʼécran dʼaperçu de ce projet. À partir de là, sélectionnez **[!UICONTROL Add event]**.

![](../images/notifications/add-event-button.png)

Une boîte de dialogue sʼaffiche, vous permettant dʼajouter un fournisseur dʼévénements à votre projet :

* Si vous vous abonnez à des alertes Experience Platform, sélectionnez **[!UICONTROL Platform notifications]**
* Si vous vous abonnez à des notifications de [!DNL Privacy Service] Adobe Experience Platform, sélectionnez **[!UICONTROL Privacy Service Events]**

Une fois que vous avez choisi un fournisseur d’événements, sélectionnez **[!UICONTROL Next]**.

![](../images/notifications/event-provider.png)

Lʼécran suivant affiche une liste des types dʼévénements auxquels vous pouvez vous abonner. Sélectionnez les événements auxquels vous souhaitez vous abonner, puis sélectionnez **[!UICONTROL Next]**.

>[!NOTE]
>
>Si vous avez des doutes sur les événements auxquels vous devez vous abonner pour le service avec lequel vous travaillez, consultez la documentation suivante :
>
>* [Notifications Platform](./rules.md)
>* [Notifications Privacy Service](../../privacy-service/privacy-events.md)

>[!IMPORTANT]
>
>les alertes liées à Edge sont actuellement en version bêta et disponibles uniquement pour certains clients bêta.

![](../images/notifications/choose-event-subscriptions.png)

Lʼécran suivant vous invite à créer un JSON Web Token (JWT). Vous avez la possibilité de générer automatiquement une paire de clés ou de télécharger votre propre clé publique générée dans le terminal.

Pour les besoins de ce tutoriel, nous avons retenu la première option. Sélectionnez la case d’option à **[!UICONTROL Generate a key pair]**, puis sélectionnez le bouton **[!UICONTROL Generate keypair]** dans le coin inférieur droit.

![](../images/notifications/generate-keypair.png)

Lorsque la paire de clés est générée, elle est automatiquement téléchargée par le navigateur. Vous devez stocker ce fichier vous-même, car il nʼest pas conservé dans Developer Console.

Lʼécran suivant vous permet dʼafficher les détails de la paire de clés nouvellement générée. Sélectionnez **[!UICONTROL Next]** pour continuer.

![](../images/notifications/keypair-generated.png)

Dans l’écran suivant, indiquez un nom et une description pour l’enregistrement de l’événement dans la section [!UICONTROL Event registration details] . Il est recommandé de créer un nom unique et facilement identifiable afin de différencier cet enregistrement dʼévénement des autres sur le même projet.

![](../images/notifications/registration-details.png)

Plus bas sur le même écran, sous la section [!UICONTROL How to receive events] , vous pouvez éventuellement configurer comment recevoir les événements. **[!UICONTROL Webhook]** vous permet de fournir une adresse webhook personnalisée pour recevoir les événements, tandis que **[!UICONTROL Runtime action]** vous permet de faire de même à l’aide de [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Pour ce tutoriel, sélectionnez **[!UICONTROL Webhook]** et fournissez l’URL du webhook que vous avez créé précédemment. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Save configured events]** pour terminer l’enregistrement de l’événement.

![](../images/notifications/receive-events.png)

La page de détails de l’enregistrement d’événement nouvellement créé s’affiche ; vous pouvez y modifier sa configuration, passer en revue les événements reçus, effectuer du suivi de débogage et ajouter de nouveaux fournisseurs d’événements.

![](../images/notifications/registration-complete.png)

## Étapes suivantes

En suivant ce tutoriel, vous avez enregistré un webhook pour recevoir des notifications [!DNL I/O Event] pour [!DNL Experience Platform] et/ou [!DNL Privacy Service]. Pour plus d’informations sur les événements disponibles et sur la façon d’interpréter les payloads des notifications pour chaque service, reportez-vous à la documentation suivante :

* [[!DNL Privacy Service] notifications](../../privacy-service/privacy-events.md)
* [Notifications [!DNL Flow Service] (sources)](../../sources/notifications.md)

Pour plus d’informations sur la façon de surveiller vos activités sur [!DNL Experience Platform] et [!DNL Privacy Service], consultez la [[!DNL Observability Insights] présentation](../home.md).
