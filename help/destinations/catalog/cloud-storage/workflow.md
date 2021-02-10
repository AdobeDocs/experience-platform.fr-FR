---
keywords: destination de l’enregistrement cloud ; enregistrement cloud
title: Création d’une destination d’enregistrement cloud
type: Tutorial
description: Instructions pour se connecter aux emplacements de stockage dans le cloud
seo-description: Instructions pour se connecter aux emplacements de stockage dans le cloud
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 49%

---


# Création d’une destination d’enregistrement cloud

Cette page explique comment vous pouvez vous connecter à des emplacements d’enregistrement cloud dans Adobe Experience Platform.

Dans **[!UICONTROL Connexions]** > **[!UICONTROL Destinations]**, sélectionnez la destination d’enregistrement de cloud préférée, puis **[!UICONTROL Configurer]**.

![Connexion à la destination de stockage dans le cloud](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>Si une connexion avec cette destination existe déjà, vous pouvez voir un bouton **[!UICONTROL Activer]** sur la carte de destination. Pour plus d&#39;informations sur la différence entre **[!UICONTROL Activer]** et **[!UICONTROL Configurer]**, consultez la section [Catalogue](../../ui/destinations-workspace.md#catalog) de la documentation de l&#39;espace de travail de destination.

À l’étape **[!UICONTROL Authentification]**, si vous avez auparavant configuré une connexion à votre destination de stockage dans le cloud, sélectionnez **[!UICONTROL Compte existant]**, puis la connexion existante. Vous pouvez également sélectionner **[!UICONTROL Nouveau compte]** pour configurer une nouvelle connexion à votre destination de stockage dans le cloud. Renseignez les informations d’authentification de votre compte et sélectionnez **[!UICONTROL Se connecter à la destination]**. Vous pouvez éventuellement joindre votre clé publique au format RSA pour ajouter un chiffrement à vos fichiers exportés. Notez que cette clé publique **doit** être écrite en tant que chaîne codée Base64.

Voir [destination Amazon S3](./amazon-s3.md), destination [[!DNL Amazon Kinesis]](./amazon-kinesis.md), destination [[!DNL Azure Event Hubs]](./azure-event-hubs.md) et destination [SFTP](./sftp.md) pour plus de détails sur les informations d’identification entrées à l’étape **Authentification**.

>[!NOTE]
>
>La plate-forme prend en charge la validation des informations d’identification dans le processus d’authentification et affiche un message d’erreur si vous saisissez des informations d’identification incorrectes à l’emplacement de votre enregistrement cloud. Ainsi, vous n’effectuez pas le workflow avec des informations d’identification incorrectes.

![Connexion à la destination de stockage dans le cloud - étape d’authentification](../../assets/catalog/cloud-storage/workflow/destination-account.png)

À l’étape **[!UICONTROL Configuration]**, saisissez un **[!UICONTROL Nom]** et une **[!UICONTROL Description]** pour votre flux d’activation.

Cette étape vous permet également de sélectionner n’importe quel **[!UICONTROL cas d’utilisation marketing]** qui doit s’appliquer à cette destination. Les cas d’utilisation marketing indiquent l’intention d’exporter les données vers la destination. Vous pouvez choisir parmi des cas d’utilisation marketing définis par Adobe ou créer votre propre cas d’utilisation marketing. Pour plus d&#39;informations sur les cas d&#39;utilisation marketing, consultez la [Présentation des stratégies d&#39;utilisation des données](../../../data-governance/policies/overview.md).

Pour les destinations Amazon S3, insérez le **[!UICONTROL Nom du compartiment]** et le **[!UICONTROL Chemin du dossier]** dans votre destination de stockage dans le cloud où les fichiers seront distribués. Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

![Connexion à la destination de stockage dans le cloud Amazon S3 : étape d’authentification](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

Pour les destinations SFTP, indiquez le **[!UICONTROL chemin du dossier]** dans lequel les fichiers seront distribués. Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

![Connexion à la destination de stockage dans le cloud SFTP : étape d’authentification](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

Pour les destinations [!DNL Amazon Kinesis], indiquez le nom de votre flux de données existant dans votre compte [!DNL Amazon Kinesis]. La plate-forme exportera les données vers ce flux. Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

![Connexion à la destination de l&#39;enregistrement cloud Kinesis - étape d&#39;authentification](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

Pour les destinations [!DNL Azure Event Hubs], indiquez le nom de votre flux de données existant dans votre compte [!DNL Amazon Event Hubs]. La plate-forme exportera les données vers ce flux. Sélectionnez **[!UICONTROL Créer la destination]** après avoir renseigné les champs ci-dessus.

![Connexion à la destination de l&#39;enregistrement cloud des concentrateurs de Événement - étape d&#39;authentification](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

Votre destination est maintenant créée. Vous pouvez sélectionner **[!UICONTROL Enregistrer et quitter]** si vous souhaitez activer les segments ultérieurement. Sélectionnez **[!UICONTROL Suivant]** pour poursuivre le workflow et choisir les segments à activer. Dans les deux cas, consultez la section suivante, [Activation des segments](#activate-segments), pour le reste du processus d’exportation des données.

## Activation des segments {#activate-segments}

Pour obtenir des informations sur le processus d’activation des segments, voir [Activer les profils et les segments à une destination](../../ui/activate-destinations.md).