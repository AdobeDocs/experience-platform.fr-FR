---
keywords: Experience Platform;api de destination;activation ad hoc;activation de segments ad hoc
solution: Experience Platform
title: (Beta) Activate audience segments to batch destinations via the ad-hoc activation API
description: This article illustrates the end-to-end workflow for activating audience segments via the ad-hoc activation API, including the segmentation jobs that take place before activation.
topic-legacy: tutorial
type: Tutorial
source-git-commit: 749fa5dc1e8291382408d9b1a0391c4c7f2b2a46
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 12%

---


# (Version bêta) Activation des segments d’audience vers des destinations par lots via l’API d’activation ad hoc

>[!IMPORTANT]
>
>Le [!DNL ad-hoc activation API] dans Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

## Présentation {#overview}

The ad-hoc activation API allows marketers to programmatically activate audience segments to destinations, in a fast and efficient manner, for situations where immediate activation is required.

The diagram below illustrates the end-to-end workflow for activating segments via the ad-hoc activation API, including the segmentation jobs that take place in Platform every 24 hours.

![activation ad hoc](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>Ad-hoc audience activation is only supported by [batch file-based destinations](../destination-types.md#file-based).

## Cas d’utilisation {#use-cases}

### Flash sales or promotions

An online retailer is preparing a limited flash sale and wants to notify customers on a short notice. Grâce à l’API d’activation ad hoc Experience Platform, l’équipe marketing peut exporter des segments à la demande et envoyer rapidement des emails promotionnels à la base de clients.


### Événements en cours ou informations de dernière minute

Un hôtel s&#39;attend à des conditions météorologiques favorables les jours suivants et l&#39;équipe veut informer rapidement les arrivants afin qu&#39;ils puissent planifier en conséquence. L’équipe marketing peut utiliser l’API d’activation ad hoc Experience Platform pour exporter des segments à la demande et en informer les invités.

### Test d’intégration

IT managers can use the Experience Platform ad-hoc activation API to export segments on-demand, so they can test their custom integration with Adobe Experience Platform, and ensure everything is working correctly.


## Barrières de sécurité {#guardrails}

Gardez à l’esprit les barrières de sécurité suivantes lors de l’utilisation de l’API d’activation ad hoc.

* Actuellement, chaque tâche d’activation ad hoc peut activer jusqu’à 20 segments. Si vous tentez d’activer plus de 20 segments par tâche, la tâche échouera. This behavior is subject to change in future releases.
* Ad-hoc activation jobs cannot run in parallel with scheduled [segment export jobs](../../segmentation/api/export-jobs.md). Before running an ad-hoc activation job, make sure the scheduled segment export job has finished. See [destination dataflow monitoring](../../dataflows/ui/monitor-destinations.md) for information on how to monitor the status of activation flows. Par exemple, si votre flux de données d’activation affiche une **[!UICONTROL Traitement]** , attendez qu’il se termine avant d’exécuter la tâche d’activation ad hoc.
* N’exécutez pas plusieurs tâches d’activation ad hoc simultanées par segment.

## Segmentation considerations {#segmentation-considerations}

Adobe Experience Platform exécute des tâches de segmentation planifiées toutes les 24 heures. The ad-hoc activation API runs based on the latest segmentation results.

## Étape 1 : Conditions préalables {#prerequisites}

Avant de pouvoir appeler les API Adobe Experience Platform, assurez-vous de respecter les conditions préalables suivantes :

* Vous disposez d’un compte de l’organisation IMS ayant accès à Adobe Experience Platform.
* Votre compte d’Experience Platform a la variable `developer` et `user` rôles activés pour le profil de produit de l’API Adobe Experience Platform. Contactez votre [Admin Console](../../access-control/home.md) pour activer ces rôles pour votre compte.
* Vous avez une Adobe ID. Si vous ne possédez pas d’Adobe ID, accédez à la [Adobe Developer Console](https://developer.adobe.com/console) et créez un compte.

## Step 2: Gather credentials {#credentials}

Pour lancer des appels aux API Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Les ressources d’Experience Platform peuvent être isolées dans des environnements de test virtuels spécifiques. Dans les requêtes aux API Platform, vous pouvez spécifier le nom et l’identifiant de l’environnement de test dans lequel l’opération aura lieu. Il s’agit de paramètres facultatifs.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les environnements de test dans Experience Platform, consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Étape 3 : Création d’un flux d’activation dans l’interface utilisateur de Platform {#activation-flow}

Avant de pouvoir activer des segments via l’API d’activation ad hoc, vous devez d’abord configurer un flux d’activation dans l’interface utilisateur de Platform, pour la destination choisie.

Cela inclut l’accès au workflow d’activation, la sélection de vos segments, la configuration d’un planning et leur activation.

Consultez le tutoriel suivant pour obtenir des instructions détaillées sur la configuration d’un flux d’activation pour vos destinations par lots : [Activation des données d’audience vers des destinations d’exportation de profils par lots](../ui/activate-batch-profile-destinations.md).

## Step 4: Obtain the latest segment export job ID {#segment-export-id}

After you configure an activation flow for your batch destination, scheduled segmentation jobs start running automatically every 24 hours.

Avant d’exécuter la tâche d’activation ad hoc, vous devez obtenir l’identifiant de la dernière tâche d’exportation de segments. Vous devez transmettre cet identifiant dans la requête de tâche d’activation ad hoc.

Follow the instructions described [here](../../segmentation/api/export-jobs.md#retrieve-list) to retrieve a list of all the segment export jobs.

Dans la réponse, recherchez le premier enregistrement contenant la propriété de schéma ci-dessous.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

The segment export job ID is in the `id` property, as shown below.

![segment export job ID](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Step 5: Run the ad-hoc activation job {#activation-job}

Adobe Experience Platform exécute des tâches de segmentation planifiées toutes les 24 heures. L’API d’activation ad hoc s’exécute en fonction des derniers résultats de segmentation.

Before running an ad-hoc activation job, make sure the scheduled segment export job for your segments has finished. Voir [surveillance des flux de données de destination](../../dataflows/ui/monitor-destinations.md) pour plus d’informations sur la manière de surveiller l’état des flux d’activation. Par exemple, si votre flux de données d’activation affiche une **[!UICONTROL Traitement]** , attendez qu’il se termine avant d’exécuter la tâche d’activation ad hoc.

Une fois la tâche d’exportation de segments terminée, vous pouvez déclencher l’activation.

>[!NOTE]
>
>Actuellement, chaque tâche d’activation ad hoc peut activer jusqu’à 20 segments. Si vous tentez d’activer plus de 20 segments par tâche, la tâche échouera. Ce comportement peut être modifié dans les prochaines versions.

### Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -d '
{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   },
   "exportIds":[
      "exportId1"
   ]
}
```

| Propriété | Description |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Les identifiants des instances de destination vers lesquelles vous souhaitez activer les segments. |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Les identifiants des segments que vous souhaitez activer vers la destination sélectionnée. |
| <ul><li>`exportId1`</li></ul> | The ID returned in the response of the [segment export](../../segmentation/api/export-jobs.md#retrieve-list) job. Voir [Étape 4 : Obtention du dernier ID de tâche d’exportation de segments](#segment-export-id) pour obtenir des instructions sur la manière de trouver cet identifiant. |

### Réponse

A successful response returns HTTP status 200.

```shell
{
   "order":[
      {
         "segment":"db8961e9-d52f-45bc-b3fb-76d0382a6851",
         "order":"ef2dcbd6-36fc-49a3-afed-d7b8e8f724eb",
         "statusURL":"https://platform.adobe.io/data/foundation/flowservice/runs/88d6da63-dc97-460e-b781-fc795a7386d9"
      }
   ]
}
```

| Propriété | Description |
| -------- | ----------- |
| `segment` | The ID of the activated segment. |
| `order` | Identifiant de la destination vers laquelle le segment a été activé. |
| `statusURL` | The status URL of the activation flow. Vous pouvez suivre la progression du flux à l’aide de la variable [API de service de flux](../../sources/tutorials/api/monitor.md). |


## Gestion des erreurs d’API

Les points d’entrée de l’API du SDK de destination suivent les principes généraux des messages d’erreur de l’API Experience Platform. Voir [Codes d’état d’API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) et [erreurs d’en-tête de requête](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) dans le guide de dépannage de Platform.
