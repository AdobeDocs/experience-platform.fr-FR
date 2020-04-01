---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: FAQ sur Privacy Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 7e2e36e13cffdb625b7960ff060f8158773c0fe3

---


# FAQ sur Privacy Service

Ce répond aux questions les plus fréquentes sur le service de confidentialité d’Adobe Experience Platform.

Privacy Service fournit une API RESTful et une interface utilisateur pour aider les à  gérer les demandes de confidentialité des données client. Avec Privacy Service, vous pouvez envoyer des demandes d’accès et de suppression de données personnelles ou privées sur vos clients, ce qui facilite la conformité automatisée avec les réglementations en matière de confidentialité d’entreprise et légales.

## Puis-je utiliser Privacy Service pour nettoyer les données qui ont été envoyées accidentellement à Platform ?

Adobe ne prend pas en charge l’utilisation de Privacy Service pour effacer les données qui ont été envoyées accidentellement à un produit. Le Service de protection de la vie privée est conçu pour vous aider à remplir vos obligations en ce qui concerne les demandes d’accès ou de suppression de personnes à l’égard des données (ou de consommateurs). Ces demandes sont sensibles au temps et sont complétées en fonction de la loi applicable sur la protection des renseignements personnels. La présentation de demandes qui ne sont pas des demandes d’accès aux données ou aux consommateurs ou de suppression a des répercussions sur tous les clients du Service de la protection des renseignements personnels et sur la capacité du Service de la protection des renseignements personnels d’appuyer les délais légaux appropriés.

Veuillez contacter votre gestionnaire de compte (MDP) pour coordonner et fournir un niveau d&#39;effort pour supprimer les informations d&#39;identification personnelle ou les problèmes de données.

## Comment puis-je obtenir des informations sur l&#39;état de ma demande de confidentialité ou de mon travail?

Vous pouvez récupérer des détails sur une tâche particulière à l’aide de l’API ou de l’interface utilisateur de Privacy Service.

### Utilisation de l’API

Pour récupérer l’état d’une tâche particulière à l’aide de l’API Privacy Service, effectuez une requête vers le point de terminaison racine (`GET /`), en utilisant l’ID de la tâche dans le chemin d’accès de la requête. Pour plus d’informations, consultez la section relative à la [vérification de l’état d’une tâche](api/privacy-jobs.md#check-the-status-of-a-job) dans le guide du développeur de Privacy Service.

### Utilisation de l’interface utilisateur

Toutes les demandes de travaux actives sont répertoriées dans le widget Demandes **de** travaux du  d’interface utilisateur de Privacy Service. L’état de chaque demande de tâche est affiché sous la colonne **État** . Pour plus d’informations sur l’affichage des demandes de travaux dans l’interface utilisateur, consultez le guide [d’utilisation du service de](ui/user-guide.md)confidentialité.

## Comment télécharger les résultats de mes tâches de confidentialité terminées ?

L’API et l’interface utilisateur de Privacy Service fournissent toutes deux des méthodes pour télécharger les résultats des tâches terminées au format ZIP.

### Utilisation de l’API

Faites une requête vers le point de terminaison racine (`GET /`) de l’API de Privacy Service, à l’aide de l’ID de la tâche dont vous souhaitez télécharger les résultats dans le chemin d’accès à la requête. Si l’état de la tâche est terminé, l’API inclut un `downloadURL` attribut dans le corps de la réponse. Cet attribut contient une URL que vous pouvez coller dans la barre d’adresse de votre navigateur pour télécharger le fichier ZIP.

Pour plus d’informations, reportez-vous à la section relative à la [recherche d’une tâche par son identifiant](api/privacy-jobs.md#check-the-status-of-a-job) dans le guide du développeur Privacy Service.

### Utilisation de l’interface utilisateur

Dans le de l’interface utilisateur de Privacy Service, recherchez la tâche que vous souhaitez télécharger à partir du widget Demandes de **travaux** . Cliquez sur l’ID de la tâche pour ouvrir la page Détails _de la_ tâche. A partir de là, cliquez sur **Télécharger** dans le coin supérieur droit pour télécharger le fichier ZIP. Consultez le guide [de l’utilisateur de](ui/user-guide.md) Privacy Service pour obtenir des instructions plus détaillées.