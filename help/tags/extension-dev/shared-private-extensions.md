---
title: Gestion des extensions de balises
description: Découvrez comment gérer et partager des packages d’extension dans Adobe Experience Platform Tags.
exl-id: 3dfd801a-febc-4461-bd99-5f97682518ce
source-git-commit: 91c8b36ec1b752e288ed8be61f3946eaf8532760
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 0%

---

# Gestion de l’extension de balises

Adobe Experience Platform permet de gérer les extensions **[!UICONTROL Owned]**. Vous pouvez charger de nouvelles extensions, déployer de nouvelles versions et les publier pour qu’elles soient disponibles en privé ou en public.

## Gestion d’une extension  {#manage-extension}

Une fois que vous avez préparé votre package d’extension localement, utilisez **[!UICONTROL Extension Management]** dans l’interface utilisateur de collecte de données pour le charger, valider le package et publier les versions via **Développement**, **Privé** et **Public** disponibilité. Vous pouvez ensuite installer l’extension sur une propriété et l’utiliser à des fins de test.

### Chargement d’une extension {#upload-extension}

Pour charger une extension, accédez à l’interface utilisateur de la collecte de données et sélectionnez **[!UICONTROL Extension Management]** dans le volet de navigation de gauche. À partir de là, sélectionnez l’onglet **[!UICONTROL Owned]** . Cet onglet affiche toutes les extensions dont vous ou votre organisation êtes propriétaire. Ils sont séparés par plateforme et vous pouvez voir les extensions dont vous disposez sur chaque plateforme (Web, Mobile et Edge) à l’aide de la liste déroulante. Sélectionnez **[!UICONTROL Upload New Extension]**.

![L’onglet Owned présentant une liste d’extensions partagées avec cette organisation, en mettant en surbrillance la liste déroulante et en chargeant une nouvelle extension.](../images/shared-extensions/upload-extension.png)

Sur la page **Télécharger une nouvelle extension**, sélectionnez **[!UICONTROL Select Extension Folder]**, accédez au dossier contenant votre extension, sélectionnez le dossier, puis sélectionnez **[!UICONTROL Upload]**.

![Extension sélectionnée dans le dossier local.](../images/shared-extensions/selected-extension.png)

Confirmez le nombre de fichiers qui seront chargés en sélectionnant **[!UICONTROL Upload]**.

Le nombre de fichiers qui seront chargés s’affiche, y compris le nom de l’extension et la version. Vous avez la possibilité d’effectuer une **[!UICONTROL Dry Run]** qui téléchargera un fichier zip sur votre ordinateur local à des fins d’inspection. Sélectionnez **[!UICONTROL Validate & Upload]**.

![Chargez une nouvelle page de package d’extension indiquant le nombre de fichiers à charger, en mettant en surbrillance Valider et Charger.](../images/shared-extensions/validate-upload.png)

La confirmation que votre extension a bien été chargée et traitée s’affiche avec votre **ID de package d’extension**. Sélectionnez **[!UICONTROL Close]** pour revenir à l’onglet **[!UICONTROL Owned]** où votre extension est affichée.

![Confirmation de l’extension chargée mettant en surbrillance l’ID de package et Fermer.](../images/shared-extensions/confirmation-upload.png)

Vous revenez alors à l’onglet [!UICONTROL Owned] dans lequel votre extension mise à jour s’affiche.

>[!IMPORTANT]
>
>Les extensions sont chargées dans la disponibilité **Développement**. Les extensions disponibles dans **Développement** ne peuvent pas être partagées tant qu’elles ne sont pas disponibles dans **Privé**.

### Publication d’une extension {#release-extension}

Pour publier l’extension afin qu’elle soit disponible en privé, sélectionnez votre extension pour afficher le panneau d’informations à droite. Vous trouverez ici les détails suivants de l’extension :

* **Version** - Affiche la dernière version et l’état dans lequel elle se trouve actuellement. Vous pouvez utiliser le menu déroulant pour afficher l’historique des versions de l’extension.
* **Actions** - Permet de **[!UICONTROL Upload New Version]** l’extension et l’**[!UICONTROL Release To Private]**.
* **ID du package d’extension** - Affiché en bas. Cela varie en fonction de la version sélectionnée.

