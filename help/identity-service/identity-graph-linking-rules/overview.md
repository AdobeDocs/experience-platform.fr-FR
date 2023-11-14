---
title: Présentation des règles de liaison de graphiques d’identités
description: Découvrez les règles de liaison de graphique d’identités dans Identity Service.
hide: true
hidefromtoc: true
badge: Alpha
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 20b8433cee719329bce562069c328adb906697a0
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 1%

---

# Présentation des règles de liaison de graphiques d’identités

>[!IMPORTANT]
>
>Les règles de liaison de graphiques d’identités sont actuellement en Alpha. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

## Table des matières 

* [Vue d’ensemble](./overview.md)
* [Algorithme d’optimisation des identités](./identity-optimization-algorithm.md)
* [Exemples de scénarios](./example-scenarios.md)
* [Identity Service et Real-time Customer Profile](identity-and-profile.md)
* [Logique de liaison d’identités](./identity-linking-logic.md)

Avec Adobe Experience Platform Identity Service et Real-time Customer Profile, il est facile de supposer que vos données sont parfaitement ingérées et que tous les profils fusionnés représentent une seule personne par le biais d’un identifiant de personne, tel qu’un identifiant CRM. Cependant, il existe des scénarios possibles où certaines données peuvent tenter de fusionner plusieurs profils disparates en un seul profil (&quot;effondrement de profil&quot;). Pour éviter ces fusions indésirables, vous pouvez utiliser les configurations fournies par le biais des règles de liaison des graphiques d’identités et permettre une personnalisation précise pour vos utilisateurs.

## Exemples de scénarios de réduction de profil

* **Appareil partagé**: un appareil partagé fait référence à des appareils utilisés par plusieurs individus. Les tablettes, les ordinateurs de bibliothèque et les kiosques sont des exemples d’appareils partagés.
* **Emails et numéros de téléphone incorrects**: les numéros de téléphone et d’email incorrects se rapportent aux utilisateurs finaux qui enregistrent des coordonnées non valides, telles que &quot;test&quot;<span>@test.com&quot; pour les e-mails et &quot;+1-111-111-1111&quot; pour le numéro de téléphone.
* **Valeurs d’identité erronées ou mauvaises**: les valeurs d’identité erronées ou incorrectes font référence à des valeurs d’identité non uniques pouvant fusionner des identifiants CRM. Par exemple, bien que les identifiants IDFA doivent comporter 36 caractères (32 caractères alphanumériques et quatre tirets), il existe des scénarios où un IDFA avec une valeur d’identité &quot;user_null&quot; peut être ingéré. De même, les numéros de téléphone ne prennent en charge que les caractères numériques, mais un espace de noms de téléphone avec une valeur d’identité &quot;non spécifié&quot; peut être ingéré.

Pour plus d’informations sur les scénarios de cas d’utilisation des règles de liaison de graphiques d’identités, consultez le document sur [scénarios d’exemple](./example-scenarios.md).

## Objectifs des règles de liaison de graphiques d’identités

Avec les règles de liaison de graphiques d’identités, vous pouvez :

* Créez un graphique d’identités/profil fusionné unique pour chaque utilisateur en configurant des espaces de noms (limites) uniques, ce qui empêchera deux identifiants de personnes disparates de se fusionner en un seul graphique d’identités.
* Associer des événements authentifiés en ligne à la personne en configurant les priorités

### Limites

Un espace de noms unique est un identifiant qui représente un individu, tel que l’identifiant CRM, l’identifiant de connexion et le courrier électronique haché. Si un espace de noms est désigné comme unique, un graphique ne peut avoir qu’une seule identité avec cet espace de noms (`limit=1`). Cela empêchera la fusion de deux identifiants de personnes disparates dans le même graphique.

* Si aucune limite n’est configurée, il peut en résulter des fusions de graphiques indésirables, telles que deux identités avec un espace de noms d’identifiant CRM dans un graphique.
* Si aucune limite n’est configurée, le graphique peut ajouter autant d’espaces de noms que nécessaire tant que le graphique se trouve dans les barrières de sécurité (50 identités/graphiques).
* Si une limite est configurée, l’algorithme d’optimisation des identités s’assure que la limite est appliquée.

