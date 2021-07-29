---
title: Octroyer un accès utilisateur
description: Configurez les comptes utilisateur et les autorisations des membres de votre équipe dans Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 23%

---

# Octroyer un accès utilisateur

>[!NOTE]
>
>Adobe Experience Platform Launch a été rebaptisé en tant que suite de technologies de collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](../../term-updates.md) suivant pour consulter une référence consolidée des modifications terminologiques.

Avant de commencer à utiliser extension_package, vous devez configurer des comptes d’utilisateur et des autorisations pour les membres de votre équipe. Vous pouvez le faire avec [Adobe Admin Console](https://adminconsole.adobe.com/).

Ce document décrit les étapes à suivre pour accorder l’accès aux balises dans Adobe Experience Platform par le biais de Admin Console.

## Conditions préalables

Ce guide suppose que vous êtes un administrateur d’organisation tel qu’établi par Admin Console. Si vous avez besoin d’informations supplémentaires sur Admin Console et l’attribution de rôles, reportez-vous aux ressources suivantes :

* [Guide pour les administrateurs](https://helpx.adobe.com/fr/enterprise/administering/user-guide.html?topic=/enterprise/administering/morehelp/introduction.ug.js) : informations complètes sur Admin Console
* [Rôles d’administration des grands comptes](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html) : en savoir plus sur les différents types de rôles d’administration. Pour le guide ci-dessous, nous supposerons que vous êtes un administrateur d’organisation.

## Choix de votre organisation

Votre administrateur d’organisation Adobe Experience Cloud doit se connecter à [Admin Console](https://adminconsole.adobe.com/). Le premier écran est la vue d’ensemble.

![Onglet Aperçu de la console d’administration](../images/getting-started/admin-console-overview.png)

Certains d’entre vous peuvent avoir accès à plusieurs organisations. Pour ajouter la fonctionnalité de balises à l’organisation appropriée, sélectionnez le nom de l’organisation qui s’affiche dans le coin supérieur droit de l’écran. Sélectionnez ensuite l’organisation dans laquelle vous souhaitez utiliser les balises dans la liste déroulante.

![Menu déroulant de sélection de l’organisation de la console d’administration](../images/getting-started/admin-console-choose-org.png)

## Création d’un profil de produit

Un profil de produit est un groupe. Les droits individuels sont attribués aux profils de produits et tous les utilisateurs du profil hériteront de ces droits.

Sélectionnez le lien **[!UICONTROL Produits]** en haut et **[!UICONTROL Experience Cloud]** à gauche. Si l’interface utilisateur de collecte de données n’est pas répertoriée, les clients doivent contacter leur équipe de compte et les partenaires doivent envoyer un courrier électronique à l’adresse <ExchangeTechEC@adobe.com>.

![Onglet Produits de la console d’administration](../images/getting-started/admin-console-products-launch.png)

La capture d’écran ci-dessus montre un exemple de profil, il se peut que vous n’en ayez pas encore. Pour en créer un, sélectionnez **[!UICONTROL Nouveau profil]**. Dans l’écran **Créer un nouveau profil**, ajoutez simplement un **nom de profil** (test de collecte de données, par exemple) et une **description** facultative, puis sélectionnez **[!UICONTROL Enregistrer]** :

![Créer un affichage de profil](../images/getting-started/admin-console-create-a-new-profile.png)

Le profil de produit a maintenant été ajouté à l’organisation. Ajoutez ensuite des utilisateurs au profil de produit.

## Affecter des utilisateurs au profil de produit

Notez que le profil de produit affiche zéro pour **UTILISATEURS AUTORISÉS** et **ADMINS**. Sélectionnez le nom du profil de produit que vous avez créé (test de collecte de données dans notre exemple).

![Affichage des profils de produit](../images/getting-started/admin-console-profiles-add-user.png)

Sélectionnez l’onglet **[!UICONTROL Utilisateurs]** . Vous pouvez y rechercher des utilisateurs Adobe ID existants par courrier électronique ou ajouter de nouveaux utilisateurs à ce profil de produit. Sélectionnez **[!UICONTROL Ajouter un lien utilisateur]**.

![Onglet Utilisateurs de profils de produit](../images/getting-started/admin-console-add-launch-user.png)

Entrez un nom, un groupe d’utilisateurs ou une adresse électronique dans le champ de texte approprié. Dans la mesure du possible, il est recommandé d’inclure un prénom et un nom. Sélectionnez **[!UICONTROL Enregistrer]** pour ajouter l’utilisateur.

![Ajout d’un utilisateur à l’affichage Profil](../images/getting-started/admin-console-add-user.png)

Lorsque vous aurez tous les utilisateurs dont vous avez besoin dans ce profil de produit, nous leur ajouterons des autorisations. Sélectionnez l&#39;onglet **[!UICONTROL Autorisations.]** Dans l’écran des autorisations, vous voyez **[!UICONTROL Propriétés]**, **[!UICONTROL Droits d’entreprise]** et **[!UICONTROL Droits de propriété]**. Sélectionnez **[!UICONTROL Modifier]**.

![Onglet Autorisations des profils de produit](../images/getting-started/admin-console-profile-permissions.png)

Pour créer des extensions, votre équipe doit disposer au minimum des autorisations suivantes :

* &quot;Gérer les propriétés&quot; à partir du groupe d’entreprises.
* &quot;Gérer les extensions&quot;, &quot;Gérer les environnements&quot; et &quot;Développer&quot; à partir du groupe de propriétés.

Vous pouvez créer d’autres profils de produit avec des droits plus limités si vous le souhaitez, mais pour l’instant, il vous suffit de sélectionner **[!UICONTROL + Ajouter tout]** pour **Droits d’entreprise** et **Droits de propriété**. Veillez à sélectionner **[!UICONTROL Enregistrer]** sur chacun d’eux.

![Gestion des droits de propriété](../images/getting-started/admin-console-add-all-property-rights.png)

![Gestion des droits d’entreprise](../images/getting-started/admin-console-add-all-company-rights.png)

Jusqu’à présent, nous avons choisi l’organisation appropriée, créé un profil de produit, ajouté des utilisateurs au profil de produit et attribué des autorisations.

Cette opération effectue la configuration requise dans Admin Console. Vous et les membres de votre équipe qui ont été configurés en tant qu’utilisateurs pouvez désormais vous connecter à [l’interface utilisateur de collecte de données](https://launch.adobe.com/).

## Confirmer l’approvisionnement

Une fois que votre société a accès aux balises et que vos utilisateurs sont configurés comme décrit ci-dessus, vous devez pouvoir accéder à l’environnement de production à partir de l’[interface utilisateur de collecte de données](https://launch.adobe.com/). Si vous avez reçu les privilèges d’accès pour les balises et que vous avez suivi les étapes du Admin Console ci-dessus, mais que vous ne pouvez toujours pas vous connecter à l’interface utilisateur de collecte de données, contactez les représentants de l’assistance à l’Adobe.
