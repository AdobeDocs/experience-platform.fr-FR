---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Modèle de documentation en libre-service pour l’interface utilisateur
description: Découvrez comment créer une connexion source YOURSOURCE à l’aide de l’interface utilisateur de Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 39accd28edc388c6444910f9a2ea6d2f01acfdaf
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---

# Créez un *VOTRE SOURCE* connexion source dans l’interface utilisateur

*Lorsque vous parcourez ce modèle, remplacez ou supprimez tous les paragraphes en italique (en commençant par celui-ci).*

*Commencez par mettre à jour les métadonnées (titre et description) en haut de la page. Veuillez ignorer toutes les instances d&#39;UICONTROL sur cette page. Il s’agit d’une balise qui aide nos processus de traduction automatique à traduire correctement la page dans les multiples langues prises en charge. Nous ajouterons des balises à votre documentation après l’avoir envoyée.*

Ce tutoriel décrit les étapes à suivre pour créer une *VOTRE SOURCE* connecteur source à l’aide de l’interface utilisateur de Platform.

## Présentation

*Fournissez un bref aperçu de votre entreprise, y compris la valeur qu’elle fournit aux clients. Pour plus d’informations, insérez un lien vers la page d’accueil de la documentation du produit.*

>[!IMPORTANT]
>
>Cette page de documentation a été créée par la fonction *VOTRE SOURCE* l&#39;équipe. Pour toute demande de mise à jour ou de renseignements, contactez-les directement à l’adresse *Ajouter un lien ou une adresse électronique permettant d’accéder aux mises à jour*.

## Conditions préalables

*Ajoutez dans cette section des informations sur tout ce dont les clients doivent tenir compte avant de commencer à configurer la source dans l’interface utilisateur de Adobe Experience Platform. Il peut s’agir :*

* *à ajouter à une liste autorisée*
* *conditions requises pour le hachage des emails*
* *toute spécification de compte de votre côté ;*
* *comment obtenir les informations d’authentification pour se connecter à votre plateforme*

### Collecte des informations d’identification requises

Pour vous connecter *VOTRE SOURCE* Pour Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Credential | Description | Exemple |
| --- | --- | --- |
| *identifiant un* | *Ajoutez ici une brève description des informations d’identification d’authentification de votre source.* | *Ajoutez ici un exemple d’informations d’identification d’authentification de votre source.* |
| *credential two* | *Ajoutez ici une brève description des informations d’identification d’authentification de votre source.* | *Ajoutez ici un exemple d’informations d’identification d’authentification de votre source.* |
| *identifiant trois* | *Ajoutez ici une brève description des informations d’identification d’authentification de votre source.* | *Ajoutez ici un exemple d’informations d’identification d’authentification de votre source.* |

Pour plus d’informations sur ces informations d’identification, voir *VOTRE SOURCE* documentation d’authentification. *Veuillez ajouter un lien vers la documentation d’authentification de votre plateforme ici*.

## Connectez-vous à *VOTRE SOURCE* account

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder au [!UICONTROL Sources] workspace. Le [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous , *LA CATÉGORIE DE VOTRE SOURCE* catégorie, sélectionnez *VOTRE SOURCE*, puis sélectionnez **[!UICONTROL Ajouter des données]**.

>[!TIP]
>
>Les captures d’écran utilisées ci-dessous sont des exemples. Lors de la création de votre documentation, veuillez remplacer les images par des captures d’écran de votre source réelle. Vous pouvez utiliser le même motif de marquage et la même couleur, ainsi que les mêmes noms de fichier. Assurez-vous que votre capture d’écran capture tout l’écran de l’interface utilisateur de Platform. Pour plus d’informations sur le téléchargement de vos captures d’écran, consultez le guide sur [Envoi de votre documentation en révision](./github.md).

![catalogue](../assets/ui/catalog.png)

Le **[!UICONTROL Connexion à votre compte SOURCE]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez la variable *VOTRE SOURCE* compte avec lequel vous souhaitez créer un nouveau flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../assets/ui/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et vos informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]** puis accorder un certain temps pour établir la nouvelle connexion.

![new](../assets/ui/new.png)

## Étapes suivantes

*Les workflows pour les étapes restantes de la création d’un flux de données sont modulaires. Si vous souhaitez effectuer des appels spécifiques concernant votre source, reportez-vous à la section Ressources supplémentaires ci-dessous.*

En suivant ce tutoriel, vous avez établi une connexion à votre *VOTRE SOURCE* compte . Vous pouvez maintenant passer au tutoriel suivant et [configuration d’un flux de données pour importer des données dans Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Ressources supplémentaires

*Il s’agit d’une section facultative dans laquelle vous pouvez fournir d’autres liens vers la documentation de votre produit ou toute autre étape, captures d’écran, nuances que vous considérez importantes pour que le client réussisse. Vous pouvez utiliser cette section pour ajouter des informations ou des conseils sur l’ensemble du workflow de votre source, en particulier s’il existe des &quot;pièges&quot; particuliers qu’un utilisateur final peut rencontrer.*
