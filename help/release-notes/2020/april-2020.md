---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience 8 avril 2020
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: 38acbb4a0130763fe0c565215eda7c0713e1ff6e

---


# Notes de mise à jour d’Adobe Experience Platform

## Date de publication : 8 avril 2020

## Contrôle d’accès

Experience Platform tire parti du de produits [Adobe Admin Console](https://adminconsole.adobe.com) pour lier les utilisateurs à des autorisations et des sandbox. Les autorisations contrôlent l’accès à diverses fonctionnalités de la plateforme, notamment la modélisation des données, la gestion des  de et l’administration des sandbox.

### Fonctionnalités clés

| Fonction | Description |
|--- | ---|
| Autorisations | Dans la console d’administration, l’onglet _Permissions_ d’un de produits de plateforme vous permet de personnaliser les fonctionnalités de plateforme disponibles pour les utilisateurs associés à ce  de.  d’autorisation disponibles : Modélisation des données, , Gestion des, Identités, Surveillance des données, Administration Sandbox, Destinations, Sources. |
| Accès aux sandbox | L’onglet _Autorisations_ d’un de produits de plateforme permet aux utilisateurs d’accéder à des sandbox spécifiques. Voir la section sur les [sandbox](#sandboxes) ci-dessous pour plus d’informations. |

Pour plus d&#39;informations, reportez-vous à l&#39;aperçu [du](../../access-control/home.md).

## Environnements de test

Experience Platform est conçue pour enrichir les applications d’expérience numérique à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience numérique en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, Experience Platform fournit des sandbox qui partitionnent une instance de plateforme unique en un virtuel distinct pour aider à développer et à développer des applications d’expérience numérique.

### Fonctionnalités clés

| Fonction | Description |
|--- | ---|
| Sandbox de production | Experience Platform fournit un sandbox de production unique, qui ne peut pas être supprimé ni réinitialisé. |
| Sandbox hors production | Plusieurs sandbox hors production peuvent être créés pour une instance de plateforme unique, ce qui vous permet de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans affecter votre sandbox de production. |
| Interrupteur de sandbox | Dans l’interface utilisateur de la plateforme d’expérience, le sélecteur de sandbox dans le coin supérieur gauche de l’écran vous permet de basculer entre les sandbox disponibles via un menu déroulant. |
| `x-sandbox-name` header | Tous les appels aux API de plateforme d’expérience doivent désormais inclure le nouvel `x-sandbox-name` en-tête, dont la valeur fait référence à l’ `name` attribut du sandbox dans lequel l’opération aura lieu. |

Pour plus d’informations, reportez-vous à la présentation [des](../../sandboxes/home.md)sandbox.