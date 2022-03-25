---
keywords: OCR;présence de texte;reconnaissance optique de caractères
solution: Intelligent Services
title: Présence de texte et reconnaissance optique des caractères
topic-legacy: Developer guide
description: Dans l’API Content and Commerce AI, le service Text Presence / Optical Character Reconnaissance (OCR) peut indiquer si du texte est présent dans une image donnée. Si du texte est présent, la reconnaissance optique des caractères peut renvoyer le texte.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 4%

---

# Présence de texte et reconnaissance optique des caractères

>[!NOTE]
>
>Content and Commerce AI est en version bêta. La documentation peut être modifiée.

Lorsqu’une image est fournie, le service de reconnaissance de caractères optique/présence de texte peut indiquer si du texte est présent dans l’image. Si du texte est présent, la reconnaissance optique des caractères peut renvoyer le texte.

L’image suivante a été utilisée dans l’exemple de requête illustré dans ce document :

![image de test](../images/shef.jpeg)

**Format d’API**

```http
POST /services/v1/predict
```

**Requête**

La requête suivante vérifie si du texte est présent en fonction de l’image d’entrée fournie dans le payload. Pour plus d’informations sur les paramètres d’entrée affichés, reportez-vous au tableau ci-dessous de l’exemple de payload.

>[!CAUTION]
>
>`analyzer_id` détermine [!DNL Sensei Content Framework] est utilisée. Vérifiez que vous disposez des `analyzer_id` avant d’effectuer votre requête. Contactez l’équipe bêta de Content and Commerce AI pour recevoir votre `analyzer_id` pour ce service.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file=@TestImage.jpg \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
    "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
    "parameters": {
      "application-id": "1234",
      "content-type": "inline",
      "encoding": "jpeg",
      "threshold": "0",
      "top-N": "0",
      "custom": {},
      "data": [{
        "content-id": "0987",
        "content": "inline-image",
        "content-type": "inline",
        "encoding": "jpeg",
        "threshold": "0",
        "top-N": "0",
        "historic-metadata": [],
        "custom": {}
        }]
      }
    }]
  }'
```

| Propriété | Description | Obligatoire |
| --- | --- | --- |
| `analyzer_id` | Le [!DNL Sensei] ID de service sous lequel votre requête est déployée. Cet identifiant détermine laquelle de la variable [!DNL Sensei Content Frameworks] sont utilisées. Pour les services personnalisés, contactez l’équipe Content and Commerce AI pour configurer un identifiant personnalisé. | Oui |
| `application-id` | L’identifiant de l’application créée. | Oui |
| `data` | Tableau contenant un objet JSON dont chaque objet du tableau représente une image transmise. Tous les paramètres transmis dans le cadre de ce tableau remplacent les paramètres globaux spécifiés en dehors de la variable `data` tableau. Toutes les propriétés restantes décrites ci-dessous dans ce tableau peuvent être remplacées dans . `data`. | Oui |
| `language` | Langue du texte de saisie. La valeur par défaut est `en`. | Non |
| `content-type` | Utilisé pour indiquer si l’entrée fait partie du corps de la requête ou une URL signée pour un compartiment S3. La valeur par défaut de cette propriété est `inline`. | Non |
| `encoding` | Format de fichier de l’image d’entrée. Actuellement, seules les images JPEG et PNG peuvent être traitées. La valeur par défaut de cette propriété est `jpeg`. | Non |
| `threshold` | Seuil de score (0 à 1) au-dessus duquel les résultats doivent être renvoyés. Utiliser la valeur `0` pour renvoyer tous les résultats. La valeur par défaut de cette propriété est `0`. | Non |
| `top-N` | Nombre de résultats à renvoyer (ne peut pas être un entier négatif). Utiliser la valeur `0` pour renvoyer tous les résultats. Utilisé conjointement avec `threshold`, le nombre de résultats renvoyés est le plus petit des jeux de limites. La valeur par défaut de cette propriété est `0`. | Non |
| `custom` | Tous les paramètres personnalisés à transmettre. Cette propriété requiert un objet JSON valide pour fonctionner. | Non |
| `content-id` | Identifiant unique de l’élément de données renvoyé dans la réponse. Si cette variable n’est pas transmise, un identifiant généré automatiquement est attribué. | Non |
| `content` | Le contenu peut être une image brute (type de contenu &quot;intégré&quot;). <br> Si le contenu est un fichier sur S3 (type de contenu &quot;s3-bucket&quot;), transmettez l’URL signée. | Oui |

**Réponse**

Une réponse réussie renvoie le texte qui a été détecté dans la variable `feature_value` tableau. Le texte est lu et renvoyé de gauche à droite. Cela signifie que si &quot;J’aime l’Adobe&quot; a été détecté, votre payload renvoie &quot;I&quot;, &quot;love&quot; et &quot;Adobe&quot; dans des objets distincts. Dans l’objet , une `feature_name` qui contient le mot et un `feature_value` qui contient une mesure de confiance pour ce texte.

```json
{
  "status": 200,
  "content_id": "TestImage.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-text-extractor-ocr:Service-b0675160421e404ca3c7ca60f46a5b29",
      "content_id": "TestImage.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "yes",
                "feature_name": "has_text"
              },
              {
                "feature_value": "0.977",
                "feature_name": "CHEF"
              },
              {
                "feature_value": "success",
                "feature_name": "text_processing_status"
              }
            ],
            "feature_name": "ocr"
          }
        ]
      }
    }
  ],
  "error": []
}
```
