---
keywords: Experience Platform;machine learning model;Data Science Workspace;Real-time Customer Profile;popular topics;machine learning insights
solution: Experience Platform
title: Enrichissement de Real-time Customer Profile avec des insights d’apprentissage automatique
topic: Tutorial
description: Ce document fournit un didacticiel détaillé pour enrichir le Profil client en temps réel avec des informations d’apprentissage automatique, les étapes sont réparties dans les sections suivantes, créer un schéma de sortie/jeu de données, configurer un schéma de sortie/jeu de données et créer des segments à l’aide du Créateur de segments.
translation-type: tm+mt
source-git-commit: 43d568a401732a753553847dee1b4a924fcc24fd
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 71%

---


# Enrich [!DNL Real-time Customer Profile] with machine learning insights

[!DNL Adobe Experience Platform] [!DNL Data Science Workspace] fournit des outils et des ressources pour créer, évaluer et utiliser des modèles d’apprentissage automatique afin de générer des prévisions et des insights sur les données. When machine learning insights are ingested into a [!DNL Profile]-enabled dataset, that same data is also ingested as [!DNL Profile] records which can then be segmented into subsets of related elements by using [!DNL Experience Platform Segmentation Service].

This document provides a step-by-step tutorial to enrich [!DNL Real-time Customer Profile] with machine learning insights, steps are broken into the following sections:

