---
title: Destination du Marketo Engage
description: Marketo Engage est la seule solution de gestion de l’expérience client de bout en bout (CXM) pour le marketing, la publicité, les analyses et le commerce. Il vous permet d’automatiser et de gérer les activités, de la gestion de la relation client à la gestion de la relation client en passant par le marketing basé sur les comptes et l’attribution des recettes.
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 3%

---


# (Version bêta) Destination du Marketo Engage {#beta-marketo-engage-destination}

>[!IMPORTANT]
>
>La destination du Marketo Engage dans Adobe Experience Platform est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

## Présentation {#overview}

Marketo Engage est la seule solution de gestion de l’expérience client de bout en bout (CXM) pour le marketing, la publicité, les analyses et le commerce. Il vous permet d’automatiser et de gérer les activités, de la gestion de la relation client à la gestion de la relation client en passant par le marketing basé sur les comptes et l’attribution des recettes.

Le connecteur de segment permet aux marketeurs de pousser les segments créés dans Adobe Experience Platform vers Marketo où ils apparaîtront sous forme de listes statiques.

## Identités prises en charge {#supported-identities}

| Identité cible | Description |
|---|---|
| ECID | Espace de noms qui représente l’ECID. Cet espace de noms peut également être référencé par les alias suivants : &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consultez le document suivant sur [ECID](/help/identity-service/ecid.md) pour plus d’informations. |
| Email | Espace de noms représentant une adresse électronique. Ce type d’espace de noms est souvent associé à une seule personne et peut donc être utilisé pour identifier cette personne sur différents canaux. |

## Type d&#39;export {#export-type}

Exportation de segments : vous exportez tous les membres d’un segment (audience) avec les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination du Marketo Engage.

## Configuration {#set-up}

Vous trouverez des instructions sur la configuration de la destination [ici](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en).

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

## Utilisation et gouvernance des données {#data-usage-governance}

Toutes les destinations [!DNL Adobe Experience Platform] sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour plus d’informations sur la façon dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Activation des segments vers cette destination {#activate}

Voir [Activation des données d’audience vers les destinations d’exportation de segments en flux continu](../../ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.
