---
title: Test des codes intégrés à l’aide du débogeur Adobe Experience Platform
description: Découvrez comment utiliser Experience Platform Debugger pour tester localement différents codes incorporés pour Adobe Experience Platform sur votre site web.
exl-id: ae6183b9-0d25-49d0-b0e9-f8b5ba58ab33
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 50%

---

# Test des codes intégrés à l’aide du débogeur Adobe Experience Platform

Lorsque vous apportez des modifications à vos versions de bibliothèque dans Adobe Experience Platform, vous devez les tester avant de déployer la version sur votre environnement de production. Si vous ne disposez pas d’un environnement d’évaluation ou de développement dédié à votre site web, vous pouvez utiliser le débogueur Adobe Experience Platform pour tester localement différents codes intégrés dans votre site.

## Conditions préalables

Ce tutoriel nécessite une bonne compréhension de l’utilisation des environnements et des codes incorporés pour les balises. Pour plus d’informations, consultez la [présentation des environnements](./environments.md).

Ce tutoriel nécessite également l’installation de l’extension de navigateur Experience Platform Debugger. Experience Platform Debugger est disponible pour le navigateur Chrome. Utilisez le lien suivant pour installer l’extension avant de commencer le tutoriel :

* [Experience Platform Debugger pour Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

## Ouvrez Experience Platform Debugger sur votre site web.

À l’aide du navigateur de votre choix, accédez à votre site web et ouvrez l’extension Experience Platform Debugger. Le site auquel Experience Platform Debugger est actuellement connecté s’affiche au bas de la fenêtre. Si les balises sont en cours d’exécution sur votre site, celui-ci est répertorié dans l’onglet [!UICONTROL Summary] .

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>Si Experience Platform Debugger ne se connecte pas initialement, vous devrez peut-être recharger l’onglet du navigateur qui affiche votre site web avant de réessayer.

## Remplacement des codes intégrés

Une fois Experience Platform Debugger connecté à votre site, sélectionnez **[!UICONTROL Launch]** dans le volet de navigation de gauche. Vous trouverez ici des informations sur la version de bibliothèque en cours d’exécution sur votre site, y compris son environnement et les extensions associées. À partir de là, sélectionnez **[!UICONTROL Configuration]** pour afficher les commandes de gestion des codes intégrés.

![](./images/embed-code-testing/launch-tab.png)

Sous [!UICONTROL Page Embed Codes], le code intégré actuellement utilisé par votre site s’affiche. Sélectionnez **[!UICONTROL Actions]** sur le côté droit du code intégré, puis sélectionnez **[!UICONTROL Replace]**.

![](./images/embed-code-testing/replace.png)

Une fenêtre contextuelle s’affiche, vous invitant à fournir un code intégré pour remplacer le code actuel. Notez que le remplacement du code incorporé à l’aide d’Experience Platform Debugger ne modifie pas le code incorporé déployé sur votre site. Il remplace uniquement le code intégré s’exécutant localement afin que vous puissiez tester et déboguer son implémentation.

Collez le code intégré à tester dans la zone de texte fournie, puis sélectionnez **[!UICONTROL Apply]**.

![](./images/embed-code-testing/paste-code.png)

L’onglet **[!UICONTROL Configuration]** réapparaît, indiquant que le code intégré actif a été remplacé par celui que vous avez fourni. Vous pouvez désormais utiliser le navigateur web pour déterminer si le code intégré que vous testez fonctionne comme prévu.

![](./images/embed-code-testing/code-replaced.png)

## Étapes suivantes

Ce tutoriel explique comment changer localement de code incorporé à des fins de test à l’aide d’Experience Platform Debugger. Reportez-vous à la documentation d’[Experience Platform Debugger](../../../debugger/home.md) pour plus d’informations sur ses différentes fonctionnalités.
