---
title: Prise en main de l’API du Privacy Service
description: Découvrez comment vous authentifier auprès de l’API du Privacy Service et comment interpréter des exemples d’appels API dans la documentation.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 16%

---

# Prise en main de l’API du Privacy Service

Ce guide présente les concepts de base que vous devez connaître avant d’effectuer des appels vers l’API Adobe Experience Platform Privacy Service.

## Conditions préalables

Ce guide nécessite une compréhension pratique de [Privacy Service](../home.md) et la manière dont il vous permet de gérer les requêtes d’accès et de suppression de vos sujets des données (clients) dans les applications Adobe Experience Cloud.

Afin de créer des informations d’identification d’accès pour l’API, un administrateur de votre entreprise doit avoir préalablement configuré les profils de produit pour Privacy Service dans Adobe Admin Console. Le profil de produit que vous affectez à une intégration d’API détermine les autorisations dont dispose cette intégration lors de l’accès aux fonctionnalités de Privacy Service. Consultez le guide sur la [gestion des autorisations de Privacy Service](../permissions.md) pour plus d’informations.

## Collecte des valeurs des en-têtes requis

Pour passer des appels à l’API du Privacy Service, vous devez d’abord rassembler vos informations d’identification d’accès à utiliser dans les en-têtes requis :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Ces valeurs sont générées à l’aide de [Console Adobe Developer](https://developer.adobe.com/console). Votre `{ORG_ID}` et `{API_KEY}` ne doit être généré qu’une seule fois et peut être réutilisé dans les prochains appels API. Cependant, votre `{ACCESS_TOKEN}` est temporaire et doit être régénéré toutes les 24 heures.

Les étapes de génération de ces valeurs sont décrites en détail ci-dessous.

### Configuration ponctuelle

Accédez à [Adobe Developer Console](https://developer.adobe.com/console) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le tutoriel sur la [création d’un projet vide](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) dans la documentation de Developer Console.

Une fois que vous avez créé un projet, sélectionnez **[!UICONTROL Ajouter au projet]** et choisissez **[!UICONTROL API]** dans le menu déroulant.

![L’option API sélectionnée dans la [!UICONTROL Ajouter au projet] menu déroulant de la page des détails du projet dans Developer Console](../images/api/getting-started/add-api-button.png)

#### Sélection d’une API et génération d’une paire de clés {#keypair}

L’écran **[!UICONTROL Ajouter une API]** s’affiche. Sélectionner **[!UICONTROL Experience Cloud]** pour réduire la liste des API disponibles, puis sélectionnez la carte pour **[!UICONTROL API Privacy Service]** avant de sélectionner **[!UICONTROL Suivant]**.

![La carte API du Privacy Service sélectionnée dans la liste des API disponibles](../images/api/getting-started/add-privacy-service-api.png)

Le **[!UICONTROL Configuration de l’API]** s’affiche. Sélectionnez l’option pour **[!UICONTROL Générer une paire de clés]**, puis sélectionnez **[!UICONTROL Générer une paire de clés]**.

![Le [!UICONTROL Générer une paire de clés] l’option sélectionnée sur la [!UICONTROL Configuration de l’API] écran](../images/api/getting-started/generate-key-pair.png)

La paire de clés est automatiquement générée et un fichier ZIP contenant une clé privée et un certificat public est téléchargé par votre navigateur (il sera utilisé à une étape ultérieure). Sélectionnez **[!UICONTROL Suivant]** pour continuer.

![La paire de clés générée affichée dans l’interface utilisateur, dont les valeurs sont automatiquement téléchargées par le navigateur.](../images/api/getting-started/key-pair-generated.png)

#### Attribution d’autorisations via les profils de produit {#product-profiles}

La dernière étape de configuration consiste à sélectionner les profils de produit à partir desquels cette intégration héritera de ses autorisations. Si vous sélectionnez plusieurs profils, leurs jeux d’autorisations seront combinés pour l’intégration.

>[!NOTE]
>
>Les profils de produit et les autorisations granulaires qu’ils fournissent sont créés et gérés par les administrateurs via Adobe Admin Console. Consultez le guide sur la [Autorisations des Privacy Service](../permissions.md) pour plus d’informations.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer l’API configurée]**.

![Un profil de produit unique sélectionné dans la liste avant d’enregistrer la configuration](../images/api/getting-started/select-product-profiles.png)

Une fois l’API ajoutée au projet, la page du projet réapparaît sur la page **API Privacy Service - Aperçu** page. À partir de là, faites défiler l’écran jusqu’au **[!UICONTROL Compte de service (JWT)]** , qui fournit les informations d’identification d’accès suivantes requises dans tous les appels à l’API du Privacy Service :

* **[!UICONTROL ID CLIENT]**: L’identifiant du client est obligatoire. `{API_KEY}` qui doit être fourni dans la variable `x-api-key` en-tête .
* **[!UICONTROL ID D’ORGANISATION]** : l’ID d’organisation est la valeur `{ORG_ID}` qui doit être utilisée dans l’en-tête `x-gw-ims-org-id`.

![Les valeurs de l’ID client et de l’ID d’organisation telles qu’elles apparaissent sur la page d’aperçu du projet une fois l’API configurée](../images/api/getting-started/jwt-credentials.png)

### Authentification pour chaque session

Les dernières informations d’identification requises que vous devez recueillir sont vos `{ACCESS_TOKEN}`, qui est utilisé dans l’en-tête d’autorisation. Contrairement aux valeurs de `{API_KEY}` et `{ORG_ID}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser l’API.

En règle générale, il existe deux méthodes pour générer un jeton d’accès :

* [Génération manuelle du jeton](#manual-token) pour les tests et le développement.
* [Automatiser la génération des jetons](#auto-token) pour les intégrations d’API.

#### Génération manuelle d’un jeton {#manual-token}

Pour générer manuellement une nouvelle `{ACCESS_TOKEN}`, ouvrez la clé privée précédemment téléchargée et collez son contenu dans la zone de texte située à côté. **[!UICONTROL Générer un jeton d’accès]** avant de sélectionner **[!UICONTROL Générer un jeton]**.

![Le jeton d’accès généré précédemment est collé sur la page d’aperçu du projet, avec la variable [!UICONTROL Générer un jeton] bouton sélectionné après](../images/api/getting-started/paste-private-key.png)

Un nouveau jeton d’accès est généré et un bouton permettant de copier le jeton dans le presse-papiers est fourni. Cette valeur est utilisée pour l’en-tête d’autorisation requis et doit être fournie au format . `Bearer {ACCESS_TOKEN}`.

![Le jeton d’accès généré en cours de copie à partir de l’interface utilisateur](../images/api/getting-started/generated-access-token.png)

#### Automatiser la génération des jetons {#auto-token}

Vous pouvez générer de nouveaux jetons d’accès pour les processus automatisés en envoyant un jeton Web JSON (JWT) via une demande de POST pour Adobe Identity Management Service (IMS). Consultez le document Developer Console sur [Authentification JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) pour obtenir des instructions détaillées.

## Lecture d’exemples d’appels API

Chaque guide de point de terminaison fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur [lecture d’exemples d’appels API](../../landing/api-guide.md#sample-api) dans le guide de prise en main des API Platform.

## Étapes suivantes

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l’API Privacy Service. Sélectionnez l’un des guides de point d’entrée pour commencer :

* [Tâches de confidentialité](./privacy-jobs.md)
* [Consentement](./consent.md)
