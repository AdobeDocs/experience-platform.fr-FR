---
keywords: Experience Platform;accueil;rubriques populaires;connecteur source Marketo;connecteur Marketo;source Marketo;Marketo
solution: Experience Platform
title: Création d’un connecteur source de Marketo Engage dans l’interface utilisateur
topic-legacy: overview
type: Tutorial
description: Ce tutoriel décrit les étapes à suivre pour créer un connecteur source de Marketo Engage dans l’interface utilisateur afin d’importer des données B2B dans Adobe Experience Platform.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 9c8b63bf577a4258a7ef87c11bc8f87c1a01cc20
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 6%

---

# Création d’un connecteur source [!DNL Marketo Engage] dans l’interface utilisateur

Ce tutoriel décrit les étapes de création d’un connecteur source [!DNL Marketo Engage] (ci-après appelé &quot;[!DNL Marketo]&quot;) dans l’interface utilisateur pour importer des données B2B dans Adobe Experience Platform.

## Prise en main

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Modèle de données d’expérience (XDM)](../../../../../xdm/home.md) : Cadre normalisé selon lequel l’Experience Platform organise les données d’expérience client.
   * [Création et modification de schémas dans l’interface utilisateur](../../../../../xdm/ui/resources/schemas.md) : Découvrez comment créer et modifier des schémas dans l’interface utilisateur.