1. [Création d’un schéma de sortie et d’un jeu de données](#create-an-output-schema-and-dataset)
2. [Configuration d’un schéma de sortie et d’un jeu de données](#configure-an-output-schema-and-dataset)
3. [Création de segments à l’aide du créateur de segments](#create-segments-using-the-segment-builder)

## Prise en main

This tutorial requires a working understanding of the various aspects of [!DNL Adobe Experience Platform] involved in ingesting [!DNL Profile] data and creating segments. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux services suivants :

* [[ !Profil client en temps réel DNL]](../../rtcdp/overview.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [[ !Service d&#39;identité DNL]](../../identity-service/home.md): Permet [!DNL Real-time Customer Profile] de relier des identités provenant de sources de données disparates et d’être assimilées à une plateforme.
* [[ ! Modèle de données d’expérience DNL (XDM)]](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.

Outre les documents mentionnés ci-dessus, il est vivement recommandé de consulter également les guides suivants sur les schémas et l’éditeur de schémas :

* [Principes de base de la composition des schémas](../../xdm/schema/composition.md) : décrit les schémas XDM, les blocs de création, les principes et les bonnes pratiques pour la composition de schémas à utiliser dans [!DNL Experience Platform].
* [Tutoriel de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md) : fournit des instructions détaillées sur la création de schémas à l’aide de l’éditeur de schémas dans [!DNL Experience Platform].

## Création d’un schéma de sortie et d’un jeu de données {#create-an-output-schema-and-dataset}

The first step towards enriching [!DNL Real-time Customer Profile] with scoring insights is knowing what real-world object (such as a person) your data defines. La compréhension de vos données vous permet de décrire et de concevoir une structure qui donne du sens à vos données, tout comme la conception d’une base de données relationnelle.

La composition d’un schéma commence par l’attribution d’une classe. Les classes définissent les aspects comportementaux des données que le schéma contiendra (enregistrements ou séries temporelles). Cette section fournit des instructions de base pour créer un schéma à l’aide du créateur de schémas. Pour un tutoriel plus détaillé, reportez-vous au tutoriel sur la [création d’un schéma à l’aide de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md).

1. Sur Adobe Experience Platform, cliquez sur l’onglet du **[!UICONTROL schéma]** pour accéder au navigateur de schéma. Cliquez sur **[!UICONTROL Créer un schéma]**, accédez à l’*éditeur de schémas*, où vous pouvez créer des schémas de manière interactive.
   ![](../images/models-recipes/enrich-rtcdp/schema_browser.png)

2. Dans la fenêtre *Composition*, cliquez sur **[!UICONTROL Attribuer]** pour parcourir les classes disponibles.
   * Pour attribuer une classe existante, cliquez et mettez en surbrillance la classe souhaitée, puis cliquez sur **[!UICONTROL Attribuer une classe]**.
      ![](../images/models-recipes/enrich-rtcdp/existing_class.png)

   * Pour créer une classe personnalisée, cliquez sur **[!UICONTROL Créer une classe]** située près du centre de la fenêtre du navigateur. Indiquez un nom de classe, une description et choisissez le comportement de la classe. Cliquez sur **[!UICONTROL Attribuer une classe]** une fois que vous avez terminé.
      ![](../images/models-recipes/enrich-rtcdp/create_new_class.png)

   À ce stade, la structure de votre schéma doit contenir certains champs de classe et vous êtes prêt à attribuer des mixins. Un mixin est un groupe d’un ou de plusieurs champs qui décrivent un concept particulier.

3. Dans la fenêtre *Composition*, cliquez sur **[!UICONTROL Ajouter]** dans la sous-section *Mixins*.
   * Pour attribuer un mixin existant, cliquez et mettez en surbrillance le mixin souhaité, puis cliquez sur **[!UICONTROL Attribuer un mixin]**. Contrairement aux classes, plusieurs mixins peuvent être attribués à un seul schéma tant qu’il est approprié de le faire.
      ![](../images/models-recipes/enrich-rtcdp/existing_mixin.png)

   * Pour créer un mixin, cliquez sur **[!UICONTROL Créer un mixin]** situé près du centre de la fenêtre du navigateur. Attribuez un nom et une description au mixin, puis cliquez sur **[!UICONTROL Attribuer un mixin]** une fois que vous avez terminé.
      ![](../images/models-recipes/enrich-rtcdp/create_new_mixin.png)

   * Pour ajouter des champs de mixin, cliquez sur le nom du mixin dans la fenêtre *Composition*. Vous aurez alors la possibilité d’ajouter des champs de mixin en cliquant sur **[!UICONTROL Ajouter un champ]** dans la fenêtre *Structure*. Veillez à fournir les propriétés de mixin en conséquence.
      ![](../images/models-recipes/enrich-rtcdp/mixin_properties.png)

4. Une fois la création de votre schéma terminée, cliquez sur le champ de niveau supérieur de votre schéma dans la fenêtre *Structure* pour afficher les propriétés du schéma dans la fenêtre des propriétés de droite. Attribuez un nom et une description, puis cliquez sur **[!UICONTROL Enregistrer]** pour créer le schéma.
   ![](../images/models-recipes/enrich-rtcdp/save_schema.png)

5. Créez un jeu de données de sortie à l’aide de votre nouveau schéma en cliquant sur **[!UICONTROL Jeu de données]** dans la colonne de navigation de gauche, puis sur **[!UICONTROL Créer un jeu de données]**. Dans l’écran suivant, choisissez **[!UICONTROL Créer un jeu de données à partir d’un schéma]**.
   ![](../images/models-recipes/enrich-rtcdp/dataset_overview.png)

6. À l’aide du navigateur de schéma, recherchez et sélectionnez le schéma nouvellement créé, puis cliquez sur **[!UICONTROL Suivant]**.
   ![](../images/models-recipes/enrich-rtcdp/choose_schema.png)

7. Attribuez un nom et une description optionnelle, puis cliquez sur **[!UICONTROL Terminer]** pour créer le jeu de données.
   ![](../images/models-recipes/enrich-rtcdp/configure_dataset.png)

Maintenant que vous avez créé un jeu de données de schéma de sortie, vous êtes prêt à passer à la section suivante pour le configurer et l’activer afin d’enrichir Profile.

## Configuration d’un schéma de sortie et d’un jeu de données {#configure-an-output-schema-and-dataset}

Before you can enable a dataset for [!DNL Profile], you need to configure the dataset&#39;s schema to having a primary identity field and then enable the schema for [!DNL Profile]. Si vous souhaitez créer et activer un nouveau schéma, vous pouvez vous reporter au tutoriel sur la [création d’un schéma à l’aide de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md). Sinon, suivez les instructions ci-dessous pour activer un schéma et un jeu de données existants.

1. On Adobe Experience Platform, use the schema browser to find the output schema you wish to enable [!DNL Profile] on and click its name to view its composition.
   ![](../images/models-recipes/enrich-rtcdp/schemas.png)

2. Développez la structure du schéma et recherchez un champ approprié à définir comme identifiant principal. Cliquez sur le champ de votre choix pour afficher ses propriétés.
   ![](../images/models-recipes/enrich-rtcdp/schema_structure.png)

3. Définissez le champ comme identité principale en activant la propriété **[!UICONTROL Identity]** du champ, la propriété **[!UICONTROL Primary Identity]**, puis en sélectionnant un **[!UICONTROL espace de noms d’identité]** approprié. Cliquez sur **[!UICONTROL Appliquer]** une fois les modifications effectuées.
   ![](../images/models-recipes/enrich-rtcdp/set_identity.png)

4. Cliquez sur l’objet de niveau supérieur de la structure de votre schéma pour afficher les propriétés de schéma et activer le schéma pour Profile à l’aide du bouton activer/désactiver de **[!UICONTROL Profile]**. Cliquez sur **[!UICONTROL Enregistrer]** pour achever vos modifications. Les jeux de données créés à l’aide de ce schéma peuvent désormais être activés pour Profile.
   ![](../images/models-recipes/enrich-rtcdp/enable_schema.png)

5. Use the dataset browser to find the dataset you wish to enable [!DNL Profile] on and click its name to access its details.
   ![](../images/models-recipes/enrich-rtcdp/datasets.png)

6. Enable the dataset for [!DNL Profile] by toggling the **[!UICONTROL Profile]** switch found in the right information column.
   ![](../images/models-recipes/enrich-rtcdp/enable_dataset.png)

When data is ingested into a [!DNL Profile]-enabled dataset, that same data is also ingested as [!DNL Profile] records. Maintenant que votre schéma et votre jeu de données sont préparés, générez des données dans le jeu de données en effectuant des exécutions de notation à l’aide d’un modèle approprié, puis poursuivez avec ce tutoriel pour créer des segments d’insights à l’aide du créateur de segments.

## Création de segments à l’aide du créateur de segments {#create-segments-using-the-segment-builder}

Now that you have generated and ingested insights into your [!DNL Profile]-enabled dataset, you can manage that data by identifying subsets of related elements using the Segment Builder. Suivez les étapes ci-dessous pour créer vos propres segments.

1. Dans Adobe Experience Platform, cliquez sur l’onglet **[!UICONTROL Segments]** suivi de **[!UICONTROL Créer un segment]** pour accéder au créateur de segments.
   ![](../images/models-recipes/enrich-rtcdp/segments_overview.png)

2. Dans le créateur de segments, le rail de gauche permet d’accéder aux principaux blocs de création des segments : attributs, événements et segments existants. Chaque bloc de création apparaît dans son propre onglet respectif. Select the class to which your [!DNL Profile]-enabled schema extends then browse and find the building blocks for your segment.
   ![](../images/models-recipes/enrich-rtcdp/segment_builder.png)

3. Faites glisser des blocs de création sur le canevas du créateur de règles, puis complétez-les en fournissant des instructions comparatives.
   ![](../images/models-recipes/enrich-rtcdp/drag_fill.gif)

4. Lorsque vous créez votre segment, vous pouvez prévisualiser les résultats estimés des segments en observant le panneau *Propriétés du segment*.
   ![](../images/models-recipes/enrich-rtcdp/preview_segment.gif)

5. Sélectionnez une **[!UICONTROL stratégie de fusion]** appropriée, attribuez-lui un nom et une description facultative, puis cliquez sur **[!UICONTROL Enregistrer]** pour terminer votre nouveau segment.
   ![](../images/models-recipes/enrich-rtcdp/save_segment.png)


## Étapes suivantes {#next-steps}

This document walked you through the steps required to enable a schema and dataset for [!DNL Profile], and briefly demonstrated the workflow for creating insight segments using the Segment Builder. Pour en savoir plus sur les segments et le créateur de segments, reportez-vous à la [présentation de Segmentation Service](../../segmentation/home.md).