---
title: Utilisation d’identityMap dans la collecte de données
description: Découvrez comment créer et envoyer des payloads identityMap pour identifier les visiteurs connus dans les espaces de noms de votre implémentation de Web SDK.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 0%

---

# Utilisation d’identityMap dans la collecte de données

L’objet de payload `identityMap` est la manière dont vous indiquez à Edge Network qui est un visiteur au-delà de son [ECID](./overview.md) au niveau de l’appareil. Lorsqu’un visiteur se connecte, effectue un achat ou est connu d’une autre manière, vous pouvez envoyer des identifiants au niveau de la personne (identifiant CRM, e-mail haché, identifiant de fidélité, etc.) avec l’ECID. Ces identifiants au niveau de la personne fournissent des informations précieuses aux services en aval afin qu’ils puissent :

* **Regrouper l’activité à une personne sur plusieurs appareils et canaux.** [Service d’identités](/help/identity-service/home.md) associe les identités que vous envoyez à un [graphique d’identités](/help/identity-service/features/identity-graph-viewer.md), établissant ainsi une connexion entre le comportement anonyme au niveau de l’appareil et une personne connue.
* **Créer des profils client unifiés.** [profil client en temps réel](/help/profile/home.md) utilise l’identité principale que vous avez définie pour ancrer les événements et les attributs à un seul profil, ce qui permet la segmentation au niveau de la personne et la création d’audiences.
* **Activer les audiences sur les destinations en aval.** de nombreuses [destinations](/help/destinations/home.md) nécessitent des identités résolues au niveau de la personne (e-mails hachés, numéros de téléphone, etc.) pour faire correspondre vos audiences à leurs bases d’utilisateurs.
* **Orchestrer des parcours cross-canal.** [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=fr) utilise des identités résolues pour déclencher et personnaliser des parcours sur les canaux e-mail, push et in-app en fonction du comportement authentifié d’un visiteur.

Cette page explique comment créer des payloads `identityMap`, choisir les paramètres appropriés pour chaque identité et gérer les scénarios d’implémentation courants.

## Structure de la payload {#structure}

Le `identityMap` est un objet JSON où chaque clé de niveau supérieur est un espace de noms et la valeur est un tableau de descripteurs d’identité. Vous pouvez inclure un ou plusieurs espaces de noms dans une seule payload et chaque descripteur contient trois champs : `id`, `authenticatedState` et `primary`.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

| Champ | Type | Obligatoire | Description |
| --- | --- | --- | --- |
| `id` | Chaîne | Oui | Valeur de l’identifiant (par exemple, `user@example.com` ou `ABC123`). |
| `authenticatedState` | Chaîne | Oui | Degré de certitude avec lequel vous savez que cette identité appartient au visiteur. Les valeurs valides comprennent `ambiguous`, `authenticated` et `loggedOut`. |
| `primary` | Booléen | Oui | Indique si cette identité doit être l’identifiant principal de l’événement. Une identité exactement sur tous les espaces de noms doit être marquée `primary: true`. |

Les sections ci-dessous présentent en détail chaque partie de la payload.

### Clés d’espace de noms {#namespace-keys}

Chaque clé de niveau supérieur dans `identityMap` est un [espace de noms d’identité](/help/identity-service/features/namespaces.md) — une chaîne qui classe le type d’identifiant (par exemple, `CRMID`, `Email`, `Phone` ou `LoyaltyId`). Les espaces de noms doivent exister dans Identity Service avant de les référencer dans une payload. Vous pouvez inclure plusieurs clés d’espace de noms dans le même événement lorsque vous disposez de plusieurs identifiants pour le visiteur.

Il n’est pas nécessaire d’inclure l’ECID comme clé d’espace de noms. Edge Network ajoute automatiquement l’ECID à la payload de l’identité. Si vous incluez l’ECID explicitement, ne le marquez pas comme `primary` lorsqu’une identité au niveau de la personne est également présente.

### `id` {#id}

