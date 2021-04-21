---
keywords: Experience Platform ; accueil ; rubriques populaires ; assimilation par lots ; assimilation par lots ; assimilation partielle ; assimilation partielle ; extraction de l'erreur ; extraction de l'erreur ; assimilation par lots partielle ; assimilation par lots partielle ; assimilation partielle ; assimilation ; assimilation ;
solution: Experience Platform
title: Présentation partielle de l'importation par lots
topic-legacy: overview
description: Ce document fournit un tutoriel pour la gestion de l’ingestion par lots partielle.
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 42%

---

# Ingestion par lots partielle

L’ingestion par lots partielle permet d’ingérer des données contenant des erreurs jusqu’à un certain seuil. Grâce à cette fonctionnalité, les utilisateurs peuvent ingérer toutes leurs données correctes dans Adobe Experience Platform, alors que toutes leurs données incorrectes sont traitées par lots séparément, avec des détails sur les raisons de leur non-validité.

Ce document fournit un tutoriel pour la gestion de l’ingestion par lots partielle.

## Prise en main

Ce tutoriel nécessite une connaissance pratique des différents services Adobe Experience Platform impliqués dans l’ingestion par lots partielle. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [Ingestion par lots](./overview.md)[!DNL Platform] : méthode d’ingestion et de stockage de données de fichiers, par exemple de type CSV et Parquet, dans 
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : Cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.

Les sections suivantes fournissent des informations supplémentaires dont vous aurez besoin pour pouvoir invoquer les API [!DNL Platform].

### Lecture d’exemples d’appels API

Ce guide fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage[!DNL Experience Platform].

### Collecter des valeurs pour les en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://www.adobe.com/go/platform-api-authentication-en). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de [!DNL Experience Platform] sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d&#39;API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l&#39;opération aura lieu :

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d&#39;informations sur les sandbox dans [!DNL Platform], consultez la [documentation d&#39;aperçu de sandbox](../../sandboxes/home.md).

## Activez un lot pour l&#39;assimilation partielle de lots dans l&#39;API {#enable-api}

>[!NOTE]
>
>Cette section décrit l&#39;activation d&#39;un lot pour l&#39;assimilation partielle de lots à l&#39;aide de l&#39;API. Pour obtenir des instructions sur l&#39;utilisation de l&#39;interface utilisateur, consultez l&#39;[activation d&#39;un lot pour l&#39;assimilation partielle de lots à l&#39;étape UI](#enable-ui).

Vous pouvez créer un nouveau lot avec l&#39;assimilation partielle activée.

