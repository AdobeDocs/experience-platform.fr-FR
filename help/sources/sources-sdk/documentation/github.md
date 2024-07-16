---
keywords: Experience Platform;accueil;rubriques populaires;sources;connecteurs;connecteurs source;sdk sources;sdk;SDK
solution: Experience Platform
title: Utilisation de l’interface web GitHub pour créer une page de documentation sur les sources
description: Ce document décrit les étapes à suivre pour utiliser l’interface web GitHub afin de créer de la documentation et d’envoyer une requête de tirage (PR).
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 2%

---

# Utilisation de l’interface web GitHub pour créer une page de documentation source

Ce document décrit les étapes à suivre pour utiliser l’interface web GitHub afin de créer de la documentation et d’envoyer une requête de tirage (PR).

>[!TIP]
>
>Vous pouvez utiliser les documents suivants du guide de contribution d’Adobe pour mieux prendre en charge votre processus de documentation : <ul><li>[Installer les outils de création Git et Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)</li><li>[Configuration locale du référentiel Git pour la documentation](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)</li><li>[Workflow de contribution GitHub pour les modifications majeures](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)</li></ul>

## Configuration de votre environnement GitHub

La première étape de la configuration de votre environnement GitHub consiste à accéder au [référentiel GitHub Adobe Experience Platform](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

Sélectionnez ensuite **Branchement**.

![fork](../assets/fork.png)

Une fois le branchement terminé, sélectionnez **master** et saisissez le nom de votre nouvelle branche dans le menu déroulant qui s’affiche. Assurez-vous de fournir un nom explicite pour votre branche, car il sera utilisé pour contenir votre travail, puis sélectionnez **créer une branche**.

![create-branch](../assets/create-branch.png)

Dans la structure de dossiers GitHub de votre référentiel dupliqué, accédez à [`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create), puis sélectionnez la catégorie appropriée à votre source dans la liste. Par exemple, si vous créez de la documentation pour une nouvelle source de gestion de la relation client, sélectionnez **crm**.

>[!TIP]
>
>Si vous créez une documentation pour l’interface utilisateur, accédez à [`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create) et sélectionnez la catégorie appropriée pour votre source. Pour ajouter vos images, accédez à [`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create), puis ajoutez vos captures d’écran au dossier `sdk`.

![crm](../assets/crm.png)

Un dossier de sources CRM existantes s’affiche. Pour ajouter la documentation d’une nouvelle source, sélectionnez **Ajouter un fichier**, puis **Créer un fichier** dans le menu déroulant qui s’affiche.

![create-new-file](../assets/create-new-file.png)

Nommez votre fichier source `YOURSOURCE.md` où YOURSOURCE est le nom de votre source dans Platform. Par exemple, si votre société est ACME CRM, votre nom de fichier doit être `acme-crm.md`.

![git-interface](../assets/git-interface.png)

## Créez la page de documentation de votre source.

Pour commencer à documenter votre nouvelle source, collez le contenu du [modèle de documentation de sources](./template.md) dans l’éditeur web GitHub. Vous pouvez également télécharger le modèle [ici](../assets/api-template.zip).

Une fois le modèle copié dans l’interface de l’éditeur web GitHub, suivez les instructions décrites dans le modèle et modifiez les valeurs contenant les informations pertinentes pour votre source.

![paste-template](../assets/paste-template.png)

Une fois terminé, validez le fichier dans votre branche.

![commit](../assets/commit.png)

## Soumettre votre documentation pour révision

Une fois votre fichier validé, vous pouvez ouvrir une requête de tirage (PR) pour fusionner votre branche opérationnelle dans la branche principale du référentiel de documentation Adobe. Assurez-vous que la branche sur laquelle vous avez travaillé est sélectionnée, puis sélectionnez **Comparer et extraire la requête**.

![compare-pr](../assets/compare-pr.png)

Assurez-vous que les branches de base et de comparaison sont correctes. Ajoutez une note au document de présentation, décrivant votre mise à jour, puis sélectionnez **Créer une requête de tirage**. Cela ouvre une requête de tirage pour fusionner la branche opérationnelle de votre travail dans la branche principale du référentiel Adobe.

>[!TIP]
>
>Laissez la case à cocher **Autoriser les modifications par les responsables** sélectionnée pour vous assurer que l’équipe de documentation d’Adobe peut apporter des modifications au résiduel.

![create-pr](../assets/create-pr.png)

À ce stade, une notification s’affiche pour vous inviter à signer le contrat de licence du contributeur Adobe (CLA). Cette étape est obligatoire. Après avoir signé le contrat de licence du contributeur, actualisez la page de requête de tirage et envoyez la requête de tirage.

Vous pouvez confirmer que la demande d’extraction a été envoyée en consultant l’onglet des demandes d’extraction dans https://github.com/AdobeDocs/experience-platform.en.

![confirm-pr](../assets/confirm-pr.png)
