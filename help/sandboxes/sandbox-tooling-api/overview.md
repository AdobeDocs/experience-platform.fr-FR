---
title: Guide de l’API des outils Sandbox
description: Les outils Sandbox dans Adobe Experience Platform vous permettent d’exporter et d’importer un instantané des configurations des environnements de test entre les environnements de test.
exl-id: 4bcc095b-5db1-4824-8b7c-c2ea5a393b98
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 14%

---

# Guide de l’API d’outils [!DNL Sandbox]

L’API d’outils [!DNL Sandbox] fournit plusieurs points de terminaison qui vous permettent d’exporter et d’importer des instantanés entre les environnements de test disponibles pour vous au sein de votre organisation. Toutes les interactions se produisent via des points de terminaison HTTP. L’environnement de test source est analysé à la recherche d’artefacts, qui sont les objets contenus dans un package, avant d’exporter un instantané. Lorsqu’une demande d’importation est effectuée, un instantané [!DNL Azure Blob] est obtenu et utilisé comme modèle pour produire des artefacts presque similaires pour l’environnement de test de destination. Pour obtenir la liste des objets et des limites pris en charge, reportez-vous à la documentation [outil de test](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) .

Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

## Packages   {#packages}

Le point de terminaison des modules d’outils Sandbox vous permet de gérer les modules. Le module d’outils d’environnement de test est une collection de définitions d’artefact, y compris l’ID de module, le nom, la description, l’ID d’organisation et l’ID de créateur. Pour plus d’informations sur l’utilisation des modules dans l’API, consultez le [guide de point de terminaison des packages](./packages.md) .

## Outils {#tools}

Le point de terminaison des outils d’environnement de test vous permet de récupérer indépendamment les données JSON de la tâche. Pour plus d’informations sur la récupération des données JSON de tâche dans l’API, consultez le [guide de point de terminaison d’outils](./tools.md) .

## Étapes suivantes {#next-steps}

Pour commencer à lancer des appels à l’aide de l’API d’outils de test, lisez le [guide de prise en main](./getting-started.md) , puis sélectionnez l’un des guides de point de terminaison pour savoir comment utiliser des points de terminaison spécifiques.
