---
title: Ingestion à la demande des flux de données des sources dans l’interface utilisateur
description: Découvrez comment créer des flux de données à la demande pour vos connexions source à l’aide de l’interface utilisateur d’Experience Platform.
exl-id: e5a70044-2484-416a-8098-48e6d99c2d98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# Ingestion à la demande des flux de données sources dans l’interface utilisateur

Vous pouvez utiliser l’ingestion à la demande pour déclencher une itération d’exécution de flux d’un flux de données existant à l’aide de l’espace de travail Sources dans l’interface utilisateur de Adobe Experience Platform.

Ce document vous fournit des instructions sur la création de flux de données à la demande pour les sources, ainsi que sur la manière de réessayer les exécutions de flux qui ont été traitées ou ont échoué.

>[!BEGINSHADEBOX]

**Qu’est-ce qu’une exécution de flux ?**

Les exécutions de flux représentent une instance d’exécution de flux de données. Par exemple, si un flux de données est planifié pour s’exécuter toutes les heures à 9 h, 10 h et 11 h, trois instances d’exécution de flux se produisent. Les exécutions de flux sont spécifiques à votre organisation.

>[!ENDSHADEBOX]

## Commencer

>[!NOTE]
>
>Pour créer une exécution de flux, vous devez d’abord disposer de l’identifiant de flux d’un flux de données planifié pour une ingestion unique.

Ce document nécessite une compréhension du fonctionnement des composants suivants d’Experience Platform :

* [Sources](../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Flux de données](../../../dataflows/home.md) : un flux de données est une représentation des tâches de données qui déplacent ces dernières dans Experience Platform. Les flux de données sont configurés sur différents services, ce qui permet de déplacer les données des connecteurs sources vers des jeux de données cibles, vers le service d’identités et le profil client en temps réel, ainsi que vers des destinations.
* [Sandbox](../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Créer un flux de données à la demande {#create-a-dataflow-on-demand}

Accédez à l’onglet *[!UICONTROL Flux de données]* de l’espace de travail des sources. À partir de là, recherchez le flux de données à exécuter à la demande, puis sélectionnez les points de suspension (**`...`**) à côté de votre nom de flux de données.

![Liste des flux de données dans l’espace de travail des sources.](../../images/tutorials/on-demand/select-dataflow.png)

Sélectionnez ensuite **[!UICONTROL Exécuter à la demande]** dans le menu déroulant qui s’affiche.

![Un menu déroulant avec l’option Exécuter à la demande sélectionnée.](../../images/tutorials/on-demand/run-on-demand.png)

Configurez le planning de votre ingestion à la demande. Sélectionnez les options **[!UICONTROL Heure de début de l’ingestion]**, **[!UICONTROL Heure de début de la période]** et **[!UICONTROL Heure de fin de la période]**.

| Configuration de la planification | Description |
| --- | --- |
| [!UICONTROL Heure de début de l’ingestion] | Heure planifiée à laquelle l’exécution du flux à la demande commencera. |
| [!UICONTROL Heure de début de la période] | Date et heure au plus tôt à partir desquelles les données seront récupérées. |
| [!UICONTROL Heure de fin de la période] | Date et heure de récupération des données. |

Sélectionnez **[!UICONTROL Planifier]** et patientez quelques instants le temps que votre flux de données à la demande se déclenche.

![Fenêtre de configuration de la planification pour l’ingestion à la demande.](../../images/tutorials/on-demand/configure-schedule.png)

Sélectionnez le nom de votre flux de données pour afficher votre activité de flux de données. Vous trouverez ici une liste de vos exécutions de flux de données qui ont été traitées. Vous pouvez réexécuter des itérations individuelles de vos exécutions de flux de données, qu’elles aient échoué ou réussi. Pour les itérations d’exécution ayant échoué, vous pouvez utiliser **[!UICONTROL Réessayer]** pour relancer l’exécution après avoir diagnostiqué et corrigé les erreurs qui ont pu se produire pendant le processus de création.

![Liste des exécutions de flux traitées pour un flux de données sélectionné.](../../images/tutorials/on-demand/processed.png)

Sélectionnez **[!UICONTROL Planifié]** pour afficher la liste des exécutions de flux de données planifiées pour une ingestion ultérieure.

![Liste des exécutions de flux planifiées pour un flux de données sélectionné.](../../images/tutorials/on-demand/scheduled.png)

## Étapes suivantes

En lisant ce document, vous avez appris à créer des exécutions de flux à la demande pour les flux de données sources existants. Pour plus d’informations sur les sources, consultez la [présentation des sources](../../home.md)
