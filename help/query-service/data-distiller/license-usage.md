---
title: Surveiller l’utilisation de la licence de requête par lots
description: L’interface utilisateur de Adobe Experience Platform fournit un tableau de bord grâce auquel vous pouvez afficher des informations importantes sur l’utilisation des licences Data Distiller de votre entreprise.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
source-git-commit: dce631923bd38f3237da3e1928e2203dc1a266ca
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# Surveiller l’utilisation des licences de requêtes par lots {#monitor-license-usage}

Le tableau de bord d’utilisation de la licence fournit des rapports granulaires sur l’utilisation de la licence Query Service de votre entreprise et des mesures d’utilisation pour chaque produit acheté. Pour en savoir plus sur les mesures disponibles affichées dans le tableau de bord, consultez le [guide du tableau de bord d’utilisation des licences](../../dashboards/guides/license-usage.md#available-metrics).

Le tableau de bord fournit des mesures d’utilisation pour chaque produit acheté, l’utilisation consolidée des mesures dans tous les sandbox de production ou de développement, ainsi que les mesures d’utilisation d’un sandbox spécifique. Les informations affichées ici sont capturées lors d’un instantané quotidien de votre instance Experience Platform. Les administrateurs peuvent surveiller et mettre fin aux sessions inactives de Query Service afin de libérer de la capacité lorsqu’aucune session supplémentaire n’est disponible et que les utilisateurs sont bloqués en raison de sessions inactives (non actives). Voir [Gérer les sessions Query Service](../ui/session-management.md) pour plus d’informations.

>[!NOTE]
>
>Le tableau de bord d’utilisation de la licence n’est pas activé par défaut. Les utilisateurs doivent disposer de l’autorisation « Afficher le tableau de bord d’utilisation des licences » pour pouvoir consulter le tableau de bord. Pour obtenir des instructions sur l’octroi des autorisations d’accès pour l’affichage du tableau de bord d’utilisation des licences, consultez le guide [autorisations des tableaux de bord](../../dashboards/permissions.md).

## Heures de calcul {#compute-hours}

La mesure [!UICONTROL Compute hours] s’applique uniquement aux clients disposant de la licence Data Distiller pour les requêtes par lots. [!UICONTROL Compute hours] sont les mesures du temps pris par les moteurs de Query Service pour lire, traiter et écrire des données dans le lac de données lorsqu’une requête par lots est exécutée.

![Tableau de bord d’utilisation de la licence avec la mesure Calculer les heures mise en surbrillance.](../images/data-distiller/compute-hours.png)

Pour plus d’informations sur les mesures disponibles pour votre organisation en fonction de la licence achetée par votre organisation, consultez le [guide du tableau de bord d’utilisation des licences](../../dashboards/guides/license-usage.md).
