---
title: Priorité des espaces de noms
description: Découvrez la priorité des espaces de noms dans Identity Service.
exl-id: bb04f02e-3826-45af-b935-752ea7e6ed7c
source-git-commit: 3efbb9614f08a74ad33eb1fbb4861c34c762b66b
workflow-type: tm+mt
source-wordcount: '1788'
ht-degree: 2%

---

# Priorité des espaces de noms

>[!AVAILABILITY]
>
>Les règles de liaison de graphiques d’identités sont actuellement en disponibilité limitée. Contactez votre équipe de compte d’Adobe pour plus d’informations sur la manière d’accéder à la fonctionnalité dans les environnements de test de développement.

Chaque mise en oeuvre client est unique et personnalisée pour répondre aux objectifs d’une organisation spécifique. Par conséquent, l’importance d’un espace de noms donné varie d’un client à l’autre. Voici des exemples concrets :

* Votre entreprise peut considérer que chaque adresse électronique représente une entité d’une seule personne et, par conséquent, utiliser les [paramètres d’identité](./identity-settings-ui.md) pour configurer l’espace de noms de l’adresse électronique comme unique. Une autre société peut toutefois vouloir représenter les entités d’une seule personne comme ayant plusieurs adresses électroniques, et configurer ainsi l’espace de noms de l’email comme non unique. Ces sociétés doivent utiliser un autre espace de noms d’identité comme espace unique, tel qu’un espace de noms CRMID, de sorte qu’un identifiant d’une seule personne puisse être associé à plusieurs adresses électroniques.
* Vous pouvez collecter des comportements en ligne à l’aide d’un espace de noms &quot;Identifiant de connexion&quot;. Cet identifiant de connexion peut avoir une relation 1:1 avec le CRMID, qui stocke ensuite les attributs d’un système CRM et peut être considéré comme l’espace de noms le plus important. Dans ce cas, vous déterminez alors que l’espace de noms CRMID est une représentation plus précise d’une personne, tandis que l’espace de noms Identifiant de connexion est le deuxième plus important.

Vous devez effectuer des configurations dans Identity Service qui reflètent l’importance de vos espaces de noms, car cela influence la manière dont les profils et leurs graphiques d’identités associés sont formés et divisés.

## Déterminer vos priorités

La détermination de la priorité d’espace de noms repose sur les facteurs suivants :

### Structure du graphique d’identités

Si la structure graphique de votre organisation est superposée, la priorité de l’espace de noms doit refléter cette valeur afin que les liens appropriés soient supprimés en cas de réduction du graphique.

>[!TIP]
>
>* &quot;Graphique réduit&quot; fait référence à des scénarios où plusieurs profils disparates sont fusionnés par inadvertance dans un seul graphique d’identités.
>
>* Un graphique à couches fait référence à des graphiques d’identités qui comportent plusieurs niveaux de liens. Affichez l’image ci-dessous pour obtenir un exemple de graphique avec trois calques.

![ Diagramme des calques graphiques ](../images/namespace-priority/graph-layers.png)

### Signification sémantique de l’espace de noms

Une identité représente un objet réel. Trois objets sont représentés dans le graphique d’identités. Par ordre d&#39;importance, ils sont :

* Personnes (multi-appareils, courrier électronique, numéro de téléphone)
* Périphérique matériel
* Navigateur web (cookie)

Les espaces de noms de personne sont relativement immuables par rapport aux appareils matériels (comme IDFA, GAID), qui sont relativement immuables par rapport aux navigateurs web. En gros, vous (personne) serez toujours une seule entité, qui peut avoir plusieurs appareils (téléphone, ordinateur portable, tablette, etc.) et utiliser plusieurs navigateurs (Google Chrome, Safari, FireFox, etc.)

