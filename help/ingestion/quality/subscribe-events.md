---
keywords: Experience Platform;home;popular topics;data ingestion notifications;notifications;subscribe events;data ingestion status events;status events;subscribe;status notifications;
solution: Experience Platform
title: Abonnement aux événements d’ingestion de données
topic: overview
description: Pour faciliter le suivi du processus d'assimilation, Adobe Experience Platform permet de s'abonner à un ensemble de événements publiés à chaque étape du processus, en vous informant de l'état des données ingérées et de toute erreur éventuelle.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 30%

---


# Notifications d’ingestion de données

Le processus d’ingestion de données dans Adobe Experience Platform se compose de plusieurs étapes. Once you identify data files that need to be ingested into [!DNL Platform], the ingestion process begins and each step occurs consecutively until the data is either successfully ingested or fails. Il est possible d’initier le processus d’ingestion à l’aide de l’[API Data Ingestion d’Adobe ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) ou de l’interface utilisateur Experience Platform.[!DNL Experience Platform]

Data loaded into [!DNL Platform] must go through multiple steps in order to reach its destination, the [!DNL Data Lake] or the [!DNL Real-time Customer Profile] data store. Chaque étape implique le traitement des données, leur validation, puis leur stockage avant de passer à l’étape suivante. En fonction de la quantité de données ingérée, ce processus peut devenir chronophage et il existe toujours une possibilité qu’il échoue en raison d’erreurs de validation, de sémantique ou de traitement. En cas d’échec, les problèmes de données doivent être résolus, puis l’ensemble du processus d’ingestion doit être redémarré en utilisant des fichiers de données corrigés.

To assist in monitoring the ingestion process, [!DNL Experience Platform] makes it possible to subscribe to a set of events that are published by each step of the process, notifying you to the status of the ingested data and any possible failures.

## Enregistrement d’un crochet Web pour les notifications d’assimilation de données

Pour recevoir des notifications d&#39;assimilation de données, vous devez utiliser [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_fr) pour enregistrer un webhook dans votre intégration Experience Platform.

Suivez le didacticiel sur les [tonotifications [!DNL Adobe I/O Event] ](../../observability/notifications/subscribe.md) d’abonnement pour obtenir des instructions détaillées sur la façon d’y parvenir.

>[!IMPORTANT]
>
>Au cours du processus d’abonnement, veillez à sélectionner les notifications **[!UICONTROL de]** plateforme en tant que fournisseur de événement et à sélectionner l’abonnement de événement de notification **[!UICONTROL d’ingestion de]** données lorsque vous y êtes invité.

## Recevoir des notifications d&#39;assimilation de données

Une fois que vous avez enregistré votre webhook et que de nouvelles données ont été ingérées, vous pouvez début recevoir des notifications de événement. Ces événements peuvent être visualisés à l&#39;aide du crochet Web lui-même ou en sélectionnant l&#39;onglet Suivi **[!UICONTROL du]** débogage dans l&#39;aperçu de l&#39;enregistrement des événements de votre projet dans Adobe Developer Console.

Le fichier JSON suivant est un exemple de charge utile de notification qui serait envoyée à votre webhook en cas d’échec d’un événement d’assimilation par lots :

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{IMS_ORG}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
        "providerMetadata": "aep_observability_catalog_events",
        "eventCode": "platform_event"
      }
    }
  }
}
```

| Propriété | Description |
| --- | --- |
| `event_id` | Identifiant unique généré par le système pour la notification. |
| `event` | Objet contenant les détails du événement qui a déclenché la notification. |
| `event.xdm:datasetId` | ID du jeu de données auquel s&#39;applique le événement d&#39;assimilation. |
| `event.xdm:eventCode` | Code d’état indiquant le type de événement déclenché pour le jeu de données. Consultez l&#39; [annexe](#event-codes) pour connaître les valeurs spécifiques et leurs définitions. |

Pour vue le schéma complet des notifications de événement, consultez le référentiel [GitHub](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)public.

## Étapes suivantes

Une fois que vous avez enregistré [!DNL Platform] des notifications à votre projet, vous pouvez vue recevoir des événements de la présentation [!UICONTROL du]projet. Refer to the guide on [tracing Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) for detailed instructions on how to trace your events.

## Annexe

La section suivante contient des informations supplémentaires sur l&#39;interprétation des charges utiles de notification d&#39;assimilation de données.

### Événements de notification d’état disponibles {#event-codes}

Le tableau suivant liste les notifications d&#39;état d&#39;assimilation de données disponibles auxquelles vous pouvez vous abonner.

| Code d’événement | Service Platform | État | Description des événements |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | Un lot a réussi à être assimilé à un jeu de données au sein du [!DNL Data Lake]groupe. |
| `ing_load_failure` | [!DNL Data Ingestion] | failure | Échec de l&#39;assimilation d&#39;un lot dans un jeu de données au sein du [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-time Customer Profile] | success | Un lot a été assimilé à un lot dans le magasin de [!DNL Profile] données. |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | failure | Échec de l&#39;assimilation d&#39;un lot dans le magasin de [!DNL Profile] données. |
| `ig_load_success` | [!DNL Identity Service] | success | Les données ont été chargées avec succès dans le graphique d&#39;identité. |
| `ig_load_failure` | [!DNL Identity Service] | failure | Échec du chargement des données dans le graphique d&#39;identité. |

>[!NOTE]
>
>Il n’y a qu’une seule rubrique d’événement fournie pour toutes les notifications d’ingestion de données. Vous pouvez utiliser le code d’événement pour faire la distinction entre les différents états.