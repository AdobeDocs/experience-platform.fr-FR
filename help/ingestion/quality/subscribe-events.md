---
keywords: Experience Platform;accueil;rubriques populaires;notifications d’ingestion de données;notifications;événements d’abonnement;événements d’état d’ingestion de données;événements d’état;abonner;notifications d’état;
solution: Experience Platform
title: Notifications d’ingestion de données
description: Pour faciliter la surveillance du processus d’ingestion, Adobe Experience Platform permet de s’abonner à un ensemble d’événements publiés par chaque étape du processus, vous informant de l’état des données ingérées et des échecs possibles.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 20%

---

# Notifications d’ingestion de données

Le processus d’ingestion de données dans Adobe Experience Platform se compose de plusieurs étapes. Une fois que vous avez identifié les fichiers de données à ingérer dans [!DNL Platform], le processus d’ingestion commence et chaque étape se produit consécutivement jusqu’à ce que les données soient correctement ingérées ou échouent. Le processus d’ingestion peut être lancé à l’aide de l’ [API d’ingestion par lots Adobe Experience Platform](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) ou de l’interface utilisateur [!DNL Experience Platform].

Les données chargées dans [!DNL Platform] doivent passer par plusieurs étapes pour atteindre leur destination, l’ [!DNL Data Lake] ou l’ [!DNL Real-Time Customer Profile] entrepôt de données. Chaque étape implique le traitement des données, leur validation, puis leur stockage avant de passer à l’étape suivante. En fonction de la quantité de données ingérée, ce processus peut devenir chronophage et il existe toujours une possibilité qu’il échoue en raison d’erreurs de validation, de sémantique ou de traitement. En cas d’échec, les problèmes de données doivent être résolus, puis l’ensemble du processus d’ingestion doit être redémarré en utilisant des fichiers de données corrigés.

Pour faciliter la surveillance du processus d’ingestion, [!DNL Experience Platform] permet d’abonner à un ensemble d’événements publiés par chaque étape du processus, vous informant de l’état des données ingérées et des échecs possibles.

## Enregistrement d’un webhook pour les notifications d’ingestion de données

Pour recevoir des notifications d’ingestion de données, vous devez utiliser [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) pour enregistrer un webhook dans votre intégration Experience Platform.

Suivez le tutoriel [abonnement à [!DNL Adobe I/O Event] notifications](../../observability/alerts/subscribe.md) pour obtenir des instructions détaillées sur la manière d’y parvenir.

>[!IMPORTANT]
>
>Pendant le processus d’abonnement, veillez à sélectionner **[!UICONTROL Notifications Platform]** en tant que fournisseur d’événement, et à sélectionner l’abonnement à l’événement **[!UICONTROL Notification d’ingestion de données]** lorsque vous y êtes invité.

## Réception de notifications d’ingestion de données

Une fois que vous avez enregistré votre webhook et que de nouvelles données ont été ingérées, vous pouvez commencer à recevoir des notifications d’événement. Ces événements peuvent être visualisés à l’aide du webhook lui-même ou en sélectionnant l’onglet **[!UICONTROL Suivi du débogage]** dans la présentation de l’enregistrement des événements de votre projet dans Adobe Developer Console.

Le fichier JSON suivant est un exemple de payload de notification qui serait envoyé à votre webhook en cas d’échec d’un événement d’ingestion par lots :

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
| `event` | Objet contenant les détails de l’événement qui a déclenché la notification. |
| `event.xdm:datasetId` | Identifiant du jeu de données auquel s’applique l’événement d’ingestion. |
| `event.xdm:eventCode` | Un code d’état indiquant le type d’événement déclenché pour le jeu de données. Consultez l’ [annexe](#event-codes) pour connaître les valeurs spécifiques et leurs définitions. |

Pour afficher le schéma complet des notifications d’événement, reportez-vous au [référentiel GitHub public](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Étapes suivantes

Une fois que vous avez enregistré [!DNL Platform] notifications sur votre projet, vous pouvez afficher les événements reçus de la [!UICONTROL présentation du projet]. Reportez-vous au guide sur le [suivi des événements d’Adobe I/O](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) pour obtenir des instructions détaillées sur la manière de suivre vos événements.

## Annexe

La section suivante contient des informations supplémentaires sur l’interprétation des payloads des notifications d’ingestion de données.

### Événements de notification d’état disponibles {#event-codes}

Le tableau suivant répertorie les notifications d’état d’ingestion de données disponibles auxquelles vous pouvez vous abonner.

| Code d’événement | Service Platform | État | Description des événements |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | Un lot a bien été ingéré dans un jeu de données dans [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | failure | Échec de l’ingestion d’un lot dans un jeu de données dans l’élément [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | success | Un lot a été ingéré avec succès dans l’entrepôt de données [!DNL Profile]. |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | failure | Échec de l’ingestion d’un lot dans l’entrepôt de données [!DNL Profile]. |
| `ig_load_success` | [!DNL Identity Service] | success | Les données ont bien été chargées dans le graphique d’identités. |
| `ig_load_failure` | [!DNL Identity Service] | failure | Échec du chargement des données dans le graphique d’identités. |

>[!NOTE]
>
>Une seule rubrique d’événement est fournie pour toutes les notifications d’ingestion de données. Vous pouvez utiliser le code d’événement pour faire la distinction entre les différents états.
