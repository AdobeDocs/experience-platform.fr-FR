---
title: Algolie
description: Utilisez ce connecteur pour activer les audiences en Algérie à des fins de personnalisation et d’utilisation dans les recherches et les recommandations. Vous pouvez ensuite utiliser le connecteur source Profil utilisateur Algolia pour importer les profils dans Real-Time CDP afin de créer des audiences riches.
source-git-commit: 2205ba48a6c17b8f34c4796c1777bfc53a6a7fe5
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 36%

---


# Connexion [!DNL Algolia]

## Présentation {#overview}

>[!IMPORTANT]
>
>Le connecteur de destination [!DNL Algolia] et la page de documentation sont créés et conservés par l’équipe des services d’intégration d’Algolia. Pour toute demande ou information, contactez-les à l’adresse [adobe-algolia-solutions@algolia.com](adobe-algolia-solutions@algolia.com).

Utilisez la connexion de destination [!DNL Algolia] pour envoyer des audiences Adobe Experience Platform en Algérie à des fins de recherche personnalisée et de recommandations. Avant de pouvoir utiliser le connecteur de destination [!DNL Algolia], vous devez d’abord configurer le connecteur source [[!DNL Algolia User Profiles]](/help/sources/connectors/data-partners/algolia-user-profiles.md). Pendant le tutoriel de configuration du connecteur source, vous allez créer l’identité du jeton d’utilisateur Algolia. Cette identité est requise pour le mappage lorsque vous configurez le connecteur de destination.

Ce tutoriel décrit les étapes à suivre pour créer une connexion de destination et un flux de données [!DNL Algolia] à l’aide de l’interface utilisateur de Adobe Experience Platform.

![Le catalogue des destinations avec la destination Algolie.](../../assets/catalog/personalization/algolia/catalog.png)

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Algolia], consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Adobe Experience Platform peut résoudre.

### Cohérence de Personalization {#personalization-consistency}

Utilisez ce connecteur de destination pour offrir une personnalisation cohérente sur l’ensemble de votre site, de la page d’accueil à la recherche.

Par exemple, en tant que spécialiste marketing, vous pouvez créer des audiences enrichies dans Adobe Experience Platform à partir de plusieurs sources de données utilisateur, y compris l’Algérie. Vous pouvez utiliser le connecteur de destination [!DNL Algolia] pour partager les audiences pour les stratégies de ciblage, ce qui permet d’améliorer la personnalisation et la conversion des campagnes.

Pour mettre en œuvre ce cas d’utilisation, vous devez utiliser les connecteurs source [[!DNL Algolia User Profiles]](/help/sources/connectors/data-partners/algolia-user-profiles.md) et de destination [!DNL Algolia].

Commencez par importer vos profils d’utilisateurs [!DNL Algolia] existants dans Adobe Experience Platform Real-Time CDP et d’autres sources pour commencer à créer des audiences riches avec le connecteur source. Les marketeurs créent des audiences à l’aide des données de profil qui peuvent être envoyées à Algolia pour la personnalisation de la recherche et des recommandations.

Ensuite, utilisez le connecteur source [[!DNL Algolia User Profiles]](/help/sources/connectors/data-partners/algolia-user-profiles.md) correspondant pour ingérer et augmenter les profils clients dans Real-Time CDP.

## Conditions préalables {#prerequisites}

>[!IMPORTANT]
>
>* Pour vous connecter à la destination, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

## Identités prises en charge {#supported-identities}

[!DNL Algolia] prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](https://experienceleague.adobe.com/fr/docs/experience-platform/identity/features/namespaces).

| Identité cible | Description | Considérations |
|---------|---------|----------|
| userId | Jeton d’utilisateur [!DNL Algolia] | Sélectionnez cette identité cible pour mapper l’identité source `AlgoliaUserToken` au `userToken` dans la plateforme [!DNL Algolia]. |

{style="table-layout:auto"}

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|---------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | ✓ | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!DNL Audience export]** | Vous exportez tous les profils membres d’une audience ainsi que les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination [!DNL Algolia]. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer et activer les destinations du jeu de données]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL ID de l’application]** : l’ID de l’application [!DNL Algolia] est un identifiant unique attribué à votre compte [!DNL Algolia].
* **[!UICONTROL Clé API]** : la clé API [!DNL Algolia] est une information d’identification utilisée pour authentifier et autoriser les requêtes API aux services de recherche et d’indexation d’[!DNL Algolia].

Pour plus d’informations sur ces informations d’identification, consultez la [!DNL Algolia] [documentation d’authentification](https://www.algolia.com/doc/tools/cli/get-started/authentication/).

![Nouveau compte](../../assets/catalog/personalization/algolia/connection.png)

### Renseigner les détails de la destination

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : renseignez le nom de votre choix pour cette destination.
* **[!UICONTROL Description]** : brève explication de l’objectif de la destination.
* **[!UICONTROL Region]** : les options sont **US** ou **EU**. Sélectionnez la région dans laquelle les données client sont stockées.


![Détails du compte](../../assets/catalog/personalization/algolia/account.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [&#128279;](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des identités, vous devez disposer de l’autorisation de contrôle d’accès Afficher le graphique [d’identités](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions).

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mapper les attributs et les identités {#mapping-attributes-identities}

Au cours de l’étape [!UICONTROL Mappage], vous devez mapper l’identité source AlgoliaUserToken à l’identité cible userId.

![Mappage terminé](../../assets/catalog/personalization/algolia/mapping-complete.png)

## Valider l’exportation des données {#exported-data}

Pour vérifier si l’exportation des audiences vers les profils utilisateur a réussi, vérifiez votre tableau de bord [!DNL Algolia] et accédez à **[!UICONTROL Personalization avancé]** puis cliquez sur **[!UICONTROL Inspecteur d’utilisateur]**. Recherchez un profil utilisateur associé à l’audience Adobe Experience Platform exportée et recherchez-le dans l’Inspecteur d’utilisateur. L’identifiant d’audience s’affiche dans la section de segment.

![Inspecteur des utilisateurs d’Algolie](../../assets/catalog/personalization/algolia/verify-segment-user-profile.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr).

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations, consultez la documentation [!DNL Algolia] suivante :

* [Qu’est-ce qu’Advanced Personalization ?](https://www.algolia.com/doc/guides/personalization/advanced-personalization/what-is-advanced-personalization/)
* [Profils utilisateur](https://www.algolia.com/doc/guides/personalization/advanced-personalization/what-is-advanced-personalization/concepts/user-profiles/)
* [Segmenter les utilisateurs avec des contextes de règle](https://www.algolia.com/doc/guides/personalization/advanced-personalization/implement/guides/segment-users-with-rule-contexts/#assign-a-segment-context-at-query-time)

## Étapes suivantes {#next-steps}

Ce tutoriel vous a permis de créer un flux de données pour exporter des audiences d’Experience Platform vers votre application [!DNL Algolia]. Pour plus d’informations sur la plateforme [!DNL Algolia], consultez la documentation [Algolia](https://www.algolia.com/doc/).