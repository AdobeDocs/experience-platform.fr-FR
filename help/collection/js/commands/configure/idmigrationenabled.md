---
title: idMigrationEnabled
description: Permet au SDK Web de lire les cookies AMCV.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# `idMigrationEnabled`

La propriété `idMigrationEnabled` permet au SDK Web de lire les cookies AMCV définis par les implémentations Adobe Experience Cloud précédentes. Si votre entreprise met à niveau votre implémentation vers Web SDK, ce paramètre permet une transition plus fluide vers le service Adobe Experience Cloud ID actuel. Ce paramètre est utile pour éviter une forte augmentation du nombre de visiteurs uniques lors de la mise à niveau vers le SDK web.

Si votre organisation exécute une nouvelle implémentation de Web SDK, l’activation de ce paramètre n’a aucun impact sur la collecte de données ou l’identification des visiteurs. Il n’y a aucun inconvénient à ce qu’il soit activé pour toutes les implémentations.

## Fonctionnement de la migration des identités {#how-it-works}

L’API visiteur stocke l’Experience Cloud ID (ECID) dans un cookie appelé `AMCV_<ORG_ID>`. Lorsque `idMigrationEnabled` est `true` (valeur par défaut), le SDK Web lit automatiquement l’ECID à partir du cookie AMCV et l’utilise comme identité du visiteur lors de la première requête Edge Network.

1. Un visiteur arrive sur une page qui utilise désormais le Web SDK plutôt que l’API visiteur.
1. Le SDK Web recherche un cookie d’identité `kndctr_` existant (son propre format de cookie). Si aucun n’est trouvé, il recherche un cookie `AMCV_`.
1. Si un cookie `AMCV_` est identifié, le SDK Web extrait l’ECID et l’utilise pour initialiser l’identité du visiteur.
1. Le SDK Web définit un nouveau cookie d’identité `kndctr_` avec le même ECID.
1. Lors des visites ultérieures, le SDK Web utilise directement le cookie `kndctr_`. Le cookie `AMCV_` n’est plus nécessaire.

Pour que la migration fonctionne, le Web SDK doit être configuré avec le même [`orgId`](/help/collection/js/commands/configure/orgid.md) que celui utilisé par l’API visiteur et doit être déployé sur le même domaine (ou un sous-domaine du même domaine parent) où le cookie AMCV a été défini.

## Scénarios de migration pris en charge

La migration des identifiants prend en charge les schémas de transition suivants :

* **Certaines pages utilisent toujours l’API visiteur tandis que d’autres pages utilisent Web SDK** : le SDK lit les cookies AMCV existants et écrit un nouveau cookie avec l’ECID existant. Il écrit également des cookies AMCV afin que les pages qui utilisent toujours l’API visiteur continuent à reconnaître le même visiteur.
* **Le SDK Web et l’API visiteur sont tous deux présents sur la même page** : si le cookie AMCV n’est pas défini, le SDK recherche l’API visiteur sur la page et l’utilise pour obtenir l’ECID.
* **Le site a été entièrement déplacé vers Web SDK** : vous pouvez laisser la migration activée pendant un certain temps afin que les visiteurs et visiteuses existants basés sur AMCV conservent la continuité pendant que leurs cookies sont transférés.

>[!IMPORTANT]
>
>Ne chargez pas simultanément l’API visiteur et le SDK web sur la même page, sauf si vous avez confirmé que le cookie AMCV est déjà défini. L’exécution des deux bibliothèques sur une seule page peut entraîner des conditions de concurrence où chaque bibliothèque tente de gérer l’identité indépendamment, générant potentiellement des ECID en double ou en conflit.

## Désactiver la migration {#turn-off-migration}

Une fois que l’ensemble de votre site s’exécute sur le Web SDK et qu’aucun visiteur ne porte uniquement un cookie `AMCV_` sans cookie `kndctr_` correspondant, vous pouvez désactiver en toute sécurité la migration d’identité en définissant `idMigrationEnabled` sur `false`. Il s’agit d’une optimisation mineure des performances qui réduit la surface de votre logique d’identité.

Pour vous guider, attendez que la durée de vie maximale du cookie AMCV soit écoulée après la dernière migration de la page. Si vos cookies AMCV ont une expiration de deux ans, attendez deux ans après que la dernière page ait été découpée dans le SDK Web. Dans la pratique, la plupart des entreprises désactivent la migration plus tôt (après quelques mois) et acceptent une quantité négligeable d&#39;inflation du petit nombre de visiteurs qui reviennent pour la première fois après une longue absence.

## Mises à jour des caractéristiques Audience Manager

Lorsque des données au format XDM sont envoyées dans Audience Manager pendant la migration, ces données doivent être converties en signaux. Vos caractéristiques doivent être mises à jour pour refléter les nouvelles clés fournies par XDM. Ce processus est facilité par l’utilisation de l’outil [&#x200B; BAAAM &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html?lang=fr#getting-started-with-bulk-management).

## Migration d’ID tiers {#third-party-id}

Si votre implémentation de l’API visiteur a utilisé des identifiants tiers (cookie `demdex.net`), Web SDK peut également les migrer. Configurez les [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) à `true` dans votre configuration de Web SDK. Le SDK Web lit le cookie Demdex existant et inclut l’identité tierce dans ses requêtes Edge Network, en suivant le même modèle de migration que le cookie AMCV.

## Validation {#validation}

Pour vérifier que la migration d’identité fonctionne correctement :

1. Ouvrez une page qui utilisait auparavant l’API visiteur (qui utilise désormais le SDK Web) dans un navigateur qui possède déjà un cookie `AMCV_`.
2. Dans les outils de développement, vérifiez qu’un cookie d’identité `kndctr_` a été défini et que l’ECID correspond à celui du cookie `AMCV_`.
3. Après le déploiement, comparez les nombres de visiteurs uniques avant et après la migration pour la même période. Un pic significatif de visiteurs uniques peut indiquer que la migration n’est pas porteuse d’identités.

>[!TIP]
>
>Utilisez `getIdentity` pour récupérer par programmation l’ECID à des fins de comparaison :
>
>```js
>alloy("getIdentity", { namespaces: ["ECID"] }).then(function(result) {
>   console.log("ECID:", result.identity.ECID);
>});
>```

## Configuration `idMigrationEnabled` {#configure}

Définissez la valeur booléenne `idMigrationEnabled` lors de l’exécution de la commande `configure`. Si vous omettez cette propriété lors de la configuration de Web SDK, elle est définie par défaut sur `true`. Définissez cette propriété si vous souhaitez désactiver la possibilité de lire les cookies AMCV définis par l’API visiteur. La plupart des organisations n’ont pas besoin de définir cette propriété.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## Activer la migration des identifiants visiteur à l’aide de l’extension de balise Web SDK

Ces paramètres peuvent être configurés dans l’extension de balise Web SDK à l’aide des [&#x200B; Paramètres de configuration des identités &#x200B;](/help/tags/extensions/client/web-sdk/configure/identity.md).
