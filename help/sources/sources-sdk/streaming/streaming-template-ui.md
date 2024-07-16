---
title: Modèle de documentation en libre-service pour l’interface utilisateur du SDK de diffusion en continu
description: Découvrez comment importer des données en continu d’une source vers Adobe Experience Platform à l’aide de l’interface utilisateur.
exl-id: 82254be0-fa31-4114-a0ec-179a990e0904
badge: Version bêta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 19%

---

# Créez une connexion source et un flux de données pour diffuser des données *YOURSOURCE* à l’aide de l’interface utilisateur.

*Lorsque vous parcourez ce modèle, remplacez ou supprimez tous les paragraphes en italique (en commençant par celui-ci).*

*Commencez par mettre à jour les métadonnées (titre et description) en haut de la page. Ignorez toutes les instances d’UICONTROL sur cette page. Il s’agit d’une balise qui aide nos processus de traduction automatique à traduire correctement la page dans les multiples langues prises en charge. Nous ajouterons des balises à votre documentation après l’avoir envoyée.*

Ce tutoriel décrit les étapes à suivre pour créer un connecteur source *YOURSOURCE* à l’aide de l’interface utilisateur de Platform.

## Vue d’ensemble

*Fournissez un bref aperçu de votre entreprise, y compris la valeur qu’elle fournit aux clients. Insérez un lien vers la page d’accueil de la documentation du produit pour une lecture plus approfondie.*

>[!IMPORTANT]
>
>Ce connecteur source et cette page de documentation sont créés et conservés par l’équipe *YOURSOURCE*. Pour toute demande de mise à jour ou de demande de mise à jour, contactez-les directement à l&#39;adresse *Ajouter un lien ou une adresse email où vous pouvez accéder pour les mises à jour*.

## Conditions préalables

*Ajoutez dans cette section des informations sur tout ce dont les clients doivent tenir compte avant de commencer à configurer la source dans l’interface utilisateur de Adobe Experience Platform. Il peut s’agir de :*

* *à ajouter à une liste autorisée*
* *Conditions requises pour le hachage des emails*
* *toutes les caractéristiques de compte de votre côté*
* *Comment obtenir les informations d’authentification pour se connecter à votre plateforme*

### Collecter les informations d’identification requises

Pour connecter *YOURSOURCE* à Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| *identifiant one* | *Ajoutez une brève description aux informations d’identification d’authentification de votre source ici* | *Ajoutez ici un exemple d&#39;informations d&#39;identification d&#39;authentification de votre source* |
| *credential two* | *Ajoutez une brève description aux informations d’identification d’authentification de votre source ici* | *Ajoutez ici un exemple d&#39;informations d&#39;identification d&#39;authentification de votre source* |
| *credential trois* | *Ajoutez une brève description aux informations d’identification d’authentification de votre source ici* | *Ajoutez ici un exemple d&#39;informations d&#39;identification d&#39;authentification de votre source* |

Pour plus d’informations sur ces informations d’identification, consultez la documentation d’authentification *YOURSOURCE*. *Ajoutez un lien vers la documentation d’authentification de votre plateforme ici*.

### Intégrer *YOURSOURCE* à votre webhook

*Le SDK de diffusion en continu nécessite que votre source puisse prendre en charge les webhooks pour communiquer avec un Experience Platform. Dans cette section, vous devez indiquer les étapes que vos utilisateurs devront suivre pour intégrer VOTRE SOURCE à un webhook.*

## Connectez votre compte *YOURSOURCE*

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie **Diffusion en continu**, sélectionnez *YOURSOURCE*, puis sélectionnez **[!UICONTROL Ajouter des données]**.

>[!TIP]
>
>Les captures d’écran utilisées ci-dessous sont des exemples. Lors de la création de votre documentation, veuillez remplacer les images par des captures d’écran de votre source réelle. Vous pouvez utiliser le même motif de marquage et la même couleur, ainsi que les mêmes noms de fichier. Assurez-vous que votre capture d’écran capture tout l’écran de l’interface utilisateur de Platform. Pour plus d’informations sur la manière de charger vos captures d’écran, consultez le guide sur l’ [envoi de votre documentation en vue de la révision](../documentation/github.md).

![Catalogue des sources Experience Platform](../assets/streaming/catalog.png)

## Sélectionner les données

L’étape **[!UICONTROL Sélectionner les données]** s’affiche, vous permettant ainsi de sélectionner les données que vous apportez à Platform.

* La partie gauche de l’interface est un navigateur qui vous permet d’afficher les flux de données disponibles dans votre compte ;
* La partie droite de l’interface vous permet de prévisualiser jusqu’à 100 lignes de données à partir d’un fichier JSON.

