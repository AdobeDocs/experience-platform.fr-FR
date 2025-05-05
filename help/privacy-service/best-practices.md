---
title: Bonnes pratiques pour les Privacy Service
description: Découvrez comment réduire le temps de traitement et les coûts générés pour votre entreprise lors de l’exécution de demandes d’accès à des informations personnelles en suivant ces instructions d’utilisation optimales.
exl-id: 1333d6c6-5ca0-41c1-9f9e-aa2a5a8b8a9c
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1234'
ht-degree: 0%

---

# Bonnes pratiques pour les Privacy Service

Utilisez Privacy Service pour automatiser la conformité aux réglementations de confidentialité des données lorsque les clients souhaitent accéder à leurs données personnelles ou les supprimer de vos entrepôts de données. Pour répondre à ces besoins commerciaux en évolution, Privacy Service propose une API RESTful et une interface utilisateur pour envoyer des demandes d’accès et de suppression de données client dans les applications Adobe Experience Cloud.

Ce guide décrit les bonnes pratiques pour traiter efficacement les demandes d’accès à des informations personnelles et optimiser les temps de réponse d’achèvement lors de la gestion des demandes de données client.

## Commencer {#getting-started}

Ce guide nécessite une compréhension pratique de [Privacy Service](./home.md) et de la manière dont il vous permet de gérer les requêtes d’accès et de suppression de vos sujets des données (clients) dans les applications Adobe Experience Cloud. Nous vous recommandons également de lire le guide sur la [création d’une requête de tâche de confidentialité dans l’interface utilisateur](./ui/user-guide.md#create-a-new-privacy-job-request) ou [l’API](./api/overview.md) et de comprendre comment effectuer ces opérations par programmation.

## Conditions préalables {#prerequisites}

L’accès à Adobe Experience Platform Privacy Service est contrôlé par le biais d’autorisations granulaires basées sur les rôles dans Adobe Admin Console. Vous avez besoin des autorisations appropriées dans un profil de produit pour utiliser des fonctionnalités spécifiques de l’interface utilisateur et de l’API du Privacy Service. Contactez votre administrateur système si vous avez besoin d’autorisations supplémentaires.

Pour plus d’informations, les administrateurs peuvent consulter le guide sur la [gestion des autorisations pour Privacy Service](./permissions.md) .

## Directives relatives à la création de tâches de confidentialité {#creation-guidelines}

Pour rationaliser le traitement de vos requêtes et améliorer les temps de réponse, tenez compte des instructions suivantes lors de la création de tâches de confidentialité. Cela s’applique aux méthodes de l’API et de l’interface utilisateur.

1. **Maximiser les sujets des données par requête :** Incluez autant de sujets des données que possible, jusqu’à 1 000, par requête.
2. **ID de groupe pour plus d’efficacité :** Regroupez plusieurs ID pour un seul sujet de données (jusqu’à neuf) dans chaque requête. Les **ID peuvent provenir de différents services Adobe dans la même requête**.
3. **Combinez les tâches d’accès et de suppression :** Incluez les types de tâche &quot;accès&quot; et &quot;suppression&quot; dans une seule requête si le sujet de données l’exige.
4. **Inclure uniquement les produits nécessaires :** Incluez uniquement les produits requis ou sous licence. Les produits supplémentaires peuvent allonger le temps de traitement et augmenter les coûts.

## Surveillance de l’état des tâches de confidentialité {#monitor-status}

Pour surveiller efficacement les tâches de confidentialité et vérifier leur état, Privacy Service fournit trois méthodes. Les méthodes disponibles sont répertoriées ci-dessous afin de surveiller l’efficacité et la productivité. Chaque méthode comprend des conseils sur les bonnes pratiques pour améliorer votre expérience, suivis d’un exemple de scénario idéal qui combine toutes les approches.

### Recevoir des notifications en temps réel {#real-time-notifications}

**Les événements I/O** offrent une surveillance de l’état en temps quasi réel par le biais d’événements d’état. Il s’agit de la méthode la plus efficace, car elle évite d’avoir à implémenter des mécanismes d’interrogation et d’engendrer un trafic API supplémentaire.

**Recommendations:**

- **Configuration de webhook :** configurez des webhooks pour recevoir des notifications push lorsque des modifications d’état se produisent pour les tâches envoyées. Cela facilite la surveillance en temps réel.
- **Notifications :** Utilisez les notifications au niveau de la tâche et du produit pour aider à surveiller la progression des requêtes.

Pour obtenir des instructions sur la configuration d’un enregistrement d’événement pour les notifications de Privacy Service et sur la manière d’interpréter les payloads des notifications, reportez-vous à la documentation sur l’ [abonnement aux événements de Privacy Service](./privacy-events.md) .

### Récupération de toutes les tâches à l’aide de filtres {#retrieve-filtered-responses-for-all-jobs}

Pour récupérer toutes vos données de tâche de confidentialité en fonction de tout filtre spécifié, **effectuez une requête de GET sur le point de terminaison `/jobs`**. Cet appel d’API est utile pour fournir une vue de haut niveau de l’état actuel de la tâche pour les jeux volumineux d’ID de tâche avec une seule requête. Il ne contient pas de réponses de produit détaillées, mais elles se trouvent à l’aide du point d’entrée [`/jobs/{jobID}`](#retrieve-detailed-responses-for-specific-jobs).

Il est préférable d’utiliser une requête de GET au point de terminaison `/jobs` pour rassembler ou comparer les données d’état d’un grand ensemble d’identifiants de tâche, mais **pas** destiné aux activités de type interrogation standard.

**Recommendations:**

- **Paramètres de requête :** Utilisez des filtres spécifiques pour limiter vos résultats, par exemple : plages de données, types de réglementation et état (traitement, fin, etc.).

Vous pouvez afficher une liste de toutes les tâches de confidentialité actuelles de votre entreprise via l’interface utilisateur de Privacy Service. Pour plus d’informations sur le filtrage de la liste des requêtes de tâche, voir la section [Gestion des tâches de confidentialité dans la documentation de l’interface utilisateur](./ui/user-guide.md#job-requests). Vous pouvez également consulter la documentation sur l’ [utilisation du point de terminaison /job dans l’API du Privacy Service](./api/privacy-jobs.md).

La documentation de l’API du Privacy Service contient des détails sur [les filtres de paramètres de requête disponibles](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#tag/Privacy-jobs/operation/listPrivacyJobs).

### Récupération des réponses détaillées pour une seule tâche {#retrieve-detailed-responses-for-specific-jobs}

Pour récupérer des réponses détaillées pour une seule tâche, **effectuez une requête de GET vers le point de terminaison /jobs/{jobID}**. Cette méthode est conçue pour une collecte d’informations plus approfondie, comme les réponses spécifiques à un produit et les messages de succès. Un appel à ce point de terminaison est le meilleur moyen de voir quels produits ont répondu et lesquels sont toujours en attente, bien qu’il soit **et non** destiné à une activité d’interrogation régulière.

Pour plus d&#39;informations sur [la vérification de l&#39;état d&#39;une tâche spécifique](./api/privacy-jobs.md#check-status), reportez-vous à la documentation du point de terminaison `/jobs/{JOB_ID}`.

### Exemple de scénario idéal {#ideal-scenario}

Utilisez un webhook afin que le système puisse mettre à jour automatiquement les enregistrements et fournir des rapports ou des alertes lorsque des groupes d’identifiants issus d’une requête sont terminés. Si des tâches sont toujours en cours, le système récupère ces états de tâches avec une requête de GET au point de terminaison `/jobs` de l’API du Privacy Service et fournit une mise à jour de haut niveau de la liste.

Si une tâche particulière est toujours en attente ou a renvoyé une erreur, vous pouvez récupérer la réponse détaillée avec une requête de GET au point de terminaison `/job/{jobId}`.

## Accès aux données de demande {#access-request-data}

Lorsque des informations sur le sujet des données sont demandées, chaque service renvoie des données dans un format cohérent avec la manière dont il les stocke et les utilise. Une fois que tous les services ont terminé la requête, une URL de fichier d’archive .ZIP est fournie dans les détails de la tâche pour permettre le téléchargement de ces données. Consultez le guide de dépannage pour plus d’informations sur [le téléchargement des résultats de la tâche de confidentialité](https://experienceleague.adobe.com/docs/experience-platform/privacy/troubleshooting-guide.html?lang=fr#how-do-i-download-the-results-of-my-completed-privacy-jobs%3F).

Voici quelques points essentiels concernant la gestion de l’archive de données :

- Tous les fichiers d’archive sont supprimés des serveurs Experience Platform après 30 jours. Vous ne pouvez pas interroger les données client datant de plus de 30 jours.
- La structure du fichier d’archive inclut les dossiers pour chaque produit inclus dans la demande et les fichiers de données qu’il contient. Les fichiers ou dossiers d’archives peuvent être vides si aucune donnée n’a été trouvée pour l’ID spécifié.
- Les données relatives aux tâches créées précédemment ne sont accessibles que pendant 30 jours à compter de la date d’achèvement. Après cette période, les données sont supprimées du système et une nouvelle requête doit être effectuée.

**Recommendations:**

- **Protect Data Archives :** L’URL et le fichier .ZIP doivent être protégés, car ils peuvent contenir des informations d’identification personnelle (PII) pour le sujet de données.

## Considérations techniques {#technical-considerations}

Certaines considérations techniques doivent être prises en compte lors de l’exécution de requêtes de Privacy Service :

- **Période de rétention des données :** La période d’analyse maximale est de 60 jours pour n’importe quel groupe de tâches, et la période maximale pour une requête est de 30 jours (dates de début/fin).
- **Délai d’expiration de la passerelle :** Gardez à l’esprit que votre demande peut être supprimée de la passerelle si elle dépasse 60 secondes.
- **Gestion des erreurs :** Examinez les messages d’erreur de manière approfondie et renvoyez les demandes le cas échéant. Privacy Service ne retraite pas automatiquement les tâches suite à une erreur.
- **Comprendre les erreurs HTTP 429 :** Familiarisez-vous avec les messages d’erreur HTTP 429 et les étapes nécessaires pour atténuer les problèmes. Les erreurs HTTP 429 sont le résultat de &quot;Too many requests&quot;. Pour plus d’informations sur la résolution du problème, consultez la section [Messages d’erreur courants](./troubleshooting-guide.md#common-error-messages) du guide de dépannage.

## Étapes suivantes

En lisant ce document, vous disposez désormais des connaissances et des pratiques nécessaires à l’utilisation efficace et efficiente du Privacy Service. Consultez ensuite le [guide de dépannage](./troubleshooting-guide.md) pour obtenir des réponses aux questions fréquentes sur Privacy Service et des informations sur les erreurs courantes de l’API.
