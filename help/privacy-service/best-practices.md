---
title: Bonnes pratiques relatives à Privacy Service
description: Découvrez comment réduire le temps de traitement et les coûts supportés par votre organisation lors de l’exécution des demandes d’accès à des informations personnelles en suivant ces directives d’utilisation optimale.
exl-id: 1333d6c6-5ca0-41c1-9f9e-aa2a5a8b8a9c
TQID: https://experienceleague.adobe.com/s12W18PJYq1-PziBxK1tNe65yiaiGEUhPiDF-dQShdg
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
subfeature_v2:
  - id: b3ddd7c3-4e07-4269-8660-8dd1e8139d74
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 1275
ht-degree: 0%

---

# Bonnes pratiques relatives à Privacy Service

Utilisez Privacy Service pour automatiser la conformité aux réglementations de confidentialité des données lorsque les clients souhaitent accéder à leurs données personnelles ou les supprimer de vos banques de données. Pour répondre à ces besoins professionnels en constante évolution, Privacy Service propose une API RESTful ainsi qu’une interface utilisateur permettant d’envoyer des demandes d’accès et de suppression de données client dans les applications Adobe Experience Cloud.

Ce guide décrit les bonnes pratiques pour traiter efficacement les demandes d’accès à des informations personnelles et optimiser les temps de réponse d’achèvement lors de la gestion des demandes de données client.

## Prise en main {#getting-started}

