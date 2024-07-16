---
title: Extensions
description: Découvrez le fonctionnement des extensions de balises dans Adobe Experience Platform.
exl-id: e911bedd-6c67-4339-91d7-839c8b00c153
source-git-commit: 31811b7448a285ee5d25872641354a6981c64471
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 94%

---

# Extensions

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Une extension est un jeu de codes empaqueté qui étend les fonctionnalités fournies par les balises ou le transfert dʼévénements.

L’ajout d’une extension ajoute de nouveaux éléments de données et de nouvelles options pour créer des règles.

Les extensions déterminent les éléments disponibles lors de la création de propriétés, de règles et d’éléments de données. Elles fournissent les éléments suivants :

* Événements, conditions et exceptions
* Éléments de données
* Code côté client

Utilisez les liens situés en haut de la liste Extensions pour afficher les extensions installées, le catalogue des extensions ou les mises à jour.

Sélectionnez une extension, puis cliquez sur [!UICONTROL Configurer] pour afficher et modifier les paramètres de l’extension. Pour plus dʼinformations sur les options des extensions, voir la section sur lʼ[ajout dʼune nouvelle extension](#add-a-new-extension).

>[!IMPORTANT]
>
>Les modifications ne prennent effet que lorsqu’elles sont [publiées](../../publishing/overview.md).

Par défaut, Adobe fournit des extensions qui prennent en charge les intégrations courantes. Les extensions peuvent être modifiées par des configurations personnalisées. Les configurations sont fournies par le biais des extensions. Pour créer une configuration, cliquez sur la carte d’extension, puis sélectionnez **[!UICONTROL Ajouter une nouvelle configuration]**.

## Catalogue d’extensions

Utilisez le catalogue dʼextensions pour parcourir, configurer et déployer la technologie publicitaire et marketing créée et conservée par des fournisseurs de logiciels indépendants, ainsi que des extensions pour les solutions Adobe.

La page Extensions propose trois options d’affichage :

* Installed (Installées)

  Affiche toutes les extensions installées.

* Catalog (Catalogue)
* Affiche toutes les extensions disponibles.
* Mises à jour

  Affiche les mises à jour des extensions installées.

Cliquez sur **[!UICONTROL Extensions]** pour afficher toutes les extensions installées. Vous pouvez également utiliser le catalogue pour afficher la liste de toutes les extensions disponibles et les extensions pour lesquelles des mises à jour sont disponibles.

Pour plus dʼinformations sur les extensions développées par Adobe, voir [Référence des extensions](../../../extensions/client/overview.md).

## Ajouter une nouvelle extension {#add-a-new-extension}

Nombre de fonctionnalités peuvent être ajoutées aux balises. Les extensions ajoutent des fonctionnalités essentielles aux balises. Les extensions sont souvent utilisées pour créer des intégrations avec d’autres applications.

>[!TIP]
>
>Utilisez l’ aide du produit dans le panneau de droite pour en savoir plus sur les extensions et afficher d’autres ressources disponibles.

1. Ouvrez l’onglet **[!UICONTROL Extensions]** à partir de la page d’aperçu de la propriété.
1. Sélectionnez l’extension.

   ![Onglet Catalogue présentant les extensions principales dans l’onglet des extensions.](../../../images/extensions.png)

   * Si l’extension existe, sélectionnez-la dans le catalogue des extensions.
   * Placez le pointeur de la souris sur une extension de votre liste pour la configurer ou la désactiver.
   * Ajoutez d’autres extensions du catalogue si elles ne figurent pas actuellement dans votre liste.

   L’extension Core est le point de départ de votre nouvelle extension. L’extension par défaut fournit :

   * Les événement par défaut
   * Les conditions et exceptions par défaut
   * Le code côté client

   Ces valeurs par défaut sont la base des règles personnalisées que vous allez créer pour créer votre extension.

Lors de la création ou de la modification d’éléments, vous pouvez enregistrer et créer une [bibliothèque active](../../publishing/libraries.md#active-library). Cette opération enregistre immédiatement votre modification dans votre bibliothèque et exécute une version. Le statut de la version s’affiche. Vous pouvez également créer une bibliothèque à partir de la liste déroulante Active Library (Bibliothèque active).

## Configuration d’une extension

Placez le pointeur de la souris sur une extension installée et cliquez sur **[!UICONTROL Configurer]**.

>[!NOTE]
>
>Certaines extensions ne nécessitent pas de configuration et ne proposent pas d’options de configuration.

Chaque extension configurable possède des options uniques. Pour plus dʼinformations sur les options disponibles pour chaque extension Adobe, reportez-vous à la section [Référence des extensions](../../../extensions/client/overview.md).
