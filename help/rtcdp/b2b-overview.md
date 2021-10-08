---
keywords: RTCDP;CDP;Édition B2B;Real-time Customer Data Platform;plateforme de données client en temps réel;cdp en temps réel;b2b;cdp;Customer AI
title: Présentation de l’édition B2B de la plateforme CDP en temps réel
seo-title: Real-time Customer Data Platform B2B Edition overview
description: Présentation du compte de l’édition B2B de Real-time Customer Data Platform
seo-description: Overview of Real-time Customer Data Platform B2B Edition Account
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: 6b582683483046efaf880e46e33d7f30a44a61bf
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 3%

---

# Présentation de Real-time Customer Data Platform B2B Edition

>[!IMPORTANT]
>
>La plateforme CDP B2B en temps réel est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

Basée sur la plateforme de données clients en temps réel de Real-time Customer Data Platform, l’édition B2B de la plateforme de données clients en temps réel est conçue spécifiquement pour les marketeurs qui utilisent un modèle de service business-to-business. Il rassemble des données provenant de plusieurs sources et les combine dans une vue unique des personnes et des profils de compte. Ces données unifiées permettent aux marketeurs de cibler précisément des audiences spécifiques et d’interagir avec celles-ci sur tous les canaux disponibles.

Il existe des améliorations à diverses fonctionnalités Adobe Experience Platform qui distinguent l’édition B2B de la plateforme CDP en temps réel de son homologue B2C. Ils incluent des améliorations du modèle de données d’expérience (XDM) pour les cas d’utilisation B2B, des mises à niveau de la résolution des identités et de la segmentation des profils, ainsi qu’un connecteur et une destination personnalisés pour [!DNL Marketo Engage]. Le connecteur [!DNL Marketo] permet aux marques B2B de connecter leurs données d’engagement B2B leaders du secteur à des informations comportementales afin d’alimenter les pistes et d’améliorer les opérations marketing basées sur les comptes.

Avec la plateforme CDP B2B en temps réel, vous pouvez :

* Combinez les données collectées à partir de plusieurs sources dans une vue unique afin de créer des personnes et des profils de compte holistiques.
* Enrichissez, segmentez et exportez toutes vos données intersources à partir d’un magasin centralisé de profils de compte unifiés.
* Gérez vos données à l’aide d’outils de gouvernance des données disponibles à chaque étape du processus de centralisation afin de vous assurer que vos données sont conformes aux réglementations légales et aux politiques commerciales.

Vous trouverez ci-dessous des informations plus détaillées sur les améliorations apportées à l’édition B2B de la plateforme CDP en temps réel.

## XDM

La plateforme CDP B2B en temps réel fournit plusieurs nouvelles classes de schémas XDM, groupes de champs et types de relations pour capturer et structurer vos données spécifiquement à des fins B2B. Consultez la présentation de [XDM dans l’édition B2B de la plateforme CDP en temps réel](./schemas/b2b.md) pour une ventilation de chacune de ces améliorations.

En utilisant des schémas B2B préconfigurés, vous pouvez importer les données dans une structure standardisée et exploitable. La plupart des nouvelles classes de schéma sont mappées presque directement à celles rencontrées dans les CRM standard, comme [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo] et d’autres sources de données B2B. Avec la plateforme CDP B2B en temps réel, vous pouvez importer des données de sources B2B dans Platform de manière simple et avec des résultats faciles à contrôler.

Ces améliorations XDM vous permettent de mieux ingérer et activer des données par le biais de sources et de destinations axées sur B2B, ce qui améliore l’unification et la présentation des données pour des cas d’utilisation plus variés et plus flexibles.

## Résolution des identités

Une fois les schémas définis et les données ingérées conformes à ces schémas, la plateforme CDP B2B Edition en temps réel identifie les enregistrements sources qui représentent les personnes et les entreprises du monde réel grâce à un puissant système de résolution d’identité en temps réel.

Le système de résolution des identités offre les fonctionnalités suivantes :

* Enregistrements combinés des personnes B2B et B2C
* Une hiérarchie de comptes à plusieurs niveaux
* Connexions de plusieurs à plusieurs personnes à un compte
* Les personnes et les identités de compte sont résolues en temps réel.

