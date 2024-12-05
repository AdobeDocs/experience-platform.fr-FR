---
title: (Sociétés) Connexion LinkedIn
description: Utilisez cette destination pour activer les audiences de votre compte pour les cas d’utilisation d’Account-Based Marketing (ABM). Activez les profils de vos campagnes LinkedIn pour le ciblage, la personnalisation et la suppression des audiences, en fonction des courriers électroniques hachés.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Édition B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
source-git-commit: e45c50a6447be4a60145eea6956d30d51166e675
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 27%

---

# (Sociétés) Connexion LinkedIn Match Audiences {#companies-linkedin}

>[!AVAILABILITY]
>
>La fonctionnalité d’activation des audiences de compte vers la destination LinkedIn (Entreprises) est disponible pour les entreprises qui achètent les éditions [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) et [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) de Real-Time Customer Data Platform.

Utilisez cette destination pour activer vos [audiences de compte](/help/segmentation/ui/account-audiences.md) pour les cas d’utilisation de Account-Based Marketing (ABM). Annoncez les rôles et les personnalités appropriés dans vos comptes cibles via la destination **[!UICONTROL (Entreprises) LinkedIn]** de commerce à entreprise. Consultez la documentation de LinkedIn pour [en savoir plus sur le ciblage de compte](https://business.linkedin.com/marketing-solutions/cx/21/10/ad-targeting/account-targeting) sur la plateforme LinkedIn.

>[!TIP]
>
>Pour les cas d’utilisation au niveau individuel (ou entre l’entreprise et le consommateur), Adobe vous recommande d’utiliser la destination [Audience mise en correspondance LinkedIn](/help/destinations/catalog/social/linkedin.md).

![Destination du compte LinkedIn affichée dans l’interface utilisateur de l’Experience Platform.](/help/destinations/assets/catalog/social/linkedin-b2b/linkedin-b2b-destination.png)

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées par l’Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | X | Audiences [importées](../../../segmentation/ui/overview.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-and-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|--------------|-----------|---------------------------|
| Type d’exportation | Exportation de l’audience | Tous les membres de l’audience seront exportés avec des identifiants clés tels que le nom, le numéro de téléphone, etc. |
| Fréquence | Diffusion en continu | Connexions basées sur des API toujours actives. Les mises à jour sont envoyées immédiatement en aval après les modifications de profil. |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

Veillez à respecter les conditions préalables ci-dessous pour exporter les audiences de compte vers LinkedIn :

### Conditions préalables au compte linkedIn {#LinkedIn-account-prerequisites}

Avant de pouvoir utiliser la destination [!UICONTROL (Entreprises) Audience mappée LinkedIn ], assurez-vous que votre compte [!DNL LinkedIn Campaign Manager] a le niveau d’autorisation [!DNL Creative Manager] ou plus.

Pour savoir comment modifier vos autorisations d’utilisateur [!DNL LinkedIn Campaign Manager], voir [Ajout, modification et suppression d’autorisations d’utilisateur sur des comptes Advertising](https://www.linkedin.com/help/lms/answer/5753) dans la documentation LinkedIn.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’autorisation de **[!UICONTROL Affichage des destinations]** et de **[!UICONTROL Gestion des destinations]** [contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

1. Recherchez la destination [!DNL (Companies) LinkedIn Matched Audiences] dans le catalogue de destination et sélectionnez **[!UICONTROL Configurer]**.
2. Sélectionnez **[!UICONTROL Se connecter à la destination]**.
   ![Authentification à LinkedIn](/help/destinations/assets/catalog/social/linkedin-b2b/authenticate-linkedin-destination.png)
3. Saisissez vos informations d’identification LinkedIn et sélectionnez **Log In**.

Après avoir terminé le processus de connexion avec LinkedIn, vous pouvez passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL ID de compte]** : votre [!DNL LinkedIn Campaign Manager Account ID]. Vous pouvez trouver cet identifiant dans votre compte [!DNL LinkedIn Campaign Manager].

Vous êtes maintenant prêt à activer les audiences de compte vers LinkedIn.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous avez besoin de l&#39;autorisation **[!UICONTROL Afficher le graphique d&#39;identités]** [ ](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences du compte vers les destinations.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences du compte vers les destinations."){width="100" zoomable="yes"}

Lisez [Activer les audiences de compte](/help/destinations/ui/activate-account-audiences.md) pour obtenir des instructions sur l’activation des audiences de compte vers cette destination.

## Paires de mappage requises à l’étape de mappage lors de l’activation des audiences de compte vers la destination **[!UICONTROL (Sociétés) LinkedIn Matched Audiences]** {#required-mappings}

Lors de l’activation des audiences de compte vers la destination **[!UICONTROL (Entreprises) Audiences mappées LinkedIn]**, notez que les deux paires de mappage suivantes sont obligatoires pour exporter les données avec succès :

![Le mappage LinkedIn nécessite des champs.](/help/destinations/assets/ui/activate-account-audiences/linkedin-mapping-required-fields.png)

| Champ source | Champ cible |
|---------|----------|
| `accountName` | `companyName` |
| `accountKey.sourceKey` | `primaryId` (sélectionnez ce champ dans la vue **[!UICONTROL Sélectionner l’espace de noms d’identité]**, lors de la sélection du **[!UICONTROL champ cible]**). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences du compte vers les destinations.](/help/destinations/assets/ui/activate-account-audiences/identity-namespace-highlighted.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences du compte vers les destinations."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

## Données exportées {#exported-data}

Une activation réussie signifie qu’une audience personnalisée [!DNL LinkedIn] est créée par programmation dans [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). L’appartenance à l’audience est ajustée lorsque les utilisateurs sont qualifiés ou disqualifiés pour les audiences activées.