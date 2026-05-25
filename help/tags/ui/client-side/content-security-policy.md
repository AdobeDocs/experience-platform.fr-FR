---
title: Prise en charge de la politique de sécurité du contenu (CSP)
description: Découvrez comment gérer les restrictions de la politique de sécurité du contenu (CSP) lors de lʼintégration de votre site web au moyen de balises dans Adobe Experience Platform.
exl-id: 9232961e-bc15-47e1-aa6d-3eb9b865ac23
TQID: https://experienceleague.adobe.com/pIeubuRMJoFa7XJkDscjwflNsOjXc9JjCjlehnmXYtc
product_v2:
  - id: a829a185-511f-4bf8-8dcf-9e684f8011cf
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: dc5cf79d-43c4-4731-bffa-1df5d7549cb1
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: d556b755-390a-43f0-be32-a08cf6236126
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2:
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 1051
ht-degree: 91%

---

# Prise en charge de la politique de sécurité du contenu (CSP)

Une politique de sécurité du contenu (CSP) est une fonctionnalité de sécurité qui aide à prévenir les attaques de type « cross-site scripting » (XSS). Elles se produisent lorsque le navigateur est amené à exécuter du contenu malveillant qui semble provenir dʼune source de confiance, mais qui vient en réalité dʼailleurs. La stratégie de sécurité du contenu permet au navigateur (au nom de l’utilisateur) de vérifier que le script provient bien d’une source de confiance.

Les fichiers CSP sont implémentés en ajoutant un en-tête HTTP `Content-Security-Policy` à vos réponses de serveur ou en ajoutant un élément `<meta>` configuré dans la section `<head>` de vos fichiers HTML.

>[!NOTE]
>
> Pour plus d’informations sur la CSP, consultez la [documentation web MDN](https://developer.mozilla.org/fr/docs/Web/HTTP/CSP).

Dans Adobe Experience Platform, les balises représentent un système de gestion des balises conçu pour charger dynamiquement des scripts sur votre site web. Une CSP par défaut bloque ces scripts chargés dynamiquement en raison de problèmes de sécurité potentiels. Ce document explique comment configurer votre CSP pour autoriser les scripts chargés dynamiquement à partir de balises.

Si vous souhaitez que les balises soient conformes à votre stratégie de sécurité du contenu, deux critères principaux doivent être remplis :

* **La source de votre bibliothèque de balises doit être fiable.** Si cette condition n’est pas remplie, la bibliothèque de balises et les autres fichiers JavaScript requis sont bloqués par le navigateur et ne se chargent pas sur la page.
* **Les scripts intégrés doivent être autorisés.** Si cette condition n’est pas remplie, les actions de règle de code personnalisé sont bloquées sur la page et ne s’exécutent pas correctement.

Une sécurité renforcée exige une quantité de travail plus importante de la part du créateur de contenu. Si vous souhaitez utiliser les balises et avoir une stratégie de sécurité du contenu mise en place, vous devez corriger ces deux problèmes sans que les autres scripts soient considérés comme sûrs par erreur. Le reste du document fournit des conseils sur la façon d’y parvenir.

## Ajouter les balises en tant que source de confiance

Lors de l’utilisation d’une CSP, vous devez inclure tous les domaines de confiance dans la valeur de l’en-tête `Content-Security-Policy`. La valeur que vous devez fournir pour les balises varie en fonction du type dʼhébergement utilisé.

### Auto-hébergement

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

Si vous utilisez un hôte [géré par Adobe](../publishing/hosts/managed-by-adobe-host.md), votre version est conservée sur `assets.adobedtm.com`. Vous devez spécifier `self` comme domaine de sécurité pour ne pas interrompre les scripts qui sont déjà en cours de chargement, mais il est également nécessaire de faire reconnaître `assets.adobedtm.com` comme sûr ou votre bibliothèque de balises ne se chargera pas sur cette page. Dans ce cas, vous devez utiliser la configuration suivante :

**En-tête HTTP**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**Balise `<meta>` HTML**


Il y a une condition préalable très importante : vous devez charger la bibliothèque de balises [de manière asynchrone](./asynchronous-deployment.md). Cela ne fonctionne pas avec un chargement synchrone de la bibliothèque de balises (entraîne des erreurs de console et des règles dont lʼexécution ne se fait pas correctement).

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
>La spécification CSP contient des détails sur une troisième option utilisant des hachages, mais cette approche ne peut pas être utilisée avec des systèmes de gestion des balises tels que des balises. Pour plus d’informations sur les limites d’utilisation des hachages avec les balises dans Experience Platform, consultez le guide [Intégrité des sous-ressources (SRI)](./sri.md).

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

Une fois que vous avez configuré lʼen-tête ou la balise HTML, vous devez indiquer à la balise où trouver la valeur à usage unique lors du chargement dʼun script intégré. Pour quʼune balise utilise la valeur à usage unique lors du chargement du script, vous devez :

1. créer un élément de données qui référence l’emplacement de la valeur à usage unique dans votre couche de données ;
1. configurer l’extension Core et spécifier l’élément de données que vous avez utilisé ;
1. publier les modifications apportées à l’élément de données et à l’extension Core.

>[!NOTE]
>
>Le processus ci-dessus gère uniquement le chargement de votre code personnalisé, et non ce que ce code personnalisé fait. Si un script intégré contient du code personnalisé qui n’est pas conforme à votre CSP, la CSP est prioritaire. Par exemple, si vous utilisez un code personnalisé pour charger un script intégré en lʼajoutant au DOM, la balise ne peut pas ajouter correctement la valeur à usage unique. Ainsi, cette action Custom Code particulière ne fonctionnera pas comme prévu.

### Autoriser tous les scripts intégrés {#unsafe-inline}

Si l’utilisation de la valeur à usage unique ne fonctionne pas pour vous, vous pouvez indiquer à votre CSP d’autoriser tous les scripts intégrés. Il s’agit de l’option la moins sécurisée, mais elle est également plus facile à mettre en œuvre et à gérer.

Les exemples ci-dessous montrent comment autoriser tous les scripts intégrés dans l’en-tête CSP.

#### Auto-hébergement

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

Grâce à ce document, vous devriez comprendre comment configurer votre en-tête CSP pour accepter le fichier de bibliothèque de balises et les scripts intégrés.

À titre de mesure de sécurité supplémentaire, vous pouvez également choisir d’utiliser l’intégrité des sous-ressources (SRI) pour valider les versions de bibliothèque récupérées. Cependant, cette fonctionnalité présente certaines limites majeures lorsquʼelle est utilisée avec des systèmes de gestion des balises tels que des balises. Pour plus d’informations, consultez le guide sur la compatibilité [SRI dans Experience Platform](./sri.md).
