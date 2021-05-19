---
keywords: Experience Platform ; profil ; profil client en temps réel ; résolution des problèmes ; API ; rapports ; rapport de chevauchement des jeux de données ; données profil
title: Générer l'état de chevauchement des jeux de données
type: Tutorial
description: Ce didacticiel décrit les étapes nécessaires pour générer le rapport de chevauchement des jeux de données à l’aide de l’API Profil client en temps réel.
source-git-commit: f30f87527f5e903c851a140e7cbaad1964a48803
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 1%

---


# Générer l&#39;état de chevauchement des jeux de données

Le rapport de chevauchement des jeux de données permet de connaître la composition du magasin [!DNL Profile] de votre organisation en exposant les jeux de données qui contribuent le plus à votre audience adressable (profils).

En plus de fournir des informations sur vos données, ce rapport peut vous aider à prendre des mesures pour optimiser l&#39;utilisation de votre licence, comme la définition d&#39;une limite de durée de vie de certaines données.

Ce didacticiel décrit les étapes nécessaires pour générer le rapport de chevauchement des jeux de données à l&#39;aide de l&#39;API [!DNL Real-time Customer Profile] et interpréter les résultats pour votre organisation.

## Prise en main

Pour utiliser les API Adobe Experience Platform, vous devez d&#39;abord suivre le didacticiel d&#39;authentification [](https://www.adobe.com/go/platform-api-authentication-en) pour rassembler les valeurs nécessaires aux en-têtes requis. Pour en savoir plus sur les API Experience Platform, consultez la documentation [Prise en main des API de plateformes](../../landing/api-guide.md).

Les en-têtes requis pour tous les appels d’API de ce didacticiel sont les suivants :

* `Authorization: Bearer {ACCESS_TOKEN}`: L’ `Authorization` en-tête requiert un jeton d&#39;accès précédé du mot  `Bearer`. Une nouvelle valeur de jeton d&#39;accès doit être générée toutes les 24 heures.
* `x-api-key: {API_KEY}`: Cette valeur  `API Key` est également connue sous le nom de  `Client ID` et est une valeur qui ne doit être générée qu’une seule fois.
* `x-gw-ims-org-id: {IMS_ORG}`: La variable  `IMS Org` est également connue sous le nom d’une  `Organization ID` et ne doit être générée qu’une seule fois.

Après avoir suivi le didacticiel d’authentification et rassemblé les valeurs des en-têtes requis, vous êtes prêt à lancer des appels à l’API Client en temps réel.

## Générer un rapport de chevauchement de jeux de données à l’aide de la ligne de commande

Si vous connaissez bien l&#39;utilisation de la ligne de commande, vous pouvez utiliser la requête cURL suivante pour générer le rapport de chevauchement de jeux de données en exécutant une requête de GET à `/previewsamplestatus/report/dataset/overlap`.

**Requête**

La requête suivante utilise le paramètre `date` pour renvoyer le rapport le plus récent pour la date spécifiée.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=2021-04-19 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

| Paramètre | Description |
|---|---|
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à la date, le rapport le plus récent pour cette date est renvoyé. Si un rapport n’existe pas pour la date spécifiée, une erreur HTTP status 404 (Introuvable) est renvoyée. Si aucune date n’est spécifiée, le rapport le plus récent est renvoyé. Format : AAAA-MM-JJ. Exemple : `date=2024-12-31` |

**Réponse**

Une requête réussie renvoie l’état HTTP 200 (OK) et le rapport de chevauchement du jeu de données. Le rapport comprend un objet `data` contenant des listes de jeux de données séparées par des virgules et leur nombre de profils respectif. Pour plus d&#39;informations sur la manière de lire le rapport, consultez la section [interprétation des données du rapport de chevauchement de jeux de données](#interpret-the-report) plus loin dans ce didacticiel.

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

### Générer un état de chevauchement de jeux de données à l&#39;aide de Postman

Postman est une plate-forme collaborative de développement d&#39;API qui permet de visualiser les appels d&#39;API. Il peut être téléchargé gratuitement à partir du [site Web Postman](https://www.postman.com) et offre une interface utilisateur facile à utiliser pour effectuer des appels d&#39;API. Les captures d&#39;écran suivantes utilisent l&#39;interface de Postman.

**Requête**

