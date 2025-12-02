---
title: renderDecisions
description: Effectuez le rendu du contenu personnalisé éligible au rendu automatique.
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# `renderDecisions`

La propriété `renderDecisions` vous permet de forcer le SDK Web à effectuer le rendu de tout contenu personnalisé éligible au rendu automatique.

Définissez la valeur booléenne `renderDecisions` lors de l’exécution de la commande `sendEvent`. Si elle est omise, cette propriété est définie par défaut sur `false`. Définissez cette propriété sur `true` si vous souhaitez effectuer automatiquement le rendu du contenu personnalisé.

>[!IMPORTANT]
>
>La propriété `renderDecisions` est incompatible avec la propriété [`documentUnloading`](documentunloading.md). Évitez de définir les deux propriétés sur `true` simultanément.

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```

Lorsque vous définissez cette propriété sur `true`, veillez à inclure également les portées ou surfaces associées. Ces portées ou surfaces peuvent être demandées automatiquement (par exemple sur la première commande `sendEvent` d’une page) ou explicitement (à l’aide de [`personalization.decisionScopes`](personalization.md#personalizationdecisionscopes) ou [`personalization.surfaces`](personalization.md#personalizationsurfaces)). Un problème courant lors du rendu de la personnalisation est le scénario suivant :

1. Une commande `sendEvent` s’exécute dès le début de la page qui demande une personnalisation par défaut sans `renderDecisions` définie (la valeur par défaut est `false`). Les propositions sont récupérées, mais pas rendues.
1. Plus loin sur la page, un autre `sendEvent` se déclenche avec `renderDecisions` défini sur `true` mais n’inclut aucune portée ni surface. Puisqu’il n’y a pas de portées ou de surfaces dans ce deuxième appel, rien n’est rendu.

Vous pouvez éviter ce problème en effectuant l’une des opérations suivantes :

* la définition de `renderDecisions` sur `true` lors du premier appel `sendEvent` ; ou
* Définition explicite de `decisionScopes` ou `surfaces` lors d’un appel `sendEvent` suivant lors de la définition de `renderDecisions` sur `true`.

## Rendre des décisions à l’aide de l’extension de balise Web SDK

L’extension de balise Web SDK équivalente à cette propriété est la case à cocher [**Rendre les décisions de personnalisation visuelle**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields) dans l’action « [!UICONTROL Send event] ».
