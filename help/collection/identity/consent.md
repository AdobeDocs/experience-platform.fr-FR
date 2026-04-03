---
title: Consentement et identité dans la collecte de données
description: Découvrez comment les choix de consentement affectent le comportement des identités dans les implémentations de Web SDK, notamment la génération d’ECID, la persistance des cookies et la continuité des visiteurs.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 2%

---

# Consentement et identité dans la collecte de données

Le consentement et l’identité sont étroitement liés dans les implémentations de Web SDK. La manière et le moment où vous collectez le consentement affectent directement le moment et le moment où le SDK Web génère un ECID, définit des cookies d’identité et envoie des données à Edge Network. Lorsque le consentement n’est pas géré soigneusement, il en résulte souvent une inflation inattendue des visiteurs et des visiteuses, des lacunes dans la continuité de l’identité, ou les deux.

Cette page explique comment les choix de consentement interagissent avec le comportement de l’identité et fournit des conseils pour configurer votre implémentation afin d’éviter les pièges courants. Pour en savoir plus sur la façon dont le SDK Web gère les ECID, les FPID et d’autres signaux d’identité, voir [Identité dans la collecte de données](./overview.md).

## Comment le consentement affecte l’identité {#how-consent-affects-identity}

Le SDK Web utilise à la fois la variable de configuration [`defaultConsent`](/help/collection/js/commands/configure/defaultconsent.md) et la commande [`setConsent`](/help/collection/js/commands/setconsent.md) pour contrôler s’il envoie des données à Edge Network. Le statut de consentement détermine directement quand un ECID est généré et quand les cookies d’identité sont définis.

Le tableau suivant présente l’effet combiné de la `defaultConsent` et de la `setConsent` sur la collecte de données, la configuration des cookies et le comportement des identités.

| `defaultConsent` | `setConsent` | Collecte de données | Cookies de navigateur définis | Comportement de l’identité |
| --- | --- | --- | --- | --- |
| `in` | Non défini | Oui | Oui | Un ECID est généré immédiatement sur la première requête. Les cookies d’identité sont définis au chargement de la page. |
| `in` | `in` | Oui | Oui | L’ECID existant du visiteur est conservé. Le comportement de l’identité reste inchangé. |
| `in` | `out` | Non | Oui | La collecte de données s’arrête. Les cookies d’identité ECID et `kndctr_` existants restent dans le navigateur jusqu’à leur expiration. |
| `pending` | Non défini | Non | Non | Aucun ECID n’est généré. Aucun cookie n’est défini. Les événements sont placés en file d’attente locale jusqu’à l’appel de `setConsent`. |
| `pending` | `in` | Oui | Oui | Les événements placés dans la file d’attente sont envoyés. Un ECID est généré sur la première demande et des cookies d’identité sont définis. |
| `pending` | `out` | Non | Oui | Les événements placés dans la file d’attente sont ignorés. Aucun ECID n’est généré. Le cookie de consentement est défini pour enregistrer les préférences du visiteur. |
| `out` | Non défini | Non | Non | Aucun ECID n’est généré. Aucun cookie n’est défini. Aucun événement n’est envoyé. |
| `out` | `in` | Oui | Oui | Un ECID est généré sur la première demande et des cookies d’identité sont définis. |
| `out` | `out` | Non | Oui | Aucun ECID n’est généré. Le cookie de consentement est défini pour enregistrer les préférences du visiteur. |

>[!NOTE]
>
>Les cookies d’identité et de consentement sont définis même lorsqu’un visiteur opt-out. Ces cookies sont nécessaires pour respecter les préférences de collecte de données du visiteur. Consultez [Cookies Web SDK](https://experienceleague.adobe.com/fr/docs/core-services/interface/data-collection/cookies/web-sdk) pour obtenir la liste complète des cookies définis par Web SDK.

Lorsqu’un visiteur accorde à nouveau son consentement après l’avoir précédemment révoqué (en appelant `setConsent` avec `"general": "in"` après `"general": "out"`), le SDK Web reprend l’envoi des événements et utilise l’ECID existant du cookie s’il n’a pas expiré. L’identité du visiteur est conservée.

Une fois qu’un visiteur a accordé ou refusé son consentement, le SDK Web conserve sa préférence dans un cookie de consentement `kndctr_`. Lors des chargements ultérieurs de la page, le SDK lit ce cookie et applique automatiquement la préférence stockée. Il n’est pas nécessaire de `setConsent` rappeler, sauf si la préférence du visiteur change. Notez que la valeur de configuration `defaultConsent` ne persiste pas entre les chargements de page, mais que le consentement résolu du visiteur (défini via `setConsent`) persiste.

>[!NOTE]
>
>Les événements placés en file d’attente pendant l’`pending` du consentement sont conservés en mémoire et ne survivent pas aux rechargements de page. Si un visiteur accède à une nouvelle page avant la résolution du consentement, les événements de la page précédente placés en file d’attente sont perdus.

## Modèles d’implémentation {#implementation-patterns}

### Modèle Opt-in (consentement requis avant la collecte) {#opt-in}

Utilisez ce modèle lorsque des réglementations (telles que le RGPD) exigent un consentement explicite avant de collecter des données.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "pending"
});

