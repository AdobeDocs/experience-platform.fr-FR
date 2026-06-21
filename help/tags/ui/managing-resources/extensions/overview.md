---
title: Extensions
description: Découvrez le fonctionnement des extensions de balises dans Adobe Experience Platform.
exl-id: e911bedd-6c67-4339-91d7-839c8b00c153
TQID: https://experienceleague.adobe.com/bezLvulAuqqAMPalccyxWvliQ0MKeRw8SHPZiTp-noc
product_v2: id: a829a185-511f-4bf8-8dcf-9e684f8011cfid: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87id: e55547f1-a1ff-40c6-8978-026e40ab7fa4id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: e08599ea-8888-4294-ba74-3ba0a7762a46
subfeature_v2: id: abc02dd6-664f-446a-9aaa-675bc0f2fe4aid: d9830f6f-ceb6-4faa-9744-f281fe4439f9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 481
ht-degree: 83%

---

# Extensions

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

Par défaut, Adobe fournit des extensions qui prennent en charge les intégrations courantes. Les extensions peuvent être modifiées par des configurations personnalisées. Les configurations sont fournies par le biais des extensions. Pour créer une configuration, sélectionnez la carte d’extension, puis sélectionnez **[!UICONTROL Ajouter une nouvelle configuration]**.

## Catalogue d’extensions

Utilisez le catalogue dʼextensions pour parcourir, configurer et déployer la technologie publicitaire et marketing créée et conservée par des fournisseurs de logiciels indépendants, ainsi que des extensions pour les solutions Adobe.

La page Extensions propose trois options d’affichage :

* Installed (Installées)

  Affiche toutes les extensions installées.

* Catalog (Catalogue)
* Affiche toutes les extensions disponibles.
* Mises à jour

  Affiche les mises à jour des extensions installées.

Sélectionnez **[!UICONTROL Extensions]** pour afficher toutes les extensions installées. Vous pouvez également utiliser le catalogue pour afficher la liste de toutes les extensions disponibles et les extensions pour lesquelles des mises à jour sont disponibles.

Pour plus dʼinformations sur les extensions développées par Adobe, voir [Référence des extensions](../../../extensions/client/overview.md).

## Ajouter une nouvelle extension {#add-a-new-extension}

Nombre de fonctionnalités peuvent être ajoutées aux balises. Les extensions ajoutent des fonctionnalités essentielles aux balises. Les extensions sont souvent utilisées pour créer des intégrations avec d’autres applications.

>[!TIP]
>
>Utilisez l’aide du produit dans le panneau de droite pour en savoir plus sur les extensions et afficher les ressources supplémentaires disponibles.

1. Ouvrez l’onglet **[!UICONTROL Extensions]** à partir de la page d’aperçu de la propriété.
1. Sélectionnez l’extension.

   ![Onglet Catalogue affichant les extensions principales dans l’onglet Extensions.](../../../images/extensions.png)

   * Si l’extension existe, sélectionnez-la dans le catalogue des extensions.
   * Placez le pointeur de la souris sur une extension de votre liste pour la configurer ou la désactiver.
   * Ajoutez d’autres extensions du catalogue si elles ne figurent pas actuellement dans votre liste.

   L’extension Core est le point de départ de votre nouvelle extension. L’extension par défaut fournit :

   * Les événement par défaut
   * Les conditions et exceptions par défaut
   * Le code côté client

   Ces valeurs par défaut sont la base des règles personnalisées que vous allez créer pour créer votre extension.

Lors de la création ou de la modification d’éléments, vous pouvez enregistrer et créer une [bibliothèque active](../../publishing/libraries.md#active-library). Cette opération enregistre immédiatement votre modification dans votre bibliothèque et exécute une version. Le statut de la version s’affiche. Vous pouvez également créer une bibliothèque à partir de la liste déroulante Bibliothèque active.

## Configuration d’une extension

Placez le pointeur de la souris sur une extension installée et sélectionnez **[!UICONTROL Configurer]**.

>[!NOTE]
>
>Certaines extensions ne nécessitent pas de configuration et ne proposent pas d’options de configuration.

Chaque extension configurable possède des options uniques. Pour plus dʼinformations sur les options disponibles pour chaque extension Adobe, reportez-vous à la section [Référence des extensions](../../../extensions/client/overview.md).
