---
title: Installation du SDK Web à l’aide de l’extension de balise
description: Référencez la bibliothèque SDK Web à l’aide de la collecte de données Adobe Experience Cloud.
exl-id: ba8348c9-f642-4230-9f7f-4496d4154d83
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Installation du SDK Web à l’aide de l’extension de balise

Adobe propose une extension de balise dédiée pour mettre en oeuvre et configurer le SDK Web. Cette méthode d’implémentation est la principale méthode recommandée par Adobe pour déployer et gérer le code de collecte de données.

Une fois que vous avez satisfait aux [conditions préalables](overview.md), vous pouvez déployer l’extension de balise SDK Web en suivant les étapes suivantes :

## Installer l’extension dans une balise

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com?lang=fr) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez une propriété de balise ou créez une propriété de balise.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]** .
1. Recherchez et installez l’extension **[!UICONTROL Adobe Experience Platform Web SDK]**.
1. Sélectionnez l’environnement de test et le flux de données appropriés pour chaque environnement, puis cliquez sur **[!UICONTROL Enregistrer]**.

Pour plus d’informations, consultez la documentation sur la [configuration de l’extension de balise SDK Web](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) .

## Publish du code de balise au développement

L’extension SDK Web est désormais installée pour cette balise. Vous pouvez désormais publier le code de balise pour l’utiliser dans un environnement de développement.

1. Accédez à **[!UICONTROL Flux de publication]**, puis sélectionnez **[!UICONTROL Ajouter une bibliothèque]**.
1. Donnez à cette bibliothèque le nom de votre choix, par exemple &quot;Ajouter une bibliothèque SDK Web&quot;. Définissez le menu déroulant [!UICONTROL Environnement] sur &quot;Développement&quot;.
1. Sélectionnez **[!UICONTROL Ajouter toutes les ressources modifiées]**, puis cliquez sur **[!UICONTROL Enregistrer et créer dans le développement]**.

## Installation du code de chargeur sur votre site

Maintenant que le code de balise est publié, vous pouvez ajouter le code de chargeur de balises à votre site web.

1. Accédez à **[!UICONTROL Environments]** (Environnements), puis cliquez sur l’icône Zone en regard de &quot;Development&quot; (Développement) pour ouvrir une fenêtre modale contenant des instructions d’installation pour cet environnement.
1. Copiez le code incorporé et collez-le dans la balise `<head>` de votre site web.

## Remplir votre mise en oeuvre et publier en production

Pour plus d’informations sur l’extension elle-même, consultez la [présentation de l’extension SDK Web](../../tags/extensions/client/web-sdk/overview.md) et la [présentation des balises](../../tags/home.md) pour plus d’informations sur la navigation dans l’interface des balises.
