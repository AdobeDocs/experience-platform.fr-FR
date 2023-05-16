---
title: Utiliser l’interface web GitHub pour créer une page de documentation de destination
description: Les instructions de cette page vous montrent comment utiliser l’interface web GitHub pour créer une page de documentation pour votre destination Experience Platform et l’envoyer pour révision.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 5%

---

# Utiliser l’interface web GitHub pour créer une page de documentation de destination {#github-interface}

Les instructions ci-dessous vous montrent comment utiliser l’interface web GitHub pour créer de la documentation et envoyer une requête de tirage (PR). Avant de passer en revue les étapes indiquées ici, veillez à lire [Document de votre destination dans les destinations Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Reportez-vous également à la documentation à l’appui du guide du contributeur d’Adobe :
>* [Installation des outils de création Git et Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Configuration locale du référentiel Git pour la documentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Workflow de contributions GitHub pour les modifications majeures](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Configuration de votre environnement de création GitHub {#set-up-environment}

1. Dans votre navigateur, accédez à la page suivante : `https://github.com/AdobeDocs/experience-platform.en`.
2. À [double](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) le référentiel, cliquez sur **Branchement** comme illustré ci-dessous. Cela crée une copie du référentiel Experience Platform dans votre propre compte GitHub.

   ![Référentiel de documentation pour les Adobes de transfert](../assets/docs-framework/ssd-fork-repository.gif)

3. Dans le branchement du référentiel, créez une branche pour votre projet, comme illustré ci-dessous. Utilisez cette nouvelle branche pour votre travail.

   ![Création d’une branche GitHub](../assets/docs-framework/new-branch-github.gif)

4. Dans la structure de dossiers GitHub du référentiel dupliqué, accédez à `experience-platform.en/help/destinations/catalog/[...]`où `[...]` est la catégorie souhaitée pour votre destination. Par exemple, si vous ajoutez une destination de personnalisation à Experience Platform, sélectionnez la variable `personalization` catégorie. Sélectionner **Ajouter un fichier > Créer un fichier**.

   ![Ajouter un nouveau fichier](../assets/docs-framework/github-navigate-and-create-file.gif)

5. Nommer votre destination `YOURDESTINATION.md`, où YOURDESTINATION est le nom de votre destination dans Adobe Experience Platform. Par exemple, si votre société s’appelle Moviestar, vous nommerez votre fichier . `moviestar.md`.

## Créez la page de documentation de votre destination. {#author-documentation}

1. Vous allez créer le contenu de votre page de destination en fonction de la variable [modèle de libre-service de documentation](./self-service-template.md). **[Télécharger](../assets/docs-framework/yourdestination-template.zip)** le modèle et décompressez-le pour extraire le `.md` modèle de fichier.
2. Collez et modifiez le contenu du modèle avec les informations pertinentes pour votre destination dans un éditeur de balisage en ligne, tel que [dillinger.io](https://dillinger.io/). Suivez les instructions du modèle pour plus d’informations sur ce que vous devez remplir et les paragraphes qui peuvent être supprimés.

   >[!TIP]
   >
   >Vous pouvez fermer la fenêtre de votre navigateur à tout moment et la rouvrir ultérieurement. Votre travail est enregistré automatiquement et vous attend lorsque vous rouvrez le navigateur.
3. Copiez le contenu de l’éditeur de Markdown dans votre nouveau fichier dans GitHub.
4. Pour toutes les captures d’écran ou images que vous prévoyez d’utiliser, utilisez l’interface GitHub pour charger les fichiers dans `experience-platform.en/help/destinations/assets/catalog/[...]`où `[...]` est la catégorie souhaitée pour votre destination. Par exemple, si vous ajoutez une destination de personnalisation à Experience Platform, sélectionnez la variable `personalization` catégorie. Vous devez créer un lien vers les images de la page que vous créez. Voir [instructions pour créer un lien vers des images](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).

   ![Chargement d’une image sur GitHub](../assets/docs-framework/upload-image.gif)

5. Lorsque vous êtes prêt, enregistrez le fichier dans votre branche.

![Confirmer la création du fichier](../assets/docs-framework/ssd-confirm-file-creation.png)

## Soumettre votre documentation pour révision {#submit-review}

>[!TIP]
>
>Notez qu’il n’y a rien que vous puissiez casser ici. En suivant les instructions de cette section, vous proposez simplement une mise à jour de la documentation. Votre mise à jour suggérée sera approuvée ou modifiée par l’équipe de documentation de Adobe Experience Platform.

1. Après avoir enregistré le fichier et téléchargé les images de votre choix, vous pouvez ouvrir une requête de tirage (PR) pour fusionner votre branche de travail dans la branche principale du référentiel de documentation Adobe. Assurez-vous que la branche sur laquelle vous avez travaillé est sélectionnée et sélectionnez **Contribution > Ouvrir la requête de tirage**.

![Créer une requête d’extraction](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Assurez-vous que les branches de base et de comparaison sont correctes. Ajoutez une note au document de présentation, décrivant votre mise à jour, puis sélectionnez **Créer une requête d’extraction**. Cela ouvre une requête de tirage pour fusionner la branche opérationnelle de votre double dans la branche principale du référentiel Adobe.

   >[!TIP]
   >
   >Laissez le champ **Autorisation des modifications par les responsables** case à cocher sélectionnée afin que l’équipe de documentation d’Adobe puisse apporter des modifications au résiduel.

   ![Création d’une requête d’extraction pour Adobe du référentiel de documentation](../assets/docs-framework/ssd-create-pull-request-2.png)

1. À ce stade, une notification s’affiche pour vous inviter à signer le contrat de licence du contributeur Adobe (CLA). Cette étape est obligatoire. Après avoir signé le contrat de licence du contributeur, actualisez la page de requête de tirage et envoyez la requête de tirage.

1. Vous pouvez confirmer que la demande d’extraction a été envoyée en examinant la variable **Requêtes de tirage** dans `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR réussi](../assets/docs-framework/ssd-pr-successful.png)

1. Merci ! L’équipe de documentation de l’Adobe contactera le service des relations publiques si des modifications sont nécessaires et vous indiquera quand la documentation sera publiée.

>[!TIP]
>
>Pour ajouter des images et des liens à votre documentation, ainsi que toute autre question concernant Markdown, reportez-vous à la section [Utilisation de Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) dans le guide d’écriture collaborative d’Adobe.
