---
title: Explorer, dépanner et vérifier l’ingestion par lots avec SQL
description: Découvrez comment comprendre et gérer le processus d’ingestion des données dans Adobe Experience Platform. Ce document explique comment vérifier les lots et interroger les données ingérées.
exl-id: 8f49680c-42ec-488e-8586-50182d50e900
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 0%

---

# Explorer, résoudre les problèmes et vérifier l’ingestion par lots avec SQL

Ce document explique comment vérifier et valider les enregistrements dans les lots ingérés avec SQL. Ce document vous apprend à :

- Accéder aux métadonnées du lot de jeux de données
- Résolution des problèmes et assurance de l’intégrité des données en interrogeant les lots

>[!NOTE]
>
>Certaines captures d’écran de ce guide sont extraites de [!DNL DBVisualizer]. Pour savoir comment [connecter Query Service à DBVisualizer](../clients/dbvisulaizer.md) ou à d’autres [outils de BI tiers](../clients/overview.md), consultez la documentation associée.

## Conditions préalables

Pour faciliter votre compréhension des concepts abordés dans ce document, vous devez posséder des connaissances sur les sujets suivants :

- **Ingestion des données** : consultez la [présentation de l’ingestion des données](../../ingestion/home.md) pour découvrir les principes de base de l’ingestion des données dans Experience Platform, y compris les différentes méthodes et processus impliqués.
- **Ingestion par lots** : consultez la présentation de l’API [ingestion par lots](../../ingestion/batch-ingestion/overview.md) pour découvrir les concepts de base de l’ingestion par lots. Plus précisément, ce qu’est un « lot » et comment il fonctionne dans le processus d’ingestion de données d’Experience Platform.
- **Métadonnées système dans les jeux de données** : consultez la [présentation du service de catalogue](../../catalog/home.md) pour savoir comment les champs de métadonnées système sont utilisés pour effectuer le suivi et l’interrogation des données ingérées.
- **Modèle de données d’expérience (XDM)** : consultez la [présentation de l’interface utilisateur des schémas](../../xdm/ui/overview.md) et les [ des principes de base de la composition des schémas](../../xdm/schema/composition.md) pour en savoir plus sur les schémas XDM et sur la manière dont ils représentent et valident la structure et le format des données ingérées dans Experience Platform.

## Accéder aux métadonnées du lot de jeux de données {#access-dataset-batch-metadata}

Pour vous assurer que les colonnes système (colonnes de métadonnées) sont incluses dans les résultats de la requête, utilisez la commande SQL `set drop_system_columns=false` dans votre Query Editor. Cela configure le comportement de votre session de requête SQL. Cette entrée doit être répétée si vous démarrez une nouvelle session.

Ensuite, pour afficher les champs système du jeu de données, exécutez une instruction SELECT all pour afficher les résultats du jeu de données, par exemple `select * from movie_data`. Les résultats comprennent deux nouvelles colonnes sur le côté droit `_acp_system_metadata` et `_ACP_BATCHID`. Les colonnes de métadonnées `_acp_system_metadata` et `_ACP_BATCHID` permettent d’identifier les partitions logiques et physiques des données ingérées.

![Interface utilisateur de DBVisualizer avec le tableau movie_data et ses colonnes de métadonnées affichées et mises en surbrillance.](../images/use-cases/movie_data-table-with-metadata-columns.png)

Lorsque des données sont ingérées dans Experience Platform, une partition logique leur est attribuée en fonction des données entrantes. Cette partition logique est représentée par `_acp_system_metadata.sourceBatchId`. Cet identifiant permet de regrouper et d’identifier logiquement les lots de données avant qu’ils ne soient traités et stockés.

Une fois les données traitées et ingérées dans le lac de données, une partition physique représentée par `_ACP_BATCHID` lui est attribuée. Cet identifiant reflète la partition de stockage réelle dans le lac de données où se trouvent les données ingérées.

### Utilisation de SQL pour comprendre les partitions logiques et physiques {#understand-partitions}

Pour comprendre comment les données sont regroupées et distribuées après ingestion, utilisez la requête suivante afin de compter le nombre de partitions physiques distinctes (`_ACP_BATCHID`) pour chaque partition logique (`_acp_system_metadata.sourceBatchId`).

```SQL
SELECT  _acp_system_metadata, COUNT(DISTINCT _ACP_BATCHID) FROM movie_data
GROUP BY _acp_system_metadata
```

Les résultats de cette requête sont affichés dans l’image ci-dessous.

![Résultats d’une requête pour afficher le nombre de partitions physiques distinctes pour chaque partition logique.](../images/use-cases/logical-and-physical-partition-count.png)

Ces résultats montrent que le nombre de lots d’entrée ne correspond pas nécessairement au nombre de lots de sortie, car le système détermine la manière la plus efficace de traiter par lots et de stocker les données dans le lac de données.

Pour les besoins de cet exemple, on suppose que vous avez ingéré un fichier CSV dans Experience Platform et créé un jeu de données appelé `drug_checkout_data`.

Le fichier `drug_checkout_data` est un ensemble profondément imbriqué de 35 000 enregistrements. Utilisez l’`SELECT * FROM drug_orders;` d’instructions SQL pour prévisualiser le premier ensemble d’enregistrements dans le jeu de données `drug_orders` basé sur JSON.

L’image ci-dessous présente un aperçu du fichier et de ses enregistrements.

