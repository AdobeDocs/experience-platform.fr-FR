---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai;color extraction;Color extraction
solution: Experience Platform
title: Extraction des couleurs
topic: Developer guide
description: Le service d’extraction des couleurs, lorsqu’on lui donne une image, peut calculer l’histogramme des couleurs de pixels et les trier par couleurs dominantes en compartiments.
translation-type: tm+mt
source-git-commit: e69f4e8ddc0fe5f7be2b2b2bd89c09efdfca8e75
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 3%

---


# Extraction des couleurs

>[!NOTE]
>
>[!DNL Content and Commerce AI] est en version bêta. La documentation peut être modifiée.

Le service d’extraction des couleurs, lorsqu’on lui donne une image, peut calculer un histogramme de couleurs de pixels et les trier par couleurs dominantes en compartiments. Les couleurs des pixels de l&#39;image sont regroupées en 40 couleurs prédominantes, représentatives du spectre de couleurs. Un histogramme de valeurs de couleur est ensuite calculé parmi ces 40 couleurs. Le service comporte deux variantes :

**Extraction des couleurs (image complète)**

Cette méthode extrait un histogramme de couleur sur l’ensemble de l’image.

**Extraction des couleurs (avec masque)**

Cette méthode utilise un extracteur de premier plan basé sur l’apprentissage profond pour identifier les objets au premier plan. Le modèle est formé sur un catalogue d&#39;images de commerce électronique. Une fois l’objet de premier plan extrait, un histogramme est calculé sur les couleurs dominantes, comme décrit précédemment.

L&#39;image suivante a été utilisée dans l&#39;exemple illustré dans ce document :

![image test](../images/test_image.jpeg)

**Format d’API**

```http
POST /services/v1/predict
```

**Requête**

L’exemple de demande suivant utilise la méthode de l’image complète pour l’extraction des couleurs.

La requête suivante extrait les couleurs d’une image en fonction des paramètres d’entrée fournis dans la charge utile. Consultez le tableau ci-dessous pour plus d’informations sur les paramètres d’entrée affichés.

>[!CAUTION]
>
>`analyzer_id` détermine lequel [!DNL Sensei Content Framework] est utilisé. Veuillez vérifier que vous en avez le bon `analyzer_id` avant de faire votre demande.

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
| `analyzer_id` | ID [!DNL Sensei] de service sous lequel votre demande est déployée. Cet identifiant détermine lequel des [!DNL Sensei Content Frameworks] est utilisé. | Oui |
| `application-id` | ID de l’application créée. | Oui |
| `data` | Tableau contenant des objets JSON. Chaque objet du tableau représente une image. Tous les paramètres transmis dans le cadre de ce tableau remplacent les paramètres globaux spécifiés en dehors du `data` tableau. Toutes les autres propriétés décrites ci-dessous dans ce tableau peuvent être remplacées de l’intérieur `data`. | Oui |
| `content-id` | ID unique de l’élément de données renvoyé dans la réponse. Si elle n’est pas transmise, un identifiant généré automatiquement est attribué. | Non |
| `content` | Contenu à analyser par le service d’extraction des couleurs. Dans le événement où l’image fait partie du corps de la requête, utilisez `-F file=@<filename>` la commande curl pour transmettre l’image, en laissant ce paramètre sous la forme d’une chaîne vide. <br> Si l’image est un fichier sur S3, transmettez l’URL signée. Lorsque le contenu fait partie du corps de la requête, la liste des éléments de données ne doit comporter qu’un seul objet. Si plusieurs objets sont transmis, seul le premier objet est traité. | Oui |
| `content-type` | Permet d’indiquer si l’entrée fait partie du corps de la requête ou si une URL signée est associée à un compartiment S3. La valeur par défaut de cette propriété est `inline`. | Non |
| `encoding` | Format de fichier de l’image d’entrée. Actuellement, seules les images JPEG et PNG peuvent être traitées. La valeur par défaut de cette propriété est `jpeg`. | Non |
| `threshold` | Seuil de score (0 à 1) au-dessus duquel les résultats doivent être renvoyés. Utilisez la valeur `0` pour renvoyer tous les résultats. La valeur par défaut de cette propriété est `0`. | Non |
| `top-N` | Nombre de résultats à renvoyer (ne peut pas être un entier négatif). Utilisez la valeur `0` pour renvoyer tous les résultats. Lorsqu&#39;elle est utilisée conjointement avec `threshold`, le nombre de résultats renvoyés est le plus faible des deux limites définies. La valeur par défaut de cette propriété est `0`. | Non |
| `custom` | Tout paramètre personnalisé à transmettre. | Non |
| `historic-metadata` | Tableau qui peut être transmis des métadonnées. | Non |

**Réponse**

Une réponse réussie renvoie les détails des couleurs extraites. Chaque couleur est représentée par une `feature_value` clé qui contient les informations suivantes :

- Nom de la couleur
- Pourcentage de cette couleur par rapport à l&#39;image
- Valeur RVB de la couleur

Dans le premier exemple d’objet ci-dessous, la valeur `feature_value` de indique `White,0.82,239,239,239` que la couleur trouvée est le blanc, que le blanc se trouve dans 82 % de l’image et que la valeur RVB est de 239 239 239.

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
                "feature_value": "White,0.82,239,239,239"
              },
              {
                "feature_value": "Dark_Blue,0.11,41,60,86",
                "feature_name": "color_name_and_rgb"
              },
              {
                "feature_name": "color_name_and_rgb",
                "feature_value": "Royal_Blue,0.08,63,91,123"
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
| `content_id` | Nom de l’image qui a été téléchargée dans votre demande de POST. |
| `feature_value` | Tableau dont les objets contiennent des clés portant le même nom de propriété. Ces clés contiennent une chaîne qui représente le nom de la couleur, un pourcentage de cette couleur qui s’affiche par rapport à l’image envoyée dans le `content_id`et la valeur RVB de la couleur. |
