---
title: Modèle de documentation en libre-service pour l’interface utilisateur du SDK de diffusion en continu
description: Découvrez comment importer des données en continu d’une source vers Adobe Experience Platform à l’aide de l’interface utilisateur.
exl-id: 82254be0-fa31-4114-a0ec-179a990e0904
badge: Version Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 19%

---

# Création d’une connexion source et d’un flux de données pour la diffusion *YOURSOURCE* données utilisant l’interface utilisateur

*Lorsque vous parcourez ce modèle, remplacez ou supprimez tous les paragraphes en italique (en commençant par celui-ci).*

*Commencez par mettre à jour les métadonnées (titre et description) en haut de la page. Ignorez toutes les instances d’UICONTROL sur cette page. Il s’agit d’une balise qui aide nos processus de traduction automatique à traduire correctement la page dans les multiples langues prises en charge. Nous ajouterons des balises à votre documentation après l’avoir envoyée.*

Ce tutoriel décrit les étapes à suivre pour créer une *YOURSOURCE* connecteur source à l’aide de l’interface utilisateur de Platform.

## Vue d’ensemble

*Fournissez un bref aperçu de votre entreprise, y compris la valeur qu’elle fournit aux clients. Pour plus d’informations, insérez un lien vers la page d’accueil de la documentation du produit.*

>[!IMPORTANT]
>
>Cette page de documentation et de connecteur source est créée et conservée par *YOURSOURCE* l&#39;équipe. Pour toute demande d’information ou de mise à jour, contactez-les directement à l’adresse *Ajouter un lien ou une adresse électronique permettant d’accéder aux mises à jour*.

## Conditions préalables

*Ajoutez dans cette section des informations sur tout ce dont les clients doivent tenir compte avant de commencer à configurer la source dans l’interface utilisateur de Adobe Experience Platform. Il peut s’agir :*

* *à ajouter à une liste autorisée*
* *conditions requises pour le hachage des emails*
* *toute spécification de compte de votre côté ;*
* *comment obtenir les informations d’authentification pour se connecter à votre plateforme*

### Collecter les informations d’identification requises

Pour vous connecter *YOURSOURCE* Pour Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| *identifiant un* | *Ajoutez ici une brève description des informations d’identification d’authentification de votre source.* | *Ajoutez ici un exemple d’informations d’identification d’authentification de votre source.* |
| *credential two* | *Ajoutez ici une brève description des informations d’identification d’authentification de votre source.* | *Ajoutez ici un exemple d’informations d’identification d’authentification de votre source.* |
| *identification d’identification trois* | *Ajoutez ici une brève description des informations d’identification d’authentification de votre source.* | *Ajoutez ici un exemple d’informations d’identification d’authentification de votre source.* |

Pour plus d’informations sur ces informations d’identification, voir *YOURSOURCE* documentation d’authentification. *Veuillez ajouter un lien vers la documentation d’authentification de votre plateforme ici*.

### Intégrer *YOURSOURCE* avec votre webhook

*Le SDK de diffusion en continu nécessite que votre source puisse prendre en charge les webhooks pour communiquer avec l’Experience Platform. Dans cette section, vous devez indiquer les étapes que vos utilisateurs devront suivre pour intégrer VOTRE SOURCE à un webhook.*

## Connectez-vous à *YOURSOURCE* account

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , **Diffusion en continu** catégorie, sélectionnez *YOURSOURCE*, puis sélectionnez **[!UICONTROL Ajouter des données]**.

>[!TIP]
>
>Les captures d’écran utilisées ci-dessous sont des exemples. Lors de la création de votre documentation, veuillez remplacer les images par des captures d’écran de votre source réelle. Vous pouvez utiliser le même motif de marquage et la même couleur, ainsi que les mêmes noms de fichier. Assurez-vous que votre capture d’écran capture tout l’écran de l’interface utilisateur de Platform. Pour plus d’informations sur le téléchargement de vos captures d’écran, consultez le guide sur [Envoi de votre documentation en révision](../documentation/github.md).

![Catalogue des sources Experience Platform](../assets/streaming/catalog.png)

