---
keywords: Experience Platform;accueil;rubriques les plus consultées;évaluation de segment;service de segmentation;segmentation;segmentation;évaluer un segment;accéder aux résultats des segments;évaluer et accéder au segment ;
solution: Experience Platform
title: Évaluation et accès aux résultats des segments
topic-legacy: tutorial
type: Tutorial
description: Suivez ce tutoriel pour savoir comment évaluer les segments et accéder aux résultats des segments à l’aide de l’API Adobe Experience Platform Segmentation Service.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 67%

---

# Évaluation et accès aux résultats de segmentation

Ce document fournit un tutoriel sur l’évaluation des segments et l’accès aux résultats de segmentation à l’aide de [[!DNL Segmentation API]](../api/getting-started.md).

## Prise en main

Ce tutoriel nécessite une compréhension pratique des différents services [!DNL Adobe Experience Platform] impliqués dans la création de segments d’audience. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fournit un profil client unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Permet de créer des segments d’audience à partir de  [!DNL Real-time Customer Profile] données.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d’expérience client.
- [Environnements de test](../../sandboxes/home.md) : [!DNL Experience Platform] fournit des environnements de test virtuels qui divisent une instance [!DNL Platform] unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### En-têtes requis

Ce tutoriel exige aussi que vous ayez terminé le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis) pour passer des appels à des API [!DNL Platform] Le tutoriel d&#39;authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d&#39;API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom de l’environnement de test dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les environnements de test dans [!DNL Platform], consultez la [documentation de présentation des environnements de test](../../sandboxes/home.md).

Toutes les requêtes POST, PUT et PATCH requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Évaluation d’un segment

Une fois que vous avez développé, testé et enregistré votre définition de segment, vous pouvez ensuite évaluer le segment soit par une évaluation planifiée soit par l’évaluation sur demande.