// When the visitor grants consent:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "in" }
  }]
});
```

Avec ce modèle :
* Aucun ECID n’est généré tant que le consentement n’est pas accordé.
* Les événements déclenchés avant le consentement (comme la page vue initiale) sont placés en file d’attente et envoyés après l’octroi du consentement.
* Les cookies d’identité ne sont définis qu’après la première demande Edge Network réussie.

### Modèle d’opt-out (collection par défaut, stop on denial) {#opt-out}

Utilisez ce modèle lorsque les réglementations autorisent la collecte de données par défaut avec une option de désinscription.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "in"
});

// If the visitor opts out:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "out" }
  }]
});
```

Avec ce modèle :
* Un ECID est généré immédiatement au premier chargement de la page.
* Tous les événements sont envoyés jusqu’à ce que le visiteur se désinscrit.
* Après la désinscription, Web SDK cesse d’envoyer des événements, mais les cookies existants restent.

## Consentement avec les identifiants d’appareils propriétaires {#consent-with-fpids}

Si votre implémentation utilise des [identifiants d’appareil interne (FPID)](./fpid.md), le cookie FPID est défini par votre serveur indépendamment de l’état de consentement du SDK Web. Le cookie FPID est un identifiant que vous gérez sur votre propre infrastructure. Cependant, le FPID n’est envoyé à Edge Network que lorsque le SDK Web effectue une requête (qui est validée par le consentement) :

* Avec `defaultConsent: "pending"`, le FPID existe dans le navigateur mais n’est pas utilisé pour envoyer un ECID tant que le consentement n’a pas été accordé.
* Avec `defaultConsent: "in"`, le FPID est utilisé lors de la première requête et amorce immédiatement l’ECID.

Si votre implémentation du consentement nécessite qu’aucun identifiant ne soit défini avant le consentement, retardez la définition du cookie FPID jusqu’à ce que le consentement soit communiqué. Le point de contrôle du consentement de SDK Web seul n’empêche pas la définition du cookie FPID, puisqu’il est géré par votre serveur.

## Pièges courants {#common-pitfalls}

+++**La bannière de consentement efface les cookies d’identité**

**Problème** : certaines plateformes de gestion du consentement (CMP) effacent tous les cookies, y compris les cookies d’identité `kndctr_`, lors de la présentation de la bannière de consentement, avant que le visiteur ne fasse un choix. Lorsque le visiteur accorde son consentement, le Web SDK génère un nouvel ECID, car l’ECID précédent a été supprimé. Le visiteur apparaît comme une nouvelle personne dans les rapports.

**Symptômes** :
* Un pic du nombre de visiteurs uniques après le déploiement d’une bannière de consentement.
* Les visiteurs récurrents sont comptés comme de nouveaux visiteurs à chaque expiration de leur consentement et interagissent à nouveau avec la bannière.

**Solution** : configurez votre CMP pour conserver les cookies `kndctr_`. Ces cookies sont des cookies d’identité, et non des cookies de suivi. Ils identifient l’appareil et ne contiennent pas de données comportementales. Si votre CMP nécessite l’effacement des cookies, ajoutez `kndctr_` cookies prédéfinis à une liste d’exclusion. Vous pouvez également retarder l’effacement des cookies jusqu’à ce que le visiteur rejette explicitement le consentement plutôt que de les effacer de manière préventive.

+++

+++**Un consentement retardé entraîne une identité en double**

**Problème** : lorsque `defaultConsent` est défini sur `pending`, le SDK Web attend le consentement avant d’envoyer des données. Si le consentement est accordé tard dans le cycle de vie de la page (par exemple, après une interaction de bannière qui déclenche le rechargement de la page), la séquence suivante peut entraîner des problèmes :

1. Chargement de la page. `defaultConsent: "pending"`. Web SDK n’envoie pas de requêtes.
2. Le visiteur accorde le consentement. La CMP déclenche un rechargement de page.
3. La page se charge à nouveau. Web SDK s’initialise avec le consentement désormais accordé et génère un ECID.

Ce flux est normal et fonctionne correctement. Le problème se produit lorsque le CMP ou votre mise en œuvre efface par inadvertance les cookies entre les étapes 2 et 3 ou lorsque le SDK Web est configuré différemment au moment du rechargement.

**Solution** : assurez-vous que la configuration de Web SDK (en particulier `orgId` et `defaultConsent`) est identique à chaque chargement de page. Si votre CMP déclenche un rechargement après le consentement, vérifiez que les cookies d’identité survivent au rechargement.

+++

+++**Utilisation de `defaultConsent: "in"` avec une bannière de consentement**

**Problème** : certaines implémentations définissent des `defaultConsent: "in"`, puis appellent des `setConsent` avec des `"general": "out"` si le visiteur refuse. Cette approche génère un ECID et envoie au moins une requête avant que le consentement ne soit refusé. Selon vos exigences réglementaires, cette collecte de données initiale peut ne pas être conforme à la politique de confidentialité de votre organisation.

**Solution** : si votre environnement réglementaire nécessite un consentement avant toute collecte de données ou génération d’ECID, utilisez plutôt `defaultConsent: "pending"` . Ce paramètre permet de s’assurer que Web SDK ne communique pas avec Edge Network tant que le consentement n’a pas été explicitement accordé.

+++
