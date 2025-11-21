---
keywords: RTCDP;CDP;Édition B2B;Real-time Customer Data Platform;real time customer data platform;real time cdp;b2b;cdp;IA dédiée aux clients
title: Présentation de l’édition B2B de Real-time CDP
description: Présentation du compte de l’édition B2B de Real-Time Customer Data Platform
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 85%

---

# Présentation de l’édition B2B de Real-time Customer Data Platform

Basée sur Real-time Customer Data Platform (Real-time CDP), l’édition B2B de Real-time CDP a été conçue pour les spécialistes du marketing travaillant sur un modèle de service business-to-business. Elle rassemble des données provenant de sources multiples et les combine en une vue unique des profils de comptes et d’utilisateurs. Ces données unifiées permettent aux spécialistes marketing de cibler précisément des audiences spécifiques afin de stimuler leur engagement sur tous les canaux disponibles.

Des améliorations ont été apportées à diverses fonctionnalités d’Adobe Experience Platform, distinguant ainsi l’édition B2B de Real-time CDP de son équivalent B2C. Il s’agit notamment d’améliorations du modèle de données d’expérience (XDM) pour les cas d’utilisation B2B, de mises à niveau de la résolution d’identité et de la segmentation de profil, ainsi que d’un connecteur et d’une destination personnalisés pour [!DNL Marketo Engage]. Le connecteur [!DNL Marketo] permet aux marques B2B de connecter ses données d’engagement B2B de pointe aux informations comportementales afin d’encourager les prospects et d’améliorer les opérations marketing basées sur les comptes.

Avec l’édition B2B de Real-time CDP, vous pouvez :

* Combiner les données collectées à partir de plusieurs sources en une seule vue afin de créer des profils de comptes et d’utilisateurs holistiques.
* Enrichir, segmenter et exporter toutes vos données inter-sources à partir d’un magasin centralisé de profils de comptes unifiés.
* Gérer vos données à l’aide d’outils de gouvernance des données mis à votre disposition à chaque étape du processus de centralisation. Cela garantit que vos données sont conformes aux réglementations légales et aux politiques commerciales.

Des détails plus complets sur les améliorations apportées à l’édition B2B de Real-time CDP sont divisés en sections indiquées ci-dessous.

## XDM

L’édition B2B de Real-time CDP fournit plusieurs nouvelles classes de schémas XDM, des groupes de champs et des types de relations pour capturer et structurer vos données spécifiquement à des fins B2B. Consultez la présentation sur [XDM dans l’édition B2B de Real-time CDP](./schemas/b2b.md) pour obtenir une explication détaillée de chacune de ces améliorations.

En utilisant des schémas B2B préconfigurés, vous pouvez importer des données dans une structure standardisée et exploitable. Parmi les nouvelles classes de schéma, un grand nombre correspond presque directement à celles que l’on trouve dans des systèmes de gestion de la relation client (CRM) classiques tels que [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo] et d’autres sources de données B2B. Avec Real-Time CDP B2B edition, vous pouvez importer des données provenant de sources B2B dans Experience Platform de manière simple et avec des résultats faciles à auditer.

Ces améliorations apportées à XDM optimisent l’ingestion et l’activation de données via des sources et des destinations centrées sur le B2B, améliorant ainsi l’unification et la présentation des données pour des cas d’utilisation plus variés et plus flexibles.

## Résolution d’identité

Une fois les schémas définis et les données ingérées conformément à ces schémas, l’édition B2B de Real-time CDP identifie les enregistrements sources qui représentent des personnes et des entreprises réels grâce à un puissant système de résolution d’identité en temps réel.

Le système de résolution d’identité propose les fonctionnalités suivantes :

* Enregistrements d’utilisateurs B2B et B2C combinés
* Une hiérarchie de comptes à plusieurs niveaux
* Connexions entre plusieurs utilisateurs et entre des utilisateurs et des comptes
* Les identités des utilisateurs et des comptes sont résolues en temps réel.

Le système de résolution d’identité a été étendu pour prendre en charge une classification des utilisateurs plus diversifiée. Le système permet d’identifier les utilisateurs en tant que prospects dans le cadre d’opportunités commerciales mais également en tant que clients.

Les enregistrements de comptes synchronisés par le système de gestion de la relation client (CRM) source et connectés via plusieurs chemins d’accès au sein du système sont fusionnés par Experience Platform. Le système regroupe les utilisateurs associés aux opportunités commerciales et ceux enregistrés en tant que clients, mais est également capable de préserver la distinction entre eux en tant qu’attribut s’ils sont identifiables.

