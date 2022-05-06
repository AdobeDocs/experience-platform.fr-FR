---
keywords: Experience Platform;api de destination;activation ad hoc;activation de segments ad hoc
solution: Experience Platform
title: (Version Beta) Activer les segments d’audience vers des destinations par lots via l’API d’activation ad hoc
description: Cet article illustre le processus de bout en bout d’activation des segments d’audience par le biais de l’API d’activation ad hoc, y compris les tâches de segmentation qui ont lieu avant l’activation.
topic-legacy: tutorial
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 20%

---

# (Version Beta) Activer les segments d’audience vers des destinations par lots via l’API d’activation ad hoc

>[!IMPORTANT]
>
>Le [!DNL ad-hoc activation API] dans Platform est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

## Présentation {#overview}

L’API d’activation ad hoc permet aux spécialistes du marketing d’activer par programmation les segments d’audience vers les destinations, de manière rapide et efficace, dans les cas où une activation immédiate est requise.

Le diagramme ci-dessous illustre le workflow de bout en bout pour l’activation des segments via l’API d’activation ad hoc, y compris les tâches de segmentation qui ont lieu dans Platform toutes les 24 heures.

![activation ad hoc](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>L’activation des audiences ad hoc n’est prise en charge que par [destinations basées sur des fichiers de lots](../destination-types.md#file-based).

## Cas dʼutilisation {#use-cases}

### Ventes ou promotions de Flash

Un détaillant en ligne prépare une vente flash limitée et souhaite informer ses clients dans un court délai. Grâce à l’API d’activation ad hoc Experience Platform, l’équipe marketing peut exporter des segments à la demande et envoyer rapidement des emails promotionnels à la base de clients.


### Événements en cours ou informations de dernière minute

Un hôtel s&#39;attend à des conditions météorologiques favorables les jours suivants et l&#39;équipe veut informer rapidement les arrivants afin qu&#39;ils puissent planifier en conséquence. L’équipe marketing peut utiliser l’API d’activation ad hoc Experience Platform pour exporter des segments à la demande et en informer les invités.

### Test d’intégration

Les responsables informatiques peuvent utiliser l’API d’activation ad hoc Experience Platform pour exporter des segments à la demande, afin qu’ils puissent tester leur intégration personnalisée avec Adobe Experience Platform et s’assurer que tout fonctionne correctement.


## Barrières de sécurité {#guardrails}

Gardez à l’esprit les barrières de sécurité suivantes lors de l’utilisation de l’API d’activation ad hoc.

* Actuellement, chaque tâche d’activation ad hoc peut activer jusqu’à 20 segments. Si vous tentez d’activer plus de 20 segments par tâche, la tâche échouera. Ce comportement peut être modifié dans les prochaines versions.
* Les tâches d’activation ad hoc ne peuvent pas s’exécuter en parallèle avec les tâches planifiées [traitements d’exportation de segments](../../segmentation/api/export-jobs.md). Avant d’exécuter une tâche d’activation ad hoc, assurez-vous que la tâche d’exportation de segments planifiée est terminée. Voir [surveillance des flux de données de destination](../../dataflows/ui/monitor-destinations.md) pour plus d’informations sur la manière de surveiller l’état des flux d’activation. Par exemple, si votre flux de données d’activation affiche une **[!UICONTROL Traitement]** , attendez qu’il se termine avant d’exécuter la tâche d’activation ad hoc.
* N’exécutez pas plusieurs tâches d’activation ad hoc simultanées par segment.

## Considérations relatives à la segmentation {#segmentation-considerations}

Adobe Experience Platform exécute des tâches de segmentation planifiées toutes les 24 heures. L’API d’activation ad hoc s’exécute en fonction des derniers résultats de segmentation.

## Étape 1 : Conditions préalables {#prerequisites}

Avant de pouvoir appeler les API Adobe Experience Platform, assurez-vous de respecter les conditions préalables suivantes :

* Vous disposez d’un compte de l’organisation IMS ayant accès à Adobe Experience Platform.
* Votre compte d’Experience Platform a la variable `developer` et `user` rôles activés pour le profil de produit de l’API Adobe Experience Platform. Contactez votre [Admin Console](../../access-control/home.md) pour activer ces rôles pour votre compte.
* Vous avez une Adobe ID. Si vous ne possédez pas d’Adobe ID, accédez à la [Adobe Developer Console](https://developer.adobe.com/console) et créez un compte.

## Étape 2 : Collecte des informations d’identification {#credentials}

Pour lancer des appels aux API Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Les ressources d’Experience Platform peuvent être isolées dans des environnements de test virtuels spécifiques. Dans les requêtes aux API Platform, vous pouvez spécifier le nom et l’identifiant de l’environnement de test dans lequel l’opération aura lieu. Il s’agit de paramètres facultatifs.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les environnements de test dans Experience Platform, consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Étape 3 : Création d’un flux d’activation dans l’interface utilisateur de Platform {#activation-flow}

Avant de pouvoir activer des segments via l’API d’activation ad hoc, vous devez d’abord configurer un flux d’activation dans l’interface utilisateur de Platform, pour la destination choisie.

Cela inclut l’accès au workflow d’activation, la sélection de vos segments, la configuration d’un planning et leur activation.

Consultez le tutoriel suivant pour obtenir des instructions détaillées sur la configuration d’un flux d’activation pour vos destinations par lots : [Activation des données d’audience vers des destinations d’exportation de profils par lots](../ui/activate-batch-profile-destinations.md).

## Étape 4 : Obtention du dernier ID de tâche d’exportation de segments {#segment-export-id}

Une fois que vous avez configuré un flux d’activation pour votre destination de lot, les tâches de segmentation planifiées commencent à s’exécuter automatiquement toutes les 24 heures.

Avant d’exécuter la tâche d’activation ad hoc, vous devez obtenir l’identifiant de la dernière tâche d’exportation de segments. Vous devez transmettre cet identifiant dans la requête de tâche d’activation ad hoc.

Suivez les instructions décrites [here](../../segmentation/api/export-jobs.md#retrieve-list) pour récupérer une liste de toutes les tâches d’exportation de segments.

Dans la réponse, recherchez le premier enregistrement contenant la propriété de schéma ci-dessous.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

L’ID de la tâche d’exportation de segments se trouve dans la variable `id` , comme illustré ci-dessous.

![identifiant de tâche d’exportation de segments](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Étape 5 : Exécution de la tâche d’activation ad hoc {#activation-job}

Adobe Experience Platform exécute des tâches de segmentation planifiées toutes les 24 heures. L’API d’activation ad hoc s’exécute en fonction des derniers résultats de segmentation.

Avant d’exécuter une tâche d’activation ad hoc, assurez-vous que la tâche d’exportation de segments planifiée pour vos segments est terminée. Voir [surveillance des flux de données de destination](../../dataflows/ui/monitor-destinations.md) pour plus d’informations sur la manière de surveiller l’état des flux d’activation. Par exemple, si votre flux de données d’activation affiche une **[!UICONTROL Traitement]** , attendez qu’il se termine avant d’exécuter la tâche d’activation ad hoc.

Une fois la tâche d’exportation de segments terminée, vous pouvez déclencher l’activation.

>[!NOTE]
>
>Actuellement, chaque tâche d’activation ad hoc peut activer jusqu’à 20 segments. Si vous tentez d’activer plus de 20 segments par tâche, la tâche échouera. Ce comportement peut être modifié dans les prochaines versions.

### Requête

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| <ul><li>`exportId1`</li></ul> | L’ID renvoyé dans la réponse de la variable [exportation de segments](../../segmentation/api/export-jobs.md#retrieve-list) tâche. Voir [Étape 4 : Obtention du dernier ID de tâche d’exportation de segments](#segment-export-id) pour obtenir des instructions sur la manière de trouver cet identifiant. |

### Réponse

Une réponse réussie renvoie un état HTTP 200.

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
| `segment` | Identifiant du segment activé. |
| `order` | Identifiant de la destination vers laquelle le segment a été activé. |
| `statusURL` | URL d’état du flux d’activation. Vous pouvez suivre la progression du flux à l’aide de la variable [API de service de flux](../../sources/tutorials/api/monitor.md). |


## Gestion des erreurs d’API

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.
