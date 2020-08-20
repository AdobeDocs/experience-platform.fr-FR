---
keywords: text classification;Text classification
solution: Experience Platform
title: Point de terminaison de l’API de classification de texte
topic: Developer guide
description: Lorsqu’un fragment de texte est fourni, le service de classification de texte peut le classifier en une ou plusieurs étiquettes. La classification peut être à libellé unique, à libellé multiple ou hiérarchique.
translation-type: tm+mt
source-git-commit: e69f4e8ddc0fe5f7be2b2b2bd89c09efdfca8e75
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 5%

---


# Classification de texte

>[!NOTE]
>
>Content and Commerce AI est en version bêta. La documentation peut être modifiée.

Lorsqu’un fragment de texte est fourni, le service de classification de texte peut le classifier en une ou plusieurs étiquettes. La classification peut être à libellé unique, à libellé multiple ou hiérarchique.

La classification de texte utilise un modèle basé sur [FastText](https://fasttext.cc/) qui a été formé à l’aide de données personnalisées.

**Format d’API**

```http
POST /services/v1/predict
```

**Requête**

La requête suivante classe le texte d’un fragment en fonction des paramètres d’entrée fournis dans la charge utile. Consultez le tableau ci-dessous pour plus d’informations sur les paramètres d’entrée affichés.

>[!CAUTION]
>
>`analyzer_id` détermine lequel [!DNL Sensei Content Framework] est utilisé. Veuillez vérifier que vous en avez le bon `analyzer_id` avant de faire votre demande.

```SHELL
curl -w'\n' -i -X POST https://sensei.adobe.io/services/v1/predict \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "Content-Type: multipart/form-data" \
  -H "cache-control: no-cache,no-cache" \
  -H "x-api-key: {API_KEY}" \
  -F file="{
    \"application-id\": \"1234\", 
    \"language\": \"en\", 
    \"content-type\": \"inline\", 
    \"encoding\": \"utf-8\", 
    \"data\": [{
      \"content-id\": \"abc123\", 
      \"content\": \"Server and Workstation Processors, Microcode Update is a self-extracting executable file containing the latest beta microcode updates (System Configuration Data) and software license agreement.\"
      }]
    }" \
  -F 'contentAnalyzerRequests={
    "enable_diagnostics":"true",
    "requests":[{
         "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
         "parameters": {}
    }]
}'
```

| Propriété | Description | Obligatoire |
| --- | --- | --- |
| `analyzer_id` | ID [!DNL Sensei] de service sous lequel votre demande est déployée. Cet identifiant détermine lequel des [!DNL Sensei Content Frameworks] est utilisé. | Oui |
| `application-id` | ID de l’application créée. | Oui |
| `data` | Tableau contenant un objet JSON avec chaque objet du tableau représentant un document. Tous les paramètres transmis dans le cadre de ce tableau remplacent les paramètres globaux spécifiés en dehors du `data` tableau. Toutes les autres propriétés décrites ci-dessous dans ce tableau peuvent être remplacées de l’intérieur `data`. | Oui |
| `language` | Langue du texte de saisie. La valeur par défaut est `en`. | Non |
| `content-type` | Permet d’indiquer si l’entrée fait partie du corps de la requête ou si une URL signée est associée à un compartiment S3. La valeur par défaut de cette propriété est `inline`. | Non |
| `encoding` | Format de codage du texte d’entrée. Cela peut être `utf-8` ou `utf-16`. La valeur par défaut de cette propriété est `utf-8`. | Non |
| `threshold` | Seuil de score (0 à 1) au-dessus duquel les résultats doivent être renvoyés. Utilisez la valeur `0` pour renvoyer tous les résultats. La valeur par défaut de cette propriété est `0`. | Non |
| `top-N` | Nombre de résultats à renvoyer (ne peut pas être un entier négatif). Utilisez la valeur `0` pour renvoyer tous les résultats. Lorsqu&#39;elle est utilisée conjointement avec `threshold`, le nombre de résultats renvoyés est le plus faible des deux limites définies. La valeur par défaut de cette propriété est `0`. | Non |
| `custom` | Tout paramètre personnalisé à transmettre. Cette propriété requiert un objet JSON valide pour fonctionner. | Non |
| `content-id` | ID unique de l’élément de données renvoyé dans la réponse. Si ce n’est pas le cas, un identifiant généré automatiquement est attribué. | Non |
| `content` | Contenu utilisé par le service de classification de texte. Le contenu peut être du texte brut (type de contenu &quot;intégré&quot;). <br> Si le contenu est un fichier sur S3 (type de contenu du compartiment 3), transmettez l’URL signée. | Oui |

**Réponse**

Une réponse réussie renvoie le texte classifié dans un tableau de réponses.

```json
{
  "status": 200,
  "cas_responses": [
    {
      "status": 200,
      "analyzer_id": "Feature:cintel-text-classifier:Service-38a4cc7b286449e6bc1977f59df01b47",
      "content_id": "",
      "result": {
        "response_type": "feature",
        "response": [
          {
            "feature_name": "abc123",
            "feature_value": [
              {
                "feature_value": [
                  {
                    "feature_value": 0.6899315714836121,
                    "feature_name": "Embedded & IoT"
                  }
                ],
                "feature_name": "labels"
              },
              {
                "feature_name": "status",
                "feature_value": "success"
              }
            ]
          }
        ]
      }
    }
  ],
  "error": []
}
```
