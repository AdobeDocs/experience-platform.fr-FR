---
title: Connecter Demandbase Intent à Experience Platform à l’aide de l’interface utilisateur
description: Découvrez comment connecter Demandbase Intent à Experience Platform
hide: true
hidefromtoc: true
exl-id: 7dc87067-cdf6-4dde-b077-19666dcb12e2
source-git-commit: 911aad600dd2618ba98d2ccee737aaedea4f2735
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 53%

---

# Connexion d’[!DNL Demandbase Intent] à Experience Platform à l’aide de l’interface utilisateur

Lisez ce guide pour savoir comment connecter votre compte [!DNL Demandbase Intent] à Adobe Experience Platform à l’aide de l’interface utilisateur.

## Commencer

Ce tutoriel nécessite une compréhension du fonctionnement des composants suivants d’Adobe Experience Platform : 

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md) : Real-Time CDP B2B edition est conçu pour les professionnels du marketing travaillant dans un modèle de service business-to-business. Elle rassemble des données provenant de sources multiples et les combine en une vue unique des profils de comptes et d’utilisateurs. Ces données unifiées permettent aux spécialistes marketing de cibler précisément des audiences spécifiques afin de stimuler leur engagement sur tous les canaux disponibles.
* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

## Parcourir le catalogue des sources {#navigate}

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Sources]** dans le volet de navigation de gauche pour accéder à l’espace de travail [!UICONTROL Sources]. Vous pouvez sélectionner la catégorie appropriée dans le catalogue sur le côté gauche de votre écran. Vous pouvez également trouver la source spécifique à utiliser à l’aide de l’option de recherche.

Sélectionnez **[!DNL Demandbase Intent]** sous la catégorie *[!UICONTROL B2B]*, puis sélectionnez **[!UICONTROL Configurer]**.

>[!TIP]
>
>Les sources du catalogue affichent l’option **[!UICONTROL Configurer]** lorsqu’une source donnée ne dispose pas encore d’un compte authentifié. Une fois qu’un compte authentifié existe, cette option devient **[!UICONTROL Ajouter des données]**.



## Utiliser un compte existant {#existing}

## Créer un nouveau compte {#create}

## Fournir des détails sur le flux de données {#provide-dataflow-details}

>[!CONTEXTUALHELP]
>id="platform_sources_demandbase_domain"
>title="Source du domaine"
>abstract="Bien qu’Adobe utilise le champ XDM accountOrganization.website, il se peut que des clientes et clients utilisent des champs personnalisés pour leurs sites web respectifs. Par conséquent, vous devez vous assurer que votre source de domaine est le champ domaine/site web qui correspondra à vos enregistrements de compte Demandbase par rapport aux comptes Experience Platform."

## Planifier le flux de données {#schedule-dataflow}

>[!CONTEXTUALHELP]
>id="platform_sources_demandbase_schedule"
>title="Planifier le flux de données"
>abstract="Demandbase délivre des données une fois par semaine, le lundi à 17 h 00 UTC. Par conséquent, vous devez configurer l’heure de début de l’ingestion après 17 h 00 UTC. De plus, lors de l’envoi de fichiers à Adobe, vous devez confirmer l’heure d’ingestion avec Demandbase, car leur planning pourrait être modifié."

## Vérifier le flux de données {#review-dataflow}
