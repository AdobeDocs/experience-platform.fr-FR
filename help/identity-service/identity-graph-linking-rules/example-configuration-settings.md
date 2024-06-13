---
title: Exemples de configurations
description: Découvrez des exemples de configuration avec l’outil de simulation graphique.
hide: true
hidefromtoc: true
badge: Version bêta
source-git-commit: ba72abd9febc6d9e6491748519199b54a26ae1c5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 21%

---

# Exemples de configurations de graphique

>[!NOTE]
>
>&quot;Identifiant CRM&quot; est un espace de noms personnalisé. Par conséquent, les exemples ci-dessous vous demandent de créer un espace de noms personnalisé avec un nom d’affichage et un symbole d’identité &quot;Identifiant CRM&quot;.

La section suivante présente des exemples de scénarios graphiques que vous pouvez rencontrer avec la simulation graphique.

## Identifiant CRM uniquement

Événements :

* Identifiant CRM : Tom, ECID : 111

Configuration d’algorithme :

| Priorité | Nom d’affichage | Symbole d’identité | Type d’identité | Unique par graphe |
| ---| --- | --- | --- | --- |
| 1 | Identifiant CRM | Identifiant CRM | CROSS_DEVICE | Oui |
| 2 | ECID | ECID | COOKIE | NON |

+++Sélectionner pour afficher le graphique simulé

+++

## Identifiant CRM avec courrier électronique haché

Dans ce scénario, un identifiant CRM est ingéré et représente à la fois des données en ligne (événement d’expérience) et hors ligne (enregistrement de profil). Ce scénario implique également l’ingestion d’un email haché, qui représente un autre espace de noms envoyé dans le jeu de données d’enregistrement CRM avec l’identifiant CRM.

Événements :

* Identifiant CRM : Tom, Email_LC_SHA256 : tom<span>@acme.com
* Identifiant CRM : Tom, ECID : 111
* Identifiant CRM : Summer, Email_LC_SHA256 : summer<span>@acme.com
* Identifiant CRM : été, ECID : 222

Configuration d’algorithme :

| Priorité | Nom d’affichage | Symbole d’identité | Type d’identité | Unique par graphe |
| ---| --- | --- | --- | --- |
| 1 | Identifiant CRM | Identifiant CRM | CROSS_DEVICE | Oui |
| 2 | E-mails (SHA256, en minuscules) | Email_LC_SHA256 | E-mail | NON |
| 3 | ECID | ECID | COOKIE | NON |

+++Sélectionner pour afficher le graphique simulé

+++

## Identifiant CRM avec courrier électronique haché, téléphone haché, GAID et IDFA

Événements :

* Identifiant CRM : Tom, Email_LC_SHA256 : aabbcc, Phone_SHA256: 123-4567
* Identifiant CRM : Tom, ECID : 111
* Identifiant CRM : Tom, ECID : 222, IDFA : A-A-A
* ID de gestion de la relation client : Summer, Email_LC_SHA256: deeff, Phone_SHA256: 765-4321
* Identifiant CRM : été, ECID : 333
* Identifiant CRM : Summer, ECID : 444, GAID:B-B-B

Configuration d’algorithme :

| Priorité | Nom d’affichage | Symbole d’identité | Type d’identité | Unique par graphe |
| ---| --- | --- | --- | --- |
| 1 | Identifiant CRM | Identifiant CRM | CROSS_DEVICE | Oui |
| 2 | E-mails (SHA256, en minuscules) | Email_LC_SHA256 | E-mail | NON |
| 3 | Téléphone (SHA256) | Phone_SHA256 | Téléphone | NON |
| 4 | Google Ad ID (GAID) | GAID | DEVICE | NON |
| 5 | Apple IDFA (ID pour Apple) | IDFA | DEVICE | NON |
| 6 | ECID | ECID | COOKIE | NON |

+++Sélectionner pour afficher le graphique simulé

+++