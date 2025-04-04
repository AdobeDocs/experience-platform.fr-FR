---
keywords: service de catalogue ; questions ; questions fréquentes ; questions fréquentes ; jeux de données faq
title: Questions fréquentes
description: Réponses aux questions les plus fréquemment posées sur le service de catalogue Adobe Experience Platform et les jeux de données.
exl-id: 70d2a352-75bd-4bbc-98e6-aeea16306f63
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# Questions fréquentes {#faq}

Ce document répond aux questions fréquentes sur le service de catalogue Adobe Experience Platform et les jeux de données. Pour toute question ou dépannage concernant d’autres services Experience Platform, y compris les problèmes rencontrés sur toutes les API d’Experience Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

## Règles et politiques de conservation {#retention-policies-and-rules}

### À quels types de jeux de données puis-je appliquer des règles de politique de rétention ?

+++Réponse

Vous pouvez configurer des politiques de conservation sur les jeux de données créés à l’aide de la classe XDM ExperienceEvent. Pour le service de profil, les politiques de conservation ne peuvent être appliquées aux jeux de données ExperienceEvent qu&#39;après avoir été activées pour le profil.

+++

### Puis-je définir différentes politiques de conservation pour le lac de données et le service de profil ?

+++Réponse

Oui, vous pouvez appliquer différentes politiques de conservation pour le lac de données et le service de profil.

+++

## Exécution et minutage des tâches de rétention {#retention-job-execution-and-timing}

### Dans combien de temps la tâche de conservation des jeux de données supprimera-t-elle les données des services de lac de données ?

+++Réponse

Les expirations de jeux de données sont évaluées et traitées chaque semaine, supprimant tous les enregistrements qui ont expiré. Un événement est considéré comme ayant expiré s’il a été ingéré dans Experience Platform pendant plus de 30 jours (date d’ingestion > 30 jours) et si sa date d’événement dépasse la période de conservation définie.

+++

### Dans combien de temps la tâche de conservation des jeux de données supprimera-t-elle les données des services de profil ?

+++Réponse

Une fois qu’une politique de conservation est définie, les événements existants sont immédiatement supprimés d’Experience Platform si leur horodatage d’événement dépasse la période de conservation. Les nouveaux événements sont supprimés une fois que leur horodatage dépasse la période de conservation.

Par exemple, si vous appliquez une politique d’expiration de 30 jours le 15 mai, ce qui suit se produit :

- Les nouveaux événements sont soumis à une expiration de 30 jours lors de leur ingestion.
- Les événements existants dont la date et heure sont antérieures au 15 avril sont immédiatement supprimés.
- Les événements existants dont la date et heure sont postérieures au 15 avril sont définis pour expirer 30 jours après leur date et heure. Par exemple, un événement du 18 avril serait supprimé le 18 mai.

+++

## Utilisation et surveillance des jeux de données

### Comment puis-je vérifier l’utilisation actuelle de mon jeu de données ?

+++Réponse

Vous pouvez afficher la dernière taille de stockage au niveau du jeu de données dans le lac de données et le profil sous la forme de mesures distinctes sur la page d’inventaire [!UICONTROL Jeux de données]. Vous pouvez également trier les colonnes pour identifier les jeux de données les plus volumineux et vous assurer que les politiques de conservation sont appliquées. L’utilisation au niveau du sandbox est disponible dans le tableau de bord Utilisation des licences . Reportez-vous à la [documentation relative à l’utilisation des licences](../dashboards/guides/license-usage.md) pour plus d’informations.

+++

### Comment puis-je vérifier si la tâche de conservation des données a réussi ?

+++Réponse

Vous pouvez vérifier la date et l’heure de la dernière tâche de conservation des données dans l’[interface utilisateur de configuration de la conservation des jeux de données](./datasets/user-guide.md#data-retention-policy) et sur la page d’inventaire [!UICONTROL Jeux de données]. Les rapports concernant l’utilisation des jeux de données historiques ne sont actuellement pas disponibles, mais sont prévus pour les prochaines versions.

+++

## Récupération de données {#data-recovery}

### Puis-je récupérer les données supprimées ?

+++Réponse

Non, une fois la politique de conservation appliquée, toutes les données antérieures à la période de conservation sont supprimées définitivement et ne peuvent pas être récupérées.

+++
