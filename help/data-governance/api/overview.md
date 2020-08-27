---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de développement de l’API Policy Service
topic: developer guide
translation-type: tm+mt
source-git-commit: 71678b10c9e137016ea404305b272508b9c8cabe
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 16%

---


# [!DNL Policy Service] Guide du développeur d’API

Adobe Experience Platform [!DNL Data Governance] allows you to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data use. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data usage policies, and controlling usage of data for marketing actions.

L’ [!DNL Policy Service] API fournit plusieurs points de terminaison qui vous permettent de gérer par programmation les étiquettes et les stratégies d’utilisation des données, ainsi que d’évaluer les actions marketing en cas de violation des stratégies. Ces points de terminaison sont décrits ci-dessous. Consultez les guides des points de terminaison individuels pour plus de détails et consultez le guide [de](./getting-started.md) prise en main pour obtenir des informations importantes sur les en-têtes requis, la lecture d&#39;exemples d&#39;appels d&#39;API, etc.

Pour vue de tous les points de terminaison et opérations CRUD disponibles, consultez la page de permutation [[!DNL Policy Service] des](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)API.

## Étiquettes

Les libellés d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Best practices encourage labeling data as soon as it is ingested into [!DNL Experience Platform], or as soon as data becomes available for use in [!DNL Platform]. Vous pouvez créer, vue, modifier et supprimer des étiquettes à l’aide du `/labels` point de terminaison. Pour savoir comment utiliser ce point de terminaison, consultez le guide [des points de terminaison des](./labels.md)étiquettes.

## Actions marketing

Actions marketing (également appelés cas d’utilisation marketing), dans le contexte de la [!DNL Data Governance] structure, sont des actions qu’un utilisateur [!DNL Experience Platform] de données peut entreprendre, pour lesquelles votre entreprise souhaite limiter l’utilisation des données. Pour plus d’informations sur l’utilisation des actions marketing, voir le guide [des points de terminaison des actions](./marketing-actions.md)marketing.

## Stratégies

Data usage policies are rules that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on data within [!DNL Experience Platform]. Une stratégie est définie par les éléments suivants :

1. Une action marketing spécifique
1. Étiquette(s) d&#39;utilisation des données pour laquelle l&#39;action est limitée ne peut pas être exécutée

Pour savoir comment gérer les stratégies dans l’API, consultez le guide des points de terminaison des [stratégies.](./policies.md)

## Évaluation

Once data usage labels have been applied to [!DNL Platform] datasets, and data usage policies have been defined for marketing actions against those labels, Data Governance capabilities allow you to enforce those policies and prevent data operations that constitute policy violations.

The [!DNL Policy Service] API provides endpoints that allow you to test marketing actions against datasets or arbitrary combinations of data usage labels in order to check if any policy violations occur. En fonction de la réponse de l’API, vous pouvez configurer des protocoles dans votre application d’expérience, afin d’être en conformité avec les stratégies d’utilisation des données. See the [evaluation endpoints guide](./evaluation.md) for more information.

## Étapes suivantes

Pour commencer à lancer des appels à l’aide de l’ [!DNL Policy Service] API, lisez le guide de [prise en main](./getting-started.md) , puis sélectionnez l’un des guides de points de terminaison pour savoir comment utiliser des points de terminaison spécifiques. Pour utiliser des libellés et des stratégies à l’aide de l’ [!DNL Experience Platform] interface utilisateur, reportez-vous au guide [d’utilisation des](../labels/user-guide.md) libellés et au guide [d’utilisation des](../policies/user-guide.md)stratégies, respectivement.