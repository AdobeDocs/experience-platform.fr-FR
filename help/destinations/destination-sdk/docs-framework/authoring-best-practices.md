---
title: Bonnes pratiques de création
description: Découvrez les règles et conseils à suivre au moment de la création de la page de documentation de destination, afin de vous assurer qu’elle respecte les normes de qualité de la documentation Adobe Experience Platform.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 98%

---

# Bonnes pratiques de création

## Vue d’ensemble {#overview}

Cette page décrit les règles à suivre au moment de la [création de la page de documentation de destination](./documentation-instructions.md), afin de vous assurer qu’elle respecte les normes de qualité de la documentation Adobe Experience Platform.

## Directives générales {#general-guidance}

* Lorsque vous remplissez le [modèle](./self-service-template.md) de la documentation de destination, consultez le guide du contributeur d’Adobe pour en savoir plus sur les [liens](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html), les [tableaux](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#tables), la [syntaxe markdown prise en charge](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html), les [guides de rédaction](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html), etc.
* N’incluez pas d’observations ni d’estimations dans la documentation du produit.
* Dans la documentation Experience Platform, les auteurs Adobe mettent les commandes de l’interface utilisateur **en gras**, comme suit :
   * Accédez à **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**. Consultez ce [tutoriel sur les destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#select-destination) pour en savoir plus sur la manière dont les commandes de l’interface utilisateur sont documentées.

## Règle de style

>[!IMPORTANT]
>
>Consultez le document [Guide de rédaction pour la documentation Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html) avant de commencer à créer la page de documentation de destination.

* Faites des phrases courtes et allez à l’essentiel. Si la phrase comporte plus de 20 mots ou plusieurs virgules, envisagez de la diviser en plusieurs phrases, car elles peuvent être particulièrement difficiles à lire.
* Ne soyez pas trop poli. Évitez d’utiliser « veuillez » ou « nous vous prions… » dans la documentation technique.

## Liaison {#linking}

Suivez le modèle de documentation fourni et ne modifiez pas les liens existant dans le modèle. Quand vous ajoutez de nouveaux liens, consultez la section [Utilisation de liens dans la documentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html) dans le guide du contributeur.

## Directives relatives à l’image de marque {#branding}

* AEP n’est pas un terme approuvé pour le public. Utilisez Adobe Experience Platform au moment de la première utilisation, puis Experience Platform, et enfin Platform.
   * **Ne pas utiliser** : avant d’exporter des données d’AEP vers YourDestination, veillez à lire et à remplir ces conditions préalables.
   * **Utiliser** : avant d’exporter des données d’Adobe Experience Platform vers YourDestination, veillez à lire et à remplir ces conditions préalables.

## Images et copies d’écran {#images-and-screenshots}

* Pour plus d’informations sur [comment créer un lien vers des images](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html#images), consultez le guide du contributeur.
* Quand vous utilisez des copies d’écran, veillez à copier l’ensemble de l’écran de l’interface utilisateur de Platform.
* Quand vous marquez des images pour mettre en évidence une certaine commande ou un certain libellé sur la page, essayez de respecter le style de marquage utilisé par l’équipe de documentation Experience Platform. Observez comment la base de profil est mise en évidence dans [cette copie d’écran](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Utilisez des images au format `png`.
* N’utilisez pas de copies d’écran numérotées comme noms de fichier. Les noms des fichiers images doivent être descriptifs.
   * **Ne pas utiliser** : `1.png`, `2.png`, `3.png`
   * **Utiliser** : `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Utilisez du texte de remplacement pour toutes les images que vous ajoutez à la documentation et veillez à respecter les règles de grammaire dans le texte de remplacement.
   * **Ne pas utiliser** : détails de la connexion de destination
   * **Utiliser** : image de l’interface utilisateur de Platform affichant les détails de connexion de destination renseignés.

## Processus {#process}

* Le [modèle de documentation](./self-service-template.md) est mis à jour périodiquement, en fonction des commentaires du partenaire. Avant de commencer à créer de la documentation pour la destination, veillez à avoir téléchargé la [dernière version du modèle](../assets/docs-framework/yourdestination-template.zip).
* Rédigez la documentation et créez la requête de tirage de la documentation (PR) à partir d’une branche de votre secteur, *autre que la branche principale*. Consultez la section « Soumission d’une destination à réviser » au moment de la création dans l’[interface GitHub](./use-github-interface-to-create-documentation.md#submit-review) ou [votre environnement local](./work-in-local-environment.md#submit-review).
