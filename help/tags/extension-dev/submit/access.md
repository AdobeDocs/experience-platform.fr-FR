---
title: Octroyer un accès utilisateur
description: Configurez les comptes utilisateur et les autorisations liés aux balises des membres de votre équipe dans Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: ht
source-wordcount: '738'
ht-degree: 100%

---

# Octroyer un accès utilisateur

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Avant de commencer à utiliser extension_package, vous devez configurer des comptes d’utilisateur et des autorisations pour les membres de votre équipe. Vous pouvez le faire avec [Adobe Admin Console](https://adminconsole.adobe.com/).

Ce document fournit des étapes permettant d’octroyer l’accès aux balises dans Adobe Experience Platform par l’intermédiaire d’Admin Console.

## Conditions préalables

Ce guide suppose que vous êtes un administrateur d’organisation tel qu’établi par Admin Console. Si vous avez besoin d’informations supplémentaires sur Admin Console et l’attribution de rôles, reportez-vous aux ressources suivantes :

* [Guide pour les administrateurs](https://helpx.adobe.com/fr/enterprise/administering/user-guide.html?topic=/enterprise/administering/morehelp/introduction.ug.js) : informations complètes sur Admin Console
* [Rôles d’administration des grands comptes](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html) : en savoir plus sur les différents types de rôles d’administration. Pour le guide ci-dessous, nous supposerons que vous êtes un administrateur d’organisation.

## Choix de votre organisation

Votre administrateur d’organisation Adobe Experience Cloud doit se connecter à [Admin Console](https://adminconsole.adobe.com/). Le premier écran affiche la présentation.

![Onglet de présentation d’Admin Console](../images/getting-started/admin-console-overview.png)

Certains d’entre vous peuvent avoir accès à plusieurs organisations (Org). Pour ajouter la fonctionnalité de balises à l’organisation appropriée, sélectionnez le nom de l’organisation qui s’affiche dans le coin supérieur droit de l’écran. Dans la liste déroulante, sélectionnez ensuite l’organisation dans laquelle vous souhaitez utiliser les balises.

![Menu déroulant de sélection d’organisation d’Admin Console](../images/getting-started/admin-console-choose-org.png)

## Création d’un profil de produits

Un profil de produits est un groupe. Les droits individuels sont attribués aux profils de produits et tous les utilisateurs du profil hériteront de ces droits.

Cliquez sur le lien **[!UICONTROL Produits]** en haut de l’écran, puis sur **[!UICONTROL Experience Cloud]** à gauche. Si lʼinterface utilisateur de la collecte de données nʼest pas répertoriée, les clients doivent contacter leur équipe de compte, et les partenaires doivent envoyer un e-mail à <ExchangeTechEC@adobe.com>.

![Onglet Produits d’Admin Console](../images/getting-started/admin-console-products-launch.png)

La capture d’écran ci-dessus présente un exemple de profil. Il se peut que vous n’en ayez pas encore. Pour en créer un, sélectionnez **[!UICONTROL Nouveau profil]**. Dans l’écran **Créer un profil**, ajoutez simplement un **Nom de profil** (Test de collecte de données, par exemple) et une **Description** facultative, puis cliquez sur **[!UICONTROL Enregistrer]** :

![Création d’un affichage de profil](../images/getting-started/admin-console-create-a-new-profile.png)

Le profil de produits a bien été ajouté à l’organisation. Ajoutez ensuite des utilisateurs au profil de produits.

## Attribution d’utilisateurs au profil de produits

Veuillez noter que le profil de produits affiche zéro pour les **UTILISATEURS** et **ADMINISTRATEURS AUTORISÉS**. Cliquez sur le nom du profil de produits que vous avez créé (Test de collecte de données dans notre exemple).

![Affichage des profils de produits](../images/getting-started/admin-console-profiles-add-user.png)

Sélectionnez l’onglet **[!UICONTROL Utilisateurs]**. Cet onglet vous permet de rechercher des utilisateurs Adobe ID existants à l’aide de leur adresse électronique ou d’ajouter de nouveaux utilisateurs au profil de produits. Sélectionnez **[!UICONTROL Ajouter un lien utilisateur]**.

![Onglet Utilisateurs des profils de produits](../images/getting-started/admin-console-add-launch-user.png)

Saisissez un nom, un groupe d’utilisateurs ou une adresse électronique dans le champ de texte approprié. Dans la mesure du possible, il est recommandé d’inclure un prénom et un nom. Sélectionnez **[!UICONTROL Enregistrer]** pour ajouter l’utilisateur.

![Ajout d’un utilisateur à l’affichage du profil](../images/getting-started/admin-console-add-user.png)

Lorsque vous disposerez de tous les utilisateurs dont vous avez besoin dans ce profil de produits, nous leur ajouterons des autorisations. Sélectionnez l’onglet **[!UICONTROL Autorisations.]** Dans l’écran Autorisations, **[!UICONTROL Propriétés]**, **[!UICONTROL Droits de société]** et **[!UICONTROL Droits de propriété]** s’affichent. Sélectionnez **[!UICONTROL Modifier]**.

![Onglet Autorisations des profils de produits](../images/getting-started/admin-console-profile-permissions.png)

Pour créer des extensions, votre équipe doit au minimum disposer des autorisations suivantes :

* « Gérer les propriétés » à partir du groupe de société.
* « Gérer les extensions », « Gérer les environnements » et « Développer » à partir du groupe de propriétés.

Si vous le souhaitez, vous pouvez créer d’autres profils de produits avec des droits plus limités. Toutefois, il vous suffit pour l’instant de sélectionner **[!UICONTROL + Ajouter tout]** pour **Droits de société** et **Droits de propriété**. Veillez à sélectionner **[!UICONTROL Enregistrer]** pour chacun.

![Gestion des droits de propriété](../images/getting-started/admin-console-add-all-property-rights.png)

![Gestion des droits de société](../images/getting-started/admin-console-add-all-company-rights.png)

Jusqu’à présent, nous avons choisi l’organisation appropriée, créé un profil de produits, ajouté des utilisateurs au profil de produits et attribué des autorisations.

Cela conclut la configuration requise dans Admin Console. Vous et les membres de votre équipe qui ont été configurés en tant qu’utilisateurs pouvez désormais vous connecter à l’[interface utilisateur de la collecte de données](https://launch.adobe.com/).

## Confirmation de l’approvisionnement

Une fois l’accès aux balises attribué à votre société et vos utilisateurs configurés comme décrit ci-dessus, vous devez pouvoir accéder à l’environnement de production à partir de l’[interface utilisateur de la collecte de données](https://launch.adobe.com/). Si des privilèges d’accès aux balises vous ont été attribués et que vous avez suivi les étapes d’Admin Console ci-dessus, mais que vous ne pouvez toujours pas vous connecter à l’interface utilisateur de la collecte de données, contactez les représentants du support Adobe.
