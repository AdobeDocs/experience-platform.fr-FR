---
title: Pagination des réponses dans l’API Reactor
description: Découvrez comment paginer les résultats lorsque vous répertoriez des ressources dans l’API Reactor.
exl-id: bccb6e78-4ac8-4786-b398-6e55109d99dd
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 86%

---

# Pagination des réponses dans l’API Reactor

Les réponses renvoyées par l’API Reactor sont mises en page. La taille de page par défaut est de 25 éléments. Des détails sur la pagination sont signalés dans la section `meta.pagination` de l’objet de réponse de l’API :

```json
"meta": {
  "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 4,
      "total_count": 90
  }
}
```

Il est possible d’obtenir une page spécifique et de modifier la taille d’une page en incluant un paramètre de requête `page` dans le chemin de requête.

## Récupération d’une page spécifique

Pour obtenir une page spécifique :

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[number]={PAGE_NUMBER}
```

## Modifier la taille de la page

Pour modifier la taille de la page :

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}
```

Différentes options peuvent être combinées :

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}&page[number]={PAGE_NUMBER}
```
