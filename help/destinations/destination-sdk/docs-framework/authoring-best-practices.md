---
title: Bonnes pratiques de création
description: Découvrez les règles et conseils à suivre lors de la création de votre page de documentation de destination, afin de vous assurer qu’elle respecte les normes de qualité de la documentation Adobe Experience Platform.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 3%

---

# Bonnes pratiques de création

## Présentation {#overview}

Cette page décrit les règles que vous devez suivre lorsque [création de votre documentation de destination](./documentation-instructions.md) pour vous assurer qu’elle respecte les normes de qualité de la documentation Adobe Experience Platform.

## Directives générales {#general-guidance}

* Lorsque vous renseignez la variable [modèle](./self-service-template.md) pour consulter la documentation de votre destination, reportez-vous au guide du contributeur d’Adobe pour plus d’informations sur [liaison](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en), [tables](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables), la variable [syntaxe markdown prise en charge](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en), [écriture de conseils](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en), etc.
* N’incluez pas d’observations et d’estimations dans la documentation du produit.
* Dans la documentation Experience Platform, les auteurs Adobe utilisent **mise en forme gras** pour faire référence aux commandes de l’interface utilisateur, comme suit :
   * Accédez à **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue.]** Consultez un exemple de la manière dont les commandes de l’interface utilisateur sont documentées dans une [tutoriel sur les destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## Style d’écriture

>[!IMPORTANT]
>
>Lecture [Rédaction de conseils pour la documentation Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) avant de commencer à créer la page de documentation de destination.

* Gardez vos phrases courtes et arrivez au point rapidement. Si votre phrase comporte plus de 20 mots ou utilise plusieurs virgules, envisagez de la diviser en phrases distinctes. Les phrases de plus de 20 mots peuvent être particulièrement difficiles pour les lecteurs.
* Ne sois pas trop poli. Évitez d’utiliser &quot;s’il vous plaît&quot; ou &quot;faites bien...&quot;. dans la documentation technique.

## Liaison {#linking}

Suivez le modèle de documentation fourni et ne modifiez pas les liens existants dans le modèle. Lorsque vous incluez de nouveaux liens, lisez [utilisation de liens dans la documentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) dans le guide du contributeur.

## Indications de marque {#branding}

* AEP n&#39;est pas un terme approuvé destiné au public. Utilisez Adobe Experience Platform lors de la première utilisation, puis Experience Platform, puis Platform.
   * **Ne pas utiliser**: Avant d’exporter des données d’AEP vers YourDestination, veillez à lire et à remplir ces conditions préalables.
   * **Utilisation**: Avant d’exporter des données de Adobe Experience Platform vers YourDestination, veillez à lire et à remplir ces conditions préalables.

## Images et captures d’écran {#images-and-screenshots}

* Pour plus d’informations sur [Comment créer un lien vers des images](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images), reportez-vous au guide du contributeur.
* Lorsque vous utilisez des captures d’écran, veillez à ce que votre capture d’écran capture l’ensemble de l’écran de l’interface utilisateur de Platform.
* Lorsque vous marquez des images pour mettre en évidence un certain contrôle ou libellé sur la page, essayez de suivre le style de balisage utilisé par l’équipe de documentation Experience Platform. Notez comment la fonction basée sur Profile est mise en surbrillance dans [cette capture d’écran](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Veuillez utiliser `png` format des images.
* N’utilisez pas de captures d’écran numérotées comme noms de fichier. Les noms des fichiers image doivent être descriptifs.
   * **Ne pas utiliser**: `1.png`, `2.png`, `3.png`
   * **Utilisez**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Veuillez utiliser du texte de remplacement pour toutes les images que vous ajoutez à la documentation et utiliser une grammaire correcte dans le texte de remplacement.
   * **Ne pas utiliser**: Détails de la connexion de destination
   * **Utilisation**: Image de l’interface utilisateur de Platform, affichant les détails de connexion de destination renseignés.

## Processus {#process}

* Le [modèle de documentation](./self-service-template.md) est rarement mis à jour, en fonction des commentaires des partenaires. Avant de commencer à créer de la documentation pour votre destination, assurez-vous d’avoir téléchargé la [dernière version du modèle](../assets/docs-framework/yourdestination-template.zip).
* Créez la documentation et créez la demande d’extraction de documentation (PR) à partir d’une branche de votre double. *autre que la branche principale*. Reportez-vous à la section Destination de l’envoi pour la révision lors de la création dans le [Interface de GitHub](./use-github-interface-to-create-documentation.md#submit-review) ou [votre environnement local](./work-in-local-environment.md#submit-review).
