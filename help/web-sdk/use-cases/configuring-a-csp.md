---
title: Configuration d’une CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Découvrez comment configurer une CSP pour le SDK Web Experience Platform
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: configuration;configuration;SDK;edge;SDK Web;configuration;contexte;web;périphérique;environnement;paramètres du sdk web;stratégie de sécurité du contenu;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 16e49628df73d5ce97ef890dbc0a6f2c8e7de346
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Configuration d’une CSP

Une [stratégie de sécurité du contenu](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) est utilisée pour restreindre les ressources qu’un navigateur est autorisé à utiliser. La CSP peut également limiter les fonctionnalités des ressources de script et de style. Le SDK Web de Adobe Experience Platform ne nécessite pas de stratégie de sécurité du contenu, mais l’ajout d’une solution peut réduire la surface d’attaque afin de prévenir les attaques malveillantes.

La CSP doit refléter la manière dont [!DNL Platform Web SDK] est déployé et configuré. La CSP suivante indique les modifications qui peuvent être nécessaires au bon fonctionnement du SDK. D’autres paramètres CSP seront probablement requis, selon votre environnement spécifique.

## Exemple de stratégie de sécurité du contenu

Les exemples suivants montrent comment configurer une CSP.

### Autoriser l’accès au domaine Edge

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

Dans l’exemple ci-dessus, `EDGE-DOMAIN` doit être remplacé par le domaine propriétaire. Le domaine propriétaire est configuré pour le paramètre [edgeDomain](../commands/configure/edgedomain.md) . Si aucun domaine propriétaire n’a été configuré, `EDGE-DOMAIN` doit être remplacé par `*.adobedc.net`. Si la migration des visiteurs est activée à l’aide de [idMigrationEnabled](../commands/configure/idmigrationenabled.md), la directive `connect-src` doit également inclure `*.demdex.net`.

### Utilisez NONCE pour autoriser les éléments de script et de style intégrés.

[!DNL Platform Web SDK] peut modifier le contenu de la page et doit être approuvé pour créer le script intégré et les balises de style. Pour ce faire, Adobe recommande d’utiliser une valeur à usage unique pour la directive CSP [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src). Une valeur à usage unique est un jeton aléatoire généré par le serveur, de manière cryptographique, et généré une fois par chaque page vue unique.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

En outre, la valeur à usage unique CSP doit être ajoutée en tant qu’attribut à la balise de script [!DNL Platform Web SDK] [code de base](../install/library.md). [!DNL Platform Web SDK] utilisera alors cette valeur à usage unique lors de l’ajout de balises de style ou de script intégrées à la page :

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Si aucune valeur à usage unique n’est utilisée, l’autre option consiste à ajouter `unsafe-inline` aux directives CSP `script-src` et `style-src` :

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe ne recommande **pas** de spécifier `unsafe-inline`, car il permet à n’importe quel script de s’exécuter sur la page, ce qui limite les avantages de la CSP.

## Configuration d’une CSP pour la messagerie in-app {#in-app-messaging}

Lorsque vous configurez la [messagerie in-app web](../personalization/web-in-app-messaging.md), vous devez inclure la directive suivante dans votre CSP :

```
default-src  blob:;
```
