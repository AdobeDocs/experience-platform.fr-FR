---
keywords: Experience Platform ; accueil ; rubriques populaires ; notifications d'assimilation de données ; notifications ; événements d'abonnement ; événements d'état d'assimilation de données ; événements d'état ; abonnement ; notifications d'état ;
solution: Experience Platform
title: Notifications d'importation de données
topic-legacy: overview
description: Pour faciliter le suivi du processus d'assimilation, Adobe Experience Platform permet de s'abonner à un ensemble de événements publiés à chaque étape du processus, en vous informant de l'état des données ingérées et de toute erreur éventuelle.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 29%

---

# Notifications d’ingestion de données

Le processus d’ingestion de données dans Adobe Experience Platform se compose de plusieurs étapes. Une fois que vous avez identifié les fichiers de données à ingérer dans [!DNL Platform], le processus d&#39;assimilation commence et chaque étape se produit consécutivement jusqu&#39;à ce que les données soient correctement ingérées ou échouent. Il est possible d’initier le processus d’ingestion à l’aide de l’[API Data Ingestion d’Adobe ](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) ou de l’interface utilisateur Experience Platform.[!DNL Experience Platform]

Les données chargées dans [!DNL Platform] doivent suivre plusieurs étapes pour atteindre leur destination, le [!DNL Data Lake] ou le magasin de données [!DNL Real-time Customer Profile]. Chaque étape implique le traitement des données, leur validation, puis leur stockage avant de passer à l’étape suivante. En fonction de la quantité de données ingérée, ce processus peut devenir chronophage et il existe toujours une possibilité qu’il échoue en raison d’erreurs de validation, de sémantique ou de traitement. En cas d’échec, les problèmes de données doivent être résolus, puis l’ensemble du processus d’ingestion doit être redémarré en utilisant des fichiers de données corrigés.

Pour vous aider à surveiller le processus d&#39;assimilation, [!DNL Experience Platform] permet de vous abonner à un ensemble de événements publiés à chaque étape du processus, en vous informant de l&#39;état des données ingérées et de tout échec éventuel.

## Enregistrement d’un crochet Web pour les notifications d’assimilation de données

Pour recevoir des notifications d&#39;assimilation de données, vous devez utiliser [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_fr) pour enregistrer un webhook dans votre intégration Experience Platform.

Suivez le didacticiel sur [l&#39;abonnement aux  [!DNL Adobe I/O Event] notifications](../../observability/notifications/subscribe.md) pour obtenir des instructions détaillées sur la façon d&#39;y parvenir.

>[!IMPORTANT]
>
>Au cours du processus d’abonnement, veillez à sélectionner **[!UICONTROL Notifications de plateforme]** comme fournisseur de événement et à sélectionner l’abonnement de événement **[!UICONTROL Notification d’assimilation de données]** lorsque vous y êtes invité.

## Recevoir des notifications d&#39;assimilation de données

Une fois que vous avez enregistré votre webhook et que de nouvelles données ont été ingérées, vous pouvez début recevoir des notifications de événement. Ces événements peuvent être visualisés à l’aide de webhook lui-même ou en sélectionnant l’onglet **[!UICONTROL Suivi du débogage]** dans l’aperçu de l’enregistrement des événements de votre projet dans Adobe Developer Console.

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
| `event.xdm:eventCode` | Code d’état indiquant le type de événement déclenché pour le jeu de données. Voir l&#39;[appendice](#event-codes) pour connaître les valeurs spécifiques et leurs définitions. |

Pour vue le schéma complet des notifications de événement, consultez le [référentiel GitHub public](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Étapes suivantes

Une fois que vous avez enregistré des notifications [!DNL Platform] à votre projet, vous pouvez vue les événements reçus de l&#39;[!UICONTROL Aperçu du projet]. Pour obtenir des instructions détaillées sur la façon de tracer vos événements, consultez le guide sur les [Événements de suivi des Adobes I/O](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md).

## Annexe

La section suivante contient des informations supplémentaires sur l&#39;interprétation des charges utiles de notification d&#39;assimilation de données.

### Événements de notification d’état disponibles {#event-codes}

Le tableau suivant liste les notifications d&#39;état d&#39;assimilation de données disponibles auxquelles vous pouvez vous abonner.

| Code d’événement | Service Platform | État | Description des événements |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | Un lot a été assimilé à un jeu de données dans [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | failure | Échec de l&#39;assimilation d&#39;un lot dans un jeu de données dans [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-time Customer Profile] | succès | Un lot a été assimilé à un lot dans le magasin de données [!DNL Profile]. |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | échec | Échec de l&#39;assimilation d&#39;un lot dans le magasin de données [!DNL Profile]. |
| `ig_load_success` | [!DNL Identity Service] | succès | Les données ont été chargées avec succès dans le graphique d&#39;identité. |
| `ig_load_failure` | [!DNL Identity Service] | échec | Échec du chargement des données dans le graphique d&#39;identité. |

>[!NOTE]
>
>Il n’y a qu’une seule rubrique d’événement fournie pour toutes les notifications d’ingestion de données. Vous pouvez utiliser le code d’événement pour faire la distinction entre les différents états.
