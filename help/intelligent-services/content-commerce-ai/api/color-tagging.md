---
keywords: Experience Platform;prise en main;contenu;balisage de contenu;balisage de couleur;extraction de couleur;
solution: Experience Platform
title: Balisage des couleurs dans l’API de balisage de contenu
description: Le service de balisage des couleurs, lorsqu’une image est donnée, peut calculer l’histogramme des couleurs des pixels et les trier par couleurs dominantes en compartiments.
exl-id: 6b3b6314-cb67-404f-888c-4832d041f5ed
source-git-commit: fd8891bdc7d528e327d2a72c2427f7bbc6dc8a03
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 6%

---

# Balisage des couleurs

Le service de balisage des couleurs, lorsqu’une image est donnée, peut calculer un histogramme des couleurs des pixels et les trier par couleurs dominantes en compartiments. Les couleurs des pixels de l’image sont regroupées en 40 couleurs prédominantes, représentatives du spectre de couleurs. Un histogramme des valeurs de couleur est ensuite calculé parmi ces 40 couleurs. Le service comporte deux variantes :

**Balisage des couleurs (image complète)**

Cette méthode extrait un histogramme des couleurs sur toute l’image.

**Balisage des couleurs (avec masque)**

Cette méthode utilise un extracteur de premier plan basé sur l’apprentissage profond pour identifier les objets au premier plan. Une fois les objets de premier plan extraits, un histogramme est calculé sur les couleurs dominantes pour les zones de premier plan et d’arrière-plan, ainsi que pour l’image entière.

**Extraction de tonalité**

Outre les variantes mentionnées ci-dessus, vous pouvez configurer le service pour récupérer un histogramme des tons pour :

- L’image globale (lors de l’utilisation d’une variante d’image complète)
- L’image globale, ainsi que les zones de premier plan et d’arrière-plan (lors de l’utilisation de la variante avec le masquage)

L’image suivante a été utilisée dans l’exemple illustré dans ce document :

![image test](../images/QQAsset1.jpg)

**Format d’API**

```http
POST /services/v2/predict
```

**Demande - variante d’image complète**

L’exemple de requête suivant utilise la méthode image complète pour le balisage colorimétrique et extrait les couleurs d’une image en fonction des paramètres d’entrée fournis dans la payload. Pour plus d’informations sur les paramètres d’entrée affichés, reportez-vous au tableau ci-dessous de l’exemple de payload.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005      
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

**Réponse - variante d’image complète**

Une réponse réussie renvoie les détails des couleurs extraites. Chaque couleur est représentée par une clé `feature_value` qui contient les informations suivantes :

- Nom de la couleur
- Pourcentage de cette couleur par rapport à l’image
- La valeur RGB de la couleur

