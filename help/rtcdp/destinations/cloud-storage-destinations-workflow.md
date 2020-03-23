---
title: 'Flux de production de destinations de  Cloud '
seo-title: 'Flux de production de destinations de  Cloud '
description: 'Instructions de connexion à votre cloud  emplacements '
seo-description: 'Instructions de connexion à votre cloud  emplacements '
translation-type: tm+mt
source-git-commit: 9221c11a30bda3a155d73afec16be55ef8f5d133

---


# Processus de création de cloud  de  destinations de

## Présentation

Cette page explique comment vous pouvez vous connecter au cloud  aux emplacements  des dans la plateforme de données clientes Adobe en temps réel.

1. Dans **[!UICONTROL Connexions > Destinations]**, sélectionnez votre cloud préféré  destination , puis sélectionnez **[!UICONTROL Connexion destination]**.

   ![Connexion au cloud  destination  du](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. À l’étape **Authentification** , si vous aviez précédemment configuré une connexion à votre cloud  destination , sélectionnez Compte **** existant et sélectionnez votre connexion existante. Vous pouvez également sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion à votre cloud  destination . Renseignez les informations d’identification d’authentification de votre compte et sélectionnez **[!UICONTROL Se connecter à la destination]**.

   >[!NOTE]
   >
   >Le CDP Adobe en temps réel prend en charge la validation des informations d’identification dans le processus d’authentification et affiche un message d’erreur si vous saisissez des informations d’identification incorrectes dans votre cloud  l’emplacement  du. Vous êtes ainsi assuré de ne pas terminer le processus avec des informations d’identification incorrectes.

   ![Connexion au cloud  destination  du - étape d’authentification](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Dans l’étape **[!UICONTROL Configuration]** , saisissez un **[!UICONTROL Nom]** et une **[!UICONTROL Description]** pour votre flux de  de .
   1. Pour les destinations Amazon S3, insérez le nom **[!UICONTROL du]** compartiment et le chemin **[!UICONTROL du]** dossier dans votre cloud  destination  où les fichiers seront distribués. Sélectionnez **[!UICONTROL Créer une destination]** après avoir rempli les champs ci-dessus.
   2. Pour les destinations SFTP, insérez le chemin d’accès au **[!UICONTROL dossier.]**
   ![Connexion au cloud  destination  du - étape d’authentification](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

4. Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement ou sélectionner **[!UICONTROL Suivant]** pour poursuivre le flux de travaux et sélectionner les segments à activer. Dans les deux cas, reportez-vous à la section suivante, [Activation des segments](#activate-segments), pour que le reste du flux de travail exporte les données.

## Activer les segments {#activate-segments}

Voir [Activation de  et de segments vers une destination](/help/rtcdp/destinations/activate-destinations.md) pour plus d’informations sur le  de flux de travail  du de segments.