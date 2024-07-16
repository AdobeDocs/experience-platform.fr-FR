---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Abonnement à des événements de Privacy Service
description: Découvrez comment vous abonner aux événements de Privacy Service à l’aide d’un webhook préconfiguré.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 8%

---

# Abonnez-vous à [!DNL Privacy Service Events]

[!DNL Privacy Service Events] sont des messages fournis par Adobe Experience Platform [!DNL Privacy Service], qui tirent parti des événements d’Adobe I/O envoyés à un webhook configuré pour faciliter l’automatisation efficace des requêtes de tâche. Elles réduisent ou éliminent la nécessité d’interroger l’API [!DNL Privacy Service] afin de vérifier si une tâche est terminée ou si un certain jalon a été atteint dans un workflow.

Il existe actuellement quatre types de notifications liées au cycle de vie de la tâche de demande d’accès à des informations personnelles :

| Type | Description |
| --- | --- |
| Fin de tâche | Toutes les applications [!DNL Experience Cloud] ont fait l’objet de rapports et l’état global ou global de la tâche a été marqué comme étant terminé. |
| Erreur de tâche | Une ou plusieurs applications ont signalé une erreur lors du traitement de la requête. |
| Produit terminé | Une des applications associées à cette tâche a terminé son travail. |
| Erreur de produit | L’une des applications a signalé une erreur lors du traitement de la requête. |

Ce document décrit les étapes de configuration d’un enregistrement d’événement pour les notifications [!DNL Privacy Service] et comment interpréter les payloads des notifications.

## Commencer

Avant de commencer ce tutoriel, consultez la documentation du Privacy Service suivante :

* [Présentation de Privacy Service](./home.md)
* [Guide de l’API Privacy Service](./api/overview.md)

## Enregistrer un webhook sur [!DNL Privacy Service Events]

Pour recevoir [!DNL Privacy Service Events], vous devez utiliser Adobe Developer Console pour enregistrer un webhook dans votre intégration [!DNL Privacy Service].

Suivez le tutoriel [abonnement aux notifications [!DNL I/O Event]](../observability/alerts/subscribe.md) pour obtenir des instructions détaillées sur la manière d’y parvenir. Veillez à choisir **[!UICONTROL Événements de Privacy Service]** comme fournisseur d’événements afin d’accéder aux événements répertoriés ci-dessus.

## Recevoir [!DNL Privacy Service Event] notifications

Une fois que vous avez enregistré votre webhook et que les tâches de confidentialité ont été exécutées, vous pouvez commencer à recevoir des notifications d’événement. Ces événements peuvent être visualisés à l’aide du webhook lui-même ou en sélectionnant l’onglet **[!UICONTROL Suivi du débogage]** dans la présentation de l’enregistrement des événements de votre projet dans Adobe Developer Console.

![](images/privacy-events/debug-tracing.png)

Le fichier JSON suivant est un exemple de payload de notification [!DNL Privacy Service Event] qui serait envoyé à votre webhook lorsque l’une des applications associées à une tâche de confidentialité a terminé son travail :

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{ORG_ID}",
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
| `type` | Le type de notification en cours d’envoi, en mettant en contexte les informations fournies sous `data`. Les valeurs potentielles sont les suivantes : <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Horodatage de l’événement. |
| `data.value` | Contient des informations supplémentaires sur ce qui a déclenché la notification : <ul><li>`jobId` : identifiant de la tâche de confidentialité qui a déclenché la notification.</li><li>`message` : message concernant l’état spécifique de la tâche. Pour les notifications `productcomplete` ou `producterror`, ce champ indique l’application Experience Cloud en question.</li></ul> |

## Étapes suivantes

Ce document explique comment enregistrer des événements de Privacy Service dans un webhook configuré et comment interpréter les payloads de notification. Pour savoir comment suivre les tâches de confidentialité à l’aide de l’interface utilisateur, consultez le [guide de l’utilisateur du Privacy Service](./ui/user-guide.md).
