---
title: Processus des destinations de stockage dans le cloud
seo-title: Processus des destinations de stockage dans le cloud
description: Instructions pour se connecter aux emplacements de stockage dans le cloud
seo-description: Instructions pour se connecter aux emplacements de stockage dans le cloud
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 68%

---


# Workdlow de création de destinations de stockage dans le cloud

## Présentation

Cette page explique comment se connecter aux emplacements de stockage dans le cloud dans la plateforme des données clients en temps réel d’Adobe.

1. Dans **[!UICONTROL Connexions > Destinations]**, sélectionnez votre destination préférée de stockage dans le cloud, puis **[!UICONTROL Connecter la destination]**.

   ![Connexion à la destination de stockage dans le cloud](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. À l’étape **[!UICONTROL Authentification]**, si vous avez auparavant configuré une connexion à votre destination de stockage dans le cloud, sélectionnez **[!UICONTROL Compte existant]**, puis la connexion existante. Vous pouvez également sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion à votre destination de stockage dans le cloud. Renseignez les informations d’authentification de votre compte et sélectionnez **[!UICONTROL Se connecter à la destination]**. <br> Voir destination, [destination,](/help/rtcdp/destinations/amazon-s3-destination.md) destination et destination [!DNL Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) SFTP [!DNL Azure Event Hubs](/help/rtcdp/destinations/azure-event-hubs-destination.md) Amazon S3 [pour en savoir plus sur les informations d’identification saisies à l’étape](/help/rtcdp/destinations/sftp-destination.md) **Authentification.**

   >[!NOTE]
   >
   >La plateforme des données clients en temps réel d’Adobe prend en charge la validation des informations d’identification dans le processus d’authentification et affiche un message d’erreur si vous saisissez des informations d’identification incorrectes pour votre emplacement de stockage dans le cloud. Ainsi, vous n’effectuez pas le workflow avec des informations d’identification incorrectes.

   ![Connexion à la destination de stockage dans le cloud - étape d’authentification](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. À l’étape **[!UICONTROL Configuration]**, saisissez un **[!UICONTROL Nom]** et une **[!UICONTROL Description]** pour votre flux d’activation. <br>
Cette étape vous permet également de sélectionner tout cas **[!UICONTROL d’utilisation]** marketing à appliquer à cette destination. Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d’informations sur les cas d’utilisation marketing, voir la page Gouvernance des [données dans le CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) en temps réel. Pour plus d’informations sur les cas d’utilisation marketing définis par l’Adobe, voir la présentation [des stratégies d’utilisation des](/help/data-governance/policies/overview.md#core-actions)données. <br>
Pour les destinations Amazon S3, insérez le **[!UICONTROL Nom du compartiment]** et le **[!UICONTROL Chemin du dossier]** dans votre destination de stockage dans le cloud où les fichiers seront distribués. Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

   ![Connexion à la destination de stockage dans le cloud Amazon S3 : étape d’authentification](/help/rtcdp/destinations/assets/amazon-s3-setup-step.png)

   Pour les destinations SFTP, indiquez le **[!UICONTROL chemin du dossier]** dans lequel les fichiers seront distribués. Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

   ![Connexion à la destination de stockage dans le cloud SFTP : étape d’authentification](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

   Pour [!DNL Amazon Kinesis] les destinations, indiquez le nom de votre flux de données existant dans votre [!DNL Amazon Kinesis] compte. Adobe Le CDP en temps réel exportera les données dans ce flux. Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

   ![Connexion à la destination de l&#39;enregistrement cloud Kinesis - étape d&#39;authentification](/help/rtcdp/destinations/assets/kinesis-destinations-setup-step.png)

   Pour [!DNL Azure Event Hubs] les destinations, indiquez le nom de votre flux de données existant dans votre [!DNL Amazon Kinesis] compte. Adobe Le CDP en temps réel exportera les données dans ce flux. Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

   ![Connexion à la destination de l&#39;enregistrement cloud Kinesis - étape d&#39;authentification](/help/rtcdp/destinations/assets/eventhubs-destinations-setup-step.png)

4. Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement. Sélectionnez **[!UICONTROL Suivant]** pour poursuivre le workflow et choisir les segments à activer. Dans les deux cas, consultez la section suivante, [Activation des segments](#activate-segments), pour le reste du processus d’exportation des données.

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](/help/rtcdp/destinations/activate-destinations.md).