---
title: Priorité d’espace de noms
description: Découvrez la priorité des espaces de noms dans Identity Service.
badge: Version bêta
source-git-commit: 85da193f422a1708999fb59b7ea095f4447d6bdf
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 2%

---

# Priorité d’espace de noms

>[!AVAILABILITY]
>
>Cette fonctionnalité n’est pas encore disponible ; le programme bêta pour les règles de liaison de graphiques d’identités devrait commencer en juillet sur les environnements de test de développement. Contactez votre équipe de compte d’Adobe pour plus d’informations sur les critères de participation.

Chaque mise en oeuvre client est unique et personnalisée pour répondre aux objectifs d’une organisation spécifique. Par conséquent, l’importance d’un espace de noms donné varie d’un client à l’autre. Voici des exemples concrets :

* D’un côté, vous pouvez considérer l’espace de noms Email comme représentant une entité de personne et donc comme unique par personne. D’un autre côté, un autre client peut considérer l’espace de noms Email comme un identifiant non fiable et donc permettre à un seul identifiant CRM d’être associé à plusieurs identités avec l’espace de noms Email.
* Vous pouvez collecter des comportements en ligne à l’aide d’un espace de noms &quot;Identifiant de connexion&quot;. Cet identifiant de connexion peut avoir une relation 1:1 avec l’identifiant CRM, qui stocke ensuite les attributs d’un système CRM et peut être considéré comme l’espace de noms le plus important. Dans ce cas, vous déterminez alors que l’espace de noms de l’ID de gestion de la relation client est une représentation plus précise d’une personne, tandis que l’espace de noms de l’ID de connexion est le deuxième plus important.

Vous devez effectuer des configurations dans Identity Service qui reflètent l’importance de vos espaces de noms, car cela influence la manière dont les profils sont formés et segmentés.

## Déterminer vos priorités

La détermination de la priorité d’espace de noms repose sur les facteurs suivants :

### Structure du graphique d’identités

Si la structure graphique de votre organisation est superposée, la priorité de l’espace de noms doit refléter cette valeur afin que les liens appropriés soient supprimés en cas de réduction du graphique.

>[!TIP]
>
>* &quot;Graphique réduit&quot; fait référence à des scénarios où plusieurs profils disparates sont fusionnés par inadvertance dans un seul graphique d’identités.
>
>* Un graphique à couches fait référence à des graphiques d’identités qui comportent plusieurs niveaux de liens. Affichez l’image ci-dessous pour obtenir un exemple de graphique avec trois calques.

![Diagramme de calques graphiques](../images/namespace-priority/graph-layers.png)

### Signification sémantique de l’espace de noms

Une identité représente un objet réel. Trois objets sont représentés dans le graphique d’identités. Par ordre d&#39;importance, ils sont :

* Personnes (multi-appareils, courrier électronique, numéro de téléphone)
* Périphérique matériel
* Navigateur web (cookie)

Les espaces de noms de personne sont relativement immuables par rapport aux appareils matériels (comme IDFA, GAID), qui sont relativement immuables par rapport aux navigateurs web. En gros, vous (personne) serez toujours une seule entité, qui peut avoir plusieurs appareils (téléphone, ordinateur portable, tablette, etc.) et utiliser plusieurs navigateurs (Google Chrome, Safari, FireFox, etc.)

Une autre façon d&#39;aborder ce sujet est la cardinalité. Pour une entité de personne donnée, combien d’identités seront créées ? Dans la plupart des cas, une personne dispose d’un identifiant CRM, d’une poignée d’identifiants d’appareil matériel (les réinitialisations IDFA/GAID ne doivent pas se produire souvent) et d’encore plus de cookies (un individu peut facilement naviguer sur plusieurs appareils, utiliser le mode incognito ou réinitialiser les cookies à tout moment). En général, **une cardinalité inférieure indique un espace de noms avec une valeur supérieure.**.

<!-- ## Step 2: Validate your namespace priority settings

Once you have an idea of how you will prioritize your namespaces, you can use the Graph Simulation tool to test out various graph collapse scenarios and ensure that your priority configurations are returning the expected graph results. For more information, read the guide on using the [Graph Simulation tool](./graph-simulation.md). -->