Les identifiants correspondants sont utilisés pour relier et fusionner les enregistrements de comptes provenant de plusieurs systèmes. Les hiérarchies de comptes sont préservées tout au long de ce processus. Des différenciateurs sont utilisés pour vérifier si un utilisateur est associé à un compte ou non. Ils permettent également de séparer l’utilisateur du compte, si nécessaire.

## Profils et segmentation

Une fois les données ingérées et les identités liées aux personnes, aux entreprises, aux attributs et aux comportements résolues par l’édition B2B de Real-time CDP, ces données sont utilisées pour générer des profils. Ces profils peuvent ensuite être segmentés en audiences navigables qui peuvent par la suite être activées vers diverses destinations.

Lorsqu’il est implémenté correctement, le système permet de suivre les utilisateurs à l’aide d’identifiants principaux uniques plutôt que d’attributs susceptibles de changer, comme les adresses e-mail. Cela signifie que lorsqu’un utilisateur change d’emploi, le système continue de le suivre. L’utilisateur correspond toujours à la même entité, mais il est lié à un nouveau compte. Cette fonctionnalité native offre un excellent vecteur d’expansion vers de nouveaux comptes, car le système suit ces utilisateurs en tant qu’individus, ce qui inclut tous leurs attributs et comportements.

## Sources B2B

Experience Platform permet d’ingérer des données à partir de sources externes tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform. La source [!DNL Marketo] vous permet de diffuser des données B2B en continu dans Experience Platform et de maintenir ces données à jour à l’aide d’applications connectées à Experience Platform. Il prend en charge un nombre illimité d’instances [!DNL Marketo] (ce qui est avantageux pour les grandes entreprises ayant de multiples instances) et effectue une extraction vers une seule organisation , où les données sont fusionnées.

>[!NOTE]
>
>La source [!DNL Marketo] n’est **pas** nécessaire à l’utilisation de l’édition B2B de Real-time CDP.

Consultez la documentation [sources dans Real-Time CDP B2B edition](./sources/b2b.md) pour plus d’informations sur Marketo et sur l’importation de données B2B dans Experience Platform.

## Destinations B2B

Les destinations d’Experience Platform telles que Google Customer Match, Facebook, LinkedIn, Marketo Engage, Amazon S3, Google Display &amp; Video 360, Google Ads et Google Ad Manager sont disponibles et entièrement prises en charge par l’édition B2B de Real-time CDP. La destination Marketo Engage diffuse également les données d’appartenance aux segments en dehors d’Experience Platform et les rend disponibles sous forme de listes dans Marketo.

Consultez la présentation de la [Destination de Marketo Engage](../destinations/catalog/adobe/marketo-engage.md) pour plus d’informations.

Pour les entreprises disposant de plusieurs CRM, l’édition B2B de Real-time CDP offre la possibilité de configurer des connecteurs de destinations vers des instances distinctes de Marketo ou de CRM. Si nécessaire, vous pouvez configurer des connecteurs de destinations pour chaque instance et envoyer des audiences à chacune des instances CRM de manière indépendante.

## Étapes suivantes

Vous avez désormais une meilleure compréhension des avantages offerts par l’édition B2B de Real-time CDP aux spécialistes du marketing et vous connaissez les différences entre cette édition et Real-time CDP. Découvrez maintenant comment appliquer ces fonctionnalités à votre propre organisation.

Pour comprendre comment l’édition B2B de Real-time CDP peut bénéficier à votre modèle de service business-to-business, consultez la documentation suivante pour vous aider à démarrer :

* [Exemple de cas d’utilisation pour l’édition B2B de Real-time CDP](./b2b-use-case.md)
* [Un tutoriel de bout en bout sur l’édition B2B de Real-time Customer Data Platform](./b2b-tutorial.md)
* [Envoi de données](./sources/b2b.md)
* [Accès aux profils](./profile/profile-overview.md)
* [Schémas dans l’édition B2B de Real-time Customer Data Platform](./schemas/b2b.md)
* [Création d’audiences](./segmentation/b2b.md)
* [Activation des audiences vers des destinations](./destinations/b2b.md)
* [Définition et application des politiques de gouvernance des données](./privacy/data-governance-overview.md)
