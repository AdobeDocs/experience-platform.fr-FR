---
keywords: classification de texte;classification de texte
solution: Intelligent Services
title: Classification de texte dans l’API Content and Commerce AI
topic-legacy: Developer guide
description: Lorsqu’un fragment de texte est fourni, le service de classification de texte peut le classer dans une ou plusieurs étiquettes. La classification peut être une seule étiquette, plusieurs étiquettes ou hiérarchique.
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 5%

---

# Classification de texte

>[!NOTE]
>
>Content and Commerce AI est en version bêta. La documentation peut être modifiée.

Lorsqu’un fragment de texte est fourni, le service de classification de texte peut le classer dans une ou plusieurs étiquettes. La classification peut être une seule étiquette, plusieurs étiquettes ou hiérarchique.

**Format d’API**

```http
POST /services/v1/predict
```

**Requête**

La requête suivante classe le texte d’un fragment en fonction des paramètres d’entrée fournis dans le payload. Pour plus d’informations sur les paramètres d’entrée affichés, reportez-vous au tableau ci-dessous de l’exemple de payload.

>[!CAUTION]
>
>`analyzer_id` détermine [!DNL Sensei Content Framework] est utilisée. Vérifiez que vous disposez des `analyzer_id` avant d’effectuer votre requête. Contactez l’équipe bêta de Content and Commerce AI pour recevoir votre `analyzer_id` pour ce service.

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
| `analyzer_id` | Le [!DNL Sensei] ID de service sous lequel votre requête est déployée. Cet identifiant détermine laquelle de la variable [!DNL Sensei Content Frameworks] sont utilisées. Pour les services personnalisés, contactez l’équipe Content and Commerce AI pour configurer un identifiant personnalisé. | Oui |
| `application-id` | L’identifiant de l’application créée. | Oui |
| `data` | Tableau contenant un objet JSON dont chaque objet du tableau représente un document. Tous les paramètres transmis dans le cadre de ce tableau remplacent les paramètres globaux spécifiés en dehors de la variable `data` tableau. Toutes les propriétés restantes décrites ci-dessous dans ce tableau peuvent être remplacées dans . `data`. | Oui |
| `language` | Langue du texte de saisie. La valeur par défaut est `en`. | Non |
| `content-type` | Utilisé pour indiquer si l’entrée fait partie du corps de la requête ou une URL signée pour un compartiment S3. La valeur par défaut de cette propriété est `inline`. | Non |
| `encoding` | Format de codage du texte d’entrée. Cela peut être `utf-8` ou `utf-16`. La valeur par défaut de cette propriété est `utf-8`. | Non |
| `threshold` | Seuil de score (0 à 1) au-dessus duquel les résultats doivent être renvoyés. Utiliser la valeur `0` pour renvoyer tous les résultats. La valeur par défaut de cette propriété est `0`. | Non |
| `top-N` | Nombre de résultats à renvoyer (ne peut pas être un entier négatif). Utiliser la valeur `0` pour renvoyer tous les résultats. Utilisé conjointement avec `threshold`, le nombre de résultats renvoyés est le plus petit des jeux de limites. La valeur par défaut de cette propriété est `0`. | Non |
| `custom` | Tous les paramètres personnalisés à transmettre. Cette propriété requiert un objet JSON valide pour fonctionner. | Non |
| `content-id` | Identifiant unique de l’élément de données renvoyé dans la réponse. Si ce n’est pas le cas, un identifiant généré automatiquement est attribué. | Non |
| `content` | Contenu utilisé par le service de classification de texte. Le contenu peut être du texte brut (type de contenu &quot;intégré&quot;). <br> Si le contenu est un fichier sur S3 (type de contenu &quot;s3-bucket&quot;), transmettez l’URL signée. | Oui |

**Réponse**

Une réponse réussie renvoie le texte classé dans un tableau de réponse.

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
