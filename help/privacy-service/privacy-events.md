---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: S'abonner aux Événements Privacy Service
topic: privacy events
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 7%

---


# S’abonner à [!DNL Privacy Service Events]

[!DNL Privacy Service Events] sont des messages fournis par Adobe Experience Platform [!DNL Privacy Service], qui tirent parti des Événements d&#39;E/S d&#39;Adobe envoyés à un webhook configuré pour faciliter l&#39;automatisation efficace des demandes d&#39;emploi. They reduce or eliminate the need to poll the [!DNL Privacy Service] API in order to check if a job is complete or if a certain milestone within a workflow has been reached.

Il existe actuellement quatre types de notifications liées au cycle de vie de la tâche de demande d’accès à des informations personnelles :

| Type | Description |
| --- | --- |
| Fin de tâche | All [!DNL Experience Cloud] applications have reported back and the overall or global status of the job has been marked as complete. |
| Erreur de tâche | Une ou plusieurs applications ont signalé une erreur lors du traitement de la demande. |
| Produit terminé | Une des demandes associées à ce travail a terminé son travail. |
| Erreur de produit | L’une des applications a signalé une erreur lors du traitement de la demande. |

Ce document décrit la procédure à suivre pour configurer un enregistrement de événement pour les [!DNL Privacy Service] notifications et pour interpréter les charges utiles des notifications.

## Prise en main

Veuillez consulter la documentation Privacy Service suivante avant de commencer ce didacticiel :

* [Présentation de Privacy Service](./home.md)
* [Guide du développeur d&#39;API Privacy Service](./api/getting-started.md)

## Enregistrement d’un webhook dans [!DNL Privacy Service Events]

Pour pouvoir recevoir [!DNL Privacy Service Events]des informations, vous devez utiliser Adobe Developer Console pour enregistrer un webhook dans votre [!DNL Privacy Service] intégration.

Suivez le didacticiel sur les [tonotifications [!DNL I/O Event] ](../observability/notifications/subscribe.md) d’abonnement pour obtenir des instructions détaillées sur la façon d’y parvenir. Veillez à choisir des Événements **** Privacy Service comme fournisseur de événements afin d’accéder aux événements répertoriés ci-dessus.

## Recevoir [!DNL Privacy Service Event] des notifications

Une fois que vous avez enregistré votre webhook et que les tâches de confidentialité ont été exécutées, vous pouvez début recevoir des notifications de événement. Ces événements peuvent être visualisés à l&#39;aide du crochet Web lui-même ou en sélectionnant l&#39;onglet Suivi **[!UICONTROL du]** débogage dans l&#39;aperçu de l&#39;enregistrement des événements de votre projet dans Adobe Developer Console.

![](images/privacy-events/debug-tracing.png)

L’objet JSON suivant est un exemple de charge utile de [!DNL Privacy Service Event] notification qui serait envoyée à votre webhook lorsque l’une des applications associées à une tâche de confidentialité a terminé son travail :

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{IMS_ORG}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| Propriété | Description |
| --- | --- |
| `id` | Identifiant unique généré par le système pour la notification. |
| `type` | Type de notification envoyée, en donnant un contexte aux informations fournies sous `data`. Les valeurs potentielles sont les suivantes : <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Horodatage du moment où le événement s’est produit. |
| `data.value` | Contient des informations supplémentaires sur ce qui a déclenché la notification : <ul><li>`jobId`: ID de la tâche de confidentialité qui a déclenché la notification.</li><li>`message`: Message concernant l’état spécifique de la tâche. Pour les `productcomplete` notifications ou `producterror` les notifications, ce champ indique l’application Experience Cloud en question.</li></ul> |

## Étapes suivantes

Ce document décrit comment enregistrer des Événements Privacy Service sur un crochet Web configuré et comment interpréter les charges utiles de notification. Pour savoir comment suivre les tâches de confidentialité à l’aide de l’interface utilisateur, consultez le guide [d’utilisation du](./ui/user-guide.md)Privacy Service.