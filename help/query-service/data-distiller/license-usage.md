---
title: Surveillance de l’utilisation de la licence de requête par lots
description: L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur l’utilisation de la licence Data Distiller de votre entreprise.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: f33629d73e9bc7273e6ee5170294618f3e9731a8
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Surveiller l’utilisation des licences de requête par lots {#monitor-license-usage}

Le tableau de bord de l’utilisation des licences fournit des rapports granulaires sur l’utilisation des licences et les mesures d’utilisation de Query Service pour chaque produit acheté. Pour en savoir plus sur les mesures disponibles affichées dans le tableau de bord, consultez la page [guide de tableau de bord d’utilisation des licences](../../dashboards/guides/license-usage.md#available-metrics).

Le tableau de bord fournit des mesures d’utilisation pour chaque produit acheté, l’utilisation consolidée des mesures dans tous les environnements de test de production ou de développement et les mesures d’utilisation d’un environnement de test spécifique. Les informations affichées ici sont capturées pendant un instantané quotidien de votre instance Platform.

>[!NOTE]
>
>Le tableau de bord de l’utilisation des licences n’est pas activé par défaut. Les utilisateurs doivent disposer de l’autorisation &quot;Afficher le tableau de bord de l’utilisation de la licence&quot; pour pouvoir afficher le tableau de bord. Pour connaître les étapes d’octroi des autorisations d’accès pour afficher le tableau de bord d’utilisation des licences, reportez-vous à la section [Guide des autorisations de tableau de bord](../../dashboards/permissions.md).

## Calculer les heures {#compute-hours}

La variable [!UICONTROL Calculer les heures] ne s’applique qu’aux clients disposant de la licence Data Distiller pour les requêtes par lots. [!UICONTROL Calculer les heures] sont la mesure du temps nécessaire aux moteurs Query Service pour lire, traiter et écrire des données dans le lac de données lors de l’exécution d’une requête par lots.

>[!NOTE]
>
>**La variable [!UICONTROL Calculer les heures] Les données sont disponibles avec des restrictions**: les données commencent le 1er octobre 2023 sans évolution.<br>La variable **renvoyer** de données à partir de la date de début de votre contrat est un travail en cours. Elle devrait être disponible d’ici la fin de l’année civile.

![Le tableau de bord de l’utilisation des licences avec la mesure Heures de calcul mise en surbrillance.](../images/data-distiller/compute-hours.png)

Pour plus d’informations sur les mesures disponibles pour votre entreprise en fonction de la licence achetée de votre entreprise, voir la section [guide de tableau de bord d’utilisation des licences](../../dashboards/guides/license-usage.md).
