---
title: Exemples de configurations
description: Découvrez des exemples de configuration avec l’outil de simulation graphique.
badge: Version bêta
source-git-commit: 536770d0c3e7e93921fe40887dafa5c76e851f5e
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 12%

---

# Exemples de configurations de graphique

>[!AVAILABILITY]
>
>Les règles de liaison de graphiques d’identités sont actuellement en version bêta. Contactez votre équipe de compte d’Adobe pour plus d’informations sur les critères de participation. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

>[!NOTE]
>
>* &quot;CRMID&quot; et &quot;loginID&quot; sont des espaces de noms personnalisés. Dans ce document, &quot;CRMID&quot; est un identifiant de personne et &quot;loginID&quot; est un identifiant de connexion associé à une personne donnée.
>* Pour simuler les exemples de scénarios graphiques décrits dans ce document, vous devez d’abord créer deux espaces de noms personnalisés, l’un avec le symbole d’identité &quot;CRMID&quot; et l’autre avec le symbole d’identité &quot;loginID&quot;. Les symboles d’identité sont sensibles à la casse.

Ce document présente des exemples de configurations graphiques des scénarios courants que vous pouvez rencontrer lors de l’utilisation de données d’identité.

## CRMID uniquement

Il s’agit d’un exemple de scénario de mise en oeuvre simple dans lequel les événements en ligne (CRMID et ECID) sont ingérés et les événements hors ligne (enregistrements de profil) ne sont stockés que par rapport au CRMID.

**Mise en oeuvre :**

| Espaces de noms utilisés | Méthode de collecte des comportements web |
| --- | --- |
| CRMID, ECID | SDK Web |

**Événements :**

Vous pouvez créer ce scénario dans la simulation graphique en copiant les événements suivants en mode texte :

* CRMID : Tom, ECID : 111

**Configuration de l’algorithme :**

Vous pouvez créer ce scénario dans la simulation graphique en configurant la configuration suivante pour votre configuration d’algorithme :

| Priorité | Nom d’affichage | Type d’identité | Unique par graphe |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Oui |
| 2 | ECID | COOKIE | Non |

**Sélection d’identité par Principal pour Real-Time Customer Profile :**

Dans le contexte de cette configuration, l’identité principale sera définie comme suit :

| État d’authentification | Espace(s) de noms dans les événements | Identité principale |
| --- | --- | --- |
| Authenticated (Authentifié) | CRMID, ECID | CRMID |
| Non authentifié | ECID | ECID |

>[!BEGINTABS]

>[!TAB Scénario de graphique à une seule personne idéal]

Voici un exemple de graphique à une seule personne idéal, où le CRMID est unique et a la priorité la plus élevée.

![Exemple simulé de graphique idéal à une seule personne, où le CRMID est unique et a la priorité la plus élevée.](../images/graph-examples/crmid_only_single.png)

>[!TAB scénario graphique multi-personne]

Voici un exemple de graphique à plusieurs personnes. Cet exemple affiche un scénario &quot;appareil partagé&quot;, où il existe deux CRMID et celui avec l’ancien lien établi est supprimé.

![Exemple de simulation d’un graphique multi-personne. Cet exemple affiche un scénario d’appareil partagé, où il existe deux CRMID et où l’ancien lien établi est supprimé.](../images/graph-examples/crmid_only_multi.png)

>[!ENDTABS]

## CRMID avec courrier électronique haché

Dans ce scénario, un CRMID est ingéré et représente les données en ligne (événement d’expérience) et hors ligne (enregistrement de profil). Ce scénario implique également l’ingestion d’un email haché, qui représente un autre espace de noms envoyé dans le jeu de données d’enregistrement CRM avec le CRMID.

**Mise en oeuvre :**

| Espaces de noms utilisés | Méthode de collecte des comportements web |
| --- | --- |
| CRMID, Email_LC_SHA256, ECID | SDK Web |

**Événements :**

Vous pouvez créer ce scénario dans la simulation graphique en copiant les événements suivants en mode texte :

* CRMID : Tom, Email_LC_SHA256 : tom<span>@acme.com
* CRMID : Tom, ECID : 111
* CRMID : Summer, Email_LC_SHA256 : summer<span>@acme.com
* CRMID : Summer, ECID : 222

**Configuration de l’algorithme :**

Vous pouvez créer ce scénario dans la simulation graphique en configurant la configuration suivante pour votre configuration d’algorithme :

| Priorité | Nom d’affichage | Type d’identité | Unique par graphe |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Oui |
| 2 | E-mails (SHA256, en minuscules) | E-mail | Non |
| 3 | ECID | COOKIE | Non |

