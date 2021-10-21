---
keywords: Experience Platform ; accueil ; rubriques populaires ; segmentation ; Segmentation ; service de segment ; segments ; segments ; multientité ; segmentation multientité ; segments multientités ; segments multientités ;
solution: Experience Platform
title: Présentation de la segmentation multientité
topic-legacy: overview
description: La segmentation d’entités multiples est la capacité à élargir les données de profil grâce à des données supplémentaires basées sur les produits, les magasins et d’autres classes hors profil. Une fois connectées, les données des classes supplémentaires deviennent disponibles comme si elles étaient des données natives du schéma Profile.
exl-id: 01a37fdc-2abe-4a84-b7da-fcbd141ff51f
source-git-commit: d036ca8c3a378494f776c2bbb05e9d687bd2e201
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 12%

---

# Présentation de la segmentation multientité

La segmentation multientité est une fonction avancée disponible dans le cadre de Adobe Experience Platform. [!DNL Segmentation Service]. Cette fonctionnalité vous permet d’étendre [!DNL Real-time Customer Profile] données avec des données &quot;non-personnes&quot; supplémentaires (également appelées &quot;entités de dimension&quot;) que votre organisation peut définir, telles que des données relatives aux produits ou aux magasins. La segmentation multi-entités offre de la souplesse lors de la définition de segments d’audience en fonction de données pertinentes pour vos besoins professionnels uniques et peut être effectuée sans avoir l’expertise nécessaire pour interroger des bases de données. Avec la segmentation multi-entités, vous pouvez ajouter des données clés à vos segments sans avoir à apporter de modifications coûteuses aux flux de données ou attendre une fusion de données back-end.

## Prise en main

La segmentation multientité nécessite une compréhension pratique des différents services Adobe Experience Platform impliqués dans la segmentation. Avant de poursuivre avec ce guide, veuillez consulter la documentation suivante :

* [[!DNL Real-time Customer Profile]](../profile/home.md): Fournit un profil de consommation unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.
   * [Gardiens de profil](../profile/guardrails.md): Meilleures pratiques pour la création de modèles de données pris en charge par [!DNL Profile].
* [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Permet de créer des segments à partir de [!DNL Real-time Customer Profile] données.
* [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Principes de base de la composition de schéma](../xdm/schema/composition.md#union): Découvrez les meilleures pratiques pour la composition de schémas à utiliser dans l’Experience Platform. Pour tirer le meilleur parti de la segmentation, assurez-vous que vos données sont assimilées en tant que profils et événements en fonction de [meilleures pratiques pour la modélisation des données](../xdm/schema/best-practices.md).

## Cas d’utilisation

Pour illustrer la valeur de la segmentation multi-entités, tenez compte de trois cas d’utilisation marketing standard qui illustrent les défis présents dans la plupart des applications marketing :

### Combinaison de données d’achat en ligne et hors ligne

Un spécialiste du marketing qui a créé une campagne par e-mail peut avoir tenté de créer un segment pour une audience cible en utilisant les achats récents des clients en boutique au cours des trois derniers mois. Idéalement, ce segment nécessiterait à la fois le nom de l’article et le nom de la boutique dans laquelle l’achat a été effectué. Auparavant, le défi consistait à capturer l’identifiant du magasin à partir de l’événement d’achat et à l’affecter à un profil de client individuel.

### Reciblage des e-mails pour abandon de panier

Il est souvent complexe de créer et de qualifier des utilisateurs en segments ciblant l’abandon de panier. Pour connaître les produits à inclure dans une campagne de reciblage personnalisée, il faut des données sur les produits abandonnés par chaque individu. Ces données sont liées à des événements commerciaux qui étaient auparavant difficiles à surveiller et à extraire des données.

## Création de segments à entités multiples

La création d&#39;un segment à entités multiples nécessite d&#39;abord de définir des relations entre les schémas avant d&#39;utiliser la propriété [!DNL Segmentation] Interface utilisateur du créateur d’API ou de segments pour créer la définition de segment.

### Définition de relations

La définition de relations au sein de la structure de vos schémas XDM (Experience Data Model) fait partie intégrante de la création de segments multientités. Pour les relations, le champ de la destination doit être marqué comme l’identité principale de ce schéma. Une identité ne peut être marquée que sur des chaînes et ne peut pas l’être sur des tableaux. En outre, les relations n’ont pas nécessairement besoin d’être individuelles, car vous pouvez connecter des profils et des événements d’expérience à plusieurs destinations.

La définition de relations peut être effectuée à l&#39;aide de l&#39;API du Registre de schémas ou de l&#39;éditeur de schémas. Pour connaître les étapes détaillées de définition d’une relation entre deux schémas, choisissez l’un des tutoriels suivants :

* [Définition d’une relation entre deux schémas à l’aide de l’API](../xdm/tutorials/relationship-api.md)
* [Définition d&#39;une relation entre deux schémas à l&#39;aide de l&#39;interface utilisateur de l&#39;éditeur de schéma](../xdm/tutorials/relationship-ui.md)

### Création d’un segment à entités multiples

Une fois que vous avez défini les relations XDM nécessaires, vous pouvez commencer à créer un segment multi-entités. Cela peut être fait à l’aide de l’API de segmentation ou de l’interface utilisateur du créateur de segments. Pour plus d’informations, veuillez choisir l’un des guides suivants :

* [Création d’un segment à l’aide de l’API de segmentation](./tutorials/create-a-segment.md)
* [Création d’un segment à l’aide de l’interface utilisateur du créateur de segments](./ui/overview.md)

## Évaluation et accès aux segments multientités

Après avoir créé un segment, vous pouvez évaluer les résultats du segment et y accéder à l’aide de l’API de segmentation. L’évaluation d’un segment à entités multiples est très similaire à l’évaluation d’un segment standard. Ce processus ne peut être effectué qu’à l’aide de l’API de segmentation. Pour obtenir un guide détaillé expliquant comment utiliser l’API pour évaluer les segments et y accéder, consultez la page [évaluation et accès aux segments](./tutorials/evaluate-a-segment.md) tutoriel.
