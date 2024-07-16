---
title: Activation des audiences vers des destinations traitées en fonction des identifiants LiveRamp
type: Tutorial
description: Découvrez comment activer les audiences de Adobe Experience Platform vers les destinations audio et TV connectées, ainsi que d’autres intégrations à l’aide de l’LiveRamp Ramp ID.
exl-id: 37e5bab9-588f-40b3-b65b-68f1a4b868f1
source-git-commit: c2e308b5e743f07062be9a34e23c4bc700b27463
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 1%

---

# Activation des audiences vers des destinations traitées en fonction des identifiants LiveRamp

Utilisez l’intégration d’Adobe Real-Time CDP avec [!DNL LiveRamp] pour activer les audiences vers une liste organisée de destinations qui utilisent [!DNL [LiveRamp RampID]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html) pour l’activation, y compris les destinations audio et TV connectées, telles que celles répertoriées ci-dessous.

>[!IMPORTANT]
>
>Vous n’avez pas besoin d’ingérer des LiveRamp Ramp ID ni de les utiliser de quelque manière que ce soit dans l’interface de l’Experience Platform.
>
> Vous pouvez exporter des identités à partir de Real-Time CDP, telles que des identifiants basés sur des informations d’identification personnelles, des identifiants connus et des identifiants personnalisés, comme décrit dans la [documentation LiveRamp](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers) officielle. Ces identités sont ensuite associées à [!DNL LiveRamp RampIDs] plus en aval du processus d’activation.


