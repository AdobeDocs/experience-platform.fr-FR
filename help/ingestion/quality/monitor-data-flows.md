---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Analyse de l'assimilation des données
topic: overview
translation-type: tm+mt
source-git-commit: 9cbc22a34613aeb58a2c5090b10978ae4428dbdb
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Analyse de l&#39;assimilation des données

L’assimilation de données vous permet d’assimiler vos données à Adobe Experience Platform. Vous pouvez utiliser l’assimilation par lot, qui vous permet d’insérer vos données à l’aide de différents types de fichiers (tels que les fichiers CSV), ou l’assimilation en flux continu, qui vous permet d’assimiler vos données à la plate-forme à l’aide de points de terminaison de flux continu en temps réel.

Ce guide d’utilisateur décrit la procédure à suivre pour surveiller vos données dans l’interface utilisateur d’Adobe Experience Platform. Ce guide nécessite que vous disposiez d’un Adobe ID et d’un accès à Adobe Experience Platform.

## Surveiller l&#39;assimilation des données de bout en bout en flux continu

Dans l’interface utilisateur [de la plateforme](https://platform.adobe.com)d’expérience, cliquez sur **Surveillance** dans le menu de navigation de gauche, puis cliquez sur **Diffusion en continu de bout en bout**.

![](../images/quality/monitor-data-flows/click-streaming-end-to-end.png)

La page de surveillance *en flux continu de bout en bout* s’affiche. Cet espace de travail fournit un graphique qui affiche le taux de événements en flux continu reçus par Plateforme, un graphique qui affiche le taux de événements en flux continu qui ont été traités avec succès par Profil [client en temps](../../profile/home.md)réel, ainsi qu’une liste détaillée des données entrantes.

![](../images/quality/monitor-data-flows/list-streams.png)

Par défaut, le graphique supérieur montre le taux d&#39;ingestion au cours des sept derniers jours. Cette plage de dates peut être ajustée pour afficher diverses périodes en cliquant sur le bouton en surbrillance.

![](../images/quality/monitor-data-flows/list-streams-focus-on-top-graph.png)

Le graphique du bas montre le taux de événements en flux continu traités avec succès par Profil au cours des sept derniers jours. Cette plage de dates peut être ajustée pour afficher diverses périodes en cliquant sur le bouton en surbrillance.

> [!NOTE] Pour que les données s’affichent sur ce graphique, elles doivent être **explicitement** activées pour le Profil. Pour savoir comment activer la diffusion en continu des données pour le Profil, consultez le guide [d’utilisation](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile)des jeux de données.

![](../images/quality/monitor-data-flows/list-streams-focus-on-bottom-graph.png)

Sous les graphiques se trouve une liste de tous les enregistrements d’assimilation en flux continu qui correspondent à la plage de dates affichée ci-dessus. Chaque lot répertorié affiche son ID, son nom de jeu de données, sa dernière mise à jour, le nombre d&#39;enregistrements du lot ainsi que le nombre d&#39;erreurs (le cas échéant). Vous pouvez cliquer sur l’un des enregistrements pour obtenir des informations plus détaillées sur cet enregistrement.

![](../images/quality/monitor-data-flows/list-streams-focus-on-streams.png)

### Affichage des enregistrements de diffusion en continu

Lors de l’affichage des détails d’un enregistrement en flux continu réussi, des informations telles que le nombre d’enregistrements ingérés, la taille du fichier, le début d’assimilation et les heures de fin s’affichent.

![](../images/quality/monitor-data-flows/successful-streaming-record.png)

Les détails d’un enregistrement de diffusion en continu ayant échoué affichent les mêmes informations qu’un enregistrement réussi.

![](../images/quality/monitor-data-flows/failed-batch.png)

En outre, les enregistrements en échec fournissent des détails sur les erreurs survenues lors du traitement du lot. Dans l&#39;exemple ci-dessous, une erreur système s&#39;est produite lors de la validation du datasetId à partir du catalogue.

![](../images/quality/monitor-data-flows/failed-batch-details.png)

## Surveiller l&#39;assimilation des données de bout en bout par lot

Dans l’interface utilisateur [de la plateforme](https://platform.adobe.com)d’expérience, cliquez sur **Surveillance** dans le menu de navigation de gauche.

![](../images/quality/monitor-data-flows/click-monitoring.png)

La page de surveillance **de bout en bout** du lot s’affiche, affichant une liste des lots précédemment assimilés. Vous pouvez cliquer sur l’un des lots pour obtenir des informations plus détaillées sur cet enregistrement.

![](../images/quality/monitor-data-flows/list-batches.png)

### Affichage des lots

Lors de l’affichage des détails d’un lot réussi, des informations telles que le nombre d’enregistrements ingérés, la taille du fichier, le début d’assimilation et les heures de fin s’affichent.

![](../images/quality/monitor-data-flows/successful-batch.png)

Les détails d&#39;un lot en échec affichent les mêmes informations qu&#39;un lot réussi, avec l&#39;ajout du nombre d&#39;enregistrements en échec.

![](../images/quality/monitor-data-flows/failed-streaming-record.png)

En outre, les lots en échec fournissent des détails sur les erreurs survenues lors du traitement du lot. Dans l&#39;exemple ci-dessous, une erreur s&#39;est produite avec le lot assimilé, car il a utilisé un champ inconnu de `_experience`.

![](../images/quality/monitor-data-flows/failed-streaming-record-details.png)