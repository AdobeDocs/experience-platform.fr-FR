---
keywords: Experience Platform;api de destination;activation ad hoc;activation d’audiences ad hoc
solution: Experience Platform
title: Activation des audiences vers des destinations par lot via l’API d’activation ad hoc
description: Cet article illustre le processus de bout en bout d’activation des audiences via l’API d’activation ad hoc, y compris les tâches de segmentation qui ont lieu avant l’activation.
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: deecaf0af269b64af507126dba0523d2b16a5721
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 12%

---

# Activation des audiences à la demande vers des destinations par lots via l’API d’activation ad hoc

>[!IMPORTANT]
>
>Une fois la phase Beta terminée, le [!DNL ad-hoc activation API] est désormais disponible (GA) pour tous les clients Experience Platform. Dans la version GA, l’API a été mise à niveau vers la version 2. L’étape 4 ([Obtenir le dernier ID de tâche d’exportation d’audience](#segment-export-id)) n’est plus requise, car l’API ne nécessite plus l’ID d’exportation.
>
>Pour plus d’informations, reportez-vous à la section [Exécution de la tâche d’activation ad hoc](#activation-job) ci-dessous dans ce tutoriel.

## Vue d’ensemble {#overview}

L’API d’activation ad hoc permet aux marketeurs d’activer par programmation les audiences d’audience vers les destinations, de manière rapide et efficace, dans les cas où une activation immédiate est requise.

Utilisez l’API d’activation ad hoc pour exporter des fichiers complets vers le système de réception de fichiers souhaité. L’activation des audiences ad hoc est uniquement prise en charge par les [destinations basées sur des fichiers de lot](../destination-types.md#file-based).

Le diagramme ci-dessous illustre le workflow de bout en bout pour activer les audiences via l’API d’activation ad hoc, y compris les tâches de segmentation qui ont lieu dans Platform toutes les 24 heures.

![ad-hoc-activation](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)



## Cas d’utilisation {#use-cases}

### Ventes ou promotions de Flash

Un détaillant en ligne prépare une vente flash limitée et souhaite informer ses clients dans un court délai. Grâce à l’API d’activation ad hoc Experience Platform, l’équipe marketing peut exporter des audiences à la demande et envoyer rapidement des emails promotionnels à la base de clients.

### Événements en cours ou informations de dernière minute

Un hôtel s&#39;attend à des conditions météorologiques favorables les jours suivants et l&#39;équipe veut informer rapidement les arrivants afin qu&#39;ils puissent planifier en conséquence. L’équipe marketing peut utiliser l’API d’activation ad hoc Experience Platform pour exporter des audiences à la demande et en informer les invités.

### Test d’intégration

Les responsables informatiques peuvent utiliser l’API d’activation ad hoc Experience Platform pour exporter des audiences à la demande, afin qu’ils puissent tester leur intégration personnalisée avec Adobe Experience Platform et s’assurer que tout fonctionne correctement.

## Mécanismes de sécurisation {#guardrails}

Gardez à l’esprit les barrières de sécurité suivantes lors de l’utilisation de l’API d’activation ad hoc.

* Actuellement, chaque tâche d’activation ad hoc peut activer jusqu’à 80 audiences. Si vous tentez d’activer plus de 80 audiences par tâche, la tâche échouera. Ce comportement peut faire l’objet de modifications dans les prochaines versions.
* Les tâches d’activation ad hoc ne peuvent pas s’exécuter en parallèle avec les [tâches d’exportation d’audiences](../../segmentation/api/export-jobs.md) planifiées. Avant d’exécuter une tâche d’activation ad hoc, assurez-vous que la tâche d’exportation d’audience planifiée est terminée. Pour plus d’informations sur la surveillance de l’état des flux d’activation, voir [surveillance des flux de données de destination](../../dataflows/ui/monitor-destinations.md) . Par exemple, si votre flux de données d’activation affiche l’état **[!UICONTROL Traitement]**, attendez qu’il se termine avant d’exécuter la tâche d’activation ad hoc.
* N’exécutez pas plusieurs tâches d’activation ad hoc simultanées par audience.

## Considérations relatives à la segmentation {#segmentation-considerations}

Adobe Experience Platform exécute des tâches de segmentation planifiées toutes les 24 heures. L’API d’activation ad hoc s’exécute en fonction des derniers résultats de segmentation.

## Etape 1 : Conditions préalables {#prerequisites}

Avant de pouvoir appeler les API Adobe Experience Platform, assurez-vous de respecter les conditions préalables suivantes :

* Vous disposez d’un compte d’organisation ayant accès à Adobe Experience Platform.
* Les rôles `developer` et `user` sont activés pour votre compte d’Experience Platform pour le profil de produit de l’API Adobe Experience Platform. Contactez votre administrateur [Admin Console](../../access-control/home.md) pour activer ces rôles pour votre compte.
* Vous avez une Adobe ID. Si vous ne possédez pas d’Adobe ID, accédez à [Adobe Developer Console](https://developer.adobe.com/console) et créez un compte.

## Étape 2 : collecte des informations d’identification {#credentials}

Pour lancer des appels aux API Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Les ressources d’Experience Platform peuvent être isolées dans des sandbox virtuels spécifiques. Dans les requêtes aux API Platform, vous pouvez spécifier le nom et l’identifiant du sandbox dans lequel l’opération aura lieu. Il s’agit de paramètres facultatifs.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans Experience Platform, consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Étape 3 : création d’un flux d’activation dans l’interface utilisateur de Platform {#activation-flow}

Avant de pouvoir activer des audiences via l’API d’activation ad hoc, vous devez d’abord configurer un flux d’activation dans l’interface utilisateur de Platform, pour la destination choisie.

Cela inclut l’accès au workflow d’activation, la sélection de vos audiences, la configuration d’un planning et leur activation. Vous pouvez utiliser l’interface utilisateur ou l’API pour créer un flux d’activation :

* [Utilisation de l’interface utilisateur de Platform pour créer un flux d’activation pour les destinations d’exportation de profils par lots](../ui/activate-batch-profile-destinations.md)
* [Utilisation de l’API Flow Service pour se connecter aux destinations d’exportation de profils par lots et activer les données](../api/connect-activate-batch-destinations.md)

## Étape 4 : Obtention du dernier ID de tâche d’exportation d’audience (non requis dans la version v2) {#segment-export-id}

>[!IMPORTANT]
>
>Dans la version v2 de l’API d’activation ad hoc, vous n’avez pas besoin d’obtenir le dernier ID de tâche d’exportation d’audience. Vous pouvez ignorer cette étape et passer à la suivante.

Une fois que vous avez configuré un flux d’activation pour votre destination de lot, les tâches de segmentation planifiées commencent à s’exécuter automatiquement toutes les 24 heures.

Avant de pouvoir exécuter la tâche d’activation ad hoc, vous devez obtenir l’identifiant de la dernière tâche d’exportation d’audience. Vous devez transmettre cet identifiant dans la requête de tâche d’activation ad hoc.

Suivez les instructions décrites [ici](../../segmentation/api/export-jobs.md#retrieve-list) pour récupérer une liste de toutes les tâches d’exportation d’audience.

Dans la réponse, recherchez le premier enregistrement contenant la propriété de schéma ci-dessous.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

L’ID de la tâche d’exportation d’audience se trouve dans la propriété `id`, comme illustré ci-dessous.

![ID de la tâche d’exportation d’audience](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Étape 5 : exécution de la tâche d’activation ad hoc {#activation-job}

Adobe Experience Platform exécute des tâches de segmentation planifiées toutes les 24 heures. L’API d’activation ad hoc s’exécute en fonction des derniers résultats de segmentation.

>[!IMPORTANT]
>
>Notez la contrainte ponctuelle suivante : avant d’exécuter une tâche d’activation ad hoc, assurez-vous qu’au moins 20 minutes se sont écoulées entre le moment où l’audience a été activée pour la première fois selon le planning que vous avez défini dans [Étape 3 - Créer un flux d’activation dans l’interface utilisateur de Platform](#activation-flow).

Avant d’exécuter une tâche d’activation ad hoc, assurez-vous que la tâche d’exportation d’audience planifiée pour vos audiences est terminée. Pour plus d’informations sur la surveillance de l’état des flux d’activation, voir [surveillance des flux de données de destination](../../dataflows/ui/monitor-destinations.md) . Par exemple, si votre flux de données d’activation affiche l’état **[!UICONTROL Traitement]**, attendez qu’il se termine avant d’exécuter la tâche d’activation ad hoc pour exporter un fichier complet.

Une fois la tâche d&#39;export d&#39;audience terminée, vous pouvez déclencher l&#39;activation.

>[!NOTE]
>
>Actuellement, chaque tâche d’activation ad hoc peut activer jusqu’à 80 audiences. Si vous tentez d’activer plus de 80 audiences par tâche, la tâche échouera. Ce comportement peut faire l’objet de modifications dans les prochaines versions.

### Requête {#request}

>[!IMPORTANT]
>
>Il est obligatoire d’inclure l’en-tête `Accept: application/vnd.adobe.adhoc.activation+json; version=2` dans votre requête afin d’utiliser la version v2 de l’API d’activation ad hoc.

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Les identifiants des instances de destination vers lesquelles vous souhaitez activer les audiences. Vous pouvez obtenir ces ID à partir de l’interface utilisateur de Platform, en accédant à l’onglet **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** et en cliquant sur la ligne de destination de votre choix pour afficher l’ID de destination dans le rail de droite. Pour plus d’informations, consultez la [documentation de l’espace de travail des destinations](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Les identifiants des audiences que vous souhaitez activer vers la destination sélectionnée. Vous pouvez utiliser l’API ad hoc pour exporter des audiences générées par Platform ainsi que des audiences externes (téléchargement personnalisé). Lors de l’activation d’audiences externes, utilisez l’identifiant généré par le système au lieu de l’identifiant d’audience. Vous pouvez trouver l&#39;identifiant généré par le système dans la vue de synthèse de l&#39;audience dans l&#39;interface utilisateur des audiences. <br> ![Affichage de l’ID d’audience qui ne doit pas être sélectionné.](/help/destinations/assets/api/ad-hoc-activation/audience-id-do-not-use.png "Affichage de l’ID d’audience qui ne doit pas être sélectionné."){width="100" zoomable="yes"} <br> ![Affichage de l’ID d’audience généré par le système qui doit être utilisé.](/help/destinations/assets/api/ad-hoc-activation/system-generated-id-to-use.png "Affichage de l’ID d’audience généré par le système qui doit être utilisé."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

### Requête avec des ID d’exportation {#request-export-ids}

<!--

>[!IMPORTANT]
>
>**Deprecated request type**. This example type describes the request type for the API version 1. In the v2 of the ad-hoc activation API, you do not need to include the latest audience export job ID.

-->

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Les identifiants des instances de destination vers lesquelles vous souhaitez activer les audiences. Vous pouvez obtenir ces ID à partir de l’interface utilisateur de Platform, en accédant à l’onglet **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]** et en cliquant sur la ligne de destination de votre choix pour afficher l’ID de destination dans le rail de droite. Pour plus d’informations, consultez la [documentation de l’espace de travail des destinations](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Les identifiants des audiences que vous souhaitez activer vers la destination sélectionnée. |
| <ul><li>`exportId1`</li></ul> | L’ID renvoyé dans la réponse de la tâche [export d’audience](../../segmentation/api/export-jobs.md#retrieve-list). Voir [Étape 4 : obtenir le dernier ID de tâche d’exportation d’audience](#segment-export-id) pour obtenir des instructions sur la manière de trouver cet ID. |

{style="table-layout:auto"}

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
| `segment` | Identifiant de l’audience activée. |
| `order` | Identifiant de la destination vers laquelle l’audience a été activée. |
| `statusURL` | URL d’état du flux d’activation. Vous pouvez suivre la progression du flux à l’aide de l’ [ API Flow Service](../../sources/tutorials/api/monitor.md). |

{style="table-layout:auto"}

## Gestion des erreurs d’API {#api-error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

### Codes d’erreur et messages d’API spécifiques à l’API d’activation ad hoc {#specific-error-messages}

Lors de l’utilisation de l’API d’activation ad hoc, vous pouvez rencontrer des messages d’erreur spécifiques à ce point de terminaison API. Consultez le tableau pour savoir comment y remédier lorsqu’il s’affiche.

| Message d’erreur | Résolution |
|---------|----------|
| Exécutez déjà pour l&#39;audience `segment ID` de la commande `dataflow ID` avec l&#39;identifiant d&#39;exécution `flow run ID` | Ce message d’erreur indique qu’un flux d’activation ad hoc est actuellement en cours pour une audience. Attendez que la tâche se termine avant de déclencher à nouveau la tâche d’activation. |
| Les segments `<segment name>` ne font pas partie de ce flux de données ou ne font pas partie de la plage de planification ! | Ce message d’erreur indique que les audiences que vous avez sélectionnées pour activer ne sont pas mappées au flux de données ou que le planning d’activation configuré pour les audiences a expiré ou n’a pas encore commencé. Vérifiez si l’audience est bien mappée au flux de données et que le planning d’activation de l’audience chevauche la date actuelle. |

## Informations connexes {#related-information}

* [Se connecter aux destinations par lots et activer des données à l’aide de l’API Flow Service](/help/destinations/api/connect-activate-batch-destinations.md)
* [(Version bêta) Exporter des fichiers à la demande vers des destinations par lots à l’aide de l’interface utilisateur Experience Platform](/help/destinations/ui/export-file-now.md)