* [Espaces de noms d’identité](../../../../../identity-service/namespaces.md) : Les espaces de noms d’identité sont des composants de  [!DNL Identity Service] qui servent d’indicateurs du contexte auquel une identité se rapporte. Une identité complète est composée d’une valeur d’identifiant et d’un espace de noms.
* [[!DNL Real-time Customer Profile]](/help/profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

### Collecte des informations d’identification requises

Pour accéder à votre compte [!DNL Marketo] sur Platform, vous devez fournir les valeurs suivantes :

| Credential | Description |
| ---------- | ----------- |
| `munchkinId` | L’identifiant Munchkin est l’identifiant unique d’une instance [!DNL Marketo] spécifique. |
| `clientId` | L’identifiant client unique de votre instance [!DNL Marketo]. |
| `clientSecret` | Le secret client unique de votre instance [!DNL Marketo]. |

Pour plus d’informations sur l’acquisition de ces valeurs, consultez le [[!DNL Marketo] guide d’authentification](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Une fois que vous avez rassemblé les informations d’identification requises, vous pouvez suivre les étapes de la section suivante.

## Connectez votre compte [!DNL Marketo]

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources pour lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de la barre de recherche.

Dans la catégorie [!UICONTROL Adobe des applications] , sélectionnez **[!UICONTROL Marketo Engage]**. Sélectionnez ensuite **[!UICONTROL Ajouter des données]** pour créer un nouveau flux de données [!DNL Marketo].

![catalogue](../../../../images/tutorials/create/marketo/catalog.png)

La page **[!UICONTROL Se connecter à Marketo Engage]** s’affiche. Sur cette page, vous pouvez utiliser un nouveau compte ou accéder à un compte existant.

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**. Dans le formulaire de saisie qui s’affiche, indiquez un nom de compte, une description facultative et vos informations d’authentification [!DNL Marketo]. Une fois que vous avez terminé, sélectionnez **[!UICONTROL Se connecter à la source]**, puis laissez un certain temps pour établir la nouvelle connexion.

![new-account](../../../../images/tutorials/create/marketo/new.png)

### Compte existant

Pour créer un flux de données avec un compte existant, sélectionnez **[!UICONTROL Compte existant]**, puis le compte [!DNL Marketo] à utiliser. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../../../../images/tutorials/create/marketo/existing.png)

## Sélection d’un jeu de données

Après avoir créé votre compte [!DNL Marketo], l’étape suivante fournit une interface vous permettant d’explorer les jeux de données [!DNL Marketo].

La moitié gauche de l’interface est un navigateur de répertoires qui affiche les 10 jeux de données [!DNL Marketo]. Une connexion source [!DNL Marketo] fonctionnelle nécessite l’ingestion des neuf jeux de données différents. Si vous utilisez également la fonction de marketing basé sur les comptes (ABM) [!DNL Marketo], vous devez également créer un 10e flux de données pour ingérer le jeu de données [!UICONTROL Comptes nommés] .

>[!NOTE]
>
>À des fins de concision, le tutoriel suivant utilise comme exemple [!UICONTROL Comptes nommés] , mais les étapes décrites ci-dessous s’appliquent à l’un des 10 jeux de données [!DNL Marketo].

Sélectionnez d’abord le jeu de données à ingérer, puis sélectionnez **[!UICONTROL Suivant]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## Faire correspondre les schémas [!DNL Marketo] à Platform

L’étape [!UICONTROL Mappage] s’affiche, fournissant une interface pour mapper les schémas [!DNL Marketo] à Platform.

Sélectionnez un jeu de données dans lequel ingérer les données entrantes. Vous pouvez utiliser un jeu de données existant ou en créer un nouveau.

### Utilisation d’un jeu de données existant

Pour ingérer des données dans un jeu de données existant, sélectionnez **[!UICONTROL Jeu de données existant]**, puis sélectionnez l’icône du jeu de données.

![existing-dataset](../../../../images/tutorials/create/marketo/existing-dataset.png)

La boîte de dialogue **[!UICONTROL Sélectionner un jeu de données]** s’affiche. Recherchez le jeu de données avec le schéma approprié que vous souhaitez utiliser, sélectionnez-le, puis sélectionnez **[!UICONTROL Confirmer]**.

![select-existing-dataset](../../../../images/tutorials/create/marketo/select-dataset.png)

### Utilisation d’un nouveau jeu de données

Pour ingérer des données dans un nouveau jeu de données, sélectionnez **[!UICONTROL Nouveau jeu de données]** et saisissez un nom et une description pour le jeu de données dans les champs fournis.

Vous pouvez rechercher un schéma en saisissant son nom dans la barre de recherche **[!UICONTROL Sélectionner le schéma]**. Vous pouvez également sélectionner l’icône de liste déroulante pour afficher la liste des schémas existants. Vous pouvez également sélectionner **[!UICONTROL Recherche avancée]** pour accéder à la page des schémas existants, y compris leurs détails respectifs.

Activez le bouton **[!UICONTROL Jeu de données de profil]** pour activer votre jeu de données cible pour [!DNL Profile], ce qui vous permet de créer une vue holistique des attributs et des comportements d’une entité. Les données de tous les [!DNL Profile] jeux de données activés seront inclus dans [!DNL Profile] et des modifications sont appliquées lorsque vous enregistrez votre flux de données.

![create-new-dataset](../../../../images/tutorials/create/marketo/new-dataset-schema.png)

Une fois que vous avez sélectionné un schéma, faites défiler l’écran vers le bas pour afficher la boîte de dialogue de mappage afin de commencer à mapper vos champs de jeu de données [!DNL Marketo] aux champs XDM cibles appropriés.

### Mappage de vos champs source de jeu de données [!DNL Marketo] pour cibler les champs XDM

Chaque jeu de données [!DNL Marketo] comporte ses propres règles de mappage spécifiques à suivre. Pour plus d’informations sur la façon de mapper des jeux de données [!DNL Marketo] à XDM, voir :

* [Activités](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Programmes](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Abonnements au programme](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Sociétés](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Listes statiques](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [Abonnements à des listes statiques](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Comptes nommés](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Opportunités](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Rôles de contact d’opportunité](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Personnes](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

Sélectionnez **[!UICONTROL Aperçu des données]** pour afficher les résultats du mappage en fonction du jeu de données sélectionné.

![mapping](../../../../images/tutorials/create/marketo/mapping.png)

La fenêtre contextuelle [!UICONTROL Aperçu] vous offre une interface pour explorer les résultats de mappage de jusqu’à 100 lignes de données d’exemple du jeu de données sélectionné.

![aperçu](../../../../images/tutorials/create/marketo/mapping-preview.png)

Une fois vos champs sources mappés aux champs cibles appropriés, sélectionnez **[!UICONTROL Fermer]**.

## Fournir des détails sur les flux de données

L’étape [!UICONTROL Détails du flux de données] s’affiche, ce qui vous permet de fournir un nom et une brève description de votre nouveau flux de données.

![dataflow-detail](../../../../images/tutorials/create/marketo/dataflow-detail.png)

Activez le bouton d’activation/désactivation **[!UICONTROL Diagnostic des erreurs]** afin de permettre la génération détaillée des messages d’erreur pour les lots nouvellement ingérés, que vous pouvez télécharger à l’aide de l’API. Pour plus d’informations, consultez le tutoriel sur la [récupération des diagnostics d’erreur d’ingestion de données](../../../../../ingestion/quality/error-diagnostics.md).

![errors](../../../../images/tutorials/create/marketo/errors.png)

Le connecteur [!DNL Marketo] utilise l’ingestion par lots pour ingérer tous les enregistrements historiques et utilise l’ingestion par flux pour les mises à jour en temps réel. Cela permet au connecteur de continuer la diffusion en continu tout en ingérant des enregistrements erronés. Activez le bouton d’activation/désactivation **[!UICONTROL Ingestion partielle]** , puis définissez le [!UICONTROL seuil d’erreur %] sur le maximum pour empêcher l’échec du flux de données.

**[!UICONTROL L’]** ingestion partielle permet d’ingérer des données contenant des erreurs jusqu’à un certain seuil. Pour plus d’informations, consultez la [présentation de l’ingestion par lots partielle](../../../../../ingestion/batch-ingestion/partial.md).

Une fois que vous avez fourni les détails de votre flux de données et défini votre seuil d’erreur sur max, sélectionnez **[!UICONTROL Suivant]**.

![ingestion partielle](../../../../images/tutorials/create/marketo/partial-ingestion.png)

## Vérification du flux de données

L’étape **[!UICONTROL Réviser]** s’affiche, ce qui vous permet de passer en revue votre nouveau flux de données avant qu’il ne soit créé. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : Affiche le type de source, le chemin d’accès approprié de l’entité source choisie et la quantité de colonnes au sein de cette entité source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : Affiche le jeu de données dans lequel les données source sont ingérées, y compris le schéma auquel le jeu de données adhère.

Une fois que vous avez examiné votre flux de données, sélectionnez **[!UICONTROL Terminer]** et laissez un certain temps pour que le flux de données soit créé.

![review](../../../../images/tutorials/create/marketo/review.png)

## Surveillance de votre flux de données

Une fois votre flux de données créé, vous pouvez surveiller les données ingérées pour afficher des informations sur les taux d’ingestion, les succès et les erreurs. Pour plus d’informations sur la manière de surveiller les flux de données, consultez le tutoriel sur la [surveillance des flux de données dans l’interface utilisateur](../../../../../dataflows/ui/monitor-sources.md).

## Suppression des attributs

Les attributs personnalisés des jeux de données ne peuvent pas être masqués ni supprimés rétroactivement. Si vous souhaitez masquer ou supprimer un attribut personnalisé d’un jeu de données existant, vous devez créer un nouveau jeu de données sans cet attribut personnalisé, un nouveau schéma XDM et configurer un nouveau flux de données pour le nouveau jeu de données que vous créez. Vous devez également désactiver ou supprimer le flux de données d’origine constitué du jeu de données avec l’attribut personnalisé que vous souhaitez masquer ou supprimer.

## Suppression de votre flux de données

Vous pouvez supprimer les flux de données qui ne sont plus nécessaires ou qui ont été créés de manière incorrecte à l’aide de la fonction **[!UICONTROL Supprimer]** disponible dans l’espace de travail [!UICONTROL Flux de données]. Pour plus d’informations sur la suppression des flux de données, consultez le tutoriel sur la [suppression des flux de données dans l’interface utilisateur](../../delete.md).

## Étapes suivantes

En suivant ce tutoriel, vous avez créé un flux de données pour importer des données [!DNL Marketo]. Les données entrantes peuvent désormais être utilisées par les services Platform en aval tels que [!DNL Real-time Customer Profile] et [!DNL Data Science Workspace]. Pour plus d’informations, consultez les documents suivants :

* [Présentation d’[!DNL Real-time Customer Profile]](/help/profile/home.md)
* [Présentation d’[!DNL Data Science Workspace]](/help/data-science-workspace/home.md)
