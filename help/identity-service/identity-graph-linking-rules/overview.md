---
title: Règles de liaison des graphiques d’identités
description: Découvrez les règles de liaison des graphiques d’identités dans Identity Service.
exl-id: 317df52a-d3ae-4c21-bcac-802dceed4e53
source-git-commit: 048d915d33a19a9d50a4951e165b5ade1b9d9734
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 5%

---

# Aperçu des règles de liaison des graphiques d’identités

>[!AVAILABILITY]
>
>Les règles de liaison de graphiques d’identités sont actuellement en disponibilité limitée. Contactez l’équipe de votre compte Adobe pour plus d’informations sur l’accès à la fonctionnalité dans les sandbox de développement.

Avec le service d’identités Adobe Experience Platform et le profil client en temps réel, il est facile de supposer que vos données sont parfaitement ingérées et que tous les profils fusionnés représentent une seule personne par le biais d’un identifiant de personne, tel qu’un CRMID. Cependant, il existe des scénarios possibles où certaines données pourraient essayer de fusionner plusieurs profils disparates en un seul profil (« réduction du graphique »). Pour éviter ces fusions indésirables, vous pouvez utiliser les configurations fournies par le biais des règles de liaison de graphiques d’identités et permettre une personnalisation précise de vos utilisateurs.

## Commencer

Les documents suivants sont essentiels à la compréhension des règles de liaison des graphiques d’identités.

* [Algorithme d’optimisation de l’identité](./identity-optimization-algorithm.md)
* [Guide de mise en œuvre](./implementation-guide.md)
* [Exemples de configurations de graphes](./example-configurations.md)
* [Résolution des problèmes et FAQ](./troubleshooting.md)
* [Priorité d’espace de noms](./namespace-priority.md)
* [Interface utilisateur de simulation de graphique](./graph-simulation.md)
* [Interface utilisateur des paramètres d’identité](./identity-settings-ui.md)

## Scénarios de réduction de graphe {#graph-collapse-scenarios}

>[!CONTEXTUALHELP]
>id="platform_identities_graphcollapsescenarios"
>title="Scénarios de réduction de graphe"
>abstract="Il existe plusieurs raisons pour lesquelles les graphes peuvent être « réduits » ou représenter plusieurs entités de personne."

Cette section présente des exemples de scénarios que vous pouvez prendre en compte lors de la configuration des règles de liaison de graphiques d’identités.

### Périphérique partagé

Il existe des instances où plusieurs connexions peuvent se produire sur un seul appareil :

| Périphérique partagé | Description |
| --- | --- |
| Ordinateurs familiaux et tablettes | Le mari et la femme se connectent à leurs comptes bancaires respectifs. |
| Kiosque public | Les voyageurs à l’aéroport se connectent en utilisant leur carte de fidélité pour enregistrer leurs bagages et imprimer leur carte d’embarquement. |
| Centre d’appel | Le personnel du centre d’appels se connecte sur un seul appareil au nom des clients qui appellent le service clientèle pour résoudre des problèmes. |

![Diagramme de certains appareils partagés courants.](../images/identity-settings/shared-devices.png)

Dans ces cas, d’un point de vue graphique, si aucune limite n’est activée, un seul ECID est lié à plusieurs CRMID.

Grâce aux règles de liaison des graphiques d’identités, vous pouvez :

* Configurez l’identifiant utilisé pour la connexion en tant qu’identifiant unique. Par exemple, vous pouvez limiter un graphique pour stocker une seule identité avec un espace de noms CRMID, et définir ce CRMID comme identifiant unique d’un appareil partagé.
   * Ce faisant, vous pouvez vous assurer que les CRMID ne sont pas fusionnés par l’ECID.

### Scénarios d’e-mail/de téléphone non valides

Il existe également des cas d’utilisateurs qui fournissent de fausses valeurs comme des numéros de téléphone et/ou des adresses e-mail lors de l’enregistrement. Dans ces cas, si les limites ne sont pas activées, les identités liées au téléphone/e-mail finiront par être liées à plusieurs CRMID différents.

![Diagramme qui représente les scénarios d’e-mail ou de téléphone non valides.](../images/identity-settings/invalid-email-phone.png)

Grâce aux règles de liaison des graphiques d’identités, vous pouvez :

