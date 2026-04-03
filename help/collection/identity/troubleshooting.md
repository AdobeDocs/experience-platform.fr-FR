---
title: Résolution des problèmes d’identité dans la collecte de données
description: Diagnostiquez les problèmes d’identité courants dans les implémentations de Web SDK, notamment le gonflement des visiteurs, les incohérences d’ECID, les conflits de cookies et les problèmes FPID.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# Résolution des problèmes d’identité dans la collecte de données

Les problèmes d’identité apparaissent souvent sous la forme de symptômes dans les rapports en aval (nombre de visiteurs exagéré, profils fragmentés ou personnalisation rompue) plutôt que sous la forme d’erreurs dans la mise en œuvre elle-même. Cette page vous aide à diagnostiquer et à résoudre les problèmes d’identité les plus courants dans les implémentations de Web SDK. Pour en savoir plus sur le fonctionnement de l’identité dans la collecte de données, consultez la [présentation des identités](./overview.md).

## Inspecter les valeurs d’identité {#inspect-identity}

Avant de résoudre un problème spécifique, récupérez les valeurs d’identité actuelles utilisées par Web SDK. Utilisez la commande [`getIdentity`](/help/collection/js/commands/getidentity.md) pour afficher l’ECID et d’autres signaux d’identité :

```js
alloy("getIdentity", { namespaces: ["ECID", "CORE"] }).then(function(result) {
  console.log("ECID:", result.identity.ECID);
  console.log("CORE ID:", result.identity.CORE);
  console.log("Edge region:", result.edge.regionID);
});
```

Vous pouvez également examiner les valeurs d’identité dans les outils de développement de votre navigateur :

1. Ouvrez l’onglet **Application** (Chrome/Edge) ou **Stockage** (Firefox/Safari).
2. Recherchez les cookies dotés du préfixe `kndctr_` sur votre domaine. Le cookie `kndctr_<ORG_ID>_AdobeOrg_identity` contient l’ECID.
3. Ouvrez l’onglet **Réseau** et recherchez une requête `interact` ou `collect` à Edge Network. Inspectez la payload de requête pour `identityMap` et la payload de réponse pour les handles d’identité.

## Problèmes courants {#common-issues}

+++**Inflation du nombre de visiteurs**

**Symptôme** : les rapports Analytics affichent plus de visiteurs uniques que prévu ou la même personne apparaît comme plusieurs visiteurs sur l’ensemble des sessions.

**Causes possibles** :

