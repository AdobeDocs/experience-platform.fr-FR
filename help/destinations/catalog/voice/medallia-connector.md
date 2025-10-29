---
title: Connexion à Medallia
description: Activez les profils pour les enquêtes et la collecte de commentaires Medallia ciblées afin de mieux comprendre les besoins et les attentes des clients.
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 29%

---

# Connexion à Medallia

## Vue d’ensemble {#overview}

Activez les profils pour les enquêtes et la collecte de commentaires Medallia ciblées afin de mieux comprendre les besoins et les attentes des clients.

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et conservés par l’équipe Medallia. Pour toute demande ou information, contactez directement l&#39;équipe à l&#39;adresse adobe-integrations@medallia.com.

## Cas d’utilisation {#use-cases}

Pour mieux comprendre quand et comment utiliser la destination Medallia, consultez les exemples de cas d’utilisation ci-dessous que la clientèle de Adobe Experience Platform peut résoudre.

### Cas d’utilisation #1

Une marque B2B souhaite évaluer et rationaliser son programme d’intégration. Ils souhaitent envoyer des questionnaires personnalisés en temps réel aux clients qui viennent de terminer le processus d’intégration.

### Cas d’utilisation #2

Un retailer cherche à mieux comprendre les préférences des clients en matière d’exécution des commandes. Ils souhaitent envoyer un court questionnaire par SMS en une seule question aux clients qui ont effectué des achats en ligne et en magasin au cours du dernier mois.

## Conditions préalables {#prerequisites}

Les informations suivantes sont nécessaires pour établir la connexion Medallia :

* **URL du point d’entrée du jeton OAuth**
* **Identifiant du client**
* **Secret du client**
* **URL de passerelle API**
* **Nom de l’API d’importation**

Contactez votre équipe de diffusion Medallia pour obtenir ces détails.

## Identités prises en charge {#supported-identities}

Medallia prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| e-mail | Adresse e-mail | Sélectionnez l’identité cible de l’e-mail lorsque vous souhaitez envoyer des questionnaires d’invitation par e-mail. Lorsqu’un profil est associé à plusieurs adresses e-mail, Medallia déclenche uniquement l’invitation au premier e-mail. |
| phone | Numéros de téléphone hachés au format E.164 | Sélectionnez l’identité de la cible téléphonique lorsque vous souhaitez envoyer des questionnaires par SMS. Le numéro de téléphone doit être au format E.164, qui comprend un signe plus (+), un indicatif national international, un indicatif régional et un numéro de téléphone. Par exemple : (+)(indicatif du pays)(indicatif régional)(numéro de téléphone). Lorsqu’un profil est associé à plusieurs numéros de téléphone, Medallia déclenche l’invitation au premier numéro de téléphone uniquement. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
|---------|----------|---------|
| Type d’exportation | **[!UICONTROL Profile-based]** | Vous exportez tous les membres nouvellement qualifiés d’un segment, ainsi que les champs de schéma souhaités (par exemple : adresse e-mail, numéro de téléphone, nom), tels qu’ils ont été choisis dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Streaming]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **[!UICONTROL View Destinations]** et **[!UICONTROL Manage Destinations]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier auprès de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Connect to destination]**.

* **[!UICONTROL OAuth Token Endpoint URL]** : se présente généralement sous la forme https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL Client ID]** : à obtenir auprès de votre équipe de diffusion Medallia.
* **[!UICONTROL Client Secret]** : à obtenir auprès de votre équipe de diffusion Medallia.

![Image illustrant l’écran d’authentification pour cette destination.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Name]** : nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL API Gateway URL]** : à obtenir auprès de votre équipe de diffusion Medallia. Se présente généralement sous la forme https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Import API Name]** : à obtenir auprès de votre équipe de diffusion Medallia. Nom de l’API d’importation Medallia (également appelée flux web) à utiliser dans cette connexion. Vous pouvez activer différentes audiences dans différentes API d’importation pour déclencher différents programmes d’enquête.

