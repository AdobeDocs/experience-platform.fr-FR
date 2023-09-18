---
keywords: mobile;destinations d’engagement mobile;LINE;destination d’engagement mobile LINE
title: Connexion LINE
description: La destination LINE vous permet d’ajouter des profils à votre audience Platform et de fournir des expériences personnalisées aux utilisateurs connectés.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 46%

---

# Connexion [!DNL LINE]

## Présentation {#overview}

[[!DNL LINE]](https://line.me/en/) est une plateforme de communication populaire qui connecte les personnes, les services et l’information et est passée d’une application de chat à un centre de divertissement, social et d’activités quotidiennes.

Ceci [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) tire parti de la fonction [[!DNL LINE] API de messagerie](https://developers.line.biz/en/reference/messaging-api/). Vous pouvez activer les profils de vos audiences Experience Platform en tant que connexions dans [!DNL LINE] pour les besoins de votre entreprise.

[!DNL LINE] utilise les jetons du porteur comme mécanisme d’authentification pour communiquer avec [!DNL LINE] API de messagerie. Instructions pour vous authentifier à votre [!DNL LINE] L’instance est plus loin, dans [Authentification à la destination](#authenticate) .

## Cas d’utilisation {#use-cases}

En tant que marketeur, vous pouvez cibler les utilisateurs dans une destination d’engagement mobile, avec des audiences intégrées [!DNL Adobe Experience Platform]. De plus, vous pouvez leur proposer des expériences personnalisées, en fonction des attributs de leur [!DNL Adobe Experience Platform] profils, dès que les audiences et les profils sont mis à jour dans [!DNL Adobe Experience Platform].

## Conditions préalables {#prerequisites}

### Conditions préalables de [!DNL LINE] {#prerequisites-destination}

Notez les conditions préalables suivantes dans [!DNL LINE], afin d’exporter des données de Platform vers votre compte [!DNL LINE] :

#### Vous devez avoir un compte [!DNL LINE]. {#prerequisites-account}

Vous devez vous enregistrer et créer une [!DNL LINE] , si vous n’en avez pas déjà un. Pour créer un compte :

1. Accédez au [!DNL LINE] [connexion au compte](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) page
2. Sélectionner **[!UICONTROL Créer un compte]**.

#### Rassemblez les [!DNL LINE channel access token (long-lived)] de la [!DNL LINE] console de développement {#gather-credentials}

Pour autoriser Platform à accéder à [!DNL LINE] , vous aurez besoin de la fonction *[!DNL Channel access token (long-lived)]* de la [!DNL LINE] *API de messagerie* canal.

1. Connectez-vous avec votre [!DNL LINE] au compte [[!DNL LINE] Developer Console](https://developers.line.biz/console).
1. Ensuite, accédez au *[!DNL Providers]* , puis sélectionnez la variable *[!DNL Provider]* d’intérêt et sélectionnez enfin la variable *API de messagerie* pour accéder à ses paramètres. Si vous accédez à la console de développement pour la première fois, suivez la [[!DNL LINE] documentation](https://developers.line.biz/en/docs/messaging-api/getting-started/) pour effectuer les étapes requises pour créer un fournisseur.
1. Enfin, accédez au ***[!DNL Channel access token]*** et copiez le fichier ***[!DNL Channel access token (long-lived)]*** valeur requise dans [Authentification à la destination](#authenticate) étape .

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | Votre [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Voir [[!DNL LINE] documentation](https://developers.line.biz/en/docs/messaging-api/getting-started/) pour obtenir des conseils sur la création d’un canal ou l’ajout d’un canal à votre [!DNL LINE] compte par le biais de [!DNL LINE] console développeurs.

## Identités prises en charge {#supported-identities}

[!DNL LINE] prend en charge la mise à jour et l’exportation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/namespaces.md).

| Identité cible | Description |
|---|---|
| ID pour les annonceurs (IFA) | Sélectionnez l’identifiant de l’identité cible des annonceurs (IFA) lorsque les identités source sont IFA *(Apple ID pour les annonceurs)* ou les espaces de noms GAID *(Google Advertising ID). |
| ID utilisateur LINE | Sélectionnez l’identité cible UserID lorsque les identités source sont des identifiants utilisateur LINE. |

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les profils membres d’une audience ainsi que les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination [!DNL LINE]. |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous devez disposer de l’[autorisation de contrôle d’accès](/help/access-control/home.md#permissions) **[!UICONTROL Gérer les destinations]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, recherchez [!DNL LINE]. Vous pouvez également la localiser sous le **[!UICONTROL Engagement mobile]** catégorie.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, sélectionnez **[!UICONTROL Se connecter à la destination]**.
![Capture d’écran montrant comment s’authentifier sur l’interface utilisateur de Platform.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

Renseignez les champs obligatoires ci-dessous.
* **[!UICONTROL Jeton de porteur]**: votre [!DNL LINE Channel access token (long-lived)] de la [!DNL LINE] console de développement. Voir [informations d’identification](#gather-credentials) .

Si les détails fournis sont valides, l’interface utilisateur affiche un statut **[!UICONTROL Connecté]** avec une coche verte. Vous pouvez ensuite passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
![Capture d’écran de l’interface utilisateur de Platform montrant les détails de destination.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Type d’audience]**: sélectionnez **[!UICONTROL ID pour les annonceurs (IFA)]** si les identités que vous souhaitez exporter sont de type *ID pour les annonceurs (IFA)*. Sélectionner **[!UICONTROL ID utilisateur LINE]** si les identités que vous souhaitez exporter sont de type *ID utilisateur LINE*. Voir [Identités prises en charge](#supported-identities) pour plus d’informations sur les types d’identité.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des [autorisations de contrôle d’accès](/help/access-control/home.md#permissions) pour les fonctions **[!UICONTROL Gérer les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Afficher les segments]**. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.
>* Pour exporter *identités*, vous avez besoin de la fonction **[!UICONTROL Affichage du graphique des identités]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mapper les attributs et les identités {#map}

Pour envoyer correctement vos données d’audience d’Adobe Experience Platform vers la destination [!DNL LINE], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents issus de la destination cible. Pour mapper correctement vos champs XDM vers les champs de destination [!DNL LINE], procédez comme suit :

En fonction de votre identité source, le ou les espaces de noms d’identité cible suivants doivent être mappés : | Identité cible | Champ source | Champ cible | | — | — | — | | ID pour les annonceurs (IFA) | `IDFA` ou `GAID` | `LineId` | | ID utilisateur LINE | `UserID` | `LineId` |

Si vos identités cibles sont *ID utilisateur LINE* vous aurez besoin des éléments suivants :
![Exemple de capture d’écran de l’interface utilisateur de Platform montrant le mapping de ciblage lors de l’utilisation d’identifiants utilisateur LINE pour les identités cibles.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Si votre identité cible est *ID pour les annonceurs (IFA)* vous aurez besoin des éléments suivants :
![Exemple de capture d’écran de l’interface utilisateur de Platform montrant le mappage de Target lors de l’utilisation d’un identifiant pour les annonceurs (IFA) pour les identités cibles.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Valider l’exportation des données {#exported-data}

Si l’exportation des données est réussie hors de l’Experience Platform, la variable [!DNL LINE] la destination crée une nouvelle audience dans [!DNL LINE] à l’aide du nom de l’audience sélectionnée.

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Dans [!DNL LINE], connectez-vous au [Console de gestion](https://manager.line.biz/).

1. Ensuite, accédez à **[!UICONTROL Contrôles de données]** > **[!UICONTROL Audiences]** et vérifiez le nom correspondant à l’audience sélectionnée dans la fonction **[!UICONTROL Nom de l’audience]** colonne .

1. Le volume mis à jour correspondrait au nombre dans le segment.

1. La variable *Type* column est mentionné **[!UICONTROL UserID]** si les identités que vous avez exportées sont de type *UserID*. De même, la variable *Type* column est mentionné **[!UICONTROL Identifiant de publicité mobile]** si les identités que vous avez exportées sont de type *IDFA*.

Exemple de configuration dans [!DNL LINE] est illustré ci-dessous :
![Capture d’écran de l’interface utilisateur LINE indiquant le volume de l’audience.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
