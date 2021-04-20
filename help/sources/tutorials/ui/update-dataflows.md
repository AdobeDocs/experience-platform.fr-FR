---
keywords: Experience Platform ; accueil ; rubriques populaires ; mettre à jour les flux de données ; modifier la planification
description: Ce didacticiel décrit les étapes de mise à jour d'un calendrier de flux de données, y compris sa fréquence d'assimilation et son taux d'intervalle, à l'aide de l'espace de travail Sources.
solution: Experience Platform
title: Mise à jour d’un flux de données de connexion source dans l’interface utilisateur
topic: overview
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
translation-type: tm+mt
source-git-commit: 3a36996b43760bc9161b8d4750a1121e9ada8d30
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 7%

---

# Mettre à jour les flux de données dans l’interface utilisateur

Ce didacticiel décrit les étapes à suivre pour mettre à jour un flux de données de sources existantes, y compris des informations sur la modification d&#39;un calendrier et d&#39;un mappage de flux de données, à l&#39;aide de l&#39;espace de travail [!UICONTROL Sources].

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

- [Sources](../../home.md) : Experience Platform permet l’assimilation de données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de plate-forme.
- [Environnements de test](../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

## Modifier le mappage

>[!NOTE]
>
>La fonction de mappage des modifications n’est actuellement pas prise en charge pour les sources suivantes : Adobe Analytics, Adobe Audience Manager, HTTP API et [!DNL Marketo Engage].

Dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Sélectionnez **[!UICONTROL Flux de données]** dans l&#39;en-tête supérieur à la vue d&#39;une liste de flux de données existants.

![catalogue](../../images/tutorials/update-dataflows/catalog.png)

La page [!UICONTROL Flux de données] contient une liste de tous les flux de données existants, y compris des informations sur leur état d&#39;exécution, leur date de dernière exécution et leur nom de compte.

Sélectionnez l’icône de filtre ![filter](../../images/tutorials/update/filter.png) en haut à gauche pour lancer le panneau de tri.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

Le panneau de tri fournit une liste de toutes les sources disponibles. Vous pouvez sélectionner plusieurs sources dans la liste pour accéder à une sélection filtrée de flux de données appartenant à différentes sources.

Sélectionnez la source à utiliser pour afficher une liste de ses flux de données existants. Une fois que vous avez identifié le flux de données à mettre à jour, sélectionnez les points de suspension (`...`) en regard du nom du compte.

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

Un menu déroulant s’affiche, vous offrant des options de mise à jour du flux de données que vous avez sélectionné. À partir de là, vous pouvez choisir de mettre à jour les jeux de correspondances d’un flux de données et le planning d’assimilation. Vous pouvez également sélectionner des options pour inspecter le flux de données dans le tableau de bord de surveillance, ainsi que désactiver ou supprimer le flux de données.

Sélectionnez **[!UICONTROL Modifier la source]** pour mettre à jour son mappage.

![edit-dataflow](../../images/tutorials/update-dataflows/edit-dataflow.png)

L’étape [!UICONTROL Ajouter les données] apparaît. Sélectionnez le format de données approprié pour examiner le contenu des données sélectionnées, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

La page [!UICONTROL Mappage] fournit une interface dans laquelle vous pouvez ajouter et supprimer des jeux de mappages associés à votre jeu de données.

>[!TIP]
>
>Les mises à jour de mappage ne sont appliquées qu’aux exécutions de flux de données planifiées à l’avenir.

Sélectionnez **[!UICONTROL Ajouter un nouveau mappage]** pour ajouter un nouveau jeu de mappages.

![add-new-mapping](../../images/tutorials/update-dataflows/add-new-mapping.png)

Ensuite, entrez l’attribut de champ source approprié et les valeurs de champ XDM de cible pour terminer votre jeu de correspondances supplémentaire. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![nouveau mappage-ajouté](../../images/tutorials/update-dataflows/new-mapping-added.png)

L&#39;étape [!UICONTROL Planification] s&#39;affiche, ce qui vous permet de mettre à jour la planification d&#39;assimilation de votre flux de données et d&#39;assimiler automatiquement les données source sélectionnées avec les mises en correspondance mises à jour.

>[!NOTE]
>
>Vous ne pouvez pas mettre à jour les jeux de correspondances pour les flux de données qui étaient planifiés pour une assimilation unique et que le temps de début est passé.

![scheduling](../../images/tutorials/update-dataflows/scheduling.png)

Dans la page [!UICONTROL Détails du flux de données], vous pouvez fournir un nom et une description mis à jour pour votre flux de données et reconfigurer le seuil d&#39;erreur de votre flux de données.

Une fois les valeurs mises à jour fournies, sélectionnez **[!UICONTROL Suivant]**.

![détails du flux de données](../../images/tutorials/update-dataflows/dataflow-detail.png)

L&#39;étape **[!UICONTROL Réviser]** s&#39;affiche, vous permettant de vérifier votre flux de données avant qu&#39;il ne soit mis à jour.

Une fois que vous avez passé en revue votre flux de données, sélectionnez **[!UICONTROL Terminer]** et attendez un certain temps pour que le flux de données avec les nouveaux jeux de mappage soit créé.

![examiner](../../images/tutorials/update-dataflows/review.png)

## Modifier le planning

Pour modifier la planification d&#39;assimilation d&#39;un flux de données existant, sélectionnez les ellipses (`...`) en regard d&#39;un nom de flux de données, puis sélectionnez **[!UICONTROL Modifier la planification]** dans le menu déroulant.

![modifier-planifier](../../images/tutorials/update-dataflows/edit-schedule.png)

La boîte de dialogue **[!UICONTROL Modifier la planification]** contient des options permettant de mettre à jour la fréquence d&#39;assimilation et le taux d&#39;intervalle de votre flux de données. Une fois que vous avez défini les valeurs de fréquence et d’intervalle mises à jour, sélectionnez **[!UICONTROL Enregistrer]**.

>[!NOTE]
>
>Vous ne pouvez pas replanifier un flux de données planifié pour une assimilation unique.

![boîte de dialogue de planification](../../images/tutorials/update-dataflows/schedule-dialog-box.png)

| Planification | Description |
| ---------- | ----------- |
| Fréquence | Fréquence à laquelle le flux de données va collecter les données. Les valeurs acceptables pour la modification de la planification des fréquences pour un flux de données existant sont les suivantes : `minute`, `hour`, `day` ou `week`. |
| Intervalle | L’intervalle désigne la période entre deux exécutions consécutives de flux. La valeur de l’intervalle doit être un entier non nul et doit être supérieure ou égale à `15`. |

Après quelques instants, une boîte de confirmation s’affiche en bas de l’écran pour confirmer une mise à jour réussie.

![schedule-verify](../../images/tutorials/update-dataflows/schedule-confirm.png)

## Étapes suivantes

En suivant ce didacticiel, vous avez utilisé l&#39;espace de travail [!UICONTROL Sources] pour mettre à jour le calendrier d&#39;assimilation et les jeux de mappage de votre flux de données.

Pour savoir comment exécuter ces opérations par programmation à l&#39;aide de l&#39;API [!DNL Flow Service], reportez-vous au didacticiel de [mise à jour des flux de données à l&#39;aide de l&#39;API Flow Service](../../tutorials/api/update-dataflows.md).