Pour créer un nouveau lot, suivez les étapes du [guide du développeur d&#39;assimilation par lot](./api-overview.md). Une fois que vous avez atteint l’étape **[!UICONTROL Créer un lot]**, ajoutez le champ suivant dans le corps de la requête :

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| Propriété | Description |
| -------- | ----------- |
| `enableErrorDiagnostics` | Indicateur qui permet à [!DNL Platform] de générer des messages d&#39;erreur détaillés sur votre lot. |
| `partialIngestionPercentage` | Pourcentage d’erreurs acceptables avant le rejet de l’ensemble du lot. Ainsi, dans cet exemple, un maximum de 5 % du lot peut être une erreur, avant qu’il ne soit endommagé. |


## Activer un lot pour l&#39;assimilation partielle de lots dans l&#39;interface utilisateur {#enable-ui}

>[!NOTE]
>
>Cette section décrit l&#39;activation d&#39;un lot pour l&#39;assimilation partielle de lots à l&#39;aide de l&#39;interface utilisateur. Si vous avez déjà activé un lot pour l&#39;assimilation partielle de lots à l&#39;aide de l&#39;API, vous pouvez passer à la section suivante.

Pour activer un lot pour l&#39;assimilation partielle via l&#39;interface utilisateur [!DNL Platform], vous pouvez créer un nouveau lot via les connexions source, créer un nouveau lot dans un jeu de données existant, ou créer un nouveau lot via &quot;[!UICONTROL Faire correspondre le flux CSV au flux XDM]&quot;.

### Créer une connexion source {#new-source}

Pour créer une nouvelle connexion source, suivez les étapes répertoriées dans la section [Présentation des sources](../../sources/home.md). Une fois que vous avez atteint l&#39;étape **[!UICONTROL Détails du flux de données]**, notez les champs **[!UICONTROL Importation partielle]** et **[!UICONTROL Diagnostic d&#39;erreur]**.

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

Le bouton **[!UICONTROL Ingestion partielle]** vous permet d’activer ou de désactiver l’utilisation de l’ingestion par lots partielle.

La bascule **[!UICONTROL Diagnostics d&#39;erreur]** n&#39;apparaît que lorsque la bascule **[!UICONTROL assimilation partielle]** est désactivée. Cette fonctionnalité permet à [!DNL Platform] de générer des messages d&#39;erreur détaillés sur vos lots assimilés. Si la bascule **[!UICONTROL assimilation partielle]** est activée, les diagnostics d&#39;erreur améliorés sont automatiquement appliqués.

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

Le **[!UICONTROL seuil d’erreur]** vous permet de définir le pourcentage d’erreurs acceptables avant le rejet de l’ensemble du lot. Par défaut, cette valeur est définie sur 5 %.

### Utilisation d’un jeu de données existant {#existing-dataset}

Pour utiliser un jeu de données existant, début en sélectionnant un jeu de données. La barre latérale droite contient des informations sur le jeu de données.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

Le bouton **[!UICONTROL Ingestion partielle]** vous permet d’activer ou de désactiver l’utilisation de l’ingestion par lots partielle.

La bascule **[!UICONTROL Diagnostics d&#39;erreur]** n&#39;apparaît que lorsque la bascule **[!UICONTROL assimilation partielle]** est désactivée. Cette fonctionnalité permet à [!DNL Platform] de générer des messages d&#39;erreur détaillés sur vos lots assimilés. Si la bascule **[!UICONTROL assimilation partielle]** est activée, les diagnostics d&#39;erreur améliorés sont automatiquement appliqués.

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

Le **[!UICONTROL seuil d’erreur]** vous permet de définir le pourcentage d’erreurs acceptables avant le rejet de l’ensemble du lot. Par défaut, cette valeur est définie sur 5 %.

Désormais, vous pouvez transférer des données à l’aide du bouton **Ajouter les données** et elles seront ingérées à l’aide de l’assimilation partielle.

### Utilisez le flux &quot;[!UICONTROL Faire correspondre le fichier CSV au schéma XDM]&quot; {#map-flow}

Pour utiliser le flux &quot;[!UICONTROL Mapper le fichier CSV au schéma XDM]&quot;, suivez les étapes répertoriées dans le didacticiel [Mapper un fichier CSV](../tutorials/map-a-csv-file.md). Une fois que vous avez atteint l&#39;étape **[!UICONTROL Ajouter les données]**, notez les champs **[!UICONTROL Envoi partiel]** et **[!UICONTROL Diagnostic d&#39;erreur]**.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

Le bouton **[!UICONTROL Ingestion partielle]** vous permet d’activer ou de désactiver l’utilisation de l’ingestion par lots partielle.

La bascule **[!UICONTROL Diagnostics d&#39;erreur]** n&#39;apparaît que lorsque la bascule **[!UICONTROL assimilation partielle]** est désactivée. Cette fonctionnalité permet à [!DNL Platform] de générer des messages d&#39;erreur détaillés sur vos lots assimilés. Si la bascule **[!UICONTROL assimilation partielle]** est activée, les diagnostics d&#39;erreur améliorés sont automatiquement appliqués.

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL Le]** seuil d’erreur vous permet de définir le pourcentage d’erreurs acceptables avant que le lot entier n’échoue. Par défaut, cette valeur est définie sur 5 %.

## Étapes suivantes {#next-steps}

Ce tutoriel explique comment créer ou modifier un jeu de données pour activer l’ingestion par lots partielle. Pour plus d’informations sur l’ingestion par lots, consultez le [guide de développement de l’ingestion par lots](./api-overview.md).

Pour plus d&#39;informations sur la surveillance des erreurs d&#39;assimilation partielle, consultez le [guide de diagnostic des erreurs d&#39;assimilation par lot](../quality/error-diagnostics.md).
