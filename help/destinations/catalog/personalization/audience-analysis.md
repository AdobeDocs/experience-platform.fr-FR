---
title: Destination de l’analyse de l’audience
description: Affichez les audiences pour lesquelles les clients remplissent les critères dans Customer Journey Analytics.
badgeLimitedAvailability: label="Disponibilité limitée" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
hide: true
hidefromtoc: yes
TQID: https://experienceleague.adobe.com/BvEkD8a3iIoQsfdSd4MyBDjEkKofmmHpkdHEL14LPv0
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: a37e4ecd-c740-426a-addf-cb1b483c5c5aid: c132d929-fa62-4271-803e-b823be07b914id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
subfeature_v2: id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342id: d1823595-9241-4128-8a33-e4ac3bf08773
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 929
ht-degree: 25%

---

# Destination de l’analyse de l’audience

Utilisez la destination [!UICONTROL Analyse de l’audience] pour enrichir [!DNL Adobe Experience Platform] données d’audience en [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=fr). Vous pouvez sélectionner les audiences à inclure dans les données enrichies résultantes. Les qualifications d’audience sont alors disponibles en tant que dimensions dans les rapports [](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html).

>[!AVAILABILITY]
>
>Cette destination se trouve dans une phase de test limitée. Si vous souhaitez utiliser cette destination, contactez l’équipe chargée de votre compte Adobe.

## Conditions préalables {#prerequisites}

Les éléments suivants sont requis avant d’utiliser cette destination :

* Les privilèges d’accès doivent vous avoir été attribués pour utiliser la destination Analyse de l’audience . Si vous n’avez pas encore l’autorisation d’utiliser cette destination, contactez l’équipe chargée de votre compte Adobe.
* Vous devez disposer des privilèges d’accès pour utiliser Customer Journey Analytics.
* Au moins une audience doit être créée dans [!DNL Adobe Experience Platform].

## Identités prises en charge {#supported-identities}

L’analyse de l’audience prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md). L’Experience Cloud ID (ECID) est généralement utilisé.

| Identité cible | Description | Considérations |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Sélectionnez l’identité cible GAID lorsque votre identité source est un espace de noms GAID. |
| IDFA | Identifiant Apple pour les annonceurs | Sélectionnez l’identité cible IDFA lorsque votre identité source est un espace de noms IDFA. |
| ECID | Experience Cloud ID | Un espace de noms représentant l’ECID. Cet espace de noms peut également être référencé par les alias suivants : « Adobe Marketing Cloud ID », « [!DNL Adobe Experience Cloud] ID », « [!DNL Adobe Experience Platform] ID ». Pour plus d’informations, consultez le document suivant sur [ECID](/help/identity-service/features/ecid.md) . |
| phone_sha256 | Numéros de téléphone hachés avec l’algorithme SHA256 | Le texte brut et les numéros de téléphone hachés SHA256 sont pris en charge par [!DNL Adobe Experience Platform]. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| email_lc_sha256 | Adresses e-mail hachées avec l’algorithme SHA256 | Le texte brut et les adresses e-mail hachées SHA256 sont pris en charge par [!DNL Adobe Experience Platform]. Lorsque votre champ source contient des attributs non hachés, cochez l’option **[!UICONTROL Appliquer la transformation]** pour que [!DNL Experience Platform] hache automatiquement les données lors de l’activation. |
| extern_id | ID d’utilisateur personnalisés | Sélectionnez cette identité cible lorsque votre identité source est un espace de noms personnalisé. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Les types d’audiences suivants sont pris en charge lors de l’utilisation de cette destination :

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Non | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform, telles que [!DNL Adobe Journey Optimizer], </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}



Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects ](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données [!DNL Adobe Experience Platform]. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Exportation de l’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination de l’analyse d’audience. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Lorsqu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation de l’audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configurer une nouvelle destination {#configure-destination}

>[!IMPORTANT]
>
>Pour créer une destination, vous avez besoin de l’autorisation de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour créer cette destination, procédez comme décrit dans le tutoriel sur la configuration des destinations [destination](../../ui/connect-destination.md).

### Détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : nom de la destination.
* **[!UICONTROL Description]** : description de la destination.
* **[!UICONTROL Identifiant du flux de données]** : l’identifiant du flux de données que vous souhaitez enrichir avec des audiences admissibles. Vous pouvez obtenir cet identifiant dans le [gestionnaire de flux de données](/help/datastreams/overview.md).
* **[!UICONTROL Alias d’intégration]** : alias d’intégration.

### Alertes {#alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface d’utilisation](../../ui/alerts.md).

* **[!UICONTROL Taux d’activations ignorées dépassé]** : recevez une notification lorsque le taux d’activations ignorées dépasse un seuil.

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

### Politique de gouvernance et mesures d’application {#governance-policy}

Cette section facultative vous permet de définir vos politiques de gouvernance des données et de vous assurer que les données utilisées sont conformes lorsque les audiences sont envoyées et actives.

Lorsque vous avez terminé de sélectionner les actions marketing souhaitées pour la destination, sélectionnez **[!UICONTROL Créer]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
>
>Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Une fois la destination créée, vous pouvez activer les audiences de votre choix pour la destination.

1. Si vous ne vous trouvez pas déjà dans la destination créée, vous pouvez la retrouver en accédant à **[!UICONTROL Destinations]** > **[!UICONTROL Parcourir]**.
1. Sélectionnez **[!UICONTROL Activer les audiences]**.
1. Sélectionnez les audiences pour lesquelles vous souhaitez analyser les qualifications. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Suivant]**.
1. Vérifiez la configuration de destination et les paramètres de l’audience, puis sélectionnez **[!UICONTROL Terminer]**.

Vous pouvez ajouter d’autres audiences à analyser à l’avenir en revenant à la page **[!UICONTROL Activer les audiences]**. Une fois activées, les audiences ne peuvent pas être supprimées.
