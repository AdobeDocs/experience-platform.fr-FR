---
keywords: Experience Platform;accueil;rubriques les plus consultées;ingestion par lots;Ingestion par lots;Ingestion partielle;Ingestion partielle;Récupérer l’erreur;récupérer l’erreur;Ingestion par lots partielle;Ingestion par lots partielle;partielle;ingestion;Ingestion;
solution: Experience Platform
title: Aperçu de l’ingestion par lots partielle
description: Ce document fournit un tutoriel pour la gestion de l’ingestion par lots partielle.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: bc72f77b1b4a48126be9b49c5c663ff11e9054ea
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 30%

---

# Ingestion par lots partielle

L’ingestion par lots partielle permet d’ingérer des données contenant des erreurs jusqu’à un certain seuil. Grâce à cette fonctionnalité, les utilisateurs peuvent ingérer toutes leurs données correctes dans Adobe Experience Platform, alors que toutes leurs données incorrectes sont traitées par lots séparément, avec des détails sur les raisons de leur non-validité.

Ce document fournit un tutoriel pour la gestion de l’ingestion par lots partielle.

## Prise en main

Ce tutoriel nécessite une connaissance pratique des différents services Adobe Experience Platform impliqués dans l’ingestion par lots partielle. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [Ingestion par lots](./overview.md) : méthode utilisée par [!DNL Experience Platform] pour ingérer et stocker des données provenant de fichiers de données, tels que CSV et Parquet.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.

Les sections suivantes contiennent des informations supplémentaires nécessaires pour passer des appels à des API [!DNL Experience Platform].

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Experience Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

## Activation d’un lot pour l’ingestion par lots partielle dans l’API {#enable-api}

>[!NOTE]
>
>Cette section décrit l’activation d’un lot pour l’ingestion par lots partielle à l’aide de l’API . Pour obtenir des instructions sur l’utilisation de l’interface utilisateur, veuillez lire l’étape [activer un lot pour l’ingestion par lots partielle dans l’interface utilisateur](#enable-ui).

Vous pouvez créer un lot pour lequel l’ingestion partielle est activée.

Pour créer un lot, suivez les étapes du guide de développement de l’ingestion par lots [batch ingestion](./api-overview.md). Une fois l’étape **[!UICONTROL Create batch]** atteinte, ajoutez le champ suivant dans le corps de la requête :

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| Propriété | Description |
| -------- | ----------- |
| `enableErrorDiagnostics` | Indicateur qui [!DNL Experience Platform] permet de générer des messages d’erreur détaillés sur votre lot. |
| `partialIngestionPercent` | Pourcentage d’erreurs acceptables avant l’échec du lot entier. Ainsi, dans cet exemple, un maximum de 5 % du lot peut être constitué d’erreurs, avant qu’il n’échoue. |


## Activer un lot pour l’ingestion de lots partiels dans l’interface utilisateur {#enable-ui}

>[!NOTE]
>
>Cette section décrit l’activation d’un lot pour l’ingestion par lots partielle à l’aide de l’interface utilisateur. Si vous avez déjà activé un lot pour l’ingestion de lots partiels à l’aide de l’API , vous pouvez passer à la section suivante.

Pour activer un lot pour une ingestion partielle via l’interface utilisateur de [!DNL Experience Platform], vous pouvez créer un lot à l’aide des connexions source, créer un lot dans un jeu de données existant ou créer un lot à l’aide de la fonction « [!UICONTROL Map CSV to XDM flow] ».

### Créer une connexion source {#new-source}

Pour créer une connexion source, procédez comme indiqué dans la section [Présentation des sources](../../sources/home.md). Une fois l’étape **[!UICONTROL Dataflow detail]** atteinte, notez les champs **[!UICONTROL Partial ingestion]** et **[!UICONTROL Error diagnostics]** .

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Le bouton (bascule) **[!UICONTROL Partial ingestion]** vous permet d’activer ou de désactiver l’utilisation de l’ingestion par lots partielle.

Le bouton **[!UICONTROL Error diagnostics]** n’apparaît que lorsque le bouton **[!UICONTROL Partial ingestion]** est désactivé. Cette fonctionnalité [!DNL Experience Platform] permet de générer des messages d’erreur détaillés sur vos lots ingérés. Si le bouton **[!UICONTROL Partial ingestion]** est activé, les diagnostics d’erreur améliorés sont automatiquement appliqués.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Le **[!UICONTROL Error threshold]** vous permet de définir le pourcentage d’erreurs acceptables avant l’échec de l’ensemble du lot. Par défaut, cette valeur est définie sur 5 %.

### Utiliser un jeu de données existant {#existing-dataset}

Pour utiliser un jeu de données existant, commencez par sélectionner un jeu de données. La barre latérale droite contient des informations sur le jeu de données.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Le bouton (bascule) **[!UICONTROL Partial ingestion]** vous permet d’activer ou de désactiver l’utilisation de l’ingestion par lots partielle.

Le bouton **[!UICONTROL Error diagnostics]** n’apparaît que lorsque le bouton **[!UICONTROL Partial ingestion]** est désactivé. Cette fonctionnalité [!DNL Experience Platform] permet de générer des messages d’erreur détaillés sur vos lots ingérés. Si le bouton **[!UICONTROL Partial ingestion]** est activé, les diagnostics d’erreur améliorés sont automatiquement appliqués.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Le **[!UICONTROL Error threshold]** vous permet de définir le pourcentage d’erreurs acceptables avant l’échec de l’ensemble du lot. Par défaut, cette valeur est définie sur 5 %.

Désormais, vous pouvez charger des données à l’aide du bouton **Ajouter des données**, et elles seront ingérées à l’aide de l’ingestion partielle.

### Utiliser le flux « [!UICONTROL Map CSV to XDM schema] » {#map-flow}

Pour utiliser le flux « [!UICONTROL Map CSV to XDM schema] », suivez les étapes répertoriées dans le tutoriel [Mapper un fichier CSV](../tutorials/map-csv/overview.md). Une fois l’étape **[!UICONTROL Add data]** atteinte, notez les champs **[!UICONTROL Partial ingestion]** et **[!UICONTROL Error diagnostics]** .

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Le bouton (bascule) **[!UICONTROL Partial ingestion]** vous permet d’activer ou de désactiver l’utilisation de l’ingestion par lots partielle.

Le bouton **[!UICONTROL Error diagnostics]** n’apparaît que lorsque le bouton **[!UICONTROL Partial ingestion]** est désactivé. Cette fonctionnalité [!DNL Experience Platform] permet de générer des messages d’erreur détaillés sur vos lots ingérés. Si le bouton **[!UICONTROL Partial ingestion]** est activé, les diagnostics d’erreur améliorés sont automatiquement appliqués.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Error threshold]** vous permet de définir le pourcentage d’erreurs acceptables avant l’échec de l’ensemble du lot. Par défaut, cette valeur est définie sur 5 %.

