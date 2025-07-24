---
title: Surveiller l’ingestion des profils en flux continu
description: Découvrez comment utiliser le tableau de bord de surveillance pour surveiller l’ingestion des profils de diffusion en continu
hide: true
hidefromtoc: true
source-git-commit: 2f78b70761ef676fe4ab61b89b6cbb261c99e9ca
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 3%

---

# Surveiller l’ingestion des profils en flux continu

Vous pouvez utiliser le tableau de bord de surveillance dans l’interface utilisateur de Adobe Experience Platform pour effectuer la surveillance en temps réel des taux d’ingestion des profils de diffusion en continu dans votre entreprise. Utilisez cette fonctionnalité pour une meilleure transparence des mesures de débit, de latence et de qualité des données entourant vos données de diffusion en continu. De plus, vous pouvez utiliser cette fonctionnalité pour des alertes proactives et la récupération d’informations exploitables afin d’identifier les violations de capacité potentielles et les problèmes d’ingestion de données.

Lisez le guide suivant pour savoir comment utiliser le tableau de bord de surveillance pour surveiller les taux et les mesures des tâches d’ingestion de profil en flux continu dans votre organisation.

## Présentation du tableau de bord d’ingestion des profils de streaming

Vous pouvez utiliser trois catégories de mesures différentes dans le tableau de bord de surveillance pour l’ingestion de profils en flux continu : [!UICONTROL Débit], [!UICONTROL Ingestion] et [!UICONTROL Latence].

* **Débit** : sélectionnez **[!UICONTROL Débit]** pour afficher des informations sur la quantité de données qu’Experience Platform traite selon une période configurée. Consultez cette mesure pour évaluer l’efficacité et la capacité de votre système.
   * **Capacité** : quantité maximale de données que votre sandbox peut traiter dans des conditions définies.
   * **Débit des requêtes** : taux auquel les événements sont reçus par le système d’ingestion, mesuré en événements par seconde.
   * **Débit de traitement** : taux auquel le système ingère et traite avec succès les payloads d’événement entrant, mesuré en événements par seconde.
* **Ingestion** : sélectionnez [!UICONTROL Ingestion] pour afficher des informations sur les tâches d’ingestion dans votre sandbox. Ces tâches d’ingestion sont mesurées selon trois mesures différentes :
   * **Enregistrements créés** : quantité totale d’enregistrements créés au cours d’une période donnée. Cette mesure représente les processus d’ingestion de données réussis dans votre sandbox.
   * **Enregistrements en échec** : nombre total d’enregistrements qui n’ont pas été ingérés en raison d’erreurs.
   * **Enregistrements supprimés** : nombre total d’enregistrements supprimés en raison d’une violation des limites de capacité.
* **Latence** : sélectionnez [!UICONTROL Latence] pour afficher des informations sur le temps nécessaire à Experience Platform pour répondre à une demande ou effectuer une opération au cours d’une période donnée.

## Surveillance des mesures pour l’ingestion de profils en flux continu {#streaming-profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile"
>title="Surveiller l’ingestion des profils en flux continu"
>abstract="Le tableau de bord de surveillance des profils de diffusion en continu affiche des informations sur le débit, les taux d’ingestion et la latence. Utilisez ce tableau de bord pour afficher, comprendre et analyser les mesures de traitement des données. de vos profils de streaming dans Experience Platform."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_request_throughput"
>title="Débit des demandes"
>abstract="Cette mesure représente le nombre d’événements entrant dans le système d’ingestion par seconde."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_processing_throughput"
>title="Débit de traitement"
>abstract="Cette mesure représente le nombre d’événements ingérés avec succès par le système chaque seconde."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_p95_ingestion_latency"
>title="Latence d’ingestion P95"
>abstract="Cette mesure mesure mesure la latence du 95e centile entre le moment où un événement arrive dans Experience Platform et celui où il est ingéré avec succès dans la banque de profils."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_max_throughput"
>title="Débit maximal"
>abstract="Cette mesure représente le nombre maximal de requêtes entrantes par seconde entrant dans l’ingestion de profil en flux continu."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_ingested"
>title="Enregistrements ingérés"
>abstract="Cette mesure représente le nombre total d’enregistrements ingérés dans la banque de profils au cours d’une période configurée."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_failed"
>title="Échec des enregistrements"
>abstract="Cette mesure représente le nombre total d’enregistrements qui ont échoué lors de l’ingestion dans la banque de profils, dans un intervalle de temps configuré, en raison d’erreurs."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_skipped"
>title="Enregistrements ignorés"
>abstract="Cette mesure représente le nombre total d’enregistrements supprimés pendant une période configurée, en raison de violations de la configuration ou de la capacité."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_error_details"
>title="Détails des erreurs"
>abstract="Cette mesure représente le nombre d’événements ayant échoué en raison d’erreurs."
>text="Learn more in documentation"

| Mesure | Description | Dimensions | Fréquence de mesure |
| --- | --- | --- | --- |
| Débit des demandes | Cette mesure représente le nombre d’événements entrant dans le système d’ingestion par seconde. | Sandbox/flux de données | Surveillance en temps réel avec une actualisation des données toutes les 60 secondes. |
| Débit de traitement | Cette mesure représente le nombre d’événements ingérés avec succès par le système chaque seconde. | Sandbox/flux de données | Surveillance en temps réel avec une actualisation des données toutes les 60 secondes. |
| Latence d’ingestion P95 | Cette mesure mesure mesure la latence du 95e centile entre le moment où un événement arrive dans Experience Platform et celui où il est ingéré avec succès dans la banque de profils. | Sandbox/flux de données | Surveillance en temps réel avec une actualisation des données toutes les 60 secondes. |
| Débit maximal |
| Enregistrements ingérés | Cette mesure représente le nombre total d’enregistrements ingérés dans la banque de profils au cours d’une période configurée. | <ul><li>Sandbox/flux de données</li><li>Exécution du flux de données</li></ul> | <ul><li>Sandbox/flux de données : surveillance en temps réel avec une actualisation des données toutes les 60 secondes.</li><li>Exécution du flux de données : regroupée en 15 minutes.</li></ul> |
| Échec des enregistrements | Cette mesure représente le nombre total d’enregistrements qui ont échoué lors de l’ingestion dans la banque de profils, dans un intervalle de temps configuré, en raison d’erreurs. | <ul><li>Sandbox/flux de données</li><li>Exécution du flux de données</li></ul> | <ul><li>Sandbox/flux de données : surveillance en temps réel avec une actualisation des données toutes les 60 secondes.</li><li>Exécution du flux de données : regroupée en 15 minutes.</li></ul> |
| Enregistrements ignorés | Cette mesure représente le nombre total d’enregistrements supprimés pendant une période configurée, en raison de violations de la configuration ou de la capacité. | <ul><li>Sandbox/flux de données</li><li>Exécution du flux de données</li></ul> | <ul><li>Sandbox/flux de données : surveillance en temps réel avec une actualisation des données toutes les 60 secondes.</li><li>Exécution du flux de données : regroupée en 15 minutes.</li></ul> |
| Détails des erreurs | Cette mesure représente le nombre d’événements ayant échoué en raison d’erreurs. | Exécution du flux de données | Regroupé dans une fenêtre horaire. |

{style="table-layout:auto"}