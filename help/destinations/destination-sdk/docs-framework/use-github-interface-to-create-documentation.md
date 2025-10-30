---
title: Utiliser l’interface web GitHub pour créer une page de documentation de destination
description: Les instructions de cette page vous montrent comment utiliser l’interface web GitHub pour créer une page de documentation pour votre destination Experience Platform et l’envoyer pour révision.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: ff094c0c2c75e097140626d77478b8da9a7edf04
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 3%

---

# Utiliser l’interface web GitHub pour créer une page de documentation de destination {#github-interface}

Les instructions ci-dessous vous montrent comment utiliser l’interface web GitHub pour créer de la documentation et envoyer une requête de tirage (PR). Avant de suivre les étapes indiquées ici, veillez à lire [Documenter la destination dans les destinations Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Reportez-vous également à la documentation d’aide du guide du contributeur d’Adobe :
>
>* [Installation des outils de création Git et Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=fr)
>* [Configurer le référentiel Git localement pour la documentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=fr)
>* [Workflow de contribution GitHub pour les modifications majeures](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=fr).

## Configuration de votre environnement de création GitHub {#set-up-environment}

1. Dans votre navigateur, accédez à `https://github.com/AdobeDocs/experience-platform.en`.
1. Pour [brancher](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=fr#fork-the-repository) le référentiel, cliquez sur **Branchement** comme illustré ci-dessous. Une copie du référentiel Experience Platform est ainsi créée dans votre propre compte GitHub.

   ![Référentiel de documentation d’Adobe en branchement](../assets/docs-framework/ssd-fork-repository.gif)

1. Dans le formulaire du référentiel, créez une branche pour votre projet, comme illustré ci-dessous. Utilisez cette nouvelle branche pour votre travail.

   ![Créer une branche GitHub](../assets/docs-framework/new-branch-github.gif)

1. Dans la structure de dossiers GitHub du référentiel dupliqué, accédez à `experience-platform.en/help/destinations/catalog/[...]`, où `[...]` est la catégorie souhaitée pour la destination. Par exemple, si vous ajoutez une destination de personnalisation à Experience Platform, sélectionnez la catégorie `personalization` . Sélectionnez **Ajouter un fichier > Créer un fichier**.

   ![Ajouter un nouveau fichier](../assets/docs-framework/github-navigate-and-create-file.gif)

1. Nommez votre `YOURDESTINATION.md` de destination, où YOURDESTINATION correspond au nom de votre destination dans Adobe Experience Platform. Par exemple, si votre société s’appelle Moviestar, vous devez nommer votre fichier `moviestar.md`.

## Créer la page de documentation pour la destination {#author-documentation}

1. Vous allez créer le contenu de votre page de destination en fonction du [modèle de libre-service de documentation](./self-service-template.md). **[Téléchargez](../assets/docs-framework/yourdestination-template.zip)** le modèle et décompressez-le pour extraire le modèle de fichier `.md`.
1. Collez et modifiez le contenu du modèle avec les informations pertinentes pour la destination dans un éditeur Markdown en ligne, tel que [dillinger.io](https://dillinger.io/). Suivez les instructions du modèle pour savoir ce que vous devez remplir et quels paragraphes peuvent être supprimés.

   >[!TIP]
   >
   >Vous pouvez fermer la fenêtre de votre navigateur à tout moment et la rouvrir ultérieurement. Votre travail est enregistré automatiquement et vous attendra lorsque vous rouvrirez le navigateur.
1. Copiez le contenu de l’éditeur Markdown dans votre nouveau fichier dans GitHub.
1. Pour toutes les captures d’écran ou images que vous prévoyez d’utiliser, utilisez l’interface GitHub pour charger les fichiers sur `experience-platform.en/help/destinations/assets/catalog/[...]`, où `[...]` est la catégorie souhaitée pour la destination. Par exemple, si vous ajoutez une destination de personnalisation à Experience Platform, sélectionnez la catégorie `personalization` . Vous devez créer un lien vers les images de la page que vous créez. Voir [instructions pour créer un lien vers des images](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=fr#link-to-images).

   ![Charger l’image sur GitHub](../assets/docs-framework/upload-image.gif)

1. Lorsque vous êtes prêt, enregistrez le fichier dans votre branche .

   ![Confirmer la création du fichier](../assets/docs-framework/ssd-confirm-file-creation.png)

## Envoi de la documentation pour révision {#submit-review}

>[!TIP]
>
>Notez qu&#39;il n&#39;y a rien à casser ici. En suivant les instructions de cette section, vous suggérez simplement une mise à jour de la documentation. La mise à jour suggérée sera approuvée ou modifiée par l’équipe de documentation de Adobe Experience Platform.

1. Après avoir enregistré le fichier et chargé les images souhaitées, vous pouvez ouvrir une demande d’extraction (PR) pour fusionner votre branche de travail dans la branche principale du référentiel de documentation d’Adobe. Assurez-vous que la branche sur laquelle vous avez travaillé est sélectionnée et sélectionnez **Contribuer > Ouvrir la demande d’extraction**.

   ![Créer une demande d’extraction](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Assurez-vous que les branches de base et de comparaison sont correctes. Ajoutez une note au PR décrivant votre mise à jour, puis sélectionnez **Créer une demande d’extraction**. Cette action ouvre une requête de tirage pour fusionner la branche de travail de votre branchement dans la branche principale du référentiel Adobe.

   >[!TIP]
   >
   >Laissez la case **Autoriser les modifications par les responsables** sélectionnée afin que l’équipe de documentation d’Adobe puisse apporter des modifications à la requête de modification.

   ![Créer une requête de tirage vers le référentiel de documentation Adobe](../assets/docs-framework/ssd-create-pull-request-2.png)

1. À ce stade, une notification s’affiche vous invitant à signer le contrat de licence du contributeur (CLA) d’Adobe. Il s’agit d’une étape obligatoire. Après avoir signé le contrat de licence du contributeur, actualisez la page de requête de tirage et envoyez la demande d’extraction.

1. Vous pouvez confirmer que la demande d’extraction a été envoyée en consultant l’onglet **Demandes d’extraction** dans `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR réussie](../assets/docs-framework/ssd-pr-successful.png)

1. Merci ! L’équipe de documentation d’Adobe contactera le service de presse si des modifications sont nécessaires et pour vous informer de la date de publication de la documentation.

>[!TIP]
>
>Pour ajouter des images et des liens à votre documentation, ainsi que pour toute autre question sur Markdown, lisez [Utilisation de Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=fr) dans le guide d’écriture collaborative d’Adobe.
