---
title: Destination Marketo Engage
description: Marketo Engage est la seule solution de gestion de l’expérience client de bout en bout (CXM) pour le marketing, la publicité, les analyses et le commerce. Il vous permet d’automatiser et de gérer les activités, de la gestion de la relation client à la gestion de la relation client en passant par le marketing basé sur les comptes et l’attribution des recettes.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 26%

---

# Destination du Marketo Engage {#beta-marketo-engage-destination}

## Journal des modifications de destination {#changelog}

>[!IMPORTANT]
>
>Avec la publication de la [connecteur de destination Marketo V2 amélioré](/help/release-notes/2022/july-2022.md#destinations), vous voyez maintenant deux cartes Marketo dans le catalogue des destinations.
>* Si vous activez déjà les données de la variable **[!UICONTROL Marketo V1]** destination : créez de nouveaux flux de données pour la variable **[!UICONTROL Marketo V2]** destination et suppression des flux de données existants dans **[!UICONTROL Marketo V1]** destination d’ici février 2023. À compter de cette date, la variable **[!UICONTROL Marketo V1]** la carte de destination sera supprimée.
>* Si vous n’avez pas encore créé de flux de données pour la variable **[!UICONTROL Marketo V1]** destination, veuillez utiliser la nouvelle **[!UICONTROL Marketo V2]** pour vous connecter à Marketo et exporter des données vers cette application.

![Image des deux cartes de destination Marketo dans une vue côte à côte.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Les améliorations apportées à la destination Marketo V2 sont les suivantes :

* Dans Marketo V1, à l’étape de **[!UICONTROL Planification de segment]** du processus d’activation, il vous fallait ajouter manuellement un **ID de mappage** pour exporter des données vers Marketo. Cette étape manuelle n’est plus obligatoire dans Marketo V2.
* Dans Marketo V1, à l’étape de **[!UICONTROL Mappage]** du processus d’activation, vous ne pouviez mapper les champs XDM qu’à trois champs cibles dans Marketo : `firstName`, `lastName` et `companyName`. Avec la version Marketo V2, vous pouvez désormais mapper des champs XDM à de nombreux autres champs dans Marketo. Pour plus d’informations, consultez la section [attributs pris en charge](#supported-attributes) voir la section ci-dessous.

## Vue d’ensemble {#overview}

[!DNL Marketo Engage] est la seule solution de gestion de l’expérience client de bout en bout (CXM) pour le marketing, la publicité, l’analyse et le commerce. Il vous permet d’automatiser et de gérer les activités, de la gestion de la relation client à la gestion de la relation client en passant par le marketing basé sur les comptes et l’attribution des recettes.

La destination permet aux marketeurs de pousser les audiences créées dans Adobe Experience Platform vers Marketo où elles apparaîtront sous forme de listes statiques.

## Identités et attributs pris en charge {#supported-identities-attributes}

>[!NOTE]
>
>Dans le [étape de mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) du workflow d’activation de destination, il s’agit de *mandatory* pour mapper les identités et *facultatif* pour mapper des attributs. Le mappage d’un e-mail et/ou d’un ECID à partir de l’onglet Espace de noms d’identité est la chose la plus importante à faire pour s’assurer que la personne correspond dans Marketo. Mapping Email garantit le taux de correspondance le plus élevé.

### Identités prises en charge {#supported-identities}

| Identité cible | Description |
|---|---|
| ECID | Espace de noms qui représente l’ECID. Cet espace de noms peut également être référencé par les alias suivants : « ID Adobe Marketing Cloud », « ID Adobe Experience Cloud », « ID Adobe Experience Platform ». Consultez le document suivant sur [ECID](/help/identity-service/features/ecid.md) pour plus d’informations. |
| E-mail | Espace de noms représentant une adresse électronique. Ce type d’espace de noms est souvent associé à une seule personne et peut donc être utilisé pour identifier cette personne sur différents canaux. |

{style="table-layout:auto"}

### Attributs pris en charge {#supported-attributes}

Vous pouvez mapper des attributs d’Experience Platform à n’importe quel attribut auquel votre organisation a accès dans Marketo. Dans Marketo, vous pouvez utiliser la variable [Description de la requête API](https://developers.marketo.com/rest-api/lead-database/leads/#describe) pour récupérer les champs d’attribut auxquels votre organisation a accès.

## Audiences prises en charge {#supported-audiences}

Cette section décrit les types d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Export d’audience]** | Vous exportez tous les membres d’une audience avec les identifiants (email, ECID) utilisés dans la variable [!DNL Marketo Engage] destination. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configuration de la destination et activation des audiences {#set-up}

>[!IMPORTANT]
> 
>* Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]** et **[!UICONTROL Gestion des destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions).
>* Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Affichage des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Pour obtenir des instructions détaillées sur la configuration de la destination et l’activation des audiences, consultez [Envoi d’une audience Adobe Experience Platform vers une liste statique Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=fr) dans la documentation de Marketo.

La vidéo ci-dessous présente également les étapes de configuration d’une destination Marketo et d’activation d’audiences.

>[!IMPORTANT]
>
>La vidéo ne reflète pas entièrement la fonctionnalité actuelle. Pour obtenir les informations les plus récentes, consultez le guide ci-dessus. Les parties suivantes de la vidéo sont obsolètes :
> 
>* La carte de destination que vous devez utiliser dans l’interface utilisateur de l’Experience Platform est **[!UICONTROL Marketo V2]**.
>* La vidéo n’affiche pas la nouvelle **[!UICONTROL Création de personne]** champ sélecteur dans le workflow de connexion à la destination.
>* Les deux limitations mentionnées dans la vidéo ne s&#39;appliquent plus. Vous pouvez désormais mapper de nombreux autres champs d’attribut de profil en plus des informations d’appartenance à l’audience qui étaient prises en charge au moment de l’enregistrement de la vidéo. Vous pouvez également exporter des membres d’audience vers Marketo qui n’existent pas encore dans vos listes statiques Marketo et qui seront ajoutés aux listes.
>* Dans le **[!UICONTROL Étape Planifier l’audience]** dans le workflow d’activation, dans Marketo V1, vous devez ajouter manuellement une **[!UICONTROL ID de mappage]** pour exporter des données vers Marketo. Cette étape manuelle n’est plus obligatoire dans Marketo V2.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr).

<!--

## Activate audiences to this destination {#activate}

See [Activate audience data to streaming audience export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audiences to this destination.

-->
