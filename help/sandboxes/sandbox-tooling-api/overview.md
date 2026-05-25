---
title: Guide de l’API pour l’outil Sandbox
description: L’outil Sandbox de Adobe Experience Platform vous permet d’exporter et d’importer un instantané des configurations de sandbox entre des sandbox.
exl-id: 4bcc095b-5db1-4824-8b7c-c2ea5a393b98
TQID: https://experienceleague.adobe.com/8d-cc04rk3OD9MKJwPb6LZomp5oI13jEVkV9-E7VfkA
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 250
ht-degree: 14%

---

# Guide de l’API d’outils [!DNL Sandbox]

L’API d’outils [!DNL Sandbox] fournit plusieurs points d’entrée qui vous permettent d’exporter et d’importer des instantanés entre les sandbox disponibles au sein de votre organisation. Toutes les interactions se produisent via des points d’entrée HTTP. Le sandbox source est vérifié pour les artefacts, qui sont les objets contenus dans un package, avant d’exporter un instantané. Lorsqu’une demande d’importation est effectuée, un instantané de [!DNL Azure Blob] est obtenu et utilisé comme modèle pour produire des artefacts presque similaires pour le sandbox de destination. Consultez la documentation [outils Sandbox](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling) pour obtenir une liste des objets et limitations pris en charge.

Ces points d’entrée sont décrits ci-dessous. Consultez le guide de chaque point d’entrée pour plus de détails et reportez-vous au [guide de prise en main](./getting-started.md) pour obtenir des informations importantes sur les en-têtes nécessaires, la lecture des exemples d’appels d’API, etc.

## Packages {#packages}

Le point d’entrée des packages d’outils Sandbox vous permet de gérer les packages. Le package d’outils Sandbox est une collection de définitions d’artefact comprenant l’ID de package, le nom, la description, l’ID d’organisation et l’ID de créateur. Pour plus d’informations sur l’utilisation de packages dans l’API[&#128279;](./packages.md) consultez le  guide des points d’entrée de packages .

## Outils {#tools}

Le point d’entrée des outils de sandbox vous permet de récupérer indépendamment les données JSON de la tâche. Pour plus d’informations sur la récupération des données JSON de tâche dans l’API[&#128279;](./tools.md) consultez le  guide des points d’entrée des outils .

## Étapes suivantes {#next-steps}

Pour commencer à effectuer des appels à l’aide de l’API d’outils Sandbox, lisez le [guide de prise en main](./getting-started.md) puis sélectionnez l’un des guides des points d’entrée pour savoir comment utiliser des points d’entrée spécifiques.
