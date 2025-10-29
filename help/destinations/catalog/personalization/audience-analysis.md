---
title: Destination de l’analyse de l’audience
description: Affichez les audiences pour lesquelles les clients remplissent les critères dans Customer Journey Analytics.
badgeLimitedAvailability: label="Disponibilité limitée" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
hide: true
hidefromtoc: true
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 33%

---

# Destination de l’analyse de l’audience

La destination [!UICONTROL Audience Analysis] vous permet d’enrichir les données d’audience Adobe Experience Platform en [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=fr). Vous pouvez sélectionner les audiences à inclure dans les données enrichies résultantes. Les qualifications d’audience sont alors disponibles en tant que dimensions dans les rapports [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html).

>[!AVAILABILITY]
>
>Cette destination se trouve dans une phase de test limitée. Si vous souhaitez utiliser cette destination, contactez l’équipe chargée de votre compte Adobe.

## Conditions préalables

Les éléments suivants sont requis avant d’utiliser cette destination :

* Les privilèges d’accès doivent vous avoir été attribués pour utiliser la destination Analyse de l’audience . Si vous n’avez pas encore l’autorisation d’utiliser cette destination, contactez l’équipe chargée de votre compte Adobe.
* Vous devez disposer des privilèges d’accès pour utiliser Customer Journey Analytics.
* Au moins une audience doit être créée dans Adobe Experience Platform.

## Identités prises en charge

L’analyse de l’audience prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md). L’Experience Cloud ID (ECID) est généralement utilisé.

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |
| ECID | Experience Cloud ID | Un espace de noms représentant l’ECID. Cet espace de noms peut également être référencé par les alias suivants : « ID Adobe Marketing Cloud », « ID Adobe Experience Cloud », « ID Adobe Experience Platform ». Pour plus d’informations, consultez le document suivant sur [ECID](/help/identity-service/features/ecid.md) . |
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Apply transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| extern_id | ID d’utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

{style="table-layout:auto"}

## Audiences prises en charge

Les types d’audiences suivants sont pris en charge lors de l’utilisation de cette destination :

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination de l’analyse d’audience. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Lorsqu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation de l’audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configurer une nouvelle destination

>[!IMPORTANT]
> 
>Pour créer la destination , vous avez besoin des autorisations **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour créer cette destination, procédez comme décrit dans le tutoriel sur la configuration des destinations [destination](../../ui/connect-destination.md).

### Détails de la destination

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : nom de la destination.
* **[!UICONTROL Description]** : description de la destination.
* **[!UICONTROL Datastream ID]** : identifiant du flux de données que vous souhaitez enrichir avec des audiences admissibles. Vous pouvez obtenir cet identifiant dans le [gestionnaire de flux de données](/help/datastreams/overview.md).
* **[!UICONTROL Integration alias]** : alias de l’intégration.

### Alertes

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface d’utilisation](../../ui/alerts.md).

* **[!UICONTROL Activation Skipped Rate Exceed]** : recevoir une notification lorsque le taux d’activation ignoré dépasse un seuil.

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

### Politique de gouvernance et mesures d’application

Cette section facultative vous permet de définir vos politiques de gouvernance des données et de vous assurer que les données utilisées sont conformes lorsque les audiences sont envoyées et actives.

Lorsque vous avez terminé de sélectionner les actions marketing souhaitées pour la destination, sélectionnez **[!UICONTROL Create]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Une fois la destination créée, vous pouvez activer les audiences de votre choix pour la destination.

1. Si vous ne vous trouvez pas déjà dans la destination créée, vous pouvez la retrouver en accédant à **[!UICONTROL Destinations]** > **[!UICONTROL Browse]**.
1. Sélectionnez **[!UICONTROL Activate audiences]**.
1. Sélectionnez les audiences pour lesquelles vous souhaitez analyser les qualifications. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Next]**.
1. Vérifiez la configuration de destination et les paramètres d’audience, puis sélectionnez **[!UICONTROL Finish]**.

Vous pouvez ajouter d’autres audiences à analyser à l’avenir en revenant à la page **[!UICONTROL Activate audiences]**. Une fois activées, les audiences ne peuvent pas être supprimées.
