---
title: Connecter Bombora Intent à Experience Platform à l’aide de l’interface utilisateur
description: Découvrez comment connecter Bombora Intent à Experience Platform
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Édition B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: 76a4fed5-b2d5-46d5-9245-b52792a7d323
source-git-commit: a1af85c6b76cc7bded07ab4acaec9c3213a94397
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 9%

---

# Connexion d’[!DNL Bombora Intent] à Experience Platform à l’aide de l’interface utilisateur

Lisez ce guide pour savoir comment connecter votre compte [!DNL Bombora Intent] à Adobe Experience Platform à l’aide de l’interface utilisateur.

## Commencer

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md) : Real-Time CDP B2B edition est conçu pour les professionnels du marketing travaillant dans un modèle de service business-to-business. Elle rassemble des données provenant de sources multiples et les combine en une vue unique des profils de comptes et d’utilisateurs. Ces données unifiées permettent aux spécialistes marketing de cibler précisément des audiences spécifiques afin de stimuler leur engagement sur tous les canaux disponibles.
* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

### Conditions préalables

Lisez la [[!DNL Bombora Intent] présentation](../../../../connectors/data-partners/bombora.md) pour plus d’informations sur la manière de récupérer vos informations d’authentification.

## Parcourir le catalogue des sources

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail *[!UICONTROL Sources]*. Vous pouvez sélectionner la catégorie appropriée dans le panneau *[!UICONTROL Catégories]*. Vous pouvez également utiliser la barre de recherche pour accéder à la source spécifique que vous souhaitez utiliser.

Pour utiliser [!DNL Bombora], sélectionnez la carte source **[!UICONTROL Intention Bombora]** sous *[!UICONTROL Partenaires de données et d’identité]*, puis sélectionnez **[!UICONTROL Ajouter des données]**.

>[!TIP]
>
>Les sources du catalogue affichent l’option **[!UICONTROL Configurer]** lorsqu’une source donnée ne dispose pas encore d’un compte authentifié. Une fois qu’un compte authentifié existe, cette option devient **[!UICONTROL Ajouter des données]**.

![Le catalogue des sources avec la vignette « Intention de Bombora » sélectionnée.](../../../../images/tutorials/create/bombora/catalog.png)

## Authentification {#authentication}

### Utiliser un compte existant {#existing}

Pour utiliser un compte existant, sélectionnez **[!UICONTROL Compte existant]** puis sélectionnez le compte à utiliser dans la liste des comptes de l’interface.

Une fois votre compte sélectionné, sélectionnez **[!UICONTROL Suivant]** pour passer à l’étape suivante.

![Interface du compte existant dans le workflow des sources.](../../../../images/tutorials/create/bombora/existing.png)

### Créer un nouveau compte {#create}

Si vous ne disposez pas d’un compte existant, vous devez créer un compte en fournissant les informations d’authentification nécessaires qui correspondent à votre source.

Pour créer un compte, sélectionnez **[!UICONTROL Nouveau compte]** puis indiquez un nom de compte et éventuellement une description pour les détails de votre compte. Indiquez ensuite les valeurs d’authentification appropriées pour authentifier votre source par rapport à Experience Platform. Pour connecter votre compte [!DNL Bombora], vous devez disposer des informations d’identification suivantes :

* **ID de la clé d’accès** : votre ID de clé d’accès [!DNL Bombora]. Il s’agit d’une chaîne alphanumérique de 61 caractères requise pour authentifier votre compte auprès d’Experience Platform.
* **Clé d’accès secrète** : votre clé d’accès secrète [!DNL Bombora]. Il s’agit d’une chaîne codée en base 64 de 40 caractères requise pour authentifier votre compte auprès d’Experience Platform.
* **Nom du compartiment** : le compartiment [!DNL Bombora] à partir duquel les données seront extraites.

![Nouvelle interface de compte dans le workflow des sources.](../../../../images/tutorials/create/bombora/new.png)

## Fournir des détails sur le flux de données {#provide-dataflow-details}

Une fois votre compte authentifié et connecté, vous devez fournir les détails suivants pour votre flux de données :

