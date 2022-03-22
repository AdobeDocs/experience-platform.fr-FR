---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
solution: Experience Platform
title: Utilisation de l’interface web GitHub pour créer une page de documentation sur les sources
topic-legacy: tutorial
description: Ce document décrit les étapes à suivre pour utiliser l’interface web GitHub afin de créer de la documentation et d’envoyer une requête de tirage (PR).
hide: true
hidefromtoc: true
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: 39accd28edc388c6444910f9a2ea6d2f01acfdaf
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 2%

---

# Utilisation de l’interface web GitHub pour créer une page de documentation source

Ce document décrit les étapes à suivre pour utiliser l’interface web GitHub afin de créer de la documentation et d’envoyer une requête de tirage (PR).

>[!TIP]
>
>Vous pouvez utiliser les documents suivants du guide de contribution d’Adobe pour mieux prendre en charge votre processus de documentation : <ul><li>[Installation des outils de création Git et Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[Configuration locale du référentiel Git pour la documentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[Workflow de contributions GitHub pour les modifications majeures](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## Configuration de votre environnement GitHub

La première étape de la configuration de votre environnement GitHub consiste à accéder au [Référentiel GitHub Adobe Experience Platform](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

Ensuite, sélectionnez **Branchement**.

![double](../assets/fork.png)

Une fois le branchement terminé, sélectionnez **master** et saisissez le nom de votre nouvelle branche dans le menu déroulant qui s’affiche. Assurez-vous de fournir un nom explicite à votre branche, car il sera utilisé pour contenir votre travail, puis sélectionnez **créer une branche**.

![create-branch](../assets/create-branch.png)

Dans la structure de dossiers GitHub de votre référentiel dupliqué, accédez à [`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create) puis sélectionnez la catégorie appropriée à votre source dans la liste. Par exemple, si vous créez de la documentation pour une nouvelle source de stockage dans le cloud, sélectionnez **espace de stockage dans le cloud**.

>[!TIP]
>
>Si vous créez une documentation pour l’interface utilisateur, accédez à [`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create) et sélectionnez la catégorie appropriée à votre source. Pour ajouter vos images, accédez à [`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create) ajoutez ensuite vos captures d’écran à la `sdk` dossier.

![espace de stockage dans le cloud](../assets/cloud-storage.png)

Un dossier de sources de stockage dans le cloud existantes s’affiche. Pour ajouter la documentation d’une nouvelle source, sélectionnez **Ajouter un fichier** puis sélectionnez **Créer un fichier** dans le menu déroulant qui s’affiche.

![create-new-file](../assets/create-new-file.png)

Nommez votre fichier source. `YOURSOURCE.md` où YOURSOURCE est le nom de votre source dans Platform. Par exemple, si votre société est [!DNL Mailchimp], alors votre nom de fichier doit être `mailchimp.md`.

![git-interface](../assets/git-interface.png)

## Créez la page de documentation de votre source.

Pour commencer à documenter votre nouvelle source, collez le contenu de la [modèle de documentation sources](./template.md) dans l’éditeur web GitHub. Vous pouvez également télécharger le modèle. [here](../assets/template.zip).

Une fois le modèle copié dans l’interface de l’éditeur web GitHub, suivez les instructions décrites dans le modèle et modifiez les valeurs contenant les informations pertinentes pour votre source.

![paste-template](../assets/paste-template.png)

Une fois terminé, validez le fichier dans votre branche.

![commit](../assets/commit.png)

## Soumettre votre documentation pour révision

Une fois votre fichier validé, vous pouvez ouvrir une requête de tirage (PR) pour fusionner votre branche opérationnelle dans la branche principale du référentiel de documentation Adobe. Assurez-vous que la branche sur laquelle vous avez travaillé est sélectionnée, puis sélectionnez **Comparaison et extraction de requête**.

![compare-pr](../assets/compare-pr.png)

Assurez-vous que les branches de base et de comparaison sont correctes. Ajoutez une note au communiqué, décrivant votre mise à jour, puis sélectionnez **Créer une requête d’extraction**. Cela ouvre une requête de tirage pour fusionner la branche opérationnelle de votre travail dans la branche principale du référentiel Adobe.

>[!TIP]
>
>Laissez le champ **Autorisation des modifications par les responsables** case à cocher sélectionnée pour vous assurer que l’équipe de documentation d’Adobe peut apporter des modifications au résiduel.

![create-pr](../assets/create-pr.png)

À ce stade, une notification s’affiche pour vous inviter à signer le contrat de licence du contributeur Adobe (CLA). Cette étape est obligatoire. Après avoir signé le contrat de licence du contributeur, actualisez la page de requête de tirage et envoyez la requête de tirage.

Vous pouvez confirmer que la demande d’extraction a été envoyée en consultant l’onglet des demandes d’extraction dans https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
