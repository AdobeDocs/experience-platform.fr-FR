---
keywords: cloud storage destination;cloud storage
title: Processus des destinations de stockage dans le cloud
seo-title: Processus des destinations de stockage dans le cloud
type: Tutorial
description: Instructions pour se connecter aux emplacements de stockage dans le cloud
seo-description: Instructions pour se connecter aux emplacements de stockage dans le cloud
translation-type: tm+mt
source-git-commit: 24c8dd0f01d7ea14b2fa5827722e797bd209f50c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 50%

---


# Workdlow de création de destinations de stockage dans le cloud

## Présentation

Cette page explique comment vous pouvez vous connecter à des emplacements d’enregistrement cloud dans la plateforme de données clientes en temps réel.

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, select your preferred cloud storage destination, then select **[!UICONTROL Configure]**.

![Connexion à la destination de stockage dans le cloud](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>Si une connexion à cette destination existe déjà, un bouton **[!UICONTROL Activer]** s’affiche sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

À l’étape **[!UICONTROL Authentification]**, si vous avez auparavant configuré une connexion à votre destination de stockage dans le cloud, sélectionnez **[!UICONTROL Compte existant]**, puis la connexion existante. Vous pouvez également sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion à votre destination de stockage dans le cloud. Renseignez les informations d’authentification de votre compte et sélectionnez **[!UICONTROL Se connecter à la destination]**. Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Notez que cette clé publique **doit** être écrite en tant que chaîne codée Base64.

See [Amazon S3](./amazon-s3.md) destination, [[!DNL Amazon Kinesis]](./amazon-kinesis.md) destination, [[!DNL Azure Event Hubs]](./azure-event-hubs.md) destination, and [SFTP](./sftp.md) destination for specifics around credentials input in the **Authentication** step.

>[!NOTE]
>
>Le CDP en temps réel prend en charge la validation des informations d’identification dans le processus d’authentification et affiche un message d’erreur si vous saisissez des informations d’identification incorrectes à l’emplacement de votre enregistrement cloud. Ainsi, vous n’effectuez pas le workflow avec des informations d’identification incorrectes.

![Connexion à la destination de stockage dans le cloud - étape d’authentification](../../assets/catalog/cloud-storage/workflow/destination-account.png)

À l’étape **[!UICONTROL Configuration]**, saisissez un **[!UICONTROL Nom]** et une **[!UICONTROL Description]** pour votre flux d’activation.

Cette étape vous permet également de sélectionner tout cas **[!UICONTROL d’utilisation]** marketing à appliquer à cette destination. Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d’informations sur les cas d’utilisation marketing, voir la page Gouvernance des [données dans le CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) en temps réel. Pour plus d’informations sur les cas d’utilisation marketing définis par l’Adobe, voir la présentation [des stratégies d’utilisation des](../../../data-governance/policies/overview.md#core-actions)données.

Pour les destinations Amazon S3, insérez le **[!UICONTROL Nom du compartiment]** et le **[!UICONTROL Chemin du dossier]** dans votre destination de stockage dans le cloud où les fichiers seront distribués. Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

![Connexion à la destination de stockage dans le cloud Amazon S3 : étape d’authentification](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

Pour les destinations SFTP, indiquez le **[!UICONTROL chemin du dossier]** dans lequel les fichiers seront distribués. Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

![Connexion à la destination de stockage dans le cloud SFTP : étape d’authentification](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

Pour [!DNL Amazon Kinesis] les destinations, indiquez le nom de votre flux de données existant dans votre [!DNL Amazon Kinesis] compte. Le CDP en temps réel exportera les données dans ce flux. Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

![Connexion à la destination de l&#39;enregistrement cloud Kinesis - étape d&#39;authentification](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

Pour [!DNL Azure Event Hubs] les destinations, indiquez le nom de votre flux de données existant dans votre [!DNL Amazon Event Hubs] compte. Le CDP en temps réel exportera les données dans ce flux. Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

![Connexion à la destination de l&#39;enregistrement cloud des concentrateurs de Événement - étape d&#39;authentification](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement. Sélectionnez **[!UICONTROL Suivant]** pour poursuivre le workflow et choisir les segments à activer. Dans les deux cas, consultez la section suivante, [Activation des segments](#activate-segments), pour le reste du processus d’exportation des données.

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](../../ui/activate-destinations.md).