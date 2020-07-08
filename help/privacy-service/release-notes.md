---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Notes de mise à jour des Privacy Service
topic: release notes
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 5%

---


# Notes de mise à jour des Privacy Service

Ce document contient des informations sur les nouvelles fonctionnalités de l’Adobe Experience Platform Privacy Service, ainsi que sur les améliorations et les correctifs de bogues significatifs.

>[!NOTE]
>
>Les dernières notes de mise à jour des autres services Experience Platform sont disponibles [ici](../release-notes/latest/latest.md).

## 8 avril 2020

### Nouvelles fonctionnalités

| Fonction | Description |
| --- | --- |
| Prise en charge de PDPA | Les demandes de confidentialité peuvent maintenant être créées et suivies en vertu de la Loi sur la protection des données personnelles (PDPA) en Thaïlande. Lorsque vous effectuez des demandes de confidentialité dans l&#39;API, le `regulation` tableau accepte la valeur &quot;pdpa_tha&quot;. |
| Types d’Espace de nommage dans l’interface utilisateur | Vous pouvez désormais spécifier différents types d’espace de nommage dans le Créateur de requêtes dans l’interface utilisateur du Privacy Service. Consultez le guide [](ui/user-guide.md) d’utilisation pour plus d’informations. |
| Ancienne obsolescence des points de terminaison | L’ancien point de terminaison API (`data/privacy/gdpr`) a été abandonné. |

## 14 janvier 2020

### Nouvelles fonctionnalités

| Fonction | Description |
| --- | --- |
| Changement de marque du Privacy Service | L&#39;ancien &quot;Service RMMD&quot; a été renommé Privacy Service car le service a pris de l&#39;ampleur pour appuyer d&#39;autres règlements en plus du RMMD. |
| Nouveaux points de terminaison API | Le chemin de base de l&#39;API du Privacy Service a été mis à jour de `/data/privacy/gdpr` à `/data/core/privacy/jobs` |
| Nouvelle propriété `regulation` requise | Lors de la création de nouvelles tâches dans l’API du Privacy Service, une `regulation` propriété doit être fournie dans la charge utile de la demande pour indiquer le règlement sous lequel effectuer le suivi de la tâche. Les valeurs acceptées sont `gdpr` et `ccpa`. Pour plus d’informations, consultez le document sur les tâches [de](api/privacy-jobs.md) confidentialité dans le guide du développeur Privacy Service. |
| Prise en charge de l’authentification Adobe Primetime | Le Privacy Service accepte désormais les demandes d’accès/de suppression provenant de l’authentification Adobe Primetime, en utilisant `primetimeAuthentication` comme valeur de produit. See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### Améliorations

* Améliorations de l’interface utilisateur du Privacy Service :
   * Pages distinctes de suivi des tâches pour les règlements sur les RGMD et les ACCP.
   * Nouvelle liste déroulante Type _de_ règlement permettant de basculer entre les données de suivi pour le RGPD et l&#39;ACCP.

## 25 juillet 2019

### Nouvelles fonctionnalités

| Fonction | Description |
| --- | --- |
| Tableau de bord de mesures de demande | Le nouveau tableau de bord de mesures dans l’interface utilisateur du Privacy Service permet d’afficher les demandes de RGD envoyées, en erreur et terminées. |
| Créateur de requêtes | Pour fournir des services aux entreprises qui utilisent à la fois des utilisateurs techniques et non techniques qui envoient des demandes de RGD, une fonctionnalité &quot;Créer une demande&quot; a été ajoutée à l’interface utilisateur. La fonctionnalité d’envoi de fichiers JSON est toujours disponible dans l’interface utilisateur du Privacy Service pour les entreprises qui préfèrent continuer à l’utiliser. |
| Notifications de Événement de travaux GDPR | Pour de nombreux workflows, les notifications Événements sur les états des tâches du RGPD sont un élément essentiel. Bien que les notifications aient été précédemment diffusées à l’aide de notifications électroniques individuelles, les notifications de événement GDPR sont des messages qui tirent parti des événements d’E/S Adobe, qui sont envoyés à un crochet Web configuré facilitant l’automatisation des demandes de travail. Les utilisateurs de l’interface utilisateur Privacy Service peuvent s’abonner aux événements GDPR d’E/S Adobe pour recevoir des mises à jour lorsqu’un produit ou la tâche GDPR est terminée. |

## 18 avril 2019

### Améliorations

* La plage par défaut du tableau d’état dans l’interface utilisateur du Privacy Service a été modifiée pour une période de 7 jours.
* Meilleure gestion des exceptions internes.
* Amélioration des performances en introduisant la mise en cache pour les appels internes courants avec un faible taux de changement des données.

### Correctifs

* Informations de journalisation manquantes Ajoutées pour les requêtes filtrées pour le `GET /` point de terminaison dans l&#39;API du Privacy Service.

## 11 avril 2019

### Améliorations

* Mise à jour de l’interface utilisateur pour la prise en charge de nouvelles fonctionnalités pour les clients bêta
* Nouvelle API de mesures pour la prise en charge des fonctionnalités de l’interface utilisateur 2.0 en version bêta

## 9 avril 2019

### Améliorations

* Mise à jour par défaut de tous les appels d’API de recherche (GET) sur une plage de recherche de 30 jours
* Utilisation restreinte de l’API pour une plage de recherche maximale de 45 jours

## 14 février 2019

### Améliorations

* Impose le `include` champ dans chaque envoi POST.
* Impose le `include` champ lors du transfert de JSON.

### Correctifs

* Correction d’un problème en raison duquel les clients ne pouvaient pas charger l’interface utilisateur du Privacy Service.