![Panneau Détails du package mettant en surbrillance la version, les actions et l’ID de package](../images/shared-extensions/package-details.png)

Sélectionnez **[!UICONTROL Release To Private]**, puis sélectionnez à nouveau **[!UICONTROL Release To Private]** pour confirmer la publication.

Une confirmation est reçue une fois que l’extension a été publiée avec succès en disponibilité **privée**. La disponibilité mise à jour s’affiche dans le panneau de droite.

![Panneau de détails du package mettant en évidence la version et la disponibilité privée](../images/shared-extensions/package-details-availability.png)

>[!NOTE]
>
>Une fois que l’extension a été publiée sur **Privé**, elle peut être partagée avec d’autres organisations.

Pour rendre l’extension disponible pour le **public**, sélectionnez **[!UICONTROL Request Public Release]** dans le panneau de droite.

L’écran **[!UICONTROL Release Extension Package]** fournit les détails qui seront requis sur le formulaire de demande, avec une option pour copier les détails. Sélectionnez **[!UICONTROL Go To Request Form]**.

![Page du package d’extension de version mettant en surbrillance les informations requises pour remplir le formulaire.](../images/shared-extensions/public-request-form.png)

Un nouvel onglet du navigateur s’ouvre, contenant le formulaire de demande. Copiez et collez les informations de l’écran **[!UICONTROL Release Extension Package]** dans les champs appropriés. Envoyez le formulaire rempli pour révision. Vous serez averti dès que l’extension aura été rendue publique.

## Partager des packages d’extension avec d’autres organisations {#share-extension}

>[!NOTE]
>
>Les packages d’extension doivent avoir une version privée ou publique pour être partagés via [!UICONTROL Usage Authorizations]. Les versions marquées comme Disponibilité pour le développement ne sont pas éligibles au partage et n’apparaîtront pas dans la liste déroulante d’autorisation. Cela s’applique même si une version antérieure (par exemple, 1.0.0) a déjà été partagée. Les versions plus récentes (par exemple, 1.0.1) doivent être rendues au moins privées avant de pouvoir être autorisées ou installées par les organisations destinataires.
>
>Toutes les instructions concernant le partage de packages d’extension privés s’appliquent également si vous choisissez par la suite de rendre ces packages publics. Les mêmes considérations concernant la visibilité, le contrôle de version, la sécurité, la compatibilité, la prise en charge et la documentation restent pertinentes, quel que soit le statut de disponibilité du package.

**[!UICONTROL Usage Authorizations]** est une fonctionnalité puissante que vous pouvez utiliser pour partager en toute sécurité des packages d’extension privés avec des partenaires de confiance sans les rendre publics dans le catalogue d’extensions. Utilisez cette fonctionnalité pour créer un pont sécurisé entre les organisations, ce qui vous permet d’exploiter le code d’extension personnalisé des unes et des autres tout en préservant la confidentialité et le contrôle sur vos solutions propriétaires.

Les entreprises développent souvent des extensions spécialisées adaptées à leurs besoins professionnels uniques. Ces extensions peuvent contenir une logique propriétaire, des intégrations personnalisées ou des configurations sensibles qui ne doivent pas être rendues publiques. Les autorisations d’utilisation résolvent ce défi en activant :

* **Partage sélectif** : partagez des extensions privées uniquement avec des organisations partenaires de confiance.
* **Confidentialité préservée** : évitez que le code d’extension sensible ne figure dans le catalogue public.
* **Développement collaboratif** : permettez à des partenaires de confiance de bénéficier de vos solutions personnalisées.
* **Accès contrôlé** : conservez un contrôle total sur les personnes qui peuvent accéder à vos extensions privées et les utiliser.

Le processus de partage implique deux participants clés :

1. **Organisation de partage** : l’organisation qui détient et partage le package d’extension privé
2. **Organisation d’accueil** : organisation approuvée qui accède à l’extension partagée

