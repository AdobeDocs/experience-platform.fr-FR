---
title: Présentation Des Événements De Diffusion En Continu Capillaires
description: Découvrez comment diffuser des données de Capillary vers Experience Platform.
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: 428aed259343f56a2bf493b40ff2388340fffb7b
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 2%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>La source [!DNL Capillary Streaming Events] est en version Beta. Lisez les [termes et conditions](../../home.md#terms-and-conditions) dans la présentation des sources pour plus d’informations sur l’utilisation de sources étiquetées bêta.

[!DNL Capillary Technologies] est une plateforme de fidélité et d’engagement de premier plan, approuvée par plus de 300 marques à travers le monde. Utilisez la source [!DNL Capillary Streaming Events] pour permettre à votre entreprise de diffuser en toute transparence les profils clients, les données de fidélité et les événements transactionnels de [!DNL Capillary] vers Adobe Experience Platform. Connectez votre source [!DNL Capillary] pour activer la personnalisation en temps réel, la segmentation avancée des audiences et l’orchestration de campagnes omnicanal.

En intégrant [!DNL Capillary] à Experience Platform, vous pouvez :

* Synchronisez **points de fidélité, niveaux et récompenses** en temps réel.
* Envoyez les **données transactionnelles** à Experience Platform à des fins d’analyse et d’activation.
* Tirez parti de Real-Time CDP, Experience Platform et Adobe Journey Optimizer pour la segmentation, l’orchestration des parcours et la personnalisation.

## Conditions préalables

Avant de connecter [!DNL Capillary] à Adobe Experience Platform, vérifiez que vous disposez des éléments suivants :

* Un **ID d’organisation Adobe valide** et l’accès à un sandbox Experience Platform activé.
* Pour connecter votre compte **[!UICONTROL à Experience Platform]** les autorisations **[!UICONTROL Afficher les sources et]** Gérer les sources[!DNL Capillary] doivent être activées. Contactez votre administrateur de produit pour obtenir les autorisations nécessaires. Pour plus d’informations, consultez le [guide de l’interface utilisateur du contrôle d’accès](../../../access-control/ui/overview.md).

### Créer un schéma

Vous devez créer un schéma de modèle de données d’expérience (XDM) pour décrire un jeu de données pouvant stocker les champs et types de données possibles qui seront envoyés depuis [!DNL Capillary].

1. Connectez-vous à Adobe Experience Platform et accédez à Experience Platform via la connexion de votre organisation.
2. Dans le panneau de navigation de gauche, sélectionnez **[!UICONTROL Schémas]** pour ouvrir l’espace de travail [!UICONTROL Schémas].
3. Sélectionnez **[!UICONTROL Créer un schéma]** dans le coin supérieur droit.
4. Dans la boîte de dialogue Créer un schéma , choisissez entre **[!UICONTROL Création manuelle]** (ajouter vous-même des champs et des groupes de champs) ou **[!UICONTROL création assistée par ML]** (chargez un fichier CSV et utilisez le machine learning pour générer un schéma recommandé).
5. Choisissez une classe de base pour votre schéma (par exemple, XDM Individual Profile, XDM ExperienceEvent ou Autre). Si vous sélectionnez **[!UICONTROL Autre]**, vous pouvez effectuer une sélection parmi les classes personnalisées ou standard disponibles.
6. Saisissez un nom et une description conviviaux pour votre schéma.
7. Utilisez l’éditeur de schémas pour : ajouter des groupes de champs (blocs de champs réutilisables), définir des champs individuels (personnaliser les noms, les types de données et les options) et, éventuellement, créer des types de données ou des groupes de champs personnalisés si les types existants ne répondent pas à vos besoins.
8. Examinez la structure du schéma dans la zone de travail. Sélectionnez **[!UICONTROL Terminer]** pour créer le schéma.
9. (Facultatif) Modifiez des champs, ajoutez des descriptions et ajustez les groupes de champs selon les besoins dans l’éditeur de schémas.

Pour obtenir des instructions détaillées sur la création d’un schéma XDM, consultez le guide sur la [création d’un schéma à l’aide de l’éditeur de schéma](../../../xdm/tutorials/create-schema-ui.md).

### Créer un jeu de données

Ensuite, vous devez créer un jeu de données qui fait référence au schéma que vous venez de créer.

1. Dans l’interface utilisateur d’Experience Platform, sélectionnez [!UICONTROL Jeux de données] dans le volet de navigation de gauche pour ouvrir l’espace de travail [!UICONTROL Jeux de données].
2. Sélectionnez **[!UICONTROL Créer un jeu de données]** en haut à droite.
3. Dans les options de création, sélectionnez **[!UICONTROL Créer un jeu de données à partir d’un schéma]**.
4. Dans la liste, recherchez et sélectionnez le schéma XDM que vous avez précédemment créé. Une fois le schéma localisé, sélectionnez **[!UICONTROL Suivant]**.
5. Saisissez un nom unique et descriptif pour votre jeu de données.
6. Si vous le souhaitez, ajoutez une description qui aidera les futurs utilisateurs à identifier le jeu de données.
7. Sélectionnez **[!UICONTROL Terminer]** pour créer le jeu de données.

Pour obtenir des instructions détaillées sur la création d’un jeu de données, consultez le [guide de l’interface utilisateur des jeux de données](../../../catalog/datasets/user-guide.md).

## Connexion de [!DNL Capillary Streaming Events] à Experience Platform

Une fois la configuration requise pour [!DNL Capillary] terminée, consultez le tutoriel [[!DNL Capillary Streaming Events] IU](../../tutorials/ui/create/loyalty/capillary.md) pour découvrir comment connecter votre compte et diffuser des données de [!DNL Capillary] vers Experience Platform.
