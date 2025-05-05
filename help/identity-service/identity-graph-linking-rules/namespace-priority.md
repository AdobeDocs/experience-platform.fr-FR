---
title: Priorité d’espace de noms
description: Découvrez la priorité des espaces de noms dans Identity Service.
exl-id: bb04f02e-3826-45af-b935-752ea7e6ed7c
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 3%

---

# Priorité d’espace de noms {#namespace-priority}

>[!CONTEXTUALHELP]
>id="platform_identities_namespacepriority"
>title="Priorité d’espace de noms"
>abstract="La priorité de l’espace de noms détermine comment les liens sont supprimés du graphique d’identité."

>[!AVAILABILITY]
>
>Les règles de liaison du graphique d’identités sont actuellement en disponibilité limitée et sont accessibles à tous les clients dans les sandbox de développement.
>
>* **Exigences d’activation** : la fonctionnalité reste inactive jusqu’à ce que vous configuriez et enregistriez votre [!DNL Identity Settings]. Sans cette configuration, le système continuera à fonctionner normalement, sans changement de comportement.
>* **Remarques importantes** : au cours de cette phase de disponibilité limitée, la segmentation d’Edge peut produire des résultats inattendus en termes d’appartenance à un segment. Cependant, la segmentation par lots et en flux continu fonctionnera comme prévu.
>* **Étapes suivantes** : pour plus d’informations sur la manière d’activer cette fonctionnalité dans les sandbox de production, contactez l’équipe de votre compte Adobe.

Chaque implémentation client est unique et adaptée pour répondre aux objectifs d’une organisation particulière. Par conséquent, l’importance d’un espace de noms donné varie d’un client à l’autre. Voici quelques exemples concrets :

* Votre entreprise peut considérer chaque adresse e-mail comme représentant une entité à une seule personne et utiliser donc les [ paramètres d’identité ](./identity-settings-ui.md) pour configurer l’espace de noms d’e-mail comme unique. Toutefois, une autre entreprise peut vouloir représenter des entités à personne unique comme ayant plusieurs adresses e-mail, et configurer ainsi l’espace de noms d’e-mail comme n’étant pas unique. Ces sociétés devraient utiliser un autre espace de noms d’identité comme espace de noms unique, tel qu’un espace de noms CRMID, de sorte qu’un identifiant de personne unique puisse être lié à plusieurs adresses e-mail.
* Vous pouvez collecter le comportement en ligne à l’aide d’un espace de noms « ID de connexion ». Cet identifiant de connexion peut avoir une relation 1:1 avec le CRMID, qui stocke ensuite les attributs d’un système CRM et peut être considéré comme l’espace de noms le plus important. Dans ce cas, vous déterminez alors que l’espace de noms CRMID est une représentation plus précise d’une personne, tandis que l’espace de noms d’identifiant de connexion est le deuxième plus important.

Vous devez effectuer des configurations dans Identity Service qui reflètent l’importance de vos espaces de noms, car cela influence la manière dont les profils et leurs graphiques d’identités associés sont formés et divisés.

## Déterminer vos priorités

La détermination de la priorité de l’espace de noms repose sur les facteurs suivants :

### Structure du graphique d’identités

Si la structure du graphique de votre organisation est superposée, la priorité de l’espace de noms doit refléter cette situation, de sorte que les liens appropriés soient supprimés en cas de réduction du graphique.

>[!TIP]
>
>* « Réduction du graphique » fait référence aux scénarios dans lesquels plusieurs profils disparates sont fusionnés par inadvertance en un seul graphique d’identités.
>
>* Un graphique en couches fait référence aux graphiques d’identités qui comportent plusieurs niveaux de liens. Consultez l’image ci-dessous pour obtenir un exemple de graphique avec trois calques.

![Diagramme de calques de graphique](../images/namespace-priority/graph-layers.png)

### Signification sémantique de l’espace de noms

Une identité représente un objet du monde réel. Trois objets sont représentés dans le graphique d’identités. Par ordre d’importance, ils sont les suivants :

* Personnes (sur plusieurs appareils, e-mail, numéro de téléphone)
* Appareil matériel
* Navigateur web (cookie)

