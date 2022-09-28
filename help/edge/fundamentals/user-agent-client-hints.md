---
title: Conseils sur le client User-Agent
description: Découvrez le fonctionnement des conseils client User-Agent dans le SDK Web
keywords: user-agent;conseils client; string; chaîne de l’agent-utilisateur ; faible entropie; entropie élevée
source-git-commit: 6c974d1a646ff1f3a8f7ad9d67a6840391fc739e
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 7%

---


# Conseils sur le client User-Agent

## Présentation {#overview}

Chaque fois qu’un navigateur Web envoie une requête à un serveur Web, l’en-tête de la requête inclut des informations sur le navigateur et l’environnement sur lequel le navigateur est exécuté. Toutes ces données sont agrégées dans une chaîne appelée [!DNL User-Agent] chaîne.

Voici un exemple de ce qu’une [!DNL User-Agent] ressemble à une chaîne sur une requête provenant d’un navigateur Chrome exécuté sur un [!DNL Mac OS] appareil.

>[!NOTE]
>
>Au fil des ans, la quantité d’informations de navigateur et de périphérique incluses dans la variable [!DNL User-Agent] chaîne a été développée et modifiée plusieurs fois. L’exemple ci-dessous présente une sélection des [!DNL User-Agent] informations.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| Champ | Valeur |
|---|---|
| Nom du logiciel | Chrome |
| Version du logiciel | 105 |
| Version complète du logiciel | 105.0.0.0 |
| Nom du moteur de rendu | AppleWebKit |
| Version du moteur de rendu | 537.36 |
| Operating system (Système d’exploitation) | Mac OS X |
| Version du système d’exploitation | 10.15.7 |
| Appareil | Intel Mac OS X 10_15_7 |

## Cas d&#39;utilisation {#use-cases}

[!DNL User-Agent] Les chaînes ont longtemps été utilisées pour fournir aux équipes de marketing et de développement des informations importantes sur la manière dont les navigateurs, les systèmes d’exploitation et les périphériques affichent le contenu du site, ainsi que sur la manière dont les utilisateurs interagissent avec les sites web.

[!DNL User-Agent] les chaînes sont également utilisées pour bloquer les spams et filtrer les robots qui analysent les sites à diverses fins supplémentaires.

## [!DNL User-Agent] chaînes dans Adobe Experience Cloud {#user-agent-in-adobe}

Les solutions Adobe Experience Cloud utilisent la variable [!DNL User-Agent] chaînes de différentes manières.

* Adobe Analytics utilise la variable [!DNL User-Agent] pour augmenter et obtenir des informations supplémentaires sur les systèmes d’exploitation, les navigateurs et les périphériques utilisés pour consulter un site web.
* Adobe Audience Manager et Adobe Target permettent aux utilisateurs finaux de réaliser des campagnes de segmentation et de personnalisation sur la base des informations fournies par le [!DNL User-Agent] chaîne.

## Présentation des conseils client User-Agent {#ua-ch}

Au cours des dernières années, les propriétaires de site et les fournisseurs marketing ont utilisé [!DNL User-Agent] chaînes ainsi que d’autres informations incluses dans les en-têtes de requête pour créer des empreintes digitales. Ces empreintes digitales peuvent être utilisées pour identifier les utilisateurs à leur insu.

Malgré l&#39;objectif important, [!DNL User-Agent] les chaînes sont destinées aux propriétaires de site. Les développeurs de navigateur ont décidé de modifier la manière dont ils gèrent les [!DNL User-Agent] les chaînes fonctionnent afin de limiter les problèmes potentiels de confidentialité pour les utilisateurs finaux.

La solution qu&#39;ils ont développée s&#39;appelle [Conseils sur le client User-Agent](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Les conseils aux clients permettent toujours aux sites web de collecter les informations nécessaires sur les navigateurs, les systèmes d’exploitation et les appareils, tout en offrant une protection accrue contre les méthodes de suivi secrètes, telles que l’empreinte digitale.

Les conseils aux clients permettent aux propriétaires de sites web d’accéder à une grande partie des mêmes informations disponibles dans la variable [!DNL User-Agent] mais d’une manière plus respectueuse de la vie privée.

Lorsque les navigateurs modernes envoient un utilisateur vers un serveur web, l’ensemble des [!DNL User-Agent] est envoyée à chaque demande, qu’elle soit requise ou non. Les conseils du client, en revanche, imposent un modèle dans lequel le serveur doit demander au navigateur les informations supplémentaires qu’il souhaite connaître sur le client. Lors de la réception de cette requête, le navigateur peut appliquer ses propres stratégies ou sa propre configuration utilisateur pour déterminer les données renvoyées. Au lieu d’exposer l’ensemble [!DNL User-Agent] pour toutes les requêtes, l’accès est désormais géré de manière explicite et auditable.

