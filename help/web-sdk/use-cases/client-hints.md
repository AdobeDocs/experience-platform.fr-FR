---
title: Indications du client de l’agent utilisateur
description: Découvrez comment fonctionnent les indications du client de l’agent utilisateur dans Web SDK. Les indications du client permettent aux propriétaires de site web d’accéder aux mêmes informations que celles disponibles dans la chaîne de l’agent utilisateur, mais d’une manière plus respectueuse de la vie privée.
keywords: user-agent;indications du client; chaîne; chaîne user-agent; faible entropie; entropie élevée
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 4%

---

# Indications du client de l’agent utilisateur

## Vue d’ensemble {#overview}

Chaque fois qu’un navigateur web envoie une requête à un serveur web, l’en-tête de la requête inclut des informations sur le navigateur et l’environnement sur lequel il s’exécute. Toutes ces données sont agrégées dans une chaîne, appelée chaîne de l’agent utilisateur.

Voici un exemple de ce à quoi ressemble une chaîne d’agent utilisateur sur une requête provenant d’un navigateur Chrome s’exécutant sur un appareil [!DNL Mac OS].

>[!NOTE]
>
>Au fil des ans, la quantité d’informations sur le navigateur et l’appareil utilisé incluses dans la chaîne de l’agent utilisateur a augmenté et modifié à plusieurs reprises. L’exemple ci-dessous montre une sélection des informations les plus courantes sur l’agent utilisateur.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| Champ | Valeur |
|---|---|
| Nom du logiciel | Chrome |
| Version du logiciel | 105 |
| Version complète du logiciel | 105.0.0.0 |
| Nom du moteur de mise en page | AppleWebKit |
| Version du moteur de disposition | 537,36 |
| Operating system (Système d’exploitation) | MAC OS X |
| Version du système d’exploitation | 10.15.7 |
| Appareil | Système d’exploitation Intel Mac X 10_15_7 |

## Cas d’utilisation {#use-cases}

Les chaînes d’agent utilisateur ont longtemps été utilisées pour fournir aux équipes de marketing et de développement des informations importantes sur la manière dont les navigateurs, les systèmes d’exploitation et les appareils affichent le contenu du site, ainsi que sur la manière dont les utilisateurs interagissent avec les sites web.

Les chaînes de l’agent utilisateur sont également utilisées pour bloquer le spam et filtrer les robots qui explorent les sites à diverses fins supplémentaires.

## Chaînes de l’agent utilisateur dans Adobe Experience Cloud {#user-agent-in-adobe}

Les solutions Adobe Experience Cloud utilisent les chaînes de l’agent utilisateur de différentes manières.

* Adobe Analytics utilise la chaîne de l’agent utilisateur pour augmenter et extraire des informations supplémentaires relatives aux systèmes d’exploitation, aux navigateurs et aux appareils utilisés pour visiter un site web.
* Adobe Audience Manager et Adobe Target qualifient les utilisateurs finaux pour les campagnes de segmentation et de personnalisation, en fonction des informations fournies par la chaîne de l’agent utilisateur.

## Présentation des indications du client de l’agent utilisateur {#ua-ch}

Ces dernières années, les propriétaires de site et les fournisseurs marketing ont utilisé des chaînes d’agent utilisateur ainsi que d’autres informations incluses dans les en-têtes de requête pour créer des empreintes numériques. Ces empreintes digitales peuvent être utilisées pour identifier des utilisateurs à leur insu.

Malgré l’objectif important que servent les chaînes d’agent utilisateur pour les propriétaires de site, les développeurs de navigateur ont décidé de modifier le fonctionnement des chaînes d’agent utilisateur, afin de limiter les problèmes de confidentialité potentiels pour les utilisateurs finaux.

