---
title: Prise en charge du consentement
seo-title: Prise en charge des préférences de consentement du SDK Web d’Adobe Experience Platform
description: Découvrez comment prendre en charge les préférences de consentement avec le SDK Web d’Experience Platform
seo-description: Découvrez comment prendre en charge les préférences de consentement avec le SDK Web d’Experience Platform
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 99%

---


# Soutien du consentement

Pour respecter la confidentialité des utilisateurs, vous pouvez leur demander leur consentement avant d’autoriser le SDK à utiliser des données spécifiques à ceux-ci à certains usages. Actuellement, le SDK permet aux utilisateurs de donner ou de refuser leur consentement uniquement pour tous les usages, mais Adobe espère prochainement offrir un contrôle plus précis sur des usages spécifiques.

Si l’utilisateur choisit de donner son consentement pour tous les usages, le SDK est autorisé à effectuer les tâches suivantes :

* envoyer des données vers et depuis les serveurs d’Adobe ;
* lire et écrire des cookies ou des éléments de stockage web (sauf pour conserver les préférences de consentement de l’utilisateur).

Si l’utilisateur choisit de refuser son consentement pour tous les usages, le SDK n’effectue aucune de ces tâches.

## Configuration du consentement

Par défaut, le consentement de l’utilisateur est donné pour tous les usages. Pour empêcher le SDK d’exécuter les tâches ci-dessus jusqu’à ce que l’utilisateur donne son consentement, transmettez `"defaultConsent": { "general": "pending" }` pendant la configuration du SDK de la manière suivante :

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": { "general": "pending" }
});
```

Lorsque le consentement par défaut pour un usage général est défini sur En attente, toute tentative d’exécution de commandes qui dépend des préférences de consentement de l’utilisateur (par exemple, la commande`event`) entraîne la mise en file d’attente de la commande dans le SDK. Ces commandes ne sont pas traitées tant que vous n’avez pas communiqué les préférences de consentement de l’utilisateur au SDK.

À ce stade, vous préférerez peut-être demander à l’utilisateur de donner son consentement à un emplacement dans l’interface utilisateur. Une fois les préférences de l’utilisateur collectées, communiquez-les au SDK.

## Communication des préférences de consentement

Si l’utilisateur accorde son consentement, exécutez la commande `setConsent` en définissant l’option `general` sur `in` de la manière suivante :

```javascript
alloy("setConsent", {
  "general": "in"
});
```

L’utilisateur ayant donné son consentement, le SDK exécute toutes les commandes précédemment mises en file d’attente. Les prochaines commandes qui dépendent du consentement de l’utilisateur _ne seront pas_ mises en file d’attente et seront exécutées rapidement.

Si l’utilisateur choisit de ne pas donner son consentement, exécutez la commande `setConsent` en définissant l’option `general` sur `out` de la manière suivante :

```javascript
alloy("setConsent", {
  "general": "out"
});
```

>[!NOTE]
>
>Lorsque l’utilisateur n’a pas donné son consentement, le SDK ne vous permet pas de définir le consentement des utilisateurs sur `in`.

L’utilisateur ayant choisi de ne pas donner son consentement, les promesses qui ont été renvoyées à partir de commandes précédemment mises en file d’attente sont rejetées. Les prochaines commandes qui dépendent du consentement de l’utilisateur retournent les promesses également rejetées. Pour plus d’informations sur la gestion ou la suppression des erreurs, reportez-vous à la section [Exécution des commandes](executing-commands.md).

>[!NOTE]
>
>Actuellement, le SDK ne prend en charge que l’usage `general`. Bien que nous prévoyions de créer un ensemble plus riche d’usages ou de catégories qui devront correspondre aux différentes capacités et offres de produits Adobe, l’implémentation actuelle s’effectue sur la base du « tout ou rien ».  Cela s’applique uniquement au SDK Web d’Adobe Experience Platform et NON aux autres bibliothèques JavaScript d’Adobe.

## Persistance des préférences de consentement

Après avoir communiqué les préférences de l’utilisateur au SDK à l’aide de la commande `setConsent`, le SDK les conserve dans un cookie. La prochaine fois que l’utilisateur charge votre site web dans le navigateur, le SDK récupère ces préférences persistantes et les utilise. Il n’est pas nécessaire d’exécuter de nouveau la commande `setConsent`, sauf pour communiquer un changement dans les préférences de l’utilisateur, ce que vous pouvez faire à tout moment.