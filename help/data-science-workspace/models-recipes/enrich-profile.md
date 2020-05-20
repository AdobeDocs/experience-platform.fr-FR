---
keywords: Experience Platform;machine learning model;Data Science Workspace;Real-time Customer Profile;popular topics
solution: Experience Platform
title: Enrichir le Profil client en temps réel grâce à des informations d’apprentissage automatique
topic: Tutorial
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 0%

---


# Enrichir le Profil client en temps réel grâce à des informations d’apprentissage automatique

L’espace de travail Data Science d’Adobe Experience Platform fournit les outils et les ressources nécessaires pour créer, évaluer et utiliser des modèles d’apprentissage automatique afin de générer des prévisions et des statistiques de données. Lorsque des informations d’apprentissage automatique sont ingérées dans un jeu de données compatible avec les Profils, ces mêmes données sont également assimilées à des enregistrements de Profil qui peuvent ensuite être segmentés en sous-ensembles d’éléments connexes à l’aide du service de segmentation de la plateforme d’expérience.

Ce document fournit un didacticiel détaillé pour enrichir le Profil client en temps réel avec des informations d’apprentissage automatique. Les étapes sont divisées en sections suivantes :

1. [Création d’un schéma de sortie et d’un jeu de données](#create-an-output-schema-and-dataset)
2. [Configuration d’un schéma de sortie et d’un jeu de données](#configure-an-output-schema-and-dataset)
3. [Création de segments à l’aide du créateur de segments](#create-segments-using-the-segment-builder)

## Prise en main

Ce didacticiel nécessite une bonne compréhension des différents aspects d’Adobe Experience Platform impliqués dans l’assimilation de données de Profil et la création de segments. Avant de commencer ce didacticiel, consultez la documentation relative aux services suivants :

* [Profil](../../rtcdp/overview.md)client en temps réel : Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.
* [Service](../../identity-service/home.md)d&#39;identité : Permet le Profil client en temps réel en rapprochant les identités des sources de données disparates qui sont incorporées dans la plate-forme.
* [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.

Outre les documents susmentionnés, il est vivement recommandé de consulter également les guides suivants sur les schémas et l’éditeur de Schémas :

* [Principes de base de la composition](../../xdm/schema/composition.md)des schémas : Décrit les schémas XDM, les blocs de création, les principes et les meilleures pratiques pour la composition de schémas à utiliser dans Experience Platform.
* [Didacticiel](../../xdm/tutorials/create-schema-ui.md)sur l’éditeur de Schéma : Fournit des instructions détaillées sur la création de schémas à l’aide de l’éditeur de Schémas dans la plate-forme d’expérience.

## Création d’un schéma de sortie et d’un jeu de données {#create-an-output-schema-and-dataset}

La première étape vers l’enrichissement du Profil client en temps réel avec des informations de score consiste à savoir quel objet réel (tel qu’une personne) vos données définissent. Comprendre vos données vous permet de décrire et de concevoir une structure qui a un sens pour vos données, tout comme concevoir une base de données relationnelle.

La composition d&#39;un schéma commence par l&#39;affectation d&#39;une classe. Les classes définissent les aspects comportementaux des données que le schéma contiendra (enregistrements ou séries chronologiques). Cette section fournit des instructions de base pour créer un schéma à l’aide du créateur de schémas. Pour un didacticiel plus détaillé, reportez-vous au didacticiel sur la [création d’un schéma à l’aide de l’éditeur](../../xdm/tutorials/create-schema-ui.md)de Schéma.

1. Sur Adobe Experience Platform, cliquez sur l’onglet **[!UICONTROL Schéma]** pour accéder à l’explorateur de schémas. Cliquez sur **[!UICONTROL Créer un Schéma]** pour accéder à l’éditeur *de*Schéma, où vous pouvez créer et créer des schémas de manière interactive.
   ![](../images/models-recipes/enrich-rtcdp/schema_browser.png)

2. Dans la fenêtre *Composition* , cliquez sur **[!UICONTROL Attribuer]** pour parcourir les classes disponibles.
   * Pour affecter une classe existante, cliquez et mettez en surbrillance la classe souhaitée, puis cliquez sur **[!UICONTROL Attribuer une classe]**.
      ![](../images/models-recipes/enrich-rtcdp/existing_class.png)

   * Pour créer une classe personnalisée, cliquez sur **[!UICONTROL Créer une classe]** située près du centre de la fenêtre du navigateur. Indiquez un nom de classe, une description et choisissez le comportement de la classe. Cliquez sur **[!UICONTROL Attribuer une classe]** une fois que vous avez terminé.
      ![](../images/models-recipes/enrich-rtcdp/create_new_class.png)
   A ce stade, la structure de votre schéma doit contenir certains champs de classe et vous êtes prêt à affecter des mixins. Un mixin est un groupe d’un ou de plusieurs champs qui décrivent un concept particulier.

3. Dans la fenêtre *Composition* , cliquez sur **[!UICONTROL Ajouter]** dans la sous-section *Mélanges* .
   * Pour attribuer un mixin existant, cliquez et mettez en surbrillance le mixin souhaité, puis cliquez sur **[!UICONTROL Ajouter Mixin]**. Contrairement aux classes, plusieurs mixins peuvent être affectés à un seul schéma tant qu&#39;il est approprié de le faire.
      ![](../images/models-recipes/enrich-rtcdp/existing_mixin.png)

   * Pour créer un nouveau mixin, cliquez sur **[!UICONTROL Créer un nouveau mixin]** situé près du centre de la fenêtre du navigateur. Indiquez un nom et une description pour le mixin, puis cliquez sur **[!UICONTROL Attribuer le mixin]** une fois que vous avez terminé.
      ![](../images/models-recipes/enrich-rtcdp/create_new_mixin.png)

   * Pour ajouter des champs de mixin, cliquez sur le nom du mixin dans la fenêtre *Composition* . Vous aurez alors la possibilité d’ajouter des champs de mixin en cliquant sur Champ **** Ajouter dans la fenêtre *Structure* . Veillez à fournir les propriétés de mixin en conséquence.
      ![](../images/models-recipes/enrich-rtcdp/mixin_properties.png)

4. Une fois votre schéma créé, cliquez sur le champ de niveau supérieur de votre schéma dans la fenêtre *Structure* pour afficher les propriétés du schéma dans la fenêtre de propriétés appropriée. Indiquez un nom et une description, puis cliquez sur **[!UICONTROL Enregistrer]** pour créer le schéma.
   ![](../images/models-recipes/enrich-rtcdp/save_schema.png)

5. Créez un jeu de données de sortie à l’aide de votre nouveau schéma en cliquant sur **[!UICONTROL Jeu de données]** dans la colonne de navigation de gauche, puis cliquez sur **[!UICONTROL Créer un jeu de données]**. Dans l’écran suivant, choisissez **[!UICONTROL Créer un jeu de données à partir du schéma]**.
   ![](../images/models-recipes/enrich-rtcdp/dataset_overview.png)

6. A l’aide de l’explorateur de schémas, recherchez et sélectionnez le schéma nouvellement créé, puis cliquez sur **[!UICONTROL Suivant]**.
   ![](../images/models-recipes/enrich-rtcdp/choose_schema.png)

7. Indiquez un nom et une description facultative, puis cliquez sur **[!UICONTROL Terminer]** pour créer le jeu de données.
   ![](../images/models-recipes/enrich-rtcdp/configure_dataset.png)

Maintenant que vous avez créé un jeu de données de schéma de sortie, vous êtes prêt à passer à la section suivante pour les configurer et les activer pour l&#39;enrichissement de Profil.

## Configuration d’un schéma de sortie et d’un jeu de données {#configure-an-output-schema-and-dataset}

Avant de pouvoir activer un jeu de données pour le Profil, vous devez configurer le schéma du jeu de données pour qu&#39;il ait un champ d&#39;identité principal, puis activer le schéma pour le Profil. Si vous souhaitez créer et activer un nouveau schéma, vous pouvez vous reporter au didacticiel sur la [création d’un schéma à l’aide de l’éditeur](../../xdm/tutorials/create-schema-ui.md)de Schéma. Sinon, suivez les instructions ci-dessous pour activer un schéma et un jeu de données existants.

1. Sur Adobe Experience Platform, utilisez l’explorateur de schémas pour rechercher le schéma de sortie sur lequel vous souhaitez activer le Profil et cliquez sur son nom pour vue sa composition.
   ![](../images/models-recipes/enrich-rtcdp/schemas.png)

2. Développez la structure du schéma et recherchez un champ approprié à définir comme identifiant principal. Cliquez sur le champ de votre choix pour afficher ses propriétés.
   ![](../images/models-recipes/enrich-rtcdp/schema_structure.png)

3. Définissez le champ comme identité principale en activant la propriété **[!UICONTROL Identity]** du champ, la propriété **[!UICONTROL Primary Identity]** , puis en sélectionnant un Espace de nommage **** Identity approprié. Cliquez sur **[!UICONTROL Appliquer]** une fois que vous avez apporté vos modifications.
   ![](../images/models-recipes/enrich-rtcdp/set_identity.png)

4. Cliquez sur l’objet de niveau supérieur de votre structure de schéma pour afficher les propriétés du schéma et activer le schéma pour le Profil en basculant le commutateur de **[!UICONTROL Profil]** . Cliquez sur **[!UICONTROL Enregistrer]** pour finaliser vos modifications, les jeux de données créés à l&#39;aide de ce schéma peuvent désormais être activés pour le Profil.
   ![](../images/models-recipes/enrich-rtcdp/enable_schema.png)

5. Utilisez le navigateur de jeux de données pour rechercher le jeu de données sur lequel vous souhaitez activer le Profil et cliquez sur son nom pour accéder à ses détails.
   ![](../images/models-recipes/enrich-rtcdp/datasets.png)

6. Activez le jeu de données pour le Profil en activant le commutateur de **[!UICONTROL Profil]** situé dans la colonne d&#39;informations appropriée.
   ![](../images/models-recipes/enrich-rtcdp/enable_dataset.png)

Lorsque des données sont ingérées dans un jeu de données compatible avec les Profils, ces mêmes données sont également assimilées à des enregistrements de Profil. Maintenant que votre schéma et votre jeu de données sont préparés, générez des données dans le jeu de données en exécutant des exécutions de score à l’aide d’un modèle approprié, puis poursuivez ce didacticiel pour créer des segments d’informations à l’aide du Créateur de segments.

## Création de segments à l’aide du créateur de segments {#create-segments-using-the-segment-builder}

Maintenant que vous avez généré et assimilé des informations dans votre jeu de données compatible avec les Profils, vous pouvez gérer ces données en identifiant des sous-ensembles d’éléments connexes à l’aide du Créateur de segments. Suivez les étapes ci-dessous pour créer vos propres segments.

1. Sur Adobe Experience Platform, cliquez sur l’onglet **[!UICONTROL Segments]** suivi de **[!UICONTROL Créer un segment]** pour accéder au créateur de segments.
   ![](../images/models-recipes/enrich-rtcdp/segments_overview.png)

2. Dans le créateur de segments, le rail de gauche permet d’accéder aux principaux blocs de création de segments : attributs, événements et segments existants. Chaque bloc de construction apparaît dans son onglet respectif. Sélectionnez la classe à laquelle votre schéma activé par Profil s’étend, puis recherchez les blocs de création de votre segment.
   ![](../images/models-recipes/enrich-rtcdp/segment_builder.png)

3. Faites glisser des blocs de création sur le canevas du créateur de règles, puis complétez-les en fournissant des instructions comparatives.
   ![](../images/models-recipes/enrich-rtcdp/drag_fill.gif)

4. Lorsque vous créez votre segment, vous pouvez prévisualisation l’estimation des résultats des segments en observant le panneau Propriétés *du* segment.
   ![](../images/models-recipes/enrich-rtcdp/preview_segment.gif)

5. Sélectionnez une stratégie **[!UICONTROL de]** fusion appropriée, attribuez un nom et une description facultative, puis cliquez sur **[!UICONTROL Enregistrer]** pour terminer votre nouveau segment.
   ![](../images/models-recipes/enrich-rtcdp/save_segment.png)


## Étapes suivantes {#next-steps}

Ce document vous a guidé tout au long des étapes nécessaires pour activer un schéma et un jeu de données pour le Profil et a brièvement démontré le processus de création de segments d’informations à l’aide du créateur de segments. Pour en savoir plus sur les segments et le créateur de segments, consultez la présentation [du service](../../segmentation/home.md)Segmentation.