---
title: Flux de travaux Destinations de réseaux sociaux
seo-title: Flux de travaux Destinations de réseaux sociaux
description: Instructions de connexion à vos comptes publicitaires de réseaux sociaux
seo-description: Instructions de connexion à vos comptes publicitaires de réseaux sociaux
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (Bêta) Processus d’authentification des destinations réseau social {#social-network-destinations-workflow}


>[!IMPORTANT]
>
>Le processus de création de destinations de réseau social dans le CDP en temps réel d’Adobe est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et la fonctionnalité peuvent changer.

## Processus de création de cloud  de  destinations de

Ce didacticiel utilise Facebook comme exemple, mais le flux de travail dans la plateforme de données clientes en temps réel d’Adobe sera le même pour toutes les destinations de réseaux sociaux, une fois le produit ajouté.

1. Dans **[!UICONTROL Connections > Destinations]**, faites défiler l’écran jusqu’au **[!UICONTROL Social]** . Sélectionnez la destination de votre réseau social préféré, puis sélectionnez **[!UICONTROL Connect destination]**.

   ![Connexion à la destination du réseau social](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. À l’étape **Authentification** , si vous aviez précédemment configuré une connexion à la destination de votre réseau social, sélectionnez **[!UICONTROL Existing Account]** et sélectionnez votre connexion existante. Vous pouvez également choisir **[!UICONTROL New Account]** de configurer une nouvelle connexion à la destination de votre réseau social. Sélectionnez **[!UICONTROL Connect to destination]** cette option pour vous amener à la destination sélectionnée du réseau social afin de vous connecter et de connecter Adobe Experience Cloud à votre compte de publicité sur le réseau social.

   >[!NOTE]
   >
   >Le CDP Adobe en temps réel prend en charge la validation des informations d’identification dans le processus d’authentification et affiche un message d’erreur si vous saisissez des informations d’identification incorrectes dans l’ID de compte de réseau social. Vous êtes ainsi assuré de ne pas terminer le processus avec des informations d’identification incorrectes.

   ![Connexion à la destination du réseau social - étape d’authentification](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Une fois vos informations d’identification confirmées et la connexion d’Adobe Experience Cloud à votre réseau social établie, vous pouvez choisir **[!UICONTROL Next]** de passer à l’ **[!UICONTROL Setup]** étape.

   ![Informations confirmées](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. Dans l’ **[!UICONTROL Setup]** étape, saisissez un **[!UICONTROL Name]** et un **[!UICONTROL Description]** pour votre flux de  de  et renseignez le **[!UICONTROL Account ID]** compte publicitaire de votre réseau social. Sélectionnez **[!UICONTROL Create Destination]** une fois que vous avez rempli les champs ci-dessus.

   >[!IMPORTANT]
   >
   >Destinations Facebook. **[!UICONTROL Account ID]** correspond à votre ID de compte publicitaire Facebook. Vous trouverez cet identifiant dans le Gestionnaire de publicités Facebook. Préfixez l’ID par `act_` comme illustré ci-dessous :

   ![Connexion à la destination du réseau social - étape de configuration](/help/rtcdp/destinations/assets/social-network-step.png)

5. Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Save & Exit]** si vous souhaitez activer les segments ultérieurement ou **[!UICONTROL Next]** pour continuer le flux de travail et sélectionner les segments à activer. Dans les deux cas, reportez-vous à la section suivante, [Activation des segments sur les réseaux](#activate-segments)sociaux, pour le reste du flux de travail.

## Activation de segments sur les réseaux sociaux {#activate-segments}

For instructions on how to activate segments to social networks, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).