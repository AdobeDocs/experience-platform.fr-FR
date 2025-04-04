---
keywords: Experience Platform;accueil;rubriques populaires;notifications d’ingestion de données;notifications;événements d’abonnement;événements de statut d’ingestion de données;événements de statut;s’abonner;notifications de statut;
solution: Experience Platform
title: Notifications d’ingestion de données
description: Pour faciliter la surveillance du processus d’ingestion, Adobe Experience Platform permet de s’abonner à un ensemble d’événements publiés pour chaque étape du processus, vous informant de l’état des données ingérées et des échecs possibles.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 20%

---

# Notifications d’ingestion de données

Le processus d’ingestion de données dans Adobe Experience Platform se compose de plusieurs étapes. Une fois que vous avez identifié les fichiers de données qui doivent être ingérés dans [!DNL Experience Platform], le processus d’ingestion commence et chaque étape se produit de manière consécutive jusqu’à ce que les données soient correctement ingérées ou échouent. Il est possible d’initier le processus d’ingestion à l’aide de l’API [Adobe Experience Platform Batch Ingestion](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) ou de l’interface utilisateur [!DNL Experience Platform].

Les données chargées dans [!DNL Experience Platform] doivent passer par plusieurs étapes pour atteindre leur destination, le [!DNL Data Lake] ou le magasin de données [!DNL Real-Time Customer Profile]. Chaque étape implique le traitement des données, leur validation, puis leur stockage avant de passer à l’étape suivante. En fonction de la quantité de données ingérée, ce processus peut devenir chronophage et il existe toujours une possibilité qu’il échoue en raison d’erreurs de validation, de sémantique ou de traitement. En cas d’échec, les problèmes de données doivent être résolus, puis l’ensemble du processus d’ingestion doit être redémarré en utilisant des fichiers de données corrigés.

Pour faciliter la surveillance du processus d’ingestion, [!DNL Experience Platform] permet de s’abonner à un ensemble d’événements publiés pour chaque étape du processus, vous informant de l’état des données ingérées et des échecs possibles.

## Enregistrer un webhook pour les notifications d’ingestion de données

Pour recevoir des notifications d’ingestion de données, vous devez utiliser [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) pour enregistrer un webhook auprès de votre intégration Experience Platform.

Suivez le tutoriel sur [l’abonnement aux notifications [!DNL Adobe I/O Event]  ](../../observability/alerts/subscribe.md) pour obtenir des instructions détaillées sur la manière d’y parvenir.

>[!IMPORTANT]
>
>Pendant le processus d’abonnement, veillez à sélectionner **[!UICONTROL Notifications Platform]** comme fournisseur d’événement et à sélectionner l’abonnement à l’événement **[!UICONTROL Notification d’ingestion de données]** lorsque vous y êtes invité.

## Recevoir des notifications d’ingestion de données

Une fois que vous avez enregistré votre webhook et que les nouvelles données ont été ingérées, vous pouvez commencer à recevoir des notifications d’événement. Ces événements peuvent être affichés à l’aide du webhook lui-même ou en sélectionnant l’onglet **[!UICONTROL Debug Tracing]** dans la présentation de l’enregistrement des événements de votre projet dans Adobe Developer Console.

Le fichier JSON suivant est un exemple de payload de notification envoyée à votre webhook en cas d’échec de l’ingestion par lots :

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{ORG_ID}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
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
| `event` | Un objet contenant les détails de l’événement qui a déclenché la notification. |
| `event.xdm:datasetId` | L’identifiant du jeu de données auquel l’événement d’ingestion s’applique. |
| `event.xdm:eventCode` | Code d’état indiquant le type d’événement déclenché pour le jeu de données. Voir [annexe](#event-codes) pour des valeurs spécifiques et leurs définitions. |

Pour afficher le schéma complet des notifications d’événement, reportez-vous au [référentiel GitHub public](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Étapes suivantes

Une fois que vous avez enregistré des notifications [!DNL Experience Platform] dans votre projet, vous pouvez afficher les événements reçus à partir de la [!UICONTROL Présentation du projet]. Reportez-vous au guide sur le [suivi de Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) pour obtenir des instructions détaillées sur la manière de suivre vos événements.

## Annexe

La section suivante contient des informations supplémentaires sur l’interprétation des payloads des notifications d’ingestion de données.

### Événements de notification d’état disponibles {#event-codes}

Le tableau suivant répertorie les notifications de statut d’ingestion des données auxquelles vous pouvez vous abonner.

| Code d’événement | Service Experience Platform | État | Description des événements |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | Un lot a bien été ingéré dans un jeu de données dans le [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | failure | Un lot n’a pas pu être ingéré dans un jeu de données dans le [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | success | Un lot a bien été ingéré dans le magasin de données [!DNL Profile]. |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | failure | Un lot n’a pas pu être ingéré dans le magasin de données [!DNL Profile]. |
| `ig_load_success` | [!DNL Identity Service] | success | Les données ont été chargées dans le graphique d’identité. |
| `ig_load_failure` | [!DNL Identity Service] | failure | Échec du chargement des données dans le graphique d’identité. |

>[!NOTE]
>
>Une seule rubrique d’événement est fournie pour toutes les notifications d’ingestion de données. Vous pouvez utiliser le code d’événement pour faire la distinction entre les différents états.
