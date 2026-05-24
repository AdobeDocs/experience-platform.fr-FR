---
title: Surveiller les audiences en flux continu
description: Découvrez comment utiliser le tableau de bord de surveillance pour surveiller les audiences évaluées à l’aide de la segmentation en flux continu
hide: true
exl-id: b47325fb-7768-4bc0-92d2-5541729e636d
TQID: https://experienceleague.adobe.com/ksp5cu-Y0PB7DOQZcDIzapoCtpGc1HXyMWQzP2l6Nbs
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914
subfeature_v2: id: b784da9a-7978-4766-bf1f-5ab2b23d894aid: d1823595-9241-4128-8a33-e4ac3bf08773id: e5ae22e3-a3b0-46ed-804f-9abf1bbe3e74
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 370
ht-degree: 19%

---

# Surveiller les audiences en flux continu

intro blurb

## Commencer

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Flux de données](../home.md) : les flux de données représentent des tâches de données qui transfèrent des informations dans Experience Platform. Ils sont configurés sur différents services pour faciliter le déplacement des données des connecteurs sources vers les jeux de données cibles, ainsi que vers le service d’identités, le profil client en temps réel et les destinations.
* [Segmentation Service](../../segmentation/home.md) :
* [Capacités](../../landing/license-usage-and-guardrails/capacity.md) : dans Experience Platform, les capacités vous permettent de savoir si votre organisation a dépassé l’un de vos mécanismes de sécurisation et vous donnent des informations sur la manière de résoudre ces problèmes.

## Surveiller des mesures pour les audiences en streaming {#streaming-audience-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_evaluation_rate"
>title="Taux d’évaluation"
>abstract="Cette mesure représente le nombre d’enregistrements évalués par seconde."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_p95_latency"
>title="Latence d’ingestion P95"
>abstract="Cette mesure mesure la latence du 95e centile d’un événement arrivant dans Adobe Experience Platform pour une évaluation réussie dans l’audience."
>text="Learn more in documentation"

Le tableau suivant fournit des informations plus détaillées sur les mesures utilisées pour les audiences en flux continu.

| Mesure | Description | Dimensions |
| ------ | ----------- | ---------- |
| Taux d’évaluation | Nombre d’évaluations d’audience traitées par seconde. | Sandbox, Jeu de données |
| Latence d’ingestion P95 | 95e centile de latence de l’événement réussi à arriver dans l’audience. | Sandbox, Jeu de données |
| Enregistrements reçus | Nombre total d’enregistrements reçus de l’ingestion en flux continu pour la segmentation en flux continu pendant la fenêtre temporelle sélectionnée. | Jeu de données |
| Enregistrements évalués | Nombre total d’enregistrements **évalués avec succès** à l’aide de la segmentation en flux continu pendant la fenêtre temporelle sélectionnée. | Jeu de données |
| Enregistrements ayant échoué | Nombre total d’enregistrements dont l’évaluation **a échoué** dans la segmentation en flux continu en raison d’erreurs pendant la période sélectionnée. | Jeu de données, exécution de flux |
| Enregistrements ignorés | Nombre total d’enregistrements qui **ont été ignorés** évaluation dans la segmentation en flux continu en raison d’erreurs pendant la fenêtre temporelle sélectionnée. | Jeu de données, exécution de flux |
| Profils qualifiés | Nombre de profils qualifiés pour l’audience pendant la fenêtre temporelle sélectionnée. | Sandbox, Audience |
| Profils disqualifiés | Nombre de profils qui ont été disqualifiés de l’audience pendant la période sélectionnée. | Sandbox, Audience |

{style="table-layout:auto"}

## Utiliser le tableau de bord de surveillance pour les audiences en flux continu {#monitoring-dashboard}

Pour accéder au tableau de bord de surveillance des audiences de diffusion en continu, accédez à l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Monitoring]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Streaming end-to-end]**.

IMAGE

La carte de mesure **[!UICONTROL Audiences]** se trouve en haut du tableau de bord. Cette option affiche des informations sur le **Taux d’évaluation** pour les audiences.