* Configurez le CRMID, le numéro de téléphone ou l’adresse e-mail comme identifiant unique et limitez ainsi une personne à un seul CRMID, numéro de téléphone et/ou adresse e-mail associé à son compte.

### Valeurs d’identité erronées ou incorrectes

Dans certains cas, des valeurs d’identité non uniques et erronées sont ingérées dans le système, quel que soit l’espace de noms. Par exemple :

* Espace de noms IDFA avec la valeur d’identité « user_null ».
   * Les valeurs d’identité IDFA doivent comporter 36 caractères : 32 caractères alphanumériques et quatre tirets.
* Espace de noms du numéro de téléphone avec la valeur d’identité « non spécifié ».
   * Les numéros de téléphone ne doivent pas comporter de caractères alphabétiques.

Ces identités peuvent entraîner les graphiques suivants, dans lesquels plusieurs CRMID sont fusionnés avec la « mauvaise » identité :

![Exemple de graphique de données d’identité avec des valeurs d’identité erronées ou incorrectes.](../images/identity-settings/bad-data.png)

Grâce aux règles de liaison des graphiques d’identités, vous pouvez configurer le CRMID en tant qu’identifiant unique afin d’empêcher la réduction des profils indésirables due à ce type de données.

## Règles de liaison des graphiques d’identités {#identity-graph-linking-rules}

Grâce aux règles de liaison des graphiques d’identités, vous pouvez :

* Créez un graphique d’identités/profil fusionné unique pour chaque utilisateur en configurant des espaces de noms uniques, ce qui empêchera la fusion de deux identifiants de personne disparates en un graphique d’identités.
* Associez des événements en ligne authentifiés à la personne en configurant des priorités

### Terminologie {#terminology}

| Terminologie | Description |
| --- | --- |
| Espace de noms unique | Un espace de noms unique est un espace de noms d’identité configuré pour être distinct dans le contexte d’un graphique d’identités. Vous pouvez configurer un espace de noms pour qu’il soit unique à l’aide de l’interface utilisateur. Une fois qu’un espace de noms est défini comme unique, un graphique ne peut avoir qu’une seule identité contenant cet espace de noms. |
| Priorité d’espace de noms | La priorité des espaces de noms fait référence à l’importance relative des espaces de noms par rapport aux autres. La priorité de l’espace de noms peut être configurée via l’interface utilisateur. Vous pouvez classer les espaces de noms dans un graphique d’identités donné. Une fois activée, la priorité des noms est utilisée dans divers scénarios, comme la saisie pour l’algorithme d’optimisation des identités et la détermination de l’identité principale pour les fragments d’événement d’expérience. |
| Algorithme d’optimisation de l’identité | L’algorithme d’optimisation des identités garantit que les instructions créées en configurant un espace de noms unique et des priorités d’espace de noms sont appliquées dans un graphique d’identités donné. |

### Espace de noms unique {#unique-namespace}

Vous pouvez configurer un espace de noms comme étant unique à l’aide de l’espace de travail de l’interface utilisateur des paramètres d’identité. Ce faisant, indique à l’algorithme d’optimisation des identités qu’un graphique donné ne peut avoir qu’une seule identité contenant cet espace de noms unique. Cela empêche la fusion de deux identifiants de personne disparates dans le même graphique.

Considérez le scénario suivant :

* Scott utilise une tablette et ouvre son navigateur Google Chrome pour accéder à acme<span>.com, où il se connecte et recherche de nouvelles chaussures de basket-ball.
   * En coulisse, ce scénario consigne les identités suivantes :
      * Un espace de noms ECID et une valeur pour représenter l’utilisation du navigateur
      * Un espace de noms CRMID et une valeur pour représenter l’utilisateur authentifié (Scott s’est connecté avec sa combinaison de nom d’utilisateur et de mot de passe).
* Son fils Peter utilise ensuite la même tablette et Google Chrome pour se rendre sur acme<span>.com, où il se connecte avec son propre compte pour rechercher de l&#39;équipement de football.
   * En coulisse, ce scénario consigne les identités suivantes :
      * Le même espace de noms ECID et la même valeur pour représenter le navigateur.
      * Un nouvel espace de noms et une nouvelle valeur CRMID pour représenter l’utilisateur authentifié.

Si le CRMID a été configuré comme un espace de noms unique, l’algorithme d’optimisation des identités divise les CRMID en deux graphiques d’identités distincts, au lieu de les fusionner.

