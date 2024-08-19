---
title: Conseils sur le client de l’agent utilisateur
description: Découvrez comment les conseils client de l’agent utilisateur fonctionnent dans le SDK Web. Les conseils aux clients permettent aux propriétaires de sites web d’accéder à une grande partie des mêmes informations disponibles dans la chaîne de l’agent utilisateur, mais de manière plus respectueuse de la vie privée.
keywords: user-agent;conseils client ; chaîne ; chaîne user-agent ; faible entropie ; grande entropie
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 89dfe037e28bae51e335dc67185afa42b2c418e3
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 4%

---

# Conseils sur le client de l’agent utilisateur

## Vue d’ensemble {#overview}

Chaque fois qu’un navigateur Web envoie une requête à un serveur Web, l’en-tête de la requête inclut des informations sur le navigateur et l’environnement sur lequel le navigateur est exécuté. Toutes ces données sont agrégées dans une chaîne appelée chaîne de l’agent utilisateur.

Voici un exemple de ce à quoi ressemble une chaîne d’agent utilisateur sur une requête provenant d’un navigateur Chrome s’exécutant sur un appareil [!DNL Mac OS].

>[!NOTE]
>
>Au fil des ans, la quantité d’informations de navigateur et d’appareil incluses dans la chaîne de l’agent utilisateur a augmenté et changé plusieurs fois. L’exemple ci-dessous illustre une sélection des informations les plus courantes sur l’agent utilisateur.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| Champ | Valeur |
|---|---|
| Nom du logiciel | Chrome |
| Version logicielle | 105 |
| Version complète du logiciel | 105.0.0.0 |
| Nom du moteur de mise en page | AppleWebKit |
| Version du moteur de mise en page | 537,36 |
| Operating system (Système d’exploitation) | MAC OS X |
| Version du système d’exploitation | 10.15.7 |
| Appareil | Intel Mac OS X 10_15_7 |

## Cas d’utilisation {#use-cases}

Les chaînes d’agent utilisateur ont longtemps été utilisées pour fournir aux équipes de marketing et de développement des informations importantes sur la manière dont les navigateurs, les systèmes d’exploitation et les périphériques affichent le contenu du site, ainsi que sur la manière dont les utilisateurs interagissent avec les sites web.

Les chaînes d’agent utilisateur sont également utilisées pour bloquer les messages indésirables et filtrer les robots qui analysent les sites à diverses fins supplémentaires.

## Chaînes d’agent utilisateur dans Adobe Experience Cloud {#user-agent-in-adobe}

Les solutions Adobe Experience Cloud utilisent les chaînes de l’agent utilisateur de différentes manières.

* Adobe Analytics utilise la chaîne de l’agent utilisateur pour augmenter et obtenir des informations supplémentaires sur les systèmes d’exploitation, les navigateurs et les périphériques utilisés pour visiter un site web.
* Adobe Audience Manager et Adobe Target permettent aux utilisateurs finaux de réaliser des campagnes de segmentation et de personnalisation sur la base des informations fournies par la chaîne de l’agent utilisateur.

## Présentation des conseils sur les clients de l’agent utilisateur {#ua-ch}

Au cours des dernières années, les propriétaires de site et les vendeurs marketing ont utilisé des chaînes d’agent utilisateur ainsi que d’autres informations incluses dans les en-têtes de demande pour créer des empreintes digitales. Ces empreintes digitales peuvent être utilisées pour identifier les utilisateurs à leur insu.

Malgré l’objectif important que les chaînes d’agent utilisateur remplissent pour les propriétaires de site, les développeurs de navigateur ont décidé de modifier le fonctionnement des chaînes d’agent utilisateur, afin de limiter les éventuels problèmes de confidentialité pour les utilisateurs finaux.

