---
keywords: Experience Platform;accueil;rubriques les plus consultées ; alertes
description: Vous pouvez vous abonner à des alertes lors de la création d’un flux de données pour recevoir des messages d’alerte concernant l’état, la réussite ou l’échec de votre exécution de flux.
title: Abonnement à des alertes contextuelles dans l’interface utilisateur
exl-id: 5d51edaa-ecba-4ac0-8d3c-49010466b9a5
source-git-commit: d450dc7b0dc0303c9d33c3e8e003659e3140cf5b
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 17%

---

# Abonnement aux alertes pour les flux de données de sources dans l’interface utilisateur

Adobe Experience Platform vous permet de vous abonner à des alertes basées sur des événements concernant les activités Adobe Experience Platform. Les alertes réduisent ou éliminent la nécessité d’interroger l’[[!DNL Observability Insights] API](../../../observability/api/overview.md) afin de vérifier si une tâche est terminée, si un certain jalon a été atteint dans un processus ou si des erreurs se sont produites.

Vous pouvez vous abonner aux alertes lors de la création d’un flux de données pour recevoir des messages d’alerte concernant le statut, le succès ou l’échec de l’exécution de votre flux de données.

Ce document décrit les étapes à suivre pour s’abonner à des messages d’alerte pour les flux de données de vos sources.

## Prise en main

Ce document nécessite une compréhension pratique des composants suivants de Adobe Experience Platform :

* [Sources ](../../home.md): [!DNL Experience Platform]permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services [!DNL Platform].
* [Observability vous permet de surveiller les activités de Platform en utilisant des mesures statistiques et des notifications dʼévénement.](../../../observability/home.md)[!DNL Observability Insights]
   * [Alertes](../../../observability/alerts/overview.md): Lorsqu’un certain ensemble de conditions de vos opérations Platform est atteint (par exemple, un problème potentiel lorsque le système enfreint un seuil), Platform peut envoyer des messages d’alerte à tous les utilisateurs de votre organisation qui se sont abonnés à eux.

## Abonnement aux alertes dans l’interface utilisateur {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="S’abonner aux alertes sur les sources"
>abstract="Les alertes vous permettent de recevoir des notifications en fonction de l’état des flux de données de vos sources. Vous pouvez définir des notifications d’alerte pour obtenir des mises à jour si votre flux de données a démarré, a réussi, a échoué ou n’a ingéré aucune donnée."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>Vous devez activer les notifications instantanées des e-mails pour votre compte Platform afin de recevoir des notifications d’alerte par e-mail pour vos flux de données.

Vous pouvez activer des alertes pour vos flux de données pendant la [!UICONTROL Détails du flux de données] de l’étape du workflow sources dans l’espace de travail sources .

![dataflow-detail](../../images/tutorials/alerts/dataflow-detail.png)

Les alertes disponibles pour les flux de données de sources sont les suivantes :

| Alertes | Description |
| --- | --- |
| Démarrage de l’exécution du flux de données sources | Cette alerte vous envoie un message lorsque votre flux de données source a démarré. |
| Réussite de l’exécution du flux de données sources | Cette alerte vous envoie un message lorsque les données de votre source sont correctement ingérées dans Platform. |
| Échec de l’exécution des flux de données sources | Cette alerte vous envoie un message si une erreur se produit dans votre flux de données. |
| ~~Sources Flux de données : absence d’ingestion~~ | ~~Cette alerte vous envoie un message si l’ingestion est retardée de plus de sept heures et qu’aucune donnée n’est ingérée dans Platform.~~ <br>**Remarque :** Vous ne recevrez plus d’alertes car cette alerte est obsolète. |

Sélectionnez les alertes auxquelles vous souhaitez vous abonner, puis sélectionnez **[!UICONTROL Suivant]** pour passer en revue et terminer votre flux de données.

![select-alertes](../../images/tutorials/alerts/select-alerts.png)

Pour obtenir des instructions détaillées sur la création d’un flux de données de sources dans l’interface utilisateur, consultez les guides suivants :