Les espaces de noms de personne sont relativement immuables par rapport aux appareils (tels qu’IDFA, GAID), qui sont relativement immuables par rapport aux navigateurs web. En gros, vous (personne) serez toujours une seule entité, qui peut avoir plusieurs appareils (téléphone, ordinateur portable, tablette, etc.) et utiliser plusieurs navigateurs (Google Chrome, Safari, FireFox, etc.)

La cardinalité est une autre façon d’aborder ce sujet. Pour une entité de personne donnée, combien d’identités seront créées ? Dans la plupart des cas, une personne dispose d’un CRMID, d’une poignée d’identifiants d’appareil (les réinitialisations IDFA/GAID ne doivent pas se produire souvent) et d’encore plus de cookies (il est concevable qu’une personne puisse naviguer sur plusieurs appareils, utiliser le mode incognito ou réinitialiser les cookies à tout moment). En règle générale, **une cardinalité inférieure indique un espace de noms avec une valeur supérieure**.

## Valider les paramètres de priorité de votre espace de noms

Une fois que vous avez une idée de la manière dont vous allez prioriser vos espaces de noms, vous pouvez utiliser l’outil Simulation de graphiques dans l’interface utilisateur pour tester divers scénarios de réduction de graphique et vous assurer que vos configurations de priorité renvoient les résultats attendus du graphique. Pour plus d’informations, consultez le guide sur l’utilisation de l’outil [Simulation graphique](./graph-simulation.md).

## Configurer la priorité des espaces de noms

La priorité des espaces de noms peut être configurée à l’aide de l’interface utilisateur [paramètres d’identité](./identity-settings-ui.md). Dans l’interface des paramètres d’identité, vous pouvez faire glisser et déposer un espace de noms afin de déterminer son importance relative.

>[!IMPORTANT]
>
>Vous ne pouvez pas donner la priorité aux espaces de noms d’appareil/de cookie sur les espaces de noms de personne. Cette restriction permet de s’assurer que des erreurs de configuration ne se produisent pas.

## Utilisation de la priorité de l’espace de noms

Actuellement, la priorité de l’espace de noms influence le comportement du système du profil client en temps réel. Le diagramme ci-dessous illustre ce concept. Pour plus d&#39;informations, consultez le guide sur les diagrammes d&#39;architecture de [Adobe Experience Platform et des applications](https://experienceleague.adobe.com/fr/docs/blueprints-learn/architecture/architecture-overview/platform-applications).

![Diagramme de la portée de l’application de priorité d’espace de noms](../images/namespace-priority/application-scope.png)

## Service d’identités : algorithme d’optimisation des identités

Pour les structures de graphique relativement complexes, la priorité de l’espace de noms joue un rôle important pour s’assurer que les liens corrects sont supprimés lorsque des scénarios de réduction du graphique se produisent. Pour plus d’informations, consultez la présentation de l’algorithme d’optimisation des identités [Identity Optimization](../identity-graph-linking-rules/identity-optimization-algorithm.md).

## Profil client en temps réel : détermination d’identité principale pour les événements d’expérience

* Une fois que vous avez configuré des paramètres d’identité pour un sandbox donné, l’identité principale des événements d’expérience est déterminée par la priorité d’espace de noms la plus élevée dans la configuration.
   * En effet, les événements d’expérience sont dynamiques par nature. Un mappage d’identités peut contenir trois identités ou plus. La priorité de l’espace de noms garantit que l’espace de noms le plus important est associé à l’événement d’expérience.
* Par conséquent, les configurations suivantes **ne seront plus utilisées par le profil client en temps réel** :
   * La configuration de l’identité principale (`primary=true`) lors de l’envoi d’identités dans identityMap à l’aide de la SDK web, de Mobile SDK ou de l’API Edge Network (l’espace de noms d’identité et la valeur d’identité continueront à être utilisés dans Profile). **Remarque** : les services situés en dehors du profil client en temps réel, tels que le stockage dans le lac de données ou Adobe Target, continueront à utiliser la configuration d’identité principale (`primary=true`).
   * Tous les champs marqués comme identité principale dans un schéma de classe d’événement d’expérience XDM.
   * Paramètres d’identité principale par défaut dans le connecteur source Adobe Analytics (ECID ou AAID).
