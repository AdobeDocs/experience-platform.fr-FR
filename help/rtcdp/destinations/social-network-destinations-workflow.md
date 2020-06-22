---
title: Flux de travaux Destinations des réseaux sociaux
seo-title: Flux de travaux Destinations des réseaux sociaux
description: Instructions de connexion à vos comptes publicitaires de réseaux sociaux
seo-description: Instructions de connexion à vos comptes publicitaires de réseaux sociaux
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 11%

---


# Processus d’authentification des destinations réseau social {#social-network-destinations-workflow}

## Processus de création de destinations de réseau social

Ce didacticiel utilise Facebook comme exemple, mais le flux de travail dans Adobe Real-time Customer Data Platform sera le même pour toutes les destinations de réseau social, une fois le produit ajouté.

1. Dans **[!UICONTROL Destinations > Catalogue]**, faites défiler l’écran jusqu’à la catégorie **[!UICONTROL Social]** . Sélectionnez la destination de réseau social que vous préférez, puis sélectionnez **[!UICONTROL Connecter la destination]**.

   ![Se connecter à la destination du réseau social](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. In the **Authentication** step, if you had previously set up a connection to your social network destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to your social network destination. Sélectionnez **[!UICONTROL Se connecter à la destination]** et vous conduira à la destination de réseau social sélectionnée pour vous connecter et connecter Adobe Experience Cloud à votre compte publicitaire de réseau social.

   >[!NOTE]
   >
   >Adobe Real-time CDP prend en charge la validation des informations d’identification dans le processus d’authentification et affiche un message d’erreur si vous saisissez des informations d’identification incorrectes dans l’ID de compte de réseau social. Ainsi, vous n’effectuez pas le processus avec des informations d’identification incorrectes.

   ![Connexion à la destination du réseau social - étape d’authentification](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Une fois vos informations d’identification confirmées et qu’Adobe Experience Cloud est connecté à votre réseau social, vous pouvez sélectionner **[!UICONTROL Suivant]** pour passer à l’étape de **[!UICONTROL configuration]** .

   ![Informations confirmées](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. À l’étape **[!UICONTROL Configuration]** , saisissez un **[!UICONTROL Nom]** et une **[!UICONTROL Description]** pour votre flux d’activation et saisissez l’ID de **[!UICONTROL compte de votre compte publicitaire réseau social.]** <br> Cette étape vous permet également de sélectionner tout cas **[!UICONTROL d’utilisation]** marketing à appliquer à cette destination. Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi les cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d’informations sur les cas d’utilisation marketing, voir la page Gouvernance des [données dans le CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) en temps réel. Pour plus d’informations sur les cas d’utilisation marketing définis individuellement par Adobe, voir l’aperçu [des stratégies d’utilisation des](/help/data-governance/policies/overview.md#core-actions)données. <br> Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

   >[!IMPORTANT]
   >
   > * Le cas d’utilisation de la personnalisation *d’identité* unique pour le marketing est sélectionné par défaut pour les destinations de réseau social et ne peut pas être supprimé.
   > * Pour les destinations Facebook. **[!UICONTROL L’ID]** de compte est votre identifiant de compte publicitaire Facebook. Cet identifiant se trouve dans le Gestionnaire d’annonces Facebook. Ajoutez un préfixe à l’identifiant `act_` , comme illustré ci-dessous :


   ![Connexion à la destination du réseau social - étape de configuration](/help/rtcdp/destinations/assets/social-networks-setup-step.png)

5. Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement. Sélectionnez **[!UICONTROL Suivant]** pour poursuivre le processus et choisir les segments à activer. In either case, see the next section, [Activate segments to social networks](#activate-segments), for the rest of the workflow.

## Activation de segments sur les réseaux sociaux {#activate-segments}

For instructions on how to activate segments to social networks, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).