---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Notes de mise à jour de Privacy Service
description: Dernières notes de mise à jour pour Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: ht
source-wordcount: '552'
ht-degree: 100%

---

# Notes de mise à jour de [!DNL Privacy Service]

Ce document contient des informations sur les nouvelles fonctionnalités d’Adobe Experience Platform [!DNL Privacy Service] ainsi que sur les améliorations et correctifs de bugs importants.

>[!NOTE]
>
>Vous trouverez [ici](../release-notes/latest/latest.md) les notes de mise à jour les plus récentes pour d’autres services [!DNL Experience Platform].

## 9 septembre 2020

### Nouvelles fonctionnalités

| Fonctionnalité | Description |
| --- | --- |
| Respect de la loi LGPD (Brésil) | Des tâches relatives à la confidentialité peuvent maintenant être créées dans le cadre de la réglementation brésilienne [!DNL Lei Geral de Proteção de Dados] (LGPD). Ces tâches sont suivies sous le code de réglementation `lgpd_bra`. |

## 8 avril 2020

### Nouvelles fonctionnalités

| Fonctionnalité | Description |
| --- | --- |
| Respect de la loi PDPA | Maintenant, les demandes d’accès à des informations personnelles ([!DNL Privacy]) peuvent être créées et suivies dans le cadre de la loi Personal Data Protection Act (PDPA) en Thaïlande. Lors de l’envoi de demandes d’accès à des informations personnelles dans l’API, le tableau `regulation` accepte la valeur « pdpa_tha ». |
| Types d’espaces de noms dans l’interface utilisateur | Vous pouvez désormais spécifier différents types d’espaces de noms dans le créateur de requêtes de l’interface utilisateur de [!DNL Privacy Service]. Pour plus d’informations, voir le [guide d’utilisation](ui/user-guide.md). |
| Abandon de l’ancien point d’entrée | L’ancien point d’entrée de l’API (`data/privacy/gdpr`) a été abandonné. |

## 14 janvier 2020

### Nouvelles fonctionnalités

| Fonctionnalité | Description |
| --- | --- |
| Nouveau nom [!DNL Privacy Service] | Le « Service RGPD » a été renommé [!DNL Privacy Service], ce service ayant été élargi pour prendre en compte des réglementations autres que le RGPD. |
| Nouveaux points d’entrée de l’API | Le chemin d’accès de base de l’API [!DNL Privacy Service] (`/data/privacy/gdpr`) a été remplacé par `/data/core/privacy/jobs`. |
| Nouvelle propriété `regulation` requise | Lors de la création de tâches dans l’API [!DNL Privacy Service], une propriété `regulation` doit être fournie dans la payload de la demande pour indiquer la réglementation à prendre en compte pour effectuer le suivi de la tâche. Les valeurs acceptées sont `gdpr` et `ccpa`. Pour plus d’informations, voir le document sur les [tâches liées à la confidentialité](api/privacy-jobs.md) dans le guide de l’API [!DNL Privacy Service]. |
| Prise en charge d’Adobe Primetime Authentication | [!DNL Privacy Service] accepte désormais les demandes d’accès/de suppression d’Adobe Primetime Authentication, en utilisant `primetimeAuthentication` comme valeur de produit. Pour plus d’informations, voir la [documentation de Prime Authentication](https://tve.helpdocsonline.com/how-to-make-a-privacy-request). |

### Améliorations

* Améliorations de l’interface utilisateur [!DNL Privacy Service] :
   * Pages de suivi des tâches distinctes pour les règlements RGPD et CCPA.
   * Nouvelle liste déroulante *Type de règlement* pour passer d’un ensemble de données de suivi à un autre dans le cadre du RGPD et du CCPA.

## 25 juillet 2019

### Nouvelles fonctionnalités

| Fonctionnalité | Description |
| --- | --- |
| Demande de tableau de bord de mesures | Le nouveau tableau de bord de mesures de l’interface utilisateur de [!DNL Privacy Service] offre une visibilité sur les demandes RGPD envoyées, erronées et terminées. |
| Créateur de requêtes | Afin de répondre aux besoins des organisations ayant des utilisateurs et utilisatrices techniques et non techniques pour l’envoi de demandes RGPD, une fonctionnalité « Créer une requête » a été ajoutée à l’interface utilisateur. La fonctionnalité d’envoi de fichiers JSON est toujours disponible dans l’interface utilisateur de [!DNL Privacy Service] pour les organisations qui préfèrent continuer à l’utiliser. |
| Notifications d’événements liés à une tâche RGPD | Les notifications d’événements relatives à des états de tâches RGPD sont un élément essentiel à de nombreux workflows. Alors que les notifications étaient précédemment diffusées à l’aide de notifications par e-mail individuelles, les notifications d’événements RGPD sont des messages tirant parti des événements d’Adobe I/O, envoyés à un webhook configuré pour faciliter l’automatisation des requêtes de tâches. Les utilisateurs de l’interface utilisateur de [!DNL Privacy Service] peuvent s’abonner aux événements RGPD d’Adobe I/O pour recevoir des mises à jour lorsqu’un produit ou la tâche RGPD est terminée. |

## 18 avril 2019

### Améliorations

* Réglage à 7 jours de la plage par défaut du tableau de statut dans l’interface utilisateur de [!DNL Privacy Service].
* Amélioration de la gestion des exceptions internes.
* Amélioration des performances par l’introduction d’une mise en cache pour les appels internes courants à faible taux de changement des données.

### Corrections de bogues

* Ajout d’informations de connexion manquantes pour les requêtes filtrées pour le point d’entrée `GET /` dans l’API [!DNL Privacy Service].

## 11 avril 2019

### Améliorations

* Mise à jour de l’interface utilisateur afin de prendre en charge les nouvelles fonctionnalités pour les clients bêta
* Utilisation d’une nouvelle API de mesures pour prendre en charge les fonctionnalités de l’interface utilisateur 2.0 en version bêta

## 9 avril 2019

### Améliorations

* Mise à jour de tous les appels API de recherche (GET) pour réinitialiser la plage de recherche tous les 30 jours
* Restriction de l’utilisation de l’API à une plage de recherche maximale de 45 jours

## 14 février 2019

### Améliorations

* Application du champ `include` dans chaque envoi POST.
* Application du champ `include` lors du téléchargement de JSON.

### Corrections de bogues

* Correction d’un problème qui empêchait la clientèle de charger l’interface utilisateur de [!DNL Privacy Service].