* D’un autre côté, la priorité **espace de noms) ne détermine pas l’identité principale des enregistrements de profil**.
   * Pour les enregistrements de profil, vous devez continuer à définir vos champs d’identité dans le schéma, y compris l’identité principale. Pour plus d’informations, consultez le guide sur la [définition de champs d’identité dans l’interface utilisateur](../../xdm/ui/fields/identity.md).

>[!TIP]
>
>* La priorité de l’espace de noms est **une propriété d’un espace de noms**. Il s’agit d’une valeur numérique attribuée à un espace de noms pour indiquer son importance relative.
>
>* L’identité du Principal est l’identité dans laquelle un fragment de profil est stocké. Un fragment de profil est un enregistrement de données qui stocke des informations sur un certain utilisateur ou une certaine utilisatrice : attributs (par exemple, enregistrements CRM) ou événements (par exemple, navigation sur le site web).

### Exemple de scénario

Cette section fournit un exemple de la manière dont la configuration de priorité peut affecter vos données.

Supposons que les configurations suivantes soient établies pour un sandbox donné :

| Espace de noms | Application réelle de l’espace de noms | Priorité |
| --- | --- | --- |
| CRMID | Utilisateur | 1 |
| IDFA | Appareil matériel Apple (iPhone, IPad, etc.) | 2 |
| GAID | Appareil matériel Google (Google Pixel, Pixelbook, etc.) | 3 |
| ECID | Navigateur web (Firefox, Safari, Google Chrome, etc.) | 4 |
| AAID | Navigateur web | 5 |

{style="table-layout:auto"}

Compte tenu des configurations décrites ci-dessus, les actions des utilisateurs et la détermination de l’identité principale seront résolues comme telles :

| Action utilisateur (événement d’expérience) | État d’authentification | Source de données | Espaces de noms dans l’événement | Espace de noms de l’identité principale |
| --- | --- | --- | --- | --- |
| Afficher la page d&#39;offre de carte de crédit | Non authentifié (anonyme) | SDK Web | `{ECID}` | ECID |
| Afficher la page d’aide | Non authentifié | SDK Mobile | `{ECID, IDFA}` | IDFA |
| Afficher le solde du compte courant | Authenticated (Authentifié) | SDK Web | `{CRMID, ECID}` | CRMID |
| S&#39;inscrire à un prêt immobilier | Authenticated (Authentifié) | Connecteur source Analytics | `{CRMID, ECID, AAID}` | CRMID |
| Transférer 1 000 $ du chèque à l&#39;épargne | Authenticated (Authentifié) | SDK Mobile | `{CRMID, GAID, ECID}` | CRMID |

{style="table-layout:auto"}

## Segmentation Service : stockage des métadonnées d’appartenance à un segment

![Diagramme de stockage de l’appartenance à un segment](../images/namespace-priority/segment-membership-storage.png)

Pour un profil fusionné donné, les appartenances aux segments seront stockées par rapport à l’identité avec la priorité d’espace de noms la plus élevée.

Supposons, par exemple, qu’il existe deux profils :

* Le profil 1 représente Jean.
   * Le profil de John est éligible pour S1 (appartenance à un segment 1). Par exemple, S1 peut faire référence à un segment de clients qui s’identifient comme étant de sexe masculin.
   * Le profil de John est également éligible pour S2 (appartenance à un segment 2). Il peut s’agir d’un segment de clients dont le statut de fidélité est Gold.
* Le profil 2 représente Jane.
   * Le profil de Jane est éligible pour S3 (appartenance à un segment 3). Il peut s’agir d’un segment de clients qui s’identifient comme étant de sexe féminin.
   * Le profil de Jane est également éligible pour S4 (appartenance à un segment 4). Il peut s’agir d’un segment de clients dont le statut de fidélité est platine.

Si John et Jane partagent un appareil, l’ECID (navigateur web) est transféré d’une personne à une autre. Toutefois, cela n’influence pas les informations d’appartenance à un segment stockées contre John et Jane.

Si les critères de qualification du segment étaient uniquement basés sur des événements anonymes stockés par rapport à l’ECID, Jane serait éligible à ce segment.

## Implications sur les autres services Experience Platform {#implications}

Cette section décrit l’impact de la priorité des espaces de noms sur d’autres services Experience Platform.

### Gestion avancée du cycle de vie des données