Si vous ne configurez pas d’espace de noms unique, vous pouvez obtenir des fusions de graphiques indésirables, telles que deux identités avec le même espace de noms CRMID, mais des valeurs d’identité différentes (ces scénarios représentent souvent deux entités de personne différentes dans le même graphique).

Vous devez configurer un espace de noms unique pour informer l’algorithme d’optimisation des identités afin d’appliquer des limitations aux données d’identité ingérées dans un graphique d’identités donné.

### Priorité d’espace de noms {#namespace-priority}

La priorité des espaces de noms fait référence à l’importance relative des espaces de noms par rapport aux autres. La priorité des espaces de noms est configurable via l’interface utilisateur et vous pouvez classer les espaces de noms dans un graphique d’identités donné.

La priorité d’espace de noms est utilisée notamment pour déterminer l’identité principale des fragments d’événement d’expérience (comportement de l’utilisateur) dans le profil client en temps réel. Si les paramètres de priorité sont configurés, le paramètre d’identité principale sur Web SDK ne sera plus utilisé pour déterminer les fragments de profil stockés.

Les espaces de noms uniques et les priorités des espaces de noms peuvent être configurés dans l’espace de travail de l’interface utilisateur des paramètres d’identité. Toutefois, les effets de leurs configurations sont différents :

| | Service d’identités | Profil client en temps réel |
| --- | --- | --- |
| Espace de noms unique | Dans Identity Service, l’algorithme d’optimisation des identités fait référence à des espaces de noms uniques pour déterminer les données d’identité ingérées par un graphique d’identités donné. | Les espaces de noms uniques n’affectent pas le profil client en temps réel. |
| Priorité d’espace de noms | Dans Identity Service, pour les graphiques comportant plusieurs calques, la priorité de l’espace de noms détermine que les liens appropriés sont supprimés. | Lorsqu’un événement d’expérience est ingéré dans Profile, l’espace de noms avec la priorité la plus élevée devient l’identité principale du fragment de profil. |

* La priorité de l’espace de noms n’affecte pas le comportement du graphique lorsque la limite de 50 identités par graphique est atteinte.
* **La priorité de l’espace de noms est une valeur numérique** attribuée à un espace de noms indiquant son importance relative. Il s’agit d’une propriété d’un espace de noms .
* L&#39;identité de Principal **est l&#39;identité dans laquelle un fragment de profil est stocké**. Un fragment de profil est un enregistrement de données qui stocke des informations sur un certain utilisateur ou une certaine utilisatrice : attributs (généralement ingérés via des enregistrements CRM) ou événements (généralement ingérés à partir d’événements d’expérience ou de données en ligne).
* La priorité de l’espace de noms détermine l’identité principale des fragments d’événement d’expérience.
   * Pour les enregistrements de profil, vous pouvez utiliser l’espace de travail des schémas dans l’interface utilisateur d’Experience Platform pour définir les champs d’identité, y compris l’identité principale. Pour plus d’informations, consultez le guide sur la [définition de champs d’identité dans l’interface utilisateur](../../xdm/ui/fields/identity.md).
* Si un événement d’expérience comporte plusieurs identités de la priorité d’espace de noms la plus élevée dans le mappage d’identité, il sera rejeté de l’ingestion, car il sera considéré comme des « données incorrectes ». Par exemple, si identityMap contient des `{ECID: 111, CRMID: John, CRMID: Jane}`, l’événement entier sera rejeté comme données incorrectes, car il implique que l’événement est associé à la fois aux `CRMID: John` et aux `CRMID: Jane` simultanément.

Pour plus d’informations, consultez le guide sur la [priorité des espaces de noms](./namespace-priority.md).

## Étapes suivantes

Pour plus d’informations sur les règles de liaison de graphiques d’identités, consultez la documentation suivante :

* [Algorithme d’optimisation de l’identité](./identity-optimization-algorithm.md)
* [Guide de mise en œuvre](./implementation-guide.md)
* [Exemples de configurations de graphes](./example-configurations.md)
* [Résolution des problèmes et FAQ](./troubleshooting.md)
* [Priorité d’espace de noms](./namespace-priority.md)
* [Interface utilisateur de simulation de graphique](./graph-simulation.md)
* [Interface utilisateur des paramètres d’identité](./identity-settings-ui.md)