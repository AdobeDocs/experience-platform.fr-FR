---
title: Journaux de requête
description: Les logs de requête sont générés automatiquement chaque fois qu’une requête est exécutée et sont disponibles via l’interface utilisateur pour faciliter la résolution des problèmes. Ce document explique comment utiliser et parcourir la section Journaux de Query Service de l’interface utilisateur.
exl-id: 929e9fba-a9ba-4bf9-a363-ca8657a84f75
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 3%

---

# Journaux de requête

>[!IMPORTANT]
>
>Certaines fonctionnalités de logs de requête sont actuellement dans une version limitée et ne sont pas disponibles pour tous les clients. Votre interface utilisateur peut apparaître légèrement différemment sans icône de modification. En outre, le processus de sélection d’un nom de requête peut permettre d’accéder à l’éditeur de requêtes au lieu de la fonction [!UICONTROL Détails du journal de requête] vue.

Adobe Experience Platform conserve un journal de tous les événements de requête qui se produisent par le biais de l’API et de l’interface utilisateur. Ces informations sont disponibles dans l’interface utilisateur de Query Service à partir du [!UICONTROL Journaux] .

Les fichiers journaux sont générés automatiquement par tout événement de requête et contiennent des informations telles que le code SQL utilisé, l’état de la requête, la durée de la requête et l’heure de la dernière exécution. Vous pouvez utiliser les données du journal des requêtes comme un outil puissant pour résoudre les problèmes de requêtes inefficaces ou problématiques. Des informations plus complètes sur le journal sont conservées dans le cadre de la fonctionnalité de journal d’audit. Vous pouvez les trouver dans la section [documentation du journal d’audit](../../landing/governance-privacy-security/audit-logs/overview.md).

## Vérifier les logs de requête

Pour vérifier les logs de requête, sélectionnez [!UICONTROL Requêtes] pour accéder à l’espace de travail Query Service et sélectionnez [!UICONTROL Journal] dans les options disponibles.

![L’interface utilisateur de Platform avec les requêtes et le journal mis en surbrillance.](../images/ui/query-log/logs.png)

## Personnalisation et recherche {#customize-and-search}

Les journaux de Query Service sont présentés dans un format de tableau personnalisable. Pour personnaliser les colonnes du tableau, cliquez sur l’icône de paramètres (![Icône Paramètres .](../images/ui/query-log/settings-icon.png)) à droite de l’écran. A [!UICONTROL Personnalisation du tableau] s’affiche, où chaque colonne peut être désélectionnée.

Vous pouvez également rechercher des logs relatifs à des modèles de requête spécifiques en saisissant le nom du modèle dans le champ de recherche.

![L’espace de travail Journal des requêtes avec la barre de recherche et la liste déroulante de gestion du tableau de colonnes mise en surbrillance.](../images/ui/query-log/customize-logs.png)

A [description de chacune des colonnes du tableau journal](./overview.md#log) se trouve dans la section Journal de la présentation de Query Service.

## Découverte des données de journal

Chaque ligne représente les données du journal d’une exécution de requête associée à un modèle de requête. Sélectionnez une ligne du tableau pour remplir la barre latérale droite avec les données de journal pour cette exécution.

![L&#39;espace de travail Journal des requêtes avec une ligne sélectionnée et les données du journal dans la barre latérale droite sont surlignées.](../images/ui/query-log/log-details.png)

Dans le panneau des détails du journal, vous pouvez sélectionner un nouveau jeu de données de sortie et voir ou copier la requête SQL complète utilisée dans l’exécution.

![Espace de travail Journal des requêtes avec une ligne sélectionnée et le jeu de données de sortie et la requête SQL mise en surbrillance.](../images/ui/query-log/edit-output-dataset.png)

>[!IMPORTANT]
>
>Certaines fonctionnalités de logs de requête sont actuellement dans une version limitée et ne sont pas disponibles pour tous les clients.

Vous pouvez également sélectionner un nom de modèle de requête à partir du champ [!UICONTROL Nom] pour accéder directement à la variable [!UICONTROL Détails du journal de requête] vue.

>[!NOTE]
>
>Si la requête a été créée à l’aide de l’API et qu’aucun nom de modèle n’a été fourni lors de l’initialisation, les premières douzaines de caractères de la requête SQL s’affichent à la place.

![La vue Détails du journal des requêtes .](../images/ui/query-log/query-log-details.png)

Une icône en forme de crayon se trouve à côté du nom de modèle de chaque ligne ou du fragment SQL (![Une icône en forme de crayon.](../images/ui/query-log/edit-icon.png)) que vous pouvez utiliser pour accéder à l’éditeur de requêtes. La requête est alors prérenseignée dans l’éditeur en vue de sa modification.

![L’espace de travail Journal des requêtes avec une icône en forme de crayon surlignée.](../images/ui/query-log/edit-query.png)

## Étapes suivantes

En lisant ce document, vous comprenez mieux comment accéder aux journaux de requêtes et les utiliser dans l’interface utilisateur de Query Service.

Voir la [présentation de l’interface utilisateur](./overview.md), ou le [guide de l’API Query Service](../api/getting-started.md) pour en savoir plus sur les fonctionnalités de Query Service.

Voir [document sur les requêtes de contrôle](./monitor-queries.md) pour découvrir comment Query Service améliore la visibilité des exécutions de requête planifiées.
