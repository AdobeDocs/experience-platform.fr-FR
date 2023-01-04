---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API;création de rapports;rapport de chevauchement de jeux de données;données de profil
title: Génération du rapport de chevauchement de jeux de données
type: Tutorial
description: Ce tutoriel décrit les étapes nécessaires à la génération du rapport de chevauchement de jeux de données à l’aide de l’API Real-time Customer Profile.
exl-id: 90894ed3-b09e-435d-a9e3-18fd6dc8e907
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 2%

---

# Génération du rapport de chevauchement de jeux de données

Le rapport de chevauchement de jeux de données offre une visibilité sur la composition de votre entreprise [!DNL Profile] stockez en exposant les jeux de données qui contribuent le plus à votre audience adressable (profils).

En plus de fournir des informations sur vos données, ce rapport peut vous aider à prendre des mesures pour optimiser l’utilisation de votre licence, comme définir une limite de durée de vie de certaines données.

Ce tutoriel décrit les étapes nécessaires à la génération du rapport de chevauchement de jeux de données à l’aide du [!DNL Real-Time Customer Profile] et interprétez les résultats pour votre organisation.

## Prise en main

Pour utiliser les API Adobe Experience Platform, vous devez d’abord renseigner la variable [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) pour rassembler les valeurs dont vous avez besoin pour les en-têtes requis. Pour en savoir plus sur les API Experience Platform, reportez-vous à la section [Prise en main de la documentation des API Platform](../../landing/api-guide.md).

Les en-têtes requis pour tous les appels API de ce tutoriel sont les suivants :

* `Authorization: Bearer {ACCESS_TOKEN}`: Le `Authorization` Un en-tête requiert un jeton d’accès précédé du mot `Bearer`. Une nouvelle valeur de jeton d’accès doit être générée toutes les 24 heures.
* `x-api-key: {API_KEY}`: Le `API Key` est également appelé `Client ID` et est une valeur qui ne doit être générée qu’une seule fois.
* `x-gw-ims-org-id: {ORG_ID}`: Le `IMS Org` est également appelé `Organization ID` et ne doit être généré qu’une seule fois.

Après avoir suivi le tutoriel sur l’authentification et rassemblé les valeurs des en-têtes requis, vous êtes prêt à lancer des appels à l’API client en temps réel.

## Générer un rapport de chevauchement de jeux de données à l’aide de la ligne de commande

Si vous maîtrisez l’utilisation de la ligne de commande, vous pouvez utiliser la requête cURL suivante pour générer le rapport de chevauchement de jeux de données en exécutant une requête de GET à la fonction `/previewsamplestatus/report/dataset/overlap`.

**Requête**

La requête suivante utilise la variable `date` pour renvoyer le rapport le plus récent pour la date spécifiée.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| Paramètre | Description |
|---|---|
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à la date, le rapport le plus récent pour cette date est renvoyé. Si un rapport n’existe pas pour la date spécifiée, une erreur d’état HTTP 404 (Not Found) est renvoyée. Si aucune date n’est spécifiée, le rapport le plus récent est renvoyé. Format : AAAA-MM-JJ. Exemple : `date=2024-12-31` |

**Réponse**

Une requête réussie renvoie un état HTTP 200 (OK) et le rapport de chevauchement de jeux de données. Le rapport comprend un `data` contenant des listes de jeux de données séparées par des virgules et leur nombre de profils respectif. Pour plus d’informations sur la lecture du rapport, reportez-vous à la section sur [interprétation des données de rapport de chevauchement de jeux de données](#interpret-the-report) plus loin dans ce tutoriel.

```json
{
    "data": {
        "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
        "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
        "5eeda0032af7bb19162172a7": 107
    },
    "reportTimestamp": "2021-04-19T19:55:31.147"
}
```

### Génération d’un rapport de chevauchement de jeux de données à l’aide de Postman

Postman est une plateforme collaborative de développement d’API qui permet de visualiser des appels d’API. Il peut être téléchargé gratuitement à partir du [Site web Postman](https://www.postman.com) et fournit une interface utilisateur facile à utiliser pour effectuer des appels API. Les captures d’écran suivantes utilisent l’interface de Postman.

**Requête**

Pour demander le rapport de chevauchement de jeux de données à l’aide de Postman, procédez comme suit :

* Dans la liste déroulante, sélectionnez GET comme type de requête.
* Saisissez les en-têtes requis dans la `KEY` column :
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* Saisissez les valeurs que vous avez générées lors de l’authentification dans la variable `VALUE` , en remplaçant les accolades (`{{ }}`) et tout contenu se trouvant dans les accolades.
* Entrez le chemin de la requête avec ou sans le paramètre `date` parameter:
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   or
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| Paramètre | Description |
|---|---|
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à la date, le rapport le plus récent pour cette date est renvoyé. Si un rapport n’existe pas pour la date spécifiée, une erreur d’état HTTP 404 (Not Found) est renvoyée. Si aucune date n’est spécifiée, le rapport le plus récent est renvoyé. <br/>Format : AAAA-MM-JJ. Exemple : `date=2024-12-31` |

Une fois le type de requête, les en-têtes, les valeurs et le chemin d’accès terminés, sélectionnez **Envoyer** pour envoyer la demande d’API et générer le rapport.

![](../images/dataset-overlap-report/postman-request.png)

**Réponse**

Une requête réussie renvoie un état HTTP 200 (OK) et le rapport de chevauchement de jeux de données. Le rapport comprend un `data` contenant des listes de jeux de données séparées par des virgules et leur nombre de profils respectif. Pour plus d’informations sur la lecture du rapport, reportez-vous à la section sur [interprétation des données de rapport de chevauchement de jeux de données](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## Interprétation des données de rapport de chevauchement de jeux de données {#interpret-the-report}

Le rapport de chevauchement de jeux de données généré fournit un horodatage indiquant la date et l’heure du rapport ainsi qu’un objet de données qui inclut des combinaisons uniques d’identifiants de jeu de données sous forme de listes séparées par des virgules. Les sections suivantes apportent des informations supplémentaires sur les composants du rapport.

### Horodatage du rapport

Le `reportTimestamp` correspond à la date fournie dans la requête API ou, si aucune date n’a été fournie, à l’horodatage du rapport le plus récent.

### Liste des identifiants des jeux de données

Le `data` inclut des combinaisons uniques d’identifiants de jeu de données sous la forme de listes séparées par des virgules avec le nombre de profils correspondant à cette combinaison de jeux de données.

>[!NOTE]
>
>La somme de tous les nombres de profils associés à chaque ligne du rapport de chevauchement de jeux de données doit être égale au nombre total de profils dans votre organisation.

Pour interpréter les résultats du rapport, prenez en compte l’exemple suivant :

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Ce rapport fournit les informations suivantes :

* Il existe 123 profils composés de données provenant des jeux de données suivants : `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Il existe 454 412 profils composés de données provenant de ces deux jeux de données : `5d92921872831c163452edc8` et `5eb2cdc6fa3f9a18a7592a98`.
* 107 profils sont constitués uniquement de données issues d’un jeu de données. `5eeda0032af7bb19162172a7`.
* Il y a un total de 454 642 profils dans l’organisation.

## Étapes suivantes

Après avoir suivi ce tutoriel, vous pouvez désormais générer le rapport de chevauchement de jeux de données à l’aide de l’API Real-time Customer Profile. Pour en savoir plus sur l’utilisation des données de profil dans l’API et l’interface utilisateur Experience Platform, commencez par lire la [Présentation des profils](../home.md).
