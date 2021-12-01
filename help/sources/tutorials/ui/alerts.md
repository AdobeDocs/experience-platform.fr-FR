---
keywords: Experience Platform;accueil;rubriques les plus consultées ; alertes
description: Vous pouvez vous abonner à des alertes lors de la création d’un flux de données pour recevoir des messages d’alerte concernant l’état, la réussite ou l’échec de votre exécution de flux.
title: Abonnement à des alertes contextuelles dans l’interface utilisateur
hide: true
hidefromtoc: true
source-git-commit: a81d21f615206e644044c2f0f546a458d1aebbf3
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 24%

---

# Abonnez-vous pour alerter les messages afin de surveiller les flux de données de vos sources dans l’interface utilisateur

Adobe Experience Platform vous permet de vous abonner à des alertes basées sur des événements concernant les activités Adobe Experience Platform. Les alertes réduisent ou éliminent la nécessité d’interroger l’[[!DNL Observability Insights] API](../../../observability/api/overview.md) afin de vérifier si une tâche est terminée, si un certain jalon a été atteint dans un processus ou si des erreurs se sont produites.

Vous pouvez vous abonner à des alertes lors de la création d’un flux de données pour recevoir des messages d’alerte concernant l’état, la réussite ou l’échec de votre exécution de flux.

Ce document décrit les étapes à suivre pour s’abonner aux alertes et recevoir des messages d’alerte pour les exécutions de flux.

## Prise en main

Ce document nécessite une compréhension pratique des composants suivants de Adobe Experience Platform :

* [Sources](../../home.md): [!DNL Experience Platform] permet d’ingérer des données provenant de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide de [!DNL Platform] services.
* [Observability vous permet de surveiller les activités de Platform en utilisant des mesures statistiques et des notifications dʼévénement.](../../../observability/home.md)[!DNL Observability Insights]
   * [Alertes](../../../observability/alerts/overview.md): Lorsqu’un certain ensemble de conditions de vos opérations Platform est atteint (par exemple, un problème potentiel lorsque le système enfreint un seuil), Platform peut envoyer des messages d’alerte à tous les utilisateurs de votre organisation qui se sont abonnés à eux.

## Abonnement aux alertes dans l’interface utilisateur {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="Abonnement aux alertes de sources"
>abstract="Les alertes vous permettent de recevoir des notifications en fonction de l’état des flux de données de vos sources. Vous pouvez définir des notifications d’alerte pour obtenir des mises à jour si votre flux de données a démarré, a réussi, a échoué ou n’a ingéré aucune donnée."
>text="Learn more in documentation"
