---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Guide de l'API de service de stratégie
topic-legacy: developer guide
description: L’API Policy Service permet aux développeurs de gérer les étiquettes d’utilisation des données et les stratégies dans l’Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 15%

---

# [!DNL Policy Service] Guide des API

Adobe Experience Platform [!DNL Data Governance] vous permet de gérer les données client et de veiller au respect des réglementations, restrictions et stratégies applicables à l’utilisation des données. Il joue un rôle clé dans [!DNL Experience Platform] à divers niveaux, notamment le catalogage, le lignage des données, l&#39;étiquetage de l&#39;utilisation des données, les stratégies d&#39;utilisation des données et le contrôle de l&#39;utilisation des données pour les actions marketing.

L&#39;API [!DNL Policy Service] fournit plusieurs points de terminaison qui vous permettent de gérer par programmation les étiquettes et les stratégies d&#39;utilisation des données, ainsi que d&#39;évaluer les actions marketing en cas de violation des stratégies. Ces points de terminaison sont décrits ci-dessous. Consultez les guides individuels des points de terminaison pour plus de détails et consultez le [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes requis, la lecture d&#39;exemples d&#39;appels d&#39;API, etc.

Pour vue de tous les points de terminaison et opérations CRUD disponibles, consultez le [[!DNL Policy Service] swagger d’API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).

## Étiquettes

Les libellés d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Les meilleures pratiques encouragent l’étiquetage des données dès qu’elles sont ingérées dans [!DNL Experience Platform] ou dès que les données sont disponibles pour être utilisées dans [!DNL Platform]. Vous pouvez créer, vue, modifier et supprimer des étiquettes à l’aide du point de terminaison `/labels`. Pour savoir comment utiliser ce point de terminaison, consultez le [guide des points de terminaison des étiquettes](./labels.md).

## Actions marketing

Actions marketing (également appelés cas d’utilisation marketing), dans le contexte de la structure [!DNL Data Governance], sont des actions qu’un utilisateur de données [!DNL Experience Platform] peut entreprendre, pour lesquelles votre entreprise souhaite limiter l’utilisation des données. Pour plus d&#39;informations sur l&#39;utilisation des actions marketing, consultez le [guide du point de terminaison des actions marketing](./marketing-actions.md).

## Stratégies

Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé à exécuter, ou dont vous êtes limité à l’exécution, sur les données dans [!DNL Experience Platform]. Une stratégie est définie par les éléments suivants :

1. Une action marketing spécifique
1. Étiquette(s) d&#39;utilisation des données pour laquelle l&#39;action est limitée ne peut pas être exécutée

Pour savoir comment gérer les stratégies dans l&#39;API, consultez le [guide des points de terminaison des stratégies](./policies.md).

## Évaluation

Une fois les étiquettes d&#39;utilisation des données appliquées aux [!DNL Platform] jeux de données et les stratégies d&#39;utilisation des données définies pour les actions marketing par rapport à ces étiquettes, les fonctionnalités de gouvernance des données vous permettent de les appliquer et d&#39;empêcher les opérations de données qui constituent des violations de stratégie.

L&#39;API [!DNL Policy Service] fournit des points de terminaison qui vous permettent de tester des actions marketing par rapport à des jeux de données ou à des combinaisons arbitraires d&#39;étiquettes d&#39;utilisation de données afin de vérifier si des violations de stratégie se produisent. En fonction de la réponse de l’API, vous pouvez configurer des protocoles dans votre application d’expérience, afin d’être en conformité avec les stratégies d’utilisation des données. Pour plus d&#39;informations, consultez le [guide des points de terminaison d&#39;évaluation](./evaluation.md).

## Étapes suivantes

Pour commencer à lancer des appels à l&#39;aide de l&#39;API [!DNL Policy Service], consultez le guide de prise en main [get started guide](./getting-started.md), puis sélectionnez l&#39;un des guides de points de terminaison pour savoir comment utiliser des points de terminaison spécifiques. Pour utiliser les libellés et les stratégies à l&#39;aide de l&#39;interface utilisateur [!DNL Experience Platform], consultez le [guide de l&#39;utilisateur ](../labels/user-guide.md) et [guide de l&#39;utilisateur des stratégies](../policies/user-guide.md), respectivement.
