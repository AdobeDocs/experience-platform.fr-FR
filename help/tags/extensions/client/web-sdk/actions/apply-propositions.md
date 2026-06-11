---
title: Appliquer les propositions
description: Propositions de rendu dans les applications monopages sans incrémenter de mesures.
exl-id: cac9c65b-259b-4776-bd32-fab070a145fb
TQID: https://experienceleague.adobe.com/dzvNI7AGqvf2e1Man7WUOugdwRTjX4IeSqkzxGh--Mk
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: daec7ead-f475-492a-a3b3-02ae08565d6fid: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: d9830f6f-ceb6-4faa-9744-f281fe4439f9id: ee602049-8a18-43df-9299-a689a025a371id: f1f1a2d4-0976-4881-b091-c2bb8de7ffacid: f6ff4d13-7b5c-4533-8556-95e76673d4cb
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 60dfb3bf6044036be567e46c3807b48408ea3477
workflow-type: tm+mt
source-wordcount: 403
ht-degree: 1%

---

# Appliquer les propositions

Le type d’action **[!UICONTROL Appliquer des propositions]** vous permet d’effectuer le rendu des propositions dans des applications d’une seule page sans incrémenter de mesures. Ce type d’action est utile lorsque vous travaillez avec des applications monopages où des parties de la page sont rendues de nouveau, ce qui peut remplacer toutes les personnalisations déjà appliquées à la page.

1. Connectez-vous à [CX Enterprise](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Règles]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez-en une.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL Adobe Experience Platform Web SDK]**, puis définissez le [!UICONTROL Type d’action] sur **[!UICONTROL Appliquer les propositions]**.

![L’interface utilisateur d’Experience Platform Tags affiche le type d’action Appliquer les propositions.](../assets/apply-propositions.png)

## Cas d’utilisation

Vous pouvez utiliser ce type d’action pour différents cas d’utilisation, tels que :

1. **Rendu des offres de mbox HTML**. Les propositions explicitement demandées via une portée ou une surface à partir d’une action **[!UICONTROL Envoyer l’événement]** ne sont pas automatiquement rendues. Vous pouvez utiliser le type d’action **[!UICONTROL Appliquer des propositions]** pour indiquer à Web SDK où effectuer leur rendu en spécifiant les métadonnées de proposition.
2. **Effectuez le rendu des offres pour une vue sur une application monopage**. Lors du rendu d’un événement de changement de vue, si les données d’analyse ne sont pas encore prêtes, vous pouvez utiliser l’action **[!UICONTROL Appliquer les propositions]** pour effectuer le rendu des propositions d’affichage en haut de la page. Voir [événements en haut et en bas de la page (Deuxième page vue - Option 2)](/help/collection/use-cases/personalization/top-bottom-page-events.md) pour plus d’informations. Pour l&#39;utiliser, saisissez un **[!UICONTROL Nom de la vue]** dans le formulaire.
3. **Restituer des propositions**. Lorsque votre site utilise un framework comme React pour effectuer à nouveau le rendu du contenu, vous devrez peut-être appliquer une nouvelle personnalisation. Dans ce cas, vous pouvez utiliser le type d&#39;action **[!UICONTROL Appliquer les propositions]**.

Ce type d’action n’envoie pas d’événement d’affichage pour les propositions rendues. Il effectue le suivi des propositions générées afin qu’elles puissent être incluses dans les appels **[!UICONTROL Envoyer l’événement]** suivants.

## Champs disponibles

Ce type d&#39;action prend en charge les champs suivants :

* **[!UICONTROL Instance]** : instance SDK à laquelle l’action s’applique. Ce menu déroulant est désactivé si votre implémentation utilise une seule instance SDK.
* **[!UICONTROL Propositions]** : tableau d’objets de proposition dont vous souhaitez effectuer à nouveau le rendu.
* **[!UICONTROL Nom de la vue]** : nom de la vue dont le rendu doit être effectué.
* **[!UICONTROL Métadonnées de proposition]** : objet qui détermine la manière dont les offres HTML peuvent être appliquées. Vous pouvez fournir ces informations par le biais du formulaire ou d’un élément de données. Il contient les propriétés suivantes :
   * **[!UICONTROL Périmètre]**
   * **[!UICONTROL Sélecteur]**
   * **[!UICONTROL Type d’action]**
