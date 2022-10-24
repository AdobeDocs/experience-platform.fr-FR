---
keywords: RTCDP;CDP;Édition B2B;Real-time Customer Data Platform;plateforme de données client en temps réel;cdp en temps réel;b2b;cdp;Customer AI
title: Présentation de l’édition B2B de Real-Time CDP
description: Présentation du compte de l’édition B2B de Real-time Customer Data Platform
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 59%

---

# Présentation de Real-time Customer Data Platform B2B Edition

Basée sur Adobe Real-time Customer Data Platform (Real-Time CDP), Real-Time CDP B2B Edition est conçue spécifiquement pour les spécialistes du marketing qui opèrent dans un modèle de service business-to-business. Elle rassemble des données provenant de sources multiples et les combine en une vue unique des profils de comptes et d’utilisateurs. Ces données unifiées permettent aux professionnels du marketing de cibler précisément des audiences spécifiques afin de stimuler leur engagement sur tous les canaux disponibles.

Il existe des améliorations à diverses fonctionnalités de Adobe Experience Platform qui distinguent Real-Time CDP Édition B2B de son homologue B2C. Il s’agit notamment d’améliorations du modèle de données d’expérience (XDM) pour les cas d’utilisation B2B, de mises à niveau de la résolution d’identité et de la segmentation de profil, ainsi que d’un connecteur et d’une destination personnalisés pour [!DNL Marketo Engage]. Le connecteur [!DNL Marketo] permet aux marques B2B de connecter ses données d’engagement B2B de pointe aux informations comportementales afin d’encourager les prospects et d’améliorer les opérations marketing basées sur les comptes.

Avec Real-Time CDP B2B Edition, vous pouvez :

* Combiner les données collectées à partir de plusieurs sources en une seule vue afin de créer des profils de comptes et d’utilisateurs holistiques.
* Enrichir, segmenter et exporter toutes vos données inter-sources à partir d’un magasin centralisé de profils de comptes unifiés.
* Gérer vos données à l’aide d’outils de gouvernance des données mis à votre disposition à chaque étape du processus de centralisation. Cela garantit que vos données sont conformes aux réglementations légales et aux stratégies commerciales.

Vous trouverez ci-dessous des informations plus détaillées sur les améliorations apportées à Real-Time CDP B2B Edition.

## XDM

Real-Time CDP Édition B2B fournit plusieurs nouvelles classes de schéma XDM, groupes de champs et types de relations pour capturer et structurer vos données spécifiquement à des fins B2B. Consultez la présentation sur [XDM dans l’édition B2B de Real-Time CDP](./schemas/b2b.md) pour une ventilation de chacune de ces améliorations.

En utilisant des schémas B2B préconfigurés, vous pouvez importer des données dans une structure standardisée et exploitable. Parmi les nouvelles classes de schéma, un grand nombre correspond presque directement à celles que l’on trouve dans des systèmes de gestion de la relation client (CRM) classiques tels que [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo] et d’autres sources de données B2B. Avec l’édition B2B de Real-Time CDP, vous pouvez importer les données de sources B2B dans Platform de manière simple et avec des résultats faciles à contrôler.

Ces améliorations apportées à XDM optimisent l’ingestion et l’activation de données via des sources et des destinations centrées sur le B2B, améliorant ainsi l’unification et la présentation des données pour des cas d’utilisation plus variés et plus flexibles.

## Résolution d’identité

Une fois les schémas définis et les données ingérées conformes à ces schémas, Real-Time CDP B2B Edition identifie les enregistrements sources qui représentent les personnes et les entreprises du monde réel grâce à un puissant système de résolution d’identité en temps réel.

Le système de résolution d’identité propose les fonctionnalités suivantes :

* Enregistrements d’utilisateurs B2B et B2C combinés
* Une hiérarchie de comptes à plusieurs niveaux
* Connexions entre plusieurs utilisateurs et entre des utilisateurs et des comptes
* Les identités des utilisateurs et des comptes sont résolues en temps réel.

Le système de résolution d’identité a été étendu pour prendre en charge une classification des utilisateurs plus diversifiée. Le système permet d’identifier les utilisateurs en tant que prospects dans le cadre d’opportunités commerciales mais également en tant que clients.

