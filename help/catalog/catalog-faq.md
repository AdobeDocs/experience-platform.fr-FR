---
keywords: service de catalogue ; questions fréquentes ; faq ; faq des jeux de données
title: Questions fréquentes
description: Réponses aux questions les plus fréquemment posées sur le service de catalogue Adobe Experience Platform et les jeux de données.
source-git-commit: 0bb10754e2f5bc289567368c803d4397cec77bf6
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# Questions fréquentes {#faq}

Ce document répond aux questions les plus fréquemment posées sur le service de catalogue Adobe Experience Platform et les jeux de données. Pour toute question ou dépannage concernant d’autres services Platform, y compris les problèmes rencontrés sur toutes les API Platform, reportez-vous au [guide de dépannage Experience Platform](../landing/troubleshooting.md).

## Stratégies et règles de rétention {#retention-policies-and-rules}

### À quels types de jeux de données puis-je appliquer des règles de politique de conservation ?

+++Réponse

Vous pouvez configurer des stratégies de rétention pour les jeux de données créés à l’aide de la classe XDM ExperienceEvent. Pour Profile Service, les stratégies de rétention peuvent uniquement être appliquées aux jeux de données ExperienceEvent après leur activation pour Profile.

+++

### Puis-je définir différentes politiques de rétention pour le lac de données et le service Profile ?

+++Réponse

Oui, vous pouvez appliquer différentes politiques de conservation pour le lac de données et le service Profile.

+++

## Exécution et timing des tâches de rétention {#retention-job-execution-and-timing}

### Dans combien de temps la tâche de conservation du jeu de données supprimera-t-elle les données des services de lac de données ?

+++Réponse

Les expirations de jeux de données sont évaluées et traitées toutes les semaines, supprimant tous les enregistrements qui ont expiré. Un événement est considéré comme ayant expiré s’il a été ingéré dans Platform pendant plus de 30 jours (date d’ingestion > 30 jours) et sa date d’événement dépasse la période de conservation définie.

+++

### Dans combien de temps la tâche de conservation du jeu de données supprimera-t-elle les données des services Profile ?

+++Réponse

Une fois une politique de conservation définie, les événements existants sont immédiatement supprimés de Platform si leur horodatage d’événement dépasse la période de conservation. Les nouveaux événements sont supprimés lorsque leur horodatage dépasse la période de conservation.

Par exemple, si vous appliquez une stratégie d’expiration de 30 jours le 15 mai, les événements suivants se produisent :

- Les nouveaux événements reçoivent une expiration de 30 jours lorsqu’ils sont ingérés.
- Les événements existants avec un horodatage antérieur au 15 avril sont immédiatement supprimés.
- Les événements existants avec un horodatage après le 15 avril expirent 30 jours après leur horodatage. Par exemple, un événement du 18 avril sera supprimé le 18 mai.

+++

## Utilisation et surveillance des jeux de données

### Comment puis-je vérifier l’utilisation actuelle de mon jeu de données ?

+++Réponse

Vous pouvez afficher la dernière taille de stockage au niveau du jeu de données dans le lac de données et dans Profile sous la forme de mesures distinctes sur la page d’inventaire [!UICONTROL Jeux de données] . Vous pouvez également trier les colonnes pour identifier les jeux de données les plus volumineux et vous assurer que les stratégies de conservation sont appliquées. L’utilisation au niveau des environnements de test est disponible dans le tableau de bord Utilisation de la licence . Pour plus d’informations, reportez-vous à la [documentation sur l’utilisation de la licence](../dashboards/guides/license-usage.md) .

+++

### Comment puis-je vérifier si la tâche de conservation des données a réussi ?

+++Réponse

Vous pouvez vérifier l’horodatage de la dernière tâche de rétention des données dans l’ [interface utilisateur de configuration de rétention des jeux de données](./datasets/user-guide.md#data-retention-policy) et sur la page d’inventaire [!UICONTROL Jeux de données] . Les rapports pour l’utilisation des jeux de données historiques sont actuellement indisponibles, mais sont prévus pour les prochaines versions.

+++

## Récupération des données {#data-recovery}

### Puis-je récupérer les données supprimées ?

+++Réponse

Non, une fois la politique de conservation appliquée, les données antérieures à la période de conservation sont définitivement supprimées et ne peuvent pas être récupérées.

+++

