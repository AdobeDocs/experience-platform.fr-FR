---
solution: Experience Platform
title: Création d’une définition de segment à l’aide de l’API Segmentation Service
type: Tutorial
description: Suivez ce tutoriel pour découvrir comment développer, tester, prévisualiser et enregistrer une définition de segment à l’aide de l’API Adobe Experience Platform Segmentation Service.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 44%

---

# Création d’une définition de segment à l’aide de l’API Segmentation Service

Ce document fournit un tutoriel pour le développement, le test, la prévisualisation et l’enregistrement d’une définition de segment à l’aide du [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Pour plus d’informations sur la création de définitions de segment à l’aide de l’interface utilisateur, voir [Guide du créateur de segments](../ui/segment-builder.md).

## Commencer

Ce tutoriel nécessite une compréhension pratique des différentes [!DNL Adobe Experience Platform] services impliqués dans la création de définitions de segment. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): vous permet de créer des audiences à l’aide de définitions de segment ou d’autres sources externes à partir de données Real-time Customer Profile.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client. Pour utiliser au mieux la segmentation, veillez à ce que vos données soient ingérées en tant que profils et événements en fonction des [bonnes pratiques pour la modélisation des données](../../xdm/schema/best-practices.md).

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à la fonction [!DNL Platform] API.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) dans le guide de dépannage [!DNL Experience Platform].

### Collecte des valeurs des en-têtes requis

Pour lancer des appels aux API [!DNL Platform], vous devez d’abord suivre le [tutoriel d’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API [!DNL Experience Platform], comme indiqué ci-dessous :

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans [!DNL Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

Toutes les requêtes contenant un payload (POST, PUT, PATCH) requièrent un en-tête supplémentaire :

- Content-Type: application/json

## Développement d’une définition de segment

La première étape de la segmentation consiste à définir une définition de segment. Une définition de segment est un objet qui contient une requête écrite dans [!DNL Profile Query Language] (PQL). Cet objet est également appelé prédicat PQL. Les prédicats PQL définissent les règles de la définition de segment en fonction des conditions liées aux données d’enregistrement ou de série temporelle que vous fournissez. [!DNL Real-Time Customer Profile]. Pour plus d’informations sur l’écriture de requêtes PQL, reportez-vous au [guide de PQL](../pql/overview.md).

Vous pouvez créer une définition de segment en adressant une requête de POST à la fonction `/segment/definitions` du point de terminaison [!DNL Segmentation] API. L’exemple suivant décrit comment formater une requête de définition, y compris les informations requises pour qu’une définition de segment soit définie avec succès.

Pour obtenir une explication détaillée sur la définition d’une définition de segment, veuillez lire le [guide de développement de la définition de segment](../api/segment-definitions.md#create).

## Estimation et prévisualisation d’une audience {#estimate-and-preview-an-audience}

Lorsque vous développez votre définition de segment, vous pouvez utiliser les outils d’estimation et de prévisualisation dans la [!DNL Real-Time Customer Profile] pour afficher des informations sommaires afin de vous assurer que vous isolez l’audience attendue. Les estimations fournissent des informations statistiques sur une définition de segment telles que la taille prévue de l’audience et l’intervalle de confiance. Les prévisualisations fournissent des listes paginées des profils admissibles pour une définition de segment, ce qui vous permet de comparer les résultats avec vos attentes.

En estimant et en prévisualisant votre audience, vous pouvez tester et optimiser vos prédicats PQL jusqu’à ce qu’ils produisent un résultat souhaitable. Ils peuvent alors être utilisés dans une définition de segment mise à jour.

Deux étapes sont nécessaires pour prévisualiser ou obtenir une estimation de votre définition de segment :

1. [Création d’une tâche de prévisualisation](#create-a-preview-job)
2. [Afficher l’estimation ou la prévisualisation](#view-an-estimate-or-preview) à l’aide de l’identifiant de la tâche de prévisualisation

### Comment sont générées les estimations

Les données activées pour Real-Time Customer Profile étant ingérées dans Platform, elles sont stockées dans la banque de données Profile. Lorsque l’ingestion d’enregistrements dans la banque de profils augmente ou diminue le nombre total de profils de plus de 5 %, une tâche d’échantillonnage est déclenchée pour mettre à jour le nombre. Si le nombre de profils ne varie pas de plus de 5 %, la tâche d’échantillonnage s’exécute automatiquement toutes les semaines.

La manière dont l’échantillon est déclenché dépend du type d’ingestion utilisé :

- Pour les workflows de données en flux continu, une vérification est effectuée sur une base horaire afin de déterminer si le seuil de 5 % d’augmentation ou de diminution a été atteint. Si ce seuil a été atteint, un exemple de tâche est automatiquement déclenché pour mettre à jour le décompte.
- Pour l’ingestion par lots, dans les 15 minutes suivant l’ingestion réussie d’un lot dans la banque de profils, si le seuil de 5 % d’augmentation ou de diminution est atteint, une tâche est exécutée pour mettre à jour le nombre. À l’aide de l’API Profile, vous pouvez prévisualiser le dernier exemple de tâche réussi, ainsi que répertorier la distribution du profil par jeu de données et par espace de noms d’identité.

La taille de l’échantillon dépend du nombre total d’entités dans votre banque de profils. Ces tailles d’échantillon sont représentées dans le tableau suivant :

| Entités dans la banque de profils | Taille de l’échantillon |
| ------------------------- | ----------- |
| Moins de 1 million | Jeu de données complet |
| 1 à 20 millions | 1 million |
| Plus de 20 millions | 5 % du total |

Les estimations durent généralement entre 10 et 15 secondes. L’estimation est d’abord approximative, et se précise au fur et à mesure de la lecture d’un plus grand nombre d’enregistrements.

### Création d’une tâche de prévisualisation

Vous pouvez créer une nouvelle tâche de prévisualisation en exécutant une requête POST sur le point d’entrée `/preview`.

Vous trouverez des instructions détaillées sur la création d’une tâche de prévisualisation dans la section [guide des prévisualisations et des points de fin d’estimation](../api/previews-and-estimates.md#create-preview).

### Affichage d’une estimation ou d’une prévisualisation

Les processus d’estimation et de prévisualisation sont exécutés de manière asynchrone, car le temps de traitement peut différer d’une requête à une autre. Une fois qu’une requête a été lancée, vous pouvez utiliser des appels API pour récupérer (GET) l’état actuel de l’estimation ou de la prévisualisation au fur et à mesure de sa progression.

En utilisant la variable [!DNL Segmentation Service] API, vous pouvez rechercher l’état actuel d’une tâche de prévisualisation par son identifiant. Si l’état affiche « RESULT_READY », vous pouvez consulter les résultats. Pour rechercher l’état actuel d’une tâche de prévisualisation, veuillez lire la section sur [récupération d’une section de tâche de prévisualisation](../api/previews-and-estimates.md#get-preview) dans le guide de points de fin previews and estimated . Pour rechercher l’état actuel d’une tâche d’estimation, veuillez lire la section sur [récupération d’une tâche d’estimation](../api/previews-and-estimates.md#get-estimate) dans le guide de points de fin previews and estimated .


## Étapes suivantes

Une fois que vous avez développé, testé et enregistré votre définition de segment, vous pouvez créer une tâche de segmentation pour créer une audience à l’aide de la fonction [!DNL Segmentation Service] API. Consultez le tutoriel portant sur l’[évaluation et l’accès aux résultats des segments](./evaluate-a-segment.md) pour obtenir des instructions détaillées sur la manière d’y parvenir.