## Prise en charge des navigateurs {#browser-support}

[Conseils sur le client User-Agent](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) ont été introduits avec [!DNL Google Chrome ]version 89.

D’autres navigateurs Chromium prennent en charge l’API Client Hints, tels que :

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Catégories {#categories}

Il existe deux catégories d’indicateurs client User-Agent :

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

| En-tête HTTP | JavaScript | Inclus par défaut dans User-Agent | Inclus dans les conseils client par défaut |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | Oui | Non |
| `Sec-CH-UA-Arc` | `architecture` | Oui | Non |
| `Sec-CH-UA-Model` | `model` | Oui | Non |
| `Sec-CH-UA-Bitness` | `Bitness` | Oui | Non |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | Oui | Non |

Les indices client à forte entropie sont désactivés par défaut dans le SDK Web. Pour les activer, vous devez configurer manuellement le SDK Web afin de demander des conseils client à forte entropie.

## Impact des indices client à forte entropie sur les solutions Experience Cloud {#impact-in-experience-cloud-solutions}

Certaines solutions Adobe Experience Cloud reposent sur des informations incluses dans les conseils client à forte entropie lors de la génération de rapports.

Si vous n’activez pas les indicateurs client à forte entropie dans votre environnement, les caractéristiques et rapports Adobe Analytics et d’Audience Manager décrits ci-dessous ne fonctionneront pas.

### Rapports Adobe Analytics reposant sur des indices client à forte entropie {#analytics}

Les rapports Adobe Analytics suivants ne fonctionneront pas lorsque les indices client à forte entropie sont désactivés.

* [Browser](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser.html) (Navigateur)
* [Type de navigateur](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html)
* [Operating system (Système d’exploitation)](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html)
* [Types de systèmes d’exploitation](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html)
* [Dimensions mobiles](https://experienceleague.adobe.com/docs/analytics/components/dimensions/mobile-dimensions.html)

### Caractéristiques d’Audience Manager reposant sur des indices client à forte entropie {#aam}

Si vos caractéristiques d’Audience Manager utilisent l’une des propriétés suivantes, vous devez activer les conseils client à forte entropie. Sinon, les caractéristiques cesseront de fonctionner.

* Version du système d’exploitation
* Modèle de périphérique
* Fabricant de l’appareil
* Fournisseur du périphérique

## Activation des conseils client à forte entropie {#enabling-high-entropy-client-hints}

Pour activer les conseils client à forte entropie sur votre déploiement du SDK Web, vous devez inclure des `highEntropyUserAgentHints` l’option de contexte, comme décrit dans la section [documentation de configuration](configuring-the-sdk.md#context), avec votre configuration existante.

Par exemple, pour récupérer des indices client à forte entropie à partir de propriétés web, votre configuration ressemblerait à ceci :

`context: ["highEntropyUserAgentHints", "web"]`

## Exemple {#example}

Les conseils du client contenus dans les en-têtes de la première requête envoyée par le navigateur à un serveur web contiendront la marque du navigateur, la version majeure du navigateur et un indicateur indiquant si le client est un appareil mobile. Chaque élément de données aura sa propre valeur d’en-tête plutôt que d’être regroupé en un seul [!DNL User-Agent] , comme illustré ci-dessous :

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

L’équivalent [!DNL User-Agent] pour le même navigateur ressemblerait à ceci :

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Bien que les informations soient similaires, la première requête au serveur contient des conseils au client. Ils incluent uniquement un sous-ensemble de ce qui est disponible dans la variable [!DNL User-Agent] chaîne. Il manque à la requête l’architecture du système d’exploitation, la version complète du système d’exploitation, le nom du moteur de mise en page, la version du moteur de mise en page et la version complète du navigateur.

Toutefois, lors des requêtes suivantes, la variable [!DNL Client Hints API] permet aux serveurs web de demander des détails supplémentaires sur l’appareil. Lorsque ces valeurs sont demandées, selon la stratégie du navigateur ou les paramètres utilisateur, la réponse du navigateur peut inclure ces informations.

Vous trouverez ci-dessous un exemple de l’objet JSON renvoyé par la fonction [!DNL Client Hints API] lorsque des valeurs à forte entropie sont demandées :


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