## Configurer la priorité des espaces de noms

La priorité des espaces de noms peut être configurée à l’aide de [!UICONTROL Paramètres d’identité]. Dans le [!UICONTROL Paramètres d’identité] , vous pouvez faire glisser et déposer un espace de noms pour déterminer son importance relative.

>[!IMPORTANT]
>
>Vous ne pouvez pas donner la priorité aux espaces de noms d’appareil/de cookie par rapport aux espaces de noms de personne. Cette restriction garantit que les erreurs de configuration ne se produisent pas.

## Utilisation des priorités des espaces de noms

Actuellement, la priorité d’espace de noms influence le comportement du système de Real-Time Customer Profile. Le diagramme ci-dessous illustre ce concept. Pour plus d’informations, consultez le guide sur [Diagrammes d’architecture de Adobe Experience Platform et d’applications](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications).

![Diagramme de la portée de l’application de priorité des espaces de noms](../images/namespace-priority/application-scope.png)

### Identity Service : algorithme d’optimisation des identités

Pour les structures graphiques relativement complexes, la priorité des espaces de noms joue un rôle important pour s’assurer que les liens corrects sont supprimés lorsque des scénarios de réduction des graphiques se produisent. Pour plus d’informations, lisez la section [[!DNL Identity Optimization Algorithm] aperçu](../identity-graph-linking-rules/identity-optimization-algorithm.md).

### Real-Time Customer Profile : détermination de l’identité principale pour les événements d’expérience

* Pour les événements d’expérience, une fois que vous avez configuré les paramètres d’identité pour un environnement de test donné, l’identité principale sera déterminée par la priorité d’espace de noms la plus élevée.
   * En effet, les événements d’expérience sont dynamiques par nature. Un mappage d’identité peut contenir trois identités ou plus et la priorité de l’espace de noms garantit que l’espace de noms le plus important est associé à l’événement d’expérience.
* Par conséquent, les configurations suivantes **ne sera plus utilisé par Real-time Customer Profile.**:
   * Case à cocher &quot;Principal&quot; sur le type d’élément de données dans WebSDK.
   * Tous les champs marqués comme identité principale sur un schéma de classe d’événement d’expérience XDM.
   * Paramètres d’identité principale par défaut dans le connecteur source Adobe Analytics (ECID ou AAID).
* D&#39;un autre côté, **la priorité d’espace de noms ne détermine pas l’identité principale des enregistrements de profil**.
   * Pour les enregistrements de profil, vous pouvez utiliser l’espace de travail des schémas de l’interface utilisateur de l’Experience Platform pour définir vos champs d’identité, y compris l’identité principale. Lisez le guide sur [définition des champs d’identité dans l’interface utilisateur](../../xdm/ui/fields/identity.md) pour plus d’informations.

>[!NOTE]
>
>* La priorité Espace de noms est **une propriété d’un espace de noms ;**. Il s’agit d’une valeur numérique attribuée à un espace de noms pour indiquer son importance relative.
>
>* L’identité de Principal est l’identité par laquelle un fragment de profil est stocké. Un fragment de profil est un enregistrement de données qui stocke des informations sur un utilisateur spécifique : des attributs (généralement ingérés via des enregistrements CRM) ou des événements (généralement ingérés à partir d’événements d’expérience ou de données en ligne).

### Exemple de scénario graphique

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

| Action de l’utilisateur (événement d’expérience) | État d’authentification | Source de données | Mappage d’identités | Identité du Principal (clé primaire du fragment de profil) |
| --- | --- | --- | --- | --- |
| Afficher la page d’offre de carte de crédit | Non authentifié (anonyme) | SDK Web | {ECID} | ECID |
| Afficher la page d’aide | Non authentifié | SDK Mobile | {ECID, IDFA} | IDFA |
| Afficher le solde du compte de contrôle | Authenticated (Authentifié) | SDK Web | {Identifiant CRM, ECID} | Identifiant CRM |
| Inscrivez-vous au prêt immobilier | Authenticated (Authentifié) | Connecteur source Analytics | {Identifiant CRM, ECID, AAID} | Identifiant CRM |
| Transférer 1 000 $ de l’archivage à l’épargne | Authenticated (Authentifié) | SDK Mobile | {Identifiant CRM, GAID, ECID} | Identifiant CRM |

