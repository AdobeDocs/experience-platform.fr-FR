---
keywords: classification de texte;classification de texte
solution: Experience Platform
title: Classification de texte dans l’API IA dédiée au contenu et à Commerce
description: Lorsqu’il reçoit un fragment de texte, le service de classification de texte peut le classer en une ou plusieurs étiquettes. La classification peut être mono-libellé, multi-libellé ou hiérarchique.
exl-id: f240519a-0d83-4309-91e4-4e48be7955a1
source-git-commit: b124ed97da8bde2a7fc4f10d350c81a47e096f29
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 5%

---

# Classification de texte

>[!NOTE]
>
>L’IA dédiée au contenu et à Commerce est en version bêta. La documentation peut faire l’objet de modifications.

Lorsqu’il reçoit un fragment de texte, le service de classification de texte peut le classer en une ou plusieurs étiquettes. La classification peut être mono-libellé, multi-libellé ou hiérarchique.

**Format d’API**

```http
POST /services/v1/predict
```

**Requête**

La requête suivante classe le texte d’un fragment en fonction des paramètres d’entrée fournis dans la payload. Pour plus d’informations sur les paramètres d’entrée affichés, consultez le tableau ci-dessous l’exemple de payload.

>[!CAUTION]
>
>`analyzer_id` détermine l’[!DNL Sensei Content Framework] utilisée. Vérifiez que vous disposez des `analyzer_id` appropriées avant d&#39;effectuer votre demande. Contactez l’équipe bêta de l’IA dédiée au contenu et à Commerce pour recevoir vos `analyzer_id` pour ce service.

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
| `analyzer_id` | Identifiant du service [!DNL Sensei] sous lequel votre requête est déployée. Cet identifiant détermine les [!DNL Sensei Content Frameworks] utilisés. Pour les services personnalisés, contactez l’équipe IA dédiée au contenu et à Commerce pour configurer un identifiant personnalisé. | Oui |
| `application-id` | Identifiant de l’application créée. | Oui |
| `data` | Un tableau qui contient un objet JSON avec chaque objet dans le tableau représentant un document. Tous les paramètres transmis dans le cadre de ce tableau remplacent les paramètres globaux spécifiés en dehors du tableau `data`. Toutes les propriétés restantes décrites ci-dessous dans ce tableau peuvent être remplacées à partir de `data`. | Oui |
| `language` | Langue du texte saisi. La valeur par défaut est `en`. | Non |
| `content-type` | Utilisé pour indiquer si l’entrée fait partie du corps de la requête ou d’une URL signée pour un compartiment S3. La valeur par défaut de cette propriété est `inline`. | Non |
| `encoding` | Format de codage du texte saisi. Cela peut être `utf-8` ou `utf-16`. La valeur par défaut de cette propriété est `utf-8`. | Non |
| `threshold` | Seuil de score (0 à 1) au-dessus duquel les résultats doivent être renvoyés. Utilisez la valeur `0` pour renvoyer tous les résultats. La valeur par défaut de cette propriété est `0`. | Non |
| `top-N` | Nombre de résultats à renvoyer (ne peut pas être un entier négatif). Utilisez la valeur `0` pour renvoyer tous les résultats. Lorsqu’il est utilisé conjointement avec `threshold`, le nombre de résultats renvoyés est la plus faible des deux limites définies. La valeur par défaut de cette propriété est `0`. | Non |
| `custom` | Tout paramètre personnalisé à transmettre. Cette propriété nécessite un objet JSON valide pour fonctionner. | Non |
| `content-id` | ID unique de l’élément de données renvoyé dans la réponse. Si cet identifiant n’est pas transmis, un identifiant généré automatiquement est attribué. | Non |
| `content` | Contenu utilisé par le service de classification de texte. Le contenu peut être du texte brut (type de contenu « inline »). <br> Si le contenu est un fichier sur S3 (type de contenu « s3-bucket »), transmettez l’URL signée. | Oui |

**Réponse**

Une réponse réussie renvoie le texte classifié dans un tableau de réponse.

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
