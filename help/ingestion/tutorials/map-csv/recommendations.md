---
title: Mappage d’un fichier CSV à un schéma XDM à l’aide de Recommendations généré par l’IA (bêta)
description: Ce tutoriel explique comment mapper un fichier CSV à un schéma XDM à l’aide de recommandations générées par l’IA.
source-git-commit: d6f858af8bc44be74b1aaf12b973fb6818c1b2a5
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 4%

---

# Mappage d’un fichier CSV à un schéma XDM à l’aide de recommandations générées par l’IA (version bêta)

>[!IMPORTANT]
>
>Cette fonctionnalité est actuellement en version bêta et votre entreprise n’y a peut-être pas encore accès. La documentation et les fonctionnalités peuvent changer.
>
>Pour plus d’informations sur les fonctionnalités de mappage CSV disponibles dans Platform, consultez le document sur [mappage d’un fichier CSV à un schéma existant](./existing-schema.md).

Pour ingérer des données CSV dans [!DNL Adobe Experience Platform], les données doivent être mappées à un [!DNL Experience Data Model] Schéma (XDM). Vous pouvez choisir de mapper sur [un schéma existant ;](./existing-schema.md), mais si vous ne savez pas exactement quel schéma utiliser ou comment il doit être structuré, vous pouvez utiliser des recommandations dynamiques basées sur des modèles d’apprentissage automatique (ML) dans l’interface utilisateur de Platform.

## Prise en main

Ce tutoriel nécessite une compréhension pratique des composants suivants de [!DNL Platform]:

