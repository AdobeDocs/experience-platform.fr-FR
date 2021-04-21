---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Tutoriels sur la gouvernance et la confidentialité des données
topic-legacy: tutorial
type: Tutorial
description: Ce document présente un aperçu des différents didacticiels disponibles relatifs à la gouvernance des données Adobe Experience Platform et au Adobe Experience Platform Privacy Service.
exl-id: c3cef447-b343-445b-a3ed-54f873f6dfb9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 50%

---

# [!DNL Data Governance] et  [!DNL Privacy] Tutorials

La gouvernance des données Adobe Experience Platform vous permet d’appliquer des étiquettes d’utilisation des données aux jeux de données et aux champs, de les classer en fonction des stratégies d’utilisation des données associées et d’évaluer les violations de stratégies lorsque certaines actions sont effectuées sur ces jeux de données et/ou ces champs. Avant de commencer à utiliser les didacticiels répertoriés dans ce document, consultez la section [[!DNL Data Governance] présentation](../data-governance/home.md) pour une présentation plus robuste du cadre.

Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface utilisateur qui vous permettent de coordonner les demandes de confidentialité et de conformité entre les différentes solutions. Pour en savoir plus, commencez par lire la [présentation de Privacy Service](../privacy-service/home.md).

## Ajout de libellés d’utilisation des données

Les libellés d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Vous pouvez appliquer les libellés à tout moment, ce qui vous offre une certaine flexibilité quant à la manière dont vous choisissez de gérer les données. Les meilleures pratiques encouragent l’étiquetage des données dès qu’elles sont ingérées dans [!DNL Experience Platform] ou dès que les données sont disponibles pour être utilisées dans [!DNL Platform]. Les libellés d’utilisation des données appliqués au niveau du jeu de données sont propagés à tous les champs du jeu de données. Vous pouvez également appliquer les libellés directement sur des champs individuels (en-têtes de colonne) d’un jeu de données, sans propagation. Pour apprendre à appliquer des libellés d’utilisation des données à vos données, consultez la [présentation des libellés d’utilisation des données](../data-governance/labels/overview.md).

## Création de stratégies d’utilisation des données

L&#39;API [!DNL Policy Service] vous permet de créer et de gérer des stratégies d&#39;utilisation des données afin de déterminer quelles actions marketing peuvent être entreprises par rapport aux données contenant certains libellés d&#39;utilisation. Pour commencer, lisez la [présentation des stratégies d’utilisation des données](../data-governance/policies/overview.md).

## Application des stratégies d’utilisation des données

Une fois que vous avez ajouté des étiquettes d’utilisation pour vos données et créé des stratégies pour les actions marketing à l’égard de ces étiquettes, vous pouvez utiliser [!DNL Policy Service API] pour déterminer si une action marketing constitue une violation de stratégie lorsqu’elle est exécutée sur un jeu de données ou un groupe arbitraire de libellés d’utilisation. Vous pouvez ensuite configurer vos propres protocoles internes pour gérer les violations de stratégie en fonction de la réponse de l’API. Pour commencer, consultez la [présentation de l’application des stratégies](../data-governance/enforcement/overview.md).

## Application de la conformité de l’utilisation des données pour un segment ciblé

Les segments qui sont activés pour une utilisation dans [!DNL Real-time Customer Profile] contiennent un ID de stratégie de fusion dans leur définition de segment. Cette stratégie de fusion contient des informations sur les jeux de données à inclure dans le segment, qui à leur tour contiennent les libellés d’utilisation de données applicables. Pour connaître les étapes spécifiques à l’application de la conformité de l’utilisation des données pour un segment ciblé, suivez le [tutoriel sur l’application de la conformité de l’utilisation des données pour les segments](../segmentation/tutorials/governance.md).

## Prise en main d’[!DNL Privacy Service]

[!DNL Privacy Service] fournit une API RESTful et une interface utilisateur qui vous permettent de gérer les données personnelles de vos titulaires de données (clients) dans les applications Adobe Experience Cloud. [!DNL Privacy Service] fournit aussi un mécanisme central d’audit et de connexion qui vous permet d’accéder à l’état et aux résultats des tâches impliquant des applications [!DNL Experience Cloud] Pour obtenir des instructions sur la création et le suivi des tâches [!DNL Privacy Service], suivez les étapes fournies dans le [guide du développeur Privacy Service](../privacy-service/api/getting-started.md) ou le [guide de l&#39;utilisateur Privacy Service](../privacy-service/ui/overview.md).