Lorsqu’une version privée est partagée, l’organisation destinataire a accès à cette version spécifique, ce qui crée une connexion directe entre les deux organisations. Si une version plus récente est rendue privée par la suite, elle sera également disponible pour l’organisation destinataire sans nécessiter d’étapes supplémentaires de sa part.

### Créer une autorisation d’utilisation de package d’extension {#package-usage-authorization}

Pour partager une extension, accédez à l’interface utilisateur de la collecte de données et sélectionnez **[!UICONTROL Extension Management]** dans le volet de navigation de gauche. À partir de là, sélectionnez l’onglet **[!UICONTROL Usage Authorizations]** .

Vous voyez ici une liste des autorisations partagées existantes organisées en deux catégories :

* **Partagé avec cette organisation** : extensions que d’autres organisations ont partagées avec vous.
* **Partagé avec d’autres organisations** : extensions que vous avez partagées avec d’autres organisations.

Sélectionnez **[!UICONTROL Add Authorization]**.

![Onglet [!UICONTROL Usage Authorizations] présentant une liste des extensions partagées avec cette organisation, en surbrillance [!UICONTROL Add Authorization]](../images/shared-extensions/add-authorization.png)

>[!IMPORTANT]
>
>Vous devez obtenir le de l&#39;organisation cible **`Organization ID`** le propriétaire de l&#39;organisation. Les organisations ne peuvent pas être recherchées par nom.

Sélectionnez la **[!UICONTROL Platform]** pour laquelle vous souhaitez autoriser une extension dans la liste déroulante. Vous pouvez partager des extensions **[!UICONTROL Web]**, **[!UICONTROL Mobile]** et **[!UICONTROL Edge]**.

Sélectionnez ensuite le **[!UICONTROL Extension]** que vous souhaitez partager parmi les extensions disponibles dans la liste déroulante. La liste affiche les extensions détenues par votre organisation ainsi que leur statut de disponibilité. Les extensions dont la dernière version est en cours de disponibilité **Développement** n’apparaîtront pas dans cette liste.

Saisissez ensuite l&#39;ID de l&#39;organisation de réception, puis sélectionnez **[!UICONTROL Save]**.

![Page [!UICONTROL Create extension package usage authorization] présentant l’extension sélectionnée et l’ID d’organisation Adobe saisi, en surbrillance [!UICONTROL Save]](../images/shared-extensions/save-authorization.png)

Vous revenez alors à l’onglet [!UICONTROL Usage Authorizations] où l’extension s’affiche dans votre liste **[!UICONTROL Shared with other orgs]**. Le statut indique **En attente d&#39;approbation** jusqu&#39;à ce que l&#39;organisation réceptrice approuve l&#39;autorisation, auquel cas elle est mise à jour sur **Approuvée**.

![Onglet [!UICONTROL Usage Authorizations] affichant une liste des extensions partagées avec d’autres organisations, en mettant en surbrillance la nouvelle autorisation](../images/shared-extensions/new-authorization.png)

>[!TIP]
>
>Vous pouvez également partager des extensions directement à partir du **[!UICONTROL Extension Catalog]** en sélectionnant le menu (⋯) sur la carte d’extension, puis en sélectionnant l’option de partage dans le menu.

Lorsqu’une autorisation est active, l’extension partagée affiche un badge ***Partage*** dans le catalogue indiquant qu’elle est partagée avec d’autres organisations.

![Onglet [!UICONTROL Catalog] affichant l’extension partagée avec le badge](../images/shared-extensions/sharing-badge.png)

### Autoriser et gérer les extensions partagées {#manage-shared-extension}

>[!NOTE]
>
>En tant qu’organisation de réception, vous pouvez uniquement approuver ou rejeter les extensions partagées. Vous ne pouvez pas gérer ni modifier les détails d’autorisation, car ils sont contrôlés par l’organisation de partage.

Pour autoriser une extension partagée pour votre organisation, accédez à l’interface utilisateur de collecte de données et sélectionnez **[!UICONTROL Extension Management]** dans le volet de navigation de gauche, puis sélectionnez l’onglet **[!UICONTROL Usage Authorizations]** .

