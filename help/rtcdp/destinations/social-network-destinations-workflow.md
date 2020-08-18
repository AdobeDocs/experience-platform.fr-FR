---
title: Workflow de destinations de réseau social
seo-title: Workflow de destinations de réseau social
description: Instructions de connexion à vos comptes publicitaires de réseau social
seo-description: Instructions de connexion à vos comptes publicitaires de réseau social
translation-type: tm+mt
source-git-commit: 9306266edc0a4afdcf378e94b46b239187b18644
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 58%

---


# Social Network destinations authentication workflow {#social-network-destinations-workflow}

## Processus de création de destinations de réseau social

This tutorial uses [!DNL Facebook] as an example, but the workflow in Adobe Real-time Customer Data Platform will be the same for all social network destinations, once more are added to the product.

1. In **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, scroll to the **[!UICONTROL Social]** category. Select your preferred social network destination, then select **[!UICONTROL Configure]**.

   ![Connexion à la destination de réseau social](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

   >[!NOTE]
   >
   >Si une connexion à cette destination existe déjà, un bouton **[!UICONTROL Activer]** s’affiche sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](/help/rtcdp/destinations/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

2. À l’étape **Authentification**, si vous avez auparavant configuré une connexion à votre destination de réseau social, sélectionnez **[!UICONTROL Compte existant]**, puis sélectionnez la connexion existante. Vous pouvez aussi sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion à votre destination de réseau social. Sélectionnez **[!UICONTROL Se connecter à la destination]** pour atteindre la destination de réseau social sélectionnée afin de vous identifier et de connecter Adobe Experience Cloud à votre compte publicitaire sur le réseau social.

   >[!NOTE]
   >
   >La plateforme de données clients en temps réel d’Adobe prend en charge la validation des informations d’identification dans le processus d’authentification et affiche un message d’erreur si vous saisissez des informations d’identification incorrectes pour votre compte sur le réseau social. Ainsi, vous n’effectuez pas le workflow avec des informations d’identification incorrectes.

   ![Connexion à la destination de réseau social - étape d’authentification](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Une fois vos informations d’identification confirmées et la connexion d’Adobe Experience Cloud à votre réseau social établie, vous pouvez sélectionner **[!UICONTROL Suivant]** pour passer à l’étape de **[!UICONTROL Configuration]**.

   ![Informations d’identification confirmées](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. À l’étape **[!UICONTROL Configuration]**, saisissez un **[!UICONTROL Nom]** et une **[!UICONTROL Description]** pour votre flux d’activation et saisissez l’**[!UICONTROL identifiant de compte]** de votre compte publicitaire sur le réseau social. <br> Cette étape vous permet également de sélectionner tout cas **[!UICONTROL d’utilisation]** marketing à appliquer à cette destination. Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d’informations sur les cas d’utilisation marketing, voir la page Gouvernance des [données dans le CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) en temps réel. Pour plus d’informations sur les cas d’utilisation marketing définis par l’Adobe, voir la présentation [des stratégies d’utilisation des](/help/data-governance/policies/overview.md#core-actions)données. <br> Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

   >[!IMPORTANT]
   >
   > * Le cas d’utilisation de la personnalisation *d’identité* unique pour le marketing est sélectionné par défaut pour les destinations de réseau social et ne peut pas être supprimé.
   > * Pour [!DNL Facebook] les destinations. **[!UICONTROL L’ID]** de compte est votre [!DNL Facebook Ad Account ID]identifiant. Vous pouvez trouver cet identifiant dans le [!DNL Facebook Ads Manager]. Préfixez l’identifiant avec `act_`, comme indiqué ci-dessous :


   ![Connexion à la destination du réseau social - étape de configuration](/help/rtcdp/destinations/assets/social-networks-setup-step.png)

5. Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement. Sélectionnez **[!UICONTROL Suivant]** pour poursuivre le workflow et choisir les segments à activer. Dans les deux cas, consultez la section suivante, [Activation des segments vers les réseaux sociaux](#activate-segments), pour le reste du workflow.

## Activation des segments vers les réseaux sociaux {#activate-segments}

Pour des instructions sur l’activation des segments vers les réseaux sociaux, consultez [Activation des données vers les destinations](/help/rtcdp/destinations/activate-destinations.md).