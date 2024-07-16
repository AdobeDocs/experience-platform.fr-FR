---
title: Connexion à Pega Customer Decision Hub
description: Utilisez la destination Pega Customer Decision Hub dans Adobe Experience Platform pour envoyer les attributs de profil et les données d’appartenance à l’audience à Pega Customer Decision Hub pour la prise de décision la plus appropriée.
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 20%

---

# Connexion à Pega Customer Decision Hub

## Vue d’ensemble {#overview}

Utilisez la destination [!DNL Pega Customer Decision Hub] de Adobe Experience Platform pour envoyer les attributs de profil et les données d’appartenance à l’audience à [!DNL Pega Customer Decision Hub] pour la prise de décision de la meilleure action à venir.

L’appartenance de l’audience de profil à partir de Adobe Experience Platform, lorsqu’elle est chargée dans [!DNL Pega Customer Decision Hub], peut être utilisée comme prédicteur dans les modèles adaptatifs et permet de fournir les données contextuelles et comportementales appropriées à des fins de prise de décision de la meilleure action.

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et conservés par les systèmes Pegasystems. Pour toute demande de mise à jour ou de demande de mise à jour, contactez directement Pega [ici](mailto:support@pega.com).

## Cas d’utilisation

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination [!DNL Customer Decision Hub], voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Télécommunications

Un spécialiste du marketing souhaite tirer parti des informations issues de la prochaine meilleure action basée sur un modèle de science des données, telle qu’elle est fournie par [!DNL Pega Customer Decision Hub] pour l’interaction client. [!DNL Pega Customer Decision Hub] dépend fortement de l’intention du client, par exemple &quot;Intéressé_In_5G&quot;, &quot;Intéressé_in_Unlimited_Dataplan&quot; ou &quot;Interest_in_iPhone_accessoires&quot;.

### Services financiers

Un spécialiste du marketing souhaite optimiser les offres destinées aux clients qui se sont inscrits ou se sont désabonnés des newsletters des régimes de retraite ou des régimes de retraite. Les sociétés de services financiers peuvent ingérer plusieurs ID de client à partir de leurs propres CRM dans Adobe Experience Platform, créer des audiences à partir de leurs propres données hors ligne et envoyer des profils qui entrent et sortent des audiences vers [!DNL Pega Customer Decision Hub] pour la prise de décision de la meilleure action (NBA) dans les canaux sortants.

## Conditions préalables {#prerequisites}

Avant d’utiliser cette destination pour exporter des données en dehors de Adobe Experience Platform, assurez-vous de remplir les conditions préalables suivantes dans [!DNL Pega Customer Decision Hub] :

* Configurez le [composant d’intégration Profil Adobe Experience Platform et Appartenance à une audience](https://docs.pega.com/component/customer-decision-hub/adobe-experience-platform-profile-and-segment-membership-integration-component) dans votre instance [!DNL Pega Customer Decision Hub].
* Configurez le type d&#39;octroi OAuth 2.0 [Enregistrement du client à l&#39;aide des informations d&#39;identification du client](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) dans votre instance [!DNL Pega Customer Decision Hub].
* Configurez le [flux de données d’exécution en temps réel](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) pour le flux de données d’adhésion à l’audience Adobe dans votre instance [!DNL Pega Customer Decision Hub].

## Identités prises en charge {#supported-identities}

[!DNL Pega Customer Decision Hub] prend en charge l’activation des ID utilisateur personnalisés décrits dans le tableau ci-dessous. Pour plus d’informations, voir [identities](/help/identity-service/features/namespaces.md).

| Identité cible | Description |
|---|---|
| *CustomerID* | Identifiant utilisateur commun qui identifie de manière unique un profil dans [!DNL Pega Customer Decision Hub] et Adobe Experience Platform |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Exportez tous les membres d’une audience avec un identifiant (*CustomerID*), des attributs (nom, prénom, emplacement, etc.) et les données d’appartenance à l’audience. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API toujours utilisées. Dès qu&#39;un profil est mis à jour en Experience Platform, sur la base de l&#39;évaluation de l&#39;audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. Pour plus d’informations, voir [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

#### Authentification avec informations d’identification du client OAuth 2 {#oauth-2-client-credentials-authentication}

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination Pega CDH, à l’aide d’OAuth 2 avec authentification des informations d’identification du client](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Renseignez les champs ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]** :