La solution qu’ils ont développée s’appelle [user agent client indice](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Les conseils aux clients permettent toujours aux sites web de collecter les informations nécessaires sur les navigateurs, les systèmes d’exploitation et les appareils, tout en offrant une protection accrue contre les méthodes de suivi secrètes, telles que l’empreinte digitale.

Les conseils aux clients permettent aux propriétaires de sites web d’accéder à une grande partie des mêmes informations disponibles dans la chaîne de l’agent utilisateur, mais de manière plus respectueuse de la vie privée.

Lorsque les navigateurs modernes envoient un utilisateur vers un serveur web, la chaîne entière de l’agent utilisateur est envoyée à chaque demande, qu’elle soit requise ou non. Les conseils du client, en revanche, imposent un modèle dans lequel le serveur doit demander au navigateur les informations supplémentaires qu’il souhaite connaître sur le client. Lors de la réception de cette requête, le navigateur peut appliquer ses propres stratégies ou sa propre configuration utilisateur pour déterminer les données renvoyées. Au lieu d’exposer la chaîne entière de l’agent utilisateur par défaut sur toutes les requêtes, l’accès est désormais géré de manière explicite et auditable.

## Prise en charge des navigateurs {#browser-support}

[Des conseils sur le client de l’agent utilisateur](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) ont été introduits avec [!DNL Google Chrome]version 89.

D’autres navigateurs Chromium prennent en charge l’API Client Hints, tels que :

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Catégories {#categories}

Il existe deux catégories d’indices client de l’agent utilisateur :

* [Conseils sur les clients à faible entropie](#low-entropy)
* [Conseils client à forte entropie](#high-entropy)

### Conseils sur les clients à faible entropie {#low-entropy}

Les indices client à faible entropie incluent des informations de base qui ne peuvent pas être utilisées pour les utilisateurs d’empreinte digitale. Informations telles que la marque du navigateur, la plateforme et si la demande provient d’un appareil mobile.

Les conseils client à faible entropie sont activés par défaut dans le SDK Web et sont transmis à chaque demande.

| En-tête HTTP | JavaScript | Inclus par défaut dans User-Agent | Inclus par défaut dans les conseils client |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | Oui | Oui |
| `Sec-CH-UA-Platform` | `platform` | Oui | Oui |
| `Sec-CH-UA-Mobile` | `mobile` | Oui | Oui |

### Conseils client à forte entropie {#high-entropy}

Les conseils client à forte entropie sont des informations plus détaillées sur l’appareil client, telles que la version de la plateforme, l’architecture, le modèle, la résolution (plateformes 64 ou 32 bits) ou la version complète du système d’exploitation. Ces informations peuvent éventuellement être utilisées pour l’empreinte digitale.

| Propriété | Description | En-tête HTTP | Chemin XDM | Exemple | Inclus par défaut dans l’agent utilisateur | Inclus par défaut dans les conseils client |
| --- | --- | --- | --- | --- |---|---|
| Version du système d’exploitation | Version du système d’exploitation. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` | Oui | Non |
| Architecture | Architecture du processeur sous-jacent. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` | Oui | Non |
| Modèle de périphérique | Nom du périphérique utilisé. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` | Oui | Non |
| Bitness | Nombre de bits pris en charge par l’architecture du processeur sous-jacente. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` | Oui | Non |
| Fournisseur du navigateur | Société qui a créé le navigateur. L’indice d’entropie faible `Sec-CH-UA` collecte également cet élément. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` | Oui | Non |
| Nom du navigateur | Le navigateur utilisé. L’indice d’entropie faible `Sec-CH-UA` collecte également cet élément. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` | Oui | Non |
| Version du navigateur | Version significative du navigateur. L’indice d’entropie faible `Sec-CH-UA` collecte également cet élément. La version exacte du navigateur n’est pas collectée automatiquement. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` | Oui | Non |


Les indices client à forte entropie sont désactivés par défaut dans le SDK Web. Pour les activer, vous devez configurer manuellement le SDK Web afin de demander des conseils client à forte entropie.

## Impact des indices client à forte entropie sur les solutions Experience Cloud {#impact-in-experience-cloud-solutions}

Certaines solutions Adobe Experience Cloud reposent sur des informations incluses dans les conseils client à forte entropie lors de la génération de rapports.

Si vous n’activez pas les indicateurs client à forte entropie dans votre environnement, les caractéristiques et rapports Adobe Analytics et d’Audience Manager décrits ci-dessous ne fonctionneront pas.

### Rapports Adobe Analytics reposant sur des indices client à forte entropie {#analytics}

La dimension [Système d’exploitation](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html) comprend la version du système d’exploitation stockée en tant qu’indice client à forte entropie. Si les indices des clients à forte entropie ne sont pas activés, la version du système d’exploitation peut être inexacte pour les accès collectés à partir des navigateurs Chromium.

### Caractéristiques d’Audience Manager reposant sur des indices client à forte entropie {#aam}

[!DNL Google] a mis à jour la fonctionnalité de navigateur [!DNL Chrome] afin de minimiser les informations collectées via l&#39;en-tête `User-Agent`. Par conséquent, les clients d’Audience Manager qui utilisent [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=fr) ne recevront plus d’informations fiables sur les caractéristiques basées sur [ clés au niveau de la plateforme ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html).

Les clients d’Audience Manager qui utilisent des clés au niveau de la plateforme pour le ciblage doivent passer à [SDK Web Experience Platform](/help/web-sdk/home.md) au lieu de [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=fr) et activer les [conseils client haute entropie](#enabling-high-entropy-client-hints) pour continuer à recevoir des données de caractéristiques fiables.

## Activation des conseils client à forte entropie {#enabling-high-entropy-client-hints}

Pour activer les conseils client à forte entropie sur votre déploiement de SDK Web, vous devez inclure l’option contextuelle `highEntropyUserAgentHints` supplémentaire dans le champ [`context`](/help/web-sdk/commands/configure/context.md).

Par exemple, pour récupérer des indices client à forte entropie à partir de propriétés web, votre configuration ressemblerait à ceci :

`context: ["highEntropyUserAgentHints", "web"]`

## Exemple {#example}

Les conseils du client contenus dans les en-têtes de la première requête envoyée par le navigateur à un serveur web contiendront la marque du navigateur, la version majeure du navigateur et un indicateur indiquant si le client est un appareil mobile. Chaque donnée possède sa propre valeur d’en-tête plutôt que d’être regroupée en une seule chaîne de l’agent utilisateur, comme illustré ci-dessous :

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

L’en-tête [!DNL User-Agent] équivalent pour le même navigateur ressemblerait à ceci :

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Bien que les informations soient similaires, la première requête au serveur contient des conseils au client. Elles incluent uniquement un sous-ensemble de ce qui est disponible dans la chaîne de l’agent utilisateur. Il manque à la requête l’architecture du système d’exploitation, la version complète du système d’exploitation, le nom du moteur de mise en page, la version du moteur de mise en page et la version complète du navigateur.

Cependant, lors de requêtes ultérieures, le [!DNL Client Hints API] permet aux serveurs web de demander des détails supplémentaires sur l’appareil. Lorsque ces valeurs sont demandées, selon la stratégie du navigateur ou les paramètres utilisateur, la réponse du navigateur peut inclure ces informations.

Vous trouverez ci-dessous un exemple de l’objet JSON renvoyé par [!DNL Client Hints API] lorsque des valeurs à forte entropie sont demandées :


```json
{
   "architecture":"x86",
   "bitness":"64",
   "brands":[
      {
         "brand":" Not A;Brand",
         "version":"99"
      },
      {
         "brand":"Chromium",
         "version":"100"
      },
      {
         "brand":"Google Chrome",
         "version":"100"
      }
   ],
   "fullVersionList":[
      {
         "brand":" Not A;Brand",
         "version":"99.0.0.0"
      },
      {
         "brand":"Chromium",
         "version":"100.0.4896.127"
      },
      {
         "brand":"Google Chrome",
         "version":"100.0.4896.127"
      }
   ],
   "mobile":false,
   "model":"",
   "platformVersion":"12.2.1"
}
```
