---
keywords: Experience Platform;accueil;rubriques les plus consultées;segmentation;segmentation;service de segments;segments;segments;plusieurs entités;segmentation d’entités multiples;segments d’entités multiples;segments d’entités multiples
solution: Experience Platform
title: Présentation de la segmentation d’entités multiples
topic-legacy: overview
description: La segmentation d’entités multiples est la capacité à élargir les données de profil grâce à des données supplémentaires basées sur les produits, les magasins et d’autres classes hors profil. Une fois connectées, les données des classes supplémentaires deviennent disponibles comme si elles étaient des données natives du schéma Profile.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: d036ca8c3a378494f776c2bbb05e9d687bd2e201
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 14%

---

# Présentation de la segmentation d’entités multiples

La segmentation d’entités multiples est une fonctionnalité avancée disponible dans Adobe Experience Platform. [!DNL Segmentation Service]. Cette fonctionnalité vous permet d’étendre [!DNL Real-time Customer Profile] données contenant des données &quot;non-personnes&quot; supplémentaires (également appelées &quot;entités de dimension&quot;) que votre organisation peut définir, telles que des données relatives aux produits ou aux magasins. La segmentation d’entités multiples offre une certaine souplesse lors de la définition de segments d’audience en fonction de données pertinentes pour vos besoins commerciaux uniques. Elle peut être exécutée sans expertise dans l’interrogation de bases de données. Avec la segmentation d’entités multiples, vous pouvez ajouter des données clés à vos segments sans avoir à apporter des modifications coûteuses aux flux de données ou attendre une fusion de données dorsales.

## Prise en main

La segmentation d’entités multiples nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans la segmentation. Avant de poursuivre avec ce guide, consultez la documentation suivante :

* [[!DNL Real-time Customer Profile]](../profile/home.md): Fournit un profil client unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
   * [Protections des profils](../profile/guardrails.md): Bonnes pratiques pour la création de modèles de données pris en charge par [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Permet de créer des segments à partir de [!DNL Real-time Customer Profile] data.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données de l’expérience client.
   * [Principes de base de la composition des schémas](../xdm/schema/composition.md#union): Découvrez les bonnes pratiques pour composer des schémas à utiliser dans Experience Platform. Pour utiliser au mieux la segmentation, veillez à ce que vos données soient ingérées en tant que profils et événements en fonction des [bonnes pratiques pour la modélisation des données](../xdm/schema/best-practices.md).

## Cas d&#39;utilisation

Pour illustrer la valeur de la segmentation d’entités multiples, prenez en compte trois cas d’utilisation marketing standard qui illustrent les défis présents dans la plupart des applications marketing :

### Combinaison de données d’achat en ligne et hors ligne

Un spécialiste du marketing qui a créé une campagne par e-mail peut avoir tenté de créer un segment pour une audience cible en utilisant les achats récents des clients en boutique au cours des trois derniers mois. Idéalement, ce segment nécessiterait à la fois le nom de l’article et le nom de la boutique dans laquelle l’achat a été effectué. Auparavant, le défi consistait à capturer l’identifiant de magasin à partir de l’événement d’achat et à l’affecter à un profil client individuel.

### Reciblage des emails pour l’abandon de panier

Il est souvent complexe de créer et de qualifier les utilisateurs en segments ciblant l’abandon de panier. Pour savoir quels produits inclure dans une campagne de reciblage personnalisée, vous devez disposer de données concernant les produits abandonnés par chaque individu. Ces données sont liées à des événements commerciaux qui étaient auparavant difficiles à surveiller et à partir desquels extraire des données.

## Création de segments d’entités multiples

La création d’un segment à plusieurs entités nécessite d’abord de définir les relations entre les schémas avant d’utiliser la variable [!DNL Segmentation] API ou interface utilisateur du créateur de segments pour créer la définition de segment.

### Définition des relations

La définition des relations au sein de la structure de vos schémas de modèle de données d’expérience (XDM) fait partie intégrante de la création de segments d’entités multiples. Pour les relations, le champ de la destination doit être marqué comme l’identité Principale de ce schéma. Une identité ne peut être marquée que sur des chaînes et ne peut pas l’être sur des tableaux. En outre, les relations ne doivent pas nécessairement être individuelles, car vous pouvez connecter des profils et des événements d’expérience à plusieurs destinations.

La définition des relations peut être effectuée à l’aide de l’API Schema Registry ou de l’éditeur de schémas. Pour obtenir des instructions détaillées sur la définition d’une relation entre deux schémas, veuillez choisir l’un des tutoriels suivants :

* [Définition d’une relation entre deux schémas à l’aide de l’API](../xdm/tutorials/relationship-api.md)
* [Définition d’une relation entre deux schémas à l’aide de l’interface utilisateur de l’éditeur de schémas](../xdm/tutorials/relationship-ui.md)

### Création d’un segment d’entités multiples

Une fois que vous avez défini les relations XDM nécessaires, vous pouvez commencer à créer un segment d’entités multiples. Vous pouvez le faire à l’aide de l’API Segmentation ou de l’interface utilisateur du créateur de segments. Pour plus d’informations, veuillez choisir dans les guides suivants :

* [Création d’un segment à l’aide de l’API Segmentation](./tutorials/create-a-segment.md)
* [Création d’un segment à l’aide de l’interface utilisateur du créateur de segments](./ui/overview.md)

## Évaluation et accès aux segments d’entités multiples

Après avoir créé un segment, vous pouvez évaluer les résultats du segment et y accéder à l’aide de l’API Segmentation. L’évaluation d’un segment d’entités multiples est très similaire à celle d’un segment standard. Ce processus ne peut être effectué qu’à l’aide de l’API Segmentation. Pour obtenir un guide détaillé sur l’utilisation de l’API pour évaluer les segments et y accéder, veuillez lire le [évaluation et accès aux segments](./tutorials/evaluate-a-segment.md) tutoriel .