### Algorithme d’optimisation des identités

L’algorithme d’optimisation des identités est une règle qui garantit que les limites sont appliquées. L’algorithme honore les liens les plus récents et supprime les liens les plus anciens pour s’assurer qu’un graphique donné reste dans les limites que vous avez définies.

Voici une liste des implications de l’algorithme sur l’association d’événements anonymes à des identifiants connus :

* L’ECID sera associé au dernier utilisateur authentifié si les conditions suivantes sont remplies :
   * Si les identifiants CRM sont fusionnés par ECID (appareil partagé).
   * Si des limites sont configurées sur un seul identifiant CRM.

Pour plus d’informations, lisez le document sur [algorithme d’optimisation des identités](./identity-optimization-algorithm.md).

### Priorité

>[!IMPORTANT]
>
>Les priorités des espaces de noms ne sont actuellement pas disponibles pour alpha.

Vous pouvez utiliser la priorité d’espace de noms pour définir les espaces de noms les plus importants que les autres. La hiérarchie que vous définissez pour vos espaces de noms est ensuite utilisée pour définir les identités primaires et stocker les fragments de profil. Si les paramètres de priorité sont configurés, le paramètre d’identité principal sur le SDK Web ne sera plus utilisé pour déterminer les fragments de profil stockés.

* Les limites et la priorité sont des configurations indépendantes. **not** se répercutent :
   * Limites est une configuration de graphique d’identités dans Identity Service.
   * La priorité est une configuration de fragment de profil sur Real-time Customer Profile.
   * La priorité est **not** affectent les barrières de sécurité du système de graphique d’identités.

>[!BEGINSHADEBOX]

**Exemple de priorité d’espace de noms**

Supposons que vous ayez configuré la priorité suivante pour vos espaces de noms :

1. Identifiant CRM : représente un utilisateur.
2. IDFA : représente un périphérique matériel Apple, tel qu’iPhone et iPad.
3. GAID : représente un périphérique matériel Google, tel que Google Pixel.
4. ECID : représente un navigateur web, tel que Firefox, Safari et Chrome.
5. AAID : représente un navigateur web.
Si ECID et AAID sont envoyés simultanément, les deux identités représentent le même navigateur web (double).

Si les événements d’expérience suivants sont ingérés dans Experience Platform, les fragments de profil sont ensuite stockés par rapport à l’espace de noms avec la priorité la plus élevée.

**Événements authentifiés :**

* Si la carte des identités contient un ECID, un GAID et un ID CRM, les informations d’événement sont stockées par rapport à l’ID CRM (identité principale).
   * GAID représente un périphérique matériel Google (par exemple, Google Pixel), ECID représente un navigateur web (par exemple, Google Chrome) et l’ID de gestion de la relation client représente un utilisateur authentifié.
   * Si la carte des identités contient un identifiant CRM, un ECID et un AAID, les informations d’événement sont stockées par rapport à l’identifiant CRM (identité principale).

**Événements non authentifiés :**

* Si la carte d’identité contient un ECID, un IDFA et un AAID, les informations d’événement sont stockées par rapport à l’IDFA (identité principale).
   * IDFA représente un périphérique matériel Apple (par exemple iPhone), ECID et AAID représentent tous deux un navigateur web (Safari).

>[!ENDSHADEBOX]

## Étapes suivantes

Pour plus d’informations sur les règles de liaison des graphiques d’identités, consultez la documentation suivante :

* [Algorithme d’optimisation des identités](./identity-optimization-algorithm.md)
* [Exemples de scénarios de configuration des règles de liaison de graphiques d’identités](./example-scenarios.md)
* [Identity Service et Real-time Customer Profile](identity-and-profile.md)
* [Logique de liaison d’identités](./identity-linking-logic.md)