Les enregistrements de comptes synchronisés par le système de gestion de la relation client (CRM) source et connectés via plusieurs chemins d’accès au sein du système sont fusionnés par Platform. Le système regroupe les utilisateurs associés aux opportunités commerciales et ceux enregistrés en tant que clients, mais est également capable de préserver la distinction entre eux en tant qu’attribut s’ils sont identifiables.

Les identifiants correspondants sont utilisés pour relier et fusionner les enregistrements de comptes provenant de plusieurs systèmes. Les hiérarchies de comptes sont préservées tout au long de ce processus. Des différenciateurs sont utilisés pour vérifier si un utilisateur est associé à un compte ou non. Ils permettent également de séparer l’utilisateur du compte, si nécessaire.

## Profils et segmentation

Une fois que Real-Time CDP B2B Edition a ingéré des données et résolu des identités liées aux personnes, aux entreprises, aux attributs et aux comportements, ces données sont utilisées pour créer des profils. Ces profils peuvent ensuite être segmentés en audiences navigables qui peuvent par la suite être activées vers diverses destinations.

Lorsqu’il est implémenté correctement, le système permet de suivre les utilisateurs à l’aide d’identifiants principaux uniques plutôt que d’attributs susceptibles de changer, comme les adresses e-mail. Cela signifie que lorsqu’un utilisateur change d’emploi, le système continue de le suivre. L’utilisateur correspond toujours à la même entité, mais il est lié à un nouveau compte. Cette fonctionnalité native offre un excellent vecteur d’expansion vers de nouveaux comptes, car le système suit ces utilisateurs en tant qu’individus, ce qui inclut tous leurs attributs et comportements.

## Sources B2B

Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. La source [!DNL Marketo] vous permet de diffuser des données B2B en continu dans Platform et de maintenir ces données à jour à l’aide d’applications connectées à Platform. Elle prend en charge un nombre illimité d’instances [!DNL Marketo] (ce qui est avantageux pour les grandes entreprises ayant de multiples instances) et effectue une extraction vers une seule organisation IMS, où les données sont fusionnées.

>[!NOTE]
>
>Le [!DNL Marketo] la source est **not** requis pour utiliser l’édition B2B de Real-Time CDP.

Voir [sources dans Real-Time CDP B2B Edition](./sources/b2b.md) documentation pour plus d’informations sur Marketo et l’introduction de données B2B dans Platform.

## Destinations B2B

Les destinations Experience Platform telles que Google Customer Match, Facebook, LinkedIn, Marketo Engage, Amazon S3, Google Display &amp; Video 360, Google Ads et Google Ad Manager sont disponibles et entièrement prises en charge par Real-Time CDP Édition B2B. La destination de Marketo Engage diffuse également les données d’adhésion aux segments en dehors de Platform et les rend disponibles sous forme de listes dans Marketo.

Consultez la présentation de la [Destination de Marketo Engage](../destinations/catalog/adobe/marketo-engage.md) pour plus d’informations.

Pour les entreprises disposant de plusieurs CRM, l’édition B2B de Real-Time CDP permet de configurer les connecteurs de destination pour séparer les instances de Marketo ou de CRM. Si nécessaire, vous pouvez configurer des connecteurs de destinations pour chaque instance et envoyer des audiences à chacune des instances CRM de manière indépendante.

## Étapes suivantes

Maintenant que vous comprenez mieux les avantages offerts aux marketeurs par l’édition B2B de Real-Time CDP et les différences entre cette dernière et Real-Time CDP, vous pouvez découvrir comment appliquer ces fonctionnalités à votre propre organisation IMS.

Pour comprendre comment Real-Time CDP B2B Edition peut bénéficier à votre modèle de service business-to-business, consultez la documentation suivante pour vous aider à démarrer :

* [Exemple de cas d’utilisation de Real-Time CDP B2B Edition](./b2b-use-case.md)
* [Tutoriel complet de Real-time Customer Data Platform Édition B2B](./b2b-tutorial.md)
* [Envoi de données](./sources/b2b.md)
* [Accès aux profils](./profile/profile-overview.md)
* [Schémas dans Real-time Customer Data Platform version B2B](./schemas/b2b.md)
* [Création de segments](./segmentation/b2b.md)
* [Activation de segments vers des destinations](./destinations/b2b.md)
* [Définition et application des stratégies de gouvernance des données](./privacy/data-governance-overview.md)
