---
solution: Experience Platform
title: Guide de segmentation en flux continu
description: Découvrez la segmentation en flux continu, notamment en quoi elle consiste, comment créer une audience évaluée à l’aide de la segmentation en flux continu et comment afficher vos audiences créées à l’aide de la segmentation en flux continu.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: cd22213be0dbc2e5a076927e560f1b23b467b306
workflow-type: tm+mt
source-wordcount: '2013'
ht-degree: 19%

---

# Guide de segmentation en flux continu

>[!BEGINSHADEBOX]

>[!NOTE]
>
>Les critères d’éligibilité de la segmentation en flux continu ont été mis à jour le 20 mai 2025.

+++Mises à jour d’éligibilité

>[!IMPORTANT]
>
>Toutes les définitions de segment existantes qui sont actuellement évaluées à l’aide de la segmentation Edge ou en flux continu continueront à fonctionner en l’état, sauf si elles sont modifiées ou mises à jour.

## Ensemble de règles {#ruleset}

Les définitions de segment **nouvelles ou modifiées** qui correspondent aux ensembles de règles suivants **plus** seront évaluées à l’aide de la segmentation Edge ou en flux continu. Au lieu de cela, elles seront évaluées à l’aide de la segmentation par lots.

- Un événement unique avec une fenêtre temporelle de plus de 24 heures.
   - Activez une audience avec tous les profils qui ont consulté une page web au cours des 3 derniers jours.
- Un événement unique sans fenêtre temporelle
   - Activez une audience avec tous les profils qui ont consulté une page web.

## Fenêtre temporelle {#time-window}

Pour évaluer une audience avec segmentation en flux continu, elle **doit** être limitée dans une fenêtre temporelle de 24 heures.

## Inclusion de données par lot dans des audiences en flux continu {#include-batch-data}

Avant cette mise à jour, vous pouviez créer une définition d’audience de diffusion en continu qui combinait des sources de données par lots et en flux continu. Cependant, avec la dernière mise à jour, la création d’une audience avec des sources de données par lots et par flux sera évaluée à l’aide de la segmentation par lots.

Si vous devez évaluer une définition de segment à l’aide de la segmentation en flux continu ou Edge qui correspond à l’ensemble de règles mis à jour, vous devez créer explicitement un lot et un ensemble de règles en flux continu et les combiner à l’aide d’un segment de segments. Ce jeu de règles par lot **doit** est basé sur un schéma de profil.

Supposons, par exemple, que vous ayez deux audiences, avec une audience contenant des données de schéma de profil et l’autre des données de schéma d’événement d’expérience de logement :

| Audience | Schéma | Type de source | Query definition | ID de l’audience |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Résidents californiens | Profile | Lot | L&#39;adresse personnelle est dans l&#39;état de la Californie | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Passages en caisse récents | Événement d’expérience | Diffusion en continu | A effectué au moins un passage en caisse au cours des dernières 24 heures | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Si vous souhaitez utiliser le composant par lot dans votre audience de diffusion en continu, vous devez faire référence à l’audience par lot à l’aide d’un segment de segments.

Voici un exemple d’ensemble de règles qui combine les deux audiences :

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

L’audience résultante *sera* évaluée à l’aide de la segmentation en flux continu, car elle exploite l’appartenance de l’audience par lots en se référant au composant d’audience par lots.

Cependant, si vous souhaitez combiner deux audiences avec des données d’événement, vous **ne pouvez pas** vous contenter de combiner les deux événements. Vous devez créer les deux audiences, puis créer une autre audience qui utilise `inSegment` pour faire référence à ces deux audiences.

Supposons, par exemple, que vous ayez deux audiences, avec les deux audiences hébergeant des données de schéma d’événement d’expérience :

| Audience | Schéma | Type de source | Query definition | ID de l’audience |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Abandons récents | Événement d’expérience | Lot | A au moins un événement d’abandon au cours des dernières 24 heures | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Passages en caisse récents | Événement d’expérience | Diffusion en continu | A effectué au moins un passage en caisse au cours des dernières 24 heures | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Dans ce cas, vous devez créer une troisième audience comme suit :

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

>[!IMPORTANT]
>
>Toutes les définitions de segment existantes qui correspondent aux ensembles de règles restent évaluées à l’aide de la segmentation en flux continu ou Edge jusqu’à ce qu’elles soient modifiées.
>
>En outre, toutes les définitions de segment existantes qui répondent actuellement aux autres critères d’évaluation de segmentation en flux continu ou Edge resteront évaluées avec la segmentation en flux continu ou Edge.

## Politique de fusion {#merge-policy}

