---
keywords: Experience Platform;accueil;rubriques les plus consultées;alertes;destinations
description: Vous pouvez vous abonner à des alertes lors de la création d’un flux de données pour recevoir des messages d’alerte concernant l’état, la réussite ou l’échec de votre exécution de flux.
title: S’abonner aux alertes de destination contextuelles
exl-id: 134144a0-cdfe-49a8-bd8b-e36a4f053de5
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 17%

---

# S’abonner aux alertes de destination contextuelles

Adobe Experience Platform vous permet de vous abonner à des alertes basées sur des événements concernant les activités Adobe Experience Platform. Les alertes réduisent ou éliminent la nécessité d’interroger l’[[!DNL Observability Insights] API](../../observability/api/overview.md) afin de vérifier si une tâche est terminée, si un certain jalon a été atteint dans un processus ou si des erreurs se sont produites.

Vous pouvez vous abonner à des alertes lors de la création d’un flux de données pour recevoir des messages d’alerte concernant l’état, la réussite ou l’échec de votre exécution de flux.

Ce document décrit les étapes à suivre pour s’abonner à des messages d’alerte pour vos flux de données de destination.

## Commencer

Ce document nécessite une compréhension pratique des composants suivants de Adobe Experience Platform :

* [Destinations](../home.md) : intégrations prédéfinies avec des plateformes de destination qui permettent l’activation transparente des données de Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.
* [Observability](../../observability/home.md) : [!DNL Observability Insights] permet de surveiller les activités de Platform à l’aide de mesures statistiques et de notifications d’événement.
   * [Alertes](../../observability/alerts/overview.md) : lorsqu’un certain ensemble de conditions de vos opérations Platform est atteint (par exemple un problème potentiel lorsque le système dépasse un seuil), Platform peut envoyer des messages d’alerte à tous les utilisateurs de votre organisation qui se sont abonnés à eux.

## S’abonner aux alertes dans l’interface utilisateur {#subscribe-destination-alerts}

>[!CONTEXTUALHELP]
>id="platform_destination_alerts_subscribe"
>title="S&#39;abonner aux alertes sur les destinations"
>abstract="Les alertes vous permettent de recevoir des notifications en fonction du statut de vos flux de données de destination. Vous pouvez définir des notifications d&#39;alerte pour obtenir des mises à jour si votre flux de données a commencé, a réussi, a échoué ou n&#39;a envoyé aucune donnée à votre destination."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>Vous devez activer les notifications instantanées des e-mails pour votre compte Platform afin de recevoir des notifications d’alerte par e-mail pour vos flux de données.

Vous pouvez activer des alertes pour vos flux de données lors de l’étape [!UICONTROL Configurer une nouvelle destination] du workflow [connexion à la destination](connect-destination.md) .

