---
title: Connexion à Medallia
description: Activez les profils pour les enquêtes et la collecte de commentaires Medallia ciblées afin de mieux comprendre les besoins et les attentes des clients.
source-git-commit: be2d4e5d1f204feefc7acb7cb4518044ab3f153a
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 6%

---


# Connexion à Medallia

## Présentation {#overview}

Activez les profils pour les enquêtes et la collecte de commentaires Medallia ciblées afin de mieux comprendre les besoins et les attentes des clients.

>[!IMPORTANT]
>
>Cette page de documentation a été créée par l’équipe de Medallia. Pour toute demande d&#39;information ou de mise à jour, contactez-les directement à l&#39;adresse adobe-integrations@medallia.com.

## Cas dʼutilisation {#use-cases}

Pour vous aider à mieux comprendre comment et à quel moment utiliser la destination Medallia, voici des exemples de cas d’utilisation que les clients Adobe Experience Platform peuvent résoudre à l’aide de cette destination.

### Cas d’utilisation #1

Une marque B2B souhaite évaluer et rationaliser son programme d’intégration. Ils souhaitent envoyer des enquêtes personnalisées en temps réel aux clients qui viennent de terminer le processus d&#39;intégration.

### Cas d’utilisation #2

Un détaillant cherche à mieux comprendre les préférences du client en matière d’exécution des commandes. Ils souhaitent envoyer un court questionnaire SMS d’une question aux clients qui ont effectué des achats en ligne et en magasin au cours du mois dernier.

## Conditions préalables {#prerequisites}

Les informations suivantes sont nécessaires pour établir la connexion à Medallia :
* **URL du point d’entrée du jeton OAuth**
* **Identifiant client**
* **Secret client**
* **URL de passerelle API**
* **Nom de l’API d’importation**

Consultez votre équipe de diffusion Medallia pour obtenir ces détails.

## Identités prises en charge {#supported-identities}

Medallia prend en charge l’activation des identités décrites dans le tableau ci-dessous. En savoir plus sur [identités](/help/identity-service/namespaces.md).

| Identité cible | Description | Considérations |
|---|---|---|
| adresse e-mail | Adresse e-mail | Sélectionnez l&#39;identité de la cible du courrier électronique lorsque vous souhaitez envoyer des enquêtes sur les invitations par courrier électronique. Lorsqu’un profil est associé à plusieurs adresses électroniques, Medallia déclenche uniquement l’invitation au premier email. |
| phone | Numéros de téléphone hachés au format E.164 | Sélectionnez l&#39;identité de la cible du téléphone lorsque vous souhaitez envoyer des enquêtes basées sur des SMS. Le numéro de téléphone doit être au format E.164, qui comprend un signe plus (+), un code d&#39;appel international, un code local et un numéro de téléphone. Par exemple : (+) (code pays) (indicatif régional) (numéro de téléphone). Lorsqu’un profil est associé à plusieurs numéros de téléphone, Medallia déclenche uniquement l’invitation au premier numéro de téléphone. |

{style=&quot;table-layout:auto&quot;}

## Type et fréquence d&#39;export {#export-type-frequency}

Reportez-vous au tableau ci-dessous pour plus d’informations sur le type et la fréquence d’exportation des destinations.

