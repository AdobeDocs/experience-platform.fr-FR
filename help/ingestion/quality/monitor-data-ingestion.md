---
keywords: Experience Platform ; accueil ; rubriques populaires ; surveillance ; surveillance ; flux de données ; surveillance ; analyse ; assimilation de données ; assimilation de données ; enregistrements de vues ; lots de vues ;
solution: Experience Platform
title: Analyse de l'importation des données
topic: aperçu
description: Ce guide d’utilisation fournit des étapes détaillées sur la manière de surveiller vos données au sein de l’interface utilisateur d’Adobe Experience Platform. Ce guide nécessite que vous possédiez déjà un Adobe ID et un accès à Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 67%

---


# Surveillance de l’ingestion des données

L’ingestion des données vous permet d’ingérer vos données dans Adobe Experience Platform. Vous pouvez utiliser l’assimilation par lot, qui vous permet d’insérer vos données à l’aide de différents types de fichiers (tels que les fichiers CSV), ou l’assimilation en flux continu, qui vous permet d’assimiler vos données à [!DNL Platform] à l’aide de points de terminaison en flux continu en temps réel.

Ce guide d’utilisation fournit des étapes détaillées sur la manière de surveiller vos données au sein de l’interface utilisateur d’Adobe Experience Platform. Ce guide nécessite que vous possédiez déjà un Adobe ID et un accès à Adobe Experience Platform.

## Surveillance de l’ingestion des données en continu de bout en bout

Dans l’[interface utilisateur d’Experience Platform](https://platform.adobe.com), cliquez sur **[!UICONTROL Surveillance]** dans le menu de navigation de gauche, puis cliquez sur **[!UICONTROL Diffusion en continu de bout en bout]**.

![](../images/quality/monitor-data-flows/click-streaming-end-to-end.png)

La page de surveillance **[!UICONTROL Diffusion en continu de bout en bout]** apparaît. Cet espace de travail fournit un graphique qui affiche le taux de événements reçus en flux continu par [!DNL Platform], un graphique qui affiche le taux de événements en flux continu qui ont été traités avec succès par [[!DNL Real-time Customer Profile]](../../profile/home.md), ainsi qu&#39;une liste détaillée des données entrantes.

![](../images/quality/monitor-data-flows/list-streams.png)

Par défaut, le graphique supérieur montre le taux d&#39;ingestion au cours des sept derniers jours. Vous pouvez ajuster cette période pour afficher diverses périodes de temps en cliquant sur le bouton en surbrillance.

![](../images/quality/monitor-data-flows/list-streams-focus-on-top-graph.png)

Le graphique du bas montre le taux de événements en flux continu traités avec succès par [!DNL Profile] au cours des sept derniers jours. Vous pouvez ajuster cette période pour afficher diverses périodes de temps en cliquant sur le bouton en surbrillance.

>[!NOTE]
>
>Pour que les données s’affichent sur ce graphique, les données doivent être **explicitement** activées pour [!DNL Profile]. Pour savoir comment activer les données en flux continu pour [!DNL Profile], consultez le [guide d&#39;utilisateur des jeux de données](../../catalog/datasets/user-guide.md#enable-a-dataset-for-real-time-customer-profile).

![](../images/quality/monitor-data-flows/list-streams-focus-on-bottom-graph.png)

Sous les graphiques se trouve une liste de tous les enregistrements d’assimilation en flux continu qui correspondent à la plage de dates affichée ci-dessus. Chaque lot répertorié affiche son identifiant, le nom du jeu de données, le moment de sa dernière mise à jour, le nombre d’enregistrements dans le lot ainsi que le nombre d’erreurs (le cas échéant). En cliquant sur l’un des enregistrements, vous trouverez des informations plus détaillées le concernant.

![](../images/quality/monitor-data-flows/list-streams-focus-on-streams.png)

### Affichage des enregistrements en continu

Lorsque vous affichez les détails d’un enregistrement diffusé en continu réussi, des informations comme le nombre d’enregistrements ingérés, la taille du fichier et les heures de début et de fin de l’ingestion s’affichent.

![](../images/quality/monitor-data-flows/successful-streaming-record.png)

Les détails de l’échec d’un enregistrement en continu affichent les mêmes informations qu’un enregistrement réussi.

![](../images/quality/monitor-data-flows/failed-batch.png)

De plus, les enregistrements en échec fournissent des informations sur les erreurs qui se sont produites au cours du traitement du lot. Dans l’exemple ci-dessous, une erreur système s’est produite lors de la validation de l’identifiant du jeu de données depuis le catalogue.

![](../images/quality/monitor-data-flows/failed-batch-details.png)

## Surveillance de l’ingestion des données du lot de bout en bout

Dans le [[!DNL Experience Platform UI]](https://platform.adobe.com), cliquez sur **[!UICONTROL Surveillance]** dans le menu de navigation de gauche.

![](../images/quality/monitor-data-flows/click-monitoring.png)

La page de surveillance de **[!UICONTROL lot de bout en bout]** apparaît et affiche une liste des lots ingérés précédemment. En cliquant sur l’un des lots, vous pourrez consulter des informations plus détaillées sur cet enregistrement.

![](../images/quality/monitor-data-flows/list-batches.png)

### Affichage des lots

Lorsque vous affichez les détails d’un lot réussi, des informations comme le nombre d’enregistrements ingérés, la taille du fichier et les heures de début et de fin de l’ingestion s’affichent.

![](../images/quality/monitor-data-flows/successful-batch.png)

Les détails d’un lot en échec affichent les mêmes informations qu’un lot réussi en plus du nombre d’enregistrements en échec.

![](../images/quality/monitor-data-flows/failed-streaming-record.png)

De plus, les lots en échec fournissent des informations sur les erreurs qui se sont produites au cours du traitement du lot. Dans l’exemple ci-dessous, une erreur s’est produite avec le lot ingéré, car il utilisait un champ inconnu de `_experience`.

![](../images/quality/monitor-data-flows/failed-streaming-record-details.png)