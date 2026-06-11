---
title: Options de build
description: Créez une version Web SDK personnalisée qui désactive les fonctionnalités pour réduire la taille de la version.
exl-id: 853e0a6c-0953-4e08-9a7d-334aab022583
source-git-commit: 60dfb3bf6044036be567e46c3807b48408ea3477
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 8%

---

# Options de build {#build-options}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_buildoptions"
>title="Options de build"
>abstract="Incluez ou excluez de manière sélective des modules de la bibliothèque JavaScript. Cela réduit la taille de la bibliothèque et améliore les performances."

La bibliothèque Web SDK comprend plusieurs modules pour différentes fonctionnalités telles que la personnalisation, l’identité, le suivi des liens, etc. Selon vos cas d’utilisation, il se peut que vous n’ayez besoin que de fonctionnalités spécifiques au lieu de l’ensemble de la bibliothèque. La désactivation des composants de version vous permet d’utiliser uniquement les modules dont vous avez besoin, ce qui réduit la taille de la bibliothèque et améliore les performances.

Lorsque vous désactivez un composant, vous ne pouvez plus modifier les paramètres de ce composant. Si vous utilisez plusieurs instances Web SDK, les composants de build sélectionnés s’appliquent à toutes les instances.

1. Connectez-vous à [CX Enterprise](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez **[!UICONTROL Configurer]** sur la vignette [!UICONTROL Adobe Experience Platform Web SDK].
1. Développez l’accordéon **[!UICONTROL Créer des options]** en haut.

>[!WARNING]
>
>Une modification incorrecte de ces paramètres peut entraîner des résultats indésirables, notamment une perte de données. Testez minutieusement votre implémentation dans un environnement de développement avant de publier ces modifications en production.

Adobe permet de désactiver les composants de build Web SDK suivants :

| Créer un composant | Description | Fonctionnalités dépendantes |
| --- | --- | --- |
| **[!UICONTROL Collecteur d’activités]** | Permet la collecte automatique de liens et le suivi d’Activity Map. | |
| **[!UICONTROL Publicité]** | Active l’intégration d’Adobe Advertising à Customer Journey Analytics. | |
| **[!UICONTROL Audiences]** | Prend en charge l’intégration à Adobe Audience Manager, comme la synchronisation des identifiants. | |
| **[!UICONTROL Concierge de marque]** | Permet l’intégration à Brand Concierge. | |
| **[!UICONTROL Consentement]** | Permet d’utiliser les fonctionnalités de consentement. | Action [[!UICONTROL Définir le consentement]](../actions/set-consent.md) |
| **[!UICONTROL Fusion des événements]** | Obsolète. | [[!UICONTROL ID de fusion d’événements]](../data-element-types.md) élément de données (obsolète)<br>[[!UICONTROL Réinitialiser l’ID de fusion d’événements]](../actions/reset-event-merge-id.md) action (obsolète) |
| **[!UICONTROL Pont Media Analytics]** | Prend en charge l’intégration à l’ancienne version de Media Analytics. | Action [[!UICONTROL Obtenir le suivi Media Analytics]](../actions/get-media-analytics-tracker.md) |
| **[!UICONTROL Personnalisation]** | Prend en charge les intégrations avec Adobe Target et Adobe Journey Optimizer. | [[!UICONTROL Application de propositions]](../actions/apply-propositions.md) action |
| **[!UICONTROL Notifications push]** | Active les notifications push web pour Adobe Journey Optimizer. | [[!UICONTROL Envoyer un abonnement push]](../actions/send-push-subscription.md) action |
| **[!UICONTROL Moteur de règles]** | Active la prise de décision de l’appareil avec Adobe Journey Optimizer. | [[!UICONTROL Évaluation des ensembles de règles]](../actions/evaluate-rulesets.md) action<br> Événement [[!UICONTROL Abonner des éléments d’ensemble de règles]](../event-types.md#subscribe-ruleset-items) |
| **[!UICONTROL Streaming Media]** | Prend en charge l’intégration à la collecte de médias en flux continu. | Action [[!UICONTROL Envoyer l’événement multimédia]](../actions/send-media-event.md) |
