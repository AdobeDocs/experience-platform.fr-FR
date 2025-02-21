---
solution: Experience Platform
title: Présentation de la segmentation d’entités multiples
description: La segmentation d’entités multiples est la capacité à élargir les données de profil grâce à des données supplémentaires basées sur les produits, les magasins et d’autres classes hors profil. Une fois connectées, les données des classes supplémentaires deviennent disponibles comme si elles étaient des données natives du schéma Profile.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: 630041a7ef82993038ef4510dd08d3bc67bfce41
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 13%

---

# Présentation de la segmentation d’entités multiples

La segmentation d’entités multiples est une fonctionnalité avancée disponible dans le cadre de Adobe Experience Platform [!DNL Segmentation Service]. Cette fonctionnalité vous permet d’étendre les données [!DNL Real-Time Customer Profile] avec des données « non-personnes » supplémentaires (également appelées « entités de dimension ») que votre organisation peut définir, telles que des données liées aux produits ou aux magasins. La segmentation d’entités multiples offre une certaine flexibilité lors de la définition de définitions de segment basées sur des données pertinentes par rapport aux besoins de votre entreprise. Elle peut être réalisée sans expertise dans l’interrogation de bases de données. La segmentation d’entités multiples vous permet d’ajouter des données clés à vos définitions de segment sans avoir à apporter de modifications coûteuses aux flux de données ou à attendre une fusion des données en arrière-plan.

## Commencer

La segmentation d’entités multiples nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans la segmentation. Avant de poursuivre avec ce guide, consultez la documentation suivante :

* [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur en temps réel unifié basé sur des données agrégées provenant de plusieurs sources.
   * [Mécanismes de sécurisation de profil](../../profile/guardrails.md) : bonnes pratiques pour la création de modèles de données pris en charge par [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](../home.md) : permet de créer des audiences à partir de données [!DNL Real-Time Customer Profile].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données de l’expérience client.
   * [Principes de base de la composition des schémas](../../xdm/schema/composition.md#union) : découvrez les bonnes pratiques relatives à la composition de schémas à utiliser dans Experience Platform. Pour utiliser au mieux la segmentation, veillez à ce que vos données soient ingérées en tant que profils et événements en fonction des [bonnes pratiques pour la modélisation des données](../../xdm/schema/best-practices.md).

## Cas d’utilisation

Pour illustrer la valeur de la segmentation d’entités multiples, prenez trois cas d’utilisation marketing standard qui illustrent les défis présents dans la plupart des applications marketing :

### Combinaison de données d’achat en ligne et hors ligne

Un spécialiste du marketing qui crée une campagne par e-mail peut avoir tenté de créer une audience à l’aide d’achats récents dans la boutique du client au cours des trois derniers mois. Idéalement, cette audience nécessite à la fois le nom de l’article et le nom du magasin où l’achat a été effectué. Auparavant, la difficulté consistait à capturer l’identifiant de magasin à partir de l’événement d’achat et à l’affecter à un profil client individuel.

### Reciblage des e-mails pour l’abandon de panier

La création et la qualification d’utilisateurs dans des définitions de segment ciblant l’abandon de panier est complexe. Savoir quels produits inclure dans une campagne de reciblage personnalisée nécessite des données concernant les produits abandonnés par chaque individu. Ces données sont liées à des événements commerciaux qui étaient auparavant difficiles à surveiller et à extraire des données.

## Création de définitions de segment d’entités multiples

La création d’une définition de segment d’entités multiples nécessite d’abord de définir des relations entre les schémas avant d’utiliser l’API [!DNL Segmentation] ou l’interface utilisateur du créateur de segments pour créer la définition de segment.

### Définition des relations

La définition de relations dans la structure de vos schémas de modèle de données d’expérience (XDM) fait partie intégrante de la création de segments d’entités multiples. Pour les relations, le champ de la destination doit être marqué comme identité principale de ce schéma. Une identité ne peut être marquée que sur des chaînes et ne peut pas être marquée sur des tableaux. En outre, les relations n’ont pas nécessairement besoin d’être individuelles, car vous pouvez connecter des profils et des événements d’expérience à plusieurs destinations.

La définition des relations peut être effectuée à l’aide de l’API Schema Registry ou de l’éditeur de schémas. Pour obtenir des instructions détaillées sur la définition d’une relation entre deux schémas, faites votre choix parmi les tutoriels suivants :

* [Définir une relation entre deux schémas à l’aide de l’API](../../xdm/tutorials/relationship-api.md)
* [Définir une relation entre deux schémas à l’aide de l’interface utilisateur de l’éditeur de schémas](../../xdm/tutorials/relationship-ui.md)

### Créer une définition de segment d’entités multiples

Une fois que vous avez défini les relations XDM nécessaires, vous pouvez commencer à créer une définition de segment à entités multiples. Vous pouvez le faire à l’aide de l’API Segmentation ou de l’interface utilisateur du créateur de segments. Pour plus d&#39;informations, veuillez choisir parmi les guides suivants :

* [Créer une définition de segment à l’aide de l’API Segmentation](./create-a-segment.md)
* [Création d’une définition de segment à l’aide de l’interface utilisateur du créateur de segments](../ui/overview.md)

## Évaluation et accès aux définitions de segment d’entités multiples

Après avoir créé une définition de segment, vous pouvez évaluer les résultats et y accéder à l’aide de l’API Segmentation. L’évaluation d’une définition de segment d’entités multiples est très similaire à l’évaluation d’une définition de segment standard. Ce processus ne peut être effectué qu’à l’aide de l’API Segmentation. Pour obtenir un guide détaillé montrant comment utiliser l’API pour évaluer les définitions de segment et y accéder, consultez le tutoriel [évaluation et accès aux définitions de segment](./evaluate-a-segment.md).
