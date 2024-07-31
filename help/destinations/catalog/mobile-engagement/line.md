---
keywords: mobile;destinations d’engagement mobile;LINE;destination d’engagement mobile LINE
title: Connexion LINE
description: La destination LINE vous permet d’ajouter des profils à votre audience Platform et de fournir des expériences personnalisées aux utilisateurs connectés.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 42%

---

# Connexion [!DNL LINE]

## Présentation {#overview}

[[!DNL LINE]](https://line.me/en/) est une plate-forme de communication populaire qui connecte les personnes, les services et les informations et est passée d&#39;une application de chat à un hub pour les activités de divertissement, sociales et quotidiennes.

Cette [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) utilise l’ [[!DNL LINE] API de messagerie](https://developers.line.biz/en/reference/messaging-api/). Vous pouvez activer les profils de vos audiences Experience Platform en tant que connexions dans [!DNL LINE] pour répondre aux besoins de votre entreprise.

[!DNL LINE] utilise des jetons porteur comme mécanisme d’authentification pour communiquer avec l’API de messagerie [!DNL LINE]. Les instructions pour vous authentifier à votre instance [!DNL LINE] sont décrites plus loin dans la section [Authentifier à la destination](#authenticate) .

## Cas d’utilisation {#use-cases}

En tant que marketeur, vous pouvez cibler les utilisateurs dans une destination d’engagement mobile, avec des audiences intégrées à [!DNL Adobe Experience Platform]. De plus, vous pouvez leur fournir des expériences personnalisées, en fonction des attributs de leurs profils [!DNL Adobe Experience Platform], dès que les audiences et les profils sont mis à jour dans [!DNL Adobe Experience Platform].

## Conditions préalables {#prerequisites}

### Conditions préalables de [!DNL LINE] {#prerequisites-destination}

Notez les conditions préalables suivantes dans [!DNL LINE], afin d’exporter des données de Platform vers votre compte [!DNL LINE] :

#### Vous devez avoir un compte [!DNL LINE]. {#prerequisites-account}

Vous devez vous enregistrer et créer un compte [!DNL LINE], si ce n&#39;est déjà fait. Pour créer un compte :

1. Accédez à la page [!DNL LINE] [login](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F)
2. Sélectionnez **[!UICONTROL Créer un compte]**.

#### Rassemblez le [!DNL LINE channel access token (long-lived)] à partir de la console de développement [!DNL LINE]. {#gather-credentials}

Pour permettre à Platform d’accéder aux ressources [!DNL LINE], vous aurez besoin de *[!DNL Channel access token (long-lived)]* du canal [!DNL LINE] *API de messagerie* souhaité.

1. Connectez-vous avec votre compte [!DNL LINE] à la [[!DNL LINE] console de développement](https://developers.line.biz/console).
1. Ensuite, accédez à la liste *[!DNL Providers]*, puis sélectionnez le *[!DNL Provider]* ciblé et enfin le canal *API de messagerie* pour accéder à ses paramètres. Si vous accédez à Developer Console pour la première fois, suivez la [[!DNL LINE] documentation](https://developers.line.biz/en/docs/messaging-api/getting-started/) pour accomplir les étapes requises pour créer un fournisseur.
1. Enfin, accédez à la section ***[!DNL Channel access token]*** et copiez la valeur ***[!DNL Channel access token (long-lived)]*** requise à l’étape [Authentifier à la destination](#authenticate) .

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | Votre [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Pour plus d&#39;informations sur la création d&#39;un canal ou l&#39;ajout d&#39;un canal à votre compte [!DNL LINE] existant via la console des développeurs [!DNL LINE], reportez-vous à la [[!DNL LINE] documentation](https://developers.line.biz/en/docs/messaging-api/getting-started/).

## Identités prises en charge {#supported-identities}

[!DNL LINE] prend en charge la mise à jour et l’exportation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description |
|---|---|
| ID pour les annonceurs (IFA) | Sélectionnez l’identifiant pour l’identité cible des annonceurs (IFA) lorsque les identités source sont les espaces de noms IFA *(Apple ID for Advertisers)* ou GAID *(Google Advertising ID). |
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
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, recherchez [!DNL LINE]. Vous pouvez également la localiser sous la catégorie **[!UICONTROL Engagement mobile]**.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, sélectionnez **[!UICONTROL Se connecter à la destination]**.
![Capture d’écran montrant comment s’authentifier sur l’interface utilisateur de Platform.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

Renseignez les champs obligatoires ci-dessous.
* **[!UICONTROL Jeton de porteur]** : votre [!DNL LINE Channel access token (long-lived)] à partir de la console de développement [!DNL LINE]. Reportez-vous à la section [rassembler les informations d’identification](#gather-credentials) .

Si les détails fournis sont valides, l’interface utilisateur affiche un statut **[!UICONTROL Connecté]** avec une coche verte. Vous pouvez ensuite passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
![Capture d’écran de l’interface utilisateur de Platform montrant les détails de destination.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Type d’audience]** : sélectionnez **[!UICONTROL ID for Advertisers(IFAs)]** si les identités que vous souhaitez exporter sont de type *ID for Advertisers(IFAs)*. Sélectionnez **[!UICONTROL ID utilisateur LINE]** si les identités que vous souhaitez exporter sont de type *ID utilisateur LINE*. Pour plus d’informations sur les types d’identité, reportez-vous à la section [Identités prises en charge](#supported-identities) .

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mapper les attributs et les identités {#map}

Pour envoyer correctement vos données d’audience d’Adobe Experience Platform vers la destination [!DNL LINE], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents issus de la destination cible. Pour mapper correctement vos champs XDM vers les champs de destination [!DNL LINE], procédez comme suit :

En fonction de votre identité source, le ou les espaces de noms d’identité cible suivants doivent être mappés :

| Identité cible | Champ source | Champ cible |
| --- | --- | --- |
| ID pour les annonceurs (IFA) | `IDFA` ou `GAID`. | `LineId` |
| ID utilisateur LINE | `UserID` | `LineId` |

Si les identités de votre cible sont *ID utilisateur LINE*, vous aurez besoin des éléments suivants :
![Exemple de capture d’écran de l’interface utilisateur de Platform montrant le mapping de ciblage lors de l’utilisation d’identifiants utilisateur LINE pour les identités cibles.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Si votre identité cible est *ID pour les annonceurs (IFA)*, vous aurez besoin de ce qui suit :
![Exemple de capture d’écran de l’interface utilisateur de Platform montrant le mappage de Target lors de l’utilisation d’un identifiant pour les annonceurs (IFA) pour les identités cibles.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Valider l’exportation des données {#exported-data}

Lors d’une exportation de données réussie hors d’Experience Platform, la destination [!DNL LINE] crée une nouvelle audience dans [!DNL LINE] à l’aide du nom d’audience sélectionné.

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Dans [!DNL LINE], connectez-vous à la [console Manager](https://manager.line.biz/).

1. Ensuite, accédez à **[!UICONTROL Contrôles de données]** > **[!UICONTROL Audiences]** et vérifiez le nom correspondant à l’audience sélectionnée dans la colonne **[!UICONTROL Nom de l’audience]**.

1. Le volume mis à jour correspondrait au nombre dans le segment.

1. La colonne *Type* mentionnera **[!UICONTROL UserID]** si les identités que vous avez exportées sont de type *UserID*. De même, la colonne *Type* mentionnera **[!UICONTROL Identifiant de publicité mobile]** si les identités que vous avez exportées sont de type *IDFA*.

Un exemple de configuration dans [!DNL LINE] est illustré ci-dessous :
![Copie d’écran de l’interface utilisateur LINE indiquant le volume de l’audience.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
