---
title: Niveau de connexion
description: Utilisez la destination de streaming Niveau pour activer les audiences dans la base de données des utilisateurs et utilisatrices de niveau et les API de gestion des segments pour le ciblage en temps réel au moment de la décision.
last-substantial-update: 2026-06-18
exl-id: 53ce2864-6a3b-4859-b14d-a03c2ce18884
TQID: https://experienceleague.adobe.com/nJ7SPoowD09LIODa9JajFZXnzw28ovZRV0-bZSIIrYY
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: a37e4ecd-c740-426a-addf-cb1b483c5c5a
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2:
  - id: cbd4a8d8-97a6-4ac9-b8d6-b6c1f28d3342
  - id: d1823595-9241-4128-8a33-e4ac3bf08773
  - id: ee602049-8a18-43df-9299-a689a025a371
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 305de8bd2ead8f6e688b34672311d119364d4d62
workflow-type: tm+mt
source-wordcount: 1524
ht-degree: 6%

---

# Connexion [!DNL Kevel] {#kevel}

[Kevel](https://www.kevel.com/) fournit la technologie compatible avec l’IA et des conseils d’experts qui aident les leaders du commerce innovants à lancer, développer et réussir dans les médias de vente au détail. Le [!DNL Retail Media Cloud] de [!DNL Kevel] fournit des formats publicitaires ciblés, attribuables et personnalisables pour la publicité sur site et hors site.

Utilisez la destination de diffusion en continu [!DNL Kevel] pour activer les audiences Adobe directement dans les API [!DNL UserDB] et de gestion des segments d’[!DNL Kevel] et prendre en charge le ciblage en temps réel au moment de la décision de publicité. Vous pouvez également exporter des attributs de profil, tels que l’affectation de groupe [test d’incrémentalité](https://dev.kevel.com/docs/incrementality) d’un utilisateur ou d’une utilisatrice, pour que les [!DNL Kevel] agissent au moment de la décision.

>[!IMPORTANT]
>
>Si vous avez des questions ou souhaitez demander une mise à jour concernant la destination [!DNL Kevel] ou sa documentation, envoyez un e-mail à l’équipe [!DNL Kevel] à l’adresse [support@kevel.com](mailto:support@kevel.com).

## Cas d’utilisation {#use-cases}

**Ciblez les audiences de médias de vente au détail en temps réel.** Vous pouvez activer les audiences comportementales propriétaires riches dans vos expériences médias de vente au détail afin de diffuser des annonces plus pertinentes et des performances plus solides. Dans Experience Platform, vous créez des audiences basées sur l’intention et les valeurs élevées, telles que les acheteurs fréquents de catégories ou les utilisateurs ayant un intérêt récent pour les produits, et synchronisez ces adhésions avec les [!DNL Kevel] en temps réel. [!DNL Kevel] rend immédiatement ces segments disponibles pour [ad decisioning](https://dev.kevel.com/docs/segment-targeting), ce qui permet un ciblage précis des produits sponsorisés et d’autres formats dans les expériences de recherche, de navigation et d’application. Dès que les utilisateurs se qualifient, vous pouvez agir sur ces signaux pour générer des impressions plus pertinentes, un meilleur ciblage, ainsi qu’une mesure et un retour sur investissement améliorés.

**Mesurer l’impact incrémentiel.** Vous pouvez également exporter l’affectation de groupe d’un utilisateur ou d’une utilisatrice en tant qu’attribut de profil pour alimenter le test d’incrémentalité [&#x200B; d’[!DNL Kevel]](https://dev.kevel.com/docs/incrementality). [!DNL Kevel] présente une cohorte de contrôle et la compare à celle des utilisateurs exposés afin de quantifier l’effet élévateur *causal* généré par vos campagnes, plutôt que de se fier à des mesures proxy telles que le nombre de nouveaux clients sur la marque ou l’effet élévateur basé sur les corrélations. Vous pouvez ainsi prouver des ventes et des conversions incrémentielles tout en réduisant [!DNL Kevel] l’impact sur le chiffre d’affaires en diffusant la meilleure publicité éligible suivante aux utilisateurs retenus.

## Conditions préalables {#prerequisites}

Pour vous préparer à l’utilisation de la destination [!DNL Kevel], assurez-vous que les conditions préalables suivantes sont remplies :

- Vous devez disposer d’un réseau **[!DNL Kevel]actif** ainsi que d’un accès API.
- Vous avez besoin d’une clé API **avec les autorisations pour créer des segments et mettre à jour les enregistrements [!DNL UserDB].**&#x200B;[!DNL Kevel]
- Vous devez configurer des espaces de noms d’identité dans Experience Platform qui correspondent aux identités envoyées par votre site ou votre application lors des demandes d’annonces [!DNL Kevel], telles que l’ECID, le GAID, l’IDFA et l’ID de fidélité.
- Mappez uniquement les identités que vous envoyez lors des demandes d’annonces en temps réel. Chaque identité mappée génère un enregistrement [!DNL UserDB].

## Identités prises en charge {#supported-identities}

La destination [!DNL Kevel] prend en charge l’activation de toute identité que votre application peut utiliser lors de l’envoi de requêtes publicitaires à [!DNL Kevel]. Vous pouvez mapper jusqu’à trois espaces de noms d’identité pour générer les enregistrements [!DNL UserDB] correspondants.

[!DNL Kevel] prend en charge les espaces de noms d’identité Experience Platform suivants :

| Espace de noms d’identité | Description | Utilisation type |
|--------------------|---------------------------------|----------------------------------------------------------------|
| **ECID** | Experience Cloud ID | Utilisé pour la personnalisation sur site et l’identification inter-Adobe. |
| **GAID** | GOOGLE ADVERTISING ID | Utilisé pour le trafic d’applications/d’appareils Android. |
| **IDFA** | APPLE ADVERTISING ID | Utilisé pour le trafic des applications/appareils iOS (sous réserve du consentement ATT). |
| **EXTERNAL_ID** | Identifiant externe (identifiant personnalisé) | Transmet des identifiants propriétaires ou générés par le serveur principal. |

{style="table-layout:auto"}

### Prise en charge des espaces de noms d’identité personnalisés {#custom-identity-namespaces}

La destination [!DNL Kevel] accepte également les espaces de noms personnalisés, tels que définis dans votre implémentation Experience Platform.

Autrement dit :

- Vous pouvez mapper des espaces de noms d’identité spécifiques au client, tels que `loyalty_id`, `gigya_id` ou toute identité personnalisée que vous avez définie dans Identity Service.
- Vous pouvez affecter ces espaces de noms à des `kevel_user_key1`, des `kevel_user_key2` ou des `kevel_user_key3` de la même manière que les espaces de noms globaux.

### Comportement du mappage d’identités {#identity-mapping-behavior}

- Vous pouvez mapper jusqu’à trois espaces de noms d’identité Experience Platform aux trois emplacements d’identités d’[!DNL Kevel].
- Pour chaque profil activé, [!DNL Kevel] génère un enregistrement [!DNL UserDB] par instance de chaque identité mappée, ce qui permet la correspondance en temps réel au moment de la décision publicitaire pour chaque identifiant envoyé par vos systèmes.
- Mappez uniquement les identités que vous envoyez dans les demandes publicitaires à [!DNL Kevel] pour éviter un stockage [!DNL UserDB] inutile.

![Copie d’écran de l’étape de mappage d’identités présentant trois espaces de noms d’identité mappés aux emplacements d’identités de niveau.](/help/destinations/assets/catalog/advertising/kevel-destination-mappings.png)

## Audiences prises en charge {#supported-audiences}

La destination [!DNL Kevel] prend en charge les origines d’audience et les types de données d’audience suivants.

| Origine de l’audience | Pris en charge | Description |
|-----------------------|-----------|---------------------------------------------------------- |
| Service de segmentation | Oui | Audiences du profil Adobe évaluées par le moteur de segmentation. |
| Toutes les autres origines d’audience | Oui | Cette catégorie inclut toutes les origines d’audience en dehors des audiences générées par le [!DNL Segmentation Service]. Découvrez les [différentes origines d’audience](/help/segmentation/ui/audience-portal.md#customize). Voici quelques exemples : <ul><li> audiences de chargement personnalisées [importées](../../../segmentation/ui/audience-portal.md#import-audience) dans Experience Platform à partir de fichiers CSV,</li><li> les audiences semblables, </li><li> les audiences fédérées, </li><li> les audiences générées dans d’autres applications Experience Platform, telles que [!DNL Adobe Journey Optimizer], </li><li> et plus encore. </li></ul> |

{style="table-layout:auto"}

Audiences prises en charge par type de données d’audience :

| Type de données d’audience | Pris en charge | Description | Cas d’utilisation |
|--------------------|-----------|-------------|-----------|
| [Audiences de personnes](/help/segmentation/types/people-audiences.md) | Oui | En fonction des profils client, ce qui vous permet de cibler des groupes spécifiques de personnes pour les campagnes marketing. | Acheteurs fréquents, personnes abandonnant leur panier |
| [Audiences de compte](/help/segmentation/types/account-audiences.md) | Non | Ciblez des individus au sein d’organisations spécifiques pour les stratégies marketing basées sur les comptes. | Marketing B2B |
| [Audiences de prospects &#x200B;](/help/segmentation/types/prospect-audiences.md) | Non | Ciblez les individus qui ne sont pas encore clients, mais qui partagent des caractéristiques avec votre audience cible. | Prospection à l’aide de données tierces |
| [Exportations de jeux de données](/help/catalog/datasets/overview.md) | Non | Collections de données structurées stockées dans le lac de données [!DNL Adobe Experience Platform]. | Rapports, workflows de science des données |

{style="table-layout:auto"}

## Type et fréquence d’exportation {#export-type-frequency}

La destination [!DNL Kevel] exporte les données à l’aide du type et de la fréquence suivants.

| Élément | Type | Notes |
|------|------|-------|
| Type d’exportation | **Exportation des segments** | [!DNL Kevel] reçoit une mise à jour chaque fois qu’un profil remplit les conditions pour une audience ou la quitte. |
| Fréquence des exportations | **Diffusion en continu** | Les mises à jour sont envoyées en temps réel à l’aide du framework de diffusion en continu Destination SDK. |

{style="table-layout:auto"}

## Se connecter à la destination {#connect}

Suivez le workflow standard Experience Platform [connecter une destination](../../ui/connect-destination.md).

>[!IMPORTANT]
>
>Vous devez disposer des autorisations **[!UICONTROL Afficher les destinations]** et **[!UICONTROL Gérer les destinations]**.

### S’authentifier auprès de la destination {#authenticate}

Lors de la connexion à [!DNL Kevel], renseignez le champ suivant :

- **[!UICONTROL Jeton porteur]** : votre clé API [!DNL Kevel].

![Capture d’écran de l’étape d’authentification affichant le champ du jeton porteur pour la destination de niveau.](/help/destinations/assets/catalog/advertising/kevel-destination-authentication.png)

### Renseigner les détails de la destination {#destination-details}

Après l’authentification, configurez :

- **[!UICONTROL Name]** : libellé permettant d’identifier cette instance de destination.
- **[!UICONTROL Description]** : texte facultatif pour décrire cette instance de destination.
- **[!UICONTROL Identifiant réseau de niveau]** : votre identifiant réseau [!DNL Kevel].

![Copie d’écran de l’étape Détails de la destination affichant le nom, la description et les champs d’ID réseau de niveau.](/help/destinations/assets/catalog/advertising/kevel-destination-details.png)

## Activer des audiences vers cette destination {#activate}

Pour envoyer des audiences à [!DNL Kevel], suivez le workflow dans [Activer les audiences vers des destinations de diffusion en streaming](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Désactiver les audiences {#deactivate}

Lorsqu’une audience est désactivée ou supprimée de la destination [!DNL Kevel] dans Experience Platform, Experience Platform cesse d’envoyer d’autres mises à jour de qualification de profil pour cette audience. Tout segment existant créé dans [!DNL Kevel] reste disponible et n’est pas automatiquement supprimé.

Si le segment [!DNL Kevel] est actuellement utilisé dans une campagne active, [!DNL Kevel] empêche la suppression pour éviter d’interrompre la diffusion en direct. Dans ce cas, la désactivation dans Experience Platform entraîne ce qui suit :

- Le flux de données Experience Platform s’arrête.
- Le segment [!DNL Kevel] existe toujours et peut rester associé aux campagnes jusqu’à ce qu’il soit supprimé manuellement ou que la campagne soit mise à jour.

Pour arrêter complètement le ciblage dans [!DNL Kevel], assurez-vous que le segment est supprimé de toutes les campagnes actives dans le système de gestion de campagnes de [!DNL Kevel].

### Mapper les attributs et les identités {#map}

[!DNL Kevel] requiert :

- **Espaces de noms d’identité** : jusqu’à trois espaces de noms d’identité mappés à [!DNL Kevel] emplacements d’identités.
- **Appartenance à une audience** : aucun mappage manuel requis. Experience Platform transmet automatiquement les identifiants et les alias d’appartenance à l’audience.

Lors de l’activation, sélectionnez les espaces de noms d’identité que vous avez configurés pour [!DNL Kevel]. Chaque identité génère son propre appel de mise à jour de [!DNL UserDB].

#### Attributs de profil (facultatif) {#profile-attributes}

Vous pouvez éventuellement mapper les attributs de profil XDM à [!DNL Kevel]. La destination reconnaît le nom d’attribut cible suivant.

| Nom du champ cible | Description | Type de valeur |
|-------------------|-------------|------------|
| **`kevelGroup`** | Affectation de groupe de test d’incrémentalité de l’utilisateur. Utilisé par [!DNL Kevel] pour diviser les utilisateurs en cohortes de test et de contrôle afin de mesurer l’impact publicitaire causal. | Entier (1 à 100) |

{style="table-layout:auto"}

Pour mapper un attribut de groupe, ajoutez une nouvelle ligne de mappage à l’étape **[!UICONTROL Mappage]** et configurez les éléments suivants :

1. **[!UICONTROL Champ Source]** : sélectionnez l’attribut XDM ou l’attribut calculé contenant le numéro de groupe de l’utilisateur, par exemple `_yourSchema.incrementalityGroup`.
1. **[!UICONTROL Champ cible]** : ouvrez le sélecteur de champ cible, conservez **[!UICONTROL Sélectionner des attributs]** sélectionné, puis sélectionnez **`kevelGroup`** (Entier) dans le schéma.

![Copie d’écran de l’étape de mappage présentant un attribut XDM mappé au champ cible kevelGroup pour la destination de niveau.](/help/destinations/assets/catalog/advertising/kevel-destination-group-mapping.png)

## Valider l’exportation des données {#exported-data}

Lorsqu’un profil est éligible ou quitte une audience, Experience Platform envoie une mise à jour en flux continu à [!DNL Kevel].

### Exemple de payload reçue par [!DNL Kevel] UserDB {#sample-payload}

Experience Platform envoie l’exemple de payload suivant à l’API [!DNL UserDB] de [!DNL Kevel].

```json
PUT /udb/{networkId}/segments?userKey=ECID-12345&group=42
{
  "segments": [1723, 3344, 9988]
}
```

| Paramètre | Description |
|-----------|-------------|
| **userKey** | Dérivé de l’identité Adobe mappée. |
| **group** | *(Facultatif)* Envoyé en tant que paramètre de requête. Groupe de test d’incrémentalité de l’utilisateur (1 à 100). Uniquement inclus si un attribut de profil est mappé au champ cible `kevelGroup`. |
| **segments** | Ensemble d’identifiants de segment [!DNL Kevel] correspondant aux audiences Adobe pour lesquelles le profil est actuellement réalisé. |

{style="table-layout:auto"}

### Exemple de profil Experience Platform utilisé pendant l’exportation {#sample-profile}

Lors de l’activation des audiences vers la destination [!DNL Kevel], Experience Platform envoie des fragments de profil contenant à la fois **qualifications de segment** et les **identités que vous avez mappées** aux emplacements d’identités de [!DNL Kevel].

Voici un exemple de profil exporté affichant :

- Plusieurs espaces de noms d’identité mappés à `kevel_user_key1`, `kevel_user_key2` et `kevel_user_key3`
- Un seul segment activé dans l’espace de noms `ups`
- Attribut de profil mappé à `kevelGroup` pour le test d’incrémentalité

```json
{
  "attributes": {
    "kevelGroup": 42
  },
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

#### Comment [!DNL Kevel] ce profil {#kevel-profile-interpretation}

Avec la configuration de destination [!DNL Kevel], chaque identité mappée génère un enregistrement [!DNL UserDB] distinct, ce qui signifie que [!DNL Kevel] reçoit :

- Une mise à jour pour `ECID-fN1zo`
- Une mise à jour pour `ECID-9Xr2p`
- Une mise à jour pour `GAID-4oic4`
- Une mise à jour pour `IDFA-nB5fU`

Cela permet à la même personne d’être reconnue au moment de la décision de publicité en utilisant l’une de ses identités disponibles, chaque identité portant un ensemble identique d’appartenances à un segment.

Lorsqu’un attribut de `kevelGroup` est mappé et présent sur le profil, chaque mise à jour de [!DNL UserDB] inclut également l’affectation de groupe de l’utilisateur comme paramètre de requête `group`, ce qui permet à la fonctionnalité de test d’incrémentalité de [!DNL Kevel] de déterminer l’appartenance à la cohorte de test et de contrôle au moment de la décision publicitaire.

## Utilisation et gouvernance des données {#data-usage-governance}

Lors de la gestion de vos données, toutes les destinations [!DNL Adobe Experience Platform] se conforment aux politiques d’utilisation des données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [Présentation de la gouvernance des données](/help/data-governance/home.md).

## Ressources supplémentaires {#additional-resources}

- [Niveau de référence UserDB](https://dev.kevel.com/reference/userdb)
- [Ciblage des segments d’utilisateurs de niveau](https://dev.kevel.com/docs/segment-targeting)