{style="table-layout:auto"}

### Segmentation Service : stockage des métadonnées d’adhésion à un segment

![Un diagramme du stockage de l’adhésion aux segments](../images/namespace-priority/segment-membership-storage.png)

Pour un profil fusionné donné, les appartenances au segment sont stockées par rapport à l’identité avec l’espace de noms de priorité la plus élevée.

Supposons, par exemple, qu’il existe deux profils :

* Le premier profil représente John.
* Le deuxième profil représente Jane.

Si John et Jane partagent un appareil, l’ECID (navigateur web) passe d’une personne à une autre. Cependant, cela n’a aucune incidence sur les informations d’adhésion au segment stockées par rapport à John et Jane.

Si les critères de qualification du segment étaient uniquement basés sur des événements anonymes stockés par rapport à l’ECID, Jane serait admissible pour ce segment.

## Implications sur d’autres services Experience Platform {#implications}

Cette section décrit comment la priorité des espaces de noms peut affecter d’autres services Experience Platform.

### Gestion avancée du cycle de vie des données

Les demandes de suppression d’enregistrements d’hygiène des données fonctionnent comme suit pour une identité donnée :

* Profil client en temps réel : supprime tout fragment de profil avec une identité spécifiée comme identité principale. **L’identité principale sur Profile sera désormais déterminée en fonction de la priorité de l’espace de noms.**
* Lac de données : supprime tout enregistrement avec l’identité spécifiée comme identité principale.

Pour plus d’informations, consultez la section [présentation avancée de la gestion du cycle de vie](../../hygiene/home.md).

### Lac de données

L’ingestion de données vers le lac de données continuera à respecter les paramètres d’identité principaux configurés sur [SDK Web](../../tags/extensions/client/web-sdk/data-element-types.md#identity-map) et schémas.

Le lac de données ne détermine pas l’identité principale en fonction de la priorité de l’espace de noms. Par exemple, Adobe Customer Journey Analytics continuera à utiliser les valeurs dans la carte d’identité même après l’activation de la priorité d’espace de noms (par exemple, l’ajout d’un jeu de données à une nouvelle connexion), car Customer Journey Analytics utilise leurs données du lac de données.

### Schémas de modèle de données d’expérience (XDM)

Tout schéma qui n’est pas un événement d’expérience XDM, tel que les profils individuels XDM, continuera à honorer tout [champs que vous marquez comme identité](../../xdm/ui/fields/identity.md).

Pour plus d’informations sur les schémas XDM, consultez la section [présentation des schémas](../../xdm/home.md).

### Services intelligents

Lors de la sélection de vos données, vous devez spécifier un espace de noms qui sera utilisé pour déterminer les événements qui calculent les scores et les événements qui stockent les scores calculés. Il est recommandé de sélectionner l’espace de noms qui représente une personne.

* Si vous collectez des données de comportement web à l’aide de WebSDk, il est recommandé de choisir l’espace de noms de l’identifiant CRM dans la carte d’identité.
* Si vous collectez des données de comportement web à l’aide du connecteur source Analytics, vous devez sélectionner le descripteur d’identité (ID CRM).

Cette configuration entraîne le calcul des scores uniquement à l’aide d’événements authentifiés.

Pour plus d’informations sur, lisez les documents sur [Attribution AI](../../intelligent-services/attribution-ai/overview.md) et [Customer AI](../../intelligent-services/customer-ai/overview.md).

### Privacy Service

[Demandes de suppression Privacy Service](../privacy.md) fonctionne de la manière suivante, pour une identité donnée :

* Profil client en temps réel : supprime tout fragment de profil avec une valeur d’identité spécifiée comme identité principale. **L’identité principale sur Profile sera désormais déterminée en fonction de la priorité de l’espace de noms.**
* Lac de données : supprime tout enregistrement avec l’identité spécifiée comme identité principale ou secondaire.

Pour plus d’informations, consultez la section [Présentation de Privacy Service](../../privacy-service/home.md).