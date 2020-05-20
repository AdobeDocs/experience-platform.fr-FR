---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Notes de mise à jour de Privacy Service
topic: release notes
translation-type: tm+mt
source-git-commit: 682436b29df4696e98ef96fe5a65ab32221098ba
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 5%

---


# Notes de mise à jour de Privacy Service

Ce document contient des informations sur les nouvelles fonctionnalités d’Adobe Experience Platform Privacy Service, ainsi que sur les améliorations et correctifs de bogues significatifs.

## 8 avril 2020

### Nouvelles fonctionnalités

| Fonction | Description |
| --- | --- |
| Prise en charge de PDPA | Les demandes de confidentialité peuvent maintenant être créées et suivies en vertu de la Loi sur la protection des données personnelles (PDPA) en Thaïlande. Lorsque vous effectuez des demandes de confidentialité dans l&#39;API, le `regulation` tableau accepte la valeur &quot;pdpa_tha&quot;. |
| Types d’Espace de nommage dans l’interface utilisateur | Vous pouvez désormais spécifier différents types d’espace de nommage dans le Créateur de requêtes de l’interface utilisateur de Privacy Service. Consultez le guide [](ui/user-guide.md) d’utilisation pour plus d’informations. |
| Ancienne obsolescence des points de terminaison | L’ancien point de terminaison API (`data/privacy/gdpr`) a été abandonné. |

## 14 janvier 2020

### Nouvelles fonctionnalités

| Fonction | Description |
| --- | --- |
| Refonte de la marque Privacy Service | Le service appelé auparavant &quot;RMMD&quot; a été rebaptisé Service de la protection des renseignements personnels, car il s&#39;est développé pour appuyer d&#39;autres règlements en plus du RMMD. |
| Nouveaux points de terminaison API | Le chemin de base de l’API Privacy Service a été mis à jour de `/data/privacy/gdpr` à `/data/core/privacy/jobs` |
| Nouvelle propriété `regulation` requise | Lors de la création de nouvelles tâches dans l’API de Privacy Service, une `regulation` propriété doit être fournie dans la charge utile de la demande pour indiquer la réglementation sous laquelle effectuer le suivi de la tâche. Les valeurs acceptées sont `gdpr` et `ccpa`. Pour plus d’informations, consultez le document sur les tâches [de](api/privacy-jobs.md) protection de la vie privée dans le guide du développeur de Privacy Service. |
| Prise en charge de l’authentification Adobe Primetime | Privacy Service accepte désormais les demandes d’accès/de suppression d’Adobe Primetime Authentication, en utilisant `primetimeAuthentication` comme valeur de produit. See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### Améliorations

* Améliorations de l’interface utilisateur de Privacy Service :
   * Pages distinctes de suivi des tâches pour les règlements sur les RGMD et les ACCP.
   * Nouvelle liste déroulante Type _de_ règlement permettant de basculer entre les données de suivi pour le RGPD et l&#39;ACCP.

## 25 juillet 2019

### Nouvelles fonctionnalités

| Fonction | Description |
| --- | --- |
| Tableau de bord de mesures de demande | Le nouveau tableau de bord de mesures dans l’interface utilisateur de Privacy Service permet de visualiser les demandes de RMPE envoyées, échouées et terminées. |
| Créateur de requêtes | Pour fournir des services aux entreprises qui utilisent à la fois des utilisateurs techniques et non techniques qui envoient des demandes de RGD, une fonctionnalité &quot;Créer une demande&quot; a été ajoutée à l’interface utilisateur. La fonctionnalité d’envoi de fichiers JSON est toujours disponible dans l’interface utilisateur de Privacy Service pour les entreprises qui préfèrent continuer à l’utiliser. |
| Notifications de Événement de travaux GDPR | Pour de nombreux workflows, les notifications Événements sur les états des tâches du RGPD sont un élément essentiel. Bien que les notifications aient été précédemment diffusées à l’aide de notifications électroniques individuelles, les notifications de événement GDPR sont des messages qui utilisent les événements d’E/S Adobe, qui sont envoyés à un crochet Web configuré facilitant l’automatisation des demandes de travail. Les utilisateurs de l’interface utilisateur de Privacy Service peuvent s’abonner aux événements GDPR d’E/S d’Adobe pour recevoir des mises à jour lorsqu’un produit ou la tâche GDPR est terminée. |

## 18 avril 2019

### Améliorations

* La plage par défaut du tableau d’état dans l’interface utilisateur de Privacy Service a été modifiée pour une période de 7 jours.
* Meilleure gestion des exceptions internes.
* Amélioration des performances en introduisant la mise en cache pour les appels internes courants avec un faible taux de changement des données.

### Corrections de bogues

* Ajout d’informations de journalisation manquantes pour les requêtes filtrées pour le `GET /` point de terminaison dans l’API Privacy Service.

## 11 avril 2019

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

### Corrections de bogues

* Correction d’un problème en raison duquel les clients ne pouvaient pas charger l’interface utilisateur de Privacy Service.