* [Advertising](./dataflow/advertising.md)
* [Stockage dans le cloud](./dataflow/batch/cloud-storage.md)
* [CRM](./dataflow/crm.md)
* [Base de données](./dataflow/databases.md)
* [Commerce électronique](./dataflow/ecommerce.md)
* [Fichiers locaux](./create/local-system/local-file-upload.md)
* [Automatisation du marketing](./dataflow/marketing-automation.md)
* [Paiements](./dataflow/payments.md)
* [Protocoles](./dataflow/protocols.md)

## Recevoir des alertes

Une fois votre flux de données exécuté, vous pouvez recevoir des alertes par le biais de l’interface utilisateur ou par courrier électronique.

### Dans l’interface utilisateur

Les alertes sont représentées dans l’interface utilisateur par une icône de notification dans l’en-tête supérieur de l’interface utilisateur de Platform. Sélectionnez l’icône de notification pour afficher des messages d’alerte spécifiques concernant vos flux de données.

![notification](../../images/tutorials/alerts/notification.png)

Le panneau des notifications s’affiche, affichant une liste des mises à jour d’état du flux de données que vous avez créé.

![alert-window](../../images/tutorials/alerts/alert-window.png)

Vous pouvez pointer sur un message d’alerte pour le marquer comme lu ou sélectionner l’icône de l’horloge pour définir des rappels futurs sur l’état de votre flux de données.

![rappel-moi](../../images/tutorials/alerts/remind-me.png)

Sélectionnez le message d’alerte pour afficher des informations spécifiques sur votre flux de données.

![select-alert-message](../../images/tutorials/alerts/select-alert-message.png)

Le [!UICONTROL Présentation de l’exécution du flux de données] s’affiche. La moitié supérieure de l’écran affiche un aperçu de votre flux de données, y compris des informations sur ses attributs, l’identifiant d’exécution de flux de données correspondant et un résumé d’erreur de haut niveau.

![dataflow-overview](../../images/tutorials/alerts/dataflow-overview.png)

La moitié inférieure de la page affiche toutes les [!UICONTROL Erreurs d’exécution du flux de données] qui se produisaient pendant l’étape d’exécution du flux de données. À partir de là, vous pouvez prévisualiser les diagnostics d’erreur ou utiliser le [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) pour télécharger les diagnostics d’erreur ou le manifeste de fichier correspondant à votre flux de données.

![dataflow-run-errors](../../images/tutorials/alerts/dataflow-run-error.png)

Pour plus d’informations sur la gestion des erreurs de flux de données, consultez le guide sur [surveillance des flux de données de sources dans l’interface utilisateur](../../../dataflows/ui/monitor-sources.md).

### Par email

Les alertes de vos flux de données vous sont également envoyées par courrier électronique. Sélectionnez le nom du flux de données dans le corps de l’email pour afficher plus d’informations sur votre flux de données.

![e-mail](../../images/tutorials/alerts/email.png)

Tout comme l’alerte de l’interface utilisateur, la variable [!UICONTROL Présentation de l’exécution du flux de données] s’affiche, vous fournissant une interface permettant d’enquêter sur les erreurs associées à votre flux de données.

![dataflow-overview](../../images/tutorials/alerts/dataflow-overview.png)

## Abonnement et désabonnement aux alertes

Vous pouvez vous abonner à d’autres alertes ou vous désabonner d’alertes établies pour un flux de données existant dans la variable [!UICONTROL Flux de données] page. Recherchez le flux de données que vous créez dans la liste, puis sélectionnez les ellipses (`...`) pour afficher un menu déroulant d’options. Ensuite, sélectionnez **[!UICONTROL Abonner des alertes]** pour modifier les paramètres d’alerte de votre flux de données.

![Options](../../images/tutorials/alerts/options.png)

Une fenêtre contextuelle s’affiche, vous indiquant la liste des alertes de sources. Sélectionnez les alertes auxquelles vous souhaitez vous abonner ou désélectionnez-les. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]**.

![save](../../images/tutorials/alerts/save.png)

## Étapes suivantes

Ce document fournit un guide détaillé sur la manière de s’abonner aux alertes contextuelles pour vos flux de données de sources. Pour plus d’informations, voir [guide de l’interface utilisateur des alertes](../../../observability/alerts/ui.md).