| Cause | Comment identifier | Résolution |
| --- | --- | --- |
| Durée de vie courte du cookie | Vérifiez l’expiration des cookies `kndctr_` dans le navigateur. S’ils expirent dans 7 jours ou moins, les politiques de navigateur limitent probablement la durée des cookies. | Implémentez des [identifiants d’appareil interne (FPID)](./fpid.md) définis à partir d’un serveur à l’aide d’un enregistrement DNS A/AAAA pour une persistance plus longue des cookies. |
| FPID manquant à la première demande | Inspectez la première requête Edge Network au chargement de la page. Si aucun cookie FPID n’est présent, Edge Network génère un nouvel ECID. Si le FPID est défini après la première requête, l’ECID généré lors de cette première requête est orphelin. | Définissez le cookie FPID avant que le SDK Web n’envoie sa première requête. Voir [Quand définir le cookie &#x200B;](./fpid.md#when-to-set-cookie). |
| Incompatibilité de `orgId` entre les domaines | Comparez la valeur de configuration `orgId` sur tous vos domaines. Les valeurs incohérentes entraînent des portées d’identité distinctes. | Utilisez le même [`orgId`](/help/collection/js/commands/configure/orgid.md) sur tous les domaines de votre organisation. |
| Bannière de consentement supprimant les cookies | Si votre implémentation de consentement efface tous les cookies avant que le consentement ne soit accordé, puis que le SDK Web s’initialise, un nouvel ECID est généré. | Configurez votre bannière de consentement pour conserver les cookies `kndctr_` ou retarder l’initialisation de Web SDK jusqu’à ce que le consentement soit établi. Voir aussi [&#x200B; Consentement et identité &#x200B;](./consent.md). |
| Cookies FPID définis par JavaScript | Les cookies définis à l’aide de `document.cookie` sont soumis à des restrictions de navigateur (ITP, ETP) qui limitent leur durée de vie, parfois à seulement 24 heures. | Définissez les cookies FPID à partir du serveur à l’aide d’un enregistrement DNS A/AAAA, et non à partir de JavaScript. |

+++

+++**L’ECID change de manière inattendue entre les pages**

**Symptôme** : l’ECID est différent sur différentes pages du même domaine ou change à chaque chargement de page.

**Étapes de diagnostic** :

1. Vérifiez que le cookie d’identité `kndctr_` est présent sur les deux pages. S’il manque sur une page, vérifiez que le SDK Web est configuré sur cette page.
2. Vérifiez que le domaine du cookie est défini suffisamment largement. Un cookie défini sur `shop.example.com` n’est pas disponible sur `www.example.com`. Assurez-vous que l’infrastructure de collecte propriétaire et de définition de cookies utilise la même portée de domaine.
3. Recherchez le JavaScript qui efface les cookies lors de la navigation (par exemple, les scripts de consentement des cookies agressifs ou les outils de confidentialité).
4. Si vous utilisez une application d’une seule page, vérifiez que le SDK Web est configuré une fois à l’initialisation de l’application, et non réinitialisé à chaque changement d’itinéraire. La réinitialisation peut générer un nouvel ECID.

+++

+++**Le FPID n’est pas l’origine de l’ECID**

**Symptôme** : vous avez défini un cookie FPID, mais `getIdentity` renvoie un ECID qui n’est pas cohérent entre les visites, ou le FPID n’apparaît pas dans les payloads de requête Edge Network.

**Étapes de diagnostic** :

1. **Vérifier le format du cookie FPID** : le FPID doit être un [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122) valide. Ouvrez les outils de développement de votre navigateur, recherchez le cookie FPID et vérifiez que la valeur correspond au modèle `xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx`.
2. **Vérifiez le nom du cookie dans le flux de données** : si vous utilisez la méthode de cookie [datastream](./fpid.md#setting-cookie-datastreams), le nom du cookie configuré dans le flux de données doit correspondre exactement au nom du cookie défini par votre serveur.
3. **Vérifiez que le cookie est envoyé sur la requête** : dans l&#39;onglet Réseau , examinez l&#39;en-tête `Cookie` sur la requête Edge Network. Le cookie FPID doit être inclus.
4. **Vérifier la priorité des identités** : si un ECID existant est déjà stocké dans un cookie `kndctr_`, il est prioritaire sur le FPID. Le FPID n’enregistre un nouvel ECID que lorsqu’aucun ECID existant n’est présent. Voir [Fonctionnement des FPID](./fpid.md#how-fpids-work) pour l’ordre de priorité complet.
5. **Valider le CNAME** : en cas d’utilisation de la méthode de cookie du flux de données, vérifiez que le CNAME de votre collection propriétaire est correctement configuré et que les requêtes y sont acheminées.

+++

+++**L’identité inter-domaines ne fonctionne pas**

**Symptôme** : un visiteur qui clique sur l’un de vos domaines pour en consulter un autre est traité comme un nouveau visiteur sur le domaine de destination.

**Étapes de diagnostic** :

1. **Vérifier l’URL** : inspectez l’URL de destination lorsque le visiteur clique sur le lien. Il doit contenir un paramètre de chaîne de requête `adobe_mc`. Si le paramètre est manquant, le domaine source ne l’ajoute pas. Voir [&#x200B; Implémentation du partage inter-domaines](./cross-domain-sharing.md#implement-cross-domain-sharing).
2. **Vérifier le minutage** : le paramètre `adobe_mc` expire au bout de cinq minutes. Si le chargement de la page de destination prend trop de temps (en raison, par exemple, de redirections ou d’un réseau lent), le paramètre peut expirer avant que le SDK Web ne puisse le lire.
3. **Vérifier `orgId` correspondance** : les deux domaines doivent utiliser la même [`orgId`](/help/collection/js/commands/configure/orgid.md). Les identifiants d’organisation incompatibles entraînent le rejet par le domaine de destination de l’identité transmise.
4. **Confirmer que Web SDK est sur la destination** : la page de destination doit disposer de Web SDK installé et configuré. Sans cela, le paramètre `adobe_mc` est ignoré.
5. **Rechercher l’effacement d’URL** : certains services de redirection, réseaux CDN ou paramètres de chaîne de requête inconnus sont effacés par une logique côté serveur. Vérifiez que `adobe_mc` survit à toute redirection intermédiaire entre les pages source et de destination.

+++

+++**Échec du transfert d’identité mobile vers le web**

**Symptôme** : un visiteur qui démarre dans l’application mobile et ouvre un navigateur WebView ou mobile est traité comme un nouveau visiteur du côté web.

**Étapes de diagnostic** :

1. **Vérifier l’URL** : consignez l’URL transmise à WebView. Il doit contenir un paramètre `adobe_mc` généré par [`getUrlVariables`](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables).
2. **Vérifier les versions de SDK** : l’extension mobile Identity for Edge Network doit être de la version 1.1.0 ou ultérieure, et le SDK Web doit être de la version 2.11.0 ou ultérieure.
3. **Vérifier le timing** : comme pour le partage inter-domaines, le paramètre `adobe_mc` expire au bout de cinq minutes. Assurez-vous que WebView se charge rapidement après la construction de l’URL.
4. **Confirmer `orgId` correspondance** : l’ID d’organisation Experience Cloud doit être le même dans les configurations SDK mobile et SDK web.

+++
