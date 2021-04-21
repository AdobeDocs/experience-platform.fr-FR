---
keywords: Experience Platform ; modèle d’apprentissage automatique ; Espace de travail des données ; Profil client en temps réel ; rubriques populaires ; informations d’apprentissage automatique
solution: Experience Platform
title: Enrichir le Profil client en temps réel grâce à des connaissances d'apprentissage automatique
topic-legacy: tutorial
type: Tutorial
description: Ce document fournit un guide sur la manière d’enrichir le Profil client en temps réel avec des informations d’apprentissage automatique.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 27%

---

# Enrichir [!DNL Real-time Customer Profile] avec des informations d’apprentissage automatique

Adobe Experience Platform [!DNL Data Science Workspace] fournit les outils et les ressources nécessaires pour créer, évaluer et utiliser des modèles d’apprentissage automatique afin de générer des prédictions et des statistiques sur les données. Lorsque des informations d’apprentissage automatique sont ingérées dans un jeu de données [!DNL Profile] activé, ces mêmes données sont également assimilées à des enregistrements [!DNL Profile] qui peuvent ensuite être segmentés à l’aide de [!DNL Adobe Experience Platform Segmentation Service]. À mesure que les données de profil et de série temporelle sont ingérées, Real-time Customer Profile décide automatiquement d’inclure ou d’exclure ces données des segments par le biais d’un processus continu appelé la segmentation par flux, avant de les fusionner avec les données existantes et de mettre à jour la vue d’union. Par conséquent, vous pouvez instantanément effectuer des calculs et prendre des décisions pour offrir aux clients de meilleures expériences personnalisées lorsqu’ils interagissent avec votre marque.

Ce document fournit des liens vers des didacticiels qui vous permettent d&#39;enrichir [!DNL Real-time Customer Profile] vos connaissances d&#39;apprentissage automatique.

## Prise en main

Pour compléter les didacticiels ci-dessous, vous devez maîtriser l&#39;assimilation des données [!DNL Profile] et la création de segments. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fournit une représentation complète et unifiée de chaque client en fonction de données agrégées provenant de plusieurs sources.
- [[!DNL Identity Service]](../../identity-service/home.md): Permet  [!DNL Real-time Customer Profile] de relier des identités provenant de sources de données disparates et d’être assimilées à une plateforme.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.

Outre les documents mentionnés ci-dessus, il est vivement recommandé de consulter également les guides suivants sur les schémas et l’éditeur de schémas :

- [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : décrit les schémas XDM, les blocs de création, les principes et les bonnes pratiques pour la composition de schémas à utiliser dans [!DNL Experience Platform].
- [Tutoriel de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md) : fournit des instructions détaillées sur la création de schémas à l’aide de l’éditeur de schémas dans [!DNL Experience Platform].

## Créer et configurer un schéma de sortie et un jeu de données {#create-an-output-schema-and-dataset}

La première étape vers l&#39;enrichissement de [!DNL Real-time Customer Profile] avec des statistiques de score consiste à savoir quel objet réel (tel qu&#39;une personne) vos données définissent. Comprendre vos données vous permet de décrire et de concevoir une structure pour ajouter du sens, tout comme concevoir une base de données relationnelle.

La composition d’un schéma commence par l’attribution d’une classe. Les classes définissent les aspects comportementaux des données que le schéma contiendra (enregistrements ou séries temporelles). Pour début de créer vos propres schémas, suivez les étapes du didacticiel sur la [création d’un schéma à l’aide de l’éditeur de Schéma](../../xdm/tutorials/create-schema-ui.md). Notez qu&#39;avant de pouvoir activer un jeu de données pour [!DNL Profile], vous devez configurer le schéma du jeu de données pour qu&#39;il ait un champ d&#39;identité Principal, puis activer le schéma pour [!DNL Profile]. Lorsque des données sont ingérées dans un jeu de données compatible [!DNL Profile], ces mêmes données sont également assimilées à des enregistrements [!DNL Profile].

Si vous préférez composer un schéma à l&#39;aide de l&#39;API [!DNL Schema Registry], début en lisant le [[!DNL Schema Registry] guide du développeur](../../xdm/api/getting-started.md) avant d&#39;essayer le didacticiel sur [la création d&#39;un schéma à l&#39;aide de l&#39;API](../../xdm/tutorials/create-schema-api.md).

Une fois votre schéma et votre jeu de données préparés, vous pouvez générer et assimiler des données de score au jeu de données en exécutant des exécutions de score à l’aide d’un modèle approprié.

## Créez des segments à l’aide de [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Une fois que vous avez généré et assimilé vos données de score à votre jeu de données activé [!DNL Profile], vous pouvez créer des segments dynamiques à l&#39;aide de [!DNL Segment Builder].

[!DNL Segment Builder] fournit un espace de travail riche qui vous permet d&#39;interagir avec des éléments de données [!DNL Profile]. L’espace de travail fournit des commandes intuitives pour la création et la modification de règles, telles que le glisser-déposer de mosaïques utilisées pour représenter les propriétés des données. Suivez le [[!DNL Segment Builder] guide de l&#39;utilisateur](../../segmentation/ui/segment-builder.md) pour en savoir plus sur :

- Création de définitions de segment à l’aide d’une combinaison d’attributs, de événements et d’audiences existantes en tant que blocs de création.
- Utilisation du canevas et des conteneurs du créateur de règles pour contrôler l’ordre d’exécution des règles de segmentation.
- Affichage des estimations de votre audience potentielle, ce qui vous permet d&#39;ajuster les définitions de segment selon vos besoins.
- Activation de toutes les définitions de segment pour la segmentation planifiée.
- Activation des définitions de segment spécifiées pour la segmentation en flux continu.

## Étapes suivantes {#next-steps}

Pour en savoir plus sur les segments et sur le [!DNL Segment Builder], consultez l&#39;[Présentation du service de segmentation](../../segmentation/home.md).

Pour en savoir plus sur [!DNL Real-time Customer Profile], consultez la [Présentation du Profil client en temps réel](../../profile/home.md).
