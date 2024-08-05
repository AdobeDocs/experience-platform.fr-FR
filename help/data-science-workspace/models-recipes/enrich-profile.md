---
keywords: Experience Platform ; modèle d’apprentissage automatique ; Data Science Workspace ; Profil client en temps réel ; sujets populaires ; Connaissances sur l’apprentissage automatique
solution: Experience Platform
title: Enrichissement de Real-Time Customer Profile avec des insights d’apprentissage automatique
type: Tutorial
description: Ce document fournit un guide sur la manière d’enrichir Real-Time Customer Profile avec des insights d’apprentissage automatique.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 13%

---

# Enrichir [!DNL Real-Time Customer Profile] avec des insights d&#39;apprentissage automatique

>[!NOTE]
>
>Data Science Workspace ne peut plus être acheté.
>
>Cette documentation est destinée aux clients existants disposant de droits préalables à la Workspace Data Science.

[!DNL Data Science Workspace] Adobe Experience Platform fournit les outils et les ressources nécessaires pour créer, évaluer et utiliser des modèles d’apprentissage automatique afin de générer des prédictions et des informations sur les données. Lorsque des informations d’apprentissage automatique sont ingérées dans un [!DNL Profile]jeu de données activé, ces mêmes données sont également ingérées sous forme [!DNL Profile] d’enregistrements qui peuvent ensuite être segmentés à l’aide [!DNL Adobe Experience Platform Segmentation Service]de .

Le processus de segmentation dépend de la méthode d’évaluation de l’audience. Si une audience est configurée en tant que **streaming**, elle traitera toutes les nouvelles mises à jour écrites par le modèle dans le profil en temps réel. Toutefois, si une audience est configurée pour **l’évaluation par lot** , les nouvelles valeurs seront évaluées dans le lot suivant.

Ce document fournit des liens vers des didacticiels qui vous permettent d’enrichir [!DNL Real-Time Customer Profile] vos informations Machine Learning.

## Commencer

Pour suivre les didacticiels ci-dessous, vous devez avoir une compréhension pratique de l’ingestion [!DNL Profile] de données et de la création d’audiences. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit une représentation complète et unifiée de chaque client en fonction de données agrégées provenant de plusieurs sources.
- [[!DNL Identity Service]](../../identity-service/home.md) : active [!DNL Real-Time Customer Profile] en rapprochant des identités de sources de données disparates ingérées dans Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md) : cadre normalisé selon lequel Platform organise les données d’expérience client.

Outre les documents mentionnés ci-dessus, il est vivement recommandé de consulter également les guides suivants sur les schémas et l’éditeur de schémas :

- [Principes de base de la composition](../../xdm/schema/composition.md) des schémas : décrit les schémas XDM, les blocs de construction, les principes et les meilleures pratiques pour composer des schémas à utiliser dans [!DNL Experience Platform].
- [Didacticiel](../../xdm/tutorials/create-schema-ui.md) sur l’éditeur de schéma : fournit des instructions détaillées sur la création de schémas à l’aide de l’éditeur de schéma dans [!DNL Experience Platform].

## Créer et configurer un schéma de sortie et un jeu de données {#create-an-output-schema-and-dataset}

La première étape pour enrichir [!DNL Real-Time Customer Profile] avec des informations de notation consiste à savoir quel objet du monde réel (comme une personne) vos données définissent. Avoir une compréhension de vos données vous permet de décrire et de concevoir une structure pour ajouter du sens, un peu comme la conception d’une base de données relationnelle.

La composition d’un schéma commence par l’attribution d’une classe. Les classes définissent les aspects comportementaux des données que le schéma contiendra (enregistrements ou séries temporelles). Pour commencer à créer vos propres schémas, suivez les étapes du didacticiel sur la création d’un schéma à [l’aide de l’éditeur de schéma](../../xdm/tutorials/create-schema-ui.md). Notez qu’avant de pouvoir activer un jeu de données pour [!DNL Profile], vous devez configurer le schéma du jeu de données pour qu’il ait un champ d’identité principal, puis activer le schéma pour [!DNL Profile]. Lorsque des données sont ingérées dans un jeu de données [!DNL Profile], ces mêmes données sont également ingérées en tant qu’enregistrements [!DNL Profile].

Si vous préférez composer un schéma à l’aide de l’API [!DNL Schema Registry], veuillez commencer par lire le guide de développement de [[!DNL Schema Registry] ](../../xdm/api/getting-started.md) avant de vous lancer dans le tutoriel sur la [création d’un schéma à l’aide de l’API](../../xdm/tutorials/create-schema-api.md).

Une fois votre schéma et votre jeu de données préparés, vous pouvez générer et ingérer des données de notation dans le jeu de données en effectuant des exécutions de notation à l’aide d’un modèle approprié.

## Créez des audiences à l’aide du [!DNL Segment Builder] {#create-audiences-using-the-segment-builder}

Après avoir généré et assimilé vos statistiques de notation dans votre [!DNL Profile]jeu de données activé, vous pouvez créer des audiences dynamiques à l’aide du [!DNL Segment Builder].

Le [!DNL Segment Builder] fournit un espace de travail riche qui vous permet d’interagir avec [!DNL Profile] les éléments de données. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que les mosaïques glisser-déposer utilisées pour représenter les propriétés des données. Suivez le guide](../../segmentation/ui/segment-builder.md) de l’utilisateur [[!DNL Segment Builder] pour en savoir plus sur :

- Créer des définitions de segment en utilisant une combinaison d’attributs, d’événements et d’audiences existantes comme blocs de création.
- Utilisation du canevas et des conteneurs du créateur de règles pour contrôler l’ordre dans lequel les règles d’audience sont exécutées.
- Affichage des estimations de votre public potentiel, vous permettant d’ajuster vos définitions de segment selon les besoins.
- Activation de toutes les définitions de segment pour la segmentation planifiée.
- Activation de définitions de segment spécifiées pour la segmentation par flux.

## Étapes suivantes {#next-steps}

Pour en savoir plus sur les audiences et le [!DNL Segment Builder], consultez la [présentation de Segmentation Service](../../segmentation/home.md).

Pour en savoir plus sur [!DNL Real-Time Customer Profile], consultez la présentation du [profil client en temps réel](../../profile/home.md)
