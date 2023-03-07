---
title: Destination Marketo Measure Ultimate
description: Découvrez comment connecter et activer des données vers la destination Marketo Measure Ultimate.
last-substantial-update: 2023-03-07T00:00:00Z
source-git-commit: 60ea8a608b85661f3a5d23dc3ba52cb0952fe2d2
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 38%

---


# Destination Marketo Measure Ultimate {#mmu-destination}

## Aperçu {#overview}

Marketo Measure (anciennement Bizible) permet aux marketeurs de savoir quels efforts marketing sont les plus efficaces pour générer des recettes et optimiser le retour sur investissement pour leur entreprise. Marketo Measure est une solution d’attribution marketing qui effectue automatiquement le suivi et les rapports sur les performances des canaux, ce qui vous permet d’identifier les canaux qui génèrent le plus d’engagement client et d’optimiser vos dépenses marketing en conséquence.

La destination active les flux de données B2B (business-to-business) de Adobe Experience Platform vers Marketo Measure. La carte est uniquement disponible pour les clients Marketo Measure Ultimate.

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination Marketo Measure, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination. Cette intégration :

* Répond aux exigences complexes en matière de données et de rapports de performance des grandes entreprises.
* Permet la création de rapports d’attribution B2B avec plusieurs systèmes de gestion de la relation client et d’automatisation marketing.
* Permet d’intégrer facilement des données de point de contact hors ligne tierces.

## Conditions préalables {#prerequisites}

Notez les conditions préalables suivantes pour la destination Marketo Measure :

* Le mappage des environnements de test Experience Platform doit être renseigné sur la page des paramètres de Marketo Measure par l’administrateur. Sans le mappage des environnements de test, vous ne pouvez pas terminer le workflow pour vous connecter à l’enregistrement et à l’activation des données de destination.
* Seuls les jeux de données des classes XDM B2B peuvent être exportés (voir, par exemple, les classes XDM Business Account et XDM Business Opportunity ). Vous ne pouvez pas importer plusieurs jeux de données de la même classe XDM B2B pour une source de données donnée.
* Chaque jeu de données ne peut être inclus que dans un seul flux de données vers la destination Marketo Measure.

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation des jeux de données]** | Vous exportez des jeux de données bruts qui ne sont pas groupés ou structurés selon les intérêts ou les qualifications de l’audience. En savoir plus sur [exportations de jeux de données](/help/destinations/destination-types.md#dataset-export-destinations). |
| Fréquence des exportations | **[!UICONTROL Lot]** | Cette destination de lot exporte les fichiers vers la plateforme Marketo Measure toutes les deux heures. En savoir plus sur [planification des exportations de jeux de données](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration de la destination, renseignez les champs répertoriés dans la section ci-dessous.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Gestion et activation des destinations de jeu de données]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lecture [(Version bêta) Exportation de jeux de données](/help/destinations/ui/export-datasets.md) pour obtenir des instructions détaillées sur l’exportation de jeux de données vers cette destination.

## Données exportées / Validation de l’exportation des données {#exported-data}

Pour valider une exportation réussie d’un jeu de données, vous pouvez vérifier que votre jeu de données a bien été transmis à votre [entrepôt de données Snowflake](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html?lang=en).

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

