---
title: Connexion HubSpot
description: La destination HubSpot vous permet de gérer les enregistrements de contact dans votre compte HubSpot.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: e2114bde-b7c3-43da-9f3a-919322000ef4
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 29%

---

# Connexion [!DNL HubSpot]

[[!DNL HubSpot]](https://www.hubspot.com) est une plateforme CRM proposant l’ensemble des logiciels, intégrations et ressources dont vous avez besoin pour connecter les services marketing, ventes, gestion de contenu et clientèle. Elle vous permet de connecter vos données, vos équipes et votre clientèle sur une seule et même plateforme CRM.

Cette [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) utilise l’API [[!DNL HubSpot] Contacts](https://developers.hubspot.com/docs/api/crm/contacts) pour mettre à jour les contacts dans [!DNL HubSpot] à partir d’une audience Experience Platform existante après activation.

Les instructions vous permettant de vous authentifier sur votre instance [!DNL HubSpot] sont plus loin dans la section [Authentifier à la destination](#authenticate).

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL HubSpot], consultez l’exemple de cas d’utilisation ci-dessous que les clientes et clients d’Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

[!DNL HubSpot] contacts stockent des informations sur les individus qui interagissent avec votre entreprise. Votre équipe utilise les contacts qui existent dans [!DNL HubSpot] pour créer les audiences Experience Platform. Après avoir envoyé ces audiences à [!DNL HubSpot], leurs informations sont mises à jour et chaque contact se voit attribuer une propriété avec sa valeur comme nom d’audience qui indique à quelle audience appartient le contact.

## Conditions préalables {#prerequisites}

Reportez-vous aux sections ci-dessous pour connaître les conditions préalables à configurer dans Experience Platform et [!DNL HubSpot] et pour obtenir des informations que vous devez rassembler avant d’utiliser la destination [!DNL HubSpot].

### Conditions préalables d’Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer des données dans la destination [!DNL HubSpot], vous devez avoir créé un [schéma](/help/xdm/schema/composition.md), un [jeu de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) et des [audiences](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) dans [!DNL Experience Platform].

Reportez-vous à la documentation Experience Platform pour le [groupe de champs de schéma Détails sur l’appartenance à une audience](/help/xdm/field-groups/profile/segmentation.md) si vous avez besoin de conseils sur les statuts de l’audience.

### Conditions préalables pour la destination [!DNL HubSpot] {#prerequisites-destination}

Notez les conditions préalables suivantes pour exporter des données d’Experience Platform vers votre compte [!DNL HubSpot] :

#### Vous devez disposer d&#39;un compte [!DNL HubSpot] {#prerequisites-account}

Pour exporter des données d’Experience Platform vers votre compte [!DNL Hubspot], vous devez disposer d’un compte [!DNL HubSpot]. Si vous n’en avez pas déjà un, rendez-vous sur la page [Configurer votre compte HubSpot](https://knowledge.hubspot.com/get-started/set-up-your-account) et suivez les conseils pour vous enregistrer et créer votre compte.

#### Collecter le jeton d’accès à l’application privée [!DNL HubSpot] {#gather-credentials}

Vous avez besoin de votre [!DNL HubSpot] `Access token` pour permettre à la destination [!DNL HubSpot] d’effectuer des appels API via votre application privée [!DNL HubSpot] dans votre compte [!DNL HubSpot]. Le `Access token` sert de `Bearer token` lorsque vous [authentifiez la destination](#authenticate).

Si vous ne disposez pas d’une application privée, consultez la documentation pour [ Créer une application privée dans  [!DNL HubSpot]](https://developers.hubspot.com/docs/api/private-apps).

>[!IMPORTANT]
>
> Les portées ci-dessous doivent être attribuées à l’application privée :
> `crm.objects.contacts.write`, `crm.objects.contacts.read`
> `crm.schemas.contacts.write`, `crm.schemas.contacts.read`

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| `Bearer token` | `Access token` de votre application privée [!DNL HubSpot]. <br>Pour obtenir votre [!DNL HubSpot], `Access token` suivre la documentation [!DNL HubSpot] pour [effectuer des appels API avec le jeton d’accès de votre application](https://developers.hubspot.com/docs/api/private-apps#make-api-calls-with-your-app-s-access-token). | `pat-na1-11223344-abcde-12345-9876-1234a1b23456` |

## Mécanismes de sécurisation {#guardrails}

[!DNL HubSpot] applications privées sont soumises à des [limites de taux](https://developers.hubspot.com/docs/api/usage-details). Le nombre d’appels que votre application privée peut effectuer est basé sur votre abonnement au compte [!DNL HubSpot] et sur le fait que vous ayez ou non acheté le module complémentaire API. Reportez-vous également à la section [ Autres limites ](https://developers.hubspot.com/docs/api/usage-details#other-limits).

## Identités prises en charge {#supported-identities}

[!DNL HubSpot] prend en charge la mise à jour des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Exemple | Description | Considérations |
|---|---|---|---|
| `email` | `test@test.com` | Adresse électronique du contact. | Obligatoire |

## Audiences prises en charge {#supported-audiences}

Cette section décrit toutes les audiences que vous pouvez exporter vers cette destination.

Cette destination prend en charge l’activation de toutes les audiences générées par le [Segmentation Service](../../../segmentation/home.md) d’Experience Platform.

Cette destination prend également en charge l’activation des audiences décrites dans le tableau ci-dessous.

| Origine de l’audience | Pris en charge | Description |
|---------|----------|----------|
| [!DNL Segmentation Service] | Oui | Audiences générées via Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Toutes les autres origines d’audience | Oui | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform telles que Adobe Journey Optimizer, </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}



Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects ](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données Adobe Experience Platform. | Rapports, workflows de science des données |

{style="table-layout:auto"}


## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Profile-based]** | <ul><li>Vous exportez tous les membres d’une audience, ainsi que les champs de schéma souhaités *(par exemple : adresse e-mail, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> En outre, une nouvelle propriété est créée dans [!DNL HubSpot] à l’aide du nom de l’audience et sa valeur est définie avec le statut d’audience correspondant d’Experience Platform, pour chacune des audiences sélectionnées.</li></ul> |
| Fréquence des exportations | **[!UICONTROL Streaming]** | <ul><li>Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, recherchez [!DNL HubSpot]. Vous pouvez également localiser cet élément dans la catégorie **[!UICONTROL CRM]** .

### S’authentifier auprès de la destination {#authenticate}

Renseignez les champs obligatoires ci-dessous. Reportez-vous à la section [Collecter le jeton  [!DNL HubSpot] ’accès d’application privée](#gather-credentials) pour obtenir des conseils.

* **[!UICONTROL Bearer token]** : jeton d’accès pour votre application privée [!DNL HubSpot].

Pour vous authentifier auprès de la destination, sélectionnez **[!UICONTROL Connect to destination]**.
![Capture d’écran de l’interface utilisateur d’Experience Platform montrant comment s’authentifier.](../../assets/catalog/crm/hubspot/authenticate-destination.png)

Si les détails fournis sont valides, l’interface utilisateur affiche un statut de **[!UICONTROL Connected]** avec une coche verte. Vous pouvez ensuite passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
![Capture d’écran de l’interface utilisateur d’Experience Platform affichant les détails de la destination.](../../assets/catalog/crm/hubspot/destination-details.png)

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
>
>Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mapper les attributs et les identités {#map}

Pour envoyer correctement vos données d’audience de Adobe Experience Platform vers la destination [!DNL HubSpot], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Experience Platform et leurs équivalents issus de la destination cible.

Pour mapper correctement vos champs XDM vers les champs de destination [!DNL HubSpot], procédez comme suit :

#### Mappage de l’identité `Email`

L’identité `Email` est un mappage obligatoire pour cette destination. Suivez les étapes ci-dessous pour le mapper :

1. À l’étape **[!UICONTROL Mapping]**, sélectionnez **[!UICONTROL Add new mapping]**. Une nouvelle ligne de mappage s’affiche désormais à l’écran.
   ![Capture d’écran de l’interface utilisateur d’Experience Platform avec le bouton Ajouter un nouveau mappage mis en surbrillance.](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. Dans la fenêtre de **[!UICONTROL Select source field]**, choisissez le **[!UICONTROL Select identity namespace]** et sélectionnez une identité.
   ![Capture d’écran de l’interface utilisateur d’Experience Platform sélectionnant l’e-mail comme attribut source à mapper en tant qu’identité.](../../assets/catalog/crm/hubspot/mapping-select-source-identity.png)
1. Dans la fenêtre de **[!UICONTROL Select target field]**, choisissez le **[!UICONTROL Select attributes]** et sélectionnez `email`.
   ![Capture d’écran de l’interface utilisateur d’Experience Platform sélectionnant l’e-mail comme attribut cible à mapper en tant qu’identité.](../../assets/catalog/crm/hubspot/mapping-select-target-identity.png)

| Champ source | Champ cible | Obligatoire |
| --- | --- | --- |
| `IdentityMap: Email` | `Identity: email` | Oui |

Un exemple avec le mappage d’identité est illustré ci-dessous :
![Exemple de capture d’écran de l’interface utilisateur d’Experience Platform avec mappage d’identité d’e-mail.](../../assets/catalog/crm/hubspot/mapping-identities.png)

#### Mappage **facultatif** attributs

Pour ajouter tout autre attribut que vous souhaitez mettre à jour entre votre schéma de profil XDM et votre compte [!DNL HubSpot], répétez les étapes ci-dessous :

1. À l’étape **[!UICONTROL Mapping]**, sélectionnez **[!UICONTROL Add new mapping]**. Une nouvelle ligne de mappage s’affiche désormais à l’écran.
   ![Capture d’écran de l’interface utilisateur d’Experience Platform avec le bouton Ajouter un nouveau mappage mis en surbrillance.](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. Dans la fenêtre **[!UICONTROL Select source field]** , choisissez la catégorie **[!UICONTROL Select attributes]** et sélectionnez l’attribut XDM .
   ![Capture d’écran de l’interface utilisateur d’Experience Platform sélectionnant le prénom en tant qu’attribut source.](../../assets/catalog/crm/hubspot/mapping-select-source-attribute.png)
1. Dans la fenêtre de **[!UICONTROL Select target field]**, choisissez **[!UICONTROL Select attributes]** catégorie et sélectionnez dans la liste des attributs automatiquement renseignés à partir de votre compte [!DNL HubSpot]. La destination utilise l’API [[!DNL HubSpot] Properties](https://developers.hubspot.com/docs/api/crm/properties) pour récupérer ces informations. Les [!DNL HubSpot] [propriétés par défaut](https://knowledge.hubspot.com/contacts/hubspots-default-contact-properties) et les propriétés personnalisées sont récupérées pour être sélectionnées en tant que champs cibles.
   ![Capture d’écran de l’interface utilisateur d’Experience Platform sélectionnant le prénom en tant qu’attribut cible.](../../assets/catalog/crm/hubspot/mapping-select-target-attribute.png)

Voici quelques mappages disponibles entre votre schéma de profil XDM et [!DNL Hubspot] :

| Champ source | Champ cible |
| --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstname` |
| `xdm: person.name.lastName` | `Attribute: lastname` |
| `xdm: workAddress.street1` | `Attribute: address` |
| `xdm: workAddress.city` | `Attribute: city` |
| `xdm: workAddress.country` | `Attribute: country` |

Un exemple d’utilisation de ces mappages d’attributs est illustré ci-dessous :
![Exemple de capture d’écran de l’interface utilisateur d’Experience Platform avec mappages d’attributs.](../../assets/catalog/crm/hubspot/mapping-attributes.png)

Lorsque vous avez terminé de fournir les mappages pour votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Valider l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Connectez-vous au site web [!DNL HubSpot], puis accédez à la page **[!UICONTROL Contacts]** pour vérifier les statuts de l’audience. Cette liste peut être configurée pour afficher des colonnes pour les propriétés personnalisées créées avec le nom de l’audience et dont la valeur est le statut de l’audience.
   Capture d’écran de l’interface utilisateur ![HubSpot) montrant la page Contacts avec des en-têtes de colonne indiquant le nom de l’audience et les cellules des statuts d’audience](../../assets/catalog/crm/hubspot/contacts.png)

1. Vous pouvez également explorer une page de **[!UICONTROL Person]** individuelle et accéder aux propriétés affichant le nom de l’audience et les statuts de l’audience.
   Capture d’écran de l’interface utilisateur ![HubSpot) montrant la page Contact avec des propriétés personnalisées affichant le nom de l’audience et les statuts de l’audience.](../../assets/catalog/crm/hubspot/contact.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Retrouvez d’autres informations utiles de la documentation [!DNL HubSpot] ci-dessous :

* [Méthodes d’authentification sur HubSpot](https://developers.hubspot.com/docs/api/intro-to-auth)
* [!DNL HubSpot] des références d’API pour les API [Contacts](https://developers.hubspot.com/docs/api/crm/contacts) et [Propriétés](https://developers.hubspot.com/docs/api/crm/properties).

### Journal des modifications

Cette section répertorie les nouvelles fonctionnalités et les mises à jour importantes de la documentation consacrée au connecteur de destination.

+++ Afficher le journal des modifications

| Mois de publication | Type de mise à jour | Description |
|---|---|---|
| Septembre 2023 | Version initiale | Publication de la destination initiale et de la documentation. |

{style="table-layout:auto"}

+++
