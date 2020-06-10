---
title: 'Notes de mise à jour d’Adobe Experience Platform '
description: Notes de mise à jour de la plateforme d’expérience le 10 août 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 7f9d1120ac323c60f899cb1cf855e55db20437ed
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 17%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : 10 juin 2020**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [Contrôle d’accès](#access-control)
- [Environnements de test](#sandboxes)

## Contrôle d’accès {#access-control}

Experience Platform tire parti des profils de produits de la Console [d’administration d’](https://adminconsole.adobe.com) Adobe pour associer les utilisateurs à des autorisations et des sandbox. Les autorisations contrôlent l’accès à diverses fonctionnalités de la plate-forme, notamment la modélisation des données, la gestion des profils et l’administration des sandbox.

**Fonctionnalités clés**

| Fonction | Description |
|--- | ---|
| Autorisations | Dans la console d’administration, l’onglet _Autorisations_ d’un profil de produits de plateforme vous permet de personnaliser les fonctionnalités de plate-forme disponibles pour les utilisateurs associés à ce profil. Les catégories d&#39;autorisation disponibles sont les suivantes : Modélisation des données, Data Management, Gestion des Profils, Identités, Surveillance des données, Administration Sandbox, Destinations, Sources. |
| Accès aux sandbox | L’onglet _Autorisations_ d’un profil de produits de plateforme permet aux utilisateurs d’accéder à des sandbox spécifiques. Pour plus d’informations, voir la section sur les [sandbox](#sandboxes) ci-dessous. |

Pour plus d&#39;informations, consultez l&#39;aperçu [du](../../access-control/home.md)contrôle d&#39;accès.

## Environnements de test {#sandboxes}

Experience Platform est conçue pour enrichir les applications d’expérience numérique à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience numérique en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, Experience Platform fournit des sandbox qui partitionnent une instance de plateforme unique en environnements virtuels distincts pour aider à développer et à développer des applications d’expérience numérique.

**Fonctionnalités clés**

| Fonction | Description |
|--- | ---|
| sandbox de production | Experience Platform fournit un sandbox de production unique, qui ne peut pas être supprimé ou réinitialisé. |
| Sandbox hors production | Vous pouvez créer plusieurs sandbox hors production pour une instance de plateforme unique, ce qui vous permet de tester des fonctionnalités, d’exécuter des expériences et de créer des configurations personnalisées sans que cela n’ait d’incidence sur votre sandbox de production. |
| Interrupteur de sandbox | Dans l’interface utilisateur de la plateforme d’expérience, le sélecteur de sandbox situé dans le coin supérieur gauche de l’écran vous permet de basculer entre les sandbox disponibles via un menu déroulant. |
| `x-sandbox-name` header | Tous les appels aux API de plateforme d’expérience doivent désormais inclure le nouvel `x-sandbox-name` en-tête, dont la valeur fait référence à l’ `name` attribut du sandbox dans lequel l’opération aura lieu. |

Pour plus d&#39;informations, consultez la présentation [des](../../sandboxes/home.md)sandbox.