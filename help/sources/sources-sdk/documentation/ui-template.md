---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Modèle de documentation en libre-service pour l’interface utilisateur
description: Découvrez comment créer une connexion source YOURSOURCE à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 6471c0a2-22e8-4133-a76f-ee3c5c669ef8
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 19%

---

# Créez une connexion source *YOURSOURCE* dans l’interface utilisateur

*Lorsque vous parcourez ce modèle, remplacez ou supprimez tous les paragraphes en italique (en commençant par celui-ci).*

*Commencez par mettre à jour les métadonnées (titre et description) en haut de la page. Ignorez toutes les instances d’UICONTROL sur cette page. Il s’agit d’une balise qui aide nos processus de traduction automatique à traduire correctement la page dans les multiples langues prises en charge. Nous ajouterons des balises à votre documentation après l’avoir envoyée.*

Ce tutoriel décrit les étapes à suivre pour créer un connecteur source *YOURSOURCE* à l’aide de l’interface utilisateur de Platform.

## Vue d’ensemble

*Fournissez un bref aperçu de votre entreprise, y compris la valeur qu’elle fournit aux clients. Insérez un lien vers la page d’accueil de la documentation du produit pour une lecture plus approfondie.*

>[!IMPORTANT]
>
>Ce connecteur source et cette page de documentation sont créés et gérés par l’équipe *YourSource*. Pour toute demande de mise à jour ou de demande de mise à jour, contactez-les directement à l&#39;adresse *Ajouter un lien ou une adresse email où vous pouvez accéder pour les mises à jour*.

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

## Connectez votre compte *YOURSOURCE*

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** à partir de la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalogue] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie *CATÉGORIE DE YOURSOURCE*, sélectionnez *YOURSOURCE*, puis sélectionnez **[!UICONTROL Ajouter des données]**.

>[!TIP]
>
>Les captures d’écran utilisées ci-dessous sont des exemples. Lors de la création de votre documentation, veuillez remplacer les images par des captures d’écran de votre source réelle. Vous pouvez utiliser le même motif de marquage et la même couleur, ainsi que les mêmes noms de fichier. Assurez-vous que votre capture d’écran capture tout l’écran de l’interface utilisateur de Platform. Pour plus d’informations sur la manière de charger vos captures d’écran, consultez le guide sur l’ [envoi de votre documentation en vue de la révision](./github.md).

![catalogue](../assets/ui/catalog.png)

La page **[!UICONTROL Connecter votre compte SOURCE]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte *YOURSOURCE* avec lequel vous souhaitez créer un nouveau flux de données, puis sélectionnez **[!UICONTROL Suivant]** pour continuer.

![existant](../assets/ui/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL Nouveau compte]**, puis fournissez un nom, une description facultative et vos informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connexion à la source]**, puis patientez quelques instants le temps que la nouvelle connexion sʼétablisse.

![nouveau](../assets/ui/new.png)

## Étapes suivantes

*Les workflows pour les étapes restantes de la création d’un flux de données sont modulaires. Si vous souhaitez effectuer des appels d’urgence spécifiques concernant votre source, reportez-vous à la section Ressources supplémentaires ci-dessous.*

En suivant ce tutoriel, vous avez établi une connexion à votre compte *YOURSOURCE*. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Ressources supplémentaires

*Il s’agit d’une section facultative dans laquelle vous pouvez fournir d’autres liens vers la documentation de votre produit ou toute autre étape, captures d’écran et nuances jugées importantes pour le succès du client. Vous pouvez utiliser cette section pour ajouter des informations ou des conseils sur l&#39;ensemble du workflow de votre source, en particulier s&#39;il existe des &quot;pièges&quot; particuliers qu&#39;un utilisateur final peut rencontrer.*
