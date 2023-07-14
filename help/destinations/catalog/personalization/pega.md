---
title: Connexion à Pega Customer Decision Hub
description: Utilisez la destination Pega Customer Decision Hub dans Adobe Experience Platform pour envoyer les attributs de profil et les données d’appartenance à l’audience à Pega Customer Decision Hub pour la prise de décision la plus appropriée.
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: 9ccfbeb6ef36b10b8ecbfc25797c26980e7d1dcd
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 25%

---

# Connexion à Pega Customer Decision Hub

## Vue d’ensemble {#overview}

Utilisez la variable [!DNL Pega Customer Decision Hub] destination dans Adobe Experience Platform pour envoyer des attributs de profil et des données d’appartenance à l’audience à [!DNL Pega Customer Decision Hub] pour la prise de décision next-best-action.

Appartenance à l’audience de profil à partir de Adobe Experience Platform, lorsqu’elle est chargée dans [!DNL Pega Customer Decision Hub], peut être utilisé comme prédicteur dans les modèles adaptatifs et aider à fournir les données contextuelles et comportementales appropriées à des fins de prise de décision de la meilleure action suivante.

>[!IMPORTANT]
>
>Cette page de documentation a été créée par Pegasystems. Pour toute demande d&#39;information ou de mise à jour, veuillez contacter directement Pega. [here](mailto:support@pega.com).

## Cas d’utilisation

Pour découvrir les avantages de la destination [!DNL Customer Decision Hub] et son utilisation, consultez les exemples de cas d’utilisation ci-dessous que la clientèle Adobe Experience Platform peut résoudre.

### Télécommunications

Un spécialiste du marketing souhaite exploiter les informations issues des meilleures actions issues d’un modèle de science des données, telles qu’elles sont fournies par [!DNL Pega Customer Decision Hub] pour l’engagement du client. [!DNL Pega Customer Decision Hub] est fortement tributaire de l’intention du client, par exemple &quot;Intéressé_In_5G&quot;, &quot;Intéressé_in_Unlimited_Dataplan&quot; ou &quot;Interest_in_iPhone_accessoires&quot;.

### Services financiers

Un spécialiste du marketing souhaite optimiser les offres destinées aux clients qui se sont inscrits ou se sont désabonnés des newsletters des régimes de retraite ou des régimes de retraite. Les sociétés de services financiers peuvent ingérer plusieurs ID de client à partir de leurs propres CRM dans Adobe Experience Platform, créer des audiences à partir de leurs propres données hors ligne et envoyer des profils qui entrent et sortent des audiences à [!DNL Pega Customer Decision Hub] pour la prise de décision next-best-action (NBA) dans les canaux sortants.

## Conditions préalables {#prerequisites}

Avant d’utiliser cette destination pour exporter des données en dehors de Adobe Experience Platform, assurez-vous de remplir les conditions préalables suivantes dans [!DNL Pega Customer Decision Hub]:

* Configurez la variable [Composant d’intégration Profil Adobe Experience Platform et Appartenance à une audience](https://docs.pega.com/component/customer-decision-hub/adobe-experience-platform-profile-and-segment-membership-integration-component) dans votre [!DNL Pega Customer Decision Hub] instance.
* Configuration d’OAuth 2.0 [Enregistrement du client à l’aide des informations d’identification du client](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) type d’octroi [!DNL Pega Customer Decision Hub] instance.
* Configurer [flux de données d’exécution en temps réel](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) pour le flux de données d’appartenance à une audience Adobe dans votre [!DNL Pega Customer Decision Hub] instance.

## Identités prises en charge {#supported-identities}

[!DNL Pega Customer Decision Hub] prend en charge l’activation des ID utilisateur personnalisés décrits dans le tableau ci-dessous. Pour plus d’informations, voir [identités](/help/identity-service/namespaces.md).

| Identité cible | Description |
|---|---|
| *CustomerID* | Identifiant utilisateur commun qui identifie de manière unique un profil dans [!DNL Pega Customer Decision Hub] et Adobe Experience Platform |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Exporter tous les membres d’une audience avec un identifiant (*CustomerID*), attributs (nom, prénom, emplacement, etc.) et les données d’appartenance à l’audience. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API toujours utilisées. Dès qu&#39;un profil est mis à jour en Experience Platform, sur la base de l&#39;évaluation de l&#39;audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. Pour plus d’informations, voir [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

#### Authentification avec informations d’identification du client OAuth 2 {#oauth-2-client-credentials-authentication}

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination Pega CDH, à l’aide d’OAuth 2 avec authentification des informations d’identification du client.](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Renseignez les champs ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]**:

