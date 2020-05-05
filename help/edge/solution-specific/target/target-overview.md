---
title: 'Adobe Cible et le SDK Web Adobe Experience Platform. '
seo-title: SDK Web d’Adobe Experience Platform et utilisation d’Adobe Cible
description: Découvrez comment rendre du contenu personnalisé avec le SDK Web Experience Platform à l’aide d’Adobe Cible
seo-description: Découvrez comment rendre du contenu personnalisé avec le SDK Web Experience Platform à l’aide d’Adobe Cible
translation-type: tm+mt
source-git-commit: db4bfec04a1116ce2b6a0be7ca0e8cb2f9639ad6

---


# Présentation de la Cible

Le SDK Web d’Adobe Experience Platform est intégré à la Cible Adobe par le biais de cette fonction [de](../../fundamentals/rendering-personalization-content.md) personnalisation et vous permet de diffuser du contenu personnalisé et de prendre des décisions simplement.

## Activation d’Adobe Cible

Pour activer la Cible, vous devez effectuer les opérations suivantes :

- Activez la cible dans votre configuration [](../../fundamentals/edge-configuration.md) Edge avec le code client approprié.
- Ajouter l&#39; `renderDecisions` option à vos événements.

Vous pouvez également :

- Ajouter `scopes` à vos événements pour récupérer des activités spécifiques (utiles pour les activités créées avec le compositeur basé sur un formulaire).
- Ajouter le [fragment de code](../../fundamentals/managing-flicker.md) prémasqué pour masquer uniquement certaines parties de la page.

## Utilisation du compositeur d’expérience visuelle

Avec le SDK, vous pouvez utiliser le compositeur d’expérience visuelle normalement, à une exception près, vous aurez besoin de l’extension [d’assistance du compositeur d’expérience visuelle de](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) cible installée et active.

## Utilisation du compositeur d’après les formulaires

Le compositeur basé sur un formulaire peut également être utilisé pour renvoyer du contenu. Les étendues s’affichent sous forme d’emplacements (mBoxes) dans l’interface utilisateur de la Cible. Vous devez également vous assurer que votre développeur recherche les réponses si vous décidez d’utiliser des étendues.

## Audiences dans XDM

Dans la Cible, les données XDM s’affichent dans le créateur d’Audiences en tant que paramètre personnalisé. Le XDM est sérialisé à l’aide de la notation par point (ex. `web.webPageDetails.name`)

## Terminologie

__Décisions__ - En Cible, elles sont corrélées à l&#39;expérience qui est sélectionnée à partir d&#39;une Activité.

__Portée__ - Portée de la décision. En Cible, il s’agit de la mBox. La mBox globale est la `__view__` portée.

__Schéma__ - Le schéma d&#39;une décision est le type d&#39;offre en Cible.

__XDM__ - Le XDM est sérialisé en notation point, puis mis en Cible en tant que paramètres mBox.