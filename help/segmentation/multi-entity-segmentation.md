---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation ; segmentation ; service de segments ; segments ; segments ; plusieurs entités ; segmentation multientités ; segments multientités ; segments multientités ;
solution: Experience Platform
title: Présentation de la segmentation multientité
topic: aperçu
description: La segmentation d’entités multiples est la capacité à élargir les données de profil grâce à des données supplémentaires basées sur les produits, les magasins et d’autres classes hors profil. Une fois connectées, les données des classes supplémentaires deviennent disponibles comme si elles étaient des données natives du schéma Profile.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 13%

---


# Présentation de la segmentation multientité

La segmentation multientité est une fonction avancée disponible dans le cadre de Adobe Experience Platform [!DNL Segmentation Service]. Cette fonctionnalité vous permet d&#39;étendre les [!DNL Real-time Customer Profile] données avec des données &quot;non-personnes&quot; supplémentaires (également appelées &quot;entités de dimension&quot;) que votre entreprise peut définir, telles que les données liées aux produits ou aux magasins. La segmentation multientité offre une flexibilité lors de la définition de segments d’audience en fonction de données pertinentes pour vos besoins commerciaux uniques et peut être effectuée sans avoir l’expertise requise pour interroger les bases de données. Avec la segmentation multientité, vous pouvez ajouter des données clés à vos segments sans avoir à apporter de modifications coûteuses aux flux de données ou attendre une fusion de données dorsales.

## Prise en main

La segmentation multientité nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans la segmentation. Avant de poursuivre avec ce guide, veuillez consulter la documentation suivante :

* [[!DNL Real-time Customer Profile]](../profile/home.md): Fournit un profil unifié pour les consommateurs en temps réel, basé sur des données agrégées provenant de plusieurs sources.
   * [Gardiens](../profile/guardrails.md) de profil : Meilleures pratiques pour la création de modèles de données pris en charge par  [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Permet de créer des segments à partir de  [!DNL Real-time Customer Profile] données.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition](../xdm/schema/composition.md#union) des schémas : Découvrez les meilleures pratiques pour composer des schémas à utiliser en Experience Platform.

## Cas d’utilisation

Pour illustrer la valeur de la segmentation multi-entités, considérez trois cas d’utilisation marketing standard qui illustrent les défis posés par la plupart des applications marketing :

### Combinaison de données d’achat en ligne et hors ligne

Un spécialiste du marketing qui a créé une campagne par e-mail peut avoir tenté de créer un segment pour une audience cible en utilisant les achats récents des clients en boutique au cours des trois derniers mois. Idéalement, ce segment nécessiterait à la fois le nom de l’article et le nom de la boutique dans laquelle l’achat a été effectué. Auparavant, le défi consistait à capturer l’identifiant de magasin à partir du événement d’achat et à l’affecter à un profil client individuel.

### Reciblage des e-mails pour l’abandon de panier

Il est souvent complexe de créer et de qualifier des utilisateurs dans des segments ciblant l’abandon de panier. Pour connaître les produits à inclure dans une campagne de reciblage personnalisée, vous devez disposer de données sur les produits abandonnés par chaque individu. Ces données sont liées à des événements commerciaux qui étaient auparavant difficiles à surveiller et à extraire des données.

## Création de segments à plusieurs entités

Pour créer un segment à plusieurs entités, vous devez d’abord définir des relations entre les schémas avant d’utiliser l’API [!DNL Segmentation] ou l’interface utilisateur du créateur de segments pour créer la définition de segment.

### Définir des relations

La définition de relations au sein de la structure de vos schémas de modèle de données d’expérience (XDM) fait partie intégrante de la création de segments à plusieurs entités. Pour les relations, le champ de la destination doit être marqué comme l&#39;identité Principale de ce schéma. Une identité ne peut être marquée que sur des chaînes et ne peut pas l&#39;être sur des tableaux. En outre, les relations n’ont pas nécessairement besoin d’être un à un, car vous pouvez connecter des profils et des événements d’expérience à plusieurs destinations.

Vous pouvez définir des relations à l&#39;aide de l&#39;API de registre de Schéma ou de l&#39;éditeur de Schéma. Pour obtenir des instructions détaillées sur la définition d’une relation entre deux schémas, veuillez choisir l’un des didacticiels suivants :

* [Définition d’une relation entre deux schémas à l’aide de l’API](../xdm/tutorials/relationship-api.md)
* [Définition d’une relation entre deux schémas à l’aide de l’interface utilisateur de l’éditeur de Schémas](../xdm/tutorials/relationship-ui.md)

### Création d’un segment à plusieurs entités

Une fois que vous avez défini les relations XDM nécessaires, vous pouvez commencer à créer un segment à plusieurs entités. Pour ce faire, vous pouvez utiliser l’API de segmentation ou l’interface utilisateur du créateur de segments. Pour plus d&#39;informations, veuillez choisir l&#39;un des guides suivants :

* [Création d’un segment à l’aide de l’API de segmentation](./tutorials/create-a-segment.md)
* [Création d’un segment à l’aide de l’interface utilisateur du créateur de segments](./ui/overview.md)

## Évaluer et accéder aux segments à plusieurs entités

Après avoir créé un segment, vous pouvez évaluer les résultats du segment et y accéder à l’aide de l’API de segmentation. L’évaluation d’un segment à plusieurs entités est très similaire à l’évaluation d’un segment standard. Ce processus ne peut être effectué qu’à l’aide de l’API de segmentation. Pour obtenir un guide détaillé sur l’utilisation de l’API pour évaluer les segments et y accéder, consultez le [didacticiel d’évaluation et d’accès aux segments](./tutorials/evaluate-a-segment.md).
