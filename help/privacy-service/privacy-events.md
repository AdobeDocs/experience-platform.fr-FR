---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: S'abonner aux Événements Privacy Service
topic-legacy: privacy events
description: Découvrez comment vous abonner à des événements Privacy Service à l’aide d’un crochet Web préconfiguré.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 7%

---

# S&#39;abonner à [!DNL Privacy Service Events]

[!DNL Privacy Service Events] sont des messages fournis par Adobe Experience Platform  [!DNL Privacy Service], qui tirent parti des Événements d&#39;Adobe I/O envoyés à un webhook configuré pour faciliter l&#39;automatisation efficace des demandes d&#39;emploi. Elles réduisent ou éliminent la nécessité de consulter l&#39;API [!DNL Privacy Service] afin de vérifier si une tâche est terminée ou si un certain jalon dans un flux de travail a été atteint.

Il existe actuellement quatre types de notifications liées au cycle de vie de la tâche de demande d’accès à des informations personnelles :

| Type | Description |
| --- | --- |
| Fin de tâche | Toutes les demandes [!DNL Experience Cloud] ont fait l&#39;objet d&#39;un rapport et l&#39;état global ou global de la tâche a été signalé comme terminé. |
| Erreur de tâche | Une ou plusieurs applications ont signalé une erreur lors du traitement de la demande. |
| Produit terminé | Une des demandes associées à ce travail a terminé son travail. |
| Erreur de produit | L’une des applications a signalé une erreur lors du traitement de la demande. |

Ce document décrit la procédure à suivre pour configurer un enregistrement de événement pour les notifications [!DNL Privacy Service] et comment interpréter les charges utiles de notification.

## Prise en main

Veuillez consulter la documentation Privacy Service suivante avant de commencer ce didacticiel :

* [Présentation de Privacy Service](./home.md)
* [Guide du développeur d&#39;API Privacy Service](./api/getting-started.md)

## Enregistrez webhook à [!DNL Privacy Service Events].

Pour recevoir [!DNL Privacy Service Events], vous devez utiliser Adobe Developer Console pour enregistrer un webhook dans votre intégration [!DNL Privacy Service].

Suivez le didacticiel sur [l&#39;abonnement aux  [!DNL I/O Event] notifications](../observability/notifications/subscribe.md) pour obtenir des instructions détaillées sur la façon d&#39;y parvenir. Veillez à choisir **[!UICONTROL Événements Privacy Service]** comme fournisseur de événements pour accéder aux événements répertoriés ci-dessus.

## Recevoir des [!DNL Privacy Service Event] notifications

Une fois que vous avez enregistré votre webhook et que les tâches de confidentialité ont été exécutées, vous pouvez début recevoir des notifications de événement. Ces événements peuvent être visualisés à l’aide de webhook lui-même ou en sélectionnant l’onglet **[!UICONTROL Suivi du débogage]** dans l’aperçu de l’enregistrement des événements de votre projet dans Adobe Developer Console.

![](images/privacy-events/debug-tracing.png)

L’objet JSON suivant est un exemple de charge utile de notification [!DNL Privacy Service Event] qui serait envoyée à votre webhook lorsque l’une des applications associées à une tâche de confidentialité a terminé son travail :

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
| `type` | Type de notification envoyée, donnant un contexte aux informations fournies sous `data`. Les valeurs potentielles sont les suivantes : <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Horodatage du moment où le événement s’est produit. |
| `data.value` | Contient des informations supplémentaires sur ce qui a déclenché la notification : <ul><li>`jobId`: ID de la tâche de confidentialité qui a déclenché la notification.</li><li>`message`: Message concernant l’état spécifique de la tâche. Pour les notifications `productcomplete` ou `producterror`, ce champ indique l&#39;application Experience Cloud en question.</li></ul> |

## Étapes suivantes

Ce document décrit comment enregistrer des Événements Privacy Service sur un crochet Web configuré et comment interpréter les charges utiles de notification. Pour savoir comment suivre les tâches de confidentialité à l’aide de l’interface utilisateur, consultez le [guide de l’utilisateur Privacy Service](./ui/user-guide.md).
