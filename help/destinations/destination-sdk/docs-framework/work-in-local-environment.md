---
title: Utilisation d’un éditeur de texte dans votre environnement local pour créer une page de documentation de destination
seo-title: Use a text editor in your local environment to create a destination documentation page
description: Les instructions de cette page vous montrent comment utiliser un éditeur de texte pour travailler dans votre environnement local afin de créer de la documentation et envoyer une requête de tirage.
seo-description: The instructions on this page show you how to use a text editor to work in your local environment to author documentation and submit a pull request.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e1e7d2f70c032d02f96b3999e4fca736070c6ca9
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 3%

---

# Utilisation d’un éditeur de texte dans votre environnement local pour créer une page de documentation de destination {#local-authoring}

Les instructions de cette page vous montrent comment utiliser un éditeur de texte pour travailler dans votre environnement local afin de créer de la documentation et envoyer une requête de tirage (PR). Avant de passer en revue les étapes indiquées ici, veillez à lire [Document de votre destination dans les destinations Adobe Experience Platform](./documentation-instructions.md).

>[!TIP]
>
>Reportez-vous également à la documentation à l’appui du guide du contributeur d’Adobe :
>* [Installation des outils de création Git et Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Configuration locale du référentiel Git pour la documentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [Workflow de contributions GitHub pour les modifications majeures](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Connectez-vous à GitHub et configurez votre environnement de création local. {#set-up-environment}

1. Dans votre navigateur, accédez à `https://github.com/AdobeDocs/experience-platform.en`
2. Pour [dupliquer](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) le référentiel, cliquez sur **Branchement** comme illustré dans la capture d’écran.

   ![Référentiel de documentation pour les Adobes de transfert](./assets/ssd-fork-repo.png)

3. Cloner le référentiel sur votre ordinateur local. Sélectionnez **Code > HTTPS > Ouvrir avec GitHub Desktop**, comme illustré ci-dessous. Vérifiez que [GitHub Desktop](https://desktop.github.com/) est installé. Pour plus d’informations, reportez-vous à la section [Création d’un clone local du référentiel](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) dans le guide du contributeur d’Adobe.

   ![Cloner le référentiel de documentation d’Adobe vers l’environnement local](./assets/clone-local.png)

4. Dans la structure de fichiers locale, accédez à `experience-platform.en/help/destinations/catalog/[...]`, où `[...]` est la catégorie souhaitée pour votre destination. Par exemple, si vous ajoutez une destination de personnalisation à Experience Platform, sélectionnez le dossier `personalization`.

## Créez la page de documentation de votre destination. {#author-documentation}

1. Votre page de documentation est basée sur le [modèle de destination en libre-service](./self-service-template.md). Téléchargez le [modèle de destination](assets/yourdestination-template.zip). Décompressez-le et extrayez le fichier `yourdestination-template.md` dans le répertoire mentionné à l’étape 4 ci-dessus.  Renommez le fichier `YOURDESTINATION.md`, YOURDESTINATION étant le nom de votre destination dans Adobe Experience Platform. Par exemple, si votre société s’appelle Moviestar, vous nommerez votre fichier `moviestar.md`.
2. Ouvrez votre nouveau fichier dans l’ [éditeur de texte de votre choix](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors). Adobe vous recommande d’utiliser [Visual Studio Code](https://code.visualstudio.com/) et d’installer l’extension de création Adobe Markdown. Pour installer l’extension, ouvrez Visual Studio Code, sélectionnez l’onglet **[!DNL Extensions]** à gauche de l’écran, puis recherchez `adobe markdown authoring`. Sélectionnez l’extension et cliquez sur **[!DNL Install]**.
   ![Installation de l’extension Adobe Markdown Author](./assets/install-adobe-markdown-extension.gif)
3. Modifiez le modèle avec les informations pertinentes pour votre destination. Suivez les instructions du modèle.
4. Pour toute capture d’écran ou image que vous prévoyez d’ajouter à votre documentation, accédez à `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, où `[...]` est la catégorie souhaitée pour votre destination. Par exemple, si vous ajoutez une destination de personnalisation à Experience Platform, sélectionnez le dossier `personalization`. Créez un dossier pour votre destination et enregistrez vos images ici. Vous devez leur créer un lien à partir de la page que vous créez. Voir les [instructions pour créer un lien vers des images](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).
5. Lorsque vous êtes prêt, enregistrez le fichier sur lequel vous travaillez.

## Soumettre votre documentation pour révision {#submit-review}

1. Dans GitHub Desktop, créez une branche opérationnelle pour vos mises à jour et sélectionnez **Publier la branche** pour publier la branche sur GitHub.

![Nouvelle branche locale](./assets/new-branch-local.gif)

1. Dans GitHub Desktop, [commit](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) votre travail, comme illustré ci-dessous.

   ![Validation en local](./assets/commit-local.png)

1. Dans GitHub Desktop, [push](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) votre travail vers la branche [remote](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote), comme illustré ci-dessous.

   ![Push your commit](./assets/push-local-to-remote.png)

1. Dans l’interface web GitHub, ouvrez une requête de tirage (PR) pour fusionner votre branche de travail dans la branche principale du référentiel de documentation d’Adobe. Assurez-vous que la branche sur laquelle vous avez travaillé est sélectionnée et sélectionnez **Requête d’extraction**.

   ![Créer une requête d’extraction](./assets/ssd-create-pull-request-1.png)

1. Assurez-vous que les branches de base et de comparaison sont correctes. Ajoutez une note au document de requête de tirage décrivant votre mise à jour, puis sélectionnez **Créer une requête de tirage**. Cela ouvre une requête de tirage pour fusionner la branche opérationnelle de votre double dans la branche principale du référentiel Adobe.
   >[!TIP]
   >
   >Laissez la case **Autoriser les modifications par les responsables** cochée afin que l’équipe de documentation d’Adobe puisse apporter des modifications au résiduel.

   ![Création d’une requête d’extraction pour Adobe du référentiel de documentation](./assets/ssd-create-pull-request-2.png)

1. À ce stade, une notification s’affiche pour vous inviter à signer le contrat de licence du contributeur Adobe (CLA). Cette étape est obligatoire. Après avoir signé le contrat de licence du contributeur, actualisez la page de requête de tirage et envoyez la requête de tirage.

1. Vous pouvez confirmer que la demande d’extraction a été envoyée en consultant l’onglet **Requêtes d’extraction** dans `https://github.com/AdobeDocs/experience-platform.en`.

![PR réussi](./assets/ssd-pr-successful.png)

1. Merci ! L’équipe de documentation de l’Adobe contactera le service des relations publiques si des modifications sont nécessaires et vous indiquera quand la documentation sera publiée.

>[!TIP]
>
>Pour ajouter des images et des liens à votre documentation, ainsi que toute autre question concernant Markdown, consultez la section [Utilisation de Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) dans le guide d’écriture collaborative de l’Adobe.
