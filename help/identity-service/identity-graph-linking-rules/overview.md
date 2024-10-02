---
title: Règles de liaison de graphiques d’identités
description: Découvrez les règles de liaison de graphiques d’identités dans Identity Service.
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: cfe0181104f09bfd91b22d165c23154a15cd5344
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 2%

---

# Présentation des règles de liaison de graphiques d’identités

>[!AVAILABILITY]
>
>Les règles de liaison de graphiques d’identités sont actuellement en disponibilité limitée. Contactez votre équipe de compte d’Adobe pour plus d’informations sur la manière d’accéder à la fonctionnalité dans les environnements de test de développement.

Avec Adobe Experience Platform Identity Service et Real-time Customer Profile, il est facile de supposer que vos données sont parfaitement ingérées et que tous les profils fusionnés représentent une seule personne par le biais d’un identifiant de personne, tel un CRMID. Cependant, il existe des scénarios possibles où certaines données peuvent tenter de fusionner plusieurs profils disparates en un seul profil (&quot;effondrement du graphique&quot;). Pour éviter ces fusions indésirables, vous pouvez utiliser les configurations fournies par le biais des règles de liaison des graphiques d’identités et permettre une personnalisation précise pour vos utilisateurs.

## Commencer

Les documents suivants sont essentiels pour comprendre les règles de liaison des graphiques d’identités.

* [Algorithme d’optimisation des identités](./identity-optimization-algorithm.md)
* [Guide de mise en oeuvre](./implementation-guide.md)
* [Exemples de configurations de graphique](./example-configurations.md)
* [Dépannage et FAQ](./troubleshooting.md)
* [Priorité des espaces de noms](./namespace-priority.md)
* [Interface utilisateur de la simulation graphique](./graph-simulation.md)
* [Interface utilisateur des paramètres d’identité](./identity-settings-ui.md)

## Exemples de scénarios de réduction de graphiques {#example-scenarios-where-graph-collapse-could-happen}

Cette section décrit les exemples de scénarios que vous pouvez prendre en compte lors de la configuration des règles de liaison de graphiques d’identités.

### Appareil partagé

Il existe des cas où plusieurs connexions peuvent se produire sur un seul appareil :

| Appareil partagé | Description |
| --- | --- |
| Ordinateurs de famille et tablettes | Le mari et la femme se connectent tous deux à leurs comptes bancaires respectifs. |
| kiosque public | Les voyageurs qui se connectent à un aéroport se servant de leur carte de fidélité pour enregistrer leurs sacs et imprimer leurs cartes d&#39;embarquement. |
| Centre d’appel | Le personnel du centre d’appels se connecte sur un seul appareil au nom des clients qui appellent le service clientèle pour résoudre les problèmes. |

![Schéma de certains appareils partagés courants.](../images/identity-settings/shared-devices.png)

Dans ce cas, d’un point de vue graphique, sans limites activées, un seul ECID est lié à plusieurs CRMID.

Avec les règles de liaison de graphiques d’identités, vous pouvez :

* Configurez l’identifiant utilisé pour la connexion en tant qu’identifiant unique. Par exemple, vous pouvez limiter un graphique pour stocker une seule identité avec un espace de noms CRMID, et ainsi définir ce CRMID en tant qu’identifiant unique d’un appareil partagé.
   * Ce faisant, vous pouvez vous assurer que les CRMID ne sont pas fusionnés par l’ECID.

### Scénarios d’email/de téléphone non valides

Il existe également des cas d’utilisateurs qui fournissent des valeurs fausses comme des numéros de téléphone et/ou des adresses électroniques lors de l’enregistrement. Dans ce cas, si les limites ne sont pas activées, les identités liées au téléphone/à l’email finiront par être liées à plusieurs CRMID différents.

![ Diagramme représentant des scénarios de courrier électronique ou de téléphone non valides.](../images/identity-settings/invalid-email-phone.png)

Avec les règles de liaison de graphiques d’identités, vous pouvez :

* Configurez le CRMID, le numéro de téléphone ou l’adresse électronique comme identifiant unique et limitez ainsi une personne à un seul CRMID, numéro de téléphone et/ou adresse électronique associée à son compte.

### Valeurs d’identité erronées ou mauvaises

