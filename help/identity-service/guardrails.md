---
keywords: Experience Platform;identité;service d’identité;dépannage;garde-fous;consignes;limite;
title: Barrières de sécurité pour Identity Service
description: Ce document fournit des informations sur l’utilisation et les limites de taux pour les données Identity Service afin de vous aider à optimiser l’utilisation du graphique d’identités.
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: b07a45e5bb9cae6e147ea790ebb77cb63f8790c1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 13%

---

# Barrières de sécurité pour [!DNL Identity Service] data

Ce document fournit des informations sur l’utilisation et les limites de taux pour [!DNL Identity Service] pour vous aider à optimiser l’utilisation du graphique d’identités. Lors de la révision des barrières de sécurité suivantes, on suppose que vous avez correctement modélisé les données. Si vous avez des questions sur la manière de modéliser vos données, contactez votre représentant du service client.

## Prise en main

Les services Experience Platform suivants sont impliqués dans la modélisation des données d’identité :

* [Identités](home.md): Associez les identités à partir de sources de données disparates lors de leur ingestion dans Platform.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Créez des profils consommateurs unifiés à l’aide de données provenant de plusieurs sources.

## Limites du modèle de données

Les tableaux ci-dessous fournissent des conseils sur les barrières de sécurité pour les limites statiques et les règles de validation à prendre en compte pour les espaces de noms d’identité.

### Limites statiques

Le tableau suivant décrit les limites statiques appliquées aux données d’identité.

| Barrière de sécurité | Limite | Notes |
| --- | --- | --- |
| Nombre d’identités dans un graphique | 150 | La limite est appliquée au niveau de l’environnement de test. Le graphique d’identités ne sera pas mis à jour une fois la limite atteinte. |
| Nombre d’identités dans un enregistrement XDM | 20 | Le nombre minimum d’enregistrements XDM requis est de deux. |
| Nombre d’espaces de noms personnalisés | Aucun | Il n’existe aucune limite au nombre d’espaces de noms personnalisés que vous pouvez créer. |
| Nombre de graphiques | Aucun | Il n’existe aucune limite au nombre de graphiques d’identités que vous pouvez créer. |
| Nombre de caractères pour un nom d’affichage d’espace de noms ou un symbole d’identité | Aucun | Le nombre de caractères du nom d’affichage ou du symbole d’identité d’un espace de noms est illimité. |

### Validation de la valeur d’identité

Le tableau suivant décrit les règles existantes que vous devez suivre pour garantir une validation réussie de votre valeur d’identité.

| Espace de noms | Règle de validation | Comportement du système en cas de violation de la règle |
| --- | --- | --- |
| ECID | <ul><li>La valeur d’identité d’un ECID doit comporter exactement 38 caractères.</li><li>La valeur d’identité d’un ECID ne doit être composée que de nombres.</li></ul> | <ul><li>Si la valeur d’identité d’ECID ne comporte pas exactement 38 caractères, l’enregistrement est ignoré.</li><li>Si la valeur d’identité d’ECID contient des caractères non numériques, l’enregistrement est ignoré.</li></ul> |
| Non ECID | La valeur d’identité ne peut pas dépasser 1 024 caractères. | Si la valeur d’identité dépasse 1 024 caractères, l’enregistrement est ignoré. |

## Étapes suivantes

Consultez la documentation suivante pour plus d’informations sur [!DNL Identity Service]:

* [Présentation de [!DNL Identity Service]](home.md)
* [Graphique d’identités observateur](ui/identity-graph-viewer.md)
