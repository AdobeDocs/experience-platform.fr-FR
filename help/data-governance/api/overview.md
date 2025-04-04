---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Guide de l’API Policy Service
description: L’API Policy Service permet aux développeurs de gérer les libellés et les politiques d’utilisation des données dans Experience Platform. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
role: Developer
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 86%

---

# Guide de l’API [!DNL Policy Service]

La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Elle joue un rôle clé dans [!DNL Experience Platform], et ce, à différents niveaux, notamment dans le catalogage, la traçabilité des données, l’étiquetage d’utilisation des données, les politiques d’utilisation des données et le contrôle de l’utilisation des données lors d’actions marketing.

L’API [!DNL Policy Service] fournit plusieurs points d’entrée vous permettant de gérer par programmation les libellés et les politiques d’utilisation des données, ainsi que d’évaluer les actions marketing en cas de violation de ces politiques. Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

Pour afficher tous les points d’entrée et opérations CRUD disponibles, consultez le document Swagger de l’[[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Libellés

Appliquez les libellés d’utilisation des données pour classer les jeux de données et les champs en fonction des politiques d’utilisation qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Les bonnes pratiques recommandent de libeller les données dès qu’elles sont ingérées dans [!DNL Experience Platform], ou dès que les données sont disponibles pour une utilisation dans [!DNL Experience Platform]. Vous pouvez créer, afficher, modifier et supprimer des libellés à l’aide du point d’entrée `/labels`. Pour découvrir comment utiliser ce point d’entrée, consultez le [guide des points d’entrée des libellés](./labels.md).

## Actions marketing

Les actions marketing (également appelées cas dʼutilisation marketing), dans le contexte du cadre de gouvernance des données, sont des actions quʼun utilisateur de données [!DNL Experience Platform] peut entreprendre et pour lesquelles votre entreprise souhaite restreindre lʼutilisation des données. Pour obtenir des informations détaillées sur l’utilisation des actions marketing, consultez le [guide des points d’entrée des actions marketing](./marketing-actions.md).

## Politiques

Les politiques de gouvernance des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé(e) ou non à effectuer sur des données dans [!DNL Experience Platform].

>[!NOTE]
>
>Les politiques de gouvernance des données ne doivent pas être confondues avec les politiques de contrôle d’accès, qui déterminent les attributs de données spécifiques accessibles par certains utilisateurs et utilisatrices d’Experience Platform dans votre organisation. Pour plus d’informations, consultez le guide sur le [contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md).

Une politique de gouvernance des données est définie par les éléments suivants :

1. Une action marketing spécifique
1. Le ou les libellé(s) d’utilisation des données envers lesquels l’action ne peut pas être exécutée

Pour savoir comment gérer les politiques dans l’API, consultez le [guide des points d’entrée des politiques](./policies.md).

## Évaluation

Une fois que les libellés d’utilisation des données ont été appliqués aux schémas Experience Platform et que les politiques d’utilisation des données ont été définies pour les actions marketing suivant ces libellés, les fonctionnalités de gouvernance des données vous permettent d’appliquer ces politiques et d’empêcher les opérations de données en violation avec celles-ci.

L’API [!DNL Policy Service] fournit des points d’entrée qui vous permettent de tester les actions marketing par rapport aux jeux de données ou à des combinaisons arbitraires de libellés d’utilisation des données, afin de vérifier si des violations de politiques se produisent. En fonction de la réponse de l’API, vous pouvez configurer des protocoles dans votre application d’expérience, afin d’être en conformité avec les politiques d’utilisation des données. Pour plus d’informations, consultez le [guide des points d’entrée d’évaluation](./evaluation.md).

## Étapes suivantes

Pour commencer à effectuer des appels à l’aide de l’API [!DNL Policy Service], consultez le guide de prise en main [guide de prise en main](./getting-started.md), puis sélectionnez l’un des guides des points d’entrée pour savoir comment utiliser des points d’entrée spécifiques. Pour utiliser les libellés et les politiques à l’aide de l’interface utilisateur [!DNL Experience Platform], reportez-vous respectivement au [guide de d’utilisation des libellés](../labels/user-guide.md) et au [guide d’utilisation des politiques](../policies/user-guide.md).
