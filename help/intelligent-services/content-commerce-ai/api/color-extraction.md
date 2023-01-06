---
keywords: Experience Platform;prise en main;contenu;commerce ai;contenu et commerce ai;extraction de couleurs;extraction de couleurs
solution: Experience Platform
title: Extraction de couleurs dans l’API Content and Commerce AI
description: Le service d’extraction de couleurs, lorsqu’on lui donne une image, peut calculer l’histogramme des couleurs des pixels et les trier par couleurs dominantes en compartiments.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 3%

---

# Extraction des couleurs

>[!NOTE]
>
>[!DNL Content and Commerce AI] est en version bêta. La documentation peut être modifiée.

Le service d’extraction de couleurs, lorsqu’on lui donne une image, peut calculer un histogramme des couleurs des pixels et les trier par couleurs dominantes en compartiments. Les couleurs des pixels de l’image sont regroupées en 40 couleurs prédominantes, représentatives du spectre de couleurs. Un histogramme des valeurs de couleur est ensuite calculé parmi ces 40 couleurs. Le service comporte deux variantes :

**Extraction des couleurs (image complète)**

Cette méthode extrait un histogramme des couleurs sur l’ensemble de l’image.

**Extraction des couleurs (avec masque)**

Cette méthode utilise un extracteur de premier plan basé sur l’apprentissage profond pour identifier les objets au premier plan. Le modèle est formé sur un catalogue d’images de commerce électronique. Une fois l’objet de premier plan extrait, un histogramme est calculé sur les couleurs dominantes, comme décrit précédemment.

L’image suivante a été utilisée dans l’exemple illustré dans ce document :

![image de test](../images/QQAsset1.jpg)

**Format d’API**

```http
POST /services/v1/predict
```

**Requête**

L’exemple de requête suivant utilise la méthode image complète pour l’extraction de couleurs.

La requête suivante extrait les couleurs d’une image en fonction des paramètres d’entrée fournis dans le payload. Pour plus d’informations sur les paramètres d’entrée affichés, reportez-vous au tableau ci-dessous de l’exemple de payload.

>[!CAUTION]
>
>`analyzer_id` détermine [!DNL Sensei Content Framework] est utilisée. Vérifiez que vous disposez des `analyzer_id` avant d’effectuer votre requête. Pour le service d’extraction de couleurs, la variable `analyzer_id` L’ID est :
>`Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7`

```SHELL
curl -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'cache-control: no-cache,no-cache' \
  -F file=@test_image.jpg \
  -F 'contentAnalyzerRequests={
   "enable_diagnostics":"true",
   "requests":[
     {
         "analyzer_id": "Feature:image-color-histogram:Service-6fe52999293e483b8e4ae9a95f1b81a7",
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
            "custom": {"exclude_mask": 1}
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
| `data` | Tableau contenant des objets JSON. Chaque objet du tableau représente une image. Tous les paramètres transmis dans le cadre de ce tableau remplacent les paramètres globaux spécifiés en dehors de la variable `data` tableau. Toutes les propriétés restantes décrites ci-dessous dans ce tableau peuvent être remplacées dans . `data`. | Oui |
| `content-id` | Identifiant unique de l’élément de données renvoyé dans la réponse. Si cette variable n’est pas transmise, un identifiant généré automatiquement est attribué. | Non |
| `content` | Contenu à analyser par le service d’extraction de couleurs. Dans le cas où l’image fait partie du corps de la requête, utilisez `-F file=@<filename>` dans la commande curl pour transmettre l’image, en laissant ce paramètre comme une chaîne vide. <br> Si l’image est un fichier sur S3, transmettez l’URL signée. Lorsque le contenu fait partie du corps de la requête, la liste des éléments de données ne doit comporter qu’un seul objet. Si plusieurs objets sont transmis, seul le premier objet est traité. | Oui |
| `content-type` | Utilisé pour indiquer si l’entrée fait partie du corps de la requête ou une URL signée pour un compartiment S3. La valeur par défaut de cette propriété est `inline`. | Non |
| `encoding` | Format de fichier de l’image d’entrée. Actuellement, seules les images JPEG et PNG peuvent être traitées. La valeur par défaut de cette propriété est `jpeg`. | Non |
| `threshold` | Seuil de score (0 à 1) au-dessus duquel les résultats doivent être renvoyés. Utiliser la valeur `0` pour renvoyer tous les résultats. La valeur par défaut de cette propriété est `0`. | Non |
| `top-N` | Nombre de résultats à renvoyer (ne peut pas être un entier négatif). Utiliser la valeur `0` pour renvoyer tous les résultats. Utilisé conjointement avec `threshold`, le nombre de résultats renvoyés est le plus petit des jeux de limites. La valeur par défaut de cette propriété est `0`. | Non |
| `custom` | Tous les paramètres personnalisés à transmettre. | Non |
| `historic-metadata` | Tableau pouvant être transmis par des métadonnées. | Non |

**Réponse**

Une réponse réussie renvoie les détails des couleurs extraites. Chaque couleur est représentée par une `feature_value` qui contient les informations suivantes :

- Nom de la couleur
- Pourcentage d’affichage de cette couleur par rapport à l’image
- Valeur RGB de la couleur

Dans le premier exemple d’objet ci-dessous, la variable `feature_value` de `White,0.59,251,251,243` signifie que la couleur trouvée est blanche, que le blanc se trouve dans 59 % de l’image et qu’elle a une valeur RGB de 251 251 243.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:image-color-histogram:Service-e952f4acd7c2425199b476a2eb459635",
      "content_id": "test_image.jpg",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_value": [
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "White,0.59,251,251,243"
              },
              {
                "feature_value": "Orange,0.30,248,169,48",
                "feature_name": "color_name_and_rgb"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Mustard,0.08,251,199,77"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Gold,0.02,250,191,55"
              }
            ],
            "feature_name": "color"
          }
        ]
      }
    }
  ],
  "error": []
}
```

| Propriété | Description |
| --- | --- |
| `content_id` | Nom de l’image qui a été chargée dans votre demande de POST. |
| `feature_value` | Tableau dont les objets contiennent des clés portant le même nom de propriété. Ces clés contiennent une chaîne qui représente le nom de la couleur. Un pourcentage de cette couleur apparaît par rapport à l’image envoyée dans la variable `content_id`et la valeur RGB de la couleur. |
