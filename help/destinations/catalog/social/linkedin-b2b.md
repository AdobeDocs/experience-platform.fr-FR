---
title: (Entreprises) Connexion LinkedIn
description: Utilisez cette destination pour activer les audiences de votre compte pour les cas d’utilisation d’Account-Based Marketing (ABM). Activez les profils de vos campagnes LinkedIn pour le ciblage, la personnalisation et la suppression des audiences, en fonction des e-mails hachés.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Édition B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: 68d2cca3-952b-49d0-8ea2-e776a233b752
source-git-commit: e7c0551276d31d6809ace096c00e0dc2665090e6
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 27%

---

# (Entreprises) Connexion LinkedIn Match Audiences {#companies-linkedin}

>[!AVAILABILITY]
>
>La fonctionnalité d’activation des audiences de compte vers la destination LinkedIn (Entreprises) est disponible pour les entreprises qui achètent les éditions [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) et [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) de Real-Time Customer Data Platform.

Utilisez cette destination pour activer vos cas d’utilisation [audiences de compte](/help/segmentation/types/account-audiences.md) pour Account-Based Marketing (ABM). Faites de la publicité pour des rôles et des rôles pertinents dans vos comptes cibles via la destination **[!UICONTROL (Entreprises) LinkedIn]** business-to-business. Consultez la documentation LinkedIn pour [en savoir plus sur le ciblage des comptes](https://business.linkedin.com/marketing-solutions/cx/21/10/ad-targeting/account-targeting) sur la plateforme LinkedIn.

>[!TIP]
>
>Pour les cas d’utilisation au niveau individuel (ou d’entreprise à consommateur), Adobe vous recommande d’utiliser la destination [LinkedIn Matched Audience](/help/destinations/catalog/social/linkedin.md).

![Destination du compte LinkedIn affichée dans l’interface utilisateur d’Experience Platform.](/help/destinations/assets/catalog/social/linkedin-b2b/linkedin-b2b-destination.png)

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | X | Audiences [importées](../../../segmentation/ui/overview.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-and-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|--------------|-----------|---------------------------|
| Type d’exportation | Exportation d’audience | Tous les membres de l’audience seront exportés avec des identifiants clés tels que le nom, le numéro de téléphone, etc. |
| Fréquence | Diffusion en continu | Connexions basées sur l’API « Toujours actives ». Les mises à jour sont envoyées en aval immédiatement après les modifications de profil. |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

Veillez à respecter les conditions préalables ci-dessous afin d’exporter les audiences de compte vers LinkedIn :

### Conditions préalables relatives au compte LinkedIn {#LinkedIn-account-prerequisites}

Avant d’utiliser la destination [!UICONTROL (Entreprises) LinkedIn Matched Audience] , assurez-vous que votre compte [!DNL LinkedIn Campaign Manager] dispose du niveau d’autorisation [!DNL Creative Manager] ou supérieur.

Pour savoir comment modifier vos autorisations d’utilisateur [!DNL LinkedIn Campaign Manager], voir [Ajouter, modifier et supprimer des autorisations d’utilisateur sur les comptes Advertising](https://www.linkedin.com/help/lms/answer/5753) dans la documentation LinkedIn.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’autorisation de contrôle d’accès **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]** [](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

1. Recherchez la destination [!DNL (Companies) LinkedIn Matched Audiences] dans le catalogue de destinations et sélectionnez **[!UICONTROL Configurer]**.
2. Sélectionnez **[!UICONTROL Se connecter à la destination]**.
   ![S’authentifier sur LinkedIn](/help/destinations/assets/catalog/social/linkedin-b2b/authenticate-linkedin-destination.png)
3. Saisissez vos identifiants LinkedIn et sélectionnez **Connexion**.

Après avoir terminé le processus de connexion avec LinkedIn, vous pouvez passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL Identifiant de compte]** : votre [!DNL LinkedIn Campaign Manager Account ID]. Cet identifiant se trouve dans votre compte [!DNL LinkedIn Campaign Manager].

Vous êtes maintenant prêt à activer les audiences de compte sur LinkedIn.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Afficher le graphique d’identités]** [](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences de compte vers les destinations.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences de compte vers les destinations."){width="100" zoomable="yes"}

Lisez [Activer les audiences de compte](/help/destinations/ui/activate-account-audiences.md) pour obtenir des instructions sur l’activation des audiences de compte vers cette destination.

## Paires de mappage requises à l’étape de mappage lors de l’activation des audiences de compte vers la destination **[!UICONTROL (Entreprises) LinkedIn Matched Audiences]** {#required-mappings}

Lors de l’activation des audiences de compte vers la destination **[!UICONTROL (Entreprises) LinkedIn Matched Audiences]** , notez que les deux paires de mappage suivantes sont obligatoires pour exporter des données :

![Mappage LinkedIn des champs obligatoires.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Champ source | Champ cible |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (sélectionnez ce champ dans la vue **[!UICONTROL Sélectionner l’espace de noms d’identité]** lors de la sélection du **[!UICONTROL Champ cible]**). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences de compte vers les destinations.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences de compte vers les destinations."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

## Données exportées {#exported-data}

Une activation réussie signifie qu’une audience personnalisée [!DNL LinkedIn] est créée par programmation dans [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). L’appartenance à l’audience est ajustée à mesure que les utilisateurs sont qualifiés ou disqualifiés pour les audiences activées.