**Sélection d’identité de Principal pour Profile :**

Dans le contexte de cette configuration, l’identité principale sera définie comme suit :

| État d’authentification | Espace(s) de noms dans les événements | Identité principale |
| --- | --- | --- |
| Authenticated (Authentifié) | CRMID, ECID | CRMID |
| Non authentifié | ECID | ECID |

>[!BEGINTABS]

>[!TAB Scénario de graphique à une seule personne idéal]

![Dans cet exemple, deux graphiques distincts sont générés, représentant chacun une entité d’une seule personne.](../images/graph-examples/crmid_hashed_single.png)

>[!TAB graphique multi-personne : appareil partagé]

![Dans cet exemple, le graphique simulé affiche un scénario &quot;appareil partagé&quot;, car Tom et Summer sont associés au même ECID.](../images/graph-examples/crmid_hashed_shared_device.png)

>[!TAB graphique multi-personne : email non unique]

![Ce scénario est similaire à un scénario &quot;appareil partagé&quot;. Cependant, au lieu d’avoir les entités de personne qui partagent l’ECID, elles sont à la place associées au même compte de messagerie.](../images/graph-examples/crmid_hashed_nonunique_email.png)

>[!ENDTABS]

## CRMID avec courrier électronique haché, téléphone haché, GAID et IDFA

Ce scénario est similaire au précédent. Cependant, dans ce scénario, le courrier électronique et le téléphone hachés sont marqués comme des identités à utiliser dans la correspondance de segments.

**Mise en oeuvre :**

| Espaces de noms utilisés | Méthode de collecte des comportements web |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, GAID, IDFA, ECID | SDK Web |

**Événements :**

Vous pouvez créer ce scénario dans la simulation graphique en copiant les événements suivants en mode texte :

* CRMID : Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID : Tom, ECID : 111
* CRMID : Tom, ECID : 222, IDFA : A-A-A
* CRMID : Summer, Email_LC_SHA256: deeff, Phone_SHA256: 765-4321
* CRMID : Summer, ECID : 333
* CRMID : Summer, ECID : 444, GAID:B-B-B

**Configuration de l’algorithme :**

Vous pouvez créer ce scénario dans la simulation graphique en configurant la configuration suivante pour votre configuration d’algorithme :

| Priorité | Nom d’affichage | Type d’identité | Unique par graphe |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Oui |
| 2 | E-mails (SHA256, en minuscules) | E-mail | Non |
| 3 | Téléphone (SHA256) | Téléphone | Non |
| 4 | Google Ad ID (GAID) | DEVICE | Non |
| 5 | Apple IDFA (ID pour Apple) | DEVICE | Non |
| 6 | ECID | COOKIE | Non |

**Sélection d’identité de Principal pour Profile :**

Dans le contexte de cette configuration, l’identité principale sera définie comme suit :

| État d’authentification | Espace(s) de noms dans les événements | Identité principale |
| --- | --- | --- |
| Authenticated (Authentifié) | CRMID, IDFA, ECID | CRMID |
| Authenticated (Authentifié) | CRMID, GAID, ECID | CRMID |
| Authenticated (Authentifié) | CRMID, ECID | CRMID |
| Non authentifié | GAID, ECID | GAID |
| Non authentifié | IDFA, ECID | IDFA |
| Non authentifié | ECID | ECID |

>[!BEGINTABS]

>[!TAB Scénario de graphique à une seule personne idéal]

![](../images/graph-examples/crmid_hashed_single_seg_match.png)

>[!ENDTABS]

<!-- 
## Single CRMID with multiple login IDs (simple)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

Therefore, **it is crucial that the CRMID is always sent for every user**. Failure to do so may result in a "dangling" login ID scenario, where a single person entity is assumed to be sharing a device with another person.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, loginID, ECID | Web SDK |

**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID: ID_A, ECID: 111
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | loginID | loginID | CROSS_DEVICE | No |
| 3 | ECID | ECID | COOKIE | No |

## Single CRMID with multiple login IDs (complex)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

The case of "dangling" loginID also applies for this scenario.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, loginID, ECID, AAID | Adobe Analytics source connector |


**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID:ID_A, ECID: 111, AAID: AAA
* CRMID: Jane, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222, AAID: BBB

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | Email_LC_SHA256 | Email_LC_SHA256 | EMAIL | No |
| 3 | Phone_SHA256 | Phone_SHA256 | PHONE | No |
| 4 | loginID | loginID | CROSS_DEVICE | No |
| 5 | ECID | ECID | COOKIE | No |
| 6 | AAID | AAID | COOKIE | No |
 -->