## Activation des diagnostics d’ingestion et d’erreur partiels pour un flux de données existant

Si un flux de données dans Experience Platform a été créé sans activer l’ingestion partielle ou les diagnostics d’erreur, vous pouvez toujours activer ces fonctionnalités sans recréer le flux. En activant l’ingestion partielle et des diagnostics d’erreur fiables, vous pouvez améliorer considérablement la fiabilité et la facilité de dépannage de vos workflows d’ingestion de données. Lisez les sections ci-dessous pour savoir comment activer l’ingestion partielle et les diagnostics d’erreur pour un flux de données existant à l’aide de l’API [!DNL Flow Service].

Par défaut, l’ingestion partielle ou les diagnostics d’erreur ne sont pas activés pour les flux de données. Ces fonctionnalités sont utiles pour identifier et isoler les problèmes lors de l’ingestion de données. À l’aide de l’API [!DNL Flow Service], vous pouvez récupérer la configuration actuelle de votre flux de données et appliquer les modifications nécessaires à l’aide d’une requête PATCH.

Suivez les étapes ci-dessous pour activer les diagnostics d’ingestion et d’erreur partiels pour un flux de données existant.

### Récupérer les détails du flux

Pour récupérer vos configurations de flux de données, envoyez une requête GET au point d’entrée `/flows/{FLOW_ID}` et indiquez l’identifiant de votre flux de données. Pour plus d’informations sur la récupération des détails du flux de données, reportez-vous au guide [Mettre à jour les flux de données à l’aide de l’API [!DNL Flow Service]  ](../../sources/tutorials/api/update-dataflows.md).

Veillez à enregistrer la valeur du champ `etag` renvoyé dans la réponse. Cela est nécessaire pour que la demande de mise à jour garantisse la cohérence des versions.

### Mettre à jour la configuration de flux

Ensuite, envoyez une requête PATCH au point d’entrée `/flows/` et indiquez l’identifiant du flux de données pour lequel vous souhaitez activer l’ingestion partielle et les diagnostics d’erreur.

>[!IMPORTANT]
>
>- Incluez la valeur de `etag` enregistrée précédemment dans l’en-tête de la requête à l’aide de la clé If-Match .
>- Vous pouvez modifier la valeur `partialIngestionPercent` en fonction de vos besoins spécifiques.

**Format d’API**

```http
PATCH /flows/{FLOW_ID}
```

**Requête**

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
        {
            "op": "add",
            "path": "/options",
            "value": {
                "partialIngestionPercent": "10"
            }
        },
        {
            "op": "add",
            "path": "/options/errorDiagnosticsEnabled",
            "value": true
        }
    ]'
```

**Réponse**

Une réponse réussie renvoie le `id` de votre flux de données et une `etag` mise à jour.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

### Vérifier la mise à jour

Une fois le PATCH terminé, envoyez une requête GET et récupérez votre flux de données pour vérifier que les modifications ont bien été apportées.

**Format d’API**

```http
GET /flows/{FLOW_ID}
```

**Requête**

La requête suivante récupère des informations mises à jour concernant votre identifiant de flux.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie les détails de votre flux de données, confirmant que l’ingestion partielle et les diagnostics d’erreur sont désormais activés dans la section `options`.

```json
"options": {
    "partialIngestionPercent": 10,
    "errorDiagnosticsEnabled": true
}
```

## Étapes suivantes {#next-steps}

Ce tutoriel explique comment créer ou modifier un jeu de données pour activer l’ingestion par lots partielle. Pour plus d’informations sur l’ingestion par lots, consultez le [guide de développement de l’ingestion par lots](./api-overview.md).

Pour plus d’informations sur la surveillance des erreurs d’ingestion partielle, consultez le [guide de diagnostic des erreurs d’ingestion par lots](../quality/error-diagnostics.md).