![Image de l&#39;interface utilisateur affichant la section d&#39;alertes de destination.](../assets/ui/alerts/destination-alerts.png)

Sélectionnez les alertes auxquelles vous souhaitez vous abonner, puis **[!UICONTROL Suivant]** pour revoir et terminer votre flux de données.

Les alertes disponibles pour les flux de données de destination sont décrites dans le tableau ci-dessous.

* Pour les destinations de diffusion en continu, seule l’alerte [!DNL Activation Skipped Rate Exceeded] est disponible.
* Pour les destinations basées sur des fichiers, toutes les alertes sont disponibles.

| Alertes | Description |
| --- | --- |
| Retard de l’exécution du flux de destinations | Cette alerte vous avertit lorsqu’une exécution de flux de destination dure plus de 150 minutes pour activer une audience. |
| Échec de l’exécution du flux de destinations | Cette alerte vous avertit lorsqu’une erreur se produit lors de l’activation d’une audience vers une destination. |
| Succès de l’exécution du flux de destinations | Cette alerte vous avertit lorsqu’une audience est correctement activée vers une destination. |
| Début de l’exécution du flux de destinations | Cette alerte vous avertit lorsqu’une exécution de flux de destination commence à activer une audience. |
| Le taux d’activation ignoré est dépassé | Cette alerte vous avertit lorsque le taux de saut d’activation a dépassé 1 % du total des activations. Les identités sont ignorées lors de l’activation lorsqu’elles comportent des attributs manquants ou une violation du consentement. |

## Recevoir des alertes {#receiving-alerts}

Une fois le flux de données de destination exécuté, vous pouvez recevoir des alertes par le biais de l’interface utilisateur ou par courrier électronique.

### Recevoir des alertes dans l’interface utilisateur {#receiving-alerts-in-ui}

Les alertes sont représentées dans l’interface utilisateur par une icône de notification dans l’en-tête supérieur de l’interface utilisateur de Platform. Sélectionnez l’icône de notification pour afficher des messages d’alerte spécifiques concernant vos flux de données.

![Image de l&#39;interface utilisateur affichant l&#39;icône de notification dans l&#39;Experience Platform](../assets/ui/alerts/notification.png)

Le panneau des notifications s’affiche, affichant une liste des mises à jour d’état du flux de données que vous avez créé.

![Image de l&#39;interface utilisateur affichant le panneau de notification](../assets/ui/alerts/alert-window.png)

Vous pouvez pointer sur un message d’alerte pour le marquer comme lu ou sélectionner l’icône de l’horloge pour définir des rappels futurs sur l’état de votre flux de données.

![Image de l&#39;interface utilisateur affichant les options de rappel de notification](../assets/ui/alerts/remind-me.png)

Sélectionnez le message d’alerte pour afficher des informations spécifiques sur votre flux de données.

![Image de l&#39;interface utilisateur montrant comment sélectionner une notification](../assets/ui/alerts/select-alert-message.png)

La page [!UICONTROL Détails de l’exécution du flux de données] s’affiche. La moitié supérieure de l’écran affiche un aperçu de votre flux de données, y compris des informations sur ses attributs, l’identifiant d’exécution de flux de données correspondant et un résumé d’erreur de haut niveau.

![Image de l’interface utilisateur montrant la page des détails de l’exécution du flux de données.](../assets/ui/alerts/dataflow-overview.png)

La moitié inférieure de la page affiche les [!UICONTROL erreurs d’exécution de flux de données] survenues pendant l’étape d’exécution du flux de données. À partir de là, vous pouvez prévisualiser les diagnostics d’erreur ou utiliser l’ [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) pour télécharger les diagnostics d’erreur ou le manifeste de fichier correspondant à votre flux de données.

![Image de l&#39;interface utilisateur montrant la page des détails de l&#39;exécution du flux de données, avec un surlignage sur la section des erreurs.](../assets/ui/alerts/dataflow-run-error.png)

Pour plus d’informations sur la gestion des erreurs de flux de données, consultez le guide sur la [surveillance des flux de données de destinations dans l’interface utilisateur](../../dataflows/ui/monitor-destinations.md).

### Recevoir des alertes par email {#receiving-alerts-by-email}

Les alertes de vos flux de données vous sont également envoyées par courrier électronique. Sélectionnez le nom du flux de données dans le corps de l’email pour afficher plus d’informations sur votre flux de données.

![Capture d’écran d’un email d’alerte](../assets/ui/alerts/email.png)

Tout comme l’alerte de l’interface utilisateur, la page [!UICONTROL Présentation de l’exécution du flux de données] s’affiche, vous fournissant une interface pour enquêter sur les erreurs associées à votre flux de données.

![dataflow-overview](../assets/ui/alerts/dataflow-overview.png)

## Abonnement et désabonnement aux alertes {#subscribe-and-unsubscribe}

Vous pouvez vous abonner à d’autres alertes ou vous désabonner d’alertes établies pour un flux de données de destination existant dans la page [!UICONTROL Parcourir] des destinations.

![Image de l’interface utilisateur montrant la page de navigation des destinations](../assets/ui/alerts/destination-list.png)

Recherchez la connexion de destination pour laquelle vous souhaitez recevoir des alertes et sélectionnez les ellipses (`...`) pour afficher un menu déroulant d’options. Sélectionnez ensuite **[!UICONTROL S’abonner aux alertes]** pour modifier les paramètres d’alerte de votre flux de données de destination.

![Image de l’interface utilisateur montrant les options de destination](../assets/ui/alerts/destination-alerts-subscribe.png)

Une fenêtre contextuelle s’affiche, vous indiquant la liste des alertes de destination. Sélectionnez les alertes auxquelles vous souhaitez vous abonner ou désélectionnez-les. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![Image de l’interface utilisateur affichant la page d’abonnements aux alertes de destination](../assets/ui/alerts/destination-alerts-list.png)

## Étapes suivantes {#next-steps}

Ce document fournit un guide détaillé sur la manière de s’abonner aux alertes contextuelles pour vos flux de données de destination. Pour plus d’informations, consultez le [guide de l’interface utilisateur d’alertes](../../observability/alerts/ui.md).
