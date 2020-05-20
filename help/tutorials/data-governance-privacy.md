---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Didacticiels sur la gouvernance des données et la confidentialité
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# Didacticiels sur la gouvernance des données et la confidentialité

L’étiquetage et l’application de l’utilisation des données (DULE) constituent le mécanisme de base de la gouvernance des données de la plate-forme Adobe Experience. Les fonctions DULE permettent d&#39;appliquer des étiquettes d&#39;utilisation des données aux jeux de données et aux champs, en les classant en fonction des stratégies d&#39;utilisation des données associées. Avant de commencer à utiliser les étiquettes, consultez la présentation [de la gouvernance des](../data-governance/home.md) données pour une présentation plus robuste de la structure DULE dans Platform.

Adobe Experience Platform Privacy Service fournit une API RESTful et une interface utilisateur qui vous permettent de coordonner les demandes de confidentialité et de conformité entre les différentes solutions. Pour en savoir plus, veuillez commencer par lire la présentation [du Service de](../privacy-service/home.md)protection des renseignements personnels.

## Ajouter étiquettes d’utilisation des données

Les étiquettes d’utilisation des données vous permettent de classer les jeux de données et les champs en fonction des stratégies d’utilisation qui s’appliquent à ces données. Les étiquettes peuvent être appliquées à tout moment, ce qui vous permet de gérer les données avec souplesse. Les meilleures pratiques encouragent l’étiquetage des données dès qu’elles sont incorporées dans la plate-forme d’expérience ou dès que les données deviennent disponibles pour une utilisation dans la plate-forme. Les étiquettes d’utilisation des données appliquées au niveau du jeu de données sont propagées à tous les champs du jeu de données. Les étiquettes peuvent également être appliquées directement à des champs individuels (en-têtes de colonne) dans un jeu de données, sans propagation. Pour savoir comment appliquer des étiquettes d&#39;utilisation de données à vos données, consultez la présentation [des étiquettes d&#39;utilisation de](../data-governance/labels/overview.md)données.

## Création de stratégies d’utilisation des données

L&#39;API DULE Policy Service vous permet de créer et de gérer des stratégies DULE afin de déterminer les actions marketing à entreprendre par rapport aux données contenant certains libellés DULE. Pour commencer, lisez la présentation [des stratégies d’utilisation des](../data-governance/policies/overview.md)données.

## Appliquer les stratégies d’utilisation des données

Une fois que vous avez créé des étiquettes d’application et d’étiquetage d’utilisation des données (DULE) pour vos données et créé des stratégies DULE pour les actions marketing sur ces étiquettes, vous pouvez utiliser l’API DULE Policy Service pour évaluer si une action marketing effectuée sur un jeu de données, ou un groupe arbitraire d’étiquettes DULE, constitue une violation de stratégie. Vous pouvez ensuite configurer vos propres protocoles internes pour gérer les violations de stratégie en fonction de la réponse de l’API. Pour commencer, consultez l’aperçu [de l’application des](../data-governance/enforcement/overview.md)stratégies.

## Appliquer la conformité à l’utilisation des données pour un segment d’audience

Les segments qui sont activés pour une utilisation dans le Profil client en temps réel contiennent un identifiant de stratégie de fusion dans leur définition de segment. Cette stratégie de fusion contient des informations sur les jeux de données à inclure dans le segment, qui contiennent à leur tour les étiquettes d’utilisation des données applicables. Pour connaître les étapes spécifiques à l&#39;application de la conformité à l&#39;utilisation des données pour un segment d&#39;audience, suivez le tutoriel d&#39;application de la conformité à l&#39;utilisation des [données pour les segments](../segmentation/tutorials/governance.md).

## Commencer avec Privacy Service

Privacy Service fournit une API RESTful et une interface utilisateur qui vous permettent de gérer les données personnelles de vos sujets de données (clients) dans les applications Adobe Experience Cloud. Privacy Service fournit également un mécanisme central d’audit et de consignation qui vous permet d’accéder à l’état et aux résultats des tâches impliquant des applications Experience Cloud. Pour obtenir des instructions sur la création et le suivi des tâches de Privacy Service, suivez les étapes fournies dans le guide [de développement](../privacy-service/api/getting-started.md) Privacy Service ou le guide [d’utilisateur](../privacy-service/ui/overview.md)Privacy Service.