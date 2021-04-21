---
keywords: OCR ; présence de texte ; reconnaissance optique de caractères
solution: Experience Platform, Intelligent Services
title: Présence de texte et reconnaissance de caractères optiques
topic-legacy: Developer guide
description: Dans l’API Content and Commerce AI, le service Text Presence / Optical Character Recognition (OCR) peut indiquer si du texte est présent dans une image donnée. Si du texte est présent, la reconnaissance optique des caractères peut renvoyer le texte.
exl-id: 85b976a7-0229-43e9-b166-cdbd213b867f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 4%

---

# Présence de texte et reconnaissance de caractères optiques

>[!NOTE]
>
>Content and Commerce AI est en version bêta. La documentation peut être modifiée.

Le service Visibilité de texte / Reconnaissance optique de caractères (OCR), lorsqu’une image est donnée, peut indiquer si du texte est présent dans l’image. Si du texte est présent, la reconnaissance optique des caractères peut renvoyer le texte.

L&#39;image suivante a été utilisée dans l&#39;exemple de demande illustré dans ce document :

![image de test](../images/shef.jpeg)

**Format d’API**

```http
POST /services/v1/predict
```

**Requête**

La requête suivante vérifie si du texte est présent en fonction de l’image d’entrée fournie dans la charge utile. Consultez le tableau ci-dessous pour plus d’informations sur les paramètres d’entrée affichés.

>[!CAUTION]
>
>`analyzer_id` détermine lequel  [!DNL Sensei Content Framework] est utilisé. Veuillez vérifier que vous disposez du `analyzer_id` approprié avant de faire votre demande. Contactez l’équipe bêta de Content and Commerce AI pour recevoir votre `analyzer_id` pour ce service.

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
| `analyzer_id` | ID de service [!DNL Sensei] sous lequel votre requête est déployée. Cet identifiant détermine lequel des [!DNL Sensei Content Frameworks] est utilisé. Pour les services personnalisés, contactez l’équipe d’API Content and Commerce pour configurer un identifiant personnalisé. | Oui |
| `application-id` | ID de l’application créée. | Oui |
| `data` | Tableau contenant un objet JSON avec chaque objet du tableau représentant une image transmise. Tout paramètre transmis dans le cadre de ce tableau remplace les paramètres globaux spécifiés en dehors du tableau `data`. Toutes les autres propriétés décrites ci-dessous dans ce tableau peuvent être remplacées à partir de `data`. | Oui |
| `language` | Langue du texte de saisie. La valeur par défaut est `en`. | Non |
| `content-type` | Permet d’indiquer si l’entrée fait partie du corps de la requête ou si une URL signée est associée à un compartiment S3. La valeur par défaut de cette propriété est `inline`. | Non |
| `encoding` | Format de fichier de l’image d’entrée. Actuellement, seules les images JPEG et PNG peuvent être traitées. La valeur par défaut de cette propriété est `jpeg`. | Non |
| `threshold` | Seuil de score (0 à 1) au-dessus duquel les résultats doivent être renvoyés. Utilisez la valeur `0` pour renvoyer tous les résultats. La valeur par défaut de cette propriété est `0`. | Non |
| `top-N` | Nombre de résultats à renvoyer (ne peut pas être un entier négatif). Utilisez la valeur `0` pour renvoyer tous les résultats. Lorsqu&#39;il est utilisé conjointement avec `threshold`, le nombre de résultats renvoyés est le moins élevé des deux limites définies. La valeur par défaut de cette propriété est `0`. | Non |
| `custom` | Tout paramètre personnalisé à transmettre. Cette propriété requiert un objet JSON valide pour fonctionner. | Non |
| `content-id` | ID unique de l’élément de données renvoyé dans la réponse. Si elle n’est pas transmise, un identifiant généré automatiquement est attribué. | Non |
| `content` | Le contenu peut être une image brute (type de contenu &quot;intégré&quot;). <br> Si le contenu est un fichier sur S3 (type de contenu du compartiment 3), transmettez l’URL signée. | Oui |

**Réponse**

Une réponse réussie renvoie le texte qui a été détecté dans le tableau `feature_value`. Le texte est lu et renvoyé de gauche à droite de haut en bas. Cela signifie que si &quot;J’aime l’Adobe&quot; a été détecté, votre charge utile renvoie &quot;I&quot;, &quot;love&quot; et &quot;Adobe&quot; dans des objets distincts. Dans l’objet, un `feature_name` contenant le mot et un `feature_value` contenant une mesure de confiance pour ce texte vous est attribué.

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
