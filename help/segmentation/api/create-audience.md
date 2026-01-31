---
title: Créer un point d’entrée de l’API Audience
description: Découvrez comment créer des métadonnées pour une audience externe à l’aide de l’API .
hide: true
hidefromtoc: true
exl-id: e841a5f6-f406-4e1d-9e8a-acb861ba6587
source-git-commit: ea7fd13675a95941be7267f1cf75056b224efcd3
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 33%

---

# Créer un point d’entrée d’audience

Le point d’entrée de `/audiences` POST peut être utilisé pour créer les métadonnées d’une audience externe, ce qui permet à l’audience d’être visible dans Audience Portal. Vous devez utiliser ce point d’entrée si l’ingestion de l’audience sera gérée dans un service distinct, tel que l’ingestion par lots.

## Prise en main

>[!IMPORTANT]
>
>Les points d’entrée de ce guide sont précédés du préfixe `/core/ais`, par opposition à `/core/ups`.

Pour utiliser les API Experience Platform, vous devez avoir suivi le tutoriel [authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels API Experience Platform, comme illustré ci-dessous :

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation des sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

**Format d’API**

>[!IMPORTANT]
>
>Vous **devez** inclure le paramètre de requête `createAudienceMetaOnly=true` dans le cadre de la requête.

```http
POST /audiences?createAudienceMetaOnly=true
```

**Requête**

>[!IMPORTANT]
>
>Vous **devez** inclure l’en-tête `Accept: application/vnd.adobe.external.audiences+json; version=2` dans le cadre de la requête API.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/audiences?createAudienceMetaOnly=true \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'\
 -H 'Accept: application/vnd.adobe.external.audiences+json; version=2'
 -d '{
    "name": "Sample audience name",
    "description": "A sample description for the audience.",
    "audienceId": "4a815904-f2f9-4237-82fb-55605bcc2ad7",
    "namespace": "agora",
    "originName": "Agora_Collaboration"
 }'
```

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| `name` | Chaîne | Nom de l’audience. |
| `description` | Chaîne | Description facultative de l’audience. |
| `audienceId` | Chaîne | Identifiant généré en externe pour l’audience. |
| `namespace` | Chaîne | Espace de noms de l’audience. |
| `originName` | Chaîne | Nom de l’origine de l’audience. |

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des informations sur l’audience nouvellement créée.

```json
{
    "id": "6bb1ee15-8f64-49fd-bce3-d5c2f22f1f14",
    "name": "Sample audience name",
    "audienceId": "4a815904-f2f9-4237-82fb-55605bcc2ad7"
}
```

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| `id` | Chaîne | L’identifiant généré par le système pour l’audience. |
| `name` | Chaîne | Nom de l’audience que vous avez créée. |
| `audienceId` | Chaîne | Identifiant fourni en externe de l’audience que vous avez créée. |
