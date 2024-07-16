---
title: Exemples De Scénarios De Configuration Des Paramètres D’Identité
description: Découvrez les exemples de scénarios de configuration des paramètres d’identité.
badge: Version bêta
exl-id: bccd5b7a-3836-47d8-b976-51747b9c1803
source-git-commit: f1779ee75c877649a69f9fa99f3872aea861beca
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%

---

# Exemples de scénarios de configuration des règles de liaison de graphiques d’identités

>[!AVAILABILITY]
>
>Cette fonctionnalité n’est pas encore disponible ; le programme bêta pour les règles de liaison de graphiques d’identités devrait commencer en juillet sur les environnements de test de développement. Contactez votre équipe de compte d’Adobe pour plus d’informations sur les critères de participation.

Ce document présente des exemples de scénarios que vous pouvez prendre en compte lors de la configuration des règles de liaison de graphiques d’identités.

## Appareil partagé

Il existe des cas où plusieurs connexions peuvent se produire sur un seul appareil :

| Appareil partagé | Description |
| --- | --- |
| Ordinateurs de famille et tablettes | Le mari et la femme se connectent tous deux à leurs comptes bancaires respectifs. |
| kiosque public | Les voyageurs qui se connectent à un aéroport se servant de leur carte de fidélité pour enregistrer leurs sacs et imprimer leurs cartes d&#39;embarquement. |
| Centre d’appel | Le personnel du centre d’appels se connecte sur un seul appareil au nom des clients qui appellent le service clientèle pour résoudre les problèmes. |

![shared-devices](../images/identity-settings/shared-devices.png)

Dans ce cas, d’un point de vue graphique, sans limites activées, un seul ECID est lié à plusieurs identifiants CRM.

Avec les règles de liaison de graphiques d’identités, vous pouvez :

* Configurez l’identifiant utilisé pour la connexion en tant qu’identifiant unique. Par exemple, vous pouvez limiter un graphique pour stocker une seule identité avec un espace de noms d’identifiant CRM, puis définir cet identifiant CRM comme identifiant unique d’un appareil partagé.
   * Ce faisant, vous pouvez vous assurer que les identifiants CRM ne sont pas fusionnés par l’ECID.

## Scénarios d’email/de téléphone non valides

Il existe également des cas d’utilisateurs qui fournissent des valeurs fausses comme des numéros de téléphone et/ou des adresses électroniques lors de l’enregistrement. Dans ce cas, si les limites ne sont pas activées, les identités liées au téléphone/à l’email finiront par être liées à plusieurs identifiants CRM différents.

![invalid-email-phone](../images/identity-settings/invalid-email-phone.png)

Avec les règles de liaison de graphiques d’identités, vous pouvez :

* Configurez l’identifiant CRM, le numéro de téléphone ou l’adresse électronique comme identifiant unique et limitez ainsi une personne à un seul identifiant CRM, numéro de téléphone et/ou adresse électronique associée à son compte.

## Valeurs d’identité erronées ou mauvaises

Dans certains cas, des valeurs d’identité erronées non uniques sont ingérées dans le système, quel que soit l’espace de noms. Par exemple :

* Espace de noms IDFA avec la valeur d’identité &quot;user_null&quot;.
   * Les valeurs d’identité IDFA doivent comporter 36 caractères : 32 caractères alphanumériques et quatre tirets.
* Espace de noms du numéro de téléphone avec la valeur d’identité &quot;non spécifié&quot;.
   * Les numéros de téléphone ne doivent pas comporter de caractères alphabétiques.

Ces identités peuvent entraîner la fusion de plusieurs identifiants CRM avec la &quot;mauvaise&quot; identité dans les graphiques suivants :

![bad-data](../images/identity-settings/bad-data.png)

Avec les règles de liaison de graphiques d’identités, vous pouvez configurer l’identifiant CRM en tant qu’identifiant unique afin d’empêcher la réduction des profils indésirables en raison de ce type de données.

## Étapes suivantes

Pour plus d’informations sur les règles de liaison des graphiques d’identités, consultez la documentation suivante :

* [Présentation des règles de liaison de graphiques d’identités](./overview.md)
* [Algorithme d’optimisation des identités](./identity-optimization-algorithm.md)
* [Identity Service et Real-time Customer Profile](../identity-and-profile.md)
* [Logique de liaison d’identités](../features/identity-linking-logic.md)
