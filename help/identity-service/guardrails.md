---
keywords: Experience Platform;identité;identity service;dépannage;mécanismes de sécurisation;instructions;limite;
title: Mécanismes de sécurisation pour Identity Service
description: Ce document fournit des informations sur les limites d’utilisation et de débit pour les données Identity Service afin de vous aider à optimiser l’utilisation du graphique d’identités.
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1586'
ht-degree: 39%

---

# Mécanismes de sécurisation pour les données [!DNL Identity Service]

Ce document traite de l’utilisation et des limites de débit des données [!DNL Identity Service] afin de vous aider à optimiser l’utilisation du graphique d’identité. Lors de la révision des mécanismes de sécurisation suivants, on suppose que vous avez correctement modélisé les données. Si vous avez des questions sur la manière de modéliser vos données, contactez votre représentant du service client.

>[!IMPORTANT]
>
>Vérifiez vos droits de licence dans votre commande client et la [Description du produit](https://helpx.adobe.com/fr/legal/product-descriptions.html) correspondante sur les limites d’utilisation réelles en plus de cette page de mécanismes de sécurisation.

## Commencer

Les services Experience Platform suivants sont impliqués dans la modélisation des données d’identités :

* [Identités](home.md) : identités Bridge provenant de sources de données disparates lors de leur ingestion dans Experience Platform.
* [[!DNL Real-Time Customer Profile]](../profile/home.md) : créez des profils clients unifiés à l’aide de données provenant de plusieurs sources.

## Limites du modèle de données

Les tableaux ci-dessous fournissent des conseils sur les barrières de sécurité des limites statiques et les règles de validation à prendre en compte pour les espaces de noms d’identité.

### Limites statiques

Le tableau suivant décrit les limites statiques appliquées aux données d’identité.

| Mécanisme de sécurisation | Limite | Notes |
| --- | --- | --- |
| Nombre d’identités dans un graphique | 50 | Lorsqu’un graphique avec 50 identités liées est mis à jour, Identity Service applique un mécanisme de « premier entré, premier sorti » et supprime l’identité la plus ancienne afin de libérer de l’espace pour l’identité la plus récente de ce graphique (**Remarque** : le profil client en temps réel n’est pas affecté). La suppression est basée sur le type d’identité et sur la date et l’heure. La limite est appliquée au niveau de la sandbox. Pour plus d’informations, consultez la section sur [comprendre la logique de suppression](#deletion-logic). |
| Nombre de liens vers une identité pour une ingestion par lots unique | 50 | Un seul lot peut contenir des identités anormales qui provoquent des fusions de graphiques indésirables. Pour éviter cela, Identity Service n’ingère pas les identités déjà liées à 50 identités ou plus. |
| Nombre d’identités dans un enregistrement XDM | 20 | Le nombre minimum d’enregistrements XDM requis est de deux. |
| Nombre d’espaces de noms personnalisés | Aucun | Vous pouvez créer autant d’espaces de noms personnalisés que vous le souhaitez. |
| Nombre de caractères présents dans le nom d’affichage d’un espace de noms ou un symbole d’identité | Aucun | Le nombre de caractères dans le nom d’affichage d’un espace de noms ou un symbole d’identité est illimité. |

{style="table-layout:auto"}

### Validation de la valeur d’identité

Le tableau suivant décrit les règles à suivre pour garantir la validation de votre valeur d’identité.

| Espace de noms | Règle de validation | Comportement du système en cas de violation de règle |
| --- | --- | --- |
| ECID | <ul><li>La valeur d’identité d’un ECID doit comporter exactement 38 caractères.</li><li>La valeur d’identité d’un ECID ne doit être composée que de chiffres.</li></ul> | <ul><li>Si la valeur d’identité d’un ECID ne comporte pas exactement 38 caractères, l’enregistrement est ignoré.</li><li>Si la valeur d’identité d’un ECID contient des caractères non numériques, l’enregistrement est ignoré.</li></ul> |
| Non-ECID | <ul><li>La valeur d’identité ne peut pas dépasser 1 024 caractères.</li><li>Les valeurs d’identité ne peuvent pas être « null », « anonyme », « non valide » ou être une chaîne vide (par exemple : « », « », « »).</li></ul> | <ul><li>Le cas échéant, l’enregistrement est ignoré.</li><li>L’identité sera bloquée lors de l’ingestion.</li></ul> |

{style="table-layout:auto"}

### Ingestion des espaces de noms d’identité

Depuis le 31 mars 2023, le service d’identités bloque l’ingestion des identifiants Adobe Analytics (AAID) pour les nouvelles clientes et les nouveaux clients. L’ingestion de cette identité s’effectue généralement par la [source Adobe Analytics](../sources/connectors/adobe-applications/analytics.md). La [source Adobe Audience Manager](../sources//connectors/adobe-applications/audience-manager.md) est redondante, car l’ECID représente le même navigateur web. Si vous souhaitez modifier cette configuration par défaut, contactez votre équipe Adobe en charge des comptes.

## Mécanismes de sécurisation des performances {#performance-guardrails}

Identity Service surveille en permanence les données entrantes pour garantir des performances élevées et une fiabilité à grande échelle. Cependant, un afflux de données d’événement d’expérience sur une courte période peut entraîner une dégradation des performances et une latence. Adobe n’est pas responsable de cette dégradation des performances.

## Comprendre la logique de suppression lorsqu’un graphique d’identité à capacité est mis à jour {#deletion-logic}

Lorsqu’un graphique d’identité complet est mis à jour, le service d’identités supprime l’identité la plus ancienne du graphique avant d’ajouter la dernière identité. Cela permet de garantir l’exactitude et la pertinence des données d’identité. Le processus de suppression suit les deux règles suivantes :

### Règle 1 : la priorité de suppression dépend du type d’identité d’un espace de noms

La priorité de suppression est comme suit :

1. ID de cookie
2. ID d’appareil
3. ID, e-mail et téléphone sur l’ensemble des appareils

### Règle 2 : la suppression est basée sur la date et l’heure stockées sur l’identité

Chaque identité liée d’un graphique possède une date et une heure correspondantes qui lui sont propres. Lorsqu’un graphique complet est mis à jour, le service d’identités supprime l’identité dont la date et l’heure sont les plus anciennes.

Lorsqu’un graphique complet est mis à jour avec une nouvelle identité, les deux règles agissent de concert pour désigner l’ancienne identité à supprimer. Le service d’identités supprime d’abord l’ID de cookie le plus ancien, puis l’ID d’appareil le plus ancien et enfin l’ID/e-mail/téléphone sur l’ensemble des appareils le plus ancien.

>[!NOTE]
>
>Si l’identité à supprimer est liée à plusieurs autres identités du graphique, les liens reliant cette identité sont également supprimés.

### Implications sur la mise en œuvre

Les sections suivantes décrivent les implications de la logique de suppression pour Identity Service, le profil client en temps réel et le SDK Web.

#### Service d’identités : modifications du type d’identité d’espace de noms personnalisé

Contactez l’équipe de votre compte Adobe pour demander un changement de type d’identité si votre sandbox de production contient :

* Un espace de noms personnalisé dans lequel les identifiants de personne (tels que les CRMID) sont configurés comme type d’identité de cookie/appareil.
* Espace de noms personnalisé dans lequel les identifiants de cookie/appareil sont configurés comme type d’identité entre appareils.

Une fois cette fonctionnalité disponible, les graphiques qui dépassent la limite de 50 identités sont réduits à 50 identités maximum. Pour Real-Time CDP B2C Edition, cela peut entraîner une augmentation minimale du nombre de profils qualifiés pour une audience, car ces profils étaient auparavant ignorés de la segmentation et de l’activation.

#### Real-Time Customer Profile : impact sur les audiences adressables

La suppression ne concerne que les données du service d’identités et non le profil client en temps réel.

* Ce comportement peut par conséquent créer plus de profils avec un seul ECID, car l’ECID ne fait plus partie du graphique d’identité.
* Pour respecter les numéros de droits d’audience adressables, il est recommandé d’activer l’[expiration des données de profil pseudonymes](../profile/pseudonymous-profiles.md) pour supprimer les anciens profils.

#### Real-Time Customer Profile et WebSDK : suppression d’identités de Principal

Si vous souhaitez conserver vos événements authentifiés par rapport au CRMID, il est recommandé de modifier vos identifiants principaux d’ECID en CRMID. Lisez les documents suivants pour savoir comment mettre en œuvre cette modification :

* [Configurer le mappage d’identités pour les balises Experience Platform](../tags/extensions/client/web-sdk/data-element-types.md#identity-map).
* [Données d’identité dans Experience Platform Web SDK](../web-sdk/identity/overview.md#using-identitymap)

### Exemples de scénarios

#### Exemple 1 : graphique volumineux standard

*Notes du diagramme :*

* `t` = date et heure.
* La valeur d’une date et heure correspond à la récence d’une identité donnée. Par exemple, `t1` représente la première identité liée (la plus ancienne) et `t51` représente la plus récente identité liée.

Dans cet exemple, avant que le graphique de gauche puisse être mis à jour avec une nouvelle identité, Identity Service supprime d’abord l’identité existante avec la date et l’heure les plus anciennes. Cependant, comme l’identité la plus ancienne est un ID d’appareil, le service d’identités ignore cette identité et cherche à supprimer un espace de noms avec un type plus élevé dans la liste de priorité de suppression, en l’occurrence `ecid-3`. Une fois la suppression de l’identité la plus ancienne avec un type de priorité de suppression plus élevé effectuée, le graphique est mis à jour avec un nouveau lien, `ecid-51`.

* Dans les rares cas où il existe deux identités avec le même horodatage et le même type d’identité, Identity Service trie les identifiants en fonction de [XID](./api/list-native-id.md) et effectue la suppression.

![Exemple de suppression de l’identité la plus ancienne afin d’incorporer l’identité la plus récente](./images/graph-limits-v3.png)

#### Exemple 2 : « division du graphique »

>[!BEGINTABS]

>[!TAB Événement entrant ]

*Notes du diagramme :*

* Le diagramme suivant suppose qu’au `timestamp=50`, 50 identités existent dans le graphique d’identités.
* `(...)` signifie les autres identités qui sont déjà liées dans le graphique.

Dans cet exemple, ECID:32110 est ingéré et lié à un graphique volumineux à `timestamp=51`, dépassant ainsi la limite de 50 identités.

![](./images/guardrails/before-split.png)

>[!TAB  Processus de suppression ]

Par conséquent, Identity Service supprime l’identité la plus ancienne en fonction de la date et de l’heure et du type d’identité. Dans ce cas, ECID:35577 n’est supprimé que du graphique d’identité.

![](./images/guardrails/during-split.png)

>[!TAB Sortie du graphique]

Suite à la suppression d’ECID:35577, les périphéries qui liaient CRMID:60013 et CRMID:25212 à l’ECID:35577 maintenant supprimé sont également supprimées. Ce processus de suppression entraîne la division du graphique en deux graphiques plus petits.

![](./images/guardrails/after-split.png)

>[!ENDTABS]

#### Exemple trois : « hub-and-speak »

>[!BEGINTABS]

>[!TAB Événement entrant ]

*Notes du diagramme :*

* Le diagramme suivant suppose qu’au `timestamp=50`, 50 identités existent dans le graphique d’identités.
* `(...)` signifie les autres identités qui sont déjà liées dans le graphique.

En vertu de la logique de suppression, certaines identités « hub » peuvent également être supprimées. Ces identités hub font référence aux nœuds qui sont liés à plusieurs identités individuelles qui seraient autrement dissociées.

Dans l’exemple ci-dessous, ECID:21011 est ingéré et lié au graphique à `timestamp=51`, dépassant ainsi la limite de 50 identités.

![](./images/guardrails/hub-and-spoke-start.png)

>[!TAB  Processus de suppression ]

Par conséquent, Identity Service supprime uniquement l’identité la plus ancienne du graphique d’identités, qui est dans ce cas ECID:35577. La suppression d’ECID:35577 entraîne également la suppression des éléments suivants :

* Le lien entre CRMID : 60013 et l’ECID : 35577 maintenant supprimé, entraînant ainsi un scénario de partage du graphique.
* IDFA : 32110, IDFA : 02383 et les identités restantes représentées par `(...)`. Ces identités sont supprimées, car, individuellement, elles ne sont liées à aucune autre identité et ne peuvent donc pas être représentées dans un graphique.

![](./images/guardrails/hub-and-spoke-process.png)

>[!TAB Sortie du graphique]

Enfin, le processus de suppression génère deux graphiques plus petits.

![](./images/guardrails/hub-and-spoke-result.png)

>[!ENDTABS]

## Étapes suivantes

Pour plus d’informations sur [!DNL Identity Service], consultez la documentation suivante :

* [Vue d’ensemble des [!DNL Identity Service]](home.md)
* [Visionneuse de graphiques d’identités](features/identity-graph-viewer.md)

Consultez la documentation suivante pour plus d’informations sur les autres mécanismes de sécurisation des services Experience Platform, sur les informations de latence de bout en bout et les informations de licence dans les documents de description du produit Real-Time CDP :

* [Mécanismes de sécurisation de Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagrammes de latence de bout en bout](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=fr#end-to-end-latency-diagrams) pour divers services Experience Platform.
* [Real-Time Customer Data Platform (édition B2C - packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Packages Prime et Ultimate)](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
