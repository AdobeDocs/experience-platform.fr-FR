---
title: Prise en charge des identités unifiées dans la collecte de données
description: Découvrez comment la prise en charge d’identité unifiée associe la persistance propriétaire et l’activation tierce prise en charge dans la collecte de données web.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 32c2565d31eed4eda28195afaf82aac6f04a6f8a
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# Prise en charge des identités unifiées dans la collecte de données

>[!AVAILABILITY]
>
>Cette fonctionnalité est actuellement en version bêta. La disponibilité, le comportement et la documentation peuvent changer.

La prise en charge d’identité unifiée permet à Edge Network de fonctionner dans des contextes d’identité propriétaires et tiers. Il associe une identification propriétaire durable sur vos propriétés à des workflows d’activation tiers dans les navigateurs qui prennent en charge les cookies tiers. Pour en savoir plus sur la façon dont le SDK Web gère les ECID, les FPID et d’autres signaux d’identité, voir [Identité dans la collecte de données](./overview.md).

Grâce à la prise en charge des identités unifiées, vous pouvez :

* **Optimiser la portée de l’audience** : activez vos audiences Experience Platform sur des destinations tierces (DSP, SSP et réseaux publicitaires) pour une plus grande part de votre trafic.
* **Maintenir la précision des mesures** : Conservez une identification cohérente des visiteurs dans vos propriétés et plateformes publicitaires.
* **Mettez votre implémentation à l’épreuve du temps** : utilisez des identifiants d’appareil propriétaires comme base tout en conservant la compatibilité avec les workflows d’activation tiers.

Lorsqu’un visiteur ou une visiteuse arrive sur votre site, Edge Network évalue les signaux d’identité disponibles, liant automatiquement des contextes propriétaires et tiers lorsque les conditions le permettent. Les navigateurs qui bloquent les cookies tiers continuent à fonctionner en mode propriétaire sans perturber votre implémentation.

## Fonctionnement

Edge Network génère des ECID en évaluant les signaux d’identité disponibles dans l’ordre de priorité suivant :

| Priorité | Source | Contexte | Comportement |
| --- | --- | --- | --- |
| 1 | **ID Demdex** | Troisième niveau | Si un ID Demdex est présent, l’ECID est prédéfini à partir de celui-ci. Cet adresse de contrôle produit un ECID cohérent sur tous les domaines qui partagent le même cookie tiers. |
| 2 | **FPID** | Premier niveau | Si aucun ID Demdex n’est présent, mais qu’un FPID existe, l’ECID est prédéfini à partir du FPID et un ID Demdex en est dérivé. |
| 3 | **Random** | Premier niveau | Si aucun ID Demdex ou FPID n’est disponible, un nouvel ECID aléatoire est généré et un ID Demdex est dérivé de celui-ci. |

Les ECID et les ID Demdex sont liés cryptographiquement par un algorithme déterministe, ce qui signifie que l’un peut être dérivé de l’autre. C’est cette relation qui permet à Edge Network de traduire entre des contextes d’identité propriétaires et tiers sans nécessiter de logique de gestion des visiteurs distincte dans votre implémentation.

Comme la relation est déterministe, les audiences créées sur des ECID propriétaires peuvent être activées via une infrastructure tierce lorsque l’identifiant Demdex correspondant est disponible.

Pour les visiteurs qui disposent déjà d’un ECID dérivé de FPID, Edge Network peut automatiquement lier leur identité propriétaire au contexte d’identité tiers. Cela se produit de manière transparente lorsque le navigateur prend en charge les cookies tiers et ne nécessite aucune modification de votre implémentation. Lorsque la liaison automatique se produit :

1. Edge Network détecte que l’ECID du visiteur n’est pas dérivé d’un ID Demdex.
1. Si le navigateur du visiteur prend en charge les cookies tiers, une synchronisation allégée des identités est déclenchée.
1. Le système crée un lien entre l’ECID propriétaire du visiteur et son identité tierce.
1. Le lien est stocké dans le magasin d’identités, ce qui permet l’activation de l’audience sur des destinations tierces.

La liaison automatique préserve les ECID existants et empêche l’altération du profil des visiteurs. Au fil du temps, une plus grande partie de votre audience devient progressivement éligible à l’activation tierce à mesure que les visiteurs reviennent et que la liaison se produit.

L’activation des audiences tierces repose sur la synchronisation des identifiants (synchronisation des identifiants). Lorsque l’Edge Network établit ou actualise une identité tierce, il renvoie des instructions de synchronisation des identifiants dans la réponse. Ces instructions demandent au navigateur de synchroniser l’identité du visiteur avec les domaines partenaires (DSP, réseaux publicitaires et autres plateformes d’activation), afin que vos audiences Experience Platform puissent être mises en correspondance et diffusées sur ces plateformes.

## Conditions préalables

La prise en charge des identités unifiées requiert tous les éléments suivants :

