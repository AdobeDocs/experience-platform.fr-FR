---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Notes de mise à jour de Privacy Service
topic: release notes
translation-type: tm+mt
source-git-commit: 682436b29df4696e98ef96fe5a65ab32221098ba

---


# Notes de mise à jour de Privacy Service

Ce contient des informations sur les nouvelles fonctionnalités d’Adobe Experience Platform Privacy Service, ainsi que sur les améliorations et correctifs de bogues significatifs.

## 8 avril 2020

### Nouvelles fonctionnalités

| Fonction | Description |
| --- | --- |
| Prise en charge de PDPA | Les demandes de protection de la vie privée peuvent maintenant être créées et suivies en vertu de la Loi sur la protection des données personnelles (PDPA) en Thaïlande. Lors de l’exécution de demandes de confidentialité dans l’API, le `regulation` tableau accepte la valeur &quot;pdpa_tha&quot;. |
|  types de  de dans l’interface utilisateur | Vous pouvez désormais spécifier différents types de  de  dans le Créateur de requêtes dans l’interface utilisateur de Privacy Service. Pour plus d’informations, consultez le guide [d’utilisation](ui/user-guide.md) . |
| Ancienne dépréciation du point de fin | L’ancien point de terminaison API (`data/privacy/gdpr`) a été abandonné. |

## 14 janvier 2020

### Nouvelles fonctionnalités

| Fonction | Description |
| --- | --- |
| Refonte de la marque Privacy Service | Le Service de protection des renseignements personnels, anciennement appelé &quot;Service RMMD&quot;, a été renommé Service de protection des renseignements personnels, car il a pris de l&#39;expansion pour appuyer d&#39;autres règlements en plus du RMMD. |
| Nouveaux points de fin API | Le chemin de base de l’API de Privacy Service a été mis à jour de `/data/privacy/gdpr` vers `/data/core/privacy/jobs` |
| Nouvelle `regulation` propriété obligatoire | Lors de la création de nouvelles tâches dans l’API de Privacy Service, une `regulation` propriété doit être fournie dans la charge utile de la demande pour indiquer la réglementation sous laquelle effectuer le suivi de la tâche. Les valeurs acceptées sont `gdpr` et `ccpa`. Pour plus d’informations, reportez-vous au  sur les tâches [de](api/privacy-jobs.md) confidentialité du guide du développeur de Privacy Service. |
| Prise en charge de l’authentification Adobe Primetime | Privacy Service accepte désormais les demandes d’accès/de suppression d’Adobe Primetime Authentication, en utilisant `primetimeAuthentication` comme valeur de produit. See the [Primetime Authentication documentation](http://tve.helpdocsonline.com/how-to-make-a-privacy-request) for more information. |

### Améliorations

* Améliorations de l’interface utilisateur de Privacy Service :
   * Pages de suivi des tâches distinctes pour les règlements sur le RMR et l&#39;ACCP.
   * Nouvelle liste déroulante Type _de_ règlement pour basculer entre les données de suivi pour le RDPC et l&#39;ACCP.

## 25 juillet 2019

### Nouvelles fonctionnalités

| Fonction | Description |
| --- | --- |
| Demander des  de mesures | Les nouvelles  de mesures dans l’interface utilisateur de Privacy Service offrent une visibilité sur les demandes GDPR envoyées, en erreur et terminées. |
| Créateur de requêtes | Pour fournir des services aux organisations dont les utilisateurs techniques et non techniques soumettent des demandes de RDMD, une fonctionnalité &quot;Créer une demande&quot; a été ajoutée à l’interface utilisateur. La fonctionnalité d’envoi de fichiers JSON est toujours disponible dans l’interface utilisateur de Privacy Service pour les organisations qui préfèrent continuer à l’utiliser. |
| Notifications  tâche GDPR | Les notifications  sur les états des tâches GDPR sont un élément essentiel pour de nombreux . Bien que les notifications aient été précédemment diffusées à l’aide de notifications électroniques individuelles, les notifications  GDPR sont des messages qui utilisent les d’E/S Adobe, qui sont envoyés à un crochet Web configuré pour faciliter l’automatisation des demandes de travaux. Les utilisateurs de l’interface utilisateur de Privacy Service peuvent s’abonner au GDPR d’E/S d’Adobe pour recevoir des mises à jour lorsqu’un produit ou la tâche GDPR est terminée. |

## 18 avril 2019

### Améliorations

* Plage par défaut du tableau d’état dans l’interface utilisateur de Privacy Service modifiée sur une période de 7 jours.
* Meilleure gestion des exceptions internes.
* Amélioration des performances en introduisant la mise en cache pour les appels internes courants avec un faible taux de changement des données.

### Corrections de bogues

* Ajout d’informations de journalisation manquantes pour les  filtrées pour le `GET /` point de terminaison dans l’API Privacy Service.

## 11 avril 2019

### Améliorations

* Interface utilisateur mise à jour pour prendre en charge les nouvelles fonctionnalités pour les clients bêta
* Nouvelle API de mesures pour la prise en charge des fonctionnalités de l’interface utilisateur 2.0 en version bêta

## 9 avril 2019

### Améliorations

* Mise à jour par défaut de tous les appels d’API de recherche (GET) sur une plage de recherche de 30 jours
* Utilisation restreinte de l’API pour une plage de recherche maximale de 45 jours

## 14 février 2019

### Améliorations

* Impose le `include` champ dans chaque envoi de post-test.
* Impose le `include` champ lors du transfert de JSON.

### Corrections de bogues

* Correction d’un problème en raison duquel les clients ne pouvaient pas charger l’interface utilisateur de Privacy Service.