Les requêtes de suppression d’enregistrements d’hygiène des données fonctionnent de la manière suivante, pour une identité donnée :

* Real-Time Customer Profile : supprime tout fragment de profil présentant l’identité spécifiée comme identité principale. **L’identité principale sur le profil sera désormais déterminée en fonction de la priorité de l’espace de noms.**
* Lac de données : supprime tout enregistrement ayant l’identité spécifiée comme identité principale. Contrairement au profil client en temps réel, l’identité principale dans le lac de données est basée sur l’identité principale spécifiée dans le WebSDK (`primary=true`) ou sur un champ marqué comme identité principale

Pour plus d’informations, consultez la [présentation de la gestion avancée du cycle de vie](../../hygiene/home.md).

### Attributs calculés

Si les paramètres d’identité sont activés, les attributs calculés utilisent la priorité de l’espace de noms pour stocker la valeur d’attribut calculée. Pour un événement donné, la valeur de l’attribut calculé sera écrite en fonction de l’identité ayant la priorité d’espace de noms la plus élevée. Pour plus d’informations, consultez le [guide de l’interface utilisateur des attributs calculés](../../profile/computed-attributes/ui.md).

### Lac de données

L’ingestion des données dans le lac de données continuera à respecter les paramètres d’identité principale configurés sur les schémas [Web SDK](../../tags/extensions/client/web-sdk/data-element-types.md#identity-map) et .

Le lac de données ne détermine pas l’identité principale en fonction de la priorité de l’espace de noms. Par exemple, Adobe Customer Journey Analytics continuera à utiliser les valeurs dans le mappage d’identités même après l’activation de la priorité de l’espace de noms (comme l’ajout d’un jeu de données à une nouvelle connexion), car Customer Journey Analytics utilise ses données du lac de données.

### Schémas de modèle de données d’expérience (XDM)

Tout schéma qui n’est pas un événement d’expérience XDM, comme les profils individuels XDM, continuera à honorer tous les [champs que vous marquez comme identité](../../xdm/ui/fields/identity.md).

Pour plus d’informations sur les schémas XDM, consultez la [ présentation des schémas ](../../xdm/home.md).

### Services intelligents

Lors de la sélection de vos données, vous devez spécifier un espace de noms, qui sera utilisé pour déterminer les événements qui calculent les scores et les événements qui stockent les scores calculés. Il est recommandé de sélectionner l’espace de noms qui représente une personne.

* Si vous collectez des données de comportement web à l’aide de WebSDK, il est recommandé de choisir l’espace de noms CRMID dans le mappage d’identités.
* Si vous collectez des données de comportement web à l’aide du connecteur source Analytics, vous devez sélectionner le descripteur d’identité (CRMID).

Cette configuration permet de calculer les scores uniquement à l’aide d’événements authentifiés.

Pour plus d’informations, consultez les documents sur l’[IA dédiée à l’attribution](../../intelligent-services/attribution-ai/overview.md) et l’[IA dédiée aux clients](../../intelligent-services/customer-ai/overview.md).

### Destinations créées par les partenaires

Les résultats de disqualification d’audience mis à jour pour les profils associés à un appareil partagé peuvent ne pas être envoyés aux destinations en aval. Cela peut se produire dans de rares cas où :

* La qualification de l’audience est basée uniquement sur une activité anonyme.
* Les connexions à plusieurs profils se produisent en peu de temps.

Pour plus d’informations sur les destinations créées par les partenaires, lisez la [présentation des destinations](../../destinations/home.md#adobe-built-and-partner-built-destinations).

### Privacy Service

Les [demandes de suppression de Privacy Service](../privacy.md) fonctionnent de la manière suivante, pour une identité donnée :

* Real-Time Customer Profile : supprime tout fragment de profil avec une valeur d’identité spécifiée comme identité principale. **L’identité principale sur le profil sera désormais déterminée en fonction de la priorité de l’espace de noms.**
* Lac de données : supprime tout enregistrement ayant l’identité spécifiée comme identité principale ou secondaire.

Pour plus d’informations, consultez la [présentation de Privacy Service](../../privacy-service/home.md).

### Adobe Target

Adobe Target peut générer un ciblage utilisateur inattendu pour les scénarios d’appareil partagé lors de l’utilisation de la segmentation Edge.