Une autre façon d&#39;aborder ce sujet est la cardinalité. Pour une entité de personne donnée, combien d’identités seront créées ? Dans la plupart des cas, une personne dispose d’un seul CRMID, d’une poignée d’identifiants d’appareil matériel (les réinitialisations IDFA/GAID ne doivent pas se produire souvent) et d’encore plus de cookies (une personne peut facilement naviguer sur plusieurs appareils, utiliser le mode incognito ou réinitialiser les cookies à tout moment). En règle générale, **la cardinalité inférieure indique un espace de noms avec une valeur supérieure**.

## Validation des paramètres de priorité de votre espace de noms

Une fois que vous avez compris comment vous allez hiérarchiser vos espaces de noms, vous pouvez utiliser l’outil Simulation de graphique dans l’interface utilisateur pour tester différents scénarios de réduction des graphiques et vous assurer que vos configurations de priorité renvoient les résultats graphiques attendus. Pour plus d’informations, lisez le guide sur l’utilisation de l’ [outil de simulation graphique](./graph-simulation.md).

## Configurer la priorité des espaces de noms

La priorité des espaces de noms peut être configurée à l’aide de l’ [ interface utilisateur des paramètres d’identité](./identity-settings-ui.md). Dans l’interface des paramètres d’identité, vous pouvez faire glisser et déposer un espace de noms pour déterminer son importance relative.

>[!IMPORTANT]
>
>Vous ne pouvez pas donner la priorité aux espaces de noms d’appareil/de cookie par rapport aux espaces de noms de personne. Cette restriction garantit que les erreurs de configuration ne se produisent pas.

## Utilisation des priorités des espaces de noms

Actuellement, la priorité d’espace de noms influence le comportement du système de Real-Time Customer Profile. Le diagramme ci-dessous illustre ce concept. Pour plus d’informations, consultez le guide sur les [diagrammes d’architecture Adobe Experience Platform et d’applications](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications).

![ Diagramme de la portée de l’application de la priorité d’espace de noms ](../images/namespace-priority/application-scope.png)

### Identity Service : algorithme d’optimisation des identités

Pour les structures graphiques relativement complexes, la priorité des espaces de noms joue un rôle important pour s’assurer que les liens corrects sont supprimés lorsque des scénarios de réduction des graphiques se produisent. Pour plus d’informations, consultez la [présentation de l’algorithme d’optimisation des identités](../identity-graph-linking-rules/identity-optimization-algorithm.md).

### Real-Time Customer Profile : détermination de l’identité principale pour les événements d’expérience

* Une fois que vous avez configuré les paramètres d’identité pour un environnement de test donné, l’identité principale des événements d’expérience sera déterminée par la priorité d’espace de noms la plus élevée dans la configuration.
   * En effet, les événements d’expérience sont dynamiques par nature. Un mappage d’identité peut contenir trois identités ou plus et la priorité de l’espace de noms garantit que l’espace de noms le plus important est associé à l’événement d’expérience.
* Par conséquent, les configurations **suivantes ne seront plus utilisées par Real-Time Customer Profile** :
   * La configuration d’identité principale (`primary=true`) lors de l’envoi d’identités dans identityMap à l’aide du SDK Web, du SDK Mobile ou de l’API de serveur Edge Network (l’espace de noms d’identité et la valeur d’identité continueront à être utilisés dans Profile). **Remarque** : les services en dehors de Real-Time Customer Profile comme le stockage de lac de données ou Adobe Target continueront à utiliser la configuration d’identité principale (`primary=true`).
   * Tous les champs marqués comme identité principale sur un schéma de classe d’événement d’expérience XDM.
   * Paramètres d’identité principale par défaut dans le connecteur source Adobe Analytics (ECID ou AAID).
* D’un autre côté, la priorité **espace de noms ne détermine pas l’identité principale des enregistrements de profil**.
   * Pour les enregistrements de profil, vous devez continuer à définir vos champs d’identité dans le schéma, y compris l’identité principale. Pour plus d’informations, consultez le guide sur la [définition des champs d’identité dans l’interface utilisateur](../../xdm/ui/fields/identity.md) .

