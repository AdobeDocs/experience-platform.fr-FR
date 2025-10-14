---
title: Utilisation de Adobe Experience Platform Assurance
description: Ce guide explique comment utiliser Adobe Experience Platform Assurance une fois qu’il a été installé et mis en oeuvre.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Utilisation de Adobe Experience Platform Assurance

Ce tutoriel explique comment utiliser Adobe Experience Platform Assurance. Pour plus d’informations sur l’installation et la mise en oeuvre de l’extension Adobe Experience Platform Assurance, consultez le tutoriel sur la [mise en oeuvre de l’extension Assurance](./implement-assurance.md).

## Créer des sessions

Après vous être connecté à l’ [interface utilisateur d’assurance](https://experience.adobe.com/assurance), vous pouvez sélectionner **[!UICONTROL Créer une session]** pour commencer à créer une session.

![&#x200B; Le bouton Créer une session est mis en surbrillance, vous indiquant où vous pouvez créer une session.](./images/using-assurance/create-session.png)

La boîte de dialogue **[!UICONTROL Créer une session]** s’affiche. Veuillez consulter les instructions données et poursuivre en sélectionnant **[!UICONTROL Démarrer]**.

![La boîte de dialogue Créer une nouvelle session s’affiche et affiche des instructions sur l’utilisation d’Assurance.](./images/using-assurance/create-new-session.png)

Vous pouvez maintenant saisir un nom pour identifier la session, puis fournir une **[!UICONTROL URL de base]** (URL de création de liens profonds pour votre application). Après avoir fourni ces détails, sélectionnez **[!UICONTROL Suivant]**.

>[!INFO]
>
>L’URL de base est la définition racine utilisée pour lancer votre application à partir d’une URL. Une URL de session est générée par laquelle vous pouvez lancer la session d’assurance. Exemple de valeur : `myapp://default` Dans le champ **[!UICONTROL URL de base]**, saisissez la définition de lien profond de base de votre application.

![&#x200B; Le workflow complet de création d&#39;une nouvelle session s&#39;affiche.](./images/using-assurance/create-session.gif)

## Connexion à une session

Après avoir créé une session, assurez-vous que la boîte de dialogue **[!UICONTROL Créer une session]** s’affiche désormais avec un lien, un code QR et un code PIN.

![Une boîte de dialogue présentant les options de connexion à votre session d’assurance s’affiche.](./images/using-assurance/create-new-session-pin.png)

Si cette boîte de dialogue s’affiche, vous pouvez utiliser l’application d’appareil photo de votre appareil pour analyser le code QR et ouvrir votre application, ou copier le lien et l’ouvrir dans votre application. Lorsque votre application est lancée, l’écran de saisie du code PIN doit s’afficher en superposition. Saisissez le code PIN de l’étape précédente et appuyez sur **[!UICONTROL Se connecter]**.

Vous pouvez vérifier que votre application est connectée à Assurance lorsque l’icône Adobe Experience Platform (Adobe rouge &quot;A&quot;) s’affiche sur votre application.

![&#x200B; Le workflow complet de connexion de votre application à une session d&#39;assurance s&#39;affiche.](./images/using-assurance/connect-session.gif)

## Exporter une session

Pour exporter une session d’assurance, sur la page des détails des sessions de votre application, sélectionnez **[!UICONTROL Exporter vers JSON]** dans une session :

![Exporter une session](./images/using-assurance/export-session.png)

L’option d’exportation respecte les résultats des filtres de recherche et exporte uniquement les événements affichés dans la vue d’événement. Par exemple, si vous avez recherché des événements &quot;track&quot;, puis sélectionnez **[!UICONTROL Export to JSON]**, seuls les résultats d’événement &quot;track&quot; sont exportés.
