---
title: Configuration d’un fichier CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Découvrez comment configurer une CSP pour Experience Platform Web SDK
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: configuration;configuration;SDK;edge;Web SDK;configurer;contexte;web;appareil;environnement;paramètres du sdk web;politique de sécurité du contenu;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Configuration d’un fichier CSP

Une [ Politique de sécurité du contenu ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) est utilisée pour restreindre les ressources qu’un navigateur est autorisé à utiliser. La CSP peut également limiter les fonctionnalités des ressources de script et de style. Adobe Experience Platform Web SDK ne nécessite pas de CSP, mais l’ajout d’un CSP peut réduire la surface d’attaque pour vous protéger contre les attaques malveillantes.

La CSP doit refléter la manière dont [!DNL Experience Platform Web SDK] est déployé et configuré. La CSP suivante indique les modifications qui peuvent être nécessaires au bon fonctionnement du SDK. D’autres paramètres de CSP seront probablement requis en fonction de votre environnement spécifique.

## Exemple de politique de sécurité du contenu

Les exemples suivants montrent comment configurer une CSP.

### Autoriser l’accès au domaine Edge

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

Dans l’exemple ci-dessus, `EDGE-DOMAIN` doit être remplacé par le domaine propriétaire. Le domaine propriétaire est configuré pour le paramètre [edgeDomain](../commands/configure/edgedomain.md). Si aucun domaine propriétaire n’a été configuré, `EDGE-DOMAIN` doit être remplacé par `*.adobedc.net`. Si la migration des visiteurs est activée à l’aide de [idMigrationEnabled](../commands/configure/idmigrationenabled.md), la directive `connect-src` doit également inclure `*.demdex.net`.

### Utiliser NONCE pour autoriser les éléments de script et de style intégrés

[!DNL Experience Platform Web SDK] pouvez modifier le contenu de la page et doivent être approuvés pour créer des balises de style et de script intégrées. Pour ce faire, Adobe recommande d’utiliser une valeur à usage unique pour la directive CSP [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src). Une valeur à usage unique est un jeton aléatoire généré par le serveur et cryptographiquement puissant, généré une fois par page vue unique.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

En outre, la valeur à usage unique de la CSP doit être ajoutée en tant qu’attribut à la balise de script [!DNL Experience Platform Web SDK] [code de base](../install/library.md). [!DNL Experience Platform Web SDK] utilisera ensuite cette valeur à usage unique lors de l’ajout de balises de script ou de style intégrées à la page :

```
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

Lorsque vous configurez la [messagerie Web In-App](../personalization/web-in-app-messaging.md), vous devez inclure la directive suivante dans votre CSP :

```
default-src  blob:;
```