* [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.
   * Vous devez au minimum comprendre le concept de [comportements dans XDM](../../../xdm/home.md#data-behaviors), afin que vous puissiez décider si vous mappez vos données à une [!UICONTROL Profil] classe (comportement d’enregistrement) ou [!UICONTROL ExperienceEvent] classe (comportement de série temporelle).
* [Ingestion par lots](../../batch-ingestion/overview.md)[!DNL Platform] : méthode employée par pour ingérer des données à partir de fichiers de données fournis par l’utilisateur.
* [Préparation de données Adobe Experience Platform](../../batch-ingestion/overview.md): Suite de fonctionnalités permettant de mapper et de transformer des données ingérées pour les rendre conformes aux schémas XDM. La documentation relative à [Fonctions de préparation des données](../../../data-prep/functions.md) est spécifiquement pertinent pour le mappage de schéma.

## Fournir des détails sur le flux de données

Dans l’interface utilisateur de l’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche. Sur le **[!UICONTROL Catalogue]** afficher, accédez à la **[!UICONTROL Système local]** catégorie. Sous **[!UICONTROL Chargement de fichier local]**, sélectionnez **[!UICONTROL Ajouter des données]**.

![Le [!UICONTROL Sources] catalogue dans l’interface utilisateur de Platform, avec [!UICONTROL Ajouter des données] under [!UICONTROL Chargement de fichier local] en cours de sélection](../../images/tutorials/map-csv-recommendations/local-file-upload.png)

Le **[!UICONTROL Mappage du schéma XDM CSV]** s’affiche, en commençant par **[!UICONTROL Détails du flux de données]** étape .

Sélectionner **[!UICONTROL Création d’un nouveau schéma à l’aide de recommandations ML]**, provoquant l’affichage de nouveaux contrôles. Sélectionnez la classe appropriée pour les données CSV que vous souhaitez mapper ([!UICONTROL Profil] ou [!UICONTROL ExperienceEvent]). Vous pouvez éventuellement utiliser le menu déroulant pour sélectionner le secteur d’activité approprié à votre entreprise ou laisser ce champ vide si les catégories fournies ne vous concernent pas. Si votre organisation fonctionne sous une [business-to-business (B2B)](../../../xdm/tutorials/relationship-b2b.md) , sélectionnez le modèle **[!UICONTROL Données B2B]** .

![Le [!UICONTROL Détails du flux de données] avec l’option de recommandation ML sélectionnée. [!UICONTROL Profil] est sélectionné pour la classe et [!UICONTROL Télécommunications] sélectionné pour le secteur](../../images/tutorials/map-csv-recommendations/select-class-and-industry.png)

À partir de là, indiquez un nom pour le schéma qui sera créé à partir des données CSV, ainsi qu’un nom pour le jeu de données de sortie qui contiendra les données ingérées sous ce schéma.

Vous pouvez éventuellement configurer les fonctionnalités supplémentaires suivantes pour le flux de données avant de poursuivre :

| Input name | Description |
| --- | --- |
| [!UICONTROL Description] | Description du flux de données. |
| [!UICONTROL Diagnostics d’erreur] | Lorsque cette option est activée, des messages d’erreur sont générés pour les lots nouvellement ingérés, qui peuvent être affichés lors de la récupération du lot correspondant dans le [API](../../batch-ingestion/api-overview.md). |
| [!UICONTROL Ingestion partielle] | Lorsque cette option est activée, les enregistrements valides pour les nouvelles données de lot sont ingérés dans un seuil d’erreur spécifié. Ce seuil vous permet de configurer le pourcentage d’erreurs acceptables avant l’échec de l’ensemble du lot. |
| [!UICONTROL Détails du flux de données] | Indiquez un nom et une description facultative du flux de données qui amènera les données CSV dans Platform. Un nom par défaut est automatiquement attribué au flux de données lors du démarrage de ce processus. La modification du nom est facultative. |
| [!UICONTROL Alertes] | Effectuer une sélection dans une liste de [alertes in-product](../../../observability/alerts/overview.md) que vous souhaitez recevoir concernant l’état du flux de données une fois qu’il a été lancé. |

{style=&quot;table-layout:auto&quot;}

Lorsque vous avez terminé de configurer le flux de données, sélectionnez **[!UICONTROL Suivant]**.

![Le [!UICONTROL Détails du flux de données] est terminée](../../images/tutorials/map-csv-recommendations/dataflow-detail-complete.png)

## Sélectionner les données

Sur le **[!UICONTROL Sélectionner des données]** utilisez la colonne de gauche pour charger votre fichier CSV. Vous pouvez sélectionner **[!UICONTROL Sélection de fichiers]** pour ouvrir une boîte de dialogue de l’explorateur de fichiers à partir de laquelle sélectionner le fichier, vous pouvez également le faire glisser directement dans la colonne.

![Le [!UICONTROL Sélection de fichiers] zone de bouton et de glisser-déposer mise en surbrillance dans la variable [!UICONTROL Sélectionner des données] step](../../images/tutorials/map-csv-recommendations/upload-files.png)

Une fois le fichier téléchargé, une section d’exemple de données s’affiche. Elle présente les dix premières lignes des données reçues afin que vous puissiez vérifier qu’elles ont bien été chargées. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![Des exemples de lignes de données sont renseignés dans l’espace de travail.](../../images/tutorials/map-csv-recommendations/data-uploaded.png)

## Configuration des mappages de schéma

Les modèles ML sont exécutés pour générer un nouveau schéma basé sur votre configuration de flux de données et votre fichier CSV transféré. Une fois le processus terminé, la variable [!UICONTROL Mappage] Cette étape est renseignée pour afficher les mappages de chaque champ avec une vue entièrement navigable de la structure de schéma générée.

![Le [!UICONTROL Mappage] dans l’interface utilisateur, affichant tous les champs CSV mappés et la structure de schéma résultante.](../../images/tutorials/map-csv-recommendations/schema-generated.png)

À partir de là, vous pouvez éventuellement [modifier les mappages des champs ;](#edit-mappings) ou [modifier les groupes de champs auxquels ils sont associés ;](#edit-schema) selon vos besoins. Lorsque vous êtes satisfait, sélectionnez **[!UICONTROL Terminer]** pour terminer le mappage et lancer le flux de données que vous avez configuré précédemment. Les données CSV sont ingérées dans le système et renseignent un jeu de données basé sur la structure de schéma générée, prêt à être utilisé par les services Platform en aval.

![Le [!UICONTROL Terminer] bouton sélectionné, exécution du processus de mappage CSV](../../images/tutorials/map-csv-recommendations/finish-mapping.png)

### Modifier les mappages de champs {#edit-mappings}

Utilisez l’aperçu du mappage des champs pour modifier les mappages existants ou les supprimer entièrement. Pour plus d’informations sur la gestion d’un jeu de mappages dans l’interface utilisateur, reportez-vous à la section [Guide de l’interface utilisateur pour le mappage de la préparation des données](../../../data-prep/ui/mapping.md#mapping-interface).

### Modifier des groupes de champs {#edit-field-groups}

Les champs CSV sont automatiquement mappés aux groupes de champs XDM existants à l’aide de modèles ML. Si vous souhaitez modifier le groupe de champs d’un champ CSV particulier, sélectionnez **[!UICONTROL Modifier]** en regard de l’arborescence du schéma.

![Le [!UICONTROL Modifier] sélectionné en regard de l’arborescence du schéma](../../images/tutorials/map-csv-recommendations/edit-schema-structure.png)

Une boîte de dialogue s’affiche, vous permettant de modifier le nom d’affichage, le type de données et le groupe de champs de n’importe quel champ du mappage. Sélectionnez l’icône de modification (![Icône Modifier](../../images/tutorials/map-csv-recommendations/edit-icon.png)) en regard d’un champ source pour modifier ses détails dans la colonne de droite avant de sélectionner **[!UICONTROL Appliquer]**.

![Groupe de champs recommandé pour un champ source en cours de modification](../../images/tutorials/map-csv-recommendations/select-schema-field.png)

Lorsque vous avez terminé d’ajuster les recommandations de schéma pour vos champs sources, sélectionnez **[!UICONTROL Enregistrer]** pour appliquer les modifications.

## Étapes suivantes

Ce guide explique comment mapper un fichier CSV à un schéma XDM à l’aide de recommandations générées par l’IA, ce qui vous permet d’importer ces données dans Platform par ingestion par lots.

Pour savoir comment mapper un fichier CSV à un schéma existant, reportez-vous à la section [workflow de mappage de schéma existant](./existing-schema.md). Pour plus d’informations sur la diffusion en continu de données vers Platform en temps réel par le biais de connexions source préconfigurées, reportez-vous à la section [présentation des sources](../../../sources/home.md).
