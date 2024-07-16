---
title: Connexion à HubSpot
description: La destination HubSpot vous permet de gérer les enregistrements de contact dans votre compte HubSpot.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: e2114bde-b7c3-43da-9f3a-919322000ef4
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 39%

---

# Connexion [!DNL HubSpot]

[[!DNL HubSpot]](https://www.hubspot.com) est une plateforme CRM proposant l’ensemble des logiciels, intégrations et ressources dont vous avez besoin pour connecter les services marketing, ventes, gestion de contenu et clientèle. Elle vous permet de connecter vos données, vos équipes et votre clientèle sur une seule et même plateforme CRM.

Cette [!DNL Adobe Experience Platform] [destination](/help/destinations/home.md) utilise l’ [[!DNL HubSpot] API Contacts](https://developers.hubspot.com/docs/api/crm/contacts) pour mettre à jour les contacts dans [!DNL HubSpot] d’une audience Experience Platform existante après l’activation.

Les instructions vous permettant de vous authentifier sur votre instance [!DNL HubSpot] sont plus loin dans la section [Authentifier à la destination](#authenticate).

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination [!DNL HubSpot], consultez l’exemple de cas d’utilisation ci-dessous que les clientes et clients d’Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

[!DNL HubSpot] contacts stockent des informations sur les individus qui interagissent avec votre entreprise. Votre équipe utilise les contacts existant dans [!DNL HubSpot] pour créer les audiences Experience Platform. Après l’envoi de ces audiences à [!DNL HubSpot], leurs informations sont mises à jour et chaque contact se voit attribuer une propriété avec sa valeur comme nom d’audience qui indique à quelle audience appartient le contact.

## Conditions préalables {#prerequisites}

Reportez-vous aux sections ci-dessous pour connaître les conditions préalables à configurer dans Experience Platform et [!DNL HubSpot], ainsi que pour obtenir des informations que vous devez rassembler avant de travailler avec la destination [!DNL HubSpot].

### Conditions préalables d’Experience Platform {#prerequisites-in-experience-platform}

Avant d’activer des données vers la destination [!DNL HubSpot], vous devez avoir un [schéma](/help/xdm/schema/composition.md), un [jeu de données](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) et des [audiences](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) créés dans [!DNL Experience Platform].

Reportez-vous à la documentation Experience Platform du [groupe de champs de schéma Détails de l’appartenance à une audience](/help/xdm/field-groups/profile/segmentation.md) si vous avez besoin de conseils sur les états d’audience.

### Conditions préalables pour la destination [!DNL HubSpot] {#prerequisites-destination}

Notez les conditions préalables suivantes pour exporter des données de Platform vers votre compte [!DNL HubSpot] :

#### Vous devez avoir un compte [!DNL HubSpot] {#prerequisites-account}

Pour exporter des données de Platform vers votre compte [!DNL Hubspot], vous devez disposer d’un compte [!DNL HubSpot]. Si vous n’en avez pas déjà un, consultez la page [Configuration de votre compte HubSpot](https://knowledge.hubspot.com/get-started/set-up-your-account) et suivez les instructions pour enregistrer et créer votre compte.

#### Collecte du jeton d’accès de l’application privée [!DNL HubSpot] {#gather-credentials}

Vous avez besoin de votre [!DNL HubSpot] `Access token` pour permettre à la destination [!DNL HubSpot] d&#39;effectuer des appels API via votre application privée [!DNL HubSpot] dans votre compte [!DNL HubSpot]. `Access token` sert de `Bearer token` lorsque vous [ authentifiez la destination](#authenticate).

Si vous ne disposez pas d’une application privée, suivez la documentation de [Création d’une application privée dans [!DNL HubSpot]](https://developers.hubspot.com/docs/api/private-apps).

>[!IMPORTANT]
>
> Les portées ci-dessous doivent être attribuées à l’application privée :
> `crm.objects.contacts.write`, `crm.objects.contacts.read`
> `crm.schemas.contacts.write`, `crm.schemas.contacts.read`

| Informations d’identification | Description | Exemple |
| --- | --- | --- |
| `Bearer token` | `Access token` de votre application privée [!DNL HubSpot]. <br>Pour obtenir votre [!DNL HubSpot] `Access token`, suivez la documentation [!DNL HubSpot] pour [ effectuer des appels API avec le jeton d’accès de votre application ](https://developers.hubspot.com/docs/api/private-apps#make-api-calls-with-your-app-s-access-token). | `pat-na1-11223344-abcde-12345-9876-1234a1b23456` |

## Mécanismes de sécurisation {#guardrails}

[!DNL HubSpot] les applications privées sont soumises aux [limites de taux](https://developers.hubspot.com/docs/api/usage-details). Le nombre d’appels que votre application privée peut effectuer dépend de l’abonnement à votre compte [!DNL HubSpot] et de l’achat ou non du module complémentaire d’API. Reportez-vous également à la section [Autres limites](https://developers.hubspot.com/docs/api/usage-details#other-limits).

## Identités prises en charge {#supported-identities}

[!DNL HubSpot] prend en charge la mise à jour des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Exemple | Description | Considérations |
|---|---|---|---|
| `email` | `test@test.com` | Adresse électronique du contact. | Obligatoire |

## Audiences prises en charge {#supported-audiences}

Cette section décrit toutes les audiences que vous pouvez exporter vers cette destination.

Cette destination prend en charge l’activation de toutes les audiences générées par le [Segmentation Service](../../../segmentation/home.md) d’Experience Platform.

Cette destination prend également en charge l’activation des audiences décrites dans le tableau ci-dessous.

| Type d’audience | Description |
|---------|----------|
| Chargements personnalisés | Audiences [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | <ul><li>Vous exportez tous les membres d’une audience, ainsi que les champs de schéma souhaités *(par exemple : adresse email, numéro de téléphone, nom)*, en fonction de votre mappage de champs.</li><li> En outre, une nouvelle propriété est créée dans [!DNL HubSpot] à l’aide du nom de l’audience et sa valeur est avec le statut d’audience correspondant de Platform, pour chacune des audiences sélectionnées.</li></ul> |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | <ul><li>Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
>
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

Dans **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]**, recherchez [!DNL HubSpot]. Vous pouvez également localiser cet élément dans la catégorie **[!UICONTROL CRM]**.

### S’authentifier auprès de la destination {#authenticate}

Renseignez les champs obligatoires ci-dessous. Pour obtenir des conseils, reportez-vous à la section [Rassembler le  [!DNL HubSpot] jeton d’accès d’application privé](#gather-credentials) .
* **[!UICONTROL Jeton de porteur]** : le jeton d’accès pour votre application privée [!DNL HubSpot].

Pour vous authentifier auprès de la destination, sélectionnez **[!UICONTROL Se connecter à la destination]**.
![Capture d’écran montrant comment s’authentifier sur l’interface utilisateur de Platform.](../../assets/catalog/crm/hubspot/authenticate-destination.png)

Si les détails fournis sont valides, l’interface utilisateur affiche un statut **[!UICONTROL Connecté]** avec une coche verte. Vous pouvez ensuite passer à l’étape suivante.

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.
![Capture d’écran de l’interface utilisateur de Platform montrant les détails de destination.](../../assets/catalog/crm/hubspot/destination-details.png)

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
>
>Pour activer les données, vous avez besoin des ****, **[!UICONTROL Activer les destinations]**, **** et **** [  autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mapper les attributs et les identités {#map}

Pour envoyer correctement les données d’audience de Adobe Experience Platform vers la destination [!DNL HubSpot], vous devez passer par l’étape de mappage des champs. Le mappage consiste à créer un lien entre vos champs de schéma de modèle de données d’expérience (XDM) dans votre compte Platform et leurs équivalents de la destination cible.

Pour mapper correctement vos champs XDM aux champs de destination [!DNL HubSpot], procédez comme suit :

#### Mappage de l’identité `Email`

L’identité `Email` est un mappage obligatoire pour cette destination. Suivez les étapes ci-dessous pour le mapper :
1. Dans l’étape **[!UICONTROL Mappage]**, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**. Vous pouvez désormais voir une nouvelle ligne de mappage sur l’écran.
   ![Copie d’écran de l’interface utilisateur de Platform avec ajout d’un nouveau bouton de mappage surligné.](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. Dans la fenêtre **[!UICONTROL Sélectionner le champ source]** , choisissez l’espace de noms **[!UICONTROL Sélectionner l’identité]** et sélectionnez une identité.
   ![Copie d’écran de l’interface utilisateur de Platform en sélectionnant email comme attribut source à mapper comme identité.](../../assets/catalog/crm/hubspot/mapping-select-source-identity.png)
1. Dans la fenêtre **[!UICONTROL Sélectionner le champ cible]**, choisissez l&#39;option **[!UICONTROL Sélectionner les attributs]** et sélectionnez `email`.
   ![Copie d’écran de l’interface utilisateur de Platform en sélectionnant email comme attribut cible à mapper en tant qu’identité.](../../assets/catalog/crm/hubspot/mapping-select-target-identity.png)

| Champ source | Champ cible | Obligatoire |
| --- | --- | --- |
| `IdentityMap: Email` | `Identity: email` | Oui |

Un exemple de mappage d’identité est illustré ci-dessous :
![Exemple de capture d’écran de l’interface utilisateur de Platform avec mappage d’identité de courrier électronique.](../../assets/catalog/crm/hubspot/mapping-identities.png)

#### Mappage des attributs **optional**

Pour ajouter d’autres attributs que vous souhaitez mettre à jour entre votre schéma de profil XDM et votre compte [!DNL HubSpot], répétez les étapes ci-dessous :
1. Dans l’étape **[!UICONTROL Mappage]**, sélectionnez **[!UICONTROL Ajouter un nouveau mappage]**. Vous pouvez désormais voir une nouvelle ligne de mappage sur l’écran.
   ![Copie d’écran de l’interface utilisateur de Platform avec ajout d’un nouveau bouton de mappage surligné.](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. Dans la fenêtre **[!UICONTROL Sélectionner le champ source]** , choisissez la catégorie **[!UICONTROL Sélectionner les attributs]** et sélectionnez l’attribut XDM.
   ![Copie d’écran de l’interface utilisateur de Platform en sélectionnant Prénom comme attribut source.](../../assets/catalog/crm/hubspot/mapping-select-source-attribute.png)
1. Dans la fenêtre **[!UICONTROL Sélectionner le champ cible]**, choisissez la catégorie **[!UICONTROL Sélectionner les attributs]** et sélectionnez dans la liste des attributs qui sont automatiquement renseignés à partir de votre compte [!DNL HubSpot]. La destination utilise l’API [[!DNL HubSpot] Properties](https://developers.hubspot.com/docs/api/crm/properties) pour récupérer ces informations. Les [!DNL HubSpot] [propriétés par défaut](https://knowledge.hubspot.com/contacts/hubspots-default-contact-properties) et toutes les propriétés personnalisées sont récupérées en vue d’être sélectionnées en tant que champs cibles.
   ![Copie d’écran de l’interface utilisateur de Platform en sélectionnant Prénom comme attribut cible.](../../assets/catalog/crm/hubspot/mapping-select-target-attribute.png)

Voici quelques mappages disponibles entre votre schéma de profil XDM et [!DNL Hubspot] :

| Champ source | Champ cible |
| --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstname` |
| `xdm: person.name.lastName` | `Attribute: lastname` |
| `xdm: workAddress.street1` | `Attribute: address` |
| `xdm: workAddress.city` | `Attribute: city` |
| `xdm: workAddress.country` | `Attribute: country` |

Un exemple utilisant ces mappages d’attributs est illustré ci-dessous :
![Exemple de capture d’écran de l’interface utilisateur de Platform avec mappages d’attributs.](../../assets/catalog/crm/hubspot/mapping-attributes.png)

Lorsque vous avez terminé de fournir les mappages pour votre connexion de destination, sélectionnez **[!UICONTROL Suivant]**.

## Valider l’exportation des données {#exported-data}

Pour vérifier que vous avez correctement configuré la destination, procédez comme suit :

1. Connectez-vous au site web [!DNL HubSpot], puis accédez à la page **[!UICONTROL Contacts]** pour vérifier le statut des audiences. Cette liste peut être configurée pour afficher les colonnes des propriétés personnalisées créées avec le nom de l’audience dont la valeur correspond aux états de l’audience.
   ![ Copie d’écran de l’interface utilisateur HubSpot montrant la page Contacts avec les en-têtes de colonne indiquant le nom de l’audience et les états de l’audience des cellules](../../assets/catalog/crm/hubspot/contacts.png)

1. Vous pouvez également explorer une page **[!UICONTROL Personne]** individuelle et accéder aux propriétés affichant le nom de l’audience et les états de l’audience.
   ![Copie d’écran de l’interface utilisateur de HubSpot présentant la page Contact avec des propriétés personnalisées indiquant le nom de l’audience et le statut de l’audience.](../../assets/catalog/crm/hubspot/contact.png)

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

Vous trouverez ci-dessous d’autres informations utiles à partir de la documentation [!DNL HubSpot] :
* [Méthodes d’authentification sur HubSpot](https://developers.hubspot.com/docs/api/intro-to-auth)
* [!DNL HubSpot] Références d’API pour les API [Contacts](https://developers.hubspot.com/docs/api/crm/contacts) et [Propriétés](https://developers.hubspot.com/docs/api/crm/properties).

### Journal des modifications

Cette section répertorie les nouvelles fonctionnalités et les mises à jour importantes de la documentation consacrée au connecteur de destination.

+++ Afficher le journal des modifications

| Mois de publication | Type de mise à jour | Description |
|---|---|---|
| Septembre 2023 | Version initiale | Version initiale de la destination et publication de la documentation. |

{style="table-layout:auto"}

+++
