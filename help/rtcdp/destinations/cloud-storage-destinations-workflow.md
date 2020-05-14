---
title: Processus des destinations de stockage dans le cloud
seo-title: Processus des destinations de stockage dans le cloud
description: Instructions pour se connecter aux emplacements de stockage dans le cloud
seo-description: Instructions pour se connecter aux emplacements de stockage dans le cloud
translation-type: tm+mt
source-git-commit: 37c51435ce8330dbd61857bda408df03ff21a491
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 67%

---


# Processus de création de destinations de stockage dans le cloud

## Présentation

Cette page explique comment se connecter aux emplacements de stockage dans le cloud dans la plateforme des données clients en temps réel d’Adobe.

1. Dans **[!UICONTROL Connexions > Destinations]**, sélectionnez votre destination préférée de stockage dans le cloud, puis **[!UICONTROL Connecter la destination]**.

   ![Connexion à la destination de stockage dans le cloud](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. À l’étape **[!UICONTROL Authentification]**, si vous avez auparavant configuré une connexion à votre destination de stockage dans le cloud, sélectionnez **[!UICONTROL Compte existant]**, puis la connexion existante. Vous pouvez également sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion à votre destination de stockage dans le cloud. Renseignez les informations d’identification d’authentification de votre compte et sélectionnez **[!UICONTROL Se connecter à la destination]**. <br> Voir destination [Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md) , destination [Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) , destination [Azure Événement Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md) et destination [SFTP pour en savoir plus sur les informations d’identification entrées à l’étape Authentication.](/help/rtcdp/destinations/sftp-destination.md)****

   >[!NOTE]
   >
   >La plateforme des données clients en temps réel d’Adobe prend en charge la validation des informations d’identification dans le processus d’authentification et affiche un message d’erreur si vous saisissez des informations d’identification incorrectes pour votre emplacement de stockage dans le cloud. Ainsi, vous n’effectuez pas le processus avec des informations d’identification incorrectes.

   ![Connexion à la destination de stockage dans le cloud - étape d’authentification](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. À l’étape **[!UICONTROL Configuration]** , saisissez un **[!UICONTROL Nom]** et une **[!UICONTROL Description]** pour votre flux d’activations. <br>
Pour les destinations Amazon S3, insérez le nom **[!UICONTROL du]** compartiment et le chemin **[!UICONTROL du]** dossier dans la destination de l’enregistrement cloud où les fichiers seront distribués. Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

   ![Connexion à l’enregistrement cloud Amazon S3 - étape d’authentification](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

   Pour les destinations SFTP, insérez le chemin **[!UICONTROL du]** dossier dans lequel les fichiers seront distribués.

   ![Connexion à la destination de l’enregistrement cloud SFTP - étape d’authentification](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

4. Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement. Sélectionnez **[!UICONTROL Suivant]** pour poursuivre le processus et choisir les segments à activer. In either case, see the next section, [Activate segments](#activate-segments), for the rest of the workflow to export data.

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](/help/rtcdp/destinations/activate-destinations.md).