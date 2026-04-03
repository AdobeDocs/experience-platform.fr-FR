---
title: Utiliser des identifiants d’appareil propriétaires dans la collecte de données
description: Configurez des identifiants d’appareil propriétaires (FPID) pour une identité durable dans les implémentations web qui envoient des données à Edge Network.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 0%

---

# Utiliser des identifiants d’appareil propriétaires dans la collecte de données

Experience Platform Edge Network utilise des Experience Cloud ID (ECID) pour identifier les visiteurs et visiteuses du site web. Pour améliorer la durabilité des identités sur les propriétés qui vous appartiennent, vous pouvez définir et gérer vos propres identifiants d’appareil, appelés identifiants d’appareil propriétaires (FPID). Edge Network utilise le FPID pour amorcer l’ECID utilisé par les solutions Adobe.

Cette page suppose que vous connaissez les ECID et les `identityMap`. Voir [Identité dans la collecte de données](./overview.md) pour plus d’informations.

## Quand utiliser les FPID {#when-to-use}

Les restrictions de navigateur peuvent raccourcir la durée de vie des cookies qu’Adobe utilise pour reconnaître les visiteurs récurrents. Si vous avez besoin d’une identité plus durable sur les sites détenus et contrôlés par votre organisation, les FPID vous permettent de gérer votre propre identifiant d’appareil et de l’utiliser pour amorcer l’ECID.

Les FPID sont pris en charge pour les implémentations web qui utilisent Web SDK, y compris l’extension de balise Web SDK. Elles sont idéales si votre objectif principal est une persistance de l’identité plus forte sur les domaines détenus par votre organisation ou si vous souhaitez une meilleure continuité pour les rapports et la personnalisation sur les propriétés web détenues. Ils vous permettent également de définir et de gérer un cookie propriétaire à partir de l’infrastructure que vous contrôlez.

Les FPID ne sont pas l’outil approprié lorsque votre objectif principal est la remise d’application à un site web ou la continuité d’identité sur plusieurs domaines. Pour ces scénarios, consultez les sections [partage d’identités mobile vers web](./mobile-to-web.md) et [partage inter-domaines](./cross-domain-sharing.md).

Les avantages de l’utilisation des FPID sont les suivants :

* Persistance plus forte sur les propriétés détenues.
* Contrôle accru de la génération et de la gestion de l’identifiant de l’appareil.
* Une base durable pour l’analyse et la personnalisation.

Les compromis à l’utilisation des FPID incluent :

* Responsabilité de mise en œuvre plus importante que celle liée au comportement d’identité par défaut.
* Coordination entre la logique des cookies côté serveur et la configuration de la collecte de données.
* Une validation supplémentaire pour confirmer que l’identifiant est utilisé comme prévu.

### Chemin de configuration de haut niveau

