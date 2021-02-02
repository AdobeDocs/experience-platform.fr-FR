---
keywords: Facebook ; facebook ; réseau social ; réseau social ; authentification du réseau social ; authentification du réseau social ; authentification du réseau social
title: Workflow de destinations de réseau social
type: Tutorial
seo-title: Workflow de destinations de réseau social
description: Instructions de connexion à vos comptes publicitaires de réseau social
seo-description: Instructions de connexion à vos comptes publicitaires de réseau social
translation-type: tm+mt
source-git-commit: d1aa2c825cd679d593cf97d84506058482a7fe8f
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 56%

---


# Processus d’authentification des destinations de réseau social {#social-network-destinations-workflow}

## Processus de création de destinations de réseau social

Ce didacticiel utilise [!DNL Facebook] comme exemple, mais le flux de travail dans Adobe Experience Platform sera le même pour toutes les destinations de réseau social, une fois de plus ajouté au produit.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, faites défiler la catégorie **[!UICONTROL Social]**. Sélectionnez la destination de votre réseau social préférée, puis **[!UICONTROL Configurer]**.

![Connexion à la destination de réseau social](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Si une connexion avec cette destination existe déjà, vous pouvez voir un bouton **[!UICONTROL Activer]** sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

À l’étape **Authentification**, si vous avez auparavant configuré une connexion à votre destination de réseau social, sélectionnez **[!UICONTROL Compte existant]**, puis sélectionnez la connexion existante. Vous pouvez aussi sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion à votre destination de réseau social. Sélectionnez **[!UICONTROL Se connecter à la destination]** pour atteindre la destination de réseau social sélectionnée afin de vous identifier et de connecter Adobe Experience Cloud à votre compte publicitaire sur le réseau social.

>[!NOTE]
>
>La plate-forme prend en charge la validation des informations d’identification dans le processus d’authentification et affiche un message d’erreur si vous saisissez des informations d’identification incorrectes à l’identifiant de compte de réseau social. Ainsi, vous n’effectuez pas le workflow avec des informations d’identification incorrectes.

![Connexion à la destination de réseau social - étape d’authentification](../../assets/catalog/social/workflow/pre-connect.png)

Une fois vos informations d’identification confirmées et la connexion d’Adobe Experience Cloud à votre réseau social établie, vous pouvez sélectionner **[!UICONTROL Suivant]** pour passer à l’étape de **[!UICONTROL Configuration]**.

![Informations d’identification confirmées](../../assets/catalog/social/workflow/post-connect.png)

À l’étape **[!UICONTROL Configuration]**, saisissez un [!UICONTROL Nom] et une [!UICONTROL Description] pour votre flux d’activation et saisissez l’[!UICONTROL identifiant de compte] de votre compte publicitaire sur le réseau social.

Cette étape vous permet également de sélectionner n’importe quel **[!UICONTROL cas d’utilisation marketing]** qui doit s’appliquer à cette destination. Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d&#39;informations sur les cas d&#39;utilisation marketing, consultez la [Présentation des stratégies d&#39;utilisation des données](../../../data-governance/policies/overview.md).

Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

>[!IMPORTANT]
>
> * Pour les destinations [!DNL Facebook]. **[!UICONTROL L’]** ID de compte est votre  [!DNL Facebook Ad Account ID]identifiant. Vous pouvez trouver cet ID dans le [!DNL Facebook Ads Manager]. Préfixez l’identifiant avec `act_`, comme indiqué ci-dessous :


![Connexion à la destination du réseau social - étape de configuration](../../assets/catalog/social/workflow/setup.png)

Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement. Sélectionnez **[!UICONTROL Suivant]** pour poursuivre le workflow et choisir les segments à activer. Dans les deux cas, consultez la section suivante, [Activation des segments vers les réseaux sociaux](#activate-segments), pour le reste du workflow.

## Activation des segments vers les réseaux sociaux {#activate-segments}

Pour des instructions sur l’activation des segments vers les réseaux sociaux, consultez [Activation des données vers les destinations](../../ui/activate-destinations.md).