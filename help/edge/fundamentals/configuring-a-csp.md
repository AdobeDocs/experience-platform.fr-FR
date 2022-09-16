---
title: Configuration d’une CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Découvrez comment configurer une CSP pour le SDK Web Experience Platform
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: configuration;configuration;SDK;edge;SDK Web;configuration;contexte;web;périphérique;environnement;paramètres du sdk web;stratégie de sécurité du contenu;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 2%

---

# Configuration d’une CSP

A [Stratégie de sécurité du contenu](https://developer.mozilla.org/fr/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) est utilisé pour restreindre les ressources qu’un navigateur est autorisé à utiliser. La CSP peut également limiter les fonctionnalités des ressources de script et de style. Le SDK Web de Adobe Experience Platform ne nécessite pas de stratégie de sécurité du contenu, mais l’ajout d’une solution peut réduire la surface d’attaque afin de prévenir les attaques malveillantes.

La stratégie de sécurité du contenu doit refléter comment [!DNL Platform Web SDK] est déployé et configuré. La CSP suivante indique les modifications qui peuvent s’avérer nécessaires au bon fonctionnement du SDK. D’autres paramètres CSP seront probablement requis, selon votre environnement spécifique.

## Exemple de stratégie de sécurité du contenu

Les exemples suivants montrent comment configurer une CSP.

### Autoriser l’accès au domaine Edge

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

Dans l’exemple ci-dessus, `EDGE-DOMAIN` doit être remplacé par le domaine propriétaire. Le domaine propriétaire est configuré pour la variable [edgeDomain](configuring-the-sdk.md#edge-domain) . Si aucun domaine propriétaire n’a été configuré, `EDGE-DOMAIN` doit être remplacé par `*.adobedc.net`. Si la migration des visiteurs est activée à l’aide de [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled), la variable `connect-src` La directive doit également inclure `*.demdex.net`.

### Utilisez NONCE pour autoriser les éléments de script et de style intégrés.

[!DNL Platform Web SDK] peut modifier le contenu de la page et doit être approuvé pour créer un script intégré et des balises de style. Pour ce faire, Adobe recommande d’utiliser une valeur à usage unique pour la variable [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) directive CSP. Une valeur à usage unique est un jeton aléatoire généré par le serveur, de manière cryptographique, et généré une fois par chaque page vue unique.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

En outre, la valeur à usage unique CSP doit être ajoutée en tant qu’attribut à la variable [!DNL Platform Web SDK] [code de base](installing-the-sdk.md#adding-the-code) balise de script. [!DNL Platform Web SDK] utilisera alors cette valeur à usage unique lors de l’ajout de balises de style ou de script intégrées à la page :

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Si une valeur à usage unique n’est pas utilisée, l’autre option consiste à ajouter `unsafe-inline` au `script-src` et `style-src` Directives CSP :

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>L’Adobe fait **not** recommandation, spécification `unsafe-inline` car il permet à n’importe quel script de s’exécuter sur la page, ce qui limite les avantages de la CSP.
