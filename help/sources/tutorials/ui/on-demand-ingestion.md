---
title: Ingestion à la demande pour les flux de données de sources dans l’interface utilisateur
description: Découvrez comment créer des flux de données à la demande pour vos connexions source à l’aide de l’interface utilisateur Experience Platform.
source-git-commit: ce1e6c08d1e53346c11f9746cea524689f402031
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 11%

---

# Ingestion à la demande pour les flux de données de sources dans l’interface utilisateur

Vous pouvez utiliser l’ingestion à la demande pour déclencher une itération d’exécution de flux d’un flux de données existant à l’aide de l’espace de travail sources dans l’interface utilisateur de Adobe Experience Platform.

Ce document décrit les étapes à suivre pour créer des flux de données à la demande pour les sources, ainsi que la manière de retenter les exécutions de flux qui ont été traitées ou qui ont échoué.

>[!BEGINSHADEBOX]

**Qu’est-ce qu’une exécution de flux ?**

Les exécutions de flux représentent une instance d’exécution de flux de données. Par exemple, si un flux de données est planifié pour s’exécuter toutes les heures à 9h00, 10h00 et 11h00, vous aurez trois instances d’une exécution de flux. Les exécutions de flux sont spécifiques à votre organisation.

>[!ENDSHADEBOX]

## Prise en main

Ce document nécessite une compréhension pratique des composants suivants de l’Experience Platform :

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform.
* [Flux de données](../../../dataflows/home.md): un flux de données est une représentation des tâches de données qui déplacent des données dans Platform. Les flux de données sont configurés sur différents services, ce qui permet de déplacer des données des connecteurs sources vers des jeux de données cibles, vers Identity Service et Real-time Customer Profile, ainsi que vers les destinations.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une seule instance de Platform en environnements virtuels distincts afin de favoriser le développement et l’évolution d’applications d’expérience digitale.

## Création d’un flux de données à la demande {#create-a-dataflow-on-demand}

Accédez au *[!UICONTROL Flux de données]* de l’espace de travail des sources. À partir de là, recherchez le flux de données que vous souhaitez exécuter à la demande, puis sélectionnez les ellipses (**`...`**) en regard de votre nom de flux de données.

![Liste des flux de données dans l’espace de travail des sources.](../../images/tutorials/on-demand/select-dataflow.png)

Ensuite, sélectionnez **[!UICONTROL Exécuter à la demande]** dans le menu déroulant qui s’affiche.

![Menu déroulant avec l’option Exécuter à la demande sélectionnée.](../../images/tutorials/on-demand/run-on-demand.png)

Configurez le planning de votre ingestion à la demande. Sélectionnez la variable **[!UICONTROL Heure de début de l’ingestion]**, la variable **[!UICONTROL Heure de début de la période]**, et la variable **[!UICONTROL Date et heure de fin de la période]**.

| Configuration de la planification | Description |
| --- | --- |
| [!UICONTROL Heure de début de l’ingestion] | Heure de début planifiée en UTC du début du flux de données à la demande. |
| [!UICONTROL Heure de début de la période] | Date et heure de début à partir desquelles les données seront extraites. |
| [!UICONTROL Date et heure de fin de la période] | Date et heure de fin auxquelles les données seront extraites. |

Sélectionner **[!UICONTROL Planification]** et laissez quelques instants à votre flux de données à la demande pour se déclencher.

![Fenêtre de configuration de planification pour l’ingestion à la demande.](../../images/tutorials/on-demand/configure-schedule.png)

Sélectionnez le nom de votre flux de données pour afficher votre activité de flux de données. Vous y trouverez la liste des exécutions de vos flux de données qui ont été traitées. Sélectionnez une exécution de flux de données, puis sélectionnez **[!UICONTROL Réessayer]** à partir du rail de droite pour relancer l’ingestion pour une itération d’exécution de flux de données sélectionnée.

![Liste des exécutions de flux traités pour un flux de données sélectionné.](../../images/tutorials/on-demand/processed.png)

Sélectionner **[!UICONTROL Planifié]** pour afficher la liste des exécutions de flux de données planifiées pour une ingestion ultérieure.

![Liste des exécutions de flux planifiées pour un flux de données sélectionné.](../../images/tutorials/on-demand/scheduled.png)

## Étapes suivantes

En lisant ce document, vous avez appris à créer des exécutions de flux à la demande pour les flux de données de sources existants. Pour plus d’informations sur les sources, consultez la [présentation des sources](../../home.md)