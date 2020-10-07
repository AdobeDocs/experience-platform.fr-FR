---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Notes de mise à jour de Privacy Service
topic: release notes
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 62%

---


# [!DNL Privacy Service] notes de mise à jour

This document contains information about new features for Adobe Experience Platform [!DNL Privacy Service], as well as enhancements and significant bug fixes.

>[!NOTE]
>
>Les dernières notes de mise à jour des autres [!DNL Experience Platform] services sont disponibles [ici](../release-notes/latest/latest.md).

## 9 septembre 2020

### Nouvelles fonctionnalités

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de la LGPD (Brésil) | Des emplois dans le domaine de la protection de la vie privée peuvent désormais être créés en vertu de la réglementation brésilienne [!DNL Lei Geral de Proteção de Dados] (LGPD). Ces emplois font l&#39;objet d&#39;un suivi dans le cadre du code réglementaire `lgpd_bra`. |

## 8 avril 2020

### Nouvelles fonctionnalités

| Fonctionnalité | Description |
| --- | --- |
| Respect de la loi PDPA | [!DNL Privacy] en Thaïlande, les requêtes peuvent désormais être créées et suivies en vertu de la loi sur la protection des données personnelles (PDPA). Lors de l’envoi de demandes d’accès à des informations personnelles dans l’API, le tableau `regulation` accepte la valeur « pdpa_tha ». |
| Types d’espaces de noms dans l’interface utilisateur | You can now specify different namespace types in the Request Builder in the [!DNL Privacy Service] UI. Pour plus d’informations, voir le [guide d’utilisation](ui/user-guide.md). |
| Abandon de l’ancien point de terminaison | L’ancien point de terminaison de l’API (`data/privacy/gdpr`) a été abandonné. |

## 14 janvier 2020

### Nouvelles fonctionnalités

| Fonctionnalité | Description |
| --- | --- |
| [!DNL Privacy Service] recomposition | The formerly named &quot;GDPR Service&quot; has been rebranded to [!DNL Privacy Service] as the service has grown to support other regulations in addition to GDPR. |
| Nouveaux points de terminaison de l’API | Base path for the [!DNL Privacy Service] API has been updated from `/data/privacy/gdpr` to `/data/core/privacy/jobs` |
| Nouvelle propriété `regulation` requise | When creating new jobs in the [!DNL Privacy Service] API, a `regulation` property must be supplied in the request payload to indicate which regulation to track the job under. Les valeurs acceptées sont `gdpr` et `ccpa`. Pour plus d’informations, voir le document sur les [tâches liées à la confidentialité](api/privacy-jobs.md) dans le guide de développement de [!DNL Privacy Service] |
| Prise en charge d’Adobe Primetime Authentication | [!DNL Privacy Service] accepte désormais les demandes d’accès/de suppression d’Adobe Primetime Authentication, en utilisant `primetimeAuthentication` comme valeur de produit. Pour plus d’informations, voir la [documentation de Prime Authentication](http://tve.helpdocsonline.com/how-to-make-a-privacy-request). |

### Améliorations

* [!DNL Privacy Service] Améliorations de l’interface utilisateur :
   * Pages de suivi des tâches distinctes pour les règlements RGPD et CCPA.
   * Nouvelle liste déroulante *Type de règlement* pour passer d’un ensemble de données de suivi à un autre dans le cadre du RGPD et du CCPA.

## 25 juillet 2019

### Nouvelles fonctionnalités

| Fonctionnalité | Description |
| --- | --- |
| Demande de tableau de bord de mesures | The new metrics dashboard in the [!DNL Privacy Service] UI provides visibility into submitted, errored, and completed GDPR requests. |
| Créateur de requêtes | Afin de répondre aux besoins des organisations ayant des utilisateurs techniques et non techniques pour l’envoi de demandes RGPD, une fonctionnalité « Créer une requête » a été ajoutée à l’interface utilisateur. The JSON file submission capability is still available in the [!DNL Privacy Service] UI for those organizations who prefer to continue using it. |
| Notifications d’événements liés à une tâche RGPD | Les notifications d’événements relatives à des états de tâches RGPD sont un élément essentiel à de nombreux workflows. Alors que les notifications étaient précédemment diffusées à l’aide de notifications par e-mail individuelles, les notifications d’événements RGPD sont des messages tirant parti des événements d’Adobe I/O, envoyés à un webhook configuré pour faciliter l’automatisation des requêtes de tâches. [!DNL Privacy Service]Les utilisateurs de l’interface utilisateur de peuvent s’abonner aux événements RGPD d’Adobe I/O pour recevoir des mises à jour lorsqu’un produit ou la tâche RGPD est terminée. |

## 18 avril 2019

### Améliorations

* Default range for the status table in the [!DNL Privacy Service] UI modified to a 7-day span.
* Amélioration de la gestion des exceptions internes.
* Amélioration des performances par l’introduction d’une mise en cache pour les appels internes courants à faible taux de changement des données.

### Corrections de bogues

* Ajout d’informations de connexion manquantes pour les requêtes filtrées pour le point de terminaison `GET /` dans l’API [!DNL Privacy Service]

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

* Fixed an issue where customers could not load the [!DNL Privacy Service] UI.