---
keywords: Experience Platform;modèle de machine learning;Workspace de science des données;Profil client en temps réel;rubriques populaires;informations de machine learning
solution: Experience Platform
title: Enrichissement du profil client en temps réel avec des informations de machine learning
type: Tutorial
description: Ce document fournit un guide sur la manière d’enrichir le profil client en temps réel avec des informations sur le machine learning.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 15%

---

# Enrichir les [!DNL Real-Time Customer Profile] avec des informations de machine learning

>[!NOTE]
>
>Le Workspace de science des données ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits antérieurs sur Data Science Workspace.

Adobe Experience Platform [!DNL Data Science Workspace] fournit des outils et des ressources pour créer, évaluer et utiliser des modèles de machine learning afin de générer des prédictions et des informations sur les données. Lorsque des informations d’apprentissage automatique sont ingérées dans un jeu de données activé pour [!DNL Profile], ces mêmes données sont également ingérées en tant qu’enregistrements [!DNL Profile] et peuvent ensuite être segmentées à l’aide de [!DNL Adobe Experience Platform Segmentation Service].

Le processus de segmentation dépend de la méthode d’évaluation de l’audience. Si une audience est configurée en tant que **diffusion en continu**, elle traite toutes les nouvelles mises à jour écrites par le modèle dans le profil en temps réel. Cependant, si une audience est configurée pour une évaluation **par lots**, les nouvelles valeurs seront évaluées dans le lot suivant.

Ce document fournit des liens vers des tutoriels qui vous permettent d’enrichir [!DNL Real-Time Customer Profile] avec vos informations sur le machine learning.

## Commencer

Pour suivre les tutoriels ci-dessous, vous devez maîtriser l’ingestion de données [!DNL Profile] et la création d’audiences. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit une représentation complète et unifiée de chaque client individuel sur la base de données agrégées provenant de plusieurs sources.
- [[!DNL Identity Service]](../../identity-service/home.md) : permet l’[!DNL Real-Time Customer Profile] en établissant un lien entre les identités des sources de données disparates ingérées dans Experience Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : framework normalisé selon lequel Experience Platform organise les données de l’expérience client.

Outre les documents mentionnés ci-dessus, il est vivement recommandé de consulter également les guides suivants sur les schémas et l’éditeur de schémas :

- [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : décrit les schémas XDM, les blocs de création, les principes et les bonnes pratiques pour la composition de schémas à utiliser dans [!DNL Experience Platform].
- [Tutoriel de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md) : fournit des instructions détaillées sur la création de schémas à l’aide de l’éditeur de schémas dans [!DNL Experience Platform].

## Créer et configurer un schéma de sortie et un jeu de données {#create-an-output-schema-and-dataset}

La première étape pour enrichir les [!DNL Real-Time Customer Profile] avec des informations de notation est de savoir quel objet du monde réel (une personne, par exemple) vos données définissent. Comprendre vos données vous permet de décrire et de concevoir une structure pour ajouter du sens, à l’instar de la conception d’une base de données relationnelle.

La composition d’un schéma commence par l’attribution d’une classe. Les classes définissent les aspects comportementaux des données que le schéma contiendra (enregistrements ou séries temporelles). Pour commencer à créer vos propres schémas, suivez les étapes du tutoriel sur la [création d’un schéma à l’aide de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md). Notez qu’avant de pouvoir activer un jeu de données pour [!DNL Profile], vous devez configurer le schéma du jeu de données pour qu’il comporte un champ d’identité principale, puis activer le schéma pour [!DNL Profile]. Lorsque des données sont ingérées dans un jeu de données activé pour [!DNL Profile], ces mêmes données sont également ingérées en tant qu’enregistrements [!DNL Profile].

Si vous préférez composer un schéma à l’aide de l’API [!DNL Schema Registry], veuillez commencer par lire le guide de développement de [[!DNL Schema Registry] &#x200B;](../../xdm/api/getting-started.md) avant de vous lancer dans le tutoriel sur la [création d’un schéma à l’aide de l’API](../../xdm/tutorials/create-schema-api.md).

Une fois votre schéma et votre jeu de données préparés, vous pouvez générer et ingérer des données de notation dans le jeu de données en exécutant des exécutions de notation à l’aide d’un modèle approprié.

## Créer des audiences à l’aide de l’[!DNL Segment Builder] {#create-audiences-using-the-segment-builder}

Une fois que vous avez généré et ingéré vos informations de données de notation dans votre jeu de données activé pour [!DNL Profile], vous pouvez créer des audiences dynamiques à l’aide de l’[!DNL Segment Builder] .

Le [!DNL Segment Builder] offre un vaste espace de travail qui vous permet d’interagir avec les éléments de données [!DNL Profile]. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données. Suivez le [[!DNL Segment Builder] guide de l’utilisateur](../../segmentation/ui/segment-builder.md) pour en savoir plus sur :

- Création de définitions de segment à l’aide d’une combinaison d’attributs, d’événements et d’audiences existantes comme blocs de création.
- Utilisation de la zone de travail et des conteneurs du créateur de règles pour contrôler l’ordre dans lequel les règles d’audience sont exécutées.
- Affichage des estimations de votre audience potentielle, ce qui vous permet d’ajuster vos définitions de segment selon vos besoins.
- Activation de toutes les définitions de segment pour la segmentation planifiée.
- Activation des définitions de segment spécifiées pour la segmentation en flux continu.

## Étapes suivantes {#next-steps}

Pour en savoir plus sur les audiences et la [!DNL Segment Builder], lisez la [&#x200B; présentation de Segmentation Service &#x200B;](../../segmentation/home.md).

Pour en savoir plus sur [!DNL Real-Time Customer Profile], lisez la [&#x200B; Présentation du profil client en temps réel &#x200B;](../../profile/home.md)
