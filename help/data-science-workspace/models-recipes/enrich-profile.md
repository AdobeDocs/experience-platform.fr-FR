---
keywords: Experience Platform;modèle d’apprentissage automatique;Data Science Workspace;profil client en temps réel;rubriques populaires;insights d’apprentissage automatique
solution: Experience Platform
title: Enrichissement de Real-Time Customer Profile avec des insights d’apprentissage automatique
topic-legacy: tutorial
type: Tutorial
description: Ce document fournit un guide sur la manière d’enrichir Real-Time Customer Profile avec des insights d’apprentissage automatique.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 21%

---

# Enrichir [!DNL Real-Time Customer Profile] avec des insights d’apprentissage automatique

Adobe Experience Platform [!DNL Data Science Workspace] fournit les outils et les ressources nécessaires pour créer, évaluer et utiliser des modèles d’apprentissage automatique afin de générer des prévisions et des insights sur les données. Lorsque des insights d’apprentissage automatique sont ingérés dans une [!DNL Profile]Jeu de données compatible, ces mêmes données sont également ingérées en tant que [!DNL Profile] enregistrements pouvant ensuite être segmentés à l’aide de [!DNL Adobe Experience Platform Segmentation Service].

Ce document fournit des liens vers des tutoriels qui vous permettent d’enrichir [!DNL Real-Time Customer Profile] avec vos insights d’apprentissage automatique.

## Prise en main

Pour pouvoir suivre les tutoriels ci-dessous, vous devez maîtriser l’ingestion. [!DNL Profile] données et création de segments. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fournit une représentation complète et unifiée de chaque client en fonction de données agrégées provenant de plusieurs sources.
- [[!DNL Identity Service]](../../identity-service/home.md): Active [!DNL Real-Time Customer Profile] en rapprochant des identités de sources de données disparates ingérées dans Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : framework normalisé selon lequel Platform organise les données de l’expérience client.

Outre les documents mentionnés ci-dessus, il est vivement recommandé de consulter également les guides suivants sur les schémas et l’éditeur de schémas :

- [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : décrit les schémas XDM, les blocs de création, les principes et les bonnes pratiques pour la composition de schémas à utiliser dans [!DNL Experience Platform].
- [Tutoriel de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md) : fournit des instructions détaillées sur la création de schémas à l’aide de l’éditeur de schémas dans [!DNL Experience Platform].

## Création et configuration d’un schéma de sortie et d’un jeu de données {#create-an-output-schema-and-dataset}

La première étape de l&#39;enrichissement [!DNL Real-Time Customer Profile] avec les informations de notation, vous savez quel objet du monde réel (une personne, par exemple) vos données définissent. La compréhension de vos données vous permet de décrire et de concevoir une structure pour ajouter du sens, tout comme la conception d’une base de données relationnelle.

La composition d’un schéma commence par l’attribution d’une classe. Les classes définissent les aspects comportementaux des données que le schéma contiendra (enregistrements ou séries temporelles). Pour commencer à créer vos propres schémas, suivez les étapes du tutoriel sur [création d’un schéma à l’aide de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md). Notez qu’avant d’activer un jeu de données pour [!DNL Profile], vous devez configurer le schéma du jeu de données pour qu’il comporte un champ d’identité Principal, puis activer le schéma pour [!DNL Profile]. Lorsque des données sont ingérées dans une [!DNL Profile]Jeu de données compatible, ces mêmes données sont également ingérées en tant que [!DNL Profile] enregistrements.

Si vous préférez composer un schéma à l’aide de la méthode [!DNL Schema Registry] à la place, commencez par lire la variable [[!DNL Schema Registry] guide de développement](../../xdm/api/getting-started.md) avant de lancer le tutoriel sur [création d’un schéma à l’aide de l’API](../../xdm/tutorials/create-schema-api.md).

Une fois votre schéma et votre jeu de données préparés, vous pouvez générer et ingérer des données de notation dans le jeu de données en effectuant des exécutions de notation à l’aide d’un modèle approprié.

## Créez des segments à l’aide du [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Après avoir généré et ingéré vos informations de données de notation sur vos [!DNL Profile]jeu de données compatible, vous pouvez créer des segments dynamiques à l’aide de la variable [!DNL Segment Builder].

Le [!DNL Segment Builder] fournit un espace de travail riche qui vous permet d’interagir avec [!DNL Profile] éléments de données. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données. Suivez la [[!DNL Segment Builder] guide de l’utilisateur](../../segmentation/ui/segment-builder.md) pour en savoir plus sur :

- Création de définitions de segment à l’aide d’une combinaison d’attributs, d’événements et d’audiences existantes comme blocs de création.
- Utilisation du canevas et des conteneurs du créateur de règles pour contrôler l’ordre d’exécution des règles de segmentation.
- Affichage des estimations de votre audience potentielle, ce qui vous permet d’ajuster vos définitions de segment selon vos besoins.
- Activation de toutes les définitions de segment pour la segmentation planifiée.
- Activation de définitions de segment spécifiées pour la segmentation par flux.

## Étapes suivantes {#next-steps}

Pour en savoir plus sur les segments et la variable [!DNL Segment Builder], lisez le [Présentation de Segmentation Service](../../segmentation/home.md).

Pour en savoir plus sur [!DNL Real-Time Customer Profile], lisez le [Présentation de Real-Time Customer Profile](../../profile/home.md)
