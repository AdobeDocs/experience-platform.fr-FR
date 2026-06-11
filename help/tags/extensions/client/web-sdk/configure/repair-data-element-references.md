---
title: Réparer les références d’élément de données
description: Découvrez comment analyser et réparer les références d’éléments de données obsolètes dans toutes les actions d’extension de Web SDK dans une propriété de balise.
source-git-commit: 6a7591682bc019be2672f543dbcc495b356b1c09
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Réparer les références d’élément de données {#repair-data-element-references}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_repairreferences"
>title="Réparer les références d’élément de données"
>abstract="Analyse chaque action de cette propriété qui appartient à l’extension AEP Web SDK et met à jour toute action qui fait référence à un élément de données qui n’est plus présent sur cette propriété."

La fonction **[!UICONTROL Réparer les références d’élément de données]** analyse chaque action de la propriété de balise active et identifie toutes les actions comportant des références d’élément de données obsolètes. Si un élément de données portant le même nom existe dans la propriété , la référence obsolète est remplacée automatiquement. Les actions qui ne peuvent pas être réparées automatiquement sont signalées afin que vous puissiez les corriger manuellement. Adobe recommande d’utiliser cette fonctionnalité après avoir copié une extension ou des règles contenant des actions **[!UICONTROL Mettre à jour l’élément de données]** sur une autre propriété, car les actions copiées peuvent toujours référencer des éléments de données de la propriété source qui ne sont plus présents dans la destination. Il est disponible à partir de la version 2.37.0 de l’extension de balise.

1. Connectez-vous à [CX Enterprise](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configurer]** sur la vignette [!UICONTROL Adobe Experience Platform Web SDK].
1. Développez l’accordéon **[!UICONTROL Actions de propriété]**.
1. Sous **[!UICONTROL Réparer les références de l’élément de données]**, sélectionnez **[!UICONTROL Exécuter la réparation]**.
1. Vérifiez la description dans la boîte de dialogue modale de confirmation, puis sélectionnez **[!UICONTROL Confirmer]**.

Une fois l’analyse terminée, les résultats affichent le nombre total d’actions analysées. Toutes les références qui ont été réparées automatiquement sont répertoriées. Les actions avec des références obsolètes qui n’ont pas pu être résolues automatiquement sont répertoriées séparément afin que vous puissiez les corriger manuellement. Sélectionnez **[!UICONTROL Exécuter à nouveau]** pour effectuer une autre analyse, ou **[!UICONTROL Fermer]** pour ignorer les résultats.
