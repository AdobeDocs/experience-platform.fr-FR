---
title: Connexion à Medallia
description: Activez les profils pour les enquêtes et la collecte de commentaires Medallia ciblées afin de mieux comprendre les besoins et les attentes des clients.
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 33%

---

# Connexion à Medallia

## Vue d’ensemble {#overview}

Activez les profils pour les enquêtes et la collecte de commentaires Medallia ciblées afin de mieux comprendre les besoins et les attentes des clients.

>[!IMPORTANT]
>
>Ce connecteur de destination et cette page de documentation sont créés et gérés par l’équipe Medallia. Pour toute demande d&#39;information ou de mise à jour, contactez-les directement à l&#39;adresse adobe-integrations@medallia.com.

## Cas d’utilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination Medallia, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation #1

Une marque B2B souhaite évaluer et rationaliser son programme d’intégration. Ils souhaitent envoyer des enquêtes personnalisées en temps réel aux clients qui viennent de terminer le processus d&#39;intégration.

### Cas d’utilisation #2

Un détaillant cherche à mieux comprendre les préférences du client en matière d’exécution des commandes. Ils souhaitent envoyer un court questionnaire SMS d’une question aux clients qui ont effectué des achats en ligne et en magasin au cours du mois dernier.

## Conditions préalables {#prerequisites}

Les informations suivantes sont nécessaires pour établir la connexion à Medallia :
* **URL du point d’entrée du jeton OAuth**
* **Identifiant du client**
* **Secret du client**
* **URL de passerelle API**
* **Nom de l’API d’importation**

Consultez votre équipe de diffusion Medallia pour obtenir ces détails.

## Identités prises en charge {#supported-identities}

Medallia prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur les [identités](/help/identity-service/features/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| adresse e-mail | Adresse e-mail | Sélectionnez l&#39;identité de la cible du courrier électronique lorsque vous souhaitez envoyer des enquêtes sur les invitations par courrier électronique. Lorsqu’un profil est associé à plusieurs adresses électroniques, Medallia ne déclenche l’invitation qu’au premier email. |
| phone | Numéros de téléphone hachés au format E.164 | Sélectionnez l&#39;identité de la cible du téléphone lorsque vous souhaitez envoyer des enquêtes basées sur des SMS. Le numéro de téléphone doit être au format E.164, qui comprend un signe plus (+), un code d&#39;appel international, un code local et un numéro de téléphone. Par exemple : (+) (code pays) (indicatif régional) (numéro de téléphone). Lorsqu’un profil est associé à plusieurs numéros de téléphone, Medallia déclenche uniquement l’invitation au premier numéro de téléphone. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres nouvellement qualifiés d’un segment, ainsi que les champs de schéma souhaités (par exemple : adresse email, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil du [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exportations | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont des connexions basées sur l’API « toujours actives ». Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des audiences, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur les [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin des **** et des **** [ ](/help/access-control/home.md#permissions) autorisations de contrôle d’accès. Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### S’authentifier auprès de la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL URL du point d’entrée du jeton OAuth]** : prend généralement la forme https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL ID client]** : procurez-vous l’identifiant auprès de votre équipe de diffusion Medallia.
* **[!UICONTROL Client Secret]** : procurez-vous auprès de votre équipe de diffusion Medallia.

![Image montrant l&#39;écran d&#39;authentification pour cette destination.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Renseigner les détails de la destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs obligatoires et facultatifs ci-dessous. Un astérisque situé en regard d’un champ de l’interface utilisateur indique que le champ est obligatoire.

* **[!UICONTROL Nom]** : un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]** : une description qui vous aidera à identifier cette destination à l’avenir.
* **[!UICONTROL URL de passerelle API]** : procurez-vous auprès de votre équipe de diffusion Medallia. Se présente généralement sous la forme https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Importer le nom de l’API]** : procurez-vous auprès de votre équipe de diffusion Medallia. Nom de l’API d’importation Medallia (également appelée flux web) à utiliser dans cette connexion. Vous pouvez activer différentes audiences sur différentes API d&#39;import afin de déclencher différents programmes d&#39;enquête.

![Image montrant l&#39;écran des détails de la destination pour cette destination.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

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

Les espaces de noms d’identité cible suivants doivent être mappés en fonction du cas d’utilisation :
* Pour les enquêtes par e-mail, **email** doit être mappé en tant que champ cible à l’aide de **Champ cible** > **Sélectionner l’espace de noms d’identité** > **email**
* Pour les enquêtes basées sur des SMS, **phone** doit être mappé en tant que champ cible à l’aide de **Champ cible** > **Sélectionner l’espace de noms d’identité** > **phone**. Les numéros de téléphone doivent être au format E.164, qui comprend un signe plus (+), un code d’appel international pour les pays, un code local et un numéro de téléphone.

Il est vivement recommandé de mapper des attributs personnalisés de ciblage supplémentaires pour créer des enquêtes personnalisées et d’ajouter des informations supplémentaires sur le client à l’enregistrement de l’enquête :

* Les enquêtes personnalisées portent généralement le nom du client
   * Faites correspondre le prénom du client à **Champ cible** > **Sélectionner des attributs personnalisés** > **Nom d’attribut** > **prénom**
   * Faites correspondre le nom de famille du client à **Champ cible** > **Sélectionner des attributs personnalisés** > **Nom d’attribut** > **nom de hôte**
* Ajoutez des mappages pour tout autre attribut personnalisé cible selon vos besoins.

![Image présentant un exemple de mappage pour les identités et les attributs.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Partagez avec votre équipe de diffusion Medallia les **noms d’attributs** exacts pour chaque attribut personnalisé cible que vous mappez à l’aide de **Champ cible** > **Sélectionner des attributs personnalisés** > **Nom d’attribut**. Vous pouvez réaliser une capture d’écran de la page de mappage à partager directement.

## Données exportées {#exported-data}

Une fois que vous avez activé vos segments vers la destination, informez votre équipe de diffusion Medallia, qui pourra valider les données exportées de Adobe Experience Platform vers Medallia. Notez que les enquêtes ne peuvent être activées dans Medallia qu’après une vérification des données réussie. Avant cela, les données seront exportées vers Medallia, mais ne déclencheront pas d’enquêtes auprès des clients.

Vous trouverez ci-dessous un exemple JSON des données exportées, qui utilise l’exemple de mappage de la capture d’écran ci-dessus dans la section **Mapper les attributs et les identités** :

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
