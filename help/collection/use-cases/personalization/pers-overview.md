---
title: Présentation des cas d’utilisation de Personalization
description: Découvrez comment implémenter des cas d’utilisation de personnalisation à l’aide de Adobe Experience Platform Web SDK, y compris des modèles pour le rendu du contenu et l’affichage du suivi.
keywords: personnalisation;sendEvent;renderDecisions;applyPropositions;decisionScopes;événements d’affichage;scintillement;
exl-id: 6beccbfd-fddb-4e19-8a56-caba276e1643
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---

# Présentation des cas d’utilisation de Personalization

Adobe Experience Platform Web SDK offre un large éventail de cas d’utilisation de la personnalisation pour les propriétés web. Il prend en charge des architectures flexibles (côté client, côté serveur et hybrides) afin que vous puissiez demander des décisions et effectuer le rendu du contenu en fonction des besoins de votre site.

## Rendu de contenu personnalisé

Le SDK Web peut récupérer les décisions de personnalisation (également appelées _propositions_) et vous aider à en effectuer le rendu sur la page. Le rendu est asynchrone. Évitez donc de supposer une durée spécifique pour l’application du contenu.

Choisissez le modèle correspondant aux éléments de proposition que vous recevez :

1. **Rendre automatiquement les propositions d’action DOM** : à utiliser lorsque les propositions incluent des éléments de `dom-action` avec des sélecteurs et des types d’action que Web SDK peut appliquer automatiquement. Consultez la section [Rendu automatique des propositions d’action DOM](render-auto-pers-content.md).
1. **Rendu des offres HTML sans sélecteurs à l’aide d’applyPropositions** : à utiliser lorsque vous recevez du contenu HTML, mais vous devez indiquer où et comment l’appliquer (sélecteur + type d’action) via des métadonnées. Voir [Rendu des offres HTML sans sélecteurs](render-html-offers.md).
1. **Propositions de rendu manuelles** : à utiliser lorsque vous avez besoin d’un contrôle complet de la logique de rendu (par exemple, pour composer l’interface utilisateur à partir de JSON ou appliquer des règles métier personnalisées). Voir [Rendu manuel des propositions](render-manual-propositions.md).

>[!TIP]
>
>Ces motifs peuvent être combinés. Par exemple, vous pouvez activer le rendu automatique des actions DOM tout en effectuant manuellement le rendu du contenu à partir de portées de décision spécifiques.

## Rubriques connexes courantes

La plupart des implémentations de personnalisation impliquent les rubriques suivantes :

* **Empêcher le scintillement** (facultatif) : masquez et affichez les conteneurs lors de la personnalisation. Voir [Gestion du scintillement](manage-flicker.md).
* **Suivi des éléments affichés** : enregistrez les événements d’affichage pour le contenu rendu. Voir [Gestion des événements d’affichage](display-events.md).
* **Récupération en haut de la page/mesures en bas de page** : demandez des décisions précoces, puis incluez la mesure plus tard. Voir [Configuration des événements en haut et en bas de page](top-bottom-page-events.md).

## Exemples de SDK Web

Outre les pages de documentation de ce dossier, Adobe conserve un référentiel d’exemples d’applications que vous pouvez référencer. Voir [Exemples de SDK web](https://github.com/adobe/alloy-samples/) sur GitHub pour d’autres scénarios de personnalisation, notamment :

* Personnalisation côté client
* Personnalisation côté serveur
* Personnalisation hybride
* Personalization dans les applications monopages
