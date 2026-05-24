---
title: Évaluation d’ensembles de règles
description: Déclenchez manuellement une évaluation d’ensemble de règles.
exl-id: 63751b47-b635-446f-af10-8144c9d3aa58
TQID: https://experienceleague.adobe.com/KTwXVG5M-hcwplzoJQIHFdFJ4v0eI3XEOXjEAaWwImQ
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: cb954087-f4fc-4456-afb9-e939cabcdc79id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 142
ht-degree: 2%

---

# Évaluation d’ensembles de règles

Le type d’action **[!UICONTROL Evaluate rulesets]** vous permet de déclencher manuellement des évaluations d’ensemble de règles. Les ensembles de règles sont renvoyés par Adobe Journey Optimizer pour prendre en charge des fonctionnalités telles que les messages dans le navigateur.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez le champ déroulant du [!UICONTROL Extension] sur **[!UICONTROL Adobe Experience Platform Web SDK]**, puis définissez le [!UICONTROL Action type] sur **[!UICONTROL Evaluate rulesets]**.

![Image de l’interface utilisateur d’Experience Platform affichant le type d’action de réponse Évaluer des ensembles de règles.](../assets/evaluate-rulesets.png)

## Champs disponibles

Ce type d’action prend en charge les options suivantes :

* **[!UICONTROL Render visual personalization decisions]** : une case à cocher qui, lorsqu’elle est activée, rend des décisions de personnalisation visuelles pour les éléments d’ensemble de règles qui correspondent.
* **[!UICONTROL Decision context]** : mappage clé-valeur utilisé lors de l’évaluation des ensembles de règles Adobe Journey Optimizer pour la prise de décision sur l’appareil. Vous pouvez fournir le contexte de décision manuellement ou par le biais d&#39;un élément de données.