* **Nom du flux de données** : le nom de votre flux de données. Vous pouvez utiliser ce nom pour rechercher votre flux de données dans l’interface utilisateur, une fois qu’il a été créé et traité.
* **Description** : (facultatif) brève explication ou informations supplémentaires pour votre flux de données.
* **Source du domaine** : champ de domaine ou de site web qui correspond aux enregistrements de votre compte source par rapport aux comptes Experience Platform. Cette valeur peut dépendre de vos configurations. S’il n’est pas fourni, le domaine est défini par défaut sur accountOrganization.website.

![Interface des détails du flux de données du workflow des sources.](../../../../images/tutorials/create/bombora/dataflow-detail.png)

## Planifier le flux de données {#schedule-dataflow}

Ensuite, utilisez l’interface de planification pour configurer un planning d’ingestion pour votre flux de données.

* **Fréquence** : configurez la fréquence pour indiquer la fréquence d’exécution du flux de données. Vous pouvez planifier votre flux de données [!DNL Bombora] pour ingérer des données à une fréquence hebdomadaire.
* **Intervalle** : l’intervalle représente la durée écoulée entre chaque cycle d’ingestion. Le seul intervalle pris en charge pour un flux de données [!DNL Bombora] est 1. Cela signifie que votre flux de données ingérera des données une fois par semaine, toutes les semaines.
* **Heure de début** : l’heure de début détermine à quel moment la première itération d’exécution de votre flux de données se produira. [!DNL Bombora] envoie les données à Adobe une fois par semaine, le lundi, à 12 h 00 UTC. Par conséquent, vous devez définir l’heure de début de l’ingestion après 12h00 UTC. En outre, vous devez confirmer l’heure d’ingestion avec [!DNL Bombora], car ils peuvent modifier leur planning lors de l’envoi de fichiers vers Adobe.

Une fois que vous avez configuré le planning d’ingestion de votre flux de données, sélectionnez **[!UICONTROL Suivant]**.

![Interface de planification du workflow des sources.](../../../../images/tutorials/create/bombora/scheduling.png)

## Vérifier le flux de données {#review-dataflow}

La dernière étape du processus de création de flux de données consiste à vérifier votre flux de données avant de l’exécuter. Utilisez l’étape *[!UICONTROL Réviser]* pour passer en revue les détails de votre nouveau flux de données avant son exécution. Les détails sont regroupés dans les catégories suivantes :

* **Connexion** : affiche le type de source, le chemin d’accès correspondant au fichier source choisi et le nombre de colonnes au sein de ce fichier source.
* **Planification** : affiche la période active, la fréquence et l’intervalle du planning d’ingestion.

Une fois que vous avez révisé votre flux de données, sélectionnez **[!UICONTROL Terminer]**.

![Interface de révision du workflow des sources.](../../../../images/tutorials/create/bombora/review.png)

## Étapes suivantes

Ce tutoriel vous a permis de créer un flux de données pour importer les données d’intention de votre source de [!DNL Bombora] vers Experience Platform. Pour obtenir des ressources supplémentaires, consultez la documentation décrite ci-dessous.

### Surveiller votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées et afficher les informations relatives au taux d’ingestion, aux succès et aux erreurs. Pour plus d’informations sur la surveillance des flux de données, consultez le tutoriel sur la [surveillance des comptes et des flux de données dans l’interface utilisateur](../../../../../dataflows/ui/monitor-sources.md).

### Mettre à jour votre flux de données

Pour mettre à jour les configurations pour la planification, le mappage et les informations générales de vos flux de données, consultez le tutoriel sur la [mise à jour des flux de données sources dans l’interface utilisateur](../../update-dataflows.md).

### Supprimer le flux de données

Vous pouvez supprimer les flux de données qui ne sont plus nécessaires ou qui ont été créés de manière incorrecte à l’aide de la fonction **[!UICONTROL Supprimer]**, disponible dans l’espace de travail **[!UICONTROL Flux de données]**. Pour plus d’informations sur la suppression des flux de données, consultez le tutoriel sur la [suppression de flux de données dans l’interface utilisateur](../../delete.md).