## Sélectionner les données

La variable **[!UICONTROL Sélectionner des données]** s’affiche, fournissant une interface vous permettant de sélectionner les données que vous apportez à Platform.

* La partie gauche de l’interface est un navigateur qui vous permet d’afficher les flux de données disponibles dans votre compte ;
* La partie droite de l’interface vous permet de prévisualiser jusqu’à 100 lignes de données à partir d’un fichier JSON.

Sélectionner **[!UICONTROL Chargement de fichiers]** pour charger un fichier JSON à partir de votre système local. Vous pouvez également faire glisser et déposer le fichier JSON que vous souhaitez charger dans le [!UICONTROL Glisser-déposer des fichiers] du panneau.

![L’étape d’ajout de données du workflow des sources.](../assets/streaming/add-data.png)

Une fois le fichier chargé, l’interface de prévisualisation se met à jour pour afficher un aperçu du schéma que vous avez chargé. L’interface d’aperçu vous permet d’examiner le contenu et la structure d’un fichier. Vous pouvez également utiliser la variable [!UICONTROL Champ de recherche] pour accéder à des éléments spécifiques de votre schéma.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![L’étape d’aperçu du workflow des sources.](../assets/streaming/preview.png)

## Détails du flux de données

La variable **Détails du flux de données** s’affiche, vous fournissant des options permettant d’utiliser un jeu de données existant ou d’établir un nouveau jeu de données pour votre flux de données, ainsi qu’une opportunité de fournir un nom et une description pour votre flux de données. Au cours de cette étape, vous pouvez également configurer des paramètres pour l’ingestion de profils, les diagnostics d’erreur, l’ingestion partielle et les alertes.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![L’étape de détail du flux de données du processus des sources.](../assets/streaming/dataflow-detail.png)

## Mappage

L’interface de [!UICONTROL mappage] fournit un outil complet pour mapper les champs sources de votre schéma source aux champs XDM cibles correspondants dans le schéma cible.

Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, voir la section [Guide de l’interface utilisateur de la préparation de données](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Une fois le mappage de vos données source réussi, sélectionnez **[!UICONTROL Suivant]**.

![L’étape de mappage du workflow des sources.](../assets/streaming/mapping.png)

## Révision

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le type de source, le chemin d’accès correspondant au fichier source choisi et le nombre de colonnes au sein de ce fichier source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois le flux de données examiné, cliquez sur **[!UICONTROL Terminer]** et accorder un certain temps pour la création du flux de données.

![L’étape de révision du processus des sources.](../assets/streaming/review.png)

## Obtention de l’URL de votre point de terminaison de diffusion

Une fois votre flux de données de diffusion en continu créé, vous pouvez désormais récupérer l’URL de votre point de terminaison de diffusion en continu. Ce point de terminaison sera utilisé pour s’abonner à votre webhook, ce qui permet à votre source de diffusion en continu de communiquer avec l’Experience Platform.

Pour récupérer votre point de terminaison de diffusion en continu, accédez à la [!UICONTROL Activité Flux de données] de la page du flux de données que vous venez de créer et de copier le point de terminaison depuis le bas de la page [!UICONTROL Propriétés] du panneau.

![Point de terminaison de diffusion en continu dans l’activité de flux de données.](../assets/testing/endpoint-test.png)

## Étapes suivantes

*Les workflows pour les étapes restantes de la création d’un flux de données sont modulaires. Si vous souhaitez effectuer des appels spécifiques concernant votre source, reportez-vous à la section Ressources supplémentaires ci-dessous.*

En suivant ce tutoriel, vous avez établi une connexion à votre *YOURSOURCE* compte . Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Ressources supplémentaires

*Il s’agit d’une section facultative dans laquelle vous pouvez fournir d’autres liens vers la documentation de votre produit ou toute autre étape, captures d’écran, nuances que vous considérez importantes pour que le client réussisse. Vous pouvez utiliser cette section pour ajouter des informations ou des conseils sur l’ensemble du workflow de votre source, en particulier s’il existe des &quot;pièges&quot; particuliers qu’un utilisateur final peut rencontrer.*