Pour demander le rapport de chevauchement de jeux de données à l&#39;aide de Postman, procédez comme suit :

* Dans la liste déroulante, sélectionnez GET comme type de requête.
* Entrez les en-têtes requis dans la colonne `KEY` :
   * `Authorization`
   * `x-api-key`
   * `x-gw-ims-org-id`
* Entrez les valeurs que vous avez générées lors de l&#39;authentification dans la colonne `VALUE`, en remplaçant les accolades (`{{ }}`) et tout contenu qu&#39;elles contiennent.
* Entrez le chemin d&#39;accès à la demande avec ou sans le paramètre facultatif `date` :
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap`\
   or
   `https://platform.adobe.io/data/core/ups/previewsamplestatus/report/dataset/overlap?date=YYYY-MM-DD`

| Paramètre | Description |
|---|---|
| `date` | Indiquez la date du rapport à renvoyer. Si plusieurs rapports ont été exécutés à la date, le rapport le plus récent pour cette date est renvoyé. Si un rapport n’existe pas pour la date spécifiée, une erreur HTTP status 404 (Introuvable) est renvoyée. Si aucune date n’est spécifiée, le rapport le plus récent est renvoyé. <br/>Format : AAAA-MM-JJ. Exemple : `date=2024-12-31` |

Une fois le type de requête, les en-têtes, les valeurs et le chemin d’accès terminés, sélectionnez **Envoyer** pour envoyer la demande d’API et générer le rapport.

![](../images/dataset-overlap-report/postman-request.png)

**Réponse**

Une requête réussie renvoie l’état HTTP 200 (OK) et le rapport de chevauchement du jeu de données. Le rapport comprend un objet `data` contenant des listes de jeux de données séparées par des virgules et leur nombre de profils respectif. Pour plus d&#39;informations sur la façon de lire le rapport, consultez la section sur [l&#39;interprétation des données du rapport de chevauchement du jeu de données](#interpret-the-report).

![](../images/dataset-overlap-report/postman-response.png)

## Interpréter les données du rapport de chevauchement du jeu de données {#interpret-the-report}

Le rapport de chevauchement de jeux de données généré fournit un horodatage indiquant la date et l&#39;heure du rapport et un objet de données qui inclut des combinaisons uniques d&#39;ID de jeux de données en tant que listes séparées par des virgules. Les sections suivantes fournissent des informations supplémentaires sur les composants du rapport.

### Horodatage du rapport

`reportTimestamp` correspond à la date fournie dans la demande d’API ou, si aucune date n’a été fournie, à l’horodatage du rapport le plus récent.

### Liste des ID de jeu de données

L&#39;objet `data` inclut des combinaisons uniques d&#39;ID de jeu de données sous la forme de listes séparées par des virgules avec le nombre de profils correspondant à cette combinaison de jeux de données.

>[!NOTE]
>
>La somme de tous les comptes de profils associés à chaque ligne du rapport de chevauchement de jeux de données doit être égale au nombre total de profils dans votre organisation.

Pour interpréter les résultats du rapport, prenez en compte l’exemple suivant :

```json
  "5d92921872831c163452edc8,5da7292579975918a851db57,5eb2cdc6fa3f9a18a7592a98": 123,
  "5d92921872831c163452edc8,5eb2cdc6fa3f9a18a7592a98": 454412,
  "5eeda0032af7bb19162172a7": 107
```

Ce rapport fournit les informations suivantes :
* Il existe 123 profils composés de données provenant des jeux de données suivants : `5d92921872831c163452edc8`, `5da7292579975918a851db57`, `5eb2cdc6fa3f9a18a7592a98`.
* Il y a 454 412 profils composés de données provenant de ces deux ensembles de données : `5d92921872831c163452edc8` et `5eb2cdc6fa3f9a18a7592a98`.
* Il y a 107 profils qui ne sont composés que de données issues du jeu de données `5eeda0032af7bb19162172a7`.
* L&#39;organisation compte 454 642 profils.

## Étapes suivantes

Après avoir suivi ce didacticiel, vous pouvez désormais générer le rapport de chevauchement des jeux de données à l’aide de l’API Profil client en temps réel. Pour en savoir plus sur l’utilisation des données de Profil dans l’API et l’interface utilisateur Experience Platform, consultez la [documentation d’aperçu du Profil](../home.md).