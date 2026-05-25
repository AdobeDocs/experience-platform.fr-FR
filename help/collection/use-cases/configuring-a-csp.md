---
title: Configuration d’un fichier CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Découvrez comment configurer une CSP pour Experience Platform Web SDK
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: configuration;configuration;SDK;edge;Web SDK;configurer;contexte;web;appareil;environnement;paramètres du sdk web;politique de sécurité du contenu;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
TQID: https://experienceleague.adobe.com/KKKsGpKtueETXu07nlNxn6zdRghWlomteunJBAP011c
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 370
ht-degree: 0%

---

# Configuration d’un fichier CSP

Une [&#x200B; Politique de sécurité du contenu &#x200B;](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) est utilisée pour restreindre les ressources qu’un navigateur est autorisé à utiliser. La CSP peut également limiter les fonctionnalités des ressources de script et de style. Adobe Experience Platform Web SDK ne nécessite pas de CSP, mais l’ajout d’un CSP peut réduire la surface d’attaque pour vous protéger contre les attaques malveillantes.

La CSP doit refléter la manière dont [!DNL Experience Platform Web SDK] est déployé et configuré. La CSP suivante indique les modifications qui peuvent être nécessaires au bon fonctionnement du SDK. D’autres paramètres de CSP seront probablement requis en fonction de votre environnement spécifique.

## Exemple de politique de sécurité du contenu

Les exemples suivants montrent comment configurer une CSP.

### Autoriser l’accès au domaine Edge

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

Dans l’exemple ci-dessus, `EDGE-DOMAIN` doit être remplacé par le domaine propriétaire. Le domaine propriétaire est configuré pour le paramètre [edgeDomain](../js/commands/configure/edgedomain.md). Si aucun domaine propriétaire n’a été configuré, `EDGE-DOMAIN` doit être remplacé par `*.adobedc.net`. Si la migration des visiteurs est activée à l’aide de [idMigrationEnabled](../js/commands/configure/idmigrationenabled.md), la directive `connect-src` doit également inclure `*.demdex.net`.

### Utiliser NONCE pour autoriser les éléments de script et de style intégrés

[!DNL Experience Platform Web SDK] pouvez modifier le contenu de la page et doivent être approuvés pour créer des balises de style et de script intégrées. Pour ce faire, Adobe recommande d’utiliser une valeur à usage unique pour la directive CSP [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src). Une valeur à usage unique est un jeton aléatoire généré par le serveur et cryptographiquement puissant, généré une fois par page vue unique.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

En outre, la valeur à usage unique de la CSP doit être ajoutée en tant qu’attribut au SDK Web [code de base](../js/install/base-code.md). Web SDK utilise ensuite cette valeur à usage unique lors de l’ajout de balises de style ou de script intégré à la page :

```html
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Si aucune valeur à usage unique n’est utilisée, l’autre option consiste à ajouter des `unsafe-inline` aux directives `script-src` et `style-src` CSP :

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe ne recommande **pas** de spécifier `unsafe-inline` car cela permet à n’importe quel script de s’exécuter sur la page, ce qui limite les avantages de la CSP.

## Configuration d’un CSP pour la messagerie In-App {#in-app-messaging}

Lorsque vous configurez la messagerie Web In-App, vous devez inclure la directive suivante dans votre CSP :

```
default-src  blob:;
```