| Élément | Type | Notes |
---------|----------|---------|
| Type d’exportation | **[!UICONTROL Basé sur les profils]** | Vous exportez tous les membres nouvellement qualifiés d’un segment, ainsi que les champs de schéma souhaités (par exemple : adresse électronique, numéro de téléphone, nom), tel que sélectionné dans l’écran de sélection des attributs de profil de la fonction [workflow d’activation de destination](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Fréquence des exports | **[!UICONTROL Diffusion en continu]** | Les destinations de diffusion en continu sont &quot;toujours sur&quot; des connexions basées sur l’API. Dès qu’un profil est mis à jour dans Experience Platform en fonction de l’évaluation des segments, le connecteur envoie la mise à jour en aval vers la plateforme de destination. En savoir plus sur [destinations de diffusion en continu](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Se connecter à la destination {#connect}

>[!IMPORTANT]
> 
>Pour vous connecter à la destination, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]** [autorisation de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Pour vous connecter à cette destination, procédez comme décrit dans le [tutoriel sur la configuration des destinations](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). Dans le workflow de configuration des destinations, renseignez les champs répertoriés dans les deux sections ci-dessous.

### Authentification à la destination {#authenticate}

Pour vous authentifier à la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Se connecter à la destination]**.

* **[!UICONTROL URL du point d’entrée du jeton OAuth]**: Se présente généralement sous la forme https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL ID client]**: Demandez à votre équipe de diffusion Medallia.
* **[!UICONTROL Secret du client]**: Demandez à votre équipe de diffusion Medallia.

![Image montrant l’écran d’authentification pour cette destination.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Renseignement des détails de destination {#destination-details}

Pour configurer les détails de la destination, renseignez les champs requis et sélectionnez **[!UICONTROL Suivant]**.

* **[!UICONTROL Nom]**: Un nom par lequel vous reconnaîtrez cette destination à l’avenir.
* **[!UICONTROL Description]**: Description qui vous aidera à identifier cette destination ultérieurement.
* **[!UICONTROL URL de passerelle API]**: Demandez à votre équipe de diffusion Medallia. Se présente généralement sous la forme https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Nom de l’API d’importation]**: Demandez à votre équipe de diffusion Medallia. Nom de l’API d’importation Medallia (également appelée flux web) à utiliser dans cette connexion. Vous pouvez activer différents segments dans différentes API d&#39;import afin de déclencher différents programmes d&#39;enquête.

![Image montrant l’écran des détails de la destination pour cette destination.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

## Activer des segments vers cette destination {#activate}

>[!IMPORTANT]
> 
>Pour activer les données, vous avez besoin de l’événement **[!UICONTROL Gestion des destinations]**, **[!UICONTROL Activation des destinations]**, **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Affichage de segments]** [autorisations de contrôle d’accès](/help/access-control/home.md#permissions). Lisez le [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur de produit pour obtenir les autorisations requises.

Lecture [Activation des profils et des segments vers des destinations d’exportation de segments en continu](/help/destinations/ui/activate-segment-streaming-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

### Mise en correspondance des attributs et des identités {#map}

Les espaces de noms d’identité cible suivants doivent être mappés en fonction du cas d’utilisation :
* Pour les enquêtes par e-mail, **email** doit être mappé en tant que champ cible à l’aide de **Champ cible** > **Sélectionner un espace de noms d’identité** > **email**
* Pour les enquêtes par SMS, **phone** doit être mappé en tant que champ cible à l’aide de **Champ cible** > **Sélectionner un espace de noms d’identité** > **phone**. Les numéros de téléphone doivent être au format E.164, qui comprend un signe plus (+), un code d’appel international pour les pays, un code local et un numéro de téléphone.

Il est vivement recommandé de mapper des attributs personnalisés de ciblage supplémentaires pour créer des enquêtes personnalisées et d’ajouter des informations supplémentaires sur le client à l’enregistrement de l’enquête :

* Les enquêtes personnalisées portent généralement le nom du client
   * Faire correspondre le prénom du client à **Champ cible** > **Sélectionner des attributs personnalisés** > **Nom de l’attribut** > **firstname**
   * Faire correspondre le nom du client à **Champ cible** > **Sélectionner des attributs personnalisés** > **Nom de l’attribut** > **lastname**
* Ajoutez des mappages pour tout autre attribut personnalisé cible selon vos besoins.

![Image présentant un exemple de mappage pour les identités et les attributs.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Partagez avec votre équipe de diffusion Medallia les **Noms d’attributs** pour chaque attribut personnalisé cible que vous mappez à l’aide de **Champ cible** > **Sélectionner des attributs personnalisés** > **Nom de l’attribut**. Vous pouvez réaliser une capture d’écran de la page de mappage à partager directement.

## Données exportées {#exported-data}

Une fois que vous avez activé vos segments vers la destination, informez votre équipe de diffusion Medallia, qui pourra valider les données exportées de Adobe Experience Platform vers Medallia. Notez que les enquêtes ne peuvent être activées dans Medallia qu’après une vérification des données réussie ; avant cela, les données seront exportées vers Medallia, mais ne déclencheront pas d&#39;enquêtes auprès des clients.

Vous trouverez ci-dessous un exemple JSON des données exportées, qui utilise l’exemple de mappage de la capture d’écran ci-dessus dans la variable **Mise en correspondance des attributs et des identités** section :

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  “John” ,
        "lastname":  “Smith”,
        "contactId": "jsmith120002",
    }
]
```

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux stratégies d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, voir [Présentation de la gouvernance des données](/help/data-governance/home.md).
