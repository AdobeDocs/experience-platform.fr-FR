---
title: Composants de build personnalisés
description: Créez une version Web SDK personnalisée qui désactive les fonctionnalités pour réduire la taille de la version.
source-git-commit: d6aea91d6989775ff5b6038b216ed2518f4a7d98
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 1%

---

# Composants de build personnalisés

La bibliothèque Web SDK comprend plusieurs modules pour différentes fonctionnalités telles que la personnalisation, l’identité, le suivi des liens, etc. Selon vos cas d’utilisation, il se peut que vous n’ayez besoin que de fonctionnalités spécifiques au lieu de l’ensemble de la bibliothèque. La désactivation des composants de version vous permet d’utiliser uniquement les modules dont vous avez besoin, ce qui réduit la taille de la bibliothèque et améliore les performances.

Lorsque vous désactivez un composant, vous ne pouvez plus modifier les paramètres de ce composant. Si vous utilisez plusieurs instances Web SDK, les composants de build sélectionnés s’appliquent à toutes les instances.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configure]** sur la carte [!UICONTROL Adobe Experience Platform Web SDK] .
1. Développez l’accordéon **[!UICONTROL Custom build components]** en haut.

>[!WARNING]
>
>Une modification incorrecte de ces paramètres peut entraîner des résultats indésirables, notamment une perte de données. Testez minutieusement votre implémentation dans un environnement de développement avant de publier ces modifications en production.

Adobe permet de désactiver les composants de build Web SDK suivants :

| Créer un composant | Description | Fonctionnalités dépendantes |
| --- | --- | --- |
| **[!UICONTROL Activity collector]** | Permet la collecte automatique de liens et le suivi d’Activity Map. | |
| **[!UICONTROL Advertising]** | Active l’intégration d’Adobe Advertising à Customer Journey Analytics. | |
| **[!UICONTROL Audiences]** | Prend en charge l’intégration à Adobe Audience Manager, comme la synchronisation des identifiants. | |
| **[!UICONTROL Consent]** | Permet d’utiliser les fonctionnalités de consentement. | action [[!UICONTROL Set consent]](../actions/set-consent.md) |
| **[!UICONTROL Event merge]** | Obsolète. | [[!UICONTROL Event merge ID]](../data-element-types.md) élément de données (obsolète)<br>[[!UICONTROL Reset event merge ID]](../actions/reset-event-merge-id.md) action (obsolète) |
| **[!UICONTROL Media Analytics bridge]** | Prend en charge l’intégration à l’ancienne version de Media Analytics. | action [[!UICONTROL Get media analytics tracker]](../actions/get-media-analytics-tracker.md) |
| **[!UICONTROL Personalization]** | Prend en charge les intégrations avec Adobe Target et Adobe Journey Optimizer. | action [[!UICONTROL Apply propositions]](../actions/apply-propositions.md) |
| **[!UICONTROL Push notifications]** | Active les notifications push web pour Adobe Journey Optimizer. | action [[!UICONTROL Send push subscription]](../actions/send-push-subscription.md) |
| **[!UICONTROL Rules engine]** | Active la prise de décision de l’appareil avec Adobe Journey Optimizer. | [[!UICONTROL Evaluate rulsets]](../actions/evaluate-rulesets.md) action <br> Événement [[!UICONTROL Subscribe ruleset items]](../event-types.md#subscribe-ruleset-items) |
| **[!UICONTROL Streaming media]** | Prend en charge l’intégration à la collecte de médias en flux continu. | action [[!UICONTROL Send media event]](../actions/send-media-event.md) |
