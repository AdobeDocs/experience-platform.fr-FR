---
title: Surveillance de l’utilisation de la licence de requête par lots
description: L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur l’utilisation de la licence Data Distiller de votre entreprise.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: f33629d73e9bc7273e6ee5170294618f3e9731a8
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Surveiller l’utilisation des licences de requête par lots {#monitor-license-usage}

Le tableau de bord de l’utilisation des licences fournit des rapports granulaires sur l’utilisation des licences et les mesures d’utilisation de Query Service pour chaque produit acheté. Pour en savoir plus sur les mesures disponibles affichées dans le tableau de bord, consultez le [guide de tableau de bord d’utilisation de licence](../../dashboards/guides/license-usage.md#available-metrics).

Le tableau de bord fournit des mesures d’utilisation pour chaque produit acheté, l’utilisation consolidée des mesures dans tous les environnements de test de production ou de développement et les mesures d’utilisation d’un environnement de test spécifique. Les informations affichées ici sont capturées pendant un instantané quotidien de votre instance Platform.

>[!NOTE]
>
>Le tableau de bord de l’utilisation des licences n’est pas activé par défaut. Les utilisateurs doivent disposer de l’autorisation &quot;Afficher le tableau de bord de l’utilisation de la licence&quot; pour pouvoir afficher le tableau de bord. Pour obtenir des instructions sur l’octroi des autorisations d’accès pour l’affichage du tableau de bord d’utilisation des licences, reportez-vous au [guide des autorisations du tableau de bord](../../dashboards/permissions.md).

## Calcul des heures {#compute-hours}

La mesure [!UICONTROL Heures de calcul] s’applique uniquement aux clients disposant de la licence Data Distiller pour les requêtes par lots. [!UICONTROL Les heures de calcul] sont la mesure du temps nécessaire aux moteurs Query Service pour lire, traiter et écrire des données dans le lac de données lors de l’exécution d’une requête par lots.

>[!NOTE]
>
>**Les données [!UICONTROL Heures de calcul] sont disponibles avec des restrictions** : les données commencent le 1er octobre 2023 sans tendances.<br>Le **renvoi** des données depuis la date de début de votre contrat est un travail en cours. Elle devrait être disponible d’ici la fin de l’année civile.

![Le tableau de bord de l’utilisation des licences avec la mesure des heures de calcul mise en surbrillance.](../images/data-distiller/compute-hours.png)

Pour plus d’informations sur les mesures disponibles pour votre entreprise en fonction de la licence achetée par celle-ci, consultez le [guide de tableau de bord de l’utilisation des licences](../../dashboards/guides/license-usage.md).