`"White":{"coverage":0.5834,"rgb":{"red":254,"green":254,"blue":243}}`signifie que la couleur trouvée est blanche, que l’on trouve dans 58,34 % de l’image et qu’elle a une valeur de RGB moyenne de 254 254 243.

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "bfpzaJxKDxtgxpjUj5QDrN1jasjUw2RM"
}  
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        }
    }
}]
```

Notez que la couleur du résultat ici est extraite de la région &quot;globale&quot; de l’image.

**Demande - variante d’image masquée**

L’exemple de requête suivant utilise la méthode de masquage pour le balisage colorimétrique. Cela est activé en définissant le paramètre `enable_mask` sur `true` dans la requête.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v2/predict \
-H 'Prefer: respond-async, wait=59' \
-H "x-api-key: $API_KEY" \
-H "content-type: multipart/form-data" \
-H "authorization: Bearer $API_TOKEN" \
-F 'contentAnalyzerRequests={
  "sensei:name": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
  "sensei:invocation_mode": "synchronous",
  "sensei:invocation_batch": false,
  "sensei:engines": [
    {
      "sensei:execution_info": {
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72"
      },
      "sensei:inputs": {
        "documents": [{
            "sensei:multipart_field_name": "infile_1",
            "dc:format": "image/jpg"
          }]
      },
      "sensei:params": {
        "top_n": 5,
        "min_coverage": 0.005,
        "enable_mask": true,
        "retrieve_tone": true     
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

>[!NOTE]
>
>De plus, le paramètre `retrieve_tone` est également défini sur `true` dans la requête ci-dessus. Cela nous permet de récupérer un histogramme de distribution des tons sur des tons chauds, neutres et froids dans l’ensemble, le premier plan et l’arrière-plan de l’image.

**Réponse - variante d’image masquée**

```json
{
    "statuses": [{
        "sensei:engine": "Feature:autocrop:Service-af865523d46547e2b17fdf9b38e32a72",
        "invocations": [{
            "sensei:outputs": {
                "result": {
                    "sensei:multipart_field_name": "result",
                    "dc:format": "application/json"
                }
            },
            "message": null,
            "status": "200"
        }]
    }],
    "request_id": "gpeCyJsrJvOWd94WwZOyPBPrKi2BQyla"
}  
 
 
[{
    "overall": {
        "colors": {
            "White": {
                "coverage": 0.5834,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Orange": {
                "coverage": 0.254,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.0817,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.0727,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0082,
                "rgb": {
                    "red": 253,
                    "green": 236,
                    "blue": 174
                }
            }
        },
        "tones": {
            "warm": 0.4084,
            "neutral": 0.5916,
            "cool": 0
        }
    },
    "foreground": {
        "colors": {
            "Orange": {
                "coverage": 0.6022,
                "rgb": {
                    "red": 249,
                    "green": 165,
                    "blue": 45
                }
            },
            "Gold": {
                "coverage": 0.1935,
                "rgb": {
                    "red": 253,
                    "green": 188,
                    "blue": 58
                }
            },
            "Mustard": {
                "coverage": 0.1722,
                "rgb": {
                    "red": 253,
                    "green": 207,
                    "blue": 84
                }
            },
            "Cream": {
                "coverage": 0.0173,
                "rgb": {
                    "red": 253,
                    "green": 235,
                    "blue": 170
                }
            },
            "Yellow": {
                "coverage": 0.0148,
                "rgb": {
                    "red": 254,
                    "green": 229,
                    "blue": 117
                }
            }
        },
        "tones": {
            "warm": 0.9827,
            "neutral": 0.0173,
            "cool": 0
        }
    },
    "background": {
        "colors": {
            "White": {
                "coverage": 0.9923,
                "rgb": {
                    "red": 254,
                    "green": 254,
                    "blue": 243
                }
            },
            "Dark_Brown": {
                "coverage": 0.0077,
                "rgb": {
                    "red": 83,
                    "green": 68,
                    "blue": 57
                }
            }
        },
        "tones": {
            "warm": 0,
            "neutral": 1.0,
            "cool": 0
        }
    }
}]
```

Outre les couleurs de l’image globale, vous pouvez désormais afficher les couleurs des régions de premier plan et d’arrière-plan. Comme la récupération des tons est activée pour chacune des régions ci-dessus, vous pouvez également récupérer l’histogramme d’une tonalité.

**Paramètres d’entrée**

| Nom | Type de données | Obligatoire | Par défaut | Valeurs | Description |
| --- | --- | --- | --- | --- | --- |
| `documents` | array (Document-Object) | Oui | - | Voir ci-dessous | Liste des éléments JSON dont chaque élément de la liste représente un document. |
| `top_n` | nombre | Non | 0 | Entier non négatif | Nombre de résultats à renvoyer. 0, pour renvoyer tous les résultats. En cas d’utilisation conjointe avec le seuil, le nombre de résultats renvoyé sera inférieur à l’une ou l’autre des limites. |
| `min_coverage` | nombre | Non | 0,05 | Nombre réel | Seuil de couverture au-dessus duquel les résultats doivent être renvoyés. Paramètre Exclure pour renvoyer tous les résultats. |
| `resize_image` | nombre | Non | True | True/False | Si vous souhaitez redimensionner l’image d’entrée ou non. Par défaut, les images sont redimensionnées à 320 x 320 pixels avant l’extraction des couleurs. À des fins de débogage, nous pouvons également permettre au code de s’exécuter sur l’image complète, en définissant ce paramètre sur `False`. |
| `enable_mask` | nombre | Non | False | True/False | Active/désactive l’extraction de couleurs |
| `retrieve_tone` | nombre | Non | False | True/False | Active/désactive l’extraction des tons |

**Objet document**

| Nom | Type de données | Obligatoire | Par défaut | Valeurs | Description |
| -----| --------- | -------- | ------- | ------ | ----------- |
| `repo:path` | chaîne | - | - | - | URL présignée du document. |
| `sensei:repoType` | Chaîne | - | - | HTTPS | Type de référentiel dans lequel l’image est stockée. |
| `sensei:multipart_field_name` | Chaîne | - | - | - | Utilisez-le lorsque vous transmettez le fichier image en tant qu’argument en plusieurs parties au lieu d’utiliser des URL présignées. |
| `dc:format` | Chaîne | Oui | - | &quot;image/jpg&quot;,<br>&quot;image/jpeg&quot;,<br>&quot;image/png&quot;,<br>&quot;image/tiff&quot; | Le codage des images est comparé aux types de codage d’entrée autorisés avant d’être traité. |