* Votre site utilise la collecte de données propriétaire sur un domaine que vous contrôlez.
* Votre implémentation utilise des FPID ou une autre stratégie de persistance propriétaire comme base.
* Les cookies tiers sont activés dans votre configuration de Web SDK.
* La synchronisation des identifiants tiers est activée pour le flux de données.
* Le visiteur utilise un navigateur qui autorise les cookies tiers (voir [Compatibilité des navigateurs](#browser-compatibility) ci-dessous).

## Configuration

1. **Activer les cookies tiers dans Web SDK** : activez le paramètre **Utiliser des cookies tiers** dans votre implémentation de Web SDK. Si vous utilisez l’extension de balise, activez la **[!UICONTROL Use third-party cookies]** dans [Paramètres de configuration des identités](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies). Si vous utilisez la bibliothèque JavaScript, définissez [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) sur `true`.

1. **Activer la synchronisation des identifiants tiers dans le flux de données** : activez l’option **[!UICONTROL Third-Party ID Sync]** dans les paramètres avancés de votre flux de données. Voir [Création et configuration des flux de données](/help/datastreams/configure.md#advanced-options).

1. **Assurez-vous que la persistance propriétaire est en place** : vérifiez que votre stratégie de persistance propriétaire (telle que les FPID) est déjà déployée sur votre domaine. Voir [Identifiants d’appareils propriétaires dans la collecte de données](fpid.md).

## Validation

Pour vérifier que la prise en charge d’identité unifiée fonctionne :

1. Ouvrez les outils de développement de votre navigateur et accédez à l’onglet **Réseau**.
1. Effacez les requêtes existantes et déclenchez un événement Web SDK (chargement de page ou événement personnalisé) dans une nouvelle session ou en privé.
1. Recherchez la réponse Edge Network (recherchez les appels à `adobedc.demdex.net` et à votre point d’entrée de collecte propriétaire).
1. Inspectez la payload de réponse pour obtenir des instructions de synchronisation des identifiants.

Lorsque des instructions de synchronisation des identifiants sont présentes, la réponse inclut un handle `identity:exchange` similaire à ce qui suit :

```json
{
  "handle": [
    {
      "type": "identity:exchange",
      "payload": [
        {
          "type": "url",
          "id": 411,
          "spec": {
            "url": "https://example.com/...",
            "hideReferrer": false,
            "ttlMinutes": 10080
          }
        },
        {
          "type": "url",
          "id": 89,
          "spec": {
            "url": "https://example.org/...",
            "hideReferrer": true,
            "ttlMinutes": 10080
          }
        }
      ]
    }
  ]
}
```

| Élément | Description |
| --- | --- |
| `type: "identity:exchange"` | Indique la présence d’instructions de synchronisation des identifiants. |
| tableau `payload` | Liste des URL de synchronisation des identifiants de partenaires. |
| `url` valeurs | Rediriger les URL vers des domaines partenaires pour la synchronisation des identifiants. |
| `id` valeurs | Identifiants de partenaire. |

>[!TIP]
>
>Si vous ne voyez pas l’identificateur `identity:exchange` dans la réponse :
>
>* Assurez-vous d’effectuer un test avec une nouvelle session de navigateur ou en navigation privée. Les identités existantes ne déclenchent pas de nouvelles synchronisations.
>* Vérifiez que les paramètres du flux de données et de Web SDK sont correctement configurés.
>* Vérifiez que vous utilisez un navigateur qui prend en charge les cookies tiers (voir le tableau ci-dessous).

Après avoir confirmé l’activité de synchronisation des identifiants, vérifiez les points suivants :

* L’identité propriétaire persiste comme prévu lors du chargement des pages sur votre domaine.
* Les flux d’activation et de création de rapports se comportent comme prévu dans les environnements que vous prenez en charge.

## Compatibilité des navigateurs {#browser-compatibility}

Les fonctionnalités d’identité tierces dépendent de la prise en charge par le navigateur des cookies tiers. Le tableau suivant résume le comportement attendu :

| Navigateur | Prise en charge des cookies tiers | Demdex disponible | Comportement de l’identité |
| --- | --- | --- | --- |
| Google Chrome | Pris en charge | Oui | Demdex → ECID (cohérent entre les domaines) |
| Microsoft Edge | Pris en charge par défaut | Oui | Demdex → ECID (cohérent entre les domaines) |
| Mozilla Firefox | Bloqué par défaut (ETP) | Non (par défaut) | FPID → ECID (par domaine) |
| Apple Safari | Bloqué (ITP) | Non | FPID → ECID (par domaine) |

Pour les navigateurs qui bloquent les cookies tiers, l’identification propriétaire continue à fonctionner normalement. Les fonctionnalités d’activation tierces ne sont disponibles que lorsque le navigateur autorise les cookies tiers.

## Limites

* Le comportement des identités tierces dépend entièrement du navigateur du visiteur qui autorise les cookies tiers. Il n’existe aucune solution de secours pour l’activation tierce dans les navigateurs qui les bloquent.
* La liaison automatique nécessite que le visiteur revienne sur le site. La part de votre audience éligible à l’activation par un tiers augmente progressivement au fil du temps.
