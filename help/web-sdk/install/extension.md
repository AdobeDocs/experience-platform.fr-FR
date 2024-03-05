---
title: Installation du SDK Web à l’aide de l’extension de balise
description: Référencez la bibliothèque SDK Web à l’aide de la collecte de données Adobe Experience Cloud.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Installation du SDK Web à l’aide de l’extension de balise

Adobe propose une extension de balise dédiée pour mettre en oeuvre et configurer le SDK Web. Cette méthode d’implémentation est la principale méthode recommandée par Adobe pour déployer et gérer le code de collecte de données.

Une fois que vous avez rencontré le [conditions préalables](overview.md), vous pouvez déployer l’extension de balise du SDK Web en procédant comme suit :

## Installer l’extension dans une balise

1. Connexion à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez une propriété de balise ou créez une propriété de balise.
1. Accédez à **[!UICONTROL Extensions]**, puis sélectionnez la variable **[!UICONTROL Catalogue]** .
1. Recherchez et installez le **[!UICONTROL SDK Web Adobe Experience Platform]** extension .
1. Sélectionnez l’environnement de test et le flux de données appropriés pour chaque environnement, puis cliquez sur **[!UICONTROL Enregistrer]**.

## Publier le code de balise dans le développement

L’extension SDK Web est désormais installée pour cette balise. Vous pouvez désormais publier le code de balise pour l’utiliser dans un environnement de développement.

1. Accédez à **[!UICONTROL Flux de publication]**, puis sélectionnez **[!UICONTROL Ajouter une bibliothèque]**.
1. Donnez à cette bibliothèque le nom de votre choix, par exemple &quot;Ajouter une bibliothèque SDK Web&quot;. Définissez la variable [!UICONTROL Environnement] dans le menu déroulant &quot;Développement&quot;.
1. Sélectionner **[!UICONTROL Ajouter toutes les ressources modifiées]**, puis cliquez sur **[!UICONTROL Enregistrement et création pour le développement]**.

## Installation du code de chargeur sur votre site

Maintenant que le code de balise est publié, vous pouvez ajouter le code de chargeur de balises à votre site web.

1. Accédez à **[!UICONTROL Environnements]**, puis cliquez sur l’icône de boîte en regard de &quot;Développement&quot; pour ouvrir une fenêtre modale contenant des instructions d’installation pour cet environnement.
1. Copiez le code incorporé et collez-le dans le `<head>` balise de votre site web.

## Remplir votre mise en oeuvre et publier en production

Voir [Présentation de l’extension SDK Web](../../tags/extensions/client/web-sdk/overview.md) pour plus d’informations sur l’extension elle-même, et [Présentation des balises](../../tags/home.md) pour plus d’informations sur la navigation dans l’interface des balises.
