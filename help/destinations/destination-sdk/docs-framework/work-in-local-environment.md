---
title: Utiliser un éditeur de texte dans votre environnement local pour créer une page de documentation de destination
description: Les instructions de cette page vous montrent comment utiliser un éditeur de texte pour travailler dans votre environnement local afin de créer une page de documentation pour votre destination Experience Platform et de l’envoyer pour révision.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: 0d98183838125fac66768b94bc1993bde9a374b5
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 4%

---

# Utiliser un éditeur de texte dans votre environnement local pour créer une page de documentation de destination {#local-authoring}

Les instructions de cette page vous montrent comment utiliser un éditeur de texte pour travailler dans votre environnement local afin de créer de la documentation et d’envoyer une requête de tirage (PR). Avant de suivre les étapes indiquées ici, veillez à lire [Documenter la destination dans les destinations Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Reportez-vous également à la documentation d’aide du guide du contributeur d’Adobe :
>* [Installation des outils de création Git et Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* [Configurer le référentiel Git localement pour la documentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [Workflow de contribution GitHub pour les modifications majeures](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## Connexion à GitHub et configuration de votre environnement de création local {#set-up-environment}

1. Dans votre navigateur, accédez à `https://github.com/AdobeDocs/experience-platform.en`
2. Pour [brancher](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) le référentiel, cliquez sur **Branchement** comme illustré ci-dessous. Une copie du référentiel Experience Platform est ainsi créée dans votre propre compte GitHub.

   ![Référentiel de documentation d’Adobe en branchement](../assets/docs-framework/ssd-fork-repository.gif)

3. Clonez le référentiel sur votre ordinateur local. Sélectionnez **Code > HTTPS > Ouvrir avec le bureau GitHub**, comme illustré ci-dessous. Vérifiez que [GitHub Desktop](https://desktop.github.com/) est installé. Pour plus d’informations, consultez la section [Création d’un clone local du référentiel](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#create-a-local-clone-of-the-repository) dans le guide du contributeur d’Adobe.

   ![Clonage du référentiel de documentation Adobe dans l’environnement local](../assets/docs-framework/clone-local.png)

4. Dans votre structure de fichiers locale, accédez à `experience-platform.en/help/destinations/catalog/[...]`, où `[...]` est la catégorie souhaitée pour la destination. Par exemple, si vous ajoutez une destination de personnalisation à Experience Platform, sélectionnez le dossier `personalization` .

## Créer la page de documentation pour la destination {#author-documentation}

1. Votre page de documentation est basée sur le modèle de destination [libre-service](../docs-framework/self-service-template.md). Téléchargez le [modèle de destination](../assets/docs-framework/yourdestination-template.zip). Décompressez-le et extrayez le fichier `yourdestination-template.md` dans le répertoire mentionné à l’étape 4 ci-dessus.  Renommez le fichier `YOURDESTINATION.md`, où YOURDESTINATION correspond au nom de la destination dans Adobe Experience Platform. Par exemple, si votre société s’appelle Moviestar, vous devez nommer votre fichier `moviestar.md`.
2. Ouvrez votre nouveau fichier dans l’éditeur de texte [ de votre choix](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html#understand-markdown-editors). Adobe vous recommande d’utiliser [Visual Studio Code](https://code.visualstudio.com/) et d’installer l’extension de création Adobe Markdown. Pour installer l’extension, ouvrez Visual Studio Code, sélectionnez l’onglet **[!DNL Extensions]** à gauche de l’écran, puis recherchez `adobe markdown authoring`. Sélectionnez l’extension et cliquez sur **[!DNL Install]**.
   ![Installer l’extension de création Adobe Markdown](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. Modifiez le modèle avec les informations pertinentes pour la destination. Suivez les instructions du modèle.
4. Pour toutes les captures d’écran ou images que vous prévoyez d’ajouter à votre documentation, accédez à `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, où `[...]` est la catégorie souhaitée pour la destination. Par exemple, si vous ajoutez une destination de personnalisation à Experience Platform, sélectionnez le dossier `personalization` . Créez un dossier pour la destination et enregistrez vos images ici. Vous devez créer un lien vers ces pages à partir de la page que vous êtes en train de créer. Voir [instructions pour créer un lien vers des images](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images).
5. Lorsque vous êtes prêt, enregistrez le fichier sur lequel vous travaillez.

## Envoi de la documentation pour révision {#submit-review}

>[!TIP]
>
>Notez qu&#39;il n&#39;y a rien à casser ici. En suivant les instructions de cette section, vous suggérez simplement une mise à jour de la documentation. La mise à jour suggérée sera approuvée ou modifiée par l’équipe de documentation de Adobe Experience Platform.

1. Dans le bureau GitHub, créez une branche de travail pour vos mises à jour, puis sélectionnez **Publier la branche** pour publier la branche sur GitHub.

![Nouvelle filiale locale](../assets/docs-framework/new-branch-local.gif)

1. Dans le bureau GitHub, [validez](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) votre travail, comme illustré ci-dessous.

   ![Validation en local](../assets/docs-framework/commit-local.png)

1. Dans le Bureau GitHub, [poussez](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) votre travail vers la branche [distante](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote), comme illustré ci-dessous.

   ![Envoyez votre validation](../assets/docs-framework/push-local-to-remote.png)

1. Dans l’interface web GitHub, ouvrez une requête de tirage (PR) pour fusionner votre branche de travail dans la branche principale du référentiel de documentation d’Adobe. Vérifiez que la branche sur laquelle vous avez travaillé est sélectionnée et sélectionnez **Contribuer > Ouvrir la demande d’extraction**.

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
>Pour ajouter des images et des liens à votre documentation, ainsi que pour toute autre question sur Markdown, lisez [Utilisation de Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html) dans le guide d’écriture collaborative d’Adobe.