>[!TIP]
>
>* La priorité de l’espace de noms est **une propriété d’un espace de noms**. Il s’agit d’une valeur numérique attribuée à un espace de noms pour indiquer son importance relative.
>
>* L’identité de Principal est l’identité par laquelle un fragment de profil est stocké. Un fragment de profil est un enregistrement de données qui stocke des informations sur un utilisateur spécifique : attributs (par exemple, enregistrements CRM) ou événements (par exemple, navigation sur un site web).

### Exemple de scénario

Cette section fournit un exemple de la manière dont la configuration des priorités peut affecter vos données.

Supposons que les configurations suivantes soient établies pour un environnement de test donné :

| Espace de noms | Application réelle de l’espace de noms | Priorité |
| --- | --- | --- |
| CRMID | Utilisateur | 1 |
| IDFA | Périphérique matériel Apple (iPhone, IPad, etc.) | 2 |
| GAID | Périphérique matériel Google (Google Pixel, Pixelbook, etc.) | 3 |
| ECID | Navigateur web (Firefox, Safari, Google Chrome, etc.) | 4 |
| AAID | Navigateur web | 5 |

{style="table-layout:auto"}

Compte tenu des configurations décrites ci-dessus, les actions de l’utilisateur et la détermination de l’identité principale seront résolues en tant que telles :

| Action de l’utilisateur (événement d’expérience) | État d’authentification | Source de données | Espaces de noms dans un événement | Espace de noms de l’identité principale |
| --- | --- | --- | --- | --- |
| Afficher la page d’offre de carte de crédit | Non authentifié (anonyme) | SDK Web | `{ECID}` | ECID |
| Afficher la page d’aide | Non authentifié | SDK Mobile | `{ECID, IDFA}` | IDFA |
| Afficher le solde du compte de contrôle | Authenticated (Authentifié) | SDK Web | `{CRMID, ECID}` | CRMID |
| Inscrivez-vous au prêt immobilier | Authenticated (Authentifié) | Connecteur source Analytics | `{CRMID, ECID, AAID}` | CRMID |
| Transférer 1 000 $ de l’archivage à l’épargne | Authenticated (Authentifié) | SDK Mobile | `{CRMID, GAID, ECID}` | CRMID |

{style="table-layout:auto"}

### Segmentation Service : stockage des métadonnées d’adhésion à un segment

![ Diagramme de stockage de l’adhésion au segment ](../images/namespace-priority/segment-membership-storage.png)

Pour un profil fusionné donné, les appartenances aux segments sont stockées par rapport à l’identité ayant la priorité d’espace de noms la plus élevée.

Supposons, par exemple, qu’il existe deux profils :

* Le profil 1 représente John.
   * Le profil de John est admissible pour S1 (adhésion au segment 1). Par exemple, S1 peut faire référence à un segment de clients qui s’identifient comme masculins.
   * Le profil de John est également admissible pour S2 (appartenance au segment 2). Cela peut faire référence à un segment de clients dont l’état de fidélité est or.
* Le profil 2 représente Jane.
   * Le profil de Jeanne est admissible pour S3 (appartenance au segment 3). Cela peut se rapporter à un segment de clients qui s’identifient comme femmes.
   * Le profil de Jeanne est également admissible pour S4 (appartenance au segment 4). Cela peut se rapporter à un segment de clients dont le statut de fidélité est platine.

Si John et Jane partagent un appareil, l’ECID (navigateur web) passe d’une personne à une autre. Cependant, cela n’a aucune incidence sur les informations d’adhésion au segment stockées par rapport à John et Jane.

Si les critères de qualification du segment étaient uniquement basés sur des événements anonymes stockés par rapport à l’ECID, Jane serait admissible pour ce segment.

## Implications sur d’autres services Experience Platform {#implications}

Cette section décrit comment la priorité des espaces de noms peut affecter d’autres services Experience Platform.

### Gestion avancée du cycle de vie des données

Les demandes de suppression d’enregistrements d’hygiène des données fonctionnent comme suit pour une identité donnée :