* [[!DNL 4C Insights]](#insights)
* [[!DNL Acast]](#acast)
* [[!DNL Ampersand.tv]](#ampersand-tv)
* [[!DNL Captify]](#captify)
* [[!DNL Cardlytics]](#cardlytics)
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [[!DNL iHeartMedia]](#iheartmedia)
* [[!DNL Index Exchange]](#index-exchange)
* [[!DNL Magnite CTV Platform]](#magnite)
* [[!DNL Magnite DV+ (Rubicon Project)]](#magnite-dv)
* [[!DNL Nexxen]](#nexxen)
* [[!DNL One Fox]](#fox)
* [[!DNL Pandora]](#pandora)
* [[!DNL Reddit]](#reddit)
* [[!DNL Roku]](#roku)
* [[!DNL Spotify]](#spotify)
* [[!DNL Taboola]](#taboola)
* [[!DNL TargetSpot]](#targetspot)
* [[!DNL Teads]](#teads)
* [[!DNL WB Discovery]](#wb-discovery)

Cet article explique le processus requis pour activer les audiences de Real-Time CDP vers les destinations répertoriées ci-dessus, directement depuis l’interface utilisateur de Real-Time CDP.

## Workflow d’activation {#workflow}

Vous activez les audiences vers les destinations audio et TV connectées en suivant un processus en deux étapes, et en utilisant les destinations [LiveRamp - Intégration](../catalog/advertising/liveramp-onboarding.md) et [LiveRamp - Distribution](../catalog/advertising/liveramp-distribution.md), comme illustré dans l’image ci-dessous.

![Diagramme présentant le workflow d’activation des audiences de Real-Time CDP vers les destinations traitées, via LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png){width="1920" zoomable="yes"}

Tout d’abord, vous exportez vos audiences de Real-Time CDP vers la destination [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) sous la forme de fichiers CSV.

Après avoir exporté vos audiences, vous les activez à l’aide de la destination [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md).

>[!TIP]
>
>Ce processus vous permet d’activer vos audiences vers des destinations telles que [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney), etc., directement depuis l’interface utilisateur de Real-Time CDP, sans avoir à vous connecter à votre compte [!DNL LiveRamp] pour l’activation.

### Tutoriel vidéo {#video}

Regardez la vidéo ci-dessous pour obtenir une explication de bout en bout du processus décrit dans cette page.

>[!VIDEO](https://video.tv.adobe.com/v/3425367)

### Étape 1 : envoyez vos audiences de l’Experience Platform vers LiveRamp, via la destination [!DNL LiveRamp - Onboarding] {#onboarding}

Pour activer vos audiences vers des destinations traitées basées sur les LiveRamp Ramp ID, vous devez d’abord **exporter vos audiences de l’Experience Platform vers[!DNL LiveRamp]**.

Pour ce faire, utilisez la destination **[!DNL LiveRamp - Onboarding]**.

![Image de l’interface utilisateur Experience Platform montrant le LiveRamp - carte de destination de l’intégration](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

Pour savoir comment configurer la destination [!DNL LiveRamp - Onboarding] et exporter vos audiences de l’Experience Platform, consultez la documentation de destination [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md).

>[!IMPORTANT]
>
>Lors de l’exportation de fichiers vers la destination [!DNL LiveRamp - Onboarding], Platform génère un fichier CSV pour chaque [ID de stratégie de fusion](../../profile/merge-policies/overview.md). Consultez la documentation de destination [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) pour obtenir des informations détaillées sur la validation de votre exportation de données vers LiveRamp.


Une fois que vous avez correctement exporté vos audiences vers LiveRamp, passez à l’ [étape 2](#distribution).

>[!TIP]
>
>Avant de passer à l’[étape 2](#distribution), [validez](../catalog/advertising/liveramp-onboarding.md#exported-data) que vos audiences ont été correctement exportées vers LiveRamp. Consultez la documentation sur la [surveillance des flux de données de destination](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) et découvrez les détails de surveillance spécifiques pour [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

### Étape 2 : activation des audiences intégrées vers les destinations audio et TV connectées, via la destination [!DNL LiveRamp - Distribution] {#distribution}

Une fois que vous avez [validé](../catalog/advertising/liveramp-onboarding.md#exported-data) que vos audiences ont été correctement exportées vers LiveRamp, il est temps d’activer les audiences vers vos destinations préférées, telles que [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney), etc.

Vous activez les audiences (exportées à l’ [étape 1](#onboarding)) à l’aide de la destination **[!DNL LiveRamp - Distribution]**.

![Image de l’interface utilisateur Experience Platform montrant le LiveRamp - Carte de destination de distribution](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

Pour savoir comment configurer la destination **[!DNL LiveRamp - Distribution]** et activer les audiences que vous avez exportées dans [étape 1](#onboarding), consultez la documentation de destination [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md).

>[!IMPORTANT]
>
>À l’étape **sélection d’audience** de la destination **[!DNL LiveRamp - Distribution]**, vous devez sélectionner les *mêmes audiences* que vous avez exportées vers la destination [LiveRamp - Intégration](../catalog/advertising/liveramp-onboarding.md) de l’ [étape 1](#onboarding).

Lorsque vous configurez la destination **[!DNL LiveRamp - Distribution]**, vous devez créer une connexion dédiée pour chaque destination en aval à utiliser (Roku, Disney, etc.).

>[!TIP]
>
>Lorsque vous nommez votre destination, Adobe recommande le format suivant : `LiveRamp - Downstream Destination Name`. Ce modèle de dénomination vous permet d’identifier rapidement vos destinations dans l’onglet [Parcourir](../ui/destinations-workspace.md#browse) de l’espace de travail des destinations.
><br>
>Exemple : `LiveRamp - Roku`.

![Copie d’écran de l’interface utilisateur de Platform montrant plusieurs destinations LiveRamp.](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## Données exportées / Valider l’exportation des données {#exported-data}

Pour valider l’exportation réussie de vos audiences vers la destination [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md), consultez la documentation sur la [surveillance des flux de données de destination](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) et découvrez les détails de surveillance spécifiques pour [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

Pour valider l’activation réussie de vos audiences sur votre plateforme publicitaire de votre choix (Roku, Disney, etc.), connectez-vous à votre compte de plateforme de destination et vérifiez les mesures d’activation.