![Image illustrant l’écran des détails de la destination pour cette destination.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### Activer les alertes {#enable-alerts}

Vous pouvez activer les alertes pour recevoir des notifications sur le statut de votre flux de données vers votre destination. Sélectionnez une alerte dans la liste et abonnez-vous à des notifications concernant le statut de votre flux de données. Pour plus d’informations sur les alertes, consultez le guide sur l’[abonnement aux alertes des destinations dans l’interface utilisateur](../../ui/alerts.md).

Lorsque vous avez terminé de renseigner les détails sur votre connexion de destination, sélectionnez **[!UICONTROL Next]**.

## Activer des audiences vers cette destination {#activate}

>[!IMPORTANT]
> 
>* Pour activer les données, vous avez besoin des autorisations de contrôle d’accès **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** et **[!UICONTROL View Segments]** [Access control](/help/access-control/home.md#permissions). Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.
>* Pour exporter des *identités*, vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL View Identity Graph]**[](/help/access-control/home.md#permissions). <br> ![Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations.](/help/destinations/assets/overview/export-identities-to-destination.png "Sélectionnez l’espace de noms d’identité en surbrillance dans le workflow pour activer les audiences vers les destinations."){width="100" zoomable="yes"}

Consultez la section [Activer les profils et les audiences vers les destinations d’exportation d’audiences en flux continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des audiences vers cette destination.

### Mapper les attributs et les identités {#map}

Le ou les espaces de noms d&#39;identité cible suivants doivent être mappés selon le cas d&#39;utilisation :

* Pour les questionnaires par e-mail, **e-mail** doit être mappé en tant que champ cible à l’aide de **Champ cible** > **Sélectionner un espace de noms d’identité** > **e-mail**
* Pour les questionnaires basés sur SMS, **téléphone** doit être mappé en tant que champ cible à l’aide de **Champ cible** > **Sélectionner un espace de noms d’identité** > **téléphone**. Les numéros de téléphone doivent être au format E.164, qui comprend un signe plus (+), un indicatif national international, un indicatif régional et un numéro de téléphone

Il est vivement recommandé de mapper également des attributs personnalisés cibles supplémentaires pour créer des questionnaires personnalisés et d’ajouter des informations supplémentaires sur le client à l’enregistrement du questionnaire :

* Les questionnaires personnalisés s’adressent généralement au client par son nom

   * Mappez le prénom du client sur **Champ cible** > **Sélectionner des attributs personnalisés** > **Nom de l’attribut** > **prénom**
   * Mappez le nom du client sur **Champ cible** > **Sélectionner les attributs personnalisés** > **Nom de l’attribut** > **nom**

* Ajoutez des mappages pour tout autre attribut personnalisé cible selon vos besoins

![Image montrant un exemple de mappage pour les identités et les attributs.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Partagez avec votre équipe de diffusion Medallia les **Noms d’attributs** exacts pour chaque attribut personnalisé cible que vous mappez à l’aide de **Champ cible** > **Sélectionner des attributs personnalisés** > **Nom de l’attribut**. Vous pouvez effectuer une capture d’écran de la page de mappage pour la partager directement.

## Données exportées {#exported-data}

Une fois que vous avez activé votre ou vos segments vers la destination, informez votre équipe de diffusion Medallia, qui pourra valider les données exportées de Adobe Experience Platform vers Medallia. Notez que les questionnaires ne peuvent être activés dans Medallia qu&#39;après vérification réussie des données. Au préalable, les données seront exportées vers Medallia, mais ne déclencheront pas de questionnaires pour les clients.

Un exemple JSON des données exportées est fourni ci-dessous, qui utilise l’exemple de mappage de la capture d’écran ci-dessus dans la section **Mapper les attributs et les identités** :

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  "John" ,
        "lastname":  "Smith",
        "contactId": "jsmith120002",
    }
]
```

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la [présentation de la gouvernance des données](/help/data-governance/home.md).