Le système de résolution des identités a été développé pour prendre en charge une classification plus multiforme des personnes. Le système permet d’identifier les personnes comme des prospects dans les opportunités commerciales ainsi que dans les clients.

Les enregistrements de compte synchronisés par le CRM source et connectés via plusieurs chemins dans le système sont fusionnés par Platform. Le système rassemble les personnes associées aux opportunités commerciales et celles enregistrées en tant que clients, mais peut également préserver la distinction entre elles en tant qu’attribut si elles sont identifiables.

Les identifiants correspondants sont utilisés pour lier et fusionner les enregistrements de compte de plusieurs systèmes. Les hiérarchies de compte sont conservées tout au long de ce processus. Les différentiateurs sont utilisés pour vérifier si une personne est associée ou non à un compte, et offrir la possibilité de les séparer du compte si nécessaire.

## Profils et segmentation

Une fois que la plateforme CDP B2B en temps réel a ingéré des données et résolu des identités liées aux personnes, aux entreprises, aux attributs et aux comportements, ces données sont utilisées pour créer des profils. Ces profils peuvent ensuite être segmentés en audiences pouvant être activées vers différentes destinations.

Lorsqu’il est correctement mis en oeuvre, le système effectue le suivi des personnes à l’aide d’identifiants Principaux uniques plutôt que d’attributs pouvant changer, tels que les adresses électroniques. Cela signifie que lorsque quelqu’un change de tâche, le système les suit toujours. La personne est toujours la même entité, mais elle est liée à un nouveau compte. Cette fonctionnalité native offre un excellent vecteur d’extension vers de nouveaux comptes, car le système suit ces personnes en tant qu’individus comprenant tous leurs attributs et comportements.

## Sources B2B

Platform permet d’ingérer des données à partir de sources externes tout en vous permettant de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform. La source [!DNL Marketo] vous permet de diffuser des données B2B dans Platform et de maintenir ces données à jour à l’aide d’applications connectées à Platform. Il prend en charge un certain nombre d’instances de [!DNL Marketo] (ce qui est bénéfique pour les grandes entreprises avec plusieurs instances) et s’insère dans une seule organisation IMS où les données sont fusionnées.

>[!NOTE]
>
>La source [!DNL Marketo] n’est **pas** requise pour utiliser l’édition B2B de la plateforme CDP en temps réel.

Pour plus d’informations sur Marketo et l’introduction de données B2B dans Platform, consultez la documentation [sources dans la plateforme CDP B2B en temps réel Edition](./sources/b2b.md) .

## Destinations B2B

Les destinations Experience Platform telles que Google, Linkedin et Facebook sont disponibles et entièrement prises en charge par l’édition B2B de la plateforme CDP en temps réel. Il existe également une destination de Marketo Engage qui diffuse les données d’adhésion au segment en dehors de Platform et les rend disponibles sous forme de listes dans Marketo.

Pour les entreprises disposant de plusieurs systèmes de gestion de la relation client, l’édition B2B de la plateforme CDP en temps réel permet de configurer les connecteurs de destination pour séparer les instances de Marketo ou de la gestion de la relation client. Si nécessaire, vous pouvez configurer les connecteurs de destination pour chaque instance et envoyer des audiences à chacune des instances CRM indépendamment.

## Étapes suivantes

Maintenant que vous comprenez mieux les avantages offerts aux marketeurs par l’édition B2B de la plateforme CDP en temps réel et les différences entre cette dernière et la plateforme CDP en temps réel, vous pouvez découvrir comment appliquer ces fonctionnalités à votre propre organisation IMS.

Pour comprendre comment l’édition B2B de la plateforme CDP en temps réel peut bénéficier à votre modèle de service business-to-business, reportez-vous à l’ [exemple d’utilisation de la plateforme CDP en temps réel B2B Edition](./b2b-use-case.md). Vous pouvez également vous reporter à la documentation [schémas dans Real-time Customer Data Platform B2B Edition](./schemas/b2b.md) pour obtenir des instructions plus spécifiques sur la création de schémas et la définition de relations pour les entités de données B2B essentielles.
