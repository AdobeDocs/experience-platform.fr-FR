---
title: Guide de mise en oeuvre d’Identity Service
description: Découvrez comment les données fournies à Adobe Experience Platform sont traitées avant d’être utilisées par Identity Service pour créer des graphiques d’identités.
exl-id: c961bbf6-6b46-470f-a671-93ff4173876c
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 64%

---

# Guide de mise en oeuvre d’Identity Service

Ce document fournit des informations sur la manière dont les données fournies à Adobe Experience Platform sont traitées avant d’être utilisées par Identity Service pour créer un graphique d’identités pour un client donné.

## Choix des champs d’identité

En fonction de la stratégie de collecte de données de votre entreprise, les champs de données que vous désignez comme identités déterminent les données qui sont incluses dans votre carte d’identité. Pour tirer le meilleur parti des identités de clients Experience Platform et les plus complètes possible, vous devez télécharger des données en ligne et hors ligne.

* Les données en ligne décrivent la présence et le comportement en ligne, comme les noms d’utilisateur et les adresses électroniques.

* Les données hors ligne ne sont pas directement liées à la présence en ligne, comme les identifiants des systèmes CRM. Ce type de données renforce vos identités et favorise la cohésion des données entre vos systèmes disparates.

## Création d’espaces de noms d’identité supplémentaires

Bien qu’Experience Platform offre de nombreux espaces de noms standard, vous devrez peut-être créer des espaces de noms supplémentaires pour classer correctement vos identités. Pour plus d’informations, consultez le guide sur la [création d’espaces de noms personnalisés pour votre organisation](./features/namespaces.md).

>[!NOTE]
>
>Les espaces de noms d’identité sont des qualificateurs d’identités. Par conséquent, une fois qu’un espace de noms a été créé, il ne peut pas être supprimé.

## Introduction de données d’identité dans le modèle de données d’expérience (XDM)

En tant que cadre normalisé selon lequel l’Experience Platform organise les données client, le modèle de données d’expérience (XDM) permet de partager et de comprendre les données entre les Experience Platform et les autres services interagissant avec l’Experience Platform. Pour plus d’informations, consultez la [présentation du système XDM](../xdm/home.md).

Les schémas d’enregistrement et de série temporelle permettent d’inclure des données d’identité. À mesure que les données sont ingérées, le graphique d’identités crée de nouvelles relations entre les fragments de données provenant de différents espaces de noms s’il s’avère qu’ils partagent des données d’identité communes.

## Étiquetage des champs XDM comme identité

Les champs de type `string` dans les schémas qui mettent en œuvre des classes XDM d’enregistrement ou de série temporelle peuvent être qualifiés de champs d’identité. Par conséquent, toutes les données ingérées dans ces champs seraient considérées comme des données d’identité.

Les champs d’identité permettent également de lier des identités si elles partagent des données PII communes.
Par exemple, en désignant les champs de numéro de téléphone comme des champs d’identité, le service d’identités crée automatiquement un graphique des relations avec les autres personnes qui utilisent le même numéro de téléphone.

>[!NOTE]
>
>* Les champs de type tableau et mappage ne sont pas pris en charge et ne peuvent pas être marqués et libellés comme des champs dʼidentité.
>* L’espace de noms des identités résultantes est fourni au moment où le champ est libellé.

Pour plus d’informations, consultez le guide sur la [définition des champs d’identité dans l’interface utilisateur](../xdm/ui/fields/identity.md).

## Configuration d’un jeu de données pour le service d’identités

Pendant le processus d’ingestion par flux, le service d’identités extrait automatiquement les données d’identité des données d’enregistrement et de série temporelle. Cependant, les données doivent être activées pour le service d’identités avant de pouvoir être ingérées. Pour plus d’informations, consultez le tutoriel sur la [configuration d’un jeu de données pour Real-Time Customer Profile et Identity Service à l’aide des API](../profile/tutorials/dataset-configuration.md) .

## Ingestion des données dans le service d’identités

Identity Service consomme des données conformes à XDM envoyées à l’Experience Platform par [ingestion par lots](../ingestion/batch-ingestion/overview.md) ou [ingestion par flux](../ingestion/streaming-ingestion/overview.md).

La vidéo suivante est destinée à vous aider à comprendre le service dʼidentités. Cette vidéo explique comment libeller les champs de données comme des identités, ingérer les données dʼidentité, puis vérifier que les données ont été enregistrées dans le graphique Privé du service d’identités d’Adobe Experience Platform.

>[!WARNING]
>
>L’interface utilisateur Experience Platform affichée dans la vidéo suivante est obsolète. Reportez-vous à la documentation pour obtenir les dernières captures dʼécran et fonctionnalités de lʼinterface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)