Toutes les définitions de segment **nouvelles ou modifiées** qui remplissent les critères de segmentation Edge ou en flux continu **doivent** doivent être sur la politique de fusion « Active-on-Edge ».

S’il n’existe aucun jeu de politiques de fusion actif, vous devez [configurer votre politique de fusion](../../profile/merge-policies/ui-guide.md#configure) et la définir sur Active-On-Edge (active sur le bord).


+++

>[!ENDSHADEBOX]

La segmentation en flux continu est la possibilité d’évaluer les audiences dans Adobe Experience Platform en temps quasi réel tout en se concentrant sur la richesse des données.

Avec la segmentation en flux continu, la qualification d’audience se produit désormais lorsque les données en flux continu entrent dans Experience Platform, ce qui évite d’avoir à planifier et à exécuter des tâches de segmentation. Vous pouvez ainsi évaluer les données telles qu’elles sont transmises à Experience Platform, ce qui permet de maintenir automatiquement à jour l’appartenance à une audience.

## Jeux de règles éligibles {#rulesets}

>[!IMPORTANT]
>
>Pour utiliser la segmentation en flux continu, vous **devez** utiliser une politique de fusion « Active-on-Edge ». Pour plus d’informations sur les politiques de fusion, consultez la [ présentation des politiques de fusion ](../../profile/merge-policies/overview.md).

Un ensemble de règles peut être segmenté en flux continu s’il répond à l’un des critères décrits dans le tableau suivant.

>[!NOTE]
>
>Pour que la segmentation en flux continu fonctionne, vous devez activer la segmentation planifiée pour l’organisation. Pour plus d’informations sur l’activation de la segmentation planifiée, reportez-vous à [présentation d’Audience Portal](../ui/audience-portal.md#scheduled-segmentation).

| Type de requête | Détails | Requête | Exemple |
| ---------- | ------- | ----- | ------- |
| Événement unique dans une fenêtre temporelle de moins de 24 heures | Toute définition de segment qui fait référence à un seul événement entrant dans une fenêtre temporelle de moins de 24 heures. | `CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![Un exemple d’événement unique dans une fenêtre temporelle relative s’affiche.](../images/methods/streaming/single-event.png) |
| Profil uniquement | Toute définition de segment qui ne fait référence qu’à un attribut de profil. | `homeAddress.country.equals("US", false)` | ![Exemple d’attribut de profil affiché.](../images/methods/streaming/profile-attribute.png) |
| Événement unique avec un attribut de profil dans une fenêtre temporelle relative de moins de 24 heures | Toute définition de segment qui fait référence à un seul événement entrant, avec un ou plusieurs attributs de profil, et qui se produit dans une fenêtre temporelle relative de moins de 24 heures. | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![Un exemple d’événement unique avec un attribut de profil dans une fenêtre temporelle relative s’affiche.](../images/methods/streaming/single-event-with-profile-attribute.png) |
| Plusieurs événements dans une fenêtre temporelle relative de 24 heures | Toute définition de segment qui fait référence à plusieurs événements **au cours des dernières 24 heures** et (éventuellement) comporte un ou plusieurs attributs de profil. | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("directMarketing.emailClicked", false)) WHEN(today), C1: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![Un exemple de plusieurs événements avec un attribut de profil s’affiche.](../images/methods/streaming/multiple-events-with-profile-attribute.png) |

Une définition de segment **non** est éligible pour la segmentation en flux continu dans les scénarios suivants :

- La définition de segment inclut des segments ou des caractéristiques Adobe Audience Manager (AAM).
- La définition de segment comprend plusieurs entités (requêtes d’entités multiples).
- La définition de segment comprend une combinaison d’un événement unique et d’un événement `inSegment`.
   - Par exemple, vous pouvez enchaîner les éléments suivants dans un seul ensemble de règles : `inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and  CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false))  WHEN(<= 24 hours before now)])`.
- La définition de segment utilise « Ignorer l’année » dans le cadre de ses contraintes de temps.

Veuillez noter les instructions suivantes qui s’appliquent aux requêtes de segmentation en flux continu :

| Type de requête | Instruction |
| ---------- | -------- |
| Ensemble de règles d’événement unique | L’intervalle de recherche en amont est limité à **un jour**. |
| Requête avec historique des événements | <ul><li>L’intervalle de recherche en amont est limité à **un jour**.</li><li>Une condition d’ordre du temps stricte **doit** exister entre les événements.</li><li>Les requêtes comportant au moins un événement annulé sont prises en charge. Cependant, l’événement entier **ne peut pas** être annulé.</li></ul> |

Si une définition de segment est modifiée de sorte qu’elle ne répond plus aux critères de la segmentation en flux continu, elle passe automatiquement de « Diffusion en flux continu » à « Lots ».

De plus, la disqualification de segment, tout comme la qualification de segment, se produit en temps réel. Par conséquent, si une audience n’est plus admissible pour être un segment, elle sera immédiatement disqualifiée. Par exemple, si la définition de segment demande « Tous les utilisateurs et utilisatrices qui ont acheté des chaussures rouges au cours des trois dernières heures », tous les profils initialement qualifiés pour la définition de segment seront disqualifiés après trois heures.

### Combinaison d’audiences {#combine-audiences}

Pour combiner des données provenant de sources par lots et en flux continu, vous devez séparer les composants par lots et en flux continu en audiences distinctes.

Par exemple, prenons en compte les deux exemples d’audiences suivants :

| Audience | Schéma | Type de source | Query definition | ID de l’audience |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Résidents californiens | Profile | Lot | L&#39;adresse personnelle est dans l&#39;état de la Californie | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Passages en caisse récents | Événement d’expérience | Diffusion en continu | A effectué au moins un passage en caisse au cours des dernières 24 heures | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Si vous souhaitez utiliser le composant par lot dans votre audience de diffusion en continu, vous devez faire référence à l’audience par lot à l’aide d’un segment de segments.

Voici un exemple d’ensemble de règles qui combine les deux audiences :

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

L’audience résultante *sera* évaluée à l’aide de la segmentation en flux continu, car elle exploite l’appartenance de l’audience par lots en se référant au composant d’audience par lots.

Cependant, si vous souhaitez combiner deux audiences avec des données d’événement, vous **ne pouvez pas** vous contenter de combiner les deux événements. Vous devez créer les deux audiences, puis créer une autre audience qui utilise `inSegment` pour faire référence à ces deux audiences.

Supposons, par exemple, que vous ayez deux audiences, avec les deux audiences hébergeant des données de schéma d’événement d’expérience :

| Audience | Schéma | Type de source | Query definition | ID de l’audience |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Abandons récents | Événement d’expérience | Lot | A au moins un événement d’abandon au cours des dernières 24 heures | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Passages en caisse récents | Événement d’expérience | Diffusion en continu | A effectué au moins un passage en caisse au cours des dernières 24 heures | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Dans ce cas, vous devez créer une troisième audience comme suit :

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

## Créer une audience {#create-audience}

Vous pouvez créer une audience évaluée à l’aide de la segmentation en flux continu à l’aide de l’API Segmentation Service ou via Audience Portal dans l’interface utilisateur.

Une définition de segment peut être activée pour le streaming si elle correspond à l’un des [ensembles de règles éligibles](#eligible-rulesets).

>[!BEGINTABS]

>[!TAB API Segmentation Service]

**Format d’API**

```http
POST /segment/definitions
```

**Requête**

+++ Exemple de requête pour créer une définition de segment activée pour la segmentation en flux continu

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People in the USA",
        "description: "An audience that looks for people who live in the USA",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "homeAddress.country = \"US\""
        },
        "evaluationInfo": {
            "batch": {
                "enabled": false
            },
            "continuous": {
                "enabled": true
            },
            "synchronous": {
                "enabled": false
            }
        },
        "schema": {
            "name": "_xdm.context.profile"
        }
     }'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de la définition de segment que vous venez de créer.

+++Exemple de réponse lors de la création d’une définition de segment.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People in the USA",
    "description": "An audience that looks for people who live in the USA",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "homeAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

+++

Vous trouverez plus d’informations sur l’utilisation de ce point d’entrée dans le [guide de point d’entrée de définition de segment](../api/segment-definitions.md).

>[!TAB Audience Portal]

Dans Audience Portal, sélectionnez **[!UICONTROL Créer une audience]**.

![Le bouton Créer une audience est mis en surbrillance dans le portail d’audiences.](../images/methods/streaming/select-create-audience.png)

Une fenêtre contextuelle s’affiche. Sélectionnez **[!UICONTROL Créer des règles]** pour accéder au créateur de segments.

![Le bouton Créer des règles est mis en surbrillance dans la fenêtre contextuelle de création d’audience.](../images/methods/streaming/select-build-rules.png)

Dans le créateur de segments, créez une définition de segment qui correspond à l’un des [ensembles de règles éligibles](#eligible-rulesets). Si la définition de segment est admissible pour la segmentation en flux continu, vous pourrez sélectionner **[!UICONTROL Diffusion en flux continu]** comme **[!UICONTROL Méthode d’évaluation]**.

![La définition de segment s’affiche. Le type d’évaluation est mis en surbrillance, montrant que la définition de segment peut être évaluée à l’aide de la segmentation en flux continu.](../images/methods/streaming/streaming-evaluation-method.png)

Pour en savoir plus sur la création de définitions de segment, consultez le [guide du créateur de segments](../ui/segment-builder.md)

>[!ENDTABS]

## Récupérer des audiences {#retrieve-audiences}

Vous pouvez récupérer toutes les audiences évaluées à l’aide de la segmentation en flux continu en utilisant l’API Segmentation Service ou en passant par Audience Portal dans l’interface utilisateur.

>[!BEGINTABS]

>[!TAB API Segmentation Service]

Récupérez une liste de toutes les définitions de segment évaluées à l’aide de la segmentation en flux continu au sein de votre organisation en envoyant une requête GET au point d’entrée `/segment/definitions`.

**Format d’API**

Vous devez inclure le paramètre de requête `evaluationInfo.synchronous.enabled=true` dans le chemin de requête pour récupérer les définitions de segment évaluées à l’aide de la segmentation en flux continu.

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**Requête**

+++ Exemple de requête pour répertorier toutes les définitions de segment activées pour la diffusion en continu

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie le statut HTTP 200 avec un tableau de définitions de segment dans votre organisation qui sont activées pour la segmentation en flux continu.

+++Exemple de réponse contenant une liste de toutes les définitions de segment activées pour la segmentation en flux continu dans votre organisation

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

Vous trouverez des informations plus détaillées sur la définition de segment renvoyée dans le [guide de point d’entrée des définitions de segment](../api/segment-definitions.md).

+++

>[!TAB Audience Portal]

Vous pouvez récupérer toutes les audiences activées pour la segmentation en flux continu au sein de votre organisation en utilisant les filtres d’Audience Portal. Sélectionnez l’icône ![icône de filtre](../../images/icons/filter.png) pour afficher la liste des filtres.

![L’icône de filtre est mise en surbrillance dans Audience Portal.](../images/methods/filter-audiences.png)

Dans les filtres disponibles, accédez à **[!UICONTROL Fréquence des mises à jour]** et sélectionnez « [!UICONTROL &#x200B; Diffusion en continu &#x200B;]. L’utilisation de ce filtre affiche toutes les audiences de votre organisation qui sont évaluées à l’aide de la segmentation en flux continu.

![La fréquence de mise à jour en flux continu est sélectionnée, affichant toutes les audiences de l’organisation qui sont évaluées à l’aide de la segmentation en flux continu.](../images/methods/streaming/filter-streaming.png)

Pour en savoir plus sur l’affichage des audiences dans Experience Platform, consultez le guide [Audience Portal](../ui/audience-portal.md).

>[!ENDTABS]

## Détails de l’audience {#audience-details}

Vous pouvez afficher les détails d’une audience spécifique évaluée à l’aide de la segmentation en flux continu en la sélectionnant dans Audience Portal.

Après avoir sélectionné une audience sur Audience Portal, la page des détails de l’audience s’affiche. Elle affiche des informations sur l’audience, notamment un résumé des détails de l’audience, la quantité de profils qualifiés au fil du temps, ainsi que les destinations vers lesquelles l’audience a été activée.

![La page Détails de l’audience s’affiche pour une audience évaluée à l’aide de la segmentation en flux continu.](../images/methods/streaming/audience-details.png)

Pour les audiences activées pour la diffusion en continu, la vignette **[!UICONTROL Profils au fil du temps]** s’affiche, affichant le total des mesures qualifiées et les nouvelles mesures d’audience mises à jour.

La mesure **[!UICONTROL Total qualifié]** représente le nombre total d’audiences qualifiées, en fonction des évaluations de lot et de flux continu pour cette audience.

La mesure **[!UICONTROL Nouvelle audience mise à jour]** est représentée par un graphique linéaire qui indique le changement de taille d’audience par le biais de la segmentation en flux continu. Vous pouvez ajuster la liste déroulante pour afficher les dernières 24 heures, la semaine dernière ou les 30 derniers jours.

![La carte Profils au fil du temps est mise en surbrillance.](../images/methods/streaming/profiles-over-time.png)

Pour plus d’informations sur les détails de l’audience, veuillez lire la [présentation du portail Audience](../ui/audience-portal.md#audience-details).

## Étapes suivantes

Ce guide explique le fonctionnement des définitions de segment activées pour la diffusion en continu sur Adobe Experience Platform et comment surveiller les définitions de segment activées pour la diffusion en continu.

Pour en savoir plus sur l’utilisation de l’interface utilisateur d’Adobe Experience Platform, veuillez lire le [guide d’utilisation de la segmentation](./overview.md).

Pour les questions fréquentes sur la segmentation en flux continu, veuillez lire la section [segmentation en flux continu) de la FAQ](../faq.md#streaming-segmentation).
