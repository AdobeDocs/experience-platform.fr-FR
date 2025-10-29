---
title: Connexion Bombora
description: Activez les profils de vos campagnes Bombora pour le ciblage, la personnalisation et la suppression des audiences, en fonction des audiences du compte.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=fr#rtcdp-editions newtab=true"
badgeB2P: label="Édition B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=fr#rtcdp-editions newtab=true"
exl-id: a2f8e399-e192-4104-876a-fe60f8403143
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 25%

---

# Connexion Bombora {#bombora}

>[!AVAILABILITY]
>
>La fonctionnalité d’activation des audiences de compte vers la destination Bombora est disponible pour les sociétés qui achètent les éditions [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) et [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) de Real-Time Customer Data Platform.

Activez les profils de vos campagnes Bombora pour le ciblage, la personnalisation et la suppression des audiences, en fonction des [&#x200B; audiences de compte &#x200B;](/help/segmentation/types/account-audiences.md).

## Cas d’utilisation {#use-case}

Pour mieux comprendre quand et comment utiliser la destination Bombora, consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Adobe Experience Platform peut résoudre.

### Intégration de DSP {#dsp-integration}

En tant que spécialiste marketing B2B, vous pouvez créer une liste de comptes dans Real-time CDP, identifier les sociétés qui affichent une forte intention pour vos produits, puis utiliser cette destination pour activer cette liste dans Bombora.

Grâce à l’intégration de Bombora aux DSP, vous pouvez exécuter des campagnes publicitaires ciblées à l’aide des données de Bombora. Cela garantit que vos dépenses publicitaires sont axées sur les entreprises les plus susceptibles de convertir leur contenu.

### Account-Based Marketing {#abm}

En tant que spécialiste marketing B2B, vous pouvez créer une liste de comptes basée sur des signaux CRM et marketing. Ensuite, vous pouvez utiliser cette destination pour activer cette liste à Bombora, où les contrôles basés sur la gestion des actifs bancaires vous aident à cibler les décideurs de ces sociétés.

### Activation marketing basée sur un compte multicanal {#multi-channel-abm}

En tant que spécialiste marketing B2B, vous pouvez créer une liste de comptes dans Real-time CDP, identifiant les entreprises à forte intention. Ensuite, vous pouvez utiliser cette destination pour activer la liste dans Bombora afin d’exécuter des campagnes ciblées sur plusieurs canaux.

Sur les médias sociaux payants, vous pouvez diffuser des annonces personnalisées aux professionnels sur des comptes cibles sur des plateformes telles que [!DNL LinkedIn] et [!DNL Facebook]. En utilisant des plateformes publicitaires natives, vous pouvez vous assurer que le contenu parvient aux décideurs appropriés.

Vous pouvez également étendre les campagnes à la télévision avancée, en diffusant des annonces sur des comptes clés.

Cette approche multicanal garantit la cohérence des messages sur toutes les plateformes, en maximisant les taux d’engagement et de conversion.

## Audiences prises en charge {#supported-audiences}

Cette section décrit le type d’audiences que vous pouvez exporter vers cette destination.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Chargements personnalisés | X | Audiences [importées](../../../segmentation/ui/overview.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Identités prises en charge {#supported-identities}

Bombora nécessite le mappage de l’identité cible décrite dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description |
|---|---|
| `primaryId` | Bombora nécessite le mappage de cette identité cible pour que l’intégration fonctionne correctement. Vous pouvez mapper n’importe quel champ source à cette identité. Ce mappage est obligatoire mais n’exporte pas les données vers Bombora. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-and-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Audience export]** | Vous exportez tous les profils membres d’une audience ainsi que les identifiants (nom, numéro de téléphone ou autres) utilisés dans la destination [!DNL Bombora]. |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Conditions préalables {#prerequisites}

Pour exporter des audiences de compte vers Bombora, vous avez besoin des informations suivantes.

1. Un compte Bombora.
2. Un **[!UICONTROL client ID]** et un **[!UICONTROL client secret]** Bombora.

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des autorisations **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Connect to destination]**.

![Ajouter un jeton porteur](../../assets/catalog/advertising/bombora/add-bearer-token.png)

* **[!UICONTROL Client ID]** : saisissez votre identifiant client [!DNL Bombora].
* **[!UICONTROL Client secret]** : saisissez votre secret client [!DNL Bombora].

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

![Ajouter des informations sur la connexion de destination](../..//assets/catalog/advertising/bombora/name-and-description.png)

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

Vous êtes maintenant prêt à activer vos audiences dans Bombora.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**&#x200B;[&#128279;](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Lisez [Activer les audiences de compte](/help/destinations/ui/activate-account-audiences.md) pour obtenir des instructions sur l’activation des audiences de compte vers cette destination.

### Mappages obligatoires {#mapping}

La destination Bombora nécessite que vous configuriez les mappages suivants pour une activation réussie des données.



| Champ source | Champ cible | Description |
|---------|----------|---------|
| Toute valeur | `Identity: primaryId` | Ce mappage est obligatoire pour qu’Experience Platform établisse une connexion à Bombora. Cette valeur n’est pas exportée vers Bombora, mais elle est requise pour la configuration de destination. Vous pouvez sélectionner n’importe quel attribut pour le champ source. |
| `xdm: accountOrganization.domain` | `xdm: companyWebsiteDomain` | Bombora utilise des adresses de sites Web ou de domaines pour créer une liste de comptes. |

![Ajouter des mappages obligatoires](../..//assets/catalog/advertising/bombora/mappings.png)


## Notes supplémentaires et légendes importantes {#additional-notes}

Si une audience de compte du même nom a été activée précédemment pour Bombora, vous recevrez une erreur si vous essayez de l’activer à nouveau par le biais d’un autre flux de données vers la destination Bombora.
