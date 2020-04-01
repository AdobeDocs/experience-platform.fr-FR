---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Présentation des stratégies d’utilisation des données
topic: policies
translation-type: tm+mt
source-git-commit: d08f06b3c2bdb21e0f4935bbcb6f163892ab9842

---


# Présentation des stratégies d’utilisation des données

Pour que les étiquettes d’utilisation des données prennent efficacement en charge la conformité des données, il faut mettre en oeuvre des stratégies d’utilisation des données. Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé à exécuter, ou dont vous êtes limité, sur les données dans la plateforme d’expérience.

Un exemple d’action marketing peut être le désir d’exporter un jeu de données vers un service tiers. S’il existe une stratégie stipulant que des types spécifiques de données, tels que les informations d’identification personnelle (informations d’identification personnelle), ne peuvent pas être exportés et qu’une étiquette &quot;I&quot; (données d’identité) a été appliquée au jeu de données, vous recevrez une réponse du service de stratégie vous indiquant qu’une stratégie d’utilisation des données a été violée.

## Création et utilisation des stratégies d’utilisation des données

Une fois les libellés d’utilisation des données appliqués, les gestionnaires de données peuvent créer des stratégies à l’aide de l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)DULE Policy Service.

En tant que gestionnaire de données, vous pouvez utiliser l’API Service de stratégie pour gérer et évaluer les stratégies liées aux actions marketing effectuées sur les données contenant des libellés DULE. L’API vous permet de créer et de mettre à jour des stratégies, de déterminer l’état d’une stratégie et d’utiliser des actions marketing pour évaluer si une action spécifique viole une stratégie d’utilisation des données.

Dans l’API du service de stratégie, toutes les stratégies et actions marketing sont appelées `core` ou `custom` ressources. `core` les ressources sont définies et gérées par Adobe, tandis que `custom` les ressources sont créées et gérées par des clients individuels. Les `custom` ressources sont donc uniques et visibles uniquement à l&#39;organisation qui les a créées.

Pour plus d&#39;informations sur l&#39;exécution des opérations clés fournies par l&#39;API DULE Policy Service, consultez le guide [du développeur](../api/getting-started.md)Policy Service. Pour obtenir des instructions détaillées sur l’utilisation des stratégies DULE, consultez le didacticiel sur la [création et l’évaluation des stratégies](create.md)DULE.