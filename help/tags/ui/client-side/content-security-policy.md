---
title: Prise en charge de la stratégie de sécurité du contenu (CSP)
description: Découvrez comment gérer les restrictions de la stratégie de sécurité du contenu (CSP) lors de l’intégration de votre site web aux balises dans Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 59%

---

# Prise en charge de la stratégie de sécurité du contenu (CSP)

>[!NOTE]
>
>Adobe Experience Platform Launch devient une suite de technologies destinées à la collecte de données dans Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Une stratégie de sécurité du contenu (CSP) est une fonctionnalité de sécurité qui aide à prévenir les attaques de type « cross-site scripting » (XSS). Cela se produit lorsque le navigateur est amené à exécuter du contenu malveillant qui semble provenir d’une source de confiance, mais qui vient réellement d’ailleurs. La stratégie de sécurité du contenu permet au navigateur (au nom de l’utilisateur) de vérifier que le script provient bien d’une source de confiance.

Les fichiers CSP sont implémentés en ajoutant un en-tête HTTP `Content-Security-Policy` à vos réponses de serveur ou en ajoutant un élément `<meta>` configuré dans la section `<head>` de vos fichiers HTML.

>[!NOTE]
>
> Pour plus d’informations sur la CSP, consultez la [documentation web MDN](https://developer.mozilla.org/fr/docs/Web/HTTP/CSP).

Dans Adobe Experience Platform, les balises sont un système de gestion des balises conçu pour charger dynamiquement les scripts sur votre site web. Une CSP par défaut bloque ces scripts chargés dynamiquement en raison de problèmes de sécurité potentiels. Ce document explique comment configurer votre CSP pour autoriser les scripts chargés dynamiquement à partir de balises.

Si vous souhaitez que les balises fonctionnent avec votre stratégie de sécurité du contenu, deux problèmes principaux doivent être résolus :

* **La source de votre bibliothèque de balises doit être fiable.** Si cette condition n’est pas remplie, la bibliothèque de balises et les autres fichiers JavaScript requis sont bloqués par le navigateur et ne se chargent pas sur la page.
* **Les scripts intégrés doivent être autorisés.** Si cette condition n’est pas remplie, les actions des règles Custom Code (Code personnalisé) sont bloquées sur la page et ne s’exécuteront pas correctement.

Une sécurité renforcée nécessite un travail accru de la part du créateur de contenu. Si vous souhaitez utiliser des balises et avoir une stratégie de sécurité du contenu mise en place, vous devez résoudre ces deux problèmes sans que les autres scripts soient considérés comme sûrs par erreur. Le reste du document fournit des conseils sur la façon d’y parvenir.

## Ajout de balises en tant que source approuvée

Lors de l’utilisation d’une CSP, vous devez inclure tous les domaines de confiance dans la valeur de l’en-tête `Content-Security-Policy`. La valeur que vous devez fournir pour les balises varie en fonction du type d’hébergement utilisé.

### Autohébergement

Si vous [autohébergez](../publishing/hosts/self-hosting-libraries.md) votre bibliothèque, alors la source de votre bibliothèque est probablement votre propre domaine. Vous pouvez spécifier que le domaine hôte est une source sûre en utilisant la configuration suivante :

**En-tête HTTP**

```http
Content-Security-Policy: script-src 'self'
```

**Balise `<meta>` HTML**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self'">
```

### Hébergement géré par Adobe

Si vous utilisez un hôte [géré par Adobe](../publishing/hosts/managed-by-adobe-host.md), votre version est conservée sur `assets.adobedtm.com`. Vous devez spécifier `self` comme domaine de sécurité afin de ne pas interrompre les scripts qui sont déjà en cours de chargement, mais vous avez également besoin de `assets.adobedtm.com` pour être répertorié comme sûr ou votre bibliothèque de balises ne se chargera pas sur la page. Dans ce cas, vous devez utiliser la configuration suivante :

**En-tête HTTP**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**Balise `<meta>` HTML**


Il y a une condition préalable très importante : Vous devez charger la bibliothèque de balises [de manière asynchrone](https://experienceleague.adobe.com/docs/launch/using/reference/client-side-info/asynchronous-deployment.html?lang=fr). Cela ne fonctionne pas avec un chargement synchrone de la bibliothèque de balises (ce qui entraîne des erreurs de console et des règles qui ne s’exécutent pas correctement).

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com">
```

Vous devez spécifier `self` comme domaine sûr pour ne pas interrompre les scripts qui sont déjà en cours de chargement, mais il est également nécessaire de faire reconnaître `assets.adobedtm.com` comme sûr ou votre version de bibliothèque ne se chargera pas sur cette page.

## Scripts intégrés

Par défaut, la CSP désactive les scripts intégrés et doit donc être configurée manuellement pour qu’ils soient autorisés. Vous disposez de deux options pour autoriser les scripts intégrés :

* [Autoriser par valeur à usage unique](#nonce) (bon niveau de sécurité)
* [Autoriser tous les scripts intégrés](#unsafe-inline) (la moins sûre)

>[!NOTE]
>
>La spécification CSP contient des détails sur une troisième option utilisant des hachages, mais cette approche ne peut pas être utilisée avec des systèmes de gestion des balises tels que les balises. Pour plus d’informations sur les limites d’utilisation des hachages avec des balises dans Platform, consultez le [guide Intégrité des sous-ressources (SRI)](./sri.md).

### Autoriser par valeur à usage unique {#nonce}

Cette méthode implique de générer une valeur à usage unique cryptographique et de l’ajouter à votre CSP et à chaque script intégré sur votre site. Lorsque le navigateur reçoit une instruction de chargement d’un script intégré avec une valeur à usage unique dessus, il compare celle-ci à ce qui est contenu dans l’en-tête de la CSP. Si cela concorde, le script est chargé. Cette valeur à usage unique doit être modifiée à chaque nouveau chargement de page.

>[!IMPORTANT]
>
>Pour utiliser cette méthode, vous devez charger la version de manière asynchrone. Cela ne fonctionne pas lors du chargement synchrone de la version, ce qui entraîne des erreurs de console et des règles qui ne s’exécutent pas correctement. Pour plus d’informations, consultez le guide sur le [déploiement asynchrone](./asynchronous-deployment.md).

Les exemples ci-dessous montrent comment ajouter votre valeur à usage unique à la configuration CSP pour un hôte géré par Adobe. Si vous utilisez l’autohébergement, vous pouvez exclure `assets.adobedtm.com`.

**En-tête HTTP**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'
```

**Balise `<meta>` HTML**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'">
```

Une fois que vous avez configuré l’en-tête ou la balise HTML, vous devez indiquer à la balise où trouver la valeur à usage unique lors du chargement d’un script intégré. Pour qu’une balise utilise la valeur à usage unique lors du chargement du script, vous devez :

1. créer un élément de données qui référence l’emplacement de la valeur à usage unique dans votre couche de données ;
1. configurer l’extension Core et spécifier l’élément de données que vous avez utilisé ;
1. publier les modifications apportées à l’élément de données et à l’extension Core.

>[!NOTE]
>
>Le processus ci-dessus gère uniquement le chargement de votre code personnalisé, et non ce que ce code personnalisé fait. Si un script intégré contient du code personnalisé qui n’est pas conforme à votre CSP, la CSP est prioritaire. Par exemple, si vous utilisez du code personnalisé pour charger un script intégré en l’ajoutant au modèle DOM, la balise ne peut pas ajouter correctement la valeur à usage unique. Par conséquent, cette action Custom Code particulière ne fonctionnera pas comme prévu.

### Autoriser tous les scripts intégrés {#unsafe-inline}

Si l’utilisation de la valeur à usage unique ne fonctionne pas pour vous, vous pouvez indiquer à votre CSP d’autoriser tous les scripts intégrés. Il s’agit de l’option la moins sécurisée, mais elle est également plus facile à mettre en œuvre et à gérer.

Les exemples ci-dessous montrent comment autoriser tous les scripts intégrés dans l’en-tête CSP.

#### Autohébergement

Utilisez les configurations suivantes si vous utilisez l’autohébergement :

**En-tête HTTP**

```http
Content-Security-Policy: script-src 'self' 'unsafe-inline'
```

**Balise `<meta>` HTML**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-inline'">
```

#### Hébergement géré par Adobe

Utilisez les configurations suivantes si vous utilisez l’hébergement géré par Adobe :

**En-tête HTTP**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'unsafe-inline'
```

**Balise `<meta>` HTML**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'unsafe-inline'">
```

## Étapes suivantes

En lisant ce document, vous devez maintenant comprendre comment configurer votre en-tête CSP pour accepter le fichier de bibliothèque de balises et les scripts intégrés.

À titre de mesure de sécurité supplémentaire, vous pouvez également choisir d’utiliser l’intégrité des sous-ressources (SRI) pour valider les versions de bibliothèque récupérées. Cependant, cette fonctionnalité présente certaines limites majeures lorsqu’elle est utilisée avec des systèmes de gestion des balises tels que les balises. Pour plus d’informations, consultez le guide sur la [compatibilité SRI dans Platform](./sri.md) .
