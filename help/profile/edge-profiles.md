---
title: Profils Edge
description: Découvrez les profils Edge, ainsi que la terminologie associée, les régions disponibles pour les profils Edge et les services disponibles pour les profils Edge.
exl-id: dcae267f-1d5a-4e90-b634-afd42b0d4edc
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Profils Edge

Dans Adobe Experience Platform, Real-Time Customer Profile est la source unique de vérité pour les données d’entité. Ces données de profil se trouvent dans un hub central et permettent d’utiliser des cas d’utilisation qui reposent sur l’exhaustivité et l’exhaustivité de vos données. Toutefois, dans les cas d’utilisation en temps réel où le respect du temps est plus important, les profils de périphérie sont l’option préférée. Les profils Edge sont des profils légers qui se trouvent en périphérie et qui aident à des cas d’utilisation de la personnalisation en temps réel.

Par exemple, les applications Adobe telles qu’Adobe Target, la destination de personnalisation personnalisée et Adobe Campaign utilisent des périphéries afin de fournir des expériences client personnalisées en temps réel. Les données sont acheminées vers une périphérie par une projection, avec une destination de projection qui définit la périphérie vers laquelle les données seront envoyées.

## Terminologie {#terminology}

Lorsque vous utilisez des bords, veillez à comprendre les concepts suivants :

- **Edge**: une périphérie est un serveur géographiquement placé qui stocke les données et les rend facilement accessibles aux applications.
- **projection de périphérie**: une projection Edge est la vue de projection système du profil sur un serveur Edge spécifique pour représenter les données de profil avec un identifiant unique conforme à un schéma donné pour un client donné. Par exemple, une entité respectant le schéma de profil avec l’ID `CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8`, visiteur du site web Luma, répliqué vers le centre de données VA6, contenant les champs `age = 35` et `gender = male`.

En d’autres termes, les données sont acheminées vers une périphérie par une projection, avec la variable **destination de la projection** définition **which** Edge les données seront envoyées à .

## Régions disponibles {#regions}

Les régions suivantes peuvent être utilisées avec Edge :

- VA6
- OR2
- IRL1
- AUS3
- SGP3
- JPN3
- IND1

Toutes ces régions sont des options valides pour que les profils puissent y accéder.

## Services disponibles {#services}

Les services suivants sont activés pour la recherche de profil en périphérie :

- [Service de traitement de projection](#mepw)
- [Service de profil express](#xps)

### Service de traitement de projection {#mepw}

Le service de traitement des projections (MEPW) surveille les changements qui se produisent sur le hub sur les profils. Après avoir examiné les modifications apportées aux configurations, ce service prépare les projections et les envoie aux régions périphériques spécifiées précédemment. En outre, ce service traite les demandes d’actualisation d’entité et envoie les projections requises aux régions nécessaires. Les actualisations d’entité sont utilisées pour garantir que l’entité est accessible en haute disponibilité.

### Service de profil express {#xps}

Le service de profil express (XPS) récupère les profils sur les différentes périphéries. Ce service reçoit les demandes des solutions en aval, telles que les destinations Adobe Target ou de personnalisation personnalisée, recherche les profils des bases de données sur les périphéries et envoie le profil demandé à la solution qui le demande. Si le profil est introuvable, une demande d’actualisation est envoyée au hub associé.

## Étapes suivantes

Après avoir lu ce guide, vous devez avoir une compréhension de base des profils Edge, y compris des informations sur les régions et services disponibles pour les profils Edge. Pour plus d’informations sur Adobe Experience Edge, veuillez lire le [Présentation d’Edge Network](../web-sdk/home.md#edge-network).

## Annexe

La section suivante répertorie les questions fréquentes sur les profils Edge :

### Quelles régions peuvent accueillir les profils en périphérie ?

Les profils Edge peuvent atterrir dans différentes régions en fonction de la situation à portée de main.

De plus, chaque profil de périphérie comporte un attribut de schéma appelé région d’activité utilisateur (UAR). Toutes les périphéries visitées par ce profil au cours des 14 derniers jours sont répertoriées dans cet attribut de profil. Par conséquent, lorsque cet attribut est présent dans un profil, toutes les modifications apportées au profil sont également envoyées à toutes les régions répertoriées dans l’UAR.

### Comment l’expiration des données fonctionne-t-elle avec les profils Edge ?

Pour les profils Edge, l’expiration des données détermine la durée pendant laquelle le profil restera sur Edge avant sa suppression. L’expiration des données est **roller**, ce qui signifie qu’à chaque accès au profil, le délai d’expiration des données est réinitialisé. Par défaut, l’expiration des données dure 14 jours.

### Quelles données sont stockées sur le profil Edge ?

Edge Profile stocke les attributs de profil, les identifiants de profil, ainsi que les identifiants d’audience qualifiés. Par défaut, l’expiration des données dure 14 jours.
