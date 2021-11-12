---
keywords: Experience Platform;accueil;rubriques les plus consultées;Marketo Engage;marketing à engager;marketing
solution: Experience Platform
title: Authentification de votre connecteur source Marketo
topic-legacy: overview
description: Ce document fournit des informations sur la génération de vos informations d’authentification Marketo.
exl-id: 594dc8b6-cd6e-49ec-9084-b88b1fe8167a
source-git-commit: 21617c6ec364fc05d7b8b6d00daa68608d1ed318
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Authentifiez votre [!DNL Marketo Engage] connecteur source

Avant de pouvoir créer un [!DNL Marketo Engage] (ci-après dénommés &quot;[!DNL Marketo]&quot;) du connecteur source, vous devez d’abord configurer un service personnalisé par le biais de la fonction [!DNL Marketo] , ainsi que de récupérer les valeurs de votre ID Munchkin, de votre ID client et de votre secret client.

La documentation ci-dessous décrit les étapes à suivre pour acquérir des informations d’authentification afin de créer une [!DNL Marketo] connecteur source.

## Configuration d’un nouveau rôle

La première étape de l’acquisition de vos informations d’identification d’authentification consiste à configurer un nouveau rôle au moyen de la fonction [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) .

Connectez-vous à [!DNL Marketo] et sélectionnez **[!DNL Admin]** dans la barre de navigation supérieure.

![Administration d’un nouveau rôle](../images/marketo/home.png)

Le *[!DNL Users & Role]s* contient des informations sur les utilisateurs, les rôles et les historiques de connexion. Pour créer un rôle, sélectionnez **[!DNL Roles]** dans l’en-tête supérieur, puis sélectionnez **[!DNL New Role]**.

![new-role](../images/marketo/new-role.png)

La boîte de dialogue **[!DNL Create New Role]** sʼaffiche. Attribuez un nom et une description, puis sélectionnez les autorisations que vous souhaitez accorder pour ce rôle. Les autorisations sont limitées à des espaces de travail spécifiques et les utilisateurs ne peuvent effectuer que des actions dans les espaces de travail dans lesquels ils disposent d’autorisations.

Une fois que vous avez sélectionné les autorisations à octroyer, sélectionnez **[!DNL Create]**.

![create-new-role](../images/marketo/create-new-role.png)

Vous pouvez gérer les autorisations restreintes sur l’API lors de la création de rôles avec [!DNL Marketo]. Au lieu de sélectionner &quot;API d’accès&quot;, vous pouvez fournir un rôle avec le niveau d’accès minimal en sélectionnant les autorisations suivantes :

* [!DNL Read-Only Activity]
* [!DNL Read-Only Assets]
* [!DNL Read-Only Campaign]
* [!DNL Read-Only Company]
* [!DNL Read-Only Custom Object]
* [!DNL Read-Only Custom Object Type]
* [!DNL Read-Only Named Account]
* [!DNL Read-Only Named Account List]
* [!DNL Read-Only Opportunity]
* [!DNL Read-Only Person]
* [!DNL Read-Only Sales Person]

## Configuration d’un nouvel utilisateur

Tout comme les rôles, vous pouvez configurer un nouvel utilisateur à partir de la fonction **[!DNL Users & Roles]** page. Le **[!DNL Users]** fournit une liste des utilisateurs principaux actuellement configurés dans Marketo. Sélectionner **[!DNL Invite New User]** pour configurer un nouvel utilisateur.

![invite-nouveau-utilisateur](../images/marketo/invite-new-user.png)

Un menu contextuel s’affiche. Indiquez les informations appropriées pour votre email, votre prénom, votre nom et votre raison. Au cours de cette étape, vous pouvez également définir une date d’expiration pour l’accès au nouveau compte utilisateur que vous invitez. Lorsque vous avez terminé, sélectionnez **[!DNL Next]**.

>[!IMPORTANT]
>
>Lors de la configuration d’un nouvel utilisateur, vous devez affecter l’accès à un utilisateur qui est dédié exclusivement au service personnalisé que vous créez.

![user-info](../images/marketo/new-user-info.png)

Sélectionnez les champs appropriés dans le **[!DNL Permissions]** puis sélectionnez l’étape **[!DNL API Only]** pour fournir un rôle API au nouvel utilisateur. Sélectionner **[!DNL Next]** pour continuer.

![autorisations](../images/marketo/permissions.png)

Pour terminer le processus, sélectionnez **[!DNL Send]**.

![message](../images/marketo/message.png)

## Configuration d’un service personnalisé

Une fois que vous avez établi un nouvel utilisateur, vous pouvez configurer un service personnalisé pour récupérer vos nouvelles informations d’identification. Dans la page d’administration, sélectionnez **[!DNL LaunchPoint]**.

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

Le **[!DNL Installed services]** contient une liste de services existants. pour créer un service personnalisé, sélectionnez **[!DNL New]** puis sélectionnez **[!DNL New Service]**.

![new-service](../images/marketo/new-service.png)

Fournissez un nom d’affichage descriptif à votre nouveau service, puis sélectionnez **[!DNL Custom]** de la **[!DNL Service]** menu déroulant. Fournissez une description appropriée, puis sélectionnez l’utilisateur que vous souhaitez configurer dans le **[!DNL API Only User]** menu déroulant. Une fois que vous avez renseigné les détails nécessaires, sélectionnez **[!DNL Create]** pour créer votre service personnalisé.

![create](../images/marketo/create.png)

## Obtention de l’ID client et du secret client

Une fois un nouveau service personnalisé créé, vous pouvez désormais récupérer les valeurs de votre ID client et de votre secret client. Dans la **[!DNL Installed Services]** , recherchez le service personnalisé auquel vous souhaitez accéder, puis sélectionnez **[!DNL View Details]**.

![view-details](../images/marketo/view-details.png)

Une boîte de dialogue s’affiche, contenant votre ID client et votre secret client.

![informations](../images/marketo/credentials.png)

## Obtention de votre Munchkin ID

La dernière étape que vous devez effectuer pour authentifier votre [!DNL Marketo] Le connecteur source doit récupérer votre Munchkin ID. Dans la page d’administration, sélectionnez **[!DNL Munchkin]** sous le **[!DNL Integration]** du panneau.

![admin-munchkin](../images/marketo/admin-munchkin.png)

Le *[!DNL Munchkin]* s’affiche, avec votre Munchkin ID unique répertorié en haut du panneau.

![munchkin-Id](../images/marketo/munchkin-id.png)

Combiné avec votre ID client et votre secret client, vous pouvez utiliser votre ID Munchkin pour configurer un nouveau compte et [créer [!DNL Marketo] connexion source](../../../tutorials/ui/create/adobe-applications/marketo.md) sur Experience Platform.