1. Générez et gérez un identifiant d’appareil propriétaire sur l’infrastructure que vous contrôlez.
1. Configurez votre implémentation pour lire cet identifiant à partir d’un [cookie propriétaire](#setting-cookie-datastreams) ou de la [payload d’identité](#identityMap).
1. Vérifiez que les visiteurs récurrents conservent une identité cohérente au fil du temps sur vos propres propriétés.

## Fonctionnement des FPID {#how-fpids-work}

Le FPID transmis à Adobe Experience Cloud est converti en ECID à l’aide d’un algorithme déterministe. Chaque fois que le même FPID est envoyé à Edge Network, le même ECID est prédéfini à partir du FPID. Une fois que le FPID a été utilisé pour initialiser un ECID, il est supprimé du `identityMap` et remplacé par l’ECID généré. Le FPID n’est pas stocké dans les solutions Adobe Experience Platform ou Experience Cloud.

Lorsqu’il existe à la fois un ECID et un FPID, l’ECID est toujours utilisé pour identifier l’utilisateur en premier. Cette hiérarchisation garantit que lorsqu’un ECID existant est présent dans la boutique de cookies de navigateur, il reste l’identifiant principal et que le nombre de visiteurs existants ne risque pas d’inflation. Pour les utilisateurs existants, le FPID ne devient pas l’identité principale tant que l’ECID n’expire pas ou n’est pas supprimé en raison d’une politique de navigateur ou d’une action manuelle.

Les identités sont hiérarchisées dans l’ordre suivant :

1. ECID inclus dans le `identityMap`
1. ECID stocké dans un cookie
1. FPID inclus dans le `identityMap`
1. FPID stocké dans un cookie

## Générer et définir le cookie FPID {#set-fpid-cookie}

Edge Network accepte uniquement les identifiants conformes au format [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Les identifiants d’appareil qui ne sont pas au format UUIDv4 sont rejetés.

* Les UUID sont uniques et aléatoires, avec une probabilité de collision négligeable.
* UUIDv4 ne peut pas être prédéfini à l&#39;aide d&#39;adresses IP ou de toute autre information d&#39;identification personnelle (PII).
* Des bibliothèques pour générer des UUID sont disponibles pour chaque langage de programmation.

### Paramètre des cookies côté serveur {#set-cookie-server}

Lors de la définition d’un cookie sur votre propre serveur , vous pouvez utiliser différentes méthodes pour empêcher que le cookie ne soit limité par des politiques de navigateur :

* Génération de cookies à l’aide de langages de script côté serveur
* Définissez des cookies en réponse à une requête d’API envoyée à un sous-domaine ou à un autre point d’entrée du site
* Générer des cookies à l’aide d’un système de gestion de contenu (CMS)
* Générer des cookies à l’aide d’un réseau de diffusion de contenu (CDN)

Les cookies propriétaires sont plus efficaces lorsqu’ils sont définis à l’aide d’un serveur qui utilise un enregistrement DNS [A](https://datatracker.ietf.org/doc/html/rfc1035) (pour IPv4) ou [enregistrement AAAA](https://datatracker.ietf.org/doc/html/rfc3596) (pour IPv6), par opposition à un `CNAME` DNS ou un code JavaScript.

>[!IMPORTANT]
>
>Les cookies définis à l’aide de la méthode de `document.cookie` JavaScript (y compris à l’aide de la méthode de balise [`cookie.set()`](../tags/cookie.md)) ne sont presque jamais protégés des politiques de navigateur qui limitent la durée des cookies.

Notez que les enregistrements `A` ou `AAAA` ne sont pris en charge que pour la définition et le suivi des cookies. La principale méthode de collecte de données consiste à utiliser un `CNAME` DNS. Les FPID sont définis à l’aide d’un enregistrement `A` ou `AAAA` et envoyés à Adobe à l’aide d’un `CNAME` . Le [Programme de certificat géré par &#x200B;](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) vous permet de configurer un `CNAME` pour la collecte de données.

### Quand définir le cookie {#when-to-set-cookie}

Le cookie FPID est idéalement défini avant l’envoi de données à Edge Network. Si votre implémentation nécessite un consentement avant la collecte des données, consultez [Consentement avec les identifiants d’appareil propriétaires](./consent.md#consent-with-fpids) pour obtenir des conseils sur la coordination du cookie FPID avec votre flux de consentement. Le gonflement des visiteurs est réduit lorsque vous vous assurez que le FPID est disponible pour amorcer l’ECID à partir de la première requête. Dans les cas où cela n’est pas possible, un ECID est toujours généré à l’aide des méthodes existantes et agit comme identifiant principal tant que le cookie existe. Le FPID généré ne devient pas l’identifiant principal tant que l’ECID n’est pas présent. En supposant que l’ECID soit finalement affecté par une politique de suppression du navigateur, mais que le FPID ne l’est pas, le FPID devient l’identifiant principal lors de la visite suivante et est utilisé pour amorcer l’ECID à chaque visite suivante.

### Définir l’expiration {#set-expiration}

Adobe recommande d’étudier soigneusement la durée de vie de votre cookie FPID. Assurez-vous de tenir compte de la politique de confidentialité de votre organisation ainsi que des lois et politiques des pays ou régions dans lesquels votre organisation opère. Selon la configuration de votre entreprise, vous pouvez adopter une politique de définition des cookies à l’échelle de l’entreprise ou une politique qui varie pour les utilisateurs dans chaque paramètre régional où vous intervenez. Quelle que soit l’expiration initiale des cookies, veillez à inclure une logique qui étend l’expiration à chaque nouvelle visite du site.

### Indicateurs de cookie {#cookie-flags}

Plusieurs indicateurs de cookie affectent la manière dont les cookies sont traités dans les différents navigateurs :

* **`HTTPOnly`** : les cookies définis à l’aide de l’indicateur `HTTPOnly` ne sont pas accessibles à l’aide de scripts côté client. Cela signifie que si vous définissez un indicateur de `HTTPOnly` lors de la définition du FPID, vous devez utiliser un langage de script côté serveur pour lire la valeur du cookie à inclure dans le `identityMap`. Si vous choisissez qu’Edge Network lise la valeur du cookie FPID, la définition de l’indicateur `HTTPOnly` garantit que la valeur n’est pas accessible par les scripts côté client, mais n’a pas d’incidence négative sur la capacité d’Edge Network à lire le cookie. L’utilisation de l’indicateur `HTTPOnly` n’affecte pas les politiques de cookie qui peuvent limiter la durée de vie des cookies. Cependant, il s’agit toujours d’un élément à prendre en compte lorsque vous définissez et lisez la valeur du FPID.
* **`Secure`** : les cookies définis avec l’attribut `Secure` ne sont envoyés au serveur qu’avec une requête chiffrée via le protocole HTTPS. L’utilisation de cet indicateur peut permettre de s’assurer que les personnes malveillantes ne peuvent pas accéder facilement à la valeur du cookie . Dans la mesure du possible, il est toujours préférable de définir l’indicateur de `Secure`.
* **`SameSite`** : l’attribut `SameSite` permet aux serveurs de déterminer si les cookies sont envoyés avec des requêtes intersites. L’attribut fournit une certaine protection contre les attaques multisites par falsification. Trois valeurs sont possibles : `Strict`, `Lax` et `None`. Consultez votre équipe interne pour déterminer le paramètre adapté à votre organisation. Si aucun attribut `SameSite` n’est spécifié, le paramètre par défaut de certains navigateurs est `SameSite=Lax`.

## Envoyer le FPID à Edge Network {#send-fpid}

Vous pouvez envoyer des FPID à Edge Network de deux manières :

* **[Méthode 1](#setting-cookie-datastreams)** : configurez un `CNAME` pour vos appels Web SDK et incluez le nom de votre cookie FPID dans la configuration de votre flux de données.
* **[Méthode 2](#identityMap)** : incluez le FPID dans le mappage d’identités.

### Méthode 1 : configuration d’un `CNAME` et définition d’un cookie d’ID propriétaire dans votre flux de données {#setting-cookie-datastreams}

Pour définir un cookie FPID à partir de votre propre domaine, vous devez configurer votre propre `CNAME` pour vos appels Web SDK, puis activer la fonctionnalité de cookie d’identifiant propriétaire dans la configuration de votre flux de données. Un enregistrement `CNAME` dans votre DNS vous permet de créer un alias d’un nom de domaine à un autre. Cet alias peut aider à faire apparaître les services tiers comme s’ils faisaient partie de votre propre domaine, ce qui fait que leurs cookies ressemblent à des cookies propriétaires. Lorsque la collecte de données propriétaire est activée à l’aide d’un `CNAME`, tous les cookies de votre domaine sont envoyés sur les requêtes effectuées au point d’entrée de la collecte de données.

1. Utilisez Adobe pour créer un enregistrement `CNAME` à des fins de collecte de données dans votre organisation. Voir le [programme de certificat géré par &#x200B;](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert) pour le processus complet.
1. Activez l’option **[!UICONTROL First Party ID Cookie]** dans votre flux de données. Ce paramètre indique à Edge Network de se référer au cookie spécifié lors de la recherche d’un identifiant d’appareil interne au lieu de rechercher la valeur dans le mappage d’identités. Lors de l’activation de ce paramètre, vous devez indiquer le nom du cookie dans lequel le FPID doit être stocké. Voir [Créer et configurer des flux de données](/help/datastreams/configure.md#advanced-options) pour plus d’informations.

   ![Image de l’interface utilisateur de Platform montrant la configuration du flux de données mettant en surbrillance le paramètre Cookie d’identifiant propriétaire](/help/collection/js/assets/first-party-id-datastreams.png)

### Méthode 2 : utiliser des FPID dans `identityMap` {#identityMap}

Au lieu de stocker le FPID dans votre propre cookie, vous pouvez envoyer le FPID à Edge Network par le biais du mappage d’identité.

Vous trouverez ci-dessous un exemple de définition d’un FPID dans le `identityMap` :

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ]
  }
}
```

Comme pour les autres types d’identité, vous pouvez inclure le FPID avec d’autres identités dans `identityMap`. L’exemple suivant inclut le FPID avec un ID CRM authentifié :

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": false
      }
    ],
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Si le FPID est contenu dans un cookie lu par Edge Network lorsque la collecte de données propriétaires est activée, capturez uniquement l’identifiant CRM authentifié :

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

La `identityMap` suivante entraîne une réponse d’erreur de la part d’Edge Network, car il lui manque l’indicateur `primary` pour le FPID. Au moins un des identifiants présents dans `identityMap` doit être marqué comme `primary`.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "authenticatedState": "ambiguous"
      }
    ],
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

## Migration vers les FPID {#migrating-to-fpid}

Si vous migrez vers des identifiants d’appareil propriétaires à partir d’une mise en œuvre précédente, il peut être difficile de visualiser à quoi la transition pourrait ressembler à un niveau inférieur. Pour illustrer ce processus, prenons un scénario qui implique un client qui a déjà visité votre site et l’impact qu’une migration FPID aurait sur la manière dont ce client est identifié dans les solutions Adobe.

![Diagramme montrant comment les valeurs d’identifiant d’un client sont mises à jour entre les visites après la migration vers les FPID](/help/collection/js/assets/identity/tracking/visits.png)

| Visite | Description |
| --- | --- |
| Première visite | Supposons que vous n’ayez pas encore commencé à définir le cookie FPID. L’ECID contenu dans le [cookie AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) est l’identifiant utilisé pour identifier le visiteur. |
| Deuxième visite | Le déploiement de la solution FPID a commencé. L’ECID existant est toujours présent et reste l’identifiant principal pour l’identification des visiteurs. |
| Troisième visite | Entre la deuxième et la troisième visite, il s’est écoulé suffisamment de temps pour que l’ECID ait été supprimé en raison d’une politique de navigateur. Cependant, comme le FPID a été défini à l’aide d’un enregistrement `A` DNS, le FPID persiste. Le FPID est désormais considéré comme l’ID principal et est utilisé pour amorcer l’ECID, qui est écrit sur l’appareil de l’utilisateur final. L’utilisateur est désormais considéré comme un nouveau visiteur dans les solutions Adobe Experience Platform et Experience Cloud. |
| Quatrième visite | Entre la troisième et la quatrième visite, il s’est écoulé suffisamment de temps pour que l’ECID ait été supprimé en raison d’une politique de navigateur. Comme lors de la visite précédente, le FPID reste en raison de la manière dont il a été défini. Cette fois, le même ECID que celui de la visite précédente est généré. L’utilisateur est affiché dans toutes les solutions Adobe Experience Platform et Experience Cloud comme le même utilisateur que lors de la visite précédente. |
| Cinquième visite | Entre la quatrième et la cinquième visite, l’utilisateur final a effacé tous les cookies dans le navigateur. Un nouveau FPID est généré et utilisé pour amorcer la création d’un nouvel ECID. L’utilisateur est désormais considéré comme un nouveau visiteur dans les solutions Adobe Experience Platform et Experience Cloud. |
