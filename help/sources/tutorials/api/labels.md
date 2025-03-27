---
title: Appliquez des libellés d’accès pour gérer l’accès des utilisateurs aux flux de données sources à l’aide de l’API
description: Découvrez comment utiliser l’API Flow Service pour appliquer des libellés d’accès et gérer l’accès des utilisateurs et utilisatrices à vos flux de données sources.
exl-id: 572d6838-3e4c-4fd5-89fa-32cad6280325
source-git-commit: f57fa04e668fa9c61b9b15778e74969edffae0fa
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 11%

---

# Appliquez des libellés d’accès pour gérer l’accès des utilisateurs aux flux de données sources à l’aide de l’API

Vous pouvez utiliser les fonctionnalités fournies par [contrôle d’accès basé sur les attributs](../../../access-control/abac/overview.md) dans Real-Time CDP pour appliquer des libellés à vos flux de données sources. Grâce à cette fonctionnalité, vous pouvez vous assurer que seul un sous-ensemble d’utilisateurs de votre organisation a accès à des flux de données sources spécifiques.

Lorsque vous ajoutez un libellé d’accès à un flux de données spécifique, seuls les utilisateurs et utilisatrices ayant accès à un rôle auquel ce libellé est affecté peuvent afficher et modifier ce flux de données. Si un flux de données de sources n’est marqué d’aucun libellé, il est visible par tous les utilisateurs appartenant à votre organisation. Par exemple, si vous appliquez le libellé C12 à un flux de données, les utilisateurs affectés à un rôle qui ne dispose pas du libellé C12 ne pourront pas afficher et modifier le flux de données avec le libellé C12.

Lisez ce guide pour plus d’informations sur la manière d’appliquer des libellés d’accès à vos flux de données sources à l’aide de l’API [[!DNL Flow Service] ](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Commencer

Avant d’utiliser des libellés de contrôle d’accès, familiarisez-vous d’abord avec les fonctionnalités du contrôle d’accès basé sur les attributs. Pour plus d’informations, consultez la documentation suivante :

* [Présentation du contrôle d’accès basé sur les attributs](../../../access-control/abac/overview.md)
* [Guide complet du contrôle d’accès basé sur les attributs](../../../access-control/abac/end-to-end-guide.md)
* [Guide de l’API de contrôle d’accès basé sur les attributs](../../../access-control/abac/api/overview.md)
* [Glossaire des étiquettes dʼutilisation des données](../../../data-governance/labels/reference.md)

## Application de libellés d’accès aux flux de données sources

>[!NOTE]
>
>* Vous ne pouvez pas appliquer de libellés à une exécution de flux. Toutefois, les exécutions de flux héritent des libellés que vous appliquez au flux de données parent.
>
>* Si vous ne disposez pas d’un accès en lecture seule à un flux de données, vous ne pourrez pas non plus afficher ses exécutions de flux correspondantes.

Pour ajouter un libellé à un flux de données, envoyez une requête PATCH au point d’entrée `/flows` et indiquez l’identifiant du flux de données à mettre à jour.

**Format d’API**

```http
PATCH /flows/{FLOW_ID}
```

| Paramètre | Description |
| --- | --- |
| `{FLOW_ID}` | Identifiant du flux de données à mettre à jour. |

**Requête**

>[!TIP]
>
>Pour effectuer une requête PATCH, indiquez la version/l’etag du flux de données que vous souhaitez mettre à jour comme paramètre d’en-tête `if-match`.

La requête suivante ajoute le libellé C12 au flux de données avec l’ID : `84224def-1e2a-4d95-9ea2-132d697ed2aa`.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/84224def-1e2a-4d95-9ea2-132d697ed2aa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'if-match: "c5002e0e-0000-0200-0000-67a3c3b70000"'
  -d '[
    {
        "op": "add",
        "path": "/labels",
        "value": ["core/C12"]
    }
]'
```

| Propriété | Description |
| --- | --- |
| `op` | Appel d’opération utilisé pour définir l’action nécessaire pour mettre à jour la connexion. Les opérations comprennent : `add`, `replace` et `remove`. |
| `path` | Partie du flux de données à mettre à jour. |
| `value` | Nouvelle valeur avec laquelle vous souhaitez mettre à jour votre propriété. |



**Réponse**

Une réponse réussie renvoie votre identifiant de flux et une balise dʼentité mise à jour. Vous pouvez vérifier la mise à jour en adressant une requête GET à l’API [!DNL Flow Service] et en y indiquant votre identifiant de flux.

```json
{
    "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

Une fois que vous avez correctement configuré les libellés d’accès à votre flux de données, tout utilisateur n’ayant pas accès à ce libellé ne pourra plus récupérer le flux de données. Par exemple, si un utilisateur qui n’est pas configuré avec le libellé C12 effectue une requête GET pour récupérer le flux de données avec l’ID : `84224def-1e2a-4d95-9ea2-132d697ed2aa`, il recevra la réponse suivante :

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-1439-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "detailed-message": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
        "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
        "request-id": "{REQUEST_ID}",
        "type": "flows"
    },
    "errorMessage": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
    "errorDetails": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again."
}
```

De même, les utilisateurs et utilisatrices qui n’ont pas accès au libellé C12 ne pourront pas effectuer de requêtes PATCH ou DELETE par rapport au flux de données mis à jour et recevront la réponse suivante :

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-2120-403",
    "title": "Forbidden",
    "status": 403,
    "report": {
        "detailed-message": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
        "request-id": "{REQUEST_ID}"
    },
    "errorMessage": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
    "errorDetails": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again."
}
```

## Étapes suivantes

Vous savez désormais comment appliquer des libellés d’accès à vos flux de données sources. Vous pouvez désormais vous assurer que seul un groupe spécifique d’utilisateurs de votre organisation peut accéder à certains flux de données sources. Pour plus d’informations, consultez la documentation suivante :

* [Appliquer des libellés d’accès aux flux de données sources dans l’interface utilisateur](../ui/labels.md)
* [Présentation du contrôle d’accès](../../../access-control/home.md)
