---
keywords: Experience Platform;modèle d’apprentissage automatique;Data Science Workspace;profil client en temps réel;rubriques populaires;insights d’apprentissage automatique
solution: Experience Platform
title: Enrichissement de Real-time Customer Profile avec des insights d’apprentissage automatique
topic-legacy: tutorial
type: Tutorial
description: Ce document fournit un guide sur la manière d’enrichir Real-time Customer Profile avec des insights d’apprentissage automatique.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 27%

---

# Enrichir [!DNL Real-time Customer Profile] avec des insights d’apprentissage automatique

Adobe Experience Platform [!DNL Data Science Workspace] fournit les outils et les ressources nécessaires pour créer, évaluer et utiliser des modèles d’apprentissage automatique afin de générer des prédictions et des insights sur les données. Lorsque des insights d’apprentissage automatique sont ingérés dans un jeu de données activé par [!DNL Profile], ces mêmes données sont également ingérées sous la forme d’enregistrements [!DNL Profile] qui peuvent ensuite être segmentés à l’aide de [!DNL Adobe Experience Platform Segmentation Service]. À mesure que les données de profil et de série temporelle sont ingérées, Real-time Customer Profile décide automatiquement d’inclure ou d’exclure ces données des segments par le biais d’un processus continu appelé la segmentation par flux, avant de les fusionner avec les données existantes et de mettre à jour la vue d’union. Par conséquent, vous pouvez instantanément effectuer des calculs et prendre des décisions pour offrir aux clients de meilleures expériences personnalisées lorsqu’ils interagissent avec votre marque.

Ce document fournit des liens vers des tutoriels qui vous permettent d’enrichir [!DNL Real-time Customer Profile] avec vos insights d’apprentissage automatique.

## Prise en main

Pour suivre les tutoriels ci-dessous, vous devez maîtriser l’ingestion de données [!DNL Profile] et la création de segments. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fournit une représentation complète et unifiée de chaque client en fonction de données agrégées provenant de plusieurs sources.
- [[!DNL Identity Service]](../../identity-service/home.md): Permet  [!DNL Real-time Customer Profile] en rapprochant des identités de sources de données disparates ingérées dans Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel Platform organise les données d’expérience client.

Outre les documents mentionnés ci-dessus, il est vivement recommandé de consulter également les guides suivants sur les schémas et l’éditeur de schémas :

- [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : décrit les schémas XDM, les blocs de création, les principes et les bonnes pratiques pour la composition de schémas à utiliser dans [!DNL Experience Platform].
- [Tutoriel de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md) : fournit des instructions détaillées sur la création de schémas à l’aide de l’éditeur de schémas dans [!DNL Experience Platform].

## Création et configuration d’un schéma de sortie et d’un jeu de données {#create-an-output-schema-and-dataset}

La première étape de l’enrichissement de [!DNL Real-time Customer Profile] avec des informations de notation consiste à savoir quel objet réel (tel qu’une personne) vos données définissent. La compréhension de vos données vous permet de décrire et de concevoir une structure pour ajouter du sens, tout comme la conception d’une base de données relationnelle.

La composition d’un schéma commence par l’attribution d’une classe. Les classes définissent les aspects comportementaux des données que le schéma contiendra (enregistrements ou séries temporelles). Pour commencer à créer vos propres schémas, suivez les étapes du tutoriel sur la [création d’un schéma à l’aide de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md). Notez qu’avant de pouvoir activer un jeu de données pour [!DNL Profile], vous devez configurer le schéma du jeu de données pour qu’il ait un champ d’identité Principal, puis activer le schéma pour [!DNL Profile]. Lorsque des données sont ingérées dans un jeu de données compatible [!DNL Profile], ces mêmes données sont également ingérées en tant qu’enregistrements [!DNL Profile].

Si vous préférez composer un schéma à l’aide de l’API [!DNL Schema Registry], commencez par lire le [[!DNL Schema Registry] guide de développement](../../xdm/api/getting-started.md) avant de lancer le tutoriel sur la [création d’un schéma à l’aide de l’API](../../xdm/tutorials/create-schema-api.md).

Une fois votre schéma et votre jeu de données préparés, vous pouvez générer et ingérer des données de notation dans le jeu de données en effectuant des exécutions de notation à l’aide d’un modèle approprié.

## Créez des segments à l’aide de [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Après avoir généré et ingéré vos informations de données de notation dans votre jeu de données activé [!DNL Profile], vous pouvez créer des segments dynamiques à l’aide de [!DNL Segment Builder].

[!DNL Segment Builder] fournit un espace de travail riche qui vous permet d’interagir avec les éléments de données [!DNL Profile]. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données. Suivez le [[!DNL Segment Builder] guide d’utilisation](../../segmentation/ui/segment-builder.md) pour en savoir plus sur :

- Création de définitions de segment à l’aide d’une combinaison d’attributs, d’événements et d’audiences existantes comme blocs de création.
- Utilisation du canevas et des conteneurs du créateur de règles pour contrôler l’ordre d’exécution des règles de segmentation.
- Affichage des estimations de votre audience potentielle, ce qui vous permet d’ajuster vos définitions de segment selon vos besoins.
- Activation de toutes les définitions de segment pour la segmentation planifiée.
- Activation de définitions de segment spécifiées pour la segmentation par flux.

## Étapes suivantes {#next-steps}

Pour en savoir plus sur les segments et la [!DNL Segment Builder], consultez la [présentation de Segmentation Service](../../segmentation/home.md).

Pour en savoir plus sur [!DNL Real-time Customer Profile], consultez la [présentation de Real-time Customer Profile](../../profile/home.md)
