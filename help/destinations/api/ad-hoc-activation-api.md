---
keywords: Experience Platform;api de destination;activation ad hoc;activation de segments ad hoc
solution: Experience Platform
title: Activation des segments d’audience vers des destinations par lots via l’API d’activation ad hoc
description: Cet article illustre le processus de bout en bout d’activation des segments d’audience par le biais de l’API d’activation ad hoc, y compris les tâches de segmentation qui ont lieu avant l’activation.
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 18%

---

# Activation des segments d’audience à la demande vers des destinations par lots via l’API d’activation ad hoc

>[!IMPORTANT]
>
>Une fois la phase bêta terminée, la variable [!DNL ad-hoc activation API] est désormais disponible (GA) pour tous les clients Experience Platform. Dans la version GA, l’API a été mise à niveau vers la version 2. Étape 4 ([Obtention du dernier ID de tâche d’exportation de segments](#segment-export-id)) n’est plus requis, car l’API ne nécessite plus l’ID d’exportation.
>
>Voir [Exécution de la tâche d’activation ad hoc](#activation-job) plus loin dans ce tutoriel pour plus d’informations.

## Présentation {#overview}

L’API d’activation ad hoc permet aux spécialistes du marketing d’activer par programmation les segments d’audience vers les destinations, de manière rapide et efficace, dans les cas où une activation immédiate est requise.

Utilisez l’API d’activation ad hoc pour exporter des fichiers complets vers le système de réception de fichiers souhaité. L’activation des audiences ad hoc n’est prise en charge que par [destinations basées sur des fichiers de lots](../destination-types.md#file-based).

Le diagramme ci-dessous illustre le workflow de bout en bout pour l’activation des segments via l’API d’activation ad hoc, y compris les tâches de segmentation qui ont lieu dans Platform toutes les 24 heures.

![activation ad hoc](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)



## Cas d’utilisation {#use-cases}

### Ventes ou promotions de Flash

Un détaillant en ligne prépare une vente flash limitée et souhaite informer ses clients dans un court délai. Grâce à l’API d’activation ad hoc Experience Platform, l’équipe marketing peut exporter des segments à la demande et envoyer rapidement des emails promotionnels à la base de clients.

### Événements en cours ou informations de dernière minute

Un hôtel s&#39;attend à des conditions météorologiques favorables les jours suivants et l&#39;équipe veut informer rapidement les arrivants afin qu&#39;ils puissent planifier en conséquence. L’équipe marketing peut utiliser l’API d’activation ad hoc Experience Platform pour exporter des segments à la demande et en informer les invités.

### Test d’intégration

Les responsables informatiques peuvent utiliser l’API d’activation ad hoc Experience Platform pour exporter des segments à la demande, afin qu’ils puissent tester leur intégration personnalisée avec Adobe Experience Platform et s’assurer que tout fonctionne correctement.

## Barrières de sécurité {#guardrails}

Gardez à l’esprit les barrières de sécurité suivantes lors de l’utilisation de l’API d’activation ad hoc.

* Actuellement, chaque traitement d’activation ad hoc peut activer jusqu’à 80 segments. Si vous tentez d’activer plus de 80 segments par traitement, celui-ci échouera. Ce comportement peut faire l’objet de modifications dans les prochaines versions.
* Les tâches d’activation ad hoc ne peuvent pas s’exécuter en parallèle avec les tâches planifiées [traitements d’exportation de segments](../../segmentation/api/export-jobs.md). Avant d’exécuter une tâche d’activation ad hoc, assurez-vous que la tâche d’exportation de segments planifiée est terminée. Voir [surveillance des flux de données de destination](../../dataflows/ui/monitor-destinations.md) pour plus d’informations sur la manière de surveiller l’état des flux d’activation. Par exemple, si votre flux de données d’activation affiche une **[!UICONTROL Traitement]** , attendez qu’il se termine avant d’exécuter la tâche d’activation ad hoc.
* N’exécutez pas plusieurs tâches d’activation ad hoc simultanées par segment.

## Considérations relatives à la segmentation {#segmentation-considerations}

Adobe Experience Platform exécute des tâches de segmentation planifiées toutes les 24 heures. L’API d’activation ad hoc s’exécute en fonction des derniers résultats de segmentation.

## Étape 1 : Conditions préalables {#prerequisites}

Avant de pouvoir appeler les API Adobe Experience Platform, assurez-vous de respecter les conditions préalables suivantes :

* Vous disposez d’un compte de l’organisation IMS ayant accès à Adobe Experience Platform.
* Votre compte d’Experience Platform a la variable `developer` et `user` rôles activés pour le profil de produit de l’API Adobe Experience Platform. Contactez votre [Admin Console](../../access-control/home.md) pour activer ces rôles pour votre compte.
* Vous avez une Adobe ID. Si vous ne possédez pas d’Adobe ID, accédez à la [Console Adobe Developer](https://developer.adobe.com/console) et créez un compte.

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

Cela inclut l’accès au workflow d’activation, la sélection de vos segments, la configuration d’un planning et leur activation. Vous pouvez utiliser l’interface utilisateur ou l’API pour créer un flux d’activation :

* [Utilisation de l’interface utilisateur de Platform pour créer un flux d’activation pour les destinations d’exportation de profils par lots](../ui/activate-batch-profile-destinations.md)
* [Utilisation de l’API Flow Service pour se connecter aux destinations d’exportation de profils par lots et activer les données](../api/connect-activate-batch-destinations.md)

## Étape 4 : Obtention du dernier ID de tâche d’exportation de segment (non requis dans la version v2) {#segment-export-id}

>[!IMPORTANT]
>
>Dans la version v2 de l’API d’activation ad hoc, vous n’avez pas besoin d’obtenir le dernier ID de tâche d’exportation de segment. Vous pouvez ignorer cette étape et passer à la suivante.

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

>[!IMPORTANT]
>
>Notez la contrainte ponctuelle suivante : Avant d’exécuter une tâche d’activation ad hoc, assurez-vous qu’au moins 20 minutes se sont écoulées entre le moment où le segment a été activé pour la première fois, selon le planning défini dans [Étape 3 - Création du flux d’activation dans l’interface utilisateur de Platform](#activation-flow).

Avant d’exécuter une tâche d’activation ad hoc, assurez-vous que la tâche d’exportation de segments planifiée pour vos segments est terminée. Voir [surveillance des flux de données de destination](../../dataflows/ui/monitor-destinations.md) pour plus d’informations sur la manière de surveiller l’état des flux d’activation. Par exemple, si votre flux de données d’activation affiche une **[!UICONTROL Traitement]** , attendez qu’il se termine avant d’exécuter la tâche d’activation ad hoc pour exporter un fichier complet.

Une fois la tâche d’exportation de segments terminée, vous pouvez déclencher l’activation.

>[!NOTE]
>
>Actuellement, chaque traitement d’activation ad hoc peut activer jusqu’à 80 segments. Si vous tentez d’activer plus de 80 segments par traitement, celui-ci échouera. Ce comportement peut faire l’objet de modifications dans les prochaines versions.

### Requête {#request}

>[!IMPORTANT]
>
>Il est obligatoire d’inclure la variable `Accept: application/vnd.adobe.adhoc.activation+json; version=2` en-tête de votre requête afin d’utiliser la version v2 de l’API d’activation ad hoc.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun' \
--header 'x-gw-ims-org-id: 5555467B5D8013E50A494220@AdobeOrg' \
--header 'Authorization: Bearer {{token}}' \
--header 'x-sandbox-id: 6ef74723-3ee7-46a4-b747-233ee7a6a41a' \
--header 'x-sandbox-name: {sandbox-id}' \
--header 'Accept: application/vnd.adobe.adhoc.activation+json; version=2' \
--header 'Content-Type: application/json' \
--data-raw '{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   }
}'
```

| Propriété | Description |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Les identifiants des instances de destination vers lesquelles vous souhaitez activer les segments. Vous pouvez obtenir ces ID à partir de l’interface utilisateur de Platform en accédant à **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** et cliquez sur la ligne de destination souhaitée pour afficher l’ID de destination dans le rail de droite. Pour plus d’informations, reportez-vous à la section [documentation de l’espace de travail des destinations](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Les identifiants des segments que vous souhaitez activer vers la destination sélectionnée. |

{style=&quot;table-layout:auto&quot;}

### Requête avec des identifiants d’exportation (à abandonner) {#request-deprecated}

>[!IMPORTANT]
>
>**Type de requête obsolète**. Cet exemple décrit le type de requête pour l’API version 1. Dans la version v2 de l’API d’activation ad hoc, vous n’avez pas besoin d’inclure le dernier ID de tâche d’exportation de segment.

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Les identifiants des instances de destination vers lesquelles vous souhaitez activer les segments. Vous pouvez obtenir ces ID à partir de l’interface utilisateur de Platform en accédant à **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** et cliquez sur la ligne de destination souhaitée pour afficher l’ID de destination dans le rail de droite. Pour plus d’informations, reportez-vous à la section [documentation de l’espace de travail des destinations](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Les identifiants des segments que vous souhaitez activer vers la destination sélectionnée. |
| <ul><li>`exportId1`</li></ul> | L’ID renvoyé dans la réponse de la variable [exportation de segments](../../segmentation/api/export-jobs.md#retrieve-list) tâche. Voir [Étape 4 : Obtention du dernier ID de tâche d’exportation de segments](#segment-export-id) pour obtenir des instructions sur la manière de trouver cet identifiant. |

{style=&quot;table-layout:auto&quot;}

### Réponse {#response}

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

{style=&quot;table-layout:auto&quot;}

## Gestion des erreurs d’API {#api-error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

### Codes d’erreur et messages d’API spécifiques à l’API d’activation ad hoc {#specific-error-messages}

Lors de l’utilisation de l’API d’activation ad hoc, vous pouvez rencontrer des messages d’erreur spécifiques à ce point de terminaison API. Consultez le tableau pour savoir comment y remédier lorsqu’il s’affiche.

| Message d’erreur | Résolution |
|---------|----------|
| Exécution déjà en cours pour le segment `segment ID` pour la commande `dataflow ID` avec identifiant d’exécution `flow run ID` | Ce message d’erreur indique qu’un flux d’activation ad hoc est actuellement en cours pour un segment. Attendez que la tâche se termine avant de déclencher à nouveau la tâche d’activation. |
| Segments `<segment name>` ne font pas partie de ce flux de données ou ne font pas partie de la plage de dates prévue. | Ce message d’erreur indique que les segments que vous avez sélectionnés pour activer ne sont pas mappés au flux de données ou que le planning d’activation configuré pour les segments a expiré ou n’a pas encore commencé. Vérifiez si le segment est bien mappé sur le flux de données et que le planning d’activation du segment chevauche la date actuelle. |

## Informations connexes {#related-information}

* [Se connecter aux destinations par lots et activer des données à l’aide de l’API Flow Service](/help/destinations/api/connect-activate-batch-destinations.md)
* [(Version bêta) Exporter des fichiers à la demande vers des destinations par lots à l’aide de l’interface utilisateur Experience Platform](/help/destinations/ui/export-file-now.md)