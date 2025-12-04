---
title: Utilisation d’Adobe Experience Platform Assurance
description: Ce guide explique comment utiliser Adobe Experience Platform Assurance une fois qu’il a été installé et implémenté.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: f8576e7f7e1da7351f7860cba27d5d09d0161132
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 3%

---

# Utilisation d’Adobe Experience Platform Assurance

Ce tutoriel explique comment utiliser Adobe Experience Platform Assurance. Pour obtenir des instructions sur l’installation et l’implémentation de l’extension Adobe Experience Platform Assurance, consultez le tutoriel sur [l’implémentation de l’extension Assurance](./implement-assurance.md).

## Créer des sessions

Après vous être connecté à l’interface utilisateur [Assurance](https://experience.adobe.com/assurance), vous pouvez sélectionner **[!UICONTROL Create Session]** pour commencer à créer une session.

![Le bouton Créer une session est mis en surbrillance et indique où vous pouvez créer une session.](./images/using-assurance/create-session.png)

La boîte de dialogue **[!UICONTROL Create New Session]** s’affiche avec deux options pour créer une session :

### Connexion de lien profond

Sélectionnez cette option pour générer une URL de session unique, un code QR et un code PIN. Scannez le code QR ou ouvrez manuellement le lien de session dans votre application, puis saisissez le code confidentiel pour établir la connexion.

Sélectionnez **[!UICONTROL Deep link connect]** et continuez en sélectionnant **[!UICONTROL Start]**.

![La boîte de dialogue Créer une session affichant l’option de connexion de lien profond sélectionnée.](./images/using-assurance/create-new-session-deep-link.png)

Vous pouvez maintenant saisir un nom pour identifier la session, puis fournir une **[!UICONTROL Base URL]** (URL de lien profond pour votre application). Après avoir fourni ces détails, sélectionnez **[!UICONTROL Next]**.

>[!INFO]
>
>L’URL de base est la définition racine utilisée pour lancer votre application à partir d’une URL. Une URL de session est générée par laquelle vous pouvez lancer la session Assurance. Voici un exemple de valeur : `myapp://default` Dans le champ **[!UICONTROL Base URL]** , saisissez la définition du lien profond de base de votre application.

![Les champs Nom de session et Entrée de l’URL de base s’affichent.](./images/using-assurance/create-session-form-deep-link.png)

### Connexion rapide

Déclenchez une connexion à partir de votre application pour que votre appareil apparaisse dans la liste des appareils disponibles. Sélectionnez **[!UICONTROL Quick connect]** pour créer la session Assurance.

#### Conditions préalables

Avant d’utiliser Quick Connect, vérifiez que votre application dispose des versions et de l’implémentation SDK requises :

**Conditions requises pour Android SDK :**

- Mobile Core v3.1.0 ou version ultérieure
- Adobe Journey Optimizer v3.1.0 ou version ultérieure
- Adobe Experience Platform Assurance v3.0.4 ou version ultérieure

**Conditions requises pour iOS SDK :**

- Mobile Core v5.2.0 ou version ultérieure
- Adobe Journey Optimizer v5.1.1 ou version ultérieure
- Adobe Experience Platform Assurance v5.0.0 ou version ultérieure

**Implémentation :**

Votre application doit mettre en œuvre l’API [`startSession`](https://developer.adobe.com/client-sdks/home/base/assurance/api-reference/#startsession-quick-connect) pour déclencher la connexion Assurance. Cet appel API est généralement inclus dans un jeu d’actions ou déclenché dans votre application.

#### Création d’une session de connexion rapide

![La boîte de dialogue Créer une session affiche l’option Connexion rapide sélectionnée.](./images/using-assurance/create-new-session-quick-connect.png)

Sélectionnez **[!UICONTROL Quick connect]** et continuez en sélectionnant **[!UICONTROL Start]**. L’interface du sélecteur d’appareil s’affiche :

1. **Déclencher la connexion Assurance** - Dans votre application mobile ou implémentation, déclenchez l’action qui lance la connexion Assurance à l’aide de l’API `startSession`. Votre appareil sera ainsi détectable.

2. **Sélectionner et connecter votre appareil** - Une fois que votre appareil apparaît dans la liste des appareils disponibles, sélectionnez-le et cliquez sur **[!UICONTROL Connect]**.

![Interface du sélecteur d’appareils Quick Connect affichant les appareils disponibles.](./images/using-assurance/quick-connect-device-picker.png)

## Connexion à une session

Les étapes de connexion dépendent du type de session utilisé :

### Sessions de connexion profonde

Pour les sessions créées avec **[!UICONTROL Deep Link Connect]** :

1. Accédez à la page des détails de la session (pour les sessions existantes) ou passez à la création de la session pour afficher le lien, le code QR et le code confidentiel
2. Utilisez l’application de caméra de votre appareil pour scanner le code QR, ou copiez le lien et ouvrez-le dans votre application
3. Lors du lancement de votre application, l’écran de saisie du code confidentiel est superposé. Saisissez le code confidentiel et appuyez sur **[!UICONTROL Connect]**

![Une boîte de dialogue affichant les options de connexion à votre session Assurance s’affiche.](./images/using-assurance/deep-link-connection.png)

### Sessions de connexion rapide

Pour les sessions créées avec **[!UICONTROL Quick Connect]** (identifiables par une URL de session commençant par `adobeassurance://`), la connexion se fait automatiquement via l’interface du sélecteur d’appareil :

1. Accédez à la page des détails de la session (pour les sessions existantes) ou continuez depuis la création de la session
2. Dans la section **[!UICONTROL Connect Device]**, vous verrez l’interface du sélecteur d’appareil
3. Déclenchez l’action définie dans votre application pour rendre l’appareil détectable
4. Sélectionnez votre appareil dans la liste et cliquez sur **[!UICONTROL Connect]**

![Interface du sélecteur d’appareils affichant les appareils disponibles pour la connexion.](./images/using-assurance/quick-connect-device-picker.png)

### Vérification de la connexion

Vous pouvez vérifier que votre application est connectée à Assurance lorsque l’icône Adobe Experience Platform (Adobe « A » rouge) s’affiche sur l’application.

## Exporter une session

Pour exporter une session Assurance, sur la page de détails des sessions de votre application, sélectionnez **[!UICONTROL Export to JSON]** dans une session :

![Exporter une session](./images/using-assurance/export-session.png)

L’option d’exportation respecte les résultats des filtres de recherche et exporte uniquement les événements affichés dans la vue d’événement. Par exemple, si vous avez recherché des événements de « suivi », puis sélectionné **[!UICONTROL Export to JSON]**, seuls les résultats des événements de « suivi » sont exportés.