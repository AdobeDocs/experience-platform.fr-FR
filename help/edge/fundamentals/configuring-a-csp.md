---
title: Configuration d’un fichier CSP
seo-title: Configuration d’un fichier CSP pour le SDK Web Adobe Experience Platform
description: Découvrez comment configurer un CSP pour le SDK Web Experience Platform
seo-description: Découvrez comment configurer un CSP pour le SDK Web Experience Platform
keywords: configuration;configuration;SDK;edge;Web SDK;configure;context;web;device;environnement;paramètres web sdk;content security policy;
translation-type: tm+mt
source-git-commit: 4f07d41197add406fbdd82caee5177a1ddaa7d7e
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 2%

---


# Configuration d’un fichier CSP

Une [stratégie de sécurité de contenu](https://developer.mozilla.org/fr/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) est utilisée pour restreindre les ressources qu&#39;un navigateur est autorisé à utiliser. Le CSP peut également limiter la fonctionnalité des ressources de script et de style. Adobe Experience Platform Web SDK n&#39;a pas besoin d&#39;un CSP, mais l&#39;ajout d&#39;un peut réduire la surface d&#39;attaque pour prévenir les attaques malveillantes.

Le CSP doit refléter la façon dont [!DNL Platform Web SDK] est déployé et configuré. Le fichier CSP suivant présente les modifications nécessaires au bon fonctionnement du SDK. D’autres paramètres CSP seront probablement requis, en fonction de votre environnement spécifique.

## Exemple de stratégie de sécurité du contenu

Les exemples suivants montrent comment configurer un fichier CSP.

### Autoriser l&#39;accès au domaine Edge

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

Dans l’exemple ci-dessus, `EDGE-DOMAIN` doit être remplacé par le domaine propriétaire. Le domaine propriétaire est configuré pour le paramètre [edgeDomain](configuring-the-sdk.md#edge-domain). Si aucun domaine propriétaire n&#39;a été configuré, `EDGE-DOMAIN` doit être remplacé par `*.adobedc.net`. Si la migration du visiteur est activée à l&#39;aide de [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled), la directive `connect-src` doit également inclure `*.demdex.net`.

### Utiliser NONCE pour autoriser les éléments de script et de style intégrés

[!DNL Platform Web SDK] peut modifier le contenu de la page et doit être approuvé pour créer des balises de style et de script intégrées. Pour ce faire, l’Adobe recommande d’utiliser un nonce pour la directive CSP [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src). Un nonce est un jeton aléatoire puissant et cryptographiquement généré par le serveur et généré une fois par vue de page unique.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

En outre, le numéro CSP doit être ajouté en tant qu’attribut à la balise de script [!DNL Platform Web SDK] [code de base](installing-the-sdk.md#adding-the-code). [!DNL Platform Web SDK] utilisera ensuite cette valeur nonce lors de l’ajout de balises de script ou de style intégrées à la page :

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Si un nonce n&#39;est pas utilisé, l&#39;autre option consiste à ajouter `unsafe-inline` aux directives CSP `script-src` et `style-src` :

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>L’Adobe ne **pas** recommande de spécifier `unsafe-inline`, car il permet l’exécution d’un script sur la page, ce qui limite les avantages du CSP.
