---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Notes de mise à jour du Privacy Service
topic-legacy: release notes
description: Notes de mise à jour les plus récentes pour Adobe Experience Platform Privacy Service.
exl-id: 66ee38f1-f0d5-44ff-823d-d1b8a9765c6d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 60%

---

# [!DNL Privacy Service] notes de mise à jour

Ce document contient des informations sur les nouvelles fonctionnalités de Adobe Experience Platform [!DNL Privacy Service], ainsi que sur les améliorations et les correctifs de bogues significatifs.

>[!NOTE]
>
>Les dernières notes de mise à jour des autres services [!DNL Experience Platform] sont disponibles [ici](../release-notes/latest/latest.md).

## 9 septembre 2020

### Nouvelles fonctionnalités

| Fonctionnalité | Description |
| --- | --- |
| Prise en charge de la LGPD (Brésil) | Des emplois dans le domaine de la protection de la vie privée peuvent désormais être créés en vertu de la réglementation brésilienne [!DNL Lei Geral de Proteção de Dados] (LGPD). Ces emplois sont suivis sous le code de réglementation `lgpd_bra`. |

## 8 avril 2020

### Nouvelles fonctionnalités

| Fonctionnalité | Description |
| --- | --- |
| Respect de la loi PDPA | [!DNL Privacy] en Thaïlande, les requêtes peuvent désormais être créées et suivies en vertu de la loi sur la protection des données personnelles (PDPA). Lors de l’envoi de demandes d’accès à des informations personnelles dans l’API, le tableau `regulation` accepte la valeur « pdpa_tha ». |
| Types d’espaces de noms dans l’interface utilisateur | Vous pouvez désormais spécifier différents types d’espace de nommage dans le Créateur de requêtes dans l’[!DNL Privacy Service] interface utilisateur. Pour plus d’informations, voir le [guide d’utilisation](ui/user-guide.md). |
| Abandon de l’ancien point de terminaison | L’ancien point de terminaison de l’API (`data/privacy/gdpr`) a été abandonné. |

## 14 janvier 2020

### Nouvelles fonctionnalités

| Fonctionnalité | Description |
| --- | --- |
| [!DNL Privacy Service] recomposition | Le service appelé auparavant &quot;Service RGMD&quot; a été renommé [!DNL Privacy Service], car il a grandi pour appuyer d&#39;autres règlements en plus du RGMD. |
| Nouveaux points de terminaison de l’API | Le chemin de base de l&#39;API [!DNL Privacy Service] a été mis à jour de `/data/privacy/gdpr` en `/data/core/privacy/jobs`. |
| Nouvelle propriété `regulation` requise | Lors de la création de nouvelles tâches dans l&#39;API [!DNL Privacy Service], une propriété `regulation` doit être fournie dans la charge utile de la demande pour indiquer la réglementation sous laquelle effectuer le suivi de la tâche. Les valeurs acceptées sont `gdpr` et `ccpa`. Pour plus d’informations, voir le document sur les [tâches liées à la confidentialité](api/privacy-jobs.md) dans le guide de développement de [!DNL Privacy Service] |
| Prise en charge d’Adobe Primetime Authentication | [!DNL Privacy Service] accepte désormais les demandes d’accès/de suppression d’Adobe Primetime Authentication, en utilisant `primetimeAuthentication` comme valeur de produit. Pour plus d’informations, voir la [documentation de Prime Authentication](http://tve.helpdocsonline.com/how-to-make-a-privacy-request). |

### Améliorations

* [!DNL Privacy Service] Améliorations de l’interface utilisateur :
   * Pages de suivi des tâches distinctes pour les règlements RGPD et CCPA.
   * Nouvelle liste déroulante *Type de règlement* pour passer d’un ensemble de données de suivi à un autre dans le cadre du RGPD et du CCPA.

## 25 juillet 2019

### Nouvelles fonctionnalités

| Fonctionnalité | Description |
| --- | --- |
| Demande de tableau de bord de mesures | Le nouveau tableau de bord de mesures dans l&#39;interface utilisateur [!DNL Privacy Service] permet de visualiser les demandes de RGD envoyées, erronées et terminées. |
| Créateur de requêtes | Afin de répondre aux besoins des organisations ayant des utilisateurs techniques et non techniques pour l’envoi de demandes RGPD, une fonctionnalité « Créer une requête » a été ajoutée à l’interface utilisateur. La fonctionnalité d’envoi de fichiers JSON est toujours disponible dans l’interface utilisateur [!DNL Privacy Service] pour les organisations qui préfèrent continuer à l’utiliser. |
| Notifications d’événements liés à une tâche RGPD | Les notifications d’événements relatives à des états de tâches RGPD sont un élément essentiel à de nombreux workflows. Alors que les notifications étaient précédemment diffusées à l’aide de notifications par e-mail individuelles, les notifications d’événements RGPD sont des messages tirant parti des événements d’Adobe I/O, envoyés à un webhook configuré pour faciliter l’automatisation des requêtes de tâches. [!DNL Privacy Service]Les utilisateurs de l’interface utilisateur de peuvent s’abonner aux événements RGPD d’Adobe I/O pour recevoir des mises à jour lorsqu’un produit ou la tâche RGPD est terminée. |

## 18 avril 2019

### Améliorations

* Plage par défaut de la table d&#39;état dans l&#39;interface utilisateur [!DNL Privacy Service] modifiée en une période de 7 jours.
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

* Correction d’un problème en raison duquel les clients ne pouvaient pas charger l’interface utilisateur [!DNL Privacy Service].