![Aperçu du premier ensemble d’enregistrements dans le jeu de données drug_orders basé sur JSON.](../images/use-cases/drug-orders-preview.png)

### Utiliser SQL pour générer des informations sur le processus d’ingestion par lots {#sql-insights-on-batch-ingestion}

Utilisez l’instruction SQL ci-dessous pour fournir des informations sur la manière dont le processus d’ingestion de données a regroupé et traité les enregistrements d’entrée par lots.

```sql
SELECT _acp_system_metadata,
       Count(DISTINCT _acp_batchid) AS numoutputbatches,
       Count(_acp_batchid)          AS recordcount
FROM   drug_orders
GROUP  BY _acp_system_metadata 
```

Les résultats de la requête sont affichés dans l’image ci-dessous.

![Tableau montrant la répartition de la manière dont les lots d’entrée ont été maîtrisés à la fois avec des nombres d’enregistrements.](../images/use-cases/distribution-of-input-batches.png)

Les résultats démontrent l’efficacité et le comportement du processus d’ingestion de données. Bien que trois lots d&#39;entrées aient été créés — contenant chacun 2 000, 24000 et 9 000 enregistrements — lorsque les enregistrements ont été combinés et dédupliqués, il ne restait qu&#39;un seul lot.

>[!NOTE]
>
>Tous les enregistrements visibles dans un jeu de données sont ceux qui ont été correctement ingérés. Une ingestion par lots réussie ne signifie pas que tous les enregistrements envoyés à partir de l’entrée source sont présents. Vous devez rechercher les échecs d’ingestion de données pour trouver les lots/enregistrements qui n’y ont pas été intégrés.

## Valider un lot avec SQL {#validate-a-batch-with-SQL}

Ensuite, validez et vérifiez les enregistrements qui ont été ingérés dans le jeu de données avec SQL.

>[!TIP]
>
>Pour récupérer l’ID de lot et les enregistrements de requête associés à cet ID de lot, vous devez d’abord créer un lot dans Experience Platform. Si vous souhaitez tester le processus vous-même, vous pouvez ingérer des données CSV dans Experience Platform. Lisez le guide sur la façon de [mapper un fichier CSV à un schéma XDM existant à l’aide de recommandations générées par l’IA](../../ingestion/tutorials/map-csv/recommendations.md).

Une fois que vous avez ingéré un lot, vous devez accéder à l’onglet [!UICONTROL Activité des jeux de données] du jeu de données dans lequel vous avez ingéré des données.

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche pour ouvrir le tableau de bord [!UICONTROL Jeux de données]. Sélectionnez ensuite le nom du jeu de données dans l’onglet [!UICONTROL Parcourir] pour accéder à l’écran [!UICONTROL Activité du jeu de données].

![Tableau de bord Jeux de données de l’interface utilisateur d’Experience Platform avec Jeux de données en surbrillance dans le volet de navigation de gauche.](../images/use-cases/datasets-workspace.png)

La vue [!UICONTROL Activité du jeu de données] s’affiche. Cette vue contient les détails du jeu de données sélectionné. Elle inclut tous les lots ingérés qui s’affichent au format tableau.

Sélectionnez un lot dans la liste des lots disponibles et copiez le [!UICONTROL Identifiant du lot] dans le panneau des détails à droite.

![Interface utilisateur des jeux de données Experience Platform affichant les enregistrements ingérés avec un identifiant de lot en surbrillance.](../images/use-cases/batch-id.png)

Ensuite, utilisez la requête suivante pour récupérer tous les enregistrements qui ont été inclus dans le jeu de données dans le cadre de ce lot :

```sql
SELECT * FROM movie_data
WHERE  _acp_batchid='01H00BKCTCADYRFACAAKJTVQ8P' 
LIMIT 1;
```

Le mot-clé `_ACP_BATCHID` est utilisé pour filtrer l’[!UICONTROL ID de lot].

>[!TIP]
>
>La clause `LIMIT` est utile si vous souhaitez limiter le nombre de lignes affichées, mais une condition de filtre est plus souhaitable.

Lorsque vous exécutez cette requête dans le Query Editor, les résultats sont tronqués à 100 lignes. Query Editor est conçu pour offrir des aperçus rapides et faciliter la recherche. Pour récupérer jusqu’à 50 000 lignes, vous pouvez utiliser un outil tiers tel que DBVisualizer ou DBeaver.

## Étapes suivantes {#next-steps}

En lisant ce document, vous avez appris les principes de base de la vérification et de la validation des enregistrements dans les lots ingérés dans le cadre du processus d’ingestion de données. Vous avez également obtenu des informations sur l’accès aux métadonnées des lots de jeux de données, la compréhension des partitions logiques et physiques et l’interrogation de lots spécifiques à l’aide de commandes SQL. Ces connaissances peuvent vous aider à assurer l’intégrité des données et à optimiser le stockage de vos données sur Experience Platform.

Ensuite, vous devez vous entraîner à ingérer des données pour appliquer les concepts appris. Ingérez un exemple de jeu de données dans Experience Platform avec les fichiers d’exemple fournis ou vos propres données. Si vous ne l’avez pas déjà fait, consultez le tutoriel sur la [ingestion de données dans Adobe Experience Platform](../../ingestion/tutorials/ingest-batch-data.md).

Vous pouvez également apprendre à [connecter et vérifier Query Service à diverses applications de bureau clientes](../clients/overview.md) afin d’améliorer vos fonctionnalités d’analyse des données.