* **[!UICONTROL URL du jeton d’accès]** : URL du jeton d’accès OAuth 2 sur votre instance [!DNL Pega Customer Decision Hub].
* **[!UICONTROL ID client]** : OAuth 2 [!DNL client ID] que vous avez généré dans votre instance [!DNL Pega Customer Decision Hub].
* **[!UICONTROL Client Secret]** : OAuth 2 [!DNL client secret] que vous avez généré dans votre instance [!DNL Pega Customer Decision Hub].

### Renseigner les détails de la destination {#destination-details}

Après avoir établi la connexion d’authentification à [!DNL Pega Customer Decision Hub], fournissez les informations suivantes pour la destination :

![Image de l’écran de l’interface utilisateur affichant les champs remplis pour les détails de destination Pega CDH](../../assets/catalog/personalization/pega/pega-connect-destination.png)

Pour configurer les détails de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Suivant]**.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Nom d’hôte]** : nom d’hôte Pega Customer Decision Hub vers lequel le profil est exporté en tant que données json.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Pour obtenir des instructions sur l’activation des audiences vers cette destination, reportez-vous à la section [Activation des données d’audience vers des destinations d’exportation de profils en continu](../../ui/activate-streaming-profile-destinations.md) .

### Attributs de destination {#attributes}

Lors de l’étape [[!UICONTROL Sélectionner des attributs]](../../ui/activate-streaming-profile-destinations.md#select-attributes), Adobe recommande de sélectionner un identifiant unique dans votre [schéma d’union](../../../profile/home.md#profile-fragments-and-union-schemas). Sélectionnez l’identifiant unique et tout autre champ XDM que vous souhaitez exporter vers la destination.

### Exemple de mappage : activation des mises à jour de profil dans [!DNL Pega Customer Decision Hub] {#mapping-example}

Vous trouverez ci-dessous un exemple de mappage d’identité correct lors de l’exportation de profils vers [!DNL Pega Customer Decision Hub].

Sélection des champs sources :

* Sélectionnez un identifiant (par exemple : CustomerID) comme identité source qui identifie de manière unique un profil dans Adobe Experience Platform et [!DNL Pega Customer Decision Hub].
* Sélectionnez les modifications de l’attribut de profil source XDM qui doivent être exportées et mises à jour dans [!DNL Pega Customer Decision Hub].

Sélection des champs cibles :

* Sélectionnez l’espace de noms `CustomerID` comme identité cible.
* Sélectionnez les noms d’attributs de profil de destination qui doivent être mappés aux attributs de profil source XDM correspondants.

![Mappage d’identités](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Données exportées / Valider l’exportation des données {#exported-data}

Une mise à jour réussie de l’appartenance à une audience pour un profil insère l’identifiant de l’audience, le nom et les états dans la banque de données de l’appartenance à une audience marketing de Pega. Les données d’adhésion sont associées à un client à l’aide de Customer Profile Designer dans [!DNL Pega Customer Decision Hub], comme illustré ci-dessous.
![Image de l’écran de l’interface utilisateur où vous pouvez associer les données d’Adobe de l’appartenance à l’audience au client à l’aide du Designer de profil client](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

Les données d’appartenance à l’audience sont utilisées dans les stratégies d’engagement Designer Pega Next-Best-Action pour la prise de décision next-best-action, comme illustré ci-dessous.
![Image de l’écran de l’interface utilisateur où vous pouvez ajouter des champs d’appartenance à l’audience comme conditions dans Stratégies d’engagement de Pega Next-Best-Action Designer](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

Les champs de données d’appartenance de l’audience du client sont ajoutés en tant que prédicteurs dans les modèles adaptatifs, comme illustré ci-dessous.
![Image de l’écran de l’interface utilisateur où vous pouvez ajouter des champs d’appartenance à l’audience en tant que prédicateurs dans les modèles adaptatifs, à l’aide de Prediction Studio](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Ressources supplémentaires {#additional-resources}

Voir [Configuration d’un enregistrement de client OAuth 2.0](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) dans [!DNL Pega Customer Decision Hub].

Voir [Création d’une exécution en temps réel pour les flux de données](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) dans [!DNL Pega Customer Decision Hub].

Voir [Gestion des enregistrements de client dans Customer Profile Designer](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