La section **répertorie les extensions partagées, y compris celles** en attente d’approbation **[!UICONTROL Shared with this org]**. Sélectionnez l’extension à approuver, puis sélectionnez **[!UICONTROL Approve]**.

![Onglet [!UICONTROL Usage Authorizations] affichant une liste des extensions partagées avec cette organisation avec l’extension en attente d’approbation sélectionnée, en mettant [!UICONTROL Approve]](../images/shared-extensions/approve-authorization.png) surbrillance

>[!NOTE]
>
>Vous pouvez également rejeter une demande dans l’onglet **[!UICONTROL Usage Authorizations]** si l’extension partagée n’est plus nécessaire pour votre organisation.

Sélectionnez **[!UICONTROL OK]** dans la boîte de dialogue **[!UICONTROL Authorization Usages]**.

![Boîte de dialogue [!UICONTROL Authorization Usages], mise en surbrillance [!UICONTROL OK]](../images/shared-extensions/confirmation.png)

Vous revenez alors à l’onglet [!UICONTROL Usage Authorizations] dans lequel vous pouvez voir que l’extension affiche désormais un statut **Approuvé**.

![Onglet [!UICONTROL Usage Authorizations] affichant une liste des extensions partagées avec cette organisation, en mettant en surbrillance l’extension avec le statut Approuvé](../images/shared-extensions/approved-authorization.png)

Une fois l’autorisation approuvée, l’extension est disponible dans votre catalogue et peut être installée et utilisée comme toute autre extension. L’extension partagée affiche un badge ***Réception*** indiquant qu’il s’agit d’une extension partagée avec vous par une autre organisation.

![Onglet [!UICONTROL Catalog] affichant l’extension partagée avec le badge « Réception »](../images/shared-extensions/receiving-badge.png)

### Révoquer les autorisations {#revoke-authorization}

En tant qu’organisation propriétaire, vous pouvez supprimer une autorisation à tout moment, quel que soit son statut actuel (En attente d’approbation, Refusée ou Approuvée).

**Si votre extension n’a jamais été rendue publique :**

* Toute version privée déjà installée par l’organisation de réception apparaîtra toujours dans la liste des extensions installées.
* Si l’organisation réceptrice n’a jamais installé votre extension, elle n’apparaîtra plus nulle part dans son interface.

**Si votre extension a été rendue publique :**

* Toute version privée installée par l’organisation de réception reste visible dans la liste des extensions installées.
* S’il n’a jamais installé votre version privée, il verra toujours la dernière version publique dans son catalogue et pourra l’installer.
* Il peut également rétrograder de votre version privée vers la dernière version publique disponible, si vous le souhaitez.

Lorsque vous révoquez une autorisation, l’organisation destinataire conserve certains droits pour protéger ses implémentations existantes :

* **Utilisation continue** : l’organisation destinataire peut continuer à utiliser toute version privée qu’elle a déjà installée, même après avoir révoqué l’accès.
* **Protection de build** : si l’organisation réceptrice a installé votre version privée v1.0.0 et que vous publiez ultérieurement une version privée v1.0.1, elle ne verra pas la version la plus récente, mais peut continuer à créer avec v1.0.0 sans interruption.
* **Mises à niveau futures** : si vous rendez par la suite votre extension publique (par exemple en publiant la version 2.0.0), l’organisation destinataire peut effectuer directement la mise à niveau de sa version 1.0.0 privée vers la nouvelle version 2.0.0 publique.

>[!IMPORTANT]
>
>La révocation de l’autorisation n’interrompt pas les versions ou implémentations existantes. Les organisations d’accueil conservent l’accès à toutes les versions privées qu’elles ont déjà installées pour assurer la continuité de l’activité.

## Étapes suivantes {#next-steps}

Ce document vous a montré comment utiliser la fonctionnalité d’extension partagée dans Experience Platform. Pour plus d’informations sur le développement d’extensions, consultez le [guide d’utilisation du développement d’extensions](./getting-started.md).

Pour une présentation générale du développement des extensions dans Experience Platform, reportez-vous à la [documentation de présentation](./overview.md).