Ce guide nécessite une compréhension pratique de [&#128279;](./home.md) et de la manière dont il permet de gérer l’accès et de supprimer les requêtes de vos titulaires de données (clients) dans les applications Adobe Experience Cloud. Il est également recommandé de lire le guide sur la [création d’une requête de tâche de confidentialité dans l’interface utilisateur](./ui/user-guide.md#create-a-new-privacy-job-request) ou [l’API](./api/overview.md) et de comprendre comment effectuer ces opérations par programmation.

## Conditions préalables {#prerequisites}

L’accès à Adobe Experience Platform Privacy Service est contrôlé par des autorisations granulaires en fonction du rôle dans Adobe Admin Console. Vous avez besoin des autorisations appropriées dans un profil de produit pour utiliser des fonctionnalités spécifiques dans l’interface utilisateur et l’API Privacy Service. Contactez votre administrateur système si vous avez besoin d’autorisations supplémentaires.

Pour plus d’informations, les administrateurs peuvent consulter le guide sur la [gestion des autorisations pour Privacy Service](./permissions.md).

## Directives de création de tâches relatives à la confidentialité {#creation-guidelines}

Pour rationaliser le traitement de vos demandes et améliorer les temps de réponse, tenez compte des instructions suivantes lors de la création de tâches relatives à la confidentialité. Cela s’applique à la fois aux méthodes de l’API et de l’interface utilisateur.

1. **Maximiser les titulaires de données par demande :** inclure autant de titulaires de données que possible, jusqu’à 1 000 par demande.
2. **ID de groupe pour plus d’efficacité :** regroupez plusieurs ID pour un seul titulaire de données (jusqu’à neuf) dans chaque demande. Les **ID peuvent provenir de différents services Adobe dans la même requête**.
3. **Combiner les tâches d’accès et de suppression :** incluez les types de tâches « d’accès » et « de suppression » dans une seule demande, si le titulaire de données l’exige.
4. **Inclure uniquement les produits nécessaires :** inclure uniquement les produits requis ou sous licence. Des produits supplémentaires peuvent allonger le temps de traitement et augmenter les coûts.

## Surveillance du statut des tâches de confidentialité {#monitor-status}

Pour surveiller efficacement les tâches de confidentialité et vérifier leur statut, Privacy Service propose trois méthodes. Les méthodes disponibles sont répertoriées ci-dessous dans l’ordre de surveillance de l’efficacité et de la productivité. Chaque méthode comprend des directives relatives aux bonnes pratiques pour améliorer votre expérience, suivies d’un exemple de scénario idéal qui combine toutes les approches.

### Recevoir des notifications en temps réel {#real-time-notifications}

**Événements I/O** permet une surveillance de l’état en temps quasi réel par le biais d’événements d’état. Il s’agit de la méthode la plus efficace, car elle évite d’avoir à mettre en œuvre des mécanismes d’interrogation et d’entraîner un trafic d’API supplémentaire.

**Recommandations :**

- **Configuration du Webhook :** configurez les webhooks pour recevoir des notifications push lorsque le statut des tâches envoyées change. Cela facilite la surveillance en temps réel.
- **Notifications :** utilisez les notifications au niveau des tâches et des produits pour surveiller la progression des requêtes.

Consultez la documentation sur l’[abonnement aux événements Privacy Service](./privacy-events.md) pour obtenir des instructions sur la configuration d’un enregistrement d’événement pour les notifications Privacy Service et sur la manière d’interpréter les payloads des notifications.

### Récupération de toutes les tâches en fonction de filtres {#retrieve-filtered-responses-for-all-jobs}

Pour récupérer toutes vos données de tâche de confidentialité en fonction de filtres spécifiés, **envoyez une requête GET au point d’entrée `/jobs`**. Cet appel d’API est utile pour fournir une vue de haut niveau de l’état actuel de la tâche pour de grands ensembles d’identifiants de tâche avec une seule requête. Il ne manque pas de réponses détaillées sur les produits, mais elles peuvent être trouvées à l’aide du point d’entrée [&#128279;](#retrieve-detailed-responses-for-specific-jobs).`/jobs/{jobID}`

Une requête GET au point d’entrée `/jobs` est plus adaptée pour collecter ou comparer les données de statut d’un jeu volumineux d’identifiants de tâche. Elle n’est cependant **pas** prévue pour les activités de type interrogation standard.

**Recommandations :**

- **Paramètres de requête :** utilisez des filtres spécifiques pour affiner vos résultats, par exemple : plages de données, types de réglementation et statut (traitement, terminé, etc.).

Vous pouvez afficher une liste de toutes les tâches actuelles liées à la confidentialité dans votre organisation via l’interface utilisateur de Privacy Service. Consultez la [gestion des tâches de confidentialité dans la documentation de l’interface utilisateur](./ui/user-guide.md#job-requests) pour plus d’informations sur la manière de filtrer la liste des demandes de tâche. Vous pouvez également consulter la documentation sur l’[utilisation du point d’entrée /job dans l’API Privacy Service](./api/privacy-jobs.md).

La documentation de l’API Privacy Service contient des détails sur [les filtres de paramètres de requête disponibles](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs).

### Récupération de réponses détaillées pour une seule tâche {#retrieve-detailed-responses-for-specific-jobs}

Pour récupérer des réponses détaillées pour une seule tâche, **envoyez une requête GET au point d’entrée /jobs/{jobID}**. Cette méthode est destinée à une collecte d’informations plus approfondie, comme les réponses spécifiques à un produit et les messages de succès. Un appel à ce point d’entrée est le meilleur moyen de voir quels produits ont répondu et lesquels sont toujours en attente, bien qu’il ne soit **pas** destiné à une activité d’interrogation régulière.

Consultez la documentation sur le point d’entrée `/jobs/{JOB_ID}` pour plus d’informations sur [comment vérifier le statut d’une tâche spécifique](./api/privacy-jobs.md#check-status).

### Exemple de scénario idéal {#ideal-scenario}

Utilisez un webhook pour que le système puisse automatiquement mettre à jour les enregistrements et fournir des rapports ou des alertes lorsque les groupes des identifiants d’une requête sont terminés. Si des tâches sont toujours en attente, le système récupère ces statuts de tâche avec une requête GET au point d’entrée de `/jobs` de l’API Privacy Service et fournit une mise à jour de haut niveau de la liste.

Si une tâche spécifique est toujours en attente ou a renvoyé une erreur, vous pouvez récupérer la réponse détaillée avec une requête GET au point d’entrée `/job/{jobId}`.

## Données de demande d’accès {#access-request-data}

Lorsque des informations sur les titulaires de données sont demandées, chaque service renvoie des données dans un format compatible avec la manière dont ils stockent et utilisent ces données. Une fois que tous les services ont terminé la requête, une URL de fichier d’archive .ZIP est fournie dans les détails de la tâche pour permettre le téléchargement de ces données. Consultez le guide de dépannage pour plus d’informations sur [&#x200B; comment télécharger les résultats des tâches de confidentialité &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=en#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F).

Les principaux points à noter concernant la gestion de l&#39;archive de données sont les suivants :

- Tous les fichiers d’archive sont supprimés des serveurs Experience Platform au bout de 30 jours. Vous ne pouvez pas interroger les données client qui ont plus de 30 jours.
- La structure du fichier d’archive comprend des dossiers pour chaque produit inclus dans la demande et les fichiers de données qu’il contient. Les fichiers ou dossiers d&#39;archives peuvent être vides si aucune donnée n&#39;a été trouvée pour l&#39;ID spécifié.
- Les données des tâches créées précédemment ne sont accessibles que pendant 30 jours après la date d’achèvement. Passé ce délai, les données sont supprimées du système et une nouvelle demande doit être envoyée.

**Recommandations :**

- **Protéger les archives de données :** l’URL et le fichier .ZIP doivent être protégés, car ils peuvent contenir des informations d’identification personnelle (PII) pour le titulaire de données.

## Considérations techniques {#technical-considerations}

Certaines considérations techniques doivent être prises en compte lors de l’exécution des requêtes Privacy Service :

- **Période de conservation des données :** la période d’analyse maximale est de 60 jours pour tout groupe de tâches et la période maximale pour une requête est de 30 jours (les dates de début et de fin).
- **Délai d’expiration de la passerelle :** gardez à l’esprit que votre requête peut être ignorée de la passerelle si elle dépasse 60 secondes.
- **Gestion des erreurs :** révisez minutieusement les messages d’erreur et renvoyez les demandes, le cas échéant. Privacy Service ne retraite pas automatiquement les tâches suite à une erreur.
- **Comprendre les erreurs HTTP 429 :** familiarisez-vous avec les messages d’erreur HTTP 429 et les étapes nécessaires pour atténuer les problèmes. Les erreurs HTTP 429 sont le résultat de « Too many requests ». Voir la section [Messages d’erreur courants](./troubleshooting-guide.md#common-error-messages) du guide de dépannage pour plus d’informations sur la façon de résoudre le problème.

## Étapes suivantes

En lisant ce document, vous disposez désormais des connaissances et des pratiques nécessaires à une utilisation efficace et efficiente de Privacy Service. Ensuite, consultez le [guide de dépannage](./troubleshooting-guide.md) pour obtenir des réponses aux questions fréquentes sur Privacy Service et des informations sur les erreurs courantes rencontrées dans l’API.
