---
title: Flux de travaux Destinations des réseaux sociaux
seo-title: Flux de travaux Destinations des réseaux sociaux
description: Instructions de connexion à vos comptes publicitaires de réseaux sociaux
seo-description: Instructions de connexion à vos comptes publicitaires de réseaux sociaux
translation-type: tm+mt
source-git-commit: ab53e2efffed536e8028beabd64aee843d1eeee8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 13%

---


# Processus d’authentification des destinations réseau social {#social-network-destinations-workflow}

## Processus de création de destinations de réseau social

Ce didacticiel utilise Facebook comme exemple, mais le flux de travail dans la plate-forme de données clientes en temps réel d’Adobe sera le même pour toutes les destinations de réseau social, une fois le produit ajouté.

1. Dans **[!UICONTROL Destinations > Catalogue]**, faites défiler l’écran jusqu’à la catégorie **[!UICONTROL Social]** . Sélectionnez la destination de réseau social que vous préférez, puis sélectionnez **[!UICONTROL Connecter la destination]**.

   ![Se connecter à la destination du réseau social](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. In the **Authentication** step, if you had previously set up a connection to your social network destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to your social network destination. Sélectionnez **[!UICONTROL Se connecter à la destination]** et vous conduira à la destination de réseau social sélectionnée pour vous connecter et connecter Adobe Experience Cloud à votre compte publicitaire de réseau social.

   >[!NOTE]
   >
   >Le CDP Adobe en temps réel prend en charge la validation des informations d’identification dans le processus d’authentification et affiche un message d’erreur si vous saisissez des informations d’identification incorrectes dans l’ID de compte de réseau social. Ainsi, vous n’effectuez pas le processus avec des informations d’identification incorrectes.

   ![Connexion à la destination du réseau social - étape d’authentification](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Une fois vos informations d’identification confirmées et qu’Adobe Experience Cloud est connecté à votre réseau social, vous pouvez sélectionner **[!UICONTROL Suivant]** pour passer à l’étape de **[!UICONTROL configuration]** .

   ![Informations confirmées](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. À l’étape **[!UICONTROL Configuration]** , saisissez un **[!UICONTROL Nom]** et une **[!UICONTROL Description]** pour votre flux d’activation et saisissez l’ID de **[!UICONTROL compte de votre compte publicitaire réseau social.]** Sélectionnez les cas d&#39;utilisation marketing qui doivent s&#39;appliquer à cette destination. Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

   >[!IMPORTANT]
   >
   > Pour les destinations Facebook. **[!UICONTROL L’ID]** de compte est votre identifiant de compte publicitaire Facebook. Cet identifiant se trouve dans le Gestionnaire d’annonces Facebook. Ajoutez un préfixe à l’identifiant `act_` , comme illustré ci-dessous :

   ![Connexion à la destination du réseau social - étape de configuration](/help/rtcdp/destinations/assets/social-network-setup-step.png)

5. Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement. Sélectionnez **[!UICONTROL Suivant]** pour poursuivre le processus et choisir les segments à activer. In either case, see the next section, [Activate segments to social networks](#activate-segments), for the rest of the workflow.

## Activation de segments sur les réseaux sociaux {#activate-segments}

For instructions on how to activate segments to social networks, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).


<!--

// update IMPORTANT note in step 4 after marketing use cases are released for RTCDP

    >[!IMPORTANT]
    >
    > * The *Single Identity Personalization* marketing use case is selected by default for social network destinations and cannot be removed. 
    > * For Facebook destinations. **[!UICONTROL Account ID]** is your Facebook Ad Account ID. You can find this ID in the Facebook Ads Manager. Prefix the ID with `act_` as shown below: 

    ![Connect to social network destination - setup step](/help/rtcdp/destinations/assets/social-networks-setup-step.png)