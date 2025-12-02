---
title: Profils Edge
description: Découvrez les profils Edge, ainsi que la terminologie associée, les régions disponibles pour les profils Edge et les services disponibles pour les profils Edge.
exl-id: dcae267f-1d5a-4e90-b634-afd42b0d4edc
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Profils Edge

Dans Adobe Experience Platform, le profil client en temps réel est la source unique de vérité pour les données d’entité. Ces données de profil se trouvent dans un hub central et répondent aux cas d’utilisation qui dépendent de l’exhaustivité et de l’exhaustivité de vos données. Toutefois, dans d’autres cas d’utilisation en temps réel, où la sensibilité au temps est plus importante, les profils Edge sont l’option préférée. Les profils Edge sont des profils légers qui s’assoient sur les bords et aident dans les cas d’utilisation de la personnalisation en temps réel.

Par exemple, les applications Adobe telles qu’Adobe Target, Destination Personalization personnalisée et Adobe Campaign utilisent des périphéries afin de fournir des expériences client personnalisées en temps réel. Les données sont acheminées vers une périphérie par projection, une destination de projection définissant la périphérie vers laquelle les données seront envoyées.

## Terminologie {#terminology}

Lorsque vous travaillez avec les périphéries, veillez à comprendre les concepts suivants :

- **Edge** : un serveur Edge est un serveur placé géographiquement qui stocke les données et les rend facilement accessibles aux applications.
- **Projection Edge** : une projection Edge est la vue de projection système d&#39;un profil sur une périphérie spécifique, qui représente les données de profil avec un identifiant unique conforme à un schéma donné pour un client donné. Par exemple, une entité respectant le schéma Profil avec l’ID `CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8`, visiteur du site web Luma, répliqué vers le centre de données VA6, contenant les champs `age = 35` et `gender = male`.

En d’autres termes, les données sont acheminées vers une périphérie par projection, la **destination de projection** définissant **vers quelle périphérie** les données seront envoyées.

## Régions disponibles {#regions}

Les régions suivantes sont disponibles pour une utilisation avec Edge :

- VA6
- OR2
- IRL1
- AUS3
- SGP3
- JPN3
- IND1

Toutes ces régions sont des options valides pour l’atterrissage des profils.

## Services disponibles {#services}

Les services suivants sont activés pour la recherche de profil sur Edge :

- [Service de programme de travail de projection](#mepw)
- [Service Express Profile](#xps)

### Service de programme de travail de projection {#mepw}

Le service de travail de projection (MEPW) surveille les modifications se produisant sur le hub dans les profils. Après avoir examiné les modifications apportées aux configurations, ce service prépare les projections et les envoie vers les régions de périphérie spécifiées précédemment. En outre, ce service traite les demandes d’actualisation d’entité et envoie les projections requises aux régions nécessaires. Les actualisations d’entité sont utilisées pour s’assurer que l’entité est accessible avec une haute disponibilité.

### Service Express Profile {#xps}

Le service XPS (Express Profile Service) récupère les profils sur les différents périphéries. Ce service reçoit les requêtes des solutions en aval, telles que les destinations Adobe Target ou Custom Personalization, et recherche les profils des bases de données sur les périphéries, puis envoie le profil demandé à la solution qui le demande. Si le profil est introuvable, une demande d’actualisation est envoyée au hub associé.

## Étapes suivantes

Après lecture de ce guide, vous devriez avoir une compréhension de base des profils Edge, y compris des informations sur les régions et services disponibles pour les profils Edge. Pour plus d’informations sur Adobe Experience Edge, voir [&#x200B; Présentation de la collecte de données &#x200B;](/help/collection/home.md).

## Annexe

La section suivante répertorie les questions fréquentes sur les profils Edge :

### Dans quelles régions les profils Edge peuvent-ils se poser ?

Les profils Edge peuvent se présenter dans différentes régions en fonction de la situation.

En outre, chaque profil Edge comporte un attribut de schéma appelé Région de l’activité utilisateur (UAR). Toutes les périphéries visitées par ce profil au cours des 14 derniers jours sont répertoriées dans cet attribut de profil. Par conséquent, lorsque cet attribut est présent dans un profil, toutes les modifications apportées au profil sont également envoyées à toutes les régions répertoriées dans l’URL.

### Comment les expirations de données fonctionnent-elles avec les profils Edge ?

Pour les profils Edge, l’expiration des données détermine la durée pendant laquelle le profil restera sur Edge avant d’être supprimé. L’expiration des données est **variable**, ce qui signifie que chaque fois que vous accédez au profil sur Edge, l’heure d’expiration des données se réinitialise. Par défaut, l’expiration des données dure 14 jours.

### Quelles données sont stockées sur le profil Edge ?

Le profil Edge stocke les attributs de profil, les identifiants de profil, ainsi que les identifiants d’audience qualifiés. Par défaut, l’expiration des données dure 14 jours.