* **[!UICONTROL URL du jeton d’accès]**: L’URL du jeton d’accès OAuth 2 sur votre [!DNL Pega Customer Decision Hub] instance.
* **[!UICONTROL ID client]**: OAuth 2 [!DNL client ID] que vous avez généré dans votre [!DNL Pega Customer Decision Hub] instance.
* **[!UICONTROL Secret du client]**: OAuth 2 [!DNL client secret] que vous avez généré dans votre [!DNL Pega Customer Decision Hub] instance.

### Renseigner les détails de la destination {#destination-details}

Après avoir établi la connexion d’authentification à la variable [!DNL Pega Customer Decision Hub], fournissez les informations suivantes pour la destination :

![Image de l’écran de l’interface utilisateur affichant les champs remplis pour les détails de destination Pega CDH](../../assets/catalog/personalization/pega/pega-connect-destination.png)

Pour configurer les détails de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Suivant]**.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Nom d’hôte]**: Nom d’hôte Pega Customer Decision Hub vers lequel le profil est exporté en tant que données json.

## Activer les audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Voir [Activation des données d’audience vers des destinations d’exportation de profils en continu](../../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Attributs de destination {#attributes}

Lors de l’étape [[!UICONTROL Sélectionner des attributs]](../../ui/activate-streaming-profile-destinations.md#select-attributes), Adobe recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination.

### Exemple de mappage : activation des mises à jour de profil dans [!DNL Pega Customer Decision Hub] {#mapping-example}

Vous trouverez ci-dessous un exemple de mappage d’identité correct lors de l’exportation de profils vers [!DNL Pega Customer Decision Hub].

Sélection des champs sources :

* Sélectionnez un identifiant (par exemple : CustomerID) comme identité source qui identifie de manière unique un profil dans Adobe Experience Platform et [!DNL Pega Customer Decision Hub].
* Sélectionnez les modifications d’attributs de profil source XDM qui doivent être exportées et mises à jour dans [!DNL Pega Customer Decision Hub].

Sélection des champs cibles :

* Sélectionnez la `CustomerID` espace de noms en tant qu’identité cible.
* Sélectionnez les noms d’attributs de profil de destination qui doivent être mappés aux attributs de profil source XDM correspondants.

![Mappage des identités](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Données exportées / Valider l’exportation des données {#exported-data}

Une mise à jour réussie de l’appartenance à une audience pour un profil insère l’identifiant de l’audience, le nom et les états dans la banque de données de l’appartenance à une audience marketing de Pega. Les données d’appartenance sont associées à un client à l’aide du Concepteur de profil client dans [!DNL Pega Customer Decision Hub], comme illustré ci-dessous.
![Image de l’écran de l’interface utilisateur dans lequel vous pouvez associer des données d’adhésion à l’audience Adobe au client à l’aide du Concepteur de profil client](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

Les données d’appartenance à l’audience sont utilisées dans les stratégies d’engagement de Pega Next-Best-Action Designer pour la prise de décision next-best-action, comme illustré ci-dessous.
![Image de l’écran de l’interface utilisateur où vous pouvez ajouter des champs d’appartenance à l’audience comme conditions dans Stratégies d’engagement de Pega Next-Best-Action Designer](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

Les champs de données d’appartenance de l’audience du client sont ajoutés en tant que prédicteurs dans les modèles adaptatifs, comme illustré ci-dessous.
![Image de l’écran de l’interface utilisateur dans lequel vous pouvez ajouter des champs d’appartenance à l’audience en tant que prédicateurs dans les modèles adaptatifs, à l’aide de Prediction Studio](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Ressources supplémentaires {#additional-resources}

Voir [Configuration d’un enregistrement client OAuth 2.0](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) in [!DNL Pega Customer Decision Hub].

Voir [Création d’une exécution en temps réel pour les flux de données](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) in [!DNL Pega Customer Decision Hub].

Voir [Gestion des enregistrements de client dans Customer Profile Designer](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
