---
title: Niveau de connexion
description: Utilisez la destination de diffusion en continu Niveau pour activer les audiences directement dans la base de données utilisateur de niveau et les API de gestion des segments, et prendre en charge le ciblage en temps réel au moment de la décision.
last-substantial-update: 2026-01-27T00:00:00Z
source-git-commit: 04d01b2deafb1b8f1b0c256f31475bb75989a2c4
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 9%

---


# Connexion [!DNL Kevel] {#kevel}

## Vue d’ensemble {#overview}

[[!DNL Kevel]](https://www.kevel.com/) fournit la technologie activée par l’IA et des conseils d’experts qui aident les leaders du commerce innovants à lancer, développer et réussir dans les médias de détail. [!DNL Kevel]’s Retail Media Cloud optimise les formats publicitaires ciblés, attribuables et personnalisables pour la publicité sur site et hors site.

La destination de diffusion en continu [!DNL Kevel] pour Adobe Experience Platform permet aux clients d’activer les audiences Adobe directement dans la base de données des utilisateurs d’[!DNL Kevel] et les API de gestion des segments afin de prendre en charge le ciblage en temps réel au moment de la décision de publicité.

>[!IMPORTANT]
> 
>Si vous avez des questions ou souhaitez demander une mise à jour concernant la destination [!DNL Kevel] ou sa documentation, envoyez un e-mail à l’équipe [!DNL Kevel] à l’adresse [support@kevel.com](mailto:support@kevel.com).

## Cas d’utilisation {#use-cases}

Vous pouvez activer les audiences comportementales propriétaires riches dans vos expériences médias de vente au détail afin de diffuser des annonces plus pertinentes et des performances plus solides. Dans Experience Platform, vous créez des audiences basées sur l’intention et les valeurs élevées, telles que les acheteurs fréquents de catégories ou les utilisateurs ayant un intérêt récent pour les produits, et synchronisez ces adhésions avec les [!DNL Kevel] en temps réel. [!DNL Kevel] rend immédiatement ces segments disponibles pour la prise de décision publicitaire, ce qui permet un ciblage précis pour les produits sponsorisés et d’autres formats dans les expériences de recherche, de navigation et d’application. Dès que les utilisateurs se qualifient, vous pouvez agir sur ces signaux pour générer des impressions plus pertinentes, un meilleur ciblage, ainsi qu’une mesure et un retour sur investissement améliorés.

## Conditions préalables {#prerequisites}

Pour vous préparer à l’utilisation de la destination [!DNL Kevel], assurez-vous que les conditions préalables suivantes sont remplies :

- Vous devez disposer d’un réseau **[!DNL Kevel]actif** ainsi que d’un accès API.
- Vous avez besoin d’une clé API **[!DNL Kevel]** avec les autorisations pour créer des segments et mettre à jour les enregistrements UserDB.
- Vous devez configurer des espaces de noms d’identité dans Experience Platform qui correspondent aux identités envoyées par votre site ou votre application lors des demandes d’annonces [!DNL Kevel] (par exemple, ECID, GAID, IDFA, identifiant de fidélité, etc.).
- Les clients Adobe ne doivent mapper que les identités utilisées lors des requêtes publicitaires en temps réel, car chaque identité entraîne un enregistrement UserDB.

## Identités prises en charge {#supported-identities}

La destination [!DNL Kevel] prend en charge l’activation de toute identité que votre application peut utiliser lors de l’envoi de requêtes publicitaires à [!DNL Kevel]. Vous pouvez mapper jusqu’à trois espaces de noms d’identité pour générer les enregistrements UserDB correspondants.

[!DNL Kevel] prend en charge les espaces de noms d’identité Experience Platform suivants :

| Espace de noms d’identité | Description | Utilisation type |
|--------------------|---------------------------------|----------------------------------------------------------------|
| **ECID** | Experience Cloud ID | Utilisé pour la personnalisation sur site et l’identification inter-Adobe. |
| **GAID** | GOOGLE ADVERTISING ID | Utilisé pour le trafic d’applications/d’appareils Android. |
| **IDFA** | APPLE ADVERTISING ID | Utilisé pour le trafic des applications/appareils iOS (sous réserve du consentement ATT). |
| **EXTERNAL_ID** | Identifiant externe (identifiant personnalisé) | Transmet des identifiants propriétaires ou générés par le serveur principal. |

{style="table-layout:auto"}

### Prise en charge des espaces de noms d’identité personnalisés

La destination [!DNL Kevel] **accepte également les espaces de noms personnalisés**, tels que définis dans votre implémentation Experience Platform.

Autrement dit :

- Vous pouvez mapper des **espaces de noms d’identité spécifiques au client** (par exemple : `loyalty_id`, `gigya_id` ou toute identité personnalisée que vous avez définie dans Identity Service).
- Ces espaces de noms peuvent être affectés à des `kevel_user_key1`, des `kevel_user_key2` ou des `kevel_user_key3` de la même manière que les espaces de noms globaux.
- [!DNL Kevel] génère **un enregistrement UserDB par instance de chaque identité mappée**, ce qui permet la correspondance en temps réel au moment de la décision publicitaire pour chaque identifiant envoyé par vos systèmes.

### Comportement du mappage d’identités

- Vous pouvez mapper **jusqu’à trois** espaces de noms d’identité Experience Platform aux trois emplacements d’identités d’[!DNL Kevel].
- Pour chaque profil activé, [!DNL Kevel] reçoit **un enregistrement UserDB par instance de chaque identité mappée**.
- Les clients ne doivent mapper que les identités qu’ils envoient réellement dans des requêtes publicitaires à [!DNL Kevel] afin d’éviter un stockage UserDB inutile.

![Exemple de mappage pour la destination de niveau](/help/destinations/assets/catalog/advertising/kevel-destination-mappings.png)

## Audiences prises en charge {#supported-audiences}

| Origine de l’audience | Pris en charge | Description |
|-----------------------|-----------|---------------------------------------------------------- |
| Service de segmentation | Oui | Audiences du profil Adobe évaluées par le moteur de segmentation. |
| Chargements personnalisés | Non | Pas de prise en charge pour le moment. |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

| Élément | Type | Notes |
|------|------|-------|
| Type d’exportation | **Exportation des segments** | [!DNL Kevel] reçoit une mise à jour chaque fois qu’un profil remplit les conditions pour une audience ou la quitte. |
| Fréquence des exportations | **Diffusion en continu** | Les mises à jour sont envoyées en temps réel à l’aide du framework de diffusion en continu Destination SDK. |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

Suivez le workflow standard Experience Platform [connecter une destination](../../ui/connect-destination.md).

>[!IMPORTANT]
> 
>Vous devez disposer des autorisations **Afficher les destinations** et **Gérer les destinations**.

### S’authentifier auprès de la destination {#authenticate}

Lors de la connexion à [!DNL Kevel], renseignez le champ suivant :

- **Jeton porteur** — Votre clé API [!DNL Kevel].

![Options d’authentification pour la destination de niveau](/help/destinations/assets/catalog/advertising/kevel-destination-authentication.png)

### Renseigner les détails de la destination {#destination-details}

Après l’authentification, configurez :

- **Nom** : libellé permettant d’identifier cette instance de destination.
- **Description** — Texte facultatif pour décrire cette instance de destination.
- **[!DNL Kevel]Identifiant réseau** — Identifiant réseau [!DNL Kevel].

![Détails de la destination pour Niveler la destination](/help/destinations/assets/catalog/advertising/kevel-destination-details.png)

## Activer des segments vers cette destination {#activate}

Pour envoyer des audiences à [!DNL Kevel], suivez le workflow dans\
[Activer des profils et des segments vers des destinations d’exportation de segments de streaming](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Désactiver les audiences {#deactivate}

Lorsqu’une audience est désactivée ou supprimée de la destination [!DNL Kevel] dans Experience Platform, Experience Platform cesse d’envoyer d’autres mises à jour de qualification de profil pour cette audience. Tout segment existant créé dans [!DNL Kevel] reste disponible et n’est pas automatiquement supprimé.

Si le segment [!DNL Kevel] est actuellement utilisé dans une campagne active, [!DNL Kevel] empêche la suppression pour éviter d’interrompre la diffusion en direct. Dans ce cas, la désactivation dans Experience Platform entraîne ce qui suit :

- Le flux de données Experience Platform s’arrête
- Le segment [!DNL Kevel] existe toujours et peut rester associé aux campagnes jusqu’à ce qu’il soit supprimé manuellement ou que la campagne soit mise à jour

Pour arrêter complètement le ciblage dans [!DNL Kevel], assurez-vous que le segment est supprimé de toutes les campagnes actives dans le système de gestion de campagnes de [!DNL Kevel].

### Mapper les attributs et les identités {#map}

[!DNL Kevel] requiert :

- **Espaces de noms d’identité** — Jusqu’à trois espaces de noms d’identité mappés à [!DNL Kevel] emplacements d’identités.
- **Appartenance à un segment** — Aucune mise en correspondance manuelle n’est requise ; Experience Platform transmet automatiquement les identifiants et les alias d’appartenance à un segment.

Lors de l’activation, sélectionnez les espaces de noms d’identité que vous avez configurés pour [!DNL Kevel]. Chaque identité génère son propre appel de mise à jour UserDB.

## Données exportées / Valider l’exportation des données {#exported-data}

Lorsqu’un profil est éligible ou quitte une audience, Experience Platform envoie une mise à jour en flux continu à [!DNL Kevel].

### Exemple de payload reçue par [!DNL Kevel] UserDB

```json
PUT /udb/{networkId}/segments?userKey=ECID-12345
{
  "segments": [1723, 3344, 9988]
}
```

| Paramètre | Description |
|-----------|-------------|
| **userKey** | Dérivé de l’identité Adobe mappée. |
| **segments** | Ensemble d’identifiants de segment [!DNL Kevel] correspondant aux audiences Adobe pour lesquelles le profil est actuellement réalisé. |

{style="table-layout:auto"}

### Exemple de profil Experience Platform utilisé pendant l’exportation {#sample-profile}

Lors de l’activation des audiences vers la destination [!DNL Kevel], Experience Platform envoie des fragments de profil contenant à la fois **qualifications de segment** et les **identités mappées par le client** aux emplacements d’identités de [!DNL Kevel].

Voici un exemple de profil exporté affichant :

- Plusieurs espaces de noms d’identité mappés à `kevel_user_key1`, `kevel_user_key2` et `kevel_user_key3`
- Un seul segment activé dans l’espace de noms `ups`

```json
{
  "segmentMembership": {
    "ups": {
      "9d161bbb-c785-474a-965b-7d7bc2adf879": {
        "status": "realized",
        "lastQualificationTime": "2025-12-10T21:43:38.541076Z"
      }
    }
  },
  "identityMap": {
    "kevel_user_key1": [
      {
        "id": "ECID-fN1zo"
      },
      {
        "id": "ECID-9Xr2p"
      }
    ],
    "kevel_user_key2": [
      {
        "id": "GAID-4oic4"
      }
    ],
    "kevel_user_key3": [
      {
        "id": "IDFA-nB5fU"
      }
    ]
  }
}
```

#### Comment [!DNL Kevel] ce profil

Avec la configuration de destination [!DNL Kevel], chaque identité mappée génère un enregistrement UserDB distinct, ce qui signifie que [!DNL Kevel] reçoit :

- Une mise à jour pour `ECID-fN1zo`
- Une mise à jour pour `ECID-9Xr2p`
- Une mise à jour pour `GAID-4oic4`
- Une mise à jour pour `IDFA-nB5fU`

Cela permet à la même personne d’être reconnue au moment de la décision de publicité en utilisant l’une de ses identités disponibles, chaque identité portant un ensemble identique d’appartenances à un segment.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

- [[!DNL Kevel] Référence UserDB](https://dev.kevel.com/reference/userdb)
- [[!DNL Kevel] Ciblage des segments utilisateur](https://dev.kevel.com/docs/segment-targeting)