Dans certains cas, des valeurs d’identité erronées non uniques sont ingérées dans le système, quel que soit l’espace de noms. Par exemple :

* Espace de noms IDFA avec la valeur d’identité &quot;user_null&quot;.
   * Les valeurs d’identité IDFA doivent comporter 36 caractères : 32 caractères alphanumériques et quatre tirets.
* Espace de noms du numéro de téléphone avec la valeur d’identité &quot;non spécifié&quot;.
   * Les numéros de téléphone ne doivent pas comporter de caractères alphabétiques.

Ces identités peuvent donner lieu aux graphiques suivants, où plusieurs CRMID sont fusionnés avec la &quot;mauvaise&quot; identité :

![Exemple graphique de données d’identité avec des valeurs d’identité erronées ou incorrectes.](../images/identity-settings/bad-data.png)

Avec les règles de liaison de graphiques d’identités, vous pouvez configurer le CRMID en tant qu’identifiant unique afin d’empêcher la réduction des profils indésirables en raison de ce type de données.

## Règles de liaison de graphiques d’identités {#identity-graph-linking-rules}

Avec les règles de liaison de graphiques d’identités, vous pouvez :

* Créez un graphique d’identités/profil fusionné unique pour chaque utilisateur en configurant des espaces de noms uniques, ce qui empêchera deux identifiants de personnes disparates de se fusionner en un seul graphique d’identités.
* Associer des événements authentifiés en ligne à la personne en configurant les priorités

### Terminologie {#terminology}

| Terminologie | Description |
| --- | --- |
| Espace de noms unique | Un espace de noms unique est un espace de noms d’identité configuré pour être distinct dans le contexte d’un graphique d’identités. Vous pouvez configurer un espace de noms pour qu’il soit unique à l’aide de l’interface utilisateur. Une fois qu’un espace de noms est défini comme unique, un graphique ne peut avoir qu’une seule identité contenant cet espace de noms. |
| Priorité des espaces de noms | La priorité d’espace de noms fait référence à l’importance relative des espaces de noms par rapport aux autres. La priorité des espaces de noms peut être configurée via l’interface utilisateur. Vous pouvez classer les espaces de noms dans un graphique d’identités donné. Une fois activée, la priorité des noms est utilisée dans divers scénarios, tels que l’entrée pour l’algorithme d’optimisation de l’identité et la détermination de l’identité principale pour les fragments d’événement d’expérience. |
| Algorithme d’optimisation des identités | L’algorithme d’optimisation des identités garantit que les instructions créées en configurant un espace de noms et des priorités d’espace de noms uniques sont appliquées dans un graphique d’identités donné. |

### Espace de noms unique {#unique-namespace}

Vous pouvez configurer un espace de noms pour qu’il soit unique à l’aide de l’espace de travail de l’interface utilisateur des paramètres d’identité. Cela permet d’informer l’algorithme d’optimisation des identités qu’un graphique donné ne peut avoir qu’une seule identité contenant cet espace de noms unique. Cela empêche la fusion de deux identifiants de personnes disparates dans le même graphique.

Examinez le scénario suivant :

* Scott utilise une tablette et ouvre son navigateur Google Chrome pour accéder à nike<span>.com, où il se connecte et recherche de nouvelles chaussures de basket.
   * En arrière-plan, ce scénario consigne les identités suivantes :
      * Espace de noms et valeur ECID représentant l’utilisation du navigateur
      * Un espace de noms et une valeur CRMID pour représenter l’utilisateur authentifié (Scott s’est connecté avec son nom d’utilisateur et son mot de passe).
* Son fils Peter utilise alors la même tablette et utilise également Google Chrome pour aller sur nike<span>.com, où il se connecte avec son propre compte pour rechercher du matériel de football.
   * En arrière-plan, ce scénario consigne les identités suivantes :
      * Espace de noms et valeur ECID identiques pour représenter le navigateur.
      * Un nouvel espace de noms et une nouvelle valeur CRMID pour représenter l’utilisateur authentifié.

Si le CRMID a été configuré en tant qu’espace de noms unique, l’algorithme d’optimisation des identités divise les CRMID en deux graphiques d’identités distincts, au lieu de les fusionner.

