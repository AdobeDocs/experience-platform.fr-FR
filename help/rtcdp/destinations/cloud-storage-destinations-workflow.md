---
title: 'Flux de production de destinations de  Cloud '
seo-title: 'Flux de production de destinations de  Cloud '
description: 'Instructions de connexion à votre cloud  emplacements '
seo-description: 'Instructions de connexion à votre cloud  emplacements '
translation-type: tm+mt
source-git-commit: 60b10aa823af55d6f38651308dc93eeb57a7fee6

---


# Processus de création de cloud  de  destinations de

## Présentation

Cette page explique comment vous pouvez vous connecter au cloud  aux emplacements  des dans la plateforme de données clientes Adobe en temps réel.

1. Dans **[!UICONTROL Connections > Destinations]**, sélectionnez votre cloud préféré   destination du, puis sélectionnez **[!UICONTROL Connect destination]**.

   ![Connexion au cloud  destination  du](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

1. À l’étape **Authentification** , si vous aviez précédemment configuré une connexion à votre cloud  destination , sélectionnez **[!UICONTROL Existing Account]** et sélectionnez votre connexion existante. Vous pouvez également choisir **[!UICONTROL New Account]** de configurer une nouvelle connexion à votre cloud  destination . Renseignez les informations d’identification d’authentification de votre compte et sélectionnez **[!UICONTROL Connect to destination]**. Voir destination [](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 et destination [](/help/rtcdp/destinations/sftp-destination.md) SFTP pour plus d’informations sur la saisie des informations d’identification à l’étape **Authentification** .

   >[!NOTE]
   >
   >Le CDP Adobe en temps réel prend en charge la validation des informations d’identification dans le processus d’authentification et affiche un message d’erreur si vous saisissez des informations d’identification incorrectes dans votre cloud  l’emplacement  du. Vous êtes ainsi assuré de ne pas terminer le processus avec des informations d’identification incorrectes.

   ![Connexion au cloud  destination  du - étape d’authentification](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

1. Dans l’ **[!UICONTROL Setup]** étape, entrez un **[!UICONTROL Name]** et un **[!UICONTROL Description]** pour votre flux  de . <br>
Pour les destinations Amazon S3, insérez le **[!UICONTROL Bucket name]** et le **[!UICONTROL Folder path]** dans votre cloud  destination  où les fichiers seront distribués. Sélectionnez **[!UICONTROL Create Destination]** une fois que vous avez rempli les champs ci-dessus.

   ![Connexion au cloud Amazon S3  destination  - étape d’authentification](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

   Pour les destinations SFTP, insérez l’ **[!UICONTROL Folder path]** emplacement de remise des fichiers.

   ![Connexion au cloud SFTP  destination  du - étape d’authentification](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

1. Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Save & Exit]** si vous souhaitez activer les segments ultérieurement ou **[!UICONTROL Next]** pour continuer le flux de travail et sélectionner les segments à activer. Dans les deux cas, reportez-vous à la section suivante, [Activation des segments](#activate-segments), pour que le reste du flux de travail exporte les données.

## Activer les segments {#activate-segments}

Voir [Activation de  et de segments vers une destination](/help/rtcdp/destinations/activate-destinations.md) pour plus d’informations sur le  de flux de travail  du de segments.