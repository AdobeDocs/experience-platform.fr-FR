---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
solution: Experience Platform
title: Utilisation d’un éditeur de texte dans votre environnement local pour créer une page de documentation sur les sources
topic-legacy: tutorial
description: Ce document décrit les étapes à suivre pour utiliser votre environnement local afin de créer de la documentation pour votre source et d’envoyer une requête de tirage (PR).
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: adf7dbe5e32310fee680f996ffbde0fd6ddd993a
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 8%

---

# Utiliser un éditeur de texte dans votre environnement local pour créer une page de documentation sur les sources

Ce document décrit les étapes à suivre pour utiliser votre environnement local afin de créer de la documentation pour votre source et d’envoyer une requête de tirage (PR).

>[!TIP]
>
>Vous pouvez utiliser les documents suivants du guide de contribution d’Adobe pour mieux prendre en charge votre processus de documentation : <ul><li>[Installation des outils de création Git et Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[Configuration locale du référentiel Git pour la documentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[Workflow de contributions GitHub pour les modifications majeures](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## Conditions préalables

Le tutoriel suivant nécessite que GitHub Desktop soit installé sur votre ordinateur local. Si vous ne disposez pas de l’appli de bureau GitHub, vous pouvez télécharger l’application. [here](https://desktop.github.com/).

## Connectez-vous à GitHub et configurez votre environnement de création local.

La première étape de la configuration de votre environnement de création local consiste à accéder au [Référentiel GitHub Adobe Experience Platform](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

Sur la page principale du référentiel Platform GitHub, sélectionnez **Branchement**.

![double](../assets/fork.png)

Pour cloner le référentiel sur votre ordinateur local, sélectionnez **Code**. Dans le menu déroulant qui s’affiche, sélectionnez **HTTPS** puis sélectionnez **Ouverture avec GitHub Desktop**.

>[!TIP]
>
>Pour plus d’informations, consultez le tutoriel sur [configuration locale du référentiel Git pour la documentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository).

![open-git-desktop](../assets/open-git-desktop.png)

Ensuite, laissez quelques instants à GitHub Desktop pour cloner la variable `experience-platform.en` référentiel.

![clonage](../assets/cloning.png)

Une fois le processus de clonage terminé, accédez à GitHub Desktop pour créer une nouvelle branche. Sélectionner **Principal** dans le volet de navigation supérieur, puis sélectionnez **Nouvelle branche**

![new-branch](../assets/new-branch.png)

Dans le panneau contextuel qui s’affiche, saisissez un nom descriptif pour votre branche, puis sélectionnez **Créer une branche**.

![create-branch-vs](../assets/create-branch-vs.png)

Ensuite, sélectionnez **Publier la branche**.

![publish-branch](../assets/publish-branch.png)

## Créez la page de documentation de votre source.

Une fois le référentiel cloné sur votre ordinateur local et une nouvelle branche créée, vous pouvez maintenant commencer à créer la page de documentation de votre nouvelle source via le [éditeur de texte de votre choix](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors).

Adobe recommande d’utiliser [Visual Studio Code](https://code.visualstudio.com/) et que vous installez l’extension Adobe Markdown Authoring. Pour installer l’extension, lancez Visual Studio Code, puis sélectionnez la variable **Extensions** dans le volet de navigation de gauche.

![ extension](../assets/extension.png)

Ensuite, saisissez `Adobe Markdown Authoring` dans la barre de recherche, puis sélectionnez **Installer** de la page qui s’affiche.

![install](../assets/install.png)

Lorsque votre ordinateur local est prêt, téléchargez le fichier [modèle de documentation sources](../assets/api-template.zip) et extrayez le fichier vers `experience-platform.en/help/sources/tutorials/api/create/...` avec [`...`] représentant la catégorie de votre choix. Par exemple, si vous créez une source de base de données, sélectionnez le dossier de base de données.

Enfin, suivez les instructions décrites dans le modèle et modifiez-le avec les informations pertinentes concernant votre source.

![edit-template](../assets/edit-template.png)

## Soumettre votre documentation pour révision

Pour créer une requête de tirage (PR) et envoyer votre documentation pour révision, enregistrez d’abord votre travail dans [!DNL Visual Studio Code] (ou l’éditeur de texte de votre choix). Ensuite, à l’aide de GitHub Desktop, saisissez un message de validation et sélectionnez **Valider à create-source-documentation**.

![commit-vs](../assets/commit-vs.png)

Ensuite, sélectionnez **Origine push** pour charger votre travail dans la branche distante.

![push-origin](../assets/push-origin.png)

Pour créer une requête d’extraction, sélectionnez **Créer une requête d’extraction**.

![create-pr-vs](../assets/create-pr-vs.png)

Assurez-vous que les branches de base et de comparaison sont correctes. Ajoutez une note au communiqué, décrivant votre mise à jour, puis sélectionnez **Créer une requête d’extraction**. Cela ouvre une requête de tirage pour fusionner la branche opérationnelle de votre travail dans la branche principale du référentiel Adobe.

>[!TIP]
>
>Laissez le champ **Autorisation des modifications par les responsables** case à cocher sélectionnée pour vous assurer que l’équipe de documentation d’Adobe peut apporter des modifications au résiduel.

![create-pr](../assets/create-pr.png)

Vous pouvez confirmer que la demande d’extraction a été envoyée en consultant l’onglet des demandes d’extraction dans https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
