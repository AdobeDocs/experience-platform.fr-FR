---
title: Création De Schémas Assistée Par Machine Learning
description: Découvrez comment créer des schémas dans l’interface utilisateur d’Experience Platform.
badgeBeta: label="Beta" type="Informative"
exl-id: 6b14caed-a3ad-4834-8fa8-8d67dce6290e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 2%

---

# Création de schémas assistée par machine learning

>[!AVAILABILITY]
>
>* La création de schémas assistée par machine learning est actuellement en version bêta. La documentation et les fonctionnalités peuvent changer.

Utilisez des algorithmes ML pour générer un schéma à partir de données d’exemple. Ce processus permet de gagner du temps et d’améliorer la précision lors de la définition de la structure, des champs et des types de données pour les jeux de données complexes volumineux.

Avec la génération de schéma ML, vous pouvez rapidement intégrer de nouvelles sources de données et réduire les erreurs liées à la création manuelle. Les utilisateurs non techniques peuvent l’utiliser pour générer des schémas ou gérer des jeux de données volumineux et complexes sans effort supplémentaire. Cette assistance accélère le processus d’obtention des données à l’obtention d’informations, car elle facilite la combinaison de nouvelles sources de données et l’analyse des données.

## Commencer

Ce tutoriel nécessite une bonne compréhension des exigences relatives à la création de schémas. Avant de poursuivre avec ce guide, vous devez lire le guide [UI guide to create and editing schemas](./resources/schemas.md).

