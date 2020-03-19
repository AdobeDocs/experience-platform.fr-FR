---
title: Soutien du consentement
seo-title: Prise en charge des préférences de consentement du SDK Web d’Adobe Experience Platform
description: Découvrez comment prendre en charge les préférences de consentement avec le SDK Web d’Experience Platform
seo-description: Découvrez comment prendre en charge les préférences de consentement avec le SDK Web d’Experience Platform
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Bêta) Consentement à l’appui

>[!IMPORTANT]
>
>Le SDK Web d’Adobe Experience Platform est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

Pour respecter la confidentialité de votre utilisateur, vous pouvez demander son consentement avant d’autoriser le SDK à utiliser des données spécifiques à l’utilisateur à certaines fins. Actuellement, le SDK permet uniquement aux utilisateurs de opt-in ou d’en dehors de tous les objectifs, mais Adobe espère à l’avenir fournir un contrôle plus précis sur des objectifs spécifiques.

Si l’utilisateur choisit de se connecter à toutes les fins, le kit SDK est autorisé à effectuer les  suivantes :

* Envoyez des données vers et depuis les serveurs d’Adobe.
* Lisez et écrivez des cookies ou des éléments de  Web (sauf pour conserver les préférences d’inclusion de l’utilisateur).

Si l’utilisateur choisit de ne pas participer à tous les , le SDK n’effectue aucune de ces opérations.

## Configuration du consentement

Par défaut, l’utilisateur est sélectionné à tous les fins. Pour empêcher le SDK d’exécuter le  ci-dessus jusqu’à ce que l’utilisateur se connecte, transmettez la configuration `"defaultConsent": { "general": "pending" }` du SDK comme suit :

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": { "general": "pending" }
});
```

Lorsque le consentement par défaut à des fins générales est défini sur En attente, toute tentative d’exécution de commandes qui dépend des préférences d’inclusion de l’utilisateur (par exemple, la `event` commande) entraîne la mise en file d’attente de la commande dans le SDK. Ces commandes ne sont pas traitées tant que vous n’avez pas communiqué les préférences d’inclusion de l’utilisateur au SDK.

A ce stade, vous préférerez peut-être demander à l’utilisateur de opt-in quelque part dans l’interface utilisateur. Une fois les préférences de l’utilisateur collectées, communiquez ces préférences au SDK.

## Communication des préférences de consentement

Si l’utilisateur accepte, exécutez la `setConsent` commande en définissant l’ `general` option `in` comme suit :

```javascript
alloy("setConsent", {
  "general": "in"
});
```

L’utilisateur ayant désormais choisi de se connecter, le SDK exécute toutes les commandes mises en file d’attente précédentes. Les futures commandes qui dépendent du choix de l’utilisateur _ne seront pas_ mises en file d’attente et seront exécutées rapidement.

Si l’utilisateur choisit de opt-out, exécutez la `setConsent` commande en définissant l’ `general` option `out` comme suit :

```javascript
alloy("setConsent", {
  "general": "out"
});
```

>[!NOTE]
>
>Une fois qu’un utilisateur s’est désabonné, le kit SDK ne vous permet pas de définir le consentement de l’utilisateur `in`.

Comme l’utilisateur a choisi de opt-out, les promesses qui ont été renvoyées à partir de commandes mises en file d’attente précédentes sont rejetées. Les futures commandes qui dépendront du choix de l&#39;utilisateur renverront des promesses qui seront également rejetées. Pour plus d&#39;informations sur la gestion ou la suppression des erreurs, reportez-vous à la section [Exécution des commandes](executing-commands.md).

>[!NOTE]
>
>Actuellement, le SDK ne prend en charge que l’ `general` objectif. Bien que nous prévoyions de créer un ensemble d’objectifs ou de  plus robustes qui correspondront aux différentes fonctionnalités et offres de produits Adobe, l’implémentation actuelle est une approche d’inclusion totale ou inexistante.  Ceci s’applique uniquement au SDK Web d’Adobe Experience Platform et NON aux autres bibliothèques JavaScript d’Adobe.

## Persistance des préférences de consentement

Après avoir communiqué les préférences de l’utilisateur au SDK à l’aide de la `setConsent` commande, le SDK conserve les préférences de l’utilisateur sur un cookie. La prochaine fois que l’utilisateur charge votre site Web dans le navigateur, le SDK récupérera et utilisera ces préférences persistantes. Il n’est pas nécessaire d’exécuter à nouveau la `setConsent` commande, sauf pour communiquer un changement dans les préférences de l’utilisateur, ce que vous pouvez faire à tout moment.