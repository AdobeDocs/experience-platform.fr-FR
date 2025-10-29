---
title: Partage de packages d’extension privés dans l’API Reactor
description: Découvrez comment autoriser d’autres entreprises à partager des packages d’extension privés dans l’API Reactor.
exl-id: 3300a630-6d22-46e1-8b1b-b5d12a3ea44c
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 3%

---

# Partage de packages d’extension privés

>[!NOTE]
>
>Les utilisateurs disposant de l’autorisation `develop_extensions` dans l’organisation du propriétaire du package d’extension peuvent créer, répertorier et supprimer les autorisations d’utilisation de package d’extension pour ce package d’extension. Les utilisateurs d’une organisation autorisée qui possèdent l’autorisation `manage_properties` sont uniquement autorisés à répertorier les autorisations d’utilisation des packages d’extension pour leur organisation et à mettre à jour leur état pour `accepted` s’ils souhaitent utiliser ce package d’extension ou pour `rejected` s’ils ne souhaitent pas l’utiliser.

Les propriétaires de packages d’extension peuvent accorder à d’autres sociétés l’autorisation d’utiliser leurs versions privées via l’API Reactor. Une licence d’utilisation pour un package d’extension est accordée à chaque entreprise approuvée, et cette autorisation est valable pour toutes les versions privées actuelles et futures du package.

Ce guide fournit une présentation détaillée de la configuration des autorisations d’utilisation des packages d’extension. Pour obtenir des instructions plus détaillées sur la gestion des autorisations dans l’API Reactor, et notamment un exemple JSON de la structure d’une autorisation, consultez le [guide des points d’entrée d’autorisation d’utilisation du package d’extension](../endpoints/extension-package-usage-authorizations.md).

## Création d’une autorisation {#create-authorization}

Pour créer une nouvelle autorisation, vous devez disposer du droit `develop_extensions`. L’exemple suivant montre comment créer une autorisation d’utilisation de package d’extension pour un package d’extension à l’aide du `authorized_org_id` de la société que vous souhaitez autoriser.

**Format d’API**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Paramètre | Description |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | `ID` du package d’extension pour lequel vous souhaitez créer une autorisation. |

{style="table-layout:auto"}

**Requête**

La requête suivante crée une autorisation de package d’extension pour la société spécifiée.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| Propriété | Description |
| --- | --- |
| `attributes.authorized_org_id` | `ID` de l’organisation que vous souhaitez autoriser. |

{style="table-layout:auto"}

L’état initial de l’autorisation en est à l’étape `pending_approval`. Avant d’utiliser le package d’extension, la société doit approuver l’autorisation. Les utilisateurs de la société peuvent parcourir le package d’extension privé lorsque l’autorisation est en attente d’approbation, mais ils ne peuvent pas l’installer et ne le trouvent pas dans leur catalogue d’extensions.

## Valider une autorisation {#approve-authorization}

Pour approuver une autorisation, vous devez disposer des droits `manage_properties`. En tant que société agréée, vous devez envoyer une requête PATCH à l’autorisation d’utilisation du package d’extension, y compris l’`ID` de l’autorisation, et définir l’état sur `approved`.

**Format d’API**

```http
PATCH //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Paramètre | Description |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | `ID` de l’autorisation que vous souhaitez approuver. |

{style="table-layout:auto"}

**Requête**

La requête PATCH suivante définit le `state` d’une autorisation sur `approved`.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "state": "approved"
            },
            "id": ":extension_package_usage_authorization_id",
            "type": "extension_package_usage_authorizations"
        }
      }
```

Une fois l’autorisation approuvée, en tant que société autorisée, vous pouvez installer le package d’extension sur vos propriétés.

>[!NOTE]
>
>Si l’autorisation est refusée, la société autorisée ne pourra pas utiliser le package d’extension.

## Suppression d’une autorisation {#delete-authorization}

En tant que propriétaire d’un package d’extension, vous pouvez révoquer l’autorisation à tout moment en supprimant l’autorisation d’utilisation du package d’extension. Cela empêchera la société autorisée de visualiser les versions privées du package d’extension dans le catalogue et de l’installer sur leurs propriétés. Cependant, les versions privées déjà installées continueront à fonctionner comme prévu après la suppression.

**Format d’API**

```http
DELETE //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Paramètre | Description |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | `ID` de l’autorisation à supprimer. |

{style="table-layout:auto"}

**Requête**

La requête DELETE suivante supprime les privilèges d’autorisation pour une société.

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
```
