---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;partial ingestion;Partial ingestion;Retrieve error;retrieve error;Partial batch ingestion;partial batch ingestion;partial;ingestion;Ingestion;
solution: Experience Platform
title: Présentation de l'assimilation par lots partielle
topic: overview
description: Ce document fournit un tutoriel pour la gestion de l’ingestion par lots partielle.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 43%

---


# Ingestion par lots partielle

L’ingestion par lots partielle permet d’ingérer des données contenant des erreurs jusqu’à un certain seuil. Grâce à cette fonctionnalité, les utilisateurs peuvent ingérer toutes leurs données correctes dans Adobe Experience Platform, alors que toutes leurs données incorrectes sont traitées par lots séparément, avec des détails sur les raisons de leur non-validité.

Ce document fournit un tutoriel pour la gestion de l’ingestion par lots partielle.

## Prise en main

Ce tutoriel nécessite une connaissance pratique des différents services Adobe Experience Platform impliqués dans l’ingestion par lots partielle. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [Ingestion par lots](./overview.md)[!DNL Platform] : méthode d’ingestion et de stockage de données de fichiers, par exemple de type CSV et Parquet, dans 
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

The following sections provide additional information that you will need to know in order to successfully make calls to [!DNL Platform] APIs.

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](../../tutorials/authentication.md). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

## Enable a batch for partial batch ingestion in the API {#enable-api}

>[!NOTE]
>
>Cette section décrit l&#39;activation d&#39;un lot pour l&#39;assimilation partielle de lots à l&#39;aide de l&#39;API. For instructions on using the UI, please read the [enable a batch for partial batch ingestion in the UI](#enable-ui) step.

Vous pouvez créer un nouveau lot avec l&#39;assimilation partielle activée.

Pour créer un nouveau lot, suivez les étapes décrites dans le guide [du développeur d&#39;assimilation](./api-overview.md)par lot. Once you reach the **[!UICONTROL Create batch]** step, add the following field within the request body:

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Propriété | Description |
| -------- | ----------- |
| `enableErrorDiagnostics` | Indicateur qui permet [!DNL Platform] de générer des messages d&#39;erreur détaillés sur votre lot. |
| `partialIngestionPercentage` | Pourcentage d’erreurs acceptables avant le rejet de l’ensemble du lot. Ainsi, dans cet exemple, un maximum de 5 % du lot peut être une erreur, avant qu’il ne soit endommagé. |


## Enable a batch for partial batch ingestion in the UI {#enable-ui}

>[!NOTE]
>
>Cette section décrit l&#39;activation d&#39;un lot pour l&#39;assimilation partielle de lots à l&#39;aide de l&#39;interface utilisateur. Si vous avez déjà activé un lot pour l&#39;assimilation partielle de lots à l&#39;aide de l&#39;API, vous pouvez passer à la section suivante.

Pour activer un lot pour l’assimilation partielle via l’ [!DNL Platform] interface utilisateur, vous pouvez créer un nouveau lot par le biais des connexions source, créer un nouveau lot dans un jeu de données existant ou créer un nouveau lot par le biais du flux[!UICONTROL &quot;]Mapper le fichier CSV au fichier XDM&quot;.

### Créer une connexion source {#new-source}

Pour créer une connexion à la source, suivez les étapes répertoriées dans l&#39;aperçu [des](../../sources/home.md)sources. Once you reach the **[!UICONTROL Dataflow detail]** step, take note of the **[!UICONTROL Partial ingestion]** and **[!UICONTROL Error diagnostics]** fields.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Le bouton **[!UICONTROL Ingestion partielle]** vous permet d’activer ou de désactiver l’utilisation de l’ingestion par lots partielle.

The **[!UICONTROL Error diagnostics]** toggle only appears when the **[!UICONTROL Partial ingestion]** toggle is off. This feature allows [!DNL Platform] to generate detailed error messages about your ingested batches. If the **[!UICONTROL Partial ingestion]** toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Le **[!UICONTROL seuil d’erreur]** vous permet de définir le pourcentage d’erreurs acceptables avant le rejet de l’ensemble du lot. Par défaut, cette valeur est définie sur 5 %.

### Utilisation d’un jeu de données existant {#existing-dataset}

Pour utiliser un jeu de données existant, début en sélectionnant un jeu de données. La barre latérale droite contient des informations sur le jeu de données.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Le bouton **[!UICONTROL Ingestion partielle]** vous permet d’activer ou de désactiver l’utilisation de l’ingestion par lots partielle.

The **[!UICONTROL Error diagnostics]** toggle only appears when the **[!UICONTROL Partial ingestion]** toggle is off. This feature allows [!DNL Platform] to generate detailed error messages about your ingested batches. If the **[!UICONTROL Partial ingestion]** toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Le **[!UICONTROL seuil d’erreur]** vous permet de définir le pourcentage d’erreurs acceptables avant le rejet de l’ensemble du lot. Par défaut, cette valeur est définie sur 5 %.

Désormais, vous pouvez transférer des données à l’aide du bouton **Ajouter les données** et elles seront ingérées à l’aide de l’assimilation partielle.

### Utilisation du flux &quot;[!UICONTROL Mapper le fichier CSV au schéma]XDM&quot; {#map-flow}

Pour utiliser le flux &quot;[!UICONTROL Mapper un fichier CSV au schéma]XDM&quot;, suivez les étapes répertoriées dans le didacticiel [](../tutorials/map-a-csv-file.md)Mapper un fichier CSV. Once you reach the **[!UICONTROL Add data]** step, take note of the **[!UICONTROL Partial ingestion]** and **[!UICONTROL Error diagnostics]** fields.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Le bouton **[!UICONTROL Ingestion partielle]** vous permet d’activer ou de désactiver l’utilisation de l’ingestion par lots partielle.

The **[!UICONTROL Error diagnostics]** toggle only appears when the **[!UICONTROL Partial ingestion]** toggle is off. This feature allows [!DNL Platform] to generate detailed error messages about your ingested batches. If the **[!UICONTROL Partial ingestion]** toggle is turned on, enhanced error diagnostics are automatically enforced.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Le seuil]** d’erreur permet de définir le pourcentage d’erreurs acceptables avant que le lot entier ne soit mis en échec. Par défaut, cette valeur est définie sur 5 %.

## Étapes suivantes {#next-steps}

Ce tutoriel explique comment créer ou modifier un jeu de données pour activer l’ingestion par lots partielle. Pour plus d’informations sur l’ingestion par lots, consultez le [guide de développement de l’ingestion par lots](./api-overview.md).

Pour plus d&#39;informations sur la surveillance des erreurs d&#39;assimilation partielle, consultez le guide [de diagnostic des erreurs d&#39;assimilation par](../quality/error-diagnostics.md)lot.
