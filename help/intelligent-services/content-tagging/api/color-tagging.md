---
keywords: Experience Platform;prise en main;content ai;commerce ai;balisage de contenu;balisage de couleur;extraction de couleurs
solution: Experience Platform
title: Balisage des couleurs dans l’API de balisage de contenu
description: Le service de balisage des couleurs, lorsqu’une image est donnée, peut calculer l’histogramme des couleurs des pixels et les trier par couleurs dominantes en compartiments.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: feebf4c20d20afcdcfe4523e0b61bff5b999084c
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 5%

---

# Balisage des couleurs

Le service de balisage des couleurs, lorsqu’une image est donnée, peut calculer un histogramme des couleurs des pixels et les trier par couleurs dominantes en compartiments. Les couleurs des pixels de l’image sont regroupées en 40 couleurs prédominantes, représentatives du spectre de couleurs. Un histogramme des valeurs de couleur est ensuite calculé parmi ces 40 couleurs. Le service comporte deux variantes :

**Balisage des couleurs (image complète)**

Cette méthode extrait un histogramme des couleurs sur l’ensemble de l’image.

**Balisage des couleurs (avec masque)**

Cette méthode utilise un extracteur de premier plan basé sur l’apprentissage profond pour identifier les objets au premier plan. Le modèle est formé sur un catalogue d’images de commerce électronique. Une fois l’objet de premier plan extrait, un histogramme est calculé sur les couleurs dominantes, comme décrit précédemment.

L’image suivante a été utilisée dans l’exemple illustré dans ce document :

![image de test](../images/QQAsset1.jpg)

**Format d’API**

```http
POST /services/v2/predict
```

**Requête**

L’exemple de requête suivant utilise la méthode image complète pour le balisage colorimétrique.

La requête suivante extrait les couleurs d’une image en fonction des paramètres d’entrée fournis dans le payload. Pour plus d’informations sur les paramètres d’entrée affichés, reportez-vous au tableau ci-dessous de l’exemple de payload.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "application-id": "1234",
        "enable_mask": 0
      },
      "sensei:outputs":{
        "result" : {
          "sensei:multipart_field_name" : "result",
          "dc:format": "application/json"
        }
      }
    }
  ]
}' \
-F 'infile_1=@1431RDMJANELLERAWJACKE_2.jpg'
```

| Propriété | Description | Obligatoire |
| --- | --- | --- |
| `application-id` | L’identifiant de l’application créée. | Oui |
| `documents` | Liste d’éléments JSON dont chaque élément de la liste représente un document. | Oui |
| `top_n` | Nombre de résultats à renvoyer (il ne peut pas s’agir d’un entier négatif). Utiliser la valeur `0` pour renvoyer tous les résultats. Utilisé conjointement avec `threshold`, le nombre de résultats renvoyés est le plus petit des jeux de limites. La valeur par défaut de cette propriété est `0`. | Non |
| `min_coverage` | Seuil de couverture au-dessus duquel les résultats doivent être renvoyés. Excluez le paramètre pour renvoyer tous les résultats. | Non |
| `resize_image` | Indique si l’image d’entrée doit être redimensionnée. Par défaut, les images sont redimensionnées à 320 x 320 pixels avant l’exécution du balisage colorimétrique. À des fins de débogage, nous pouvons également permettre au code de s’exécuter sur l’image complète, en définissant ce paramètre sur False. | Non |
| `enable_mask` | Active/désactive le balisage des couleurs dans le masque. | Non |

| Nom | Type de données | Obligatoire | Par défaut | Valeurs | Description |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | chaîne | - | - | - | URL présignée du document duquel extraire les expressions clés. |
| `sensei:repoType` | chaîne | - | - | HTTPS | Type de référentiel dans lequel l’image est stockée. |
| `sensei:multipart_field_name` | chaîne | - | - | - | Utilisez-le lorsque vous transmettez un fichier image comme argument multipart au lieu d’utiliser des URL présignées. |
| `dc:format` | chaîne | Oui | - | &quot;image/jpg&quot;, <br> &quot;image/jpeg&quot;, <br>&quot;image/png&quot;, <br>&quot;image/tiff&quot; | Le codage des images est comparé aux types de codage d’entrée autorisés avant d’être traité. |

**Réponse**

Une réponse réussie renvoie les détails des couleurs extraites. Chaque couleur est représentée par une `feature_value` qui contient les informations suivantes :

- Nom de la couleur
- Pourcentage d’affichage de cette couleur par rapport à l’image
- Valeur RGB de la couleur

Dans le premier exemple d’objet ci-dessous, la variable `feature_value` de `Mud_Green,0.069,102,72,95` signifie que la couleur trouvée est le vert boueux, le vert boueux se trouve dans 6,9 % de l’image et a une valeur RGB de 102 7295.

```json
{
  "status": 200,
  "content_id": "test_image.jpg",
  "cas_responses": [
    {
{
  "statuses": [
    {
      "sensei:engine": "Feature:cintel-image-classifier:Service-60887e328ded447d86e01122a4f19c58",
      "invocations": [
        {
          "sensei:outputs": {
            "result": {
              "sensei:multipart_field_name": "result",
              "dc:format": "application/json"
            }
          },
          "message": null,
          "status": "200"
        }
      ]
    }
  ],
  "request_id": "hsxycVq5Q9KbZ7MWrt6NXcSNWbonSLf3"
}

[
  {
    "request_element_id": "0",
    "colors": {
      "Mud_Green": {
        "coverage": 0.0694,
        "rgb": {
          "red": 102,
          "blue": 72,
          "green": 95
        }
      },
      "Dark_Brown": {
        "coverage": 0.1226,
        "rgb": {
          "red": 113,
          "blue": 77,
          "green": 84
        }
      },
      "Pink": {
        "coverage": 0.0731,
        "rgb": {
          "red": 234,
          "blue": 201,
          "green": 209
        }
      },
      "Dark_Gray": {
        "coverage": 0.1533,
        "rgb": {
          "red": 63,
          "blue": 58,
          "green": 59
        }
      },
      "Olive": {
        "coverage": 0.492,
        "rgb": {
          "red": 177,
          "blue": 126,
          "green": 170
        }
      },
      "Brown": {
        "coverage": 0.0896,
        "rgb": {
          "red": 141,
          "blue": 85,
          "green": 105
        }
      }
    }
  }
]
}
```
