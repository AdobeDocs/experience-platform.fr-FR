---
keywords: similarité visuelle;similarité visuelle;api cai
solution: Experience Platform
title: Similarité visuelle dans l’API Content and Commerce AI
description: Le service de similarité visuelle, lorsqu’une image est fournie, recherche automatiquement les images visuellement similaires d’un catalogue.
exl-id: fe31d9be-ee42-44fa-b83f-3b8a718cb4e3
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# Similarité visuelle

>[!NOTE]
>
>[!DNL Content and Commerce AI] est en version bêta. La documentation peut être modifiée.

Le service de similarité visuelle, lorsqu’une image est fournie, recherche automatiquement les images visuellement similaires d’un catalogue.

L’image suivante a été utilisée dans l’exemple de requête illustré dans ce document :

![image de test](../images/Query_Image.jpeg)

**Format d’API**

```http
POST /services/v1/predict
```

**Requête**

La requête suivante récupère des images visuellement similaires d’un catalogue, en fonction des paramètres d’entrée fournis dans la payload. Pour plus d’informations sur les paramètres d’entrée affichés, reportez-vous au tableau ci-dessous de l’exemple de payload.

>[!CAUTION]
>
>`analyzer_id` détermine [!DNL Sensei Content Framework] est utilisée. Vérifiez que vous disposez des `analyzer_id` avant d’effectuer votre requête. Contactez l’équipe bêta de Content and Commerce AI pour recevoir votre `analyzer_id` pour ce service.

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer $API_TOKEN' \
  -H 'Content-Type: multipart/form-data' \
  -H 'cache-control: no-cache,no-cache' \
  -H 'x-api-key: $API_KEY' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
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
      }
    ]
}'
```

| Propriété | Description | Obligatoire |
| --- | --- | --- |
| `analyzer_id` | Le [!DNL Sensei] ID de service sous lequel votre requête est déployée. Cet identifiant détermine laquelle de la variable [!DNL Sensei Content Frameworks] sont utilisées. Pour les services personnalisés, contactez l’équipe Content and Commerce AI pour configurer un identifiant personnalisé. | Oui |
| `application-id` | L’identifiant de l’application créée. | Oui |
| `data` | Tableau contenant un objet JSON dont chaque objet du tableau représente une image. Tous les paramètres transmis dans le cadre de ce tableau remplacent les paramètres globaux spécifiés en dehors de la variable `data` tableau. Toutes les propriétés restantes décrites ci-dessous dans ce tableau peuvent être remplacées dans . `data`. | Oui |
| `content-id` | Identifiant unique de l’élément de données renvoyé dans la réponse. Si cette variable n’est pas transmise, un identifiant généré automatiquement est attribué. | Non |
| `content` | Contenu à analyser par le service de similarité visuelle. Dans le cas où l’image fait partie du corps de la requête, utilisez `-F file=@<filename>` dans la commande curl pour transmettre l’image, en laissant ce paramètre comme une chaîne vide. <br> Si l’image est un fichier sur S3, transmettez l’URL signée. Lorsque le contenu fait partie du corps de la requête, la liste des éléments de données ne doit comporter qu’un seul objet. Si plusieurs objets sont transmis, seul le premier objet est traité. | Oui |
| `content-type` | Utilisé pour indiquer si l’entrée fait partie du corps de la requête ou une URL signée pour un compartiment S3. La valeur par défaut de cette propriété est `inline`. | Non |
| `encoding` | Format de fichier de l’image d’entrée. Actuellement, seules les images JPEG et PNG peuvent être traitées. La valeur par défaut de cette propriété est `jpeg`. | Non |
| `threshold` | Seuil de score (0 à 1) au-dessus duquel les résultats doivent être renvoyés. Utiliser la valeur `0` pour renvoyer tous les résultats. La valeur par défaut de cette propriété est `0`. | Non |
| `top-N` | Nombre de résultats à renvoyer (ne peut pas être un entier négatif). Utiliser la valeur `0` pour renvoyer tous les résultats. Utilisé conjointement avec `threshold`, le nombre de résultats renvoyés est le plus petit des jeux de limites. La valeur par défaut de cette propriété est `0`. | Non |
| `custom` | Tous les paramètres personnalisés à transmettre. | Non |
| `historic-metadata` | Tableau pouvant être transmis par des métadonnées. | Non |

**Réponse**

Une réponse réussie renvoie une `response` tableau contenant un `feature_value` et `feature_name` pour chacune des images visuellement similaires trouvées dans le catalogue.

Les images visuellement similaires suivantes ont été renvoyées dans l’exemple de réponse illustré ci-dessous :

![images similaires](../images/results.jpg)

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-deep-product-search:Service-316a8cf750c6440396061c8f73a7a585",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_value": "678",
                "feature_name": "G34WS945.F1"
              },
              {
                "feature_value": "678",
                "feature_name": "1431RDM JANELLE RAW JACKE"
              },
              {
                "feature_value": "657",
                "feature_name": "GF4045877841 CARLA FLR"
              },
              {
                "feature_name": "1707-686-SGU PATCH XYZ",
                "feature_value": "657"
              },
              {
                "feature_name": "5495MJT AJA BLK",
                "feature_value": "646"
              },
              {
                "feature_name": "IDEAL",
                "feature_value": "645"
              },
              {
                "feature_value": "644",
                "feature_name": "HCAJRA439 CALI JEAN"
              },
              {
                "feature_name": "KT279RK-ONL",
                "feature_value": "644"
              },
              {
                "feature_name": "SP190404-ELLIS",
                "feature_value": "642"
              },
              {
                "feature_name": "GF4174848718 KENDALL DIS",
                "feature_value": "640"
              }
            ],
            "feature_name": "visual_similarity"
          }
        ]
      }
    }
  ],
  "error": []
}
```
