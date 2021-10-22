---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: S’abonner à des événements Privacy Service
topic-legacy: privacy events
description: Découvrez comment vous abonner à des événements Privacy Service à l’aide d’un webhook préconfiguré.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 15%

---

# S’abonner à [!DNL Privacy Service Events]

[!DNL Privacy Service Events] sont des messages fournis par Adobe Experience Platform [!DNL Privacy Service], qui tirent parti des événements d&#39;Adobe I/O envoyés à un webhook configuré pour faciliter l&#39;automatisation efficace des demandes d&#39;emploi. Ils réduisent ou éliminent la nécessité de consulter l’API [!DNL Privacy Service] pour savoir si une tâche est terminée ou si un certain jalon a été atteint dans un workflow.

Il existe actuellement quatre types de notifications liées au cycle de vie de la tâche de demande d’accès à des informations personnelles :

| Type | Description |
| --- | --- |
| Fin de tâche | Tout [!DNL Experience Cloud] les demandes ont fait l&#39;objet d&#39;un rapport et l&#39;état global ou global de la tâche a été marqué comme terminé. |
| Erreur de tâche | Une ou plusieurs applications ont signalé une erreur lors du traitement de la demande. |
| Produit terminé | Une des applications associées à ce travail a terminé son travail. |
| Erreur de produit | Une des applications a signalé une erreur lors du traitement de la demande. |

Ce document fournit les étapes permettant de configurer un enregistrement d’événement pour [!DNL Privacy Service] et comment interpréter les charges de notification.

## Prise en main

Avant de commencer ce tutoriel, consultez la documentation Privacy Service suivante :

* [Présentation de Privacy Service](./home.md)
* [Guide de l’API Privacy Service](./api/overview.md)

## Enregistrer un webhook pour [!DNL Privacy Service Events]

Pour recevoir [!DNL Privacy Service Events], vous devez utiliser Adobe Developer Console pour enregistrer un webhook dans votre [!DNL Privacy Service] intégration.

Suivez le tutoriel sur [abonnement à [!DNL I/O Event] notifications](../observability/alerts/subscribe.md) pour des étapes détaillées sur la façon d’y parvenir. Assurez-vous de choisir **[!UICONTROL Événements Privacy Service]** en tant que fournisseur d’événements afin d’accéder aux événements répertoriés ci-dessus.

## Réception [!DNL Privacy Service Event] notifications

Une fois que vous avez correctement enregistré vos travaux de webhook et de confidentialité exécutés, vous pouvez commencer à recevoir des notifications d’événements. Ces événements peuvent être affichés à l’aide du webhook lui-même ou en sélectionnant l’option **[!UICONTROL Suivi du débogage]** dans la vue d’ensemble de l’enregistrement des événements de votre projet dans Adobe Developer Console.

![](images/privacy-events/debug-tracing.png)

Le fichier JSON suivant est un exemple de [!DNL Privacy Service Event] charge utile de notification qui serait envoyée à votre webhook lorsque l’une des applications associées à une tâche de confidentialité a terminé son travail :

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
| `id` | ID unique généré par le système pour la notification. |
| `type` | Le type de notification à envoyer, en donnant le contexte des informations fournies sous `data`. Les valeurs possibles sont les suivantes : <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Horodatage de l’événement. |
| `data.value` | Contient des informations supplémentaires sur ce qui a déclenché la notification : <ul><li>`jobId`: ID de la tâche de confidentialité qui a déclenché la notification.</li><li>`message`: Un message concernant l&#39;état spécifique du travail. Pour `productcomplete` ou `producterror` , ce champ indique l’application Experience Cloud en question.</li></ul> |

## Étapes suivantes

Ce document explique comment enregistrer des événements Privacy Service dans un webhook configuré et comment interpréter les charges de notification. Pour savoir comment suivre les tâches de confidentialité à l’aide de l’interface utilisateur, consultez la section [Guide de l’utilisateur Privacy Service](./ui/user-guide.md).
