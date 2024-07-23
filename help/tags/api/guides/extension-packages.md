---
title: Partage de modules d’extension privés dans l’API Reactor
description: Découvrez comment autoriser d’autres entreprises à partager des packages d’extension privés dans l’API Reactor.
source-git-commit: ea9a2bb00d3ce59e28ea4cda0d30945e77aa95cb
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 3%

---


# Partage de packages d’extension privés

>[!NOTE]
>
>Les utilisateurs disposant de l’autorisation `develop_extensions` dans l’organisation du propriétaire du package d’extension peuvent créer, répertorier et supprimer les autorisations d’utilisation du package d’extension pour ce package d’extension. Les utilisateurs d’une organisation autorisée disposant de l’autorisation `manage_properties` ne sont autorisés à répertorier que les autorisations d’utilisation des modules d’extension pour leur organisation et à mettre à jour leur état sur `accepted` s’ils souhaitent utiliser ce module d’extension, ou sur `rejected` s’ils ne souhaitent pas l’utiliser.

Les propriétaires des packages d’extension peuvent accorder l’autorisation à d’autres entreprises d’utiliser leurs versions privées via l’API Reactor. Une licence d’utilisation pour un package d’extension est accordée à chaque entreprise approuvée. Cette autorisation est valable pour toutes les versions privées actuelles et futures du package.

Ce guide donne un aperçu général de la configuration des autorisations d’utilisation des modules d’extension. Pour obtenir des instructions plus détaillées sur la gestion des autorisations dans l’API Reactor, y compris un exemple JSON de la structure d’une autorisation, reportez-vous au [guide de point d’entrée d’autorisation d’utilisation du package d’extension](../endpoints/extension-package-usage-authorizations.md).

## Création d’une autorisation {#create-authorization}

Pour créer une autorisation, vous devez disposer du droit `develop_extensions`. L’exemple suivant montre comment créer une autorisation d’utilisation de package d’extension pour un package d’extension à l’aide de `authorized_org_id` de la société que vous souhaitez autoriser.

**Format d’API**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Paramètre | Description |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | `ID` du package d’extension pour lequel vous souhaitez créer une autorisation. |

{style="table-layout:auto"}

**Requête**

La requête suivante crée une nouvelle autorisation de package d’extension pour la société spécifiée.

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
| `attributes.authorized_org_id` | `ID` de l’organisation à autoriser. |

{style="table-layout:auto"}

L’état initial de l’autorisation se trouve à l’étape `pending_approval` . Avant d’utiliser le package d’extension, l’entreprise doit approuver l’autorisation. Les utilisateurs de la société peuvent parcourir le package d’extension privé pendant que l’autorisation est en attente d’approbation, mais ils ne peuvent pas l’installer et ne peuvent pas le trouver dans leur catalogue d’extensions.

## Approbation d’une autorisation {#approve-authorization}

Pour approuver une autorisation, vous devez disposer des droits `manage_properties`. En tant qu’entreprise autorisée, vous devrez envoyer une demande de PATCH à l’autorisation d’utilisation du package d’extension, y compris l’ `ID` de l’autorisation et définir l’état sur `approved`.

**Format d’API**

```http
PATCH //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Paramètre | Description |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | `ID` de l’autorisation que vous souhaitez approuver. |

{style="table-layout:auto"}

**Requête**

La requête de PATCH suivante définit le `state` d’une autorisation sur `approved`.

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

Une fois l’autorisation approuvée, en tant qu’entreprise autorisée, vous pouvez désormais installer le package d’extension sur vos propriétés.

>[!NOTE]
>
>Si l’autorisation est refusée, la société autorisée ne pourra pas utiliser le package d’extension.

## Suppression d’une autorisation {#delete-authorization}

En tant que propriétaire d’un package d’extension, vous pouvez révoquer l’autorisation à tout moment en supprimant l’autorisation d’utilisation du package d’extension. Cela empêchera l’entreprise autorisée d’afficher les versions privées du package d’extension dans le catalogue et de l’installer sur ses propriétés. Toutefois, les versions privées déjà installées continueront à fonctionner comme prévu après la suppression.

**Format d’API**

```http
DELETE //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Paramètre | Description |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | `ID` de l’autorisation que vous souhaitez supprimer. |

{style="table-layout:auto"}

**Requête**

La requête de DELETE suivante supprime les privilèges d’autorisation pour une société.

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
```
