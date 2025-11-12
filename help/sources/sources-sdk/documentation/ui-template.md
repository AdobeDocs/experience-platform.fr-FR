---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
title: Modèle de documentation en libre-service pour l’interface utilisateur
description: Découvrez comment créer une connexion source YOURSOURCE à l’aide de l’interface utilisateur de Adobe Experience Platform.
exl-id: 6471c0a2-22e8-4133-a76f-ee3c5c669ef8
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 10%

---

# Créer une connexion source *YOURSOURCE* dans l’interface utilisateur

*Au fur et à mesure que vous parcourez ce modèle, remplacez ou supprimez tous les paragraphes en italique (en commençant par celui-ci).*

*Commencez par mettre à jour les métadonnées (titre et description) en haut de la page. Veuillez ignorer toutes les instances d&#39;UICONTROL sur cette page. Il s’agit d’une balise qui aide nos processus de traduction automatique à traduire correctement la page dans les différentes langues que nous prenons en charge. Nous ajouterons des balises à votre documentation une fois que vous l’aurez envoyée.*

Ce tutoriel décrit les étapes à suivre pour créer un connecteur source *YOURSOURCE* à l’aide de l’interface utilisateur d’Experience Platform.

## Vue d’ensemble

*Donnez un bref aperçu de votre entreprise, y compris de la valeur qu&#39;elle offre aux clients. Insérez un lien vers la page d’accueil de la documentation de votre produit pour en savoir plus.*

>[!IMPORTANT]
>
>Ce connecteur source et cette page de documentation sont créés et gérés par l’équipe *YourSource*. Pour toute demande ou information, contactez-les directement à l&#39;adresse *Insérez un lien ou une adresse e-mail où vous pouvez être contacté pour les mises à jour*.

## Conditions préalables

*Ajoutez dans cette section des informations sur tout ce que les clients doivent savoir avant de commencer à configurer la source dans l’interface utilisateur de Adobe Experience Platform. Cela peut concerner :*

* *nécessité d’être ajouté à une place sur la liste autorisée*
* *exigences relatives au hachage des e-mails*
* *toutes les caractéristiques du compte de votre côté*
* *comment obtenir les informations d’authentification pour vous connecter à votre plateforme*

### Collecter les informations d’identification requises

Pour connecter *YOURSOURCE* à Experience Platform, vous devez fournir des valeurs pour les propriétés de connexion suivantes :

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| *informations d’identification un* | *Ajoutez une brève description aux informations d’authentification de votre source ici* | *Veuillez ajouter un exemple des informations d’authentification de votre source ici* |
| *informations d’identification 2* | *Ajoutez une brève description aux informations d’authentification de votre source ici* | *Veuillez ajouter un exemple des informations d’authentification de votre source ici* |
| *informations d’identification trois* | *Ajoutez une brève description aux informations d’authentification de votre source ici* | *Veuillez ajouter un exemple des informations d’authentification de votre source ici* |

Pour plus d’informations sur ces informations d’identification, consultez la documentation sur l’authentification *YOURSOURCE*. *Ajoutez un lien vers la documentation d’authentification de votre plateforme ici*.

## Connecter votre compte *YOURSOURCE*

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Sources]** dans la barre de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. L’écran [!UICONTROL Catalog] affiche diverses sources avec lesquelles vous pouvez créer un compte.

Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sous la catégorie *CATÉGORIE DE YOURSOURCE*, sélectionnez *YOURSOURCE*, puis sélectionnez **[!UICONTROL Add data]**.

>[!TIP]
>
>Les captures d’écran utilisées ci-dessous sont des exemples. Lors de la création de votre documentation, veuillez remplacer les images par des captures d’écran de votre source réelle. Vous pouvez utiliser le même motif et la même couleur de marquage, ainsi que les mêmes noms de fichier. Assurez-vous que la capture d’écran capture l’ensemble de l’écran de l’interface utilisateur Experience Platform. Pour plus d’informations sur le téléchargement des captures d’écran, consultez le guide sur la [soumission de la documentation à révision](./github.md).

![catalogue](../assets/ui/catalog.png)

La page **[!UICONTROL Connect YOURSOURCE account]** s’affiche. Sur cette page, vous pouvez utiliser de nouvelles informations d’identification ou des informations d’identification existantes.

### Compte existant

Pour utiliser un compte existant, sélectionnez le compte *YOURSOURCE* avec lequel vous souhaitez créer un flux de données, puis sélectionnez **[!UICONTROL Next]** pour continuer.

![existant](../assets/ui/existing.png)

### Nouveau compte

Si vous créez un compte, sélectionnez **[!UICONTROL New account]**, puis fournissez un nom, une description facultative et vos informations d’identification. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Connect to source]** puis attendez que la nouvelle connexion s’établisse.

![nouveau](../assets/ui/new.png)

## Étapes suivantes

*Les workflows des étapes restantes de la création d’un flux de données sont modularisés. Si vous souhaitez effectuer des appels externes spécifiques concernant votre source, reportez-vous à la section Ressources supplémentaires ci-dessous.*

En suivant ce tutoriel, vous avez établi une connexion à votre compte *YOURSOURCE*. Vous pouvez maintenant passer au tutoriel suivant et [configurer un flux de données pour importer des données dans Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Ressources supplémentaires

*Il s’agit d’une section facultative dans laquelle vous pouvez fournir des liens supplémentaires vers la documentation de votre produit ou toute autre étape, capture d’écran ou nuance que vous jugez importante pour le succès du client. Vous pouvez utiliser cette section pour ajouter des informations ou des conseils sur l’ensemble du workflow de votre source, en particulier s’il existe des « pièges » particuliers qu’un utilisateur final peut rencontrer.*
