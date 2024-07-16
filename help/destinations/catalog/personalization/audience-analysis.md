---
title: Destination Audience Analysis
description: Afficher les audiences auxquelles les clients sont qualifiés dans Customer Journey Analytics.
badgeLimitedAvailability: label="Disponibilité limitée" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 38%

---

# Destination Audience Analysis

La destination [!UICONTROL Audience Analysis] vous permet d’enrichir les données d’audience Adobe Experience Platform en [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=fr). Vous pouvez sélectionner les audiences à inclure dans les données enrichies obtenues. Les qualifications d’audience sont ensuite disponibles en tant que dimensions dans les rapports [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html).

>[!AVAILABILITY]
>
>Cette destination est en phase de test limitée. Si vous souhaitez utiliser cette destination, contactez votre équipe de compte d’Adobe.

## Conditions préalables

Les éléments suivants sont requis avant d’utiliser cette destination :

* Vous devez être configuré pour utiliser la destination Audience Analysis. Si vous n’êtes pas encore configuré pour utiliser cette destination, contactez votre équipe de compte d’Adobe.
* Vous devez être configuré pour utiliser Customer Journey Analytics.
* Vous devez avoir au moins une audience créée dans Adobe Experience Platform.

## Identités prises en charge

Audience Analysis prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md). L’ID d’Experience Cloud (ECID) est généralement utilisé.

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |
| ECID | Experience Cloud ID | Espace de noms qui représente l’ECID. Cet espace de noms peut également être référencé par les alias suivants : « ID Adobe Marketing Cloud », « ID Adobe Experience Cloud », « ID Adobe Experience Platform ». Consultez le document suivant sur [ECID](/help/identity-service/features/ecid.md) pour plus d’informations. |
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les numéros de téléphone hachés avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Adobe Experience Platform prend en charge le texte brut et les adresses e-mail hachées avec SHA256. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Platform] hache automatiquement les données lors de l’activation. |
| extern_id | ID utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

{style="table-layout:auto"}

## Audiences prises en charge

Les types d’audiences suivants sont pris en charge lors de l’utilisation de cette destination :

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination de l’analyse de l’audience. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Lorsqu’un profil est mis à jour en Experience Platform en fonction de l’évaluation de l’audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configurer une nouvelle destination

>[!IMPORTANT]
> 
>Pour créer une destination, vous avez besoin de l’autorisation de **[!UICONTROL Affichage des destinations]** et de **[!UICONTROL Gestion des destinations]** [ ](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour créer cette destination, suivez les étapes décrites dans le [tutoriel de configuration de destination](../../ui/connect-destination.md).

### Détails de la destination

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : nom de destination.
* **[!UICONTROL Description]** : description de la destination.
* **[!UICONTROL Identifiant du flux de données]** : l’identifiant du flux de données que vous souhaitez enrichir avec les audiences admissibles. Vous pouvez obtenir cet identifiant dans le [gestionnaire de jeux de données](/help/datastreams/overview.md).
* **[!UICONTROL Alias d’intégration]** : alias d’intégration.

### Alertes

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

* **[!UICONTROL Taux d’activation ignoré dépassé]** : soyez averti lorsque le taux d’activation ignoré dépasse un seuil.

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

### Politiques de gouvernance et actions d’application

Cette section facultative vous permet de définir vos stratégies de gouvernance des données et de vous assurer que les données utilisées sont conformes lorsque les audiences sont envoyées et actives.

Lorsque vous avez terminé de sélectionner les actions marketing souhaitées pour la destination, sélectionnez **[!UICONTROL Créer]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Une fois la destination créée, vous pouvez activer les audiences de votre choix pour la destination.

1. Si vous n’êtes pas déjà dans la destination créée, vous pouvez la retrouver en accédant à **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]**.
1. Sélectionnez **[!UICONTROL Activer les audiences]**.
1. Sélectionnez les audiences pour lesquelles vous souhaitez analyser les qualifications. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.
1. Vérifiez la configuration de destination et les paramètres de l’audience, puis sélectionnez **[!UICONTROL Terminer]**.

Vous pouvez ajouter d’autres audiences à analyser ultérieurement en revenant à la page **[!UICONTROL Activer les audiences]** . Une fois activées, les audiences ne peuvent pas être supprimées.