Sélectionnez **[!UICONTROL Télécharger des fichiers]** pour charger un fichier JSON à partir de votre système local. Vous pouvez également faire glisser et déposer le fichier JSON que vous souhaitez charger dans le panneau [!UICONTROL Glisser-déposer des fichiers].

![L’étape d’ajout de données du workflow des sources.](../assets/streaming/add-data.png)

Une fois le fichier chargé, l’interface de prévisualisation se met à jour pour afficher un aperçu du schéma que vous avez chargé. L’interface d’aperçu vous permet d’examiner le contenu et la structure d’un fichier. Vous pouvez également utiliser l’utilitaire [!UICONTROL Search field] pour accéder à des éléments spécifiques à partir de votre schéma.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![L’étape d’aperçu du workflow des sources.](../assets/streaming/preview.png)

## Détails du flux de données

L’étape **Détails du flux de données** s’affiche, vous fournissant des options permettant d’utiliser un jeu de données existant ou d’établir un nouveau jeu de données pour votre flux de données, ainsi qu’une opportunité de fournir un nom et une description pour votre flux de données. Au cours de cette étape, vous pouvez également configurer des paramètres pour l’ingestion de profils, les diagnostics d’erreur, l’ingestion partielle et les alertes.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.

![L’étape de détail du flux de données du flux de sources.](../assets/streaming/dataflow-detail.png)

## Mappage

L’interface de [!UICONTROL mappage] fournit un outil complet pour mapper les champs sources de votre schéma source aux champs XDM cibles correspondants dans le schéma cible.

Platform fournit des recommandations intelligentes pour les champs mappés automatiquement en fonction du schéma ou du jeu de données cible que vous avez sélectionné. Vous pouvez ajuster manuellement les règles de mappage en fonction de vos cas d’utilisation. Selon vos besoins, vous pouvez choisir de mapper directement des champs ou d’utiliser des fonctions de préparation de données pour transformer les données sources afin d’obtenir des valeurs informatisées ou calculées. Pour obtenir des instructions complètes sur l’utilisation de l’interface du mappeur et des champs calculés, consultez le [guide de l’interface utilisateur de la préparation des données](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Une fois le mappage de vos données source réussi, sélectionnez **[!UICONTROL Suivant]**.

![L’étape de mappage du workflow des sources.](../assets/streaming/mapping.png)

## Révision

L’écran de **[!UICONTROL Révision]** s’affiche, vous permettant dʼexaminer votre nouveau flux de données avant sa création. Les détails sont regroupés dans les catégories suivantes :

* **[!UICONTROL Connexion]** : affiche le type de source, le chemin d’accès correspondant au fichier source choisi et le nombre de colonnes au sein de ce fichier source.
* **[!UICONTROL Attribuer des champs de jeu de données et de mappage]** : affiche le jeu de données dans lequel les données sources sont ingérées, y compris le schéma auquel le jeu de données se conforme.

Une fois que vous avez examiné votre flux de données, cliquez sur **[!UICONTROL Terminer]** et laissez un certain temps pour créer le flux de données.

![L’étape de révision du workflow des sources.](../assets/streaming/review.png)

## Obtention de l’URL de votre point de terminaison de diffusion

Une fois votre flux de données de diffusion en continu créé, vous pouvez désormais récupérer l’URL de votre point de terminaison de diffusion en continu. Ce point de terminaison sera utilisé pour s’abonner à votre webhook, ce qui permet à votre source de diffusion en continu de communiquer avec l’Experience Platform.

Pour récupérer votre point de terminaison de diffusion en continu, accédez à la page [!UICONTROL Activité Flux de données] du flux de données que vous venez de créer et copiez le point de terminaison depuis le bas du panneau [!UICONTROL Propriétés].

![Le point d’entrée de diffusion en continu dans l’activité de flux de données.](../assets/testing/endpoint-test.png)

## Étapes suivantes

*Les workflows pour les étapes restantes de la création d’un flux de données sont modulaires. Si vous souhaitez effectuer des appels d’urgence spécifiques concernant votre source, reportez-vous à la section Ressources supplémentaires ci-dessous.*

En suivant ce tutoriel, vous avez établi une connexion à votre compte *YOURSOURCE*. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Ressources supplémentaires

*Il s’agit d’une section facultative dans laquelle vous pouvez fournir d’autres liens vers la documentation de votre produit ou toute autre étape, captures d’écran et nuances jugées importantes pour le succès du client. Vous pouvez utiliser cette section pour ajouter des informations ou des conseils sur l&#39;ensemble du workflow de votre source, en particulier s&#39;il existe des &quot;pièges&quot; particuliers qu&#39;un utilisateur final peut rencontrer.*
