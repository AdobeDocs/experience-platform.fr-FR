---
title: Recherche d’attributs de profil Edge en temps réel
description: Découvrez comment rechercher des attributs de profil Edge en temps réel à l’aide de la destination Personalization personnalisée et de l’API Edge Network
type: Tutorial
exl-id: e185d741-af30-4706-bc8f-d880204d9ec7
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1911'
ht-degree: 7%

---

# Recherche d’attributs de profil sur le serveur Edge en temps réel

Adobe Experience Platform utilise le [profil client en temps réel](../../profile/home.md) comme source unique de vérité pour toutes les données de profil. Pour une récupération rapide des données en temps réel, il utilise des [profils Edge](../../profile/edge-profiles.md), qui sont des profils légers répartis dans [Edge Network](../../collection/home.md#edge). Cela permet d’obtenir des cas d’utilisation de personnalisation rapides et en temps réel.

## Cas d’utilisation {#use-cases}

Vous trouverez ci-dessous deux cas d’utilisation pour lesquels la recherche de profil Edge peut vous aider.

* **Real-Time Personalization** : récupérez rapidement les informations de profil du profil Edge pour personnaliser l’expérience d’un utilisateur sur votre site web.
* **Service clientèle** : récupérez les informations de profil en temps réel lorsqu’un client appelle un agent du centre d’assistance.

Cette page décrit les étapes à suivre pour rechercher des données de profil Edge en temps réel, pour offrir des expériences de personnalisation ou pour informer les règles de prise de décision par le biais d’applications en aval.

## Terminologie et conditions préalables {#prerequisites}

Lors de la configuration du cas d’utilisation décrit sur cette page, vous utiliserez les composants Experience Platform suivants :

* [Flux de données](../../datastreams/overview.md) : un flux de données reçoit des données d’événement entrantes de Web SDK et répond avec des données de profil Edge.
* [Politiques de fusion](../../segmentation/ui/segment-builder.md#merge-policies) : vous allez créer une politique de fusion [!UICONTROL Active-On-Edge] pour vous assurer que les profils Edge utilisent les données de profil correctes.
* [Connexion Personalization personnalisée](../catalog/personalization/custom-personalization.md) : vous allez configurer une nouvelle connexion de personnalisation personnalisée qui enverra les attributs de profil à Edge Network.
* [API Edge Network ](https://developer.adobe.com/data-collection-apis/docs/) : vous utiliserez la fonctionnalité d’API Edge Network [collecte de données interactive](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) pour récupérer rapidement les attributs de profil des profils Edge.

## Mécanismes de sécurisation des performances {#guardrails}

Les cas d’utilisation de la recherche de profil Edge sont soumis aux mécanismes de sécurisation de performances spécifiques décrits dans le tableau ci-dessous. Pour plus d’informations sur les mécanismes de sécurisation de l’API Edge Network, consultez la page de documentation [mécanismes de sécurisation](https://developer.adobe.com/data-collection-apis/docs/getting-started/guardrails/).

| Service Edge Network | Segmentation Edge | Demandes par seconde |
|---------|----------|---------|
| [Destination de personnalisation personnalisée](../catalog/personalization/custom-personalization.md) via l’API [Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/) | Oui | 1 500 |
| [Destination de personnalisation personnalisée](../catalog/personalization/custom-personalization.md) via l’API [Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/) | Non | 1 500 |

## Étape 1 : créer et configurer un flux de données {#create-datastream}

Suivez les étapes de la documentation [configuration du flux de données](../../datastreams/configure.md#create-a-datastream) pour créer un flux de données avec les paramètres **[!UICONTROL Service]** suivants :

* **[!UICONTROL Service]** : [!UICONTROL Adobe Experience Platform]
* **[!UICONTROL Destinations Personalization]** : Activé
* **[!UICONTROL Segmentation Edge]** : si vous avez besoin d’une segmentation Edge, activez cette option. Si vous souhaitez uniquement rechercher des attributs de profil sur le serveur Edge, mais que vous ne souhaitez pas effectuer de segmentation en fonction des profils Edge, laissez cette option désactivée.


  <!-- >[!IMPORTANT]
    >
    >Enabling edge segmentation limits the maximum number of lookup requests to 1500 request per second. If you need a higher request throughput, disable edge segmentation for your datastream. See the [guardrails documentation](../guardrails.md#edge-destinations-activation) for detailed information. -->

  ![Image de l’interface utilisateur d’Experience Platform affichant l’écran de configuration du flux de données.](../assets/ui/activate-edge-profile-lookup/datastream-config.png)


## Étape 2 : configurer vos audiences pour l’évaluation Edge {#audience-edge-evaluation}

La recherche d’attributs de profil sur Edge nécessite que vos audiences soient configurées pour l’évaluation Edge.

Assurez-vous que la [Politique de fusion Active-on-Edge](../../segmentation/ui/segment-builder.md#merge-policies) est définie par défaut pour les audiences que vous prévoyez d’activer. La politique de fusion [!DNL Active-On-Edge] garantit que les audiences sont constamment évaluées [à la périphérie](../../segmentation/methods/edge-segmentation.md) et sont disponibles pour les cas d’utilisation de la personnalisation en temps réel.

Suivez les instructions de la section [création d’une politique de fusion](../../profile/merge-policies/ui-guide.md#create-a-merge-policy) et assurez-vous d’activer le bouton **[!UICONTROL Politique de fusion Active-On-Edge]**.

>[!IMPORTANT]
>
>Si vos audiences utilisent une autre politique de fusion, vous ne pourrez pas récupérer les attributs de profil à partir du serveur Edge et vous ne pourrez pas effectuer de recherche de profil Edge.

## Étape 3 : envoi de données d’attribut de profil à Edge Network{#configure-custom-personalization-connection}

Pour rechercher des profils Edge, y compris les attributs et les données d’appartenance à une audience, en temps réel, les données doivent être disponibles sur Edge Network. À cet effet, vous devez établir une connexion à une destination **[!UICONTROL Custom Personalization With Attributes]** et activer les audiences, y compris les attributs que vous souhaitez rechercher sur les profils Edge.

+++ Configuration d’une connexion Personalization personnalisée avec les attributs

Suivez le [tutoriel sur la création de connexion de destination](../ui/connect-destination.md) pour obtenir des instructions détaillées sur la création d’une connexion de destination.

Pendant la configuration de la nouvelle destination, sélectionnez le flux de données que vous avez créé à l’[étape 1](#create-datastream) dans le champ **[!UICONTROL Identifiant du flux de données]**. Pour **[!UICONTROL Alias d’intégration]** vous pouvez utiliser n’importe quelle valeur qui vous aidera à identifier cette connexion de destination à l’avenir, comme le nom de la destination.

![Image de l’interface utilisateur d’Experience Platform montrant l’écran de configuration Personalization personnalisé avec les attributs.](../assets/ui/activate-edge-profile-lookup/destination-config.png)

+++

+++Activer vos audiences vers la connexion Personalization personnalisé avec les attributs

Après avoir créé une connexion **[!UICONTROL Custom Personalization With Attributes]**, vous êtes prêt à envoyer des données de profil à Edge Network.

>[!IMPORTANT]
> 
> * Pour activer les données et activer l’[étape de mappage](#mapping) du workflow, vous devez disposer des autorisations de contrôle d’accès **[!UICONTROL Afficher les destinations]**, **[!UICONTROL Activer les destinations]**, **[!UICONTROL Afficher les profils]** et **[!UICONTROL Afficher les segments]** [](/help/access-control/home.md#permissions).
> 
> Lisez la [présentation du contrôle d’accès](/help/access-control/ui/overview.md) ou contactez votre administrateur ou administratrice du produit pour obtenir les autorisations requises.

1. Accédez à **[!UICONTROL Connexions > Destinations]**, puis sélectionnez l’onglet **[!UICONTROL Catalogue]**.

   ![Onglet Catalogue de destinations mis en surbrillance dans l’interface utilisateur d’Experience Platform.](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. Recherchez la vignette de destination **[!UICONTROL Custom Personalization With Attributes]** puis sélectionnez **[!UICONTROL Activer les audiences]**, comme illustré dans l’image ci-dessous.

   ![Activer le contrôle d’audience en surbrillance sur une carte de destination dans le catalogue.](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. Sélectionnez la connexion de destination que vous avez précédemment configurée, puis sélectionnez **[!UICONTROL Suivant]**.

   ![Sélectionnez l’étape de destination dans le workflow d’activation.](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. Sélectionnez vos audiences. Utilisez les cases à cocher situées à gauche des noms d’audience pour sélectionner les audiences à activer vers la destination, puis sélectionnez **[!UICONTROL Suivant]**.

   Vous pouvez effectuer un choix parmi plusieurs types d’audiences, selon leur origine :

   * **[!UICONTROL Segmentation Service]** : audiences générées dans Experience Platform par le service de segmentation. Voir la [documentation sur la segmentation](../../segmentation/ui/overview.md) pour plus d’informations.
   * **[!UICONTROL Chargement personnalisé]** : audiences générées en dehors d’Experience Platform et chargées dans Experience Platform au format CSV. Pour en savoir plus sur les audiences externes, consultez la documentation sur [importation d’une audience](../../segmentation/ui/overview.md#import-audience).
   * Autres types d’audiences, provenant d’autres solutions Adobe, telles que [!DNL Audience Manager].

     ![L’étape Sélectionner les audiences du workflow d’activation avec plusieurs audiences mises en surbrillance.](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

1. Sélectionnez les attributs de profil que vous souhaitez rendre disponibles pour les profils Edge.

   * **Sélectionnez les attributs sources**. Pour ajouter des attributs sources, sélectionnez le contrôle **[!UICONTROL Ajouter un nouveau champ]** dans la colonne **[!UICONTROL Source]** et recherchez ou accédez au champ d’attribut XDM de votre choix, comme illustré ci-dessous.

     ![Enregistrement d’écran montrant comment sélectionner un attribut cible dans l’étape de mappage.](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

   * **Sélectionner les attributs de la cible**. Pour ajouter des attributs cibles, sélectionnez le contrôle **[!UICONTROL Ajouter un nouveau champ]** dans la colonne **[!UICONTROL Champ cible]** et saisissez le nom de l’attribut personnalisé auquel vous souhaitez mapper l’attribut source.

     ![Enregistrement d’écran montrant comment sélectionner un attribut XDM dans l’étape de mappage](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)



Lorsque vous avez terminé de mapper les attributs de profil, sélectionnez **[!UICONTROL Suivant]**.

Sur la page **[!UICONTROL Vérifier]**, vous pouvez voir un résumé de votre sélection. Sélectionnez **[!UICONTROL Annuler]** pour interrompre le flux, **[!UICONTROL Précédent]** pour modifier vos paramètres ou **[!UICONTROL Terminer]** pour confirmer votre sélection et commencer à envoyer des données de profil à Edge Network.

![Résumé de la sélection à l’étape de révision.](../assets/ui/activate-edge-personalization-destinations/review.png)

+++

+++Évaluation des politiques de consentement

Si votre organisation a acheté **Adobe HealthCare Shield** ou **Adobe Privacy &amp; Security Shield**, sélectionnez **[!UICONTROL Afficher les politiques de consentement applicables]** pour identifier les politiques de consentement appliquées et le nombre de profils inclus dans l&#39;activation qui en résulte. Pour plus d’informations, consultez [ Évaluation des politiques de consentement ](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) .

**Vérifications des politiques d’utilisation des données**

À l’étape **[!UICONTROL Révision]**, Experience Platform vérifie également les violations de la politique d’utilisation des données. Vous trouverez ci-dessous un exemple de violation de la politique. Vous ne pouvez pas terminer le workflow d’activation de l’audience tant que vous n’avez pas résolu la violation. Pour plus d’informations sur la résolution des violations de politique, consultez la section sur les violations de politique d’utilisation des données [data usage policy violations](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) dans la documentation sur la gouvernance des données .

![Exemple de violation de politique de données.](../assets/common/data-policy-violation.png)

+++

+++Filtrer les audiences

Dans l’étape **[!UICONTROL Révision]**, vous pouvez utiliser les filtres disponibles sur la page pour afficher uniquement les audiences dont le planning ou le mappage a été mis à jour dans le cadre de ce workflow. Vous pouvez également activer/désactiver les colonnes du tableau à afficher.

![Enregistrement d’écran affichant les filtres d’audience disponibles à l’étape de révision.](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)


Si vous êtes satisfait(e) de votre sélection et qu’aucune violation de politique n’a été détectée, sélectionnez **[!UICONTROL Terminer]** pour confirmer votre sélection.

+++

## Étape 4 : Rechercher les attributs de profil sur le serveur Edge {#configure-edge-profile-lookup}

À l’heure actuelle, vous devriez avoir terminé [configuration de votre flux de données](#create-datastream), vous avez [créé une nouvelle connexion de destination Personalization personnalisée avec attributs](#configure-destination) et vous avez utilisé cette connexion pour [envoyer les attributs de profil](#activate-audiences) que vous pourrez rechercher dans Edge Network.

L’étape suivante consiste à configurer votre solution de personnalisation pour récupérer les attributs de profil des profils Edge.

>[!IMPORTANT]
>
>Les attributs de profil peuvent contenir des données sensibles. Pour protéger ces données, vous devez récupérer les attributs de profil via l’[API Edge Network](https://developer.adobe.com/data-collection-apis/docs/getting-started/). De plus, vous devez récupérer les attributs de profil via l’API Edge Network [point d’entrée de la collecte de données interactive](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) pour que les appels API soient authentifiés.
><br>Si vous ne suivez pas les exigences ci-dessus, la personnalisation sera basée sur l’appartenance à l’audience uniquement et les attributs de profil ne seront pas disponibles pour vous.

Le flux de données que vous avez configuré à l’[étape 1](#create-datastream) est maintenant prêt à accepter les données d’événement entrantes et à répondre avec des informations de profil Edge.

Configurez votre intégration pour récupérer les informations de profil Edge comme illustré dans les exemples ci-dessous.

### Requête {#request}

Pour récupérer les données de profil Edge, envoyez un appel de `POST` vide au point d’entrée `/interact`, avec l’identité principale pour laquelle vous recherchez des attributs de profil inclus dans l’événement, comme illustré ci-dessous.

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" 
-d '{
    "event":
    {
        "xdm": {
            "identityMap": {
                "Email": [
                    {  
                        "id":"test123@adobetest.com",
                        "primary":true
                    }
                ]
            }
        }
    }
    
}'
```

| Paramètre | Type | Obligatoire | Description |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Oui. | Identifiant du flux de données que vous avez créé à l’[étape 1](#create-datastream). |

### Réponse {#response}

Une réponse réussie renvoie des `200 OK` de statut HTTP, avec un objet `Handle` qui inclut des informations similaires aux exemples dans les onglets ci-dessous, selon que le profil se trouve sur le serveur Edge ou non.

>[!NOTE]
>
>Les réponses de l’API sont modulaires et l’objet `handle` peut inclure plusieurs objets `payload` de différents types. Les informations relatives à la recherche de profil Edge sont regroupées sous l&#39;objet `payload` avec `"type": "activation:pull"`,

>[!BEGINTABS]

>[!TAB Le profil existe sur le serveur Edge]

Si le profil existe sur le serveur Edge, en fonction des attributs de profil et des audiences activés sur le serveur Edge, vous pouvez vous attendre à une réponse avec des attributs et des appartenances à l’audience similaires à celui ci-dessous.

```json
{
  "requestId": "3c600138-d785-42ca-a025-bb725f4b5da9",
  "handle": [
    {
      "payload": [
        {
          "type": "profileLookup",
          "destinationId": "9218b727-ec59-4a46-b8b9-05503f138c5d",
          "alias": "rk-demo-custom-personalization-XXXX",
          "attributes": {
            "zip": {
              "value": "19000"
            },
            "firstName": {
              "value": "Test"
            },
            "lastName": {
              "value": "User123"
            },
            "gender": {
              "value": "male"
            },
            "city": {
              "value": "Philadelphia"
            },
            "state": {
              "value": "PA"
            },
            "email": {
              "value": "test123@adobetest.com"
            }
          },
          "segments": [
            {
              "id": "85018bd8-7ad1-4e17-ae30-8389c04bd3c0",
              "namespace": "ups"
            },
            {
              "id": "d09a8159-8b30-4178-b2f2-7a8c5e3168d9",
              "namespace": "ups"
            }
          ]
        }
      ],
      "type": "activation:pull",
      "eventIndex": 0
    }
  ]
}
```

L’objet `handle` fournit les informations décrites dans le tableau ci-dessous.

| Paramètre | Description |
|---------|----------|
| `payload` | Objet `payload` contenant les informations de recherche Edge. La réponse peut contenir plusieurs objets `payload` supplémentaires, sans rapport avec la recherche Edge. |
| `type` | Les payloads sont regroupées dans la réponse par type. Le type de payload pour la recherche de profil Edge est toujours défini sur `profileLookup`. |
| `destinationId` | Identifiant de l’instance de connexion **[!UICONTROL Custom Personalization]** que vous avez créée à l’étape [3](#configure-custom-personalization-connection). |
| `alias` | Alias de la connexion de destination, configuré par l’utilisateur lors de la création de la connexion de destination [Custom Personalization](../catalog/personalization/custom-personalization.md). |
| `attributes` | Ce tableau inclut les attributs de profil Edge des audiences que vous avez activées à [étape 3](#configure-custom-personalization-connection). |
| `segments` | Ce tableau inclut les audiences que vous avez activées à [étape 3](#configure-custom-personalization-connection). |
| `type` | `handle` objets sont regroupés par type. Pour les cas d’utilisation de la recherche de profil Edge, le type de l’objet `handle` est toujours `activation:pull`. |
| `eventIndex` | L’Edge Network reçoit les événements du client sous la forme de tableaux. L’ordre des événements dans le tableau est conservé pendant leur traitement et reflété par cet index. L’indexation des événements commence par `0`. |

>[!TAB Le profil n’existe pas sur le serveur Edge]

Si le profil n’existe pas sur le serveur Edge, vous pouvez vous attendre à une réponse similaire à celle ci-dessous.

```json
{
  "requestId": "531b541a-4541-419e-ac99-fd7e452f0c0f",
  "handle": [
    {
      "payload": [],
      "type": "activation:pull",
      "eventIndex": 0
    }
  ]
}
```

L’objet `handle` fournit les informations décrites dans le tableau ci-dessous.

| Paramètre | Description |
|---------|----------|
| `payload` | Lorsque le profil n’est pas présent sur le bord, l’objet `payload` est vide. |
| `type` | `payload` objets sont regroupés par type. Pour les cas d’utilisation de la recherche de profil Edge, le type de l’objet `payload` est toujours `activation:pull`. |
| `eventIndex` | L’Edge Network reçoit les événements du client sous la forme de tableaux. L’ordre des événements dans le tableau est conservé pendant leur traitement et reflété par cet index. L’indexation des événements commence par `0`. |

>[!ENDTABS]

>[!SUCCESS]
>
>Si vous avez correctement configuré l’intégration, vous avez désormais accès aux données de profil Edge et vous pouvez utiliser les attributs et l’appartenance à l’audience de vos profils Edge pour déclencher la personnalisation en temps réel dans votre moteur de personnalisation en aval.

## Conclusion {#conclusion}

En suivant les étapes ci-dessus, vous pouvez rechercher efficacement des attributs de profil Edge en temps réel, ce qui vous permet d’obtenir des expériences personnalisées et une prise de décision éclairée via les applications en aval.