[L’évaluation planifiée](#scheduled-evaluation) (également appelée « segmentation planifiée ») vous permet de créer un planning récurrent pour exécuter une tâche d’exportation à un moment précis, tandis que l’[évaluation sur demande](#on-demand-evaluation) implique la création d’une tâche de segmentation pour créer immédiatement l’audience. Les étapes à suivre pour chaque type d’évaluation sont décrites ci-dessous.

Si vous n’avez pas encore terminé le [tutoriel Créer un segment à l’aide de l’API Segmentation](./create-a-segment.md) ou créé une définition de segment à l’aide du [créateur de segments](../ui/overview.md), faites-le avant de suivre ce tutoriel.

## Évaluation planifiée {#scheduled-evaluation}

L’évaluation planifiée permet à votre organisation IMS de créer un planning récurrent pour exécuter automatiquement les tâches d’exportation.

>[!NOTE]
>
>L’évaluation planifiée peut être activée pour les environnements de test avec un maximum de cinq (5) stratégies de fusion pour [!DNL XDM Individual Profile]. Si votre organisation possède plus de cinq stratégies de fusion pour [!DNL XDM Individual Profile] dans un seul environnement de test, vous ne pourrez pas utiliser l’évaluation planifiée.

### Création d’un planning

En effectuant une requête POST sur le point de terminaison `/config/schedules`, vous pouvez créer un planning et inclure l’heure spécifique à laquelle le planning doit être déclenché.

Vous trouverez des informations plus détaillées sur l’utilisation de ce point de terminaison dans le [guide du point de terminaison de plannings](../api/schedules.md#create)

### Activation d’un planning

Par défaut, un planning est inactif lors de la création, sauf si la propriété `state` est définie sur `active` dans le corps de la requête de création (POST). Vous pouvez activer un planning (définissez `state` sur `active`) en effectuant une requête PATCH sur le point de terminaison `/config/schedules` et en incluant l’identifiant du planning dans le chemin.

Vous trouverez des informations plus détaillées sur l’utilisation de ce point de terminaison dans le [guide du point de terminaison de plannings](../api/schedules.md#update-state)

### Mise à jour de l’heure du planning

Vous pouvez mettre à jour l’heure du planning en effectuant une requête PATCH sur le point de terminaison `/config/schedules` et en incluant l’identifiant du planning dans le chemin.

Vous trouverez des informations plus détaillées sur l’utilisation de ce point de terminaison dans le [guide du point de terminaison de plannings](../api/schedules.md#update-schedule)

## Évaluation sur demande

L’évaluation sur demande vous permet de créer une tâche de segmentation afin de générer un segment ciblé chaque fois que vous en avez besoin. Contrairement à l’évaluation planifiée, celle-ci n’a lieu que sur demande et n’est pas récurrente.

### Création d’une tâche de segmentation

Une tâche de segmentation est un processus asynchrone qui crée un nouveau segment ciblé. Il fait référence à une définition de segment, ainsi qu’à toute stratégie de fusion contrôlant la manière dont [!DNL Real-time Customer Profile] fusionne les attributs qui se chevauchent dans vos fragments de profil. Lorsqu’une tâche de segmentation se termine avec succès, vous pouvez collecter diverses informations sur le segment, telles que les erreurs qui se sont produites au cours du traitement et la taille finale de votre audience.

Vous pouvez créer une tâche de segmentation en exécutant une requête POST sur le point de terminaison `/segment/jobs` dans l’API [!DNL Real-time Customer Profile]

Vous trouverez des informations plus détaillées sur l’utilisation de ce point de terminaison dans le [guide des points de terminaison des tâches de segmentation](../api/segment-jobs.md#create)


### Recherche de l’état de la tâche de segmentation

Vous pouvez utiliser l’`id` pour une tâche de segmentation spécifique afin d’effectuer une requête de recherche (GET) pour afficher l’état actuel de la tâche.

Vous trouverez des informations plus détaillées sur l’utilisation de ce point de terminaison dans le [guide des points de terminaison des tâches de segmentation](../api/segment-jobs.md#get)

## Interprétation des résultats de segmentation

Lorsque les tâches de segmentation sont exécutées avec succès, le mappage `segmentMembership` est mis à jour pour chaque profil inclus dans le segment. `segmentMembership` stocke également tous les segments d’audience préévalués qui sont ingérés  [!DNL Platform], ce qui permet l’intégration à d’autres solutions telles que  [!DNL Adobe Audience Manager].

L’exemple suivant illustre l’attribut `segmentMembership` pour chaque enregistrement de profil individuel :

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Propriété | Description |
| -------- | ----------- |
| `lastQualificationTime` | La date et l’heure auxquelles l’appartenance au segment a été affirmée et le profil est entré dans le segment ou en est sorti. |
| `status` | L’état de la participation au segment dans le cadre de la requête actuelle. Doit être égal à l’une des valeurs connues suivantes : <ul><li>`existing` : l’entité reste dans le segment.</li><li>`realized` : l’entité entre dans le segment.</li><li>`exited` : l’entité quitte le segment.</li></ul> |

## Accès aux résultats de segmentation

Vous pouvez accéder aux résultats d’une tâche de segmentation de deux manières : en accédant aux profils individuels ou en exportant une audience entière vers un jeu de données.

Les sections suivantes décrivent ces options de manière plus détaillée.

## Recherche d’un profil

Si vous connaissez le profil spécifique auquel vous souhaitez accéder, vous pouvez le faire à l’aide de l’API [!DNL Real-time Customer Profile]. Toutes les étapes pour accéder aux profils individuels sont disponibles dans le tutoriel sur l’[accès aux données de Real-time Customer Profile à l’aide de l’API Profile](../../profile/api/entities.md).

## Exportation d’un segment {#export}

Une fois la tâche de segmentation terminée (la valeur de l’attribut `status` correspond à &quot;SUCCEEDED&quot;), vous pouvez exporter votre audience vers un jeu de données permettant son accès et son utilisation.

Les étapes suivantes sont requises pour exporter votre audience :

- [Création d’un jeu de données cible](#create-a-target-dataset) : créez le jeu de données permettant de contenir les membres de l’audience.
- [Génération de profils d’audience dans le jeu de données](#generate-profiles-for-audience-members) : renseignez le jeu de données avec des profils individuels XDM en fonction des résultats d’une tâche de segmentation.
- [Contrôle de la progression de l’exportation](#monitor-export-progress) : vérifiez la progression actuelle du processus d’exportation.
- [Lecture des données d’audience](#next-steps) : récupérez les profils individuels XDM obtenus représentant les membres de votre audience.

### Création d’un jeu de données cible

Lors de l’exportation d’une audience, un jeu de données cible doit d’abord être créé. Il est important que le jeu de données soit correctement configuré pour garantir la réussite de l’exportation.

Le schéma sur lequel repose le jeu de données est l’une des principales considérations (`schemaRef.id` dans l’exemple de requête API ci-dessous). Pour exporter un segment, le jeu de données doit être basé sur la balise [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Un schéma d’union est un schéma en lecture seule généré par le système regroupant les champs des schémas qui partagent la même classe, dans ce cas précis, la classe XDM Individual Profile. Pour plus d’informations sur la vue d’union des schémas, consultez la [section Real-time Customer Profile du guide de développement du registre des schémas](../../xdm/api/getting-started.md).

Il existe deux manières de créer le jeu de données nécessaire :

- **Utilisation d’API :** les étapes suivantes de ce tutoriel indiquent comment créer un jeu de données qui référence le à  [!DNL XDM Individual Profile Union Schema] l’aide de l’ [!DNL Catalog] API.
- **Utilisation de l’interface utilisateur :** pour utiliser l’interface  [!DNL Adobe Experience Platform] utilisateur afin de créer un jeu de données qui référence le schéma d’union, suivez les étapes du tutoriel sur l’ [interface utilisateur, puis revenez à ce tutoriel pour passer aux étapes de ](../ui/overview.md) génération de profils d’audience [ ](#generate-xdm-profiles-for-audience-members).

Si vous disposez déjà d’un jeu de données compatible et que vous connaissez son identifiant, vous pouvez passer directement à l’étape de [génération de profils](#generate-xdm-profiles-for-audience-members).

**Format d’API**

```http
POST /dataSets
```

**Requête**

La requête suivante crée un jeu de données et fournit des paramètres de configuration dans le payload.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Propriété | Description |
| -------- | ----------- |
| `name` | Un nom explicite pour le jeu de données. |
| `schemaRef.id` | L’identifiant de la vue d’union (schéma) à laquelle le jeu de données sera associé. |

**Réponse**

Une réponse réussie renvoie un tableau contenant l’ID unique et en lecture seule généré par le système du jeu de données que vous venez de créer. Un identifiant de jeu de données correctement configuré est nécessaire pour exporter les membres de l’audience.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Génération de profils pour les membres de l’audience {#generate-profiles}

Une fois que vous disposez d’un jeu de données d’union persistant, vous pouvez créer une tâche d’exportation afin de conserver les membres de l’audience dans le jeu de données, en effectuant une requête POST sur le point de terminaison `/export/jobs` dans l’API et en fournissant l’identifiant du jeu de données et les informations sur les segments que vous souhaitez exporter.[!DNL Real-time Customer Profile]

Vous trouverez des informations plus détaillées sur l’utilisation de ce point de terminaison dans le [guide de point de terminaison des tâches d’exportation](../api/export-jobs.md#create)

### Contrôle de la progression de l’exportation

Lorsqu’une tâche d’exportation est en cours de traitement, vous pouvez contrôler son état en effectuant une requête GET sur le point de terminaison `/export/jobs` et en incluant l’`id` de la tâche d’exportation dans le chemin. La tâche d’exportation est terminée lorsque le champ `status` renvoie la valeur &quot;SUCCEEDED&quot;.

Vous trouverez des informations plus détaillées sur l’utilisation de ce point de terminaison dans le [guide de point de terminaison des tâches d’exportation](../api/export-jobs.md#get)

## Étapes suivantes

Une fois l’exportation terminée, vos données sont disponibles dans la balise [!DNL Data Lake] de [!DNL Experience Platform]. Vous pouvez ensuite utiliser la balise [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) pour accéder aux données à l’aide de la balise `batchId` associée à l’exportation. Selon la taille du segment, les données peuvent se présenter sous forme de blocs et le lot peut être constitué de plusieurs fichiers.

Pour obtenir des instructions détaillées sur l’utilisation de l’API [!DNL Data Access] pour accéder et télécharger des fichiers de lot, suivez le [tutoriel sur l’accès aux données](../../data-access/tutorials/dataset-data.md).

Vous pouvez également accéder aux données de segment correctement exportées à l’aide de [!DNL Adobe Experience Platform Query Service]. À l’aide de l’interface utilisateur ou de l’API RESTful, [!DNL Query Service] vous permet d’écrire, de valider et d’exécuter des requêtes sur des données dans [!DNL Data Lake].

Pour plus d’informations sur la manière d’interroger les données d’audience, consultez la documentation sur [[!DNL Query Service]](../../query-service/home.md).
