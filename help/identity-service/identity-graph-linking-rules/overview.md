---
title: Présentation des règles de liaison de graphiques d’identités
description: Découvrez les règles de liaison de graphique d’identités dans Identity Service.
badge: Version bêta
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 67b08acaecb4adf4d30d6d4aa7b8c24b30dfac2e
workflow-type: tm+mt
source-wordcount: '1114'
ht-degree: 1%

---

# Présentation des règles de liaison de graphiques d’identités

>[!AVAILABILITY]
>
>Cette fonctionnalité n’est pas encore disponible ; le programme bêta pour les règles de liaison de graphiques d’identités devrait commencer en juillet sur les environnements de test de développement. Contactez votre équipe de compte d’Adobe pour plus d’informations sur les critères de participation.

## Table des matières 

* [Vue d’ensemble](./overview.md)
* [Algorithme d’optimisation des identités](./identity-optimization-algorithm.md)
* [Exemples de scénarios](./example-scenarios.md)

Avec Adobe Experience Platform Identity Service et Real-time Customer Profile, il est facile de supposer que vos données sont parfaitement ingérées et que tous les profils fusionnés représentent une seule personne par le biais d’un identifiant de personne, tel qu’un identifiant CRM. Cependant, il existe des scénarios possibles où certaines données peuvent tenter de fusionner plusieurs profils disparates en un seul profil (&quot;effondrement du graphique&quot;). Pour éviter ces fusions indésirables, vous pouvez utiliser les configurations fournies par le biais des règles de liaison des graphiques d’identités et permettre une personnalisation précise pour vos utilisateurs.

## Exemples de scénarios de réduction de graphiques

* **Appareil partagé**: un appareil partagé fait référence à des appareils utilisés par plusieurs individus. Les tablettes, les ordinateurs de bibliothèque et les kiosques sont des exemples d’appareils partagés.
* **Emails et numéros de téléphone incorrects**: les numéros de téléphone et d’email incorrects se rapportent aux utilisateurs finaux qui enregistrent des coordonnées non valides, telles que &quot;test&quot;<span>@test.com&quot; pour les e-mails et &quot;+1-111-111-1111&quot; pour le numéro de téléphone.
* **Valeurs d’identité erronées ou mauvaises**: les valeurs d’identité erronées ou incorrectes font référence à des valeurs d’identité non uniques pouvant fusionner des identifiants CRM. Par exemple, bien que les identifiants IDFA doivent comporter 36 caractères (32 caractères alphanumériques et quatre tirets), il existe des scénarios où un IDFA avec une valeur d’identité &quot;user_null&quot; peut être ingéré. De même, les numéros de téléphone ne prennent en charge que les caractères numériques, mais un espace de noms de téléphone avec une valeur d’identité &quot;non spécifié&quot; peut être ingéré.

Pour plus d’informations sur les scénarios de cas d’utilisation des règles de liaison de graphiques d’identités, consultez le document sur [scénarios d’exemple](./example-scenarios.md).

## Règles de liaison de graphiques d’identités {#identity-graph-linking-rules}

Avec les règles de liaison de graphiques d’identités, vous pouvez :

* Créez un graphique d’identités/profil fusionné unique pour chaque utilisateur en configurant des espaces de noms uniques, ce qui empêchera deux identifiants de personnes disparates de se fusionner en un seul graphique d’identités.
* Associer des événements authentifiés en ligne à la personne en configurant les priorités

### Terminologie {#terminology}

| Terminologie | Description |
| --- | --- |
| Espace de noms unique | Un espace de noms unique est un espace de noms d’identité configuré pour être distinct dans le contexte d’un graphique d’identités. Vous pouvez configurer un espace de noms pour qu’il soit unique à l’aide de l’interface utilisateur. Une fois qu’un espace de noms est défini comme unique, un graphique ne peut avoir qu’une seule identité contenant cet espace de noms. |
| Priorité d’espace de noms | La priorité d’espace de noms fait référence à l’importance relative des espaces de noms par rapport aux autres. La priorité des espaces de noms peut être configurée via l’interface utilisateur. Vous pouvez classer les espaces de noms dans un graphique d’identités donné. Une fois activée, la priorité des noms est utilisée dans divers scénarios, tels que l’entrée pour l’algorithme d’optimisation de l’identité et la détermination de l’identité principale pour les fragments d’événement d’expérience. |
| Algorithme d’optimisation des identités | L’algorithme d’optimisation des identités garantit que les instructions créées en configurant un espace de noms et des priorités d’espace de noms uniques sont appliquées dans un graphique d’identités donné. |

### Espace de noms unique {#unique-namespace}

Vous pouvez configurer un espace de noms pour qu’il soit unique à l’aide de l’espace de travail de l’interface utilisateur des paramètres d’identité. Cela permet d’informer l’algorithme d’optimisation des identités qu’un graphique donné ne peut avoir qu’une seule identité contenant cet espace de noms unique. Cela empêche la fusion de deux identifiants de personnes disparates dans le même graphique.