Ce guide explique comment créer des schémas à l’aide d’algorithmes de machine learning (ML) pour générer un schéma à partir de données d’exemple. Consultez le [guide des workflows de création manuelle de schéma](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas#add-field-groups) pour plus d’informations sur la création de schémas ou le document sur les workflows basés sur des champs [ dans l’éditeur de schémas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/field-based-workflows) afin de mieux comprendre le processus de création de schémas.

>[!NOTE]
>
>Vous pouvez également composer un schéma à l’aide de l’API [!DNL Schema Registry]. Pour créer un schéma manuellement à l’aide de l’API , lisez d’abord le [[!DNL Schema Registry] guide de développement](../api/getting-started.md) avant de vous lancer dans le tutoriel sur [la création d’un schéma à l’aide de l’API](../tutorials/create-schema-api.md).

## Accès au workflow Créer un schéma {#navigate-to-schema-creation-workflow}

Dans le volet de navigation de gauche de l’interface utilisateur d’Experience Platform, sélectionnez l’espace de travail **[!UICONTROL Schémas]**. L’espace de travail **[!UICONTROL Schémas]** s’affiche. Sélectionnez **[!UICONTROL Créer un schéma]** pour ajouter un nouveau schéma afin de démarrer un workflow de création de schéma.

![L’espace de travail Schémas avec Schéma dans le volet de navigation de gauche et Créer un schéma en surbrillance.](../images/ui/ml-schema-creation/schemas-workspace-create-schema.png)

## Créer un schéma {#create-a-schema}

La boîte de dialogue [!UICONTROL Créer un schéma] s’affiche. Sélectionnez l’option de création de schéma **[assistée par ML]**, puis **[!UICONTROL Sélectionner]** pour confirmer votre choix.

![ La boîte de dialogue [!UICONTROL Créer un schéma] avec l’[!UICONTROL Assistant ML] mise en surbrillance.](../images/ui/ml-schema-creation/use-sample-csv.png)

### Sélectionner une classe de base {#select-base-class}

Le workflow [!UICONTROL Créer un schéma] s’affiche. Sélectionnez une classe de base pour votre schéma, suivie de **[!UICONTROL Suivant]**.

![L’espace de travail Détails du schéma avec une classe et le suivant en surbrillance.](../images/ui/ml-schema-creation/select-base-class.png)

### Chargement d’un fichier CSV {#upload-csv}

L’étape **[!UICONTROL Sélectionner les données]** du workflow de création s’affiche. Dans la section **[!UICONTROL Télécharger des fichiers]**, sélectionnez **[!UICONTROL Choisir les fichiers]** ou la section **[!UICONTROL Glisser-déposer des fichiers]**. Sélectionnez un fichier .csv sur votre ordinateur pour générer un schéma.

![L’étape Sélectionner des données du workflow Créer un schéma avec la section Télécharger les fichiers mise en surbrillance.](../images/ui/ml-schema-creation/upload-files.png)

### Aperçu des données {#preview-data}

La section [!UICONTROL Télécharger le fichier] affiche le nom du fichier CSV importé et la section **[!UICONTROL Prévisualisation]** affiche des lignes de données d’exemple du fichier que vous avez chargé. Sélectionnez **[!UICONTROL Suivant]** pour continuer le workflow.

![Lignes de données d’exemple mises en surbrillance dans la section d’aperçu et Suivant mis en surbrillance.](../images/ui/ml-schema-creation/preview-data.png)

### Vérifier et modifier le schéma {#review-schema}

L’étape **[!UICONTROL Révision et modification]** du workflow de création s’affiche désormais, affichant la **[!UICONTROL recommandation de schéma]** assistée par machine learning dans une vue tabulée. À ce stade, vous pouvez modifier, ajouter ou supprimer des champs du schéma recommandé généré par le modèle de machine learning. Le tableau contient les champs suivants :

| Nom du champ | Description |
|------------------|---------------------------------------------------------|
| [!UICONTROL Tableau de données] | Jeu de données ou base de données d’où provient le champ. |
| [!UICONTROL Champ Source] | Nom du champ d’origine du système source. |
| [!UICONTROL  Champ cible ] | Nom du champ dans le système cible où les données seront mappées. |
| [!UICONTROL Nom d’affichage] | Nom utilisé pour afficher le champ dans l’interface utilisateur. Ce nom doit être plus convivial ou descriptif. |
| [!UICONTROL Type de données] | Type de données stocké dans le champ (par exemple, `String`, `Date`). |
| [!UICONTROL Groupe de champs] | Catégorisation du champ en fonction de son utilisation ou de son contexte (par exemple, [!UICONTROL Détails démographiques], [!UICONTROL Détails Commerce]). |

![Étape Vérifier et modifier du workflow de création de schéma.](../images/ui/ml-schema-creation/schema-recommendation.png)

#### Ajouter un champ {#add-field}

Pour ajouter un champ au schéma, sélectionnez **[!UICONTROL Ajouter un nouveau champ]**.

![L’étape Vérifier et modifier du workflow de création de schéma avec l’option Ajouter un nouveau champ mise en surbrillance.](../images/ui/ml-schema-creation/add-new-field.png)

La boîte de dialogue [!UICONTROL Sélectionner un champ] s’affiche. La boîte de dialogue contient un diagramme du schéma tel qu’il existe actuellement. Sélectionnez le champ souhaité, puis sélectionnez **[Sélectionner]** pour ajouter un nouveau champ au schéma. Sélectionnez **[Annuler]** pour fermer la boîte de dialogue si nécessaire.

![Boîte de dialogue Sélectionner un champ avec un champ sélectionné et Sélectionner en surbrillance.](../images/ui/ml-schema-creation/select-field-dialog.png)

Une nouvelle ligne s’affiche sur votre schéma recommandé. Vous pouvez maintenant modifier le champ .

#### Modification d’un champ {#edit-field}

Pour modifier un champ, sélectionnez l’icône en forme de crayon de la ligne à modifier. Un panneau de détails s’affiche à droite, où vous pouvez modifier le mappage des champs personnalisés. Le panneau Détails contient les [!UICONTROL Champ cible], [!UICONTROL Nom d’affichage], [!UICONTROL Type de données] et [!UICONTROL Groupe de champs]. Apportez les modifications nécessaires et sélectionnez **[!UICONTROL Appliquer]** pour confirmer. Sélectionnez à nouveau l’icône en forme de crayon pour fermer le panneau des détails.

![L’étape Vérifier et modifier du workflow de création de schéma avec l’icône en forme de crayon et le panneau des détails mis en surbrillance.](../images/ui/ml-schema-creation/edit-field.png)

#### Supprimer un champ {#remove-field}

Pour supprimer un champ, sélectionnez l’icône moins sur une ligne à supprimer.

>[!CAUTION]
>
>Aucune boîte de dialogue de confirmation ne s’affiche lors de la suppression de cet élément.

![L’étape Vérifier et modifier du workflow de création de schéma avec l’icône moins mise en surbrillance.](../images/ui/ml-schema-creation/remove-field.png)

#### Approuver le schéma recommandé {#approve}

Pour approuver le schéma recommandé et poursuivre le workflow **[!UICONTROL Créer un schéma]**, sélectionnez **[Suivant]**.

![L’étape Vérifier et modifier du workflow de création de schéma avec l’option Suivant mise en surbrillance.](../images/ui/ml-schema-creation/next.png)

### Nommer et enregistrer le schéma {#name-and-save}

L’étape **[!UICONTROL Nommer et enregistrer]** du workflow de création s’affiche. Saisissez un **[nom d’affichage du schéma]** et une description facultative. La section **[Schéma généré]** fournit un diagramme du schéma généré par ML. Sélectionnez **[Terminer]** pour terminer le workflow de création de schéma.

![L’étape Nom et Enregistrer le schéma du workflow de création de schéma avec l’option Terminer mise en surbrillance.](../images/ui/ml-schema-creation/name-and-save.png)

### Affichage dans l’éditeur de schémas {#view-in-editor}

L’éditeur de schémas s’affiche avec le schéma que vous venez de créer dans la zone de travail. Sélectionnez **[!UICONTROL Enregistrer]** pour revenir à l’espace de travail [!UICONTROL Schémas].

![Éditeur de schéma affichant le schéma généré par ML nommé.](../images/ui/ml-schema-creation/schema-editor.png)

## Étapes suivantes

Après avoir créé votre schéma, vous pouvez utiliser l’éditeur de schémas pour apporter d’autres modifications, si nécessaire. Votre nouveau schéma est maintenant prêt à être intégré à vos sources de données et utilisé pour l’analyse des données.

Pour plus d’informations sur l’utilisation de l’éditeur de schémas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas#edit) consultez le guide [Modifier un schéma existant ».
