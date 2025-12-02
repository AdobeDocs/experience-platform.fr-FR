---
title: defaultConsent
description: Définissez la méthode de collecte de consentement par défaut pour votre propriété web.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: 1e272eb18fac2f59f9737756d48947a25573d772
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 5%

---


# `defaultConsent`

La propriété `defaultConsent` détermine la manière dont vous gérez le consentement de la collecte de données avant d’appeler la commande [`setConsent`](../setconsent.md). Cette propriété est utile lorsque vous ne souhaitez pas collecter accidentellement des données auprès de personnes qui résident dans des zones où le consentement est requis avant de collecter des données.

Si vous avez un visiteur qui ne relève pas de la compétence du Règlement général sur la protection des données (RGPD), le consentement par défaut peut être défini sur `in`. Le consentement par défaut des visiteurs relevant de la compétence du RGPD peut être défini sur `pending`. Votre plateforme de gestion du consentement (CMP) peut détecter la région du client et fournir l’indicateur `gdprApplies` à IAB TCF 2.0. Cet indicateur peut être utilisé pour définir le consentement par défaut.

Définissez la propriété de chaîne de `defaultConsent` sur le niveau de consentement souhaité lors de l’exécution de la commande `configure`. Cette propriété est sensible à la casse et ne prend en charge que les trois valeurs suivantes : `"in"`, `"out"` et `"pending"`. Si vous tentez d’utiliser une autre valeur, la bibliothèque renvoie une erreur. Si elle n’est pas définie dans la commande `configure`, la valeur par défaut est **`in`**.

>[!IMPORTANT]
>
>La valeur `defaultConsent` n’est pas conservée entre les chargements de page. Assurez-vous de définir le consentement par défaut souhaité à chaque appel de la commande `configure`.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```

* **`in`** : la collecte de données fonctionne normalement jusqu’à ce que l’utilisateur se désinscrit.
* **`out`** : les données sont définitivement ignorées jusqu’à la souscription de l’utilisateur.
* **`pending`** : les données sont stockées localement jusqu’à ce que l’utilisateur accepte à l’aide de la commande [`setConsent`](../setconsent.md).

>[!NOTE]
>
>Bien qu’Adobe prévoit de créer un ensemble plus robuste d’objectifs ou de catégories correspondant aux fonctionnalités et aux offres de produits d’Adobe, la mise en œuvre actuelle est une approche tout ou rien de l’opt-in. Cette limitation s’applique uniquement à Web SDK et non aux autres bibliothèques Adobe JavaScript.

## Utilisation de `defaultConsent` avec `setConsent` {#using-consent}

Web SDK propose deux options de consentement complémentaires :

* `defaultConsent` (cette page) : détermine les préférences de consentement par défaut.
* [`setConsent`](../setconsent.md) : capturez les préférences de consentement des visiteurs.

Utilisés conjointement, ces paramètres peuvent donner lieu à différents résultats de collecte de données et de définition de cookies, en fonction de leurs valeurs configurées.

Consultez le tableau ci-dessous pour comprendre à quel moment la collecte de données a lieu et quand les cookies sont définis, en fonction des paramètres de consentement.

| `defaultConsent` | `setConsent` | Collecte de données | Web SDK définit les cookies de navigateur |
|---------|----------|---------|---------|
| `in` | `in` | Oui | Oui |
| `in` | `out` | Non | Oui |
| `in` | Non défini | Oui | Oui |
| `pending` | `in` | Oui | Oui |
| `pending` | `out` | Non | Oui |
| `pending` | Non défini | Non | Non |
| `out` | `in` | Oui | Oui |
| `out` | `out` | Non | Oui |
| `out` | Non défini | Non | Non |

Consultez [Cookies Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk) pour obtenir la liste des cookies définis par la bibliothèque.

>[!NOTE]
>
>Les cookies d’identité et de consentement sont définis même si un visiteur choisit de ne pas effectuer de suivi. Ces cookies sont nécessaires pour respecter leurs préférences de collecte de données.

## Définition du consentement par défaut en fonction des `gdprApplies`

Certaines CMP permettent de déterminer si le Règlement général sur la protection des données (RGPD) s’applique au client. Si vous souhaitez supposer le consentement des clients pour lesquels le RGPD ne s’applique pas, vous pouvez utiliser l’indicateur `gdprApplies` dans un appel API TCF. Par exemple :

```js
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

Dans le bloc de code ci-dessus, la commande `configure` est appelée après l’obtention du `tcData` à partir de l’API TCF. Si `gdprApplies` est vrai, le consentement par défaut est défini sur `pending`. Si `gdprApplies` est faux, le consentement par défaut est défini sur `in`. Veillez à renseigner la variable `alloyConfiguration` avec votre configuration.

## Consentement par défaut à l’aide de l’extension de balise Web SDK

Voir [Paramètres de consentement](/help/tags/extensions/client/web-sdk/configure/consent.md) dans la documentation de l’extension de balise Web SDK pour savoir comment effectuer ces actions à l’aide de balises.
