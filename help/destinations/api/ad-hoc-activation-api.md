---
keywords: Experience Platform;api de destination;activation ad hoc;activer des audiences ad hoc
solution: Experience Platform
title: Activer des audiences vers des destinations par lots via l’API d’activation ad hoc
description: Cet article illustre le workflow de bout en bout pour activer des audiences via l’API d’activation ad hoc, y compris les tâches de segmentation qui ont lieu avant l’activation.
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: f01a044d3d12ef457c6242a0b93acbfeeaf48588
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 12%

---

# Activer les audiences à la demande vers des destinations par lots via l’API d’activation ad hoc

>[!IMPORTANT]
>
>Une fois la phase Beta terminée, la [!DNL ad-hoc activation API] est désormais disponible pour tous les clients Experience Platform. Dans la version mise à disposition générale, l’API a été mise à niveau vers la version 2. L’étape 4 ([Obtention du dernier identifiant de tâche d’exportation d’audience](#segment-export-id)) n’est plus nécessaire, car l’API ne nécessite plus l’identifiant d’exportation.
>
>Pour plus d’informations](#activation-job) consultez la section [Exécution de la tâche d’activation ad hoc plus bas dans ce tutoriel.

## Vue d’ensemble {#overview}

L’API d’activation ad hoc permet aux spécialistes marketing d’activer par programmation les audiences vers les destinations, de manière rapide et efficace, dans les cas où une activation immédiate est requise.

Utilisez l’API d’activation ad hoc pour exporter des fichiers complets vers le système de réception de fichiers de votre choix. L’activation des audiences ad hoc n’est prise en charge que par les [destinations basées sur des fichiers par lots](../destination-types.md#file-based).

Le diagramme ci-dessous illustre le workflow de bout en bout pour activer des audiences via l’API d’activation ad hoc, y compris les tâches de segmentation qui ont lieu dans Platform toutes les 24 heures.

![ad hoc-activation](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

## Cas d’utilisation {#use-cases}

### Ventes ou promotions Flash

Un retailer en ligne prépare une vente flash limitée et souhaite avertir les clients dans un court délai. Grâce à l’API d’activation ad hoc d’Experience Platform, l’équipe marketing peut exporter des audiences à la demande et envoyer rapidement des e-mails promotionnels à la base de clients.

### Événements actuels ou dernières nouvelles

Un hôtel s&#39;attend à un mauvais temps les jours suivants, et l&#39;équipe souhaite informer rapidement les clients afin qu&#39;ils puissent se préparer en conséquence. L’équipe marketing peut utiliser l’API d’activation ad hoc d’Experience Platform pour exporter des audiences à la demande et informer les invités.

### Test de l’intégration

Les responsables informatiques peuvent utiliser l’API d’activation ad hoc d’Experience Platform pour exporter des audiences à la demande, afin de pouvoir tester leur intégration personnalisée à Adobe Experience Platform et s’assurer que tout fonctionne correctement.

## Mécanismes de sécurisation {#guardrails}

Gardez à l’esprit les mécanismes de sécurisation suivants lors de l’utilisation de l’API d’activation ad hoc .

* Actuellement, chaque traitement d’activation ad hoc peut activer jusqu’à 80 audiences. Si vous tentez d’activer plus de 80 audiences par traitement, celui-ci échouera. Ce comportement peut faire l’objet de modifications dans les prochaines versions.
* Les traitements d’activation ad hoc ne peuvent pas s’exécuter en parallèle avec les traitements d’exportation d’audiences [ planifiés](../../segmentation/api/export-jobs.md). Avant d’exécuter une tâche d’activation ad hoc, assurez-vous que la tâche d’exportation de l’audience planifiée est terminée. Consultez [surveillance des flux de données de destination](../../dataflows/ui/monitor-destinations.md) pour plus d’informations sur la surveillance du statut des flux d’activation. Par exemple, si votre flux de données d’activation affiche un statut **[!UICONTROL Traitement]**, attendez qu’il se termine avant d’exécuter la tâche d’activation ad hoc.
* N’exécutez pas plusieurs traitements d’activation ad hoc simultanés par audience.

## Considérations relatives à la segmentation {#segmentation-considerations}

Adobe Experience Platform exécute des tâches de segmentation planifiées une fois toutes les 24 heures. L’API d’activation ad hoc s’exécute en fonction des derniers résultats de segmentation.

## Etape 1 : prérequis {#prerequisites}

Avant d’effectuer des appels vers les API Adobe Experience Platform, veillez à respecter les conditions préalables suivantes :

* Vous disposez d’un compte d’organisation avec un accès à Adobe Experience Platform.
* Les rôles `developer` et `user` sont activés pour le profil de produit API Adobe Experience Platform de votre compte Experience Platform. Contactez votre administrateur [Admin Console](../../access-control/home.md) pour activer ces rôles pour votre compte.
* Vous disposez d’une Adobe ID. Si vous ne disposez pas d’un Adobe ID, accédez au [Adobe Developer Console](https://developer.adobe.com/console) et créez un compte.

## Étape 2 : collecter les informations d’identification {#credentials}

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

## Étape 3 : créer un flux d’activation dans l’interface utilisateur de Platform {#activation-flow}

Avant de pouvoir activer des audiences par le biais de l’API d’activation ad hoc, vous devez d’abord configurer un flux d’activation dans l’interface utilisateur de Platform, pour la destination choisie.

Cela inclut l’entrée dans le workflow d’activation, la sélection de vos audiences, la configuration d’un planning et leur activation. Vous pouvez utiliser l’interface utilisateur ou l’API pour créer un flux d’activation :

* [Utilisez l’interface utilisateur de Platform pour créer un flux d’activation vers des destinations d’exportation de profils par lots](../ui/activate-batch-profile-destinations.md)
* [Utilisez l’API Flow Service pour vous connecter aux destinations d’exportation de profils par lots et activer les données](../api/connect-activate-batch-destinations.md)

## Étape 4 : obtenir le dernier identifiant de tâche d&#39;exportation d&#39;audience (non requis dans v2) {#segment-export-id}

>[!IMPORTANT]
>
>Dans la version v2 de l’API d’activation ad hoc, vous n’avez pas besoin d’obtenir le dernier identifiant de tâche d’exportation d’audience. Vous pouvez ignorer cette étape et passer à l’étape suivante.

Une fois que vous avez configuré un flux d’activation pour la destination par lots, les tâches de segmentation planifiées commencent à s’exécuter automatiquement toutes les 24 heures.

Avant de pouvoir exécuter la tâche d’activation ad hoc, vous devez obtenir l’identifiant de la dernière tâche d’exportation d’audience. Vous devez transmettre cet identifiant dans la demande de traitement d’activation ad hoc.

Suivez les instructions décrites [ici](../../segmentation/api/export-jobs.md#retrieve-list) pour récupérer une liste de toutes les tâches d’exportation d’audience.

Dans la réponse, recherchez le premier enregistrement qui inclut la propriété de schéma ci-dessous.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

L’identifiant de la tâche d’exportation d’audience se trouve dans la propriété `id` , comme illustré ci-dessous.

![ID de tâche d’exportation d’audience](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Étape 5 : exécuter la tâche d’activation ad hoc {#activation-job}

Adobe Experience Platform exécute des tâches de segmentation planifiées une fois toutes les 24 heures. L’API d’activation ad hoc s’exécute en fonction des derniers résultats de segmentation.

>[!IMPORTANT]
>
>Notez la contrainte unique suivante : avant d’exécuter une tâche d’activation ad hoc, assurez-vous qu’au moins une heure s’est écoulée depuis le moment où l’audience a été activée pour la première fois, conformément au planning que vous avez défini à l’[Étape 3 - Créer un flux d’activation dans l’interface utilisateur de Platform](#activation-flow).

Avant d’exécuter une tâche d’activation ad hoc, assurez-vous que la tâche d’exportation d’audience planifiée pour vos audiences est terminée. Consultez [surveillance des flux de données de destination](../../dataflows/ui/monitor-destinations.md) pour plus d’informations sur la surveillance du statut des flux d’activation. Par exemple, si votre flux de données d’activation affiche un statut **[!UICONTROL Traitement]**, attendez qu’il soit terminé avant d’exécuter la tâche d’activation ad hoc pour exporter un fichier complet.

Une fois la tâche d’exportation d’audience terminée, vous pouvez déclencher l’activation.

>[!NOTE]
>
>Actuellement, chaque traitement d’activation ad hoc peut activer jusqu’à 80 audiences. Si vous tentez d’activer plus de 80 audiences par traitement, celui-ci échouera. Ce comportement peut faire l’objet de modifications dans les prochaines versions.

### Requête {#request}

>[!IMPORTANT]
>
>Il est obligatoire d’inclure l’en-tête `Accept: application/vnd.adobe.adhoc.activation+json; version=2` dans votre requête pour utiliser la version v2 de l’API d’activation ad hoc.

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Identifiants des instances de destination vers lesquelles vous souhaitez activer des audiences. Vous pouvez obtenir ces identifiants à partir de l’interface utilisateur de Platform en accédant à l’onglet **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]**, puis en cliquant sur la ligne de destination souhaitée pour afficher l’identifiant de destination dans le rail de droite. Pour plus d’informations, consultez la [documentation de l’espace de travail des destinations](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Identifiants des audiences que vous souhaitez activer vers la destination sélectionnée. Vous pouvez utiliser l’API ad hoc pour exporter des audiences générées par Platform ainsi que des audiences externes (chargement personnalisé). Lors de l’activation d’audiences externes, utilisez l’identifiant généré par le système plutôt que l’identifiant d’audience. L’identifiant généré par le système est disponible dans la vue de résumé de l’audience dans l’interface utilisateur des audiences. <br> ![Vue de l’ID d’audience qui ne doit pas être sélectionné.](/help/destinations/assets/api/ad-hoc-activation/audience-id-do-not-use.png "Vue de l’ID d’audience qui ne doit pas être sélectionné."){width="100" zoomable="yes"} <br> ![Vue de l’identifiant d’audience généré par le système qui doit être utilisé.](/help/destinations/assets/api/ad-hoc-activation/system-generated-id-to-use.png "Vue de l’identifiant d’audience généré par le système qui doit être utilisé."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

### Requête avec ID d’export {#request-export-ids}

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Identifiants des instances de destination vers lesquelles vous souhaitez activer des audiences. Vous pouvez obtenir ces identifiants à partir de l’interface utilisateur de Platform en accédant à l’onglet **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]**, puis en cliquant sur la ligne de destination souhaitée pour afficher l’identifiant de destination dans le rail de droite. Pour plus d’informations, consultez la [documentation de l’espace de travail des destinations](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Identifiants des audiences que vous souhaitez activer vers la destination sélectionnée. |
| <ul><li>`exportId1`</li></ul> | L’identifiant renvoyé dans la réponse de la tâche [exportation de l’audience](../../segmentation/api/export-jobs.md#retrieve-list). Voir [Étape 4 : obtenir le dernier identifiant de tâche d’exportation d’audience](#segment-export-id) pour obtenir des instructions sur la manière de trouver cet identifiant. |

{style="table-layout:auto"}

### Réponse {#response}

Une réponse réussie renvoie un statut HTTP 200.

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
| `statusURL` | URL de statut du flux d’activation. Vous pouvez suivre la progression du flux à l’aide de l’[API Flow Service](../../sources/tutorials/api/monitor.md). |

{style="table-layout:auto"}

## Gestion des erreurs d’API {#api-error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

### Codes d’erreur d’API et messages spécifiques à l’API d’activation ad hoc {#specific-error-messages}

Lors de l’utilisation de l’API d’activation ad hoc, vous pouvez rencontrer des messages d’erreur spécifiques à ce point d’entrée de l’API. Consultez le tableau pour comprendre comment y remédier lorsqu’ils apparaissent.

| Message d’erreur | Résolution |
|---------|----------|
| Exécution déjà en cours pour l’audience `segment ID` pour la commande `dataflow ID` avec l’ID d’exécution `flow run ID` | Ce message d’erreur indique qu’un flux d’activation ad hoc est actuellement en cours pour une audience. Attendez que le traitement se termine avant de déclencher à nouveau le traitement d’activation. |
| Les segments `<segment name>` ne font pas partie de ce flux de données ou sont hors plage de planification. | Ce message d’erreur indique que les audiences que vous avez sélectionnées pour activation ne sont pas mappées au flux de données ou que le planning d’activation configuré pour les audiences a expiré ou n’a pas encore commencé. Vérifiez si l’audience est bien mappée au flux de données et que le planning d’activation de l’audience chevauche la date actuelle. |

## Informations connexes {#related-information}

* [Se connecter aux destinations par lots et activer des données à l’aide de l’API Flow Service](/help/destinations/api/connect-activate-batch-destinations.md)
* [(Version bêta) Exporter des fichiers à la demande vers des destinations par lots à l’aide de l’interface utilisateur Experience Platform](/help/destinations/ui/export-file-now.md)