Le champ `id` est la chaîne d’identifiant elle-même — la valeur qui indique à Experience Platform quelle personne ou appareil spécifique cette identité représente. Chaque [espace de noms d’identité](/help/identity-service/features/namespaces.md) exige un format de valeur spécifique. L’envoi d’une valeur dans un format incorrect crée une identité distincte qui ne peut pas être fusionnée avec la version correctement formatée, ce qui entraîne la fragmentation des profils.

Avant d’inclure une valeur dans `identityMap`, préparez-la selon le format attendu par votre espace de noms cible :

| Types d’espaces de noms courants | Préparation de la valeur | Exemple |
| --- | --- | --- |
| **CRM / identifiant interne** | Utilisez l’identifiant exact attribué par votre système d’enregistrement. Conservez la cohérence du format pour tous les événements (casse, zéros de début, préfixes). | `ABC-12345`, `00098765` |
| **E-mail (brut)** | Mettez en minuscules l’adresse e-mail complète et supprimez les espaces de début et de fin. | `user@example.com` |
| **E-mail (haché)** | Réduisez d’abord la casse de l’adresse e-mail, puis hachez-la avec SHA-256. Envoyez la chaîne hexadécimale de 64 caractères obtenue. N’ajoutez pas de sel, sauf si votre définition d’espace de noms en requiert un. | `a1b2c3d4e5f6a7b8c9...` |
| **Téléphone (E.164)** | Formatez le nombre en [E.164](https://en.wikipedia.org/wiki/E.164) : un `+` de début, l&#39;indicatif du pays et le numéro de l&#39;abonné sans espaces ni ponctuation. | `+15551234567` |
| **FPID** | Générez une chaîne [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Consultez [Identifiants d’appareil propriétaires](./fpid.md) pour connaître les exigences de génération. | `123e4567-e89b-42d3-9456-426614174000` |

Pour obtenir la liste complète des espaces de noms standard et leurs définitions, voir [ Présentation des espaces de noms d’identité ](/help/identity-service/features/namespaces.md#standard).

>[!TIP]
>
>La valeur `id` respecte la casse. `User@Example.com` et `user@example.com` sont traités comme deux identités distinctes. Normalisez la casse avant d’envoyer la valeur (généralement en mettant en minuscules les e-mails et en réduisant les espaces) pour éviter de créer des identités en double dans le graphique.

#### Collecter les `id` au moment de l’exécution {#collect-id}

L’identifiant dont vous avez besoin est rarement disponible directement sur la page. Les stratégies de collecte courantes sont les suivantes :

* **Couche de données** : lisez l’identifiant à partir de la couche de données de votre site une fois le visiteur connecté. Cet emplacement est l’approche la plus fiable, car la couche de données est renseignée par le serveur principal de votre application et reflète l’état de session authentifié.
* **Jeton d’authentification ou cookie de session** : décodez ou recherchez l’identifiant d’un cookie JWT ou de session défini par votre système d’authentification. Vérifiez que le jeton est toujours actif avant d’utiliser la valeur .
* **Enrichissement côté serveur** : utilisez [Préparation des données pour la collecte de données](/help/datastreams/data-prep.md) ou une règle de transfert d’événement [event](/help/tags/ui/event-forwarding/overview.md) pour mapper ou transformer l’identifiant au niveau d’Edge avant qu’il n’atteigne les services en aval. Cet emplacement est utile lorsque le client ne dispose que d’un jeton de session opaque qui correspond à un ID interne côté serveur.

>[!TIP]
>
>Si une valeur de `id` donnée est résolue sur une chaîne, une `null` ou une `undefined` vide, n’incluez pas l’espace de noms dans le `identityMap`. L’envoi d’un `id` vide crée un enregistrement d’identité rompu. Protégez votre implémentation avec une vérification avant de créer la payload.

### `authenticatedState` {#authenticated-state}

Le champ `authenticatedState` indique aux services en aval le niveau de confiance à accorder à une identité donnée. Les valeurs suivantes sont valides pour ce champ :

| Valeur | Quand l’utiliser |
| --- | --- |
| **`authenticated`** | Le visiteur a prouvé activement son identité au cours de la session en cours (par exemple, en se connectant avec des informations d’identification, en complétant une authentification multifacteur ou une vérification similaire). |
| **`loggedOut`** | Le visiteur a été authentifié précédemment mais s’est déconnecté depuis. L’identité est toujours associée à l’appareil, mais la session n’est plus active. |
| **`ambiguous`** | L’identité ne peut pas être confirmée comme appartenant au visiteur actuel. Utilisez cette valeur pour les identifiants au niveau de l’appareil, tels que les FPID, ou pour tout identifiant pour lequel l’authentification n’a pas encore eu lieu. |

>[!TIP]
>
>La valeur `authenticatedState` affecte la manière dont Adobe Experience Platform Identity Service crée et fusionne des graphiques d’identités. L’envoi de `authenticated` pour une identité qui n’a pas été vérifiée peut créer des liens incorrects entre appareils, qui sont difficiles à annuler.

### `primary` {#primary-identity}

Chaque payload `identityMap` doit comporter exactement une identité marquée comme `primary: true`. L’identité principale détermine l’identité utilisée comme ancrage de l’événement dans Experience Platform.

Suivez ces instructions lors de la définition de l’identité principale :

* **Lorsqu’une identité au niveau de la personne est disponible** (le visiteur est connecté), marquez l’espace de noms au niveau de la personne comme principal et l’ECID comme non principal. Cela indique à Experience Platform d’ancrer l’événement à la personne plutôt qu’à l’appareil.
* **Lorsque seules des identités au niveau de l’appareil sont disponibles** (le visiteur est anonyme), l’ECID est automatiquement utilisé comme identité principale. Il n’est pas nécessaire d’inclure l’ECID dans votre `identityMap` : Edge Network l’ajoute automatiquement.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

## Envoi d’identityMap dans votre implémentation {#send-identity}

>[!BEGINTABS]

>[!TAB Bibliothèque ]

Transmettez le `identityMap` dans l’objet `xdm` d’un appel [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) :

```js
alloy("sendEvent", {
  xdm: {
    identityMap: {
      CRMID: [
        {
          id: "abc-123-xyz",
          authenticatedState: "authenticated",
          primary: true
        }
      ]
    },
    eventType: "web.webpagedetails.pageViews"
  }
});
```

>[!TAB Extension de balise Web SDK]

Utilisez le type d’élément de données [Mappage d’identités](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) pour créer la payload d’identité dans l’interface utilisateur des balises :

1. Créez un élément de données avec l’extension **[!UICONTROL Adobe Experience Platform Web SDK]** et le type d’élément de données **[!UICONTROL Identity map]**.
2. Ajoutez des identités en spécifiant l’espace de noms, l’élément de données ou la valeur qui est résolu sur l’identifiant et l’état authentifié.
3. Marquez une identité comme principale.
4. Référencez cet élément de données dans votre action **[!UICONTROL Send event]** sous **[!UICONTROL Identity map]**.

>[!ENDTABS]

## Scénarios courants {#common-scenarios}

+++**Connexion**

Lorsqu’un visiteur se connecte, envoyez son identifiant de niveau personne avec `authenticatedState: "authenticated"` et `primary: true`. Incluez cette identité sur le premier événement après l’authentification et sur tous les événements suivants de la session.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

+++

+++**Déconnexion**

Lorsqu’un visiteur se déconnecte, mettez à jour la `authenticatedState` sur `loggedOut` tout en conservant le même identifiant. Cela permet de conserver l’association entre l’appareil et la personne tout en signalant que la session n’est plus active.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "loggedOut",
        "primary": false
      }
    ]
  }
}
```

Après la déconnexion, l’ECID revient à être l’identité principale effective (Edge Network l’applique automatiquement). Ne marquez pas une autre identité de niveau personne comme principale, sauf si le visiteur se connecte avec un autre compte.

>[!IMPORTANT]
>
>N’arrêtez pas complètement l’envoi de l’identifiant après la déconnexion. Le passage de `authenticated` à `loggedOut` indique aux services en aval que la session s’est terminée. L’omission de l’identifiant laisse un espace dans le graphique d’identités qui peut entraîner la fragmentation des profils.

+++

+++**Espaces de noms multiples**

Vous pouvez envoyer plusieurs espaces de noms d’identité dans le même événement. Ce scénario est courant lorsqu’un visiteur est connecté et que vous disposez de plusieurs identifiants (par exemple, un identifiant CRM, un e-mail haché et un identifiant de fidélité). Incluez tous les identifiants connus, marquez un seul comme principal et définissez les autres sur `primary: false`.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email_LC_SHA256": [
      {
        "id": "a1b2c3d4e5f6...",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ],
    "LoyaltyId": [
      {
        "id": "LOY-98765",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

>[!TIP]
>
>L’envoi de plusieurs espaces de noms avec le même `authenticatedState` sur le même événement fournit au service d’identités le signal le plus puissant pour lier ces identités. Incluez tous les identifiants disponibles au point d’authentification plutôt que de les répartir sur plusieurs événements distincts.

+++

+++**Visiteurs anonymes**

Pour les visiteurs anonymes, il n’est généralement pas nécessaire d’envoyer de `identityMap`. Edge Network attribue automatiquement un ECID et l’utilise comme identité principale. Si vous utilisez des [identifiants d’appareil propriétaires](./fpid.md), le FPID est la seule identité que vous devez inclure pour les visiteurs anonymes.

+++

## Comment identityMap affecte le graphique d’identités {#identity-graph}

Chaque payload de `identityMap` qui atteint Experience Platform est traitée par [Service d’identités](/help/identity-service/home.md), qui lie les identités que vous envoyez à un [graphique d’identités](/help/identity-service/features/identity-graph-viewer.md). Les espaces de noms que vous incluez, la manière dont vous définissez les `authenticatedState` et l’identité que vous marquez comme `primary` déterminent directement la manière dont Identity Service crée et fusionne ces graphiques.

Comportements clés à connaître :

* **Les identités envoyées sur le même événement sont liées.** Si vous incluez un CRMID et un espace de noms d’e-mail sur le même appel `sendEvent`, Identity Service crée un lien entre ces deux identités. La diffusion des identifiants sur des événements distincts génère des liens plus faibles et peut entraîner la fragmentation des graphiques.
* **L’identité `primary` ancre l’événement dans le profil client en temps réel.** profil utilise l’identité principale pour déterminer à quel profil l’événement appartient. Le marquage d’une identité incorrecte en tant que principale (par exemple, la définition de l’ECID en tant que principal lorsqu’un identifiant au niveau de la personne est disponible) peut entraîner le stockage d’événements par rapport aux profils au niveau de l’appareil plutôt que des profils au niveau de la personne.
* **La `authenticatedState` influence le degré de confiance du graphique.** L’envoi de `authenticated` pour une identité qui n’a pas réellement été vérifiée peut créer des liens incorrects entre appareils, qui sont difficiles à annuler. N’utilisez `authenticated` que lorsque le visiteur a prouvé activement son identité au cours de la session en cours.

Si votre implémentation utilise des [règles de liaison de graphiques d’identités](/help/identity-service/identity-graph-linking-rules/overview.md) (telles que la priorité de l’espace de noms ou l’algorithme d’optimisation des identités), consultez le [guide d’implémentation](/help/identity-service/identity-graph-linking-rules/implementation-guide.md) pour comprendre comment ces règles interagissent avec les identités que vous envoyez via `identityMap`.

>[!NOTE]
>
>Le `identityMap` n’est envoyé que lorsque le SDK Web adresse une requête à Edge Network, qui est validée par l’état de consentement du visiteur. Si votre implémentation utilise `defaultConsent: "pending"`, les identités ne sont pas envoyées tant que le consentement n’a pas été accordé. Voir [ Consentement et identité ](./consent.md) pour plus d’informations.
