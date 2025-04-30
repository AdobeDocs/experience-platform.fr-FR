---
title: (V2) Connexion à l’audience en temps réel Pega CDH
description: Utilisez la destination Audience en temps réel de Pega Customer Decision Hub dans Adobe Experience Platform pour envoyer des attributs de profil et des données d'appartenance à l'audience au Pega Customer Decision Hub pour la prise de décision la plus appropriée.
source-git-commit: a51f6bd189bc25018cf25e69fe23bc9f6b3372dd
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 16%

---

# (V2) Connexion à l’audience en temps réel Pega CDH

## Vue d’ensemble {#overview}

Utilisez la destination [!DNL Pega CDH Realtime Audience] (V2) dans Adobe Experience Platform pour envoyer les attributs de profil et les données d’appartenance à l’audience à [!DNL Pega Customer Decision Hub] pour la prise de décision la plus appropriée.

L’appartenance à une audience de profil depuis Adobe Experience Platform, lorsqu’elle est chargée dans [!DNL Pega Customer Decision Hub], peut être utilisée comme prédicteur dans les modèles adaptatifs et contribuer à fournir les données contextuelles et comportementales appropriées pour la prise de décision la plus appropriée.

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par Pegasystems. Pour toute demande ou information, veuillez contacter Pega directement [ici](mailto:support@pega.com).

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL Customer Decision Hub], consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Adobe Experience Platform peut résoudre.

### Télécommunications {#telecommunications}

Un spécialiste marketing souhaite tirer parti des informations issues de la meilleure action basée sur le modèle de science des données fournie par [!DNL Pega Customer Decision Hub] pour l’engagement du client. [!DNL Pega Customer Decision Hub] dépend considérablement de l’intention du client, telle que « Interested_In_5G », « Interested_in_Unlimited_Dataplan » ou « Interest_in_iPhone_accessoires » pour déterminer la prise de décision de meilleure action suivante (NBA) dans les canaux sortants.

### Services financiers {#financial-services}

Un spécialiste du marketing souhaite optimiser les offres pour les clients qui se sont inscrits ou désinscrits à des bulletins d’information sur un régime de retraite ou un régime de retraite. Les sociétés de services financiers peuvent ingérer plusieurs ID de client de leurs propres CRM dans Adobe Experience Platform, créer des audiences à partir de leurs propres données hors ligne et envoyer des profils qui entrent dans les audiences et en sortent pour [!DNL Pega Customer Decision Hub] la prise de décision de meilleure action (NBA) dans les canaux sortants.

## Prérequis {#prerequisites}

Avant de pouvoir utiliser cette destination pour exporter des données en dehors de Adobe Experience Platform, veillez à remplir les conditions préalables suivantes en [!DNL Pega Customer Decision Hub] :

