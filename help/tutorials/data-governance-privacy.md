---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Didacticiels sur la gouvernance des données et la confidentialité
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# Didacticiels sur la gouvernance des données et la confidentialité

L’étiquetage et l’application de l’utilisation des données (DULE) constituent le mécanisme de base de la gouvernance des données d’Adobe Experience Platform. Les fonctionnalités DULE vous permettent d’appliquer des libellés d’utilisation des données aux jeux de données et aux champs, en les classant en fonction des stratégies d’utilisation des données associées. Avant de commencer avec les étiquettes, reportez-vous à la présentation [de la gouvernance des](../data-governance/home.md) données pour une présentation plus robuste de la structure DULE dans Platform.

Le service de confidentialité d’Adobe Experience Platform fournit une API RESTful et une interface utilisateur qui vous permettent de coordonner les demandes de confidentialité et de conformité entre différentes solutions. Pour en savoir plus, veuillez commencer par lire l’aperçu [du Service de](../privacy-service/home.md)protection des renseignements personnels.

## Ajouter des étiquettes d’utilisation des données

Les étiquettes d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Les étiquettes peuvent être appliquées à tout moment, ce qui offre une certaine souplesse quant à la manière dont vous décidez de gérer les données. Les bonnes pratiques encouragent l’étiquetage des données dès qu’elles sont assimilées à une plateforme d’expérience ou dès que les données deviennent disponibles pour une utilisation dans la plateforme. Les étiquettes d’utilisation des données appliquées au niveau du jeu de données sont propagées à tous les champs du jeu de données. Les étiquettes peuvent également être appliquées directement à des champs individuels (en-têtes de colonne) d’un jeu de données, sans propagation. Pour savoir comment appliquer des étiquettes d’utilisation des données à vos données, consultez la présentation [des étiquettes d’utilisation des](../data-governance/labels/overview.md)données.

## Création de stratégies d’utilisation des données

L’API DULE Policy Service vous permet de créer et de gérer des stratégies DULE afin de déterminer quelles actions marketing peuvent être entreprises par rapport aux données qui contiennent certaines étiquettes DULE. Pour commencer, lisez la présentation [des stratégies d’utilisation des](../data-governance/policies/overview.md)données.

## Appliquer les stratégies d’utilisation des données

Une fois que vous avez créé des étiquettes d’application et d’étiquetage d’utilisation des données (DULE) pour vos données et que vous avez créé des stratégies DULE pour les actions marketing contre ces étiquettes, vous pouvez utiliser l’API DULE Policy Service pour évaluer si une action marketing effectuée sur un jeu de données, ou un groupe arbitraire de libellés DULE, constitue une violation de stratégie. Vous pouvez ensuite configurer vos propres protocoles internes pour gérer les violations de stratégie en fonction de la réponse de l’API. Pour commencer, consultez la présentation [de l’application des](../data-governance/enforcement/overview.md)stratégies.

## Appliquer la conformité d’utilisation des données à un segment  

Les segments qui sont activés pour une utilisation dans le de clients en temps réel contiennent un ID de stratégie de fusion dans leur définition de segment. Cette stratégie de fusion contient des informations sur les jeux de données à inclure dans le segment, qui à son tour contiennent les étiquettes d’utilisation de données applicables. Pour connaître les étapes spécifiques à l’application de la conformité à l’utilisation des données pour un segment  de , suivez le didacticiel sur l’application de la conformité à l’utilisation des [données pour les segments](../segmentation/tutorials/governance.md).

## Commencer avec Privacy Service

Privacy Service fournit une API RESTful et une interface utilisateur qui vous permettent de gérer les données personnelles de vos personnes (clients) dans les applications Adobe Experience Cloud. Privacy Service fournit également un mécanisme central d’audit et de journalisation qui vous permet d’accéder à l’état et aux résultats des tâches impliquant des applications Experience Cloud. Pour obtenir des instructions sur la création et le suivi des tâches du service de confidentialité, suivez les étapes fournies dans le guide [du développeur du service de](../privacy-service/api/getting-started.md) confidentialité ou le guide [de l’utilisateur du service de](../privacy-service/ui/overview.md)confidentialité.