Examinez le scénario suivant :

* Scott utilise une tablette et ouvre son navigateur Chrome Google pour accéder à nike<span>.com, où il se connecte et recherche de nouvelles chaussures de basket.
   * En arrière-plan, ce scénario consigne les identités suivantes :
      * Espace de noms et valeur ECID représentant l’utilisation du navigateur
      * Un espace de noms et une valeur de l’identifiant CRM pour représenter l’utilisateur authentifié (Scott s’est connecté avec son nom d’utilisateur et son mot de passe).
* Son fils Peter utilise alors la même tablette et utilise également Google Chrome pour accéder à nike<span>.com, où il se connecte avec son propre compte pour rechercher du matériel de football.
   * En arrière-plan, ce scénario consigne les identités suivantes :
      * Espace de noms et valeur ECID identiques pour représenter le navigateur.
      * Un nouvel espace de noms et une nouvelle valeur de l’identifiant CRM pour représenter l’utilisateur authentifié.

Si l’identifiant CRM a été configuré en tant qu’espace de noms unique, l’algorithme d’optimisation des identités divise les identifiants CRM en deux graphiques d’identités distincts, au lieu de les fusionner.

Si vous ne configurez pas d’espace de noms unique, vous pouvez obtenir des fusions de graphiques indésirables, telles que deux identités avec le même espace de noms d’identifiant CRM, mais des valeurs d’identité différentes (des scénarios comme celui-ci représentent souvent deux entités de personne différentes dans le même graphique).

Vous devez configurer un espace de noms unique pour informer l’algorithme d’optimisation des identités afin d’appliquer des limites aux données d’identité ingérées dans un graphique d’identités donné.

### Priorité d’espace de noms {#namespace-priority}

La priorité d’espace de noms fait référence à l’importance relative des espaces de noms par rapport aux autres. La priorité des espaces de noms est configurable par le biais de l’interface utilisateur et vous pouvez classer les espaces de noms dans un graphique d’identités donné.

L’une des façons dont la priorité d’espace de noms est utilisée est de déterminer l’identité principale des fragments d’événement d’expérience (comportement de l’utilisateur) sur Real-time Customer Profile. Si les paramètres de priorité sont configurés, le paramètre d’identité principal sur le SDK Web ne sera plus utilisé pour déterminer les fragments de profil stockés.

Les espaces de noms uniques et les priorités d’espace de noms peuvent être configurés dans l’espace de travail de l’interface utilisateur des paramètres d’identité. Toutefois, les effets de leurs configurations sont différents :

| | Service d’identités | Profil client en temps réel |
| --- | --- | --- |
| Espace de noms unique | Dans Identity Service, l’algorithme d’optimisation des identités fait référence aux espaces de noms uniques afin de déterminer les données d’identité ingérées dans un graphique d’identités donné. | Les espaces de noms uniques n’affectent pas Real-Time Customer Profile. |
| Priorité d’espace de noms | Dans Identity Service, pour les graphiques comportant plusieurs calques, la priorité de l’espace de noms détermine que les liens appropriés sont supprimés. | Lorsqu’un événement d’expérience est ingéré dans Profile, l’espace de noms ayant la priorité la plus élevée devient l’identité principale du fragment de profil. |

* La priorité de l’espace de noms n’affecte pas le comportement du graphique lorsque la limite de 50 identités par graphique est atteinte.
* **La priorité de l’espace de noms est une valeur numérique** affecté à un espace de noms indiquant son importance relative. Il s’agit d’une propriété d’un espace de noms.
* **L’identité du Principal est l’identité par laquelle un fragment de profil est stocké.**. Un fragment de profil est un enregistrement de données qui stocke des informations sur un utilisateur spécifique : des attributs (généralement ingérés via des enregistrements CRM) ou des événements (généralement ingérés à partir d’événements d’expérience ou de données en ligne).
* La priorité d’espace de noms détermine l’identité principale des fragments d’événement d’expérience.
   * Pour les enregistrements de profil, vous pouvez utiliser l’espace de travail des schémas de l’interface utilisateur de l’Experience Platform pour définir les champs d’identité, y compris l’identité principale. Lisez le guide sur [définition des champs d’identité dans l’interface utilisateur](../../xdm/ui/fields/identity.md) pour plus d’informations.

Pour plus d’informations, consultez le guide sur [priorité d’espace](./namespace-priority.md).

## Étapes suivantes

Pour plus d’informations sur les règles de liaison des graphiques d’identités, consultez la documentation suivante :

* [Algorithme d’optimisation des identités](./identity-optimization-algorithm.md).
* [Priorité d’espace de noms](./namespace-priority.md).
* [Exemples de scénarios de configuration des règles de liaison de graphiques d’identités](./example-scenarios.md).