Si vous ne configurez pas d’espace de noms unique, vous pouvez obtenir des fusions de graphiques indésirables, telles que deux identités avec le même espace de noms CRMID, mais des valeurs d’identité différentes (des scénarios comme celui-ci représentent souvent deux entités de personne différentes dans le même graphique).

Vous devez configurer un espace de noms unique pour informer l’algorithme d’optimisation des identités afin d’appliquer des limites aux données d’identité ingérées dans un graphique d’identités donné.

### Priorité des espaces de noms {#namespace-priority}

La priorité d’espace de noms fait référence à l’importance relative des espaces de noms par rapport aux autres. La priorité des espaces de noms est configurable par le biais de l’interface utilisateur et vous pouvez classer les espaces de noms dans un graphique d’identités donné.

L’une des façons dont la priorité d’espace de noms est utilisée consiste à déterminer l’identité principale des fragments d’événement d’expérience (comportement de l’utilisateur) dans Real-time Customer Profile. Si les paramètres de priorité sont configurés, le paramètre d’identité principal sur le SDK Web ne sera plus utilisé pour déterminer les fragments de profil stockés.

Les espaces de noms uniques et les priorités d’espace de noms peuvent être configurés dans l’espace de travail de l’interface utilisateur des paramètres d’identité. Toutefois, les effets de leurs configurations sont différents :

| | Service d’identités | Profil client en temps réel |
| --- | --- | --- |
| Espace de noms unique | Dans Identity Service, l’algorithme d’optimisation des identités fait référence aux espaces de noms uniques afin de déterminer les données d’identité ingérées dans un graphique d’identités donné. | Les espaces de noms uniques n’affectent pas Real-Time Customer Profile. |
| Priorité des espaces de noms | Dans Identity Service, pour les graphiques comportant plusieurs calques, la priorité de l’espace de noms détermine que les liens appropriés sont supprimés. | Lorsqu’un événement d’expérience est ingéré dans Profile, l’espace de noms ayant la priorité la plus élevée devient l’identité principale du fragment de profil. |

* La priorité de l’espace de noms n’affecte pas le comportement du graphique lorsque la limite de 50 identités par graphique est atteinte.
* **La priorité de l’espace de noms est une valeur numérique** affectée à un espace de noms indiquant son importance relative. Il s’agit d’une propriété d’un espace de noms.
* **L’identité de Principal est l’identité dans laquelle un fragment de profil est stocké par rapport à**. Un fragment de profil est un enregistrement de données qui stocke des informations sur un utilisateur spécifique : des attributs (généralement ingérés via des enregistrements CRM) ou des événements (généralement ingérés à partir d’événements d’expérience ou de données en ligne).
* La priorité d’espace de noms détermine l’identité principale des fragments d’événement d’expérience.
   * Pour les enregistrements de profil, vous pouvez utiliser l’espace de travail des schémas de l’interface utilisateur de l’Experience Platform pour définir les champs d’identité, y compris l’identité principale. Pour plus d’informations, consultez le guide sur la [définition des champs d’identité dans l’interface utilisateur](../../xdm/ui/fields/identity.md) .
* Si un événement d’expérience a deux identités ou plus ayant la priorité d’espace de noms la plus élevée dans identityMap, il sera rejeté de l’ingestion car il sera considéré comme &quot;données incorrectes&quot;. Par exemple, si identityMap contient `{ECID: 111, CRMID: John, CRMID: Jane}`, l’ensemble de l’événement sera rejeté comme des données incorrectes, car il implique que l’événement est associé simultanément à `CRMID: John` et `CRMID: Jane`.

Pour plus d’informations, consultez le guide sur [la priorité d’espace de noms](./namespace-priority.md).

## Étapes suivantes

Pour plus d’informations sur les règles de liaison des graphiques d’identités, consultez la documentation suivante :

* [Algorithme d’optimisation des identités](./identity-optimization-algorithm.md)
* [Guide de mise en oeuvre](./implementation-guide.md)
* [Exemples de configurations de graphique](./example-configurations.md)
* [Dépannage et FAQ](./troubleshooting.md)
* [Priorité des espaces de noms](./namespace-priority.md)
* [Interface utilisateur de la simulation graphique](./graph-simulation.md)
* [Interface utilisateur des paramètres d’identité](./identity-settings-ui.md)