La solution qu’ils ont développée est appelée [user agent client hints](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Les indications du client permettent toujours aux sites web de collecter les informations nécessaires sur le navigateur, le système d’exploitation et l’appareil utilisé, tout en offrant une protection accrue contre les méthodes de suivi secrètes, telles que l’empreinte numérique.

Les indications du client permettent aux propriétaires de site web d’accéder aux mêmes informations que celles disponibles dans la chaîne de l’agent utilisateur, mais d’une manière plus respectueuse de la vie privée.

Lorsque les navigateurs modernes envoient un utilisateur à un serveur web, l’intégralité de la chaîne de l’agent utilisateur est envoyée à chaque requête, même si elle n’est pas obligatoire. Les indications du client, en revanche, appliquent un modèle dans lequel le serveur doit demander au navigateur les informations supplémentaires qu’il souhaite connaître sur le client. À la réception de cette requête, le navigateur peut appliquer ses propres politiques ou sa propre configuration utilisateur pour déterminer les données renvoyées. Au lieu d’exposer l’intégralité de la chaîne de l’agent utilisateur par défaut sur toutes les requêtes, l’accès est désormais géré de manière explicite et auditable.

## Prise en charge des navigateurs {#browser-support}

[User agent client hints](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) ont été introduits avec la version 89 de [!DNL Google Chrome].

D’autres navigateurs basés sur Chromium prennent en charge l’API Client Hints, tels que :

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Catégories {#categories}

Il existe deux catégories d’indications du client de l’agent utilisateur :

* [Indications du client à faible entropie](#low-entropy)
* [Indications du client à entropie élevée](#high-entropy)

### Indications du client à faible entropie {#low-entropy}

Les indications du client à faible entropie incluent des informations de base qui ne peuvent pas être utilisées pour relever les empreintes des utilisateurs. Informations telles que la marque du navigateur, la plateforme et si la requête provient d’un appareil mobile.

Les indications du client à faible entropie sont activées par défaut dans Web SDK et sont transmises à chaque requête.

| En-tête HTTP | JavaScript | Inclus dans User-Agent par défaut | Inclus dans les indications du client par défaut |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | Oui | Oui |
| `Sec-CH-UA-Platform` | `platform` | Oui | Oui |
| `Sec-CH-UA-Mobile` | `mobile` | Oui | Oui |

### Indications du client à entropie élevée {#high-entropy}

Les indications du client à entropie élevée sont des informations plus détaillées sur l’appareil client, telles que la version de la plateforme, l’architecture, le modèle, le débit (plateformes 64 ou 32 bits) ou la version complète du système d’exploitation. Ces informations pourraient éventuellement être utilisées pour les empreintes digitales.

| Propriété | Description | En-tête HTTP | Chemin XDM | Exemple | Inclus dans l’agent utilisateur par défaut | Inclus dans les indications du client par défaut |
| --- | --- | --- | --- | --- |---|---|
| Version du système d’exploitation | Version du système d’exploitation. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` | Oui | Non |
| Architecture | Architecture CPU sous-jacente. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` | Oui | Non |
| Modèle d’appareil | Nom de l’appareil utilisé. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` | Oui | Non |
| Bitness | Nombre de bits pris en charge par l’architecture CPU sous-jacente. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` | Oui | Non |
| Fournisseur du navigateur | Société qui a créé le navigateur. L’indice à faible entropie `Sec-CH-UA` collecte également cet élément. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` | Oui | Non |
| Nom du navigateur | Le navigateur utilisé. L’indice à faible entropie `Sec-CH-UA` collecte également cet élément. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` | Oui | Non |
| Version du navigateur | Version significative du navigateur. L’indice à faible entropie `Sec-CH-UA` collecte également cet élément. La version exacte du navigateur n’est pas collectée automatiquement. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` | Oui | Non |


Les indications du client à entropie élevée sont désactivées par défaut dans Web SDK. Pour les activer, vous devez configurer manuellement le SDK Web pour demander des indications du client à entropie élevée.

## Impact des indications du client à entropie élevée sur les solutions Experience Cloud {#impact-in-experience-cloud-solutions}

Certaines solutions Adobe Experience Cloud reposent sur des informations incluses dans les indications du client à entropie élevée lors de la génération de rapports.

Si vous n’activez pas les indications du client à entropie élevée dans votre environnement, les rapports et caractéristiques Adobe Analytics et Audience Manager décrits ci-dessous ne fonctionneront pas.

### Rapports Adobe Analytics reposant sur des indications du client à entropie élevée {#analytics}

La dimension [ Système d’exploitation ](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html?lang=fr) inclut la version du système d’exploitation stockée en tant qu’indicateur client à entropie élevée. Si les indications des clients à entropie élevée ne sont pas activées, la version du système d’exploitation peut être inexacte pour les accès collectés à partir des navigateurs Chromium.

### Caractéristiques d’Audience Manager reposant sur des indications du client à entropie élevée {#aam}

[!DNL Google] a mis à jour la fonctionnalité du navigateur [!DNL Chrome] afin de minimiser les informations collectées via l’en-tête `User-Agent`. Par conséquent, les clients Audience Manager utilisant [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=fr) ne recevront plus d’informations fiables pour les caractéristiques basées sur [clés au niveau de la plateforme](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html?lang=fr).

Les clients Audience Manager qui utilisent des clés au niveau de la plateforme pour le ciblage doivent passer à [Experience Platform Web SDK](/help/web-sdk/home.md) au lieu de [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=fr) et permettre à [High Entropy Client Hints](#enabling-high-entropy-client-hints) de continuer à recevoir des données de caractéristiques fiables.

## Activation des indications du client à entropie élevée {#enabling-high-entropy-client-hints}

Pour activer les indications du client à entropie élevée dans votre déploiement de Web SDK, vous devez inclure l’option de contexte de `highEntropyUserAgentHints` supplémentaire dans le champ [`context`](/help/web-sdk/commands/configure/context.md) .

Par exemple, pour récupérer des indications du client à entropie élevée à partir de propriétés web, votre configuration ressemblerait à ceci :

`context: ["highEntropyUserAgentHints", "web"]`

## Exemple {#example}

Les indications du client contenues dans les en-têtes de la première requête envoyée par le navigateur à un serveur web contiennent la marque du navigateur, la version majeure du navigateur et un indicateur indiquant si le client est un appareil mobile. Chaque élément de données aura sa propre valeur d’en-tête plutôt que d’être regroupé en une seule chaîne d’agent utilisateur, comme illustré ci-dessous :

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

L’en-tête [!DNL User-Agent] équivalent pour le même navigateur serait le suivant :

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Bien que les informations soient similaires, la première requête au serveur contient des indications du client. Ils incluent uniquement un sous-ensemble de ce qui est disponible dans la chaîne de l’agent utilisateur. La requête ne contient pas l’architecture du système d’exploitation, la version complète du système d’exploitation, le nom du moteur de rendu, la version du moteur de rendu et la version complète du navigateur.

Toutefois, lors des requêtes ultérieures, le [!DNL Client Hints API] permet aux serveurs web de demander des détails supplémentaires sur l’appareil. Lorsque ces valeurs sont demandées, en fonction de la politique du navigateur ou des paramètres utilisateur, la réponse du navigateur peut inclure ces informations.

Vous trouverez ci-dessous un exemple de l’objet JSON renvoyé par le [!DNL Client Hints API] lorsque des valeurs à entropie élevée sont demandées :


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
