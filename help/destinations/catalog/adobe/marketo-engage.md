---
title: Destination du Marketo Engage
description: Marketo Engage is the only end-to-end customer experience management (CXM) solution for marketing, advertising, analytics, and commerce. Il vous permet d’automatiser et de gérer les activités, de la gestion de la relation client à la gestion de la relation client en passant par le marketing basé sur les comptes et l’attribution des recettes.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 9c5a5a49385baa7377ebdc806fd22918c39ad0b2
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 1%

---

# Destination du Marketo Engage {#beta-marketo-engage-destination}

## Présentation {#overview}

Marketo Engage is the only end-to-end customer experience management (CXM) solution for marketing, advertising, analytics, and commerce. Il vous permet d’automatiser et de gérer les activités, de la gestion de la relation client à la gestion de la relation client en passant par le marketing basé sur les comptes et l’attribution des recettes.

La destination permet aux spécialistes du marketing de pousser les segments créés dans Adobe Experience Platform vers Marketo où ils apparaîtront sous forme de listes statiques.

## Supported identities {#supported-identities}

| Identité cible | Description |
|---|---|
| ECID | Espace de noms qui représente l’ECID. Cet espace de noms peut également être référencé par les alias suivants : &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consultez le document suivant sur [ECID](/help/identity-service/ecid.md) pour plus d’informations. |
| Adresse e-mail | Espace de noms représentant une adresse électronique. Ce type d’espace de noms est souvent associé à une seule personne et peut donc être utilisé pour identifier cette personne sur différents canaux. |

>[!NOTE]
>
>Dans le [étape de mappage](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) du workflow d’activation de destination, il s’agit de *mandatory* pour mapper les identités et *facultatif* pour mapper des attributs. Le mappage d’un e-mail et/ou d’un ECID à partir de l’onglet Espace de noms d’identité est la chose la plus importante à faire pour s’assurer que la personne correspond dans Marketo. Mapping Email garantit le taux de correspondance le plus élevé.

## Type d&#39;export {#export-type}

Segment Export - you are exporting all members of a segment (audience) with the identifiers (email, ECID) used in the Marketo Engage destination.

## Configuration de la destination et activation des segments {#set-up}

For detailed instructions on how to set up the destination and activate segments, read [Push an Adobe Experience Platform Segment to a Marketo Static List](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) in the Marketo documentation.

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Utilisation et gouvernance des données {#data-usage-governance}

Tous [!DNL Adobe Experience Platform] Les destinations sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