* Profil client en temps réel : supprime tout fragment de profil avec une identité spécifiée comme identité principale. **L’identité principale sur Profile sera désormais déterminée en fonction de la priorité de l’espace de noms.**
* Lac de données : supprime tout enregistrement avec l’identité spécifiée comme identité principale. Contrairement à Real-Time Customer Profile, l’identité principale dans le lac de données est basée sur l’identité principale spécifiée sur WebSDK (`primary=true`) ou un champ marqué comme identité principale.

Pour plus d’informations, consultez la [présentation de la gestion avancée du cycle de vie](../../hygiene/home.md).

### Attributs calculés

Si les paramètres d’identité sont activés, les attributs calculés utiliseront la priorité d’espace de noms pour stocker la valeur d’attribut calculée. Pour un événement donné, l’identité avec la priorité d’espace de noms la plus élevée aura la valeur de l’attribut calculé écrit sur celle-ci. Pour plus d’informations, consultez le [guide de l’interface utilisateur des attributs calculés](../../profile/computed-attributes/ui.md).

### Lac de données

L’ingestion de données vers le lac de données continuera à respecter les paramètres d’identité principaux configurés sur le [SDK Web](../../tags/extensions/client/web-sdk/data-element-types.md#identity-map) et les schémas.

Le lac de données ne détermine pas l’identité principale en fonction de la priorité de l’espace de noms. Par exemple, Adobe Customer Journey Analytics continuera à utiliser les valeurs dans la carte d’identité même après l’activation de la priorité d’espace de noms (par exemple, l’ajout d’un jeu de données à une nouvelle connexion), car Customer Journey Analytics utilise leurs données du lac de données.

### Schémas de modèle de données d’expérience (XDM)

Tout schéma qui n’est pas un événement d’expérience XDM, tel que les profils individuels XDM, continuera à honorer tous les champs [que vous marquez comme identité](../../xdm/ui/fields/identity.md).

Pour plus d’informations sur les schémas XDM, consultez la [présentation des schémas](../../xdm/home.md).

### Services intelligents

Lors de la sélection de vos données, vous devez spécifier un espace de noms qui sera utilisé pour déterminer les événements qui calculent les scores et les événements qui stockent les scores calculés. Il est recommandé de sélectionner l’espace de noms qui représente une personne.

* Si vous collectez des données de comportement web à l’aide de WebSDk, il est recommandé de choisir l’espace de noms CRMID dans la carte d’identité.
* Si vous collectez des données de comportement web à l’aide du connecteur source Analytics, vous devez sélectionner le descripteur d’identité (CRMID).

Cette configuration entraîne le calcul des scores uniquement à l’aide d’événements authentifiés.

Pour plus d’informations, lisez les documents sur [Attribution AI](../../intelligent-services/attribution-ai/overview.md) et [Customer AI](../../intelligent-services/customer-ai/overview.md).

### Destinations conçues par les partenaires

Les résultats d’exclusion d’audience mis à jour pour les profils associés à un appareil partagé peuvent ne pas être envoyés vers les destinations en aval. Cela peut se produire dans certains cas rares où :

* La qualification de l’audience est basée uniquement sur une activité anonyme.
* Les connexions entre plusieurs profils se produisent en peu de temps.

Pour plus d’informations sur les destinations créées par des partenaires, consultez la [présentation des destinations](../../destinations/home.md#adobe-built-and-partner-built-destinations).

### Privacy Service

La fonction [Demandes de suppression de Privacy Service](../privacy.md) fonctionne de la manière suivante pour une identité donnée :

* Profil client en temps réel : supprime tout fragment de profil avec une valeur d’identité spécifiée comme identité principale. **L’identité principale sur Profile sera désormais déterminée en fonction de la priorité de l’espace de noms.**
* Lac de données : supprime tout enregistrement avec l’identité spécifiée comme identité principale ou secondaire.

Pour plus d’informations, consultez la [présentation de Privacy Service](../../privacy-service/home.md).

### Adobe Target

Adobe Target peut générer un ciblage utilisateur inattendu pour les scénarios d’appareils partagés lors de l’utilisation de la segmentation Edge.