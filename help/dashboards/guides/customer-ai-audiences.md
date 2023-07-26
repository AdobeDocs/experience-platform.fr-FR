---
title: Widgets Customer AI du tableau de bord Audiences
description: Découvrez comment Customer AI fournit des informations importantes sur l’attrition ou la propension des audiences Real-time Customer Profile de votre entreprise.
hide: true
hidefromtoc: true
source-git-commit: 162ef470751b9fb252658cff4b43595ddb7fe5d5
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 10%

---

# Widgets de l’IA dédiée aux clients du tableau de bord Audiences {#customer-ai-audiences-widgets}

Customer AI est utilisé pour générer des scores de propension personnalisés tels que les taux d’attrition et de conversion de profils individuels à grande échelle. Pour ce faire, Customer AI analyse les données d’événement d’expérience client existantes afin de prédire **scores de propension à l’attrition ou à la conversion**. Ces modèles de propension des clients à haute précision permettent une segmentation et un ciblage plus précis. La variable [distribution des scores](#customer-ai-distribution-of-scores) et [résumé de notation](#customer-ai-scoring-summary) les insights montrent la division de votre audience. Ils mettent en évidence les profils qui correspondent à une propension élevée/faible/moyenne et la manière dont ils sont répartis dans les nombres de profils.

<!-- 
THe links when required
* [[!UICONTROL Customer AI scoring summary]](#customer-ai-scoring-summary)
* [[!UICONTROL Customer AI distribution of scores]](#customer-ai-distribution-of-scores) 
-->

## [!UICONTROL Distribution des scores par Customer AI] {#customer-ai-distribution-of-scores}

>[!CONTEXTUALHELP]
>id="platform_dashboards_audiences_distributionOfScores"
>title="Distribution des scores"
>abstract="Ce widget visualise la distribution du nombre total de profils en fonction de leurs scores de propension, par incréments de 5 %. La distribution du nombre de profils est déterminée par le modèle AI et la stratégie de fusion sélectionnée. Vous pouvez modifier le modèle AI dans le menu déroulant sous le titre du widget."

La variable [!UICONTROL Distribution des scores par Customer AI] widget classe le nombre total de profils en fonction de leurs scores de propension. La distribution du nombre de profils est déterminée par le modèle AI et la stratégie de fusion sélectionnée, puis visualisée par incréments de 5 % qui indiquent leur propension. Le nombre de profils est fourni le long de l’axe Y et les scores de propension sont fournis le long de l’axe X.

>[!NOTE]
>
>Si la visualisation est un score de propension à la conversion, les scores élevés sont en vert et les scores faibles en rouge. Si vous prédisez la propension à l’attrition, les scores élevés sont en rouge et les scores faibles en vert. Le compartiment moyen reste jaune quel que soit le type de propension sélectionné.

Le modèle AI qui détermine les scores de propension est sélectionné dans le sélecteur de liste déroulante sous le titre du widget. La liste déroulante contient une liste de tous les modèles Customer AI configurés. Sélectionnez le modèle d’IA approprié à votre analyse dans la liste des modèles disponibles. Si aucun modèle Customer AI n’est disponible, un message du widget vous invite à configurer au moins un modèle Customer AI et fournit un lien hypertexte vers la page de configuration du modèle Customer AI. Consultez la documentation pour obtenir des instructions sur [Configuration d’une instance Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>Sélectionnez la liste déroulante juste en dessous de l’onglet d’aperçu pour modifier la stratégie de fusion qui détermine les profils inclus dans l’analyse. Voir la section sur [stratégies de fusion](#merge-policies) pour une brève description, ou la variable [présentation des stratégies de fusion](../../profile/merge-policies/overview.md) pour plus d’informations.

Pour accéder à la page d’informations détaillées du modèle Customer AI sélectionné, sélectionnez **[!UICONTROL Affichage des détails du modèle]**.

![Le tableau de bord Audiences Experience Platform avec la variable [!UICONTROL Distribution des scores par Customer AI] widget [!UICONTROL Affichage des détails du modèle] surlignée.](../images/segments/customer-ai-distribution-of-scores.png)

La page d’informations détaillées sur les modèles s’affiche.

![Page d’informations de Customer AI.](../images/profiles/customer-ai-insights-page.png)

Pour plus d’informations sur Customer AI, voir [guide de l’interface utilisateur de discover insights](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## [!UICONTROL Résumé de notation de Customer AI] {#customer-ai-scoring-summary}

>[!CONTEXTUALHELP]
>id="platform_dashboards_audiences_scoringSummary"
>title="Résumé de notation"
>abstract="Ce widget affiche le nombre total de profils notés et les classe en compartiments de propension élevée, moyenne et faible. Le graphique en anneau illustre la composition proportionnelle des profils totaux selon la propension élevée, moyenne et faible."

Ce widget affiche le nombre total de profils notés et les classe en compartiments de propension élevée, moyenne et faible sous la forme respectivement de vert, de jaune et de rouge. Un graphique en anneau est utilisé pour illustrer la composition proportionnelle des profils totaux entre les propensions élevées, moyennes et faibles, en vert, jaune et rouge, respectivement. Un profil est admissible pour une propension élevée à plus de 75 ans, une propension moyenne entre 25 et 74 ans et une propension faible à moins de 24 ans. Une légende indique le code couleur et les seuils de propension. Les valeurs de profil correspondant aux propensions élevées, moyennes et faibles s’affichent dans une boîte de dialogue lorsque le curseur survole la section correspondante du graphique en anneau.

>[!NOTE]
>
>Si la visualisation est un score de propension à la conversion, les scores élevés sont en vert et les scores faibles en rouge. Si vous prédisez la propension à l’attrition, les scores élevés sont en rouge et les scores faibles en vert. Le compartiment moyen reste jaune quel que soit le type de propension sélectionné.

Le menu déroulant sous le titre du widget fournit une liste de tous les modèles Customer AI configurés. Sélectionnez le modèle d’IA approprié à votre analyse dans la liste des modèles disponibles. Si aucun modèle Customer AI n’est disponible, un message du widget vous invite à configurer au moins un modèle Customer AI et fournit un lien hypertexte vers la page de configuration du modèle Customer AI. Consultez la documentation relative à [Configuration d’une instance Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md) pour obtenir des instructions détaillées.

>[!NOTE]
>
>Le nombre total de profils calculés dépend de la stratégie de fusion choisie. Pour modifier la stratégie de fusion utilisée, sélectionnez la liste déroulante juste en dessous de l’onglet d’aperçu. Voir la section sur [stratégies de fusion](#merge-policies) pour une brève description, ou la variable [présentation des stratégies de fusion](../../profile/merge-policies/overview.md) pour plus d’informations.

![Le tableau de bord Audiences Experience Platform avec le widget de résumé de notation de Customer AI mis en surbrillance.](../images/segments/customer-ai-scoring-summary.png)

Sélectionner **[!UICONTROL Affichage des détails du modèle]** pour accéder à la page d’informations détaillées du modèle Customer AI sélectionné. Pour plus d’informations sur Customer AI, voir [guide de l’interface utilisateur de discover insights](../../intelligent-services/customer-ai/user-guide/discover-insights.md).