* Configurez le composant d’intégration Profil Adobe Experience Platform et Appartenance à une audience [](https://docs.pega.com/bundle/components/page/customer-decision-hub/components/adobe-membership-component.html) dans votre instance [!DNL Pega Customer Decision Hub].
* Configurez OAuth 2.0 [Enregistrement du client à l’aide des informations d’identification client](https://docs.pega.com/bundle/platform/page/platform/security/configure-oauth-2-client-registration.html) type d’octroi dans votre instance [!DNL Pega Customer Decision Hub].
* Configurez le [flux de données d’exécution en temps réel](https://docs.pega.com/bundle/platform/page/platform/decision-management/data-flow-run-real-time-create.html) pour le flux de données d’appartenance à une audience Adobe dans votre instance de [!DNL Pega Customer Decision Hub].

## Identités prises en charge {#supported-identities}

[!DNL Pega Customer Decision Hub] prend en charge l’activation des ID utilisateur personnalisés décrits dans le tableau ci-dessous. Pour plus d’informations, voir [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| `CustomerID` | Identifiant client | Identifiant utilisateur commun qui identifie de manière unique un profil dans [!DNL Pega Customer Decision Hub] et Adobe Experience Platform. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Exportez tous les membres d’une audience avec un identifiant (*CustomerID*), des attributs (nom, prénom, emplacement, etc.) et des données d’appartenance à l’audience. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API toujours actives. Dès qu’un profil est mis à jour dans Experience Platform, en fonction de l’évaluation de l’audience, le connecteur envoie la mise à jour en aval vers la plateforme de destination. Pour plus d’informations, voir [Destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

#### Authentification avec informations d’identification du client OAuth 2 {#oauth-2-client-credentials-authentication}

![Image de l’écran de l’interface utilisateur où vous pouvez vous connecter à la destination Pega CDH, à l’aide d’OAuth 2 avec authentification par informations d’identification du client](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Renseignez les champs ci-dessous et sélectionnez **[!UICONTROL Se connecter à la destination]** :

* **[!UICONTROL URL du jeton d’accès]** : URL du jeton d’accès OAuth 2 sur votre instance [!DNL Pega Customer Decision Hub].
* **[!UICONTROL ID client]** : [!DNL client ID] OAuth 2 que vous avez généré dans votre instance [!DNL Pega Customer Decision Hub].
* **[!UICONTROL Secret client]** : [!DNL client secret] OAuth 2 que vous avez généré dans votre instance [!DNL Pega Customer Decision Hub].

### Renseigner les détails de la destination {#destination-details}

Après avoir établi la connexion d’authentification au [!DNL Pega Customer Decision Hub], fournissez les informations suivantes pour la destination :

![Image de l’écran de l’interface utilisateur affichant les champs remplis pour les détails de destination Pega CDH](../../assets/catalog/personalization/pega/pega-connect-destination-v2.png)

Pour configurer les détails de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Suivant]**.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Nom d’hôte CDH Pega]** : nom d’hôte du Pega Customer Decision Hub vers lequel le profil est exporté en tant que données JSON.
* **[!UICONTROL Alias de l’application]** : alias de l’application que vous avez configuré pour votre compte Customer Decision Hub. Pour plus d’informations, voir [Ajout d’un alias d’URL d’application](https://docs.pega.com/bundle/platform/page/platform/user-experience/adding-application-url-alias.html) dans votre instance [!DNL Pega Customer Decision Hub].

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez [ Activer les données d’audience vers des destinations d’exportation de profil de diffusion en continu ](../../ui/activate-streaming-profile-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mappage {#mapping}

À l’étape [!UICONTROL Mappage], sélectionnez un identifiant unique dans votre schéma d’union et tout autre champ XDM que vous souhaitez exporter vers la destination.

### Exemple de mappage : activation des mises à jour de profil dans [!DNL Pega Customer Decision Hub] {#mapping-example}

Vous trouverez ci-dessous un exemple de mappage d’identité correct lors de l’exportation de profils vers [!DNL Pega Customer Decision Hub].

* Sélectionnez une identité source qui identifie de manière unique un profil dans Adobe Experience Platform et [!DNL Pega Customer Decision Hub]. Par exemple : `CustomerID`.
* Sélectionnez les attributs de profil de destination auxquels vous souhaitez mapper les attributs de profil source sélectionnés.

![Mappage d’identité](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Données exportées / Valider l’exportation des données {#exported-data}

Une mise à jour réussie de l’appartenance à une audience pour un profil insérerait l’identifiant de l’audience, son nom et ses statuts dans le magasin de données d’appartenance à une audience marketing Pega. Les données d’abonnement sont associées à un client à l’aide de Designer du profil client dans [!DNL Pega Customer Decision Hub], comme illustré ci-dessous.

![Image de l’écran de l’interface utilisateur où vous pouvez associer les données d’appartenance à une audience Adobe au client, à l’aide de Customer Profile Designer](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

Les données d’appartenance à l’audience sont utilisées dans les politiques d’engagement Designer Pega Next-Best-Action pour la prise de décision next-best-action, comme illustré ci-dessous.

![Image de l’écran de l’interface utilisateur où vous pouvez ajouter des champs d’appartenance à l’audience en tant que conditions dans les politiques d’engagement du Designer Next-Best-Action de Pega](../../assets/catalog/personalization/pega/pega-profile-designer-engagement.png)

Les champs de données Abonnement de l’audience client sont ajoutés comme prédicteurs dans les modèles adaptatifs, comme illustré ci-dessous.

![Image de l’écran de l’interface utilisateur où vous pouvez ajouter des champs d’appartenance à l’audience en tant que prédicateurs dans les modèles adaptatifs, à l’aide de Prediction Studio](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations, consultez la documentation [!DNL Pega] suivante :

* [Configuration d’un enregistrement client OAuth 2.0](https://docs.pega.com/bundle/platform/page/platform/security/configure-oauth-2-client-registration.html)
* [Création d’une exécution en temps réel pour les flux de données](https://docs.pega.com/bundle/platform/page/platform/decision-management/data-flow-run-real-time-create.html)
* [Gérer les enregistrements de clients dans le Designer du profil client](https://docs.pega.com/bundle/customer-decision-hub/page/customer-decision-hub/implement/profile-designer-data-management.html)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
