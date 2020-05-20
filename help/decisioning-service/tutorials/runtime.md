---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utilisation de l’exécution du service de prise de décision à l’aide d’API
topic: tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a
workflow-type: tm+mt
source-wordcount: '2022'
ht-degree: 0%

---


# Utilisation de l’exécution du service de prise de décision à l’aide d’API

Ce document fournit un didacticiel pour l’utilisation des services d’exécution de Decisioning Service à l’aide des API Adobe Experience Platform.

## Prise en main

Ce didacticiel nécessite une bonne compréhension des services Experience Platform impliqués dans la prise de décision et la détermination de la prochaine meilleure offre à présenter lors des expériences client. Avant de commencer ce didacticiel, consultez la documentation relative aux éléments suivants :

- [Service](./../home.md)de prise de décision : Fournit la structure permettant d’ajouter et de supprimer des offres et de créer des algorithmes pour choisir le meilleur à présenter lors de l’expérience d’un client.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.
- [Langage de Requête de Profil (PQL)](../../segmentation/pql/overview.md): PQL est utilisé pour définir des règles et des filtres.
- [Gérez les objets et les règles de prise de décision à l’aide des API](./entities.md): Avant d’utiliser le runtime des services de prise de décision, vous devez configurer les entités associées.

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître pour pouvoir invoquer les API de plate-forme.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../tutorials/authentication.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

Également requis pour les demandes d’exécution :

- x-request-id : `{UUID}`

>[!NOTE] `UUID` est une chaîne au format UUID unique au niveau mondial et ne doit pas être réutilisée pour différents appels d’API.

Le service de prise de décision est contrôlé par un certain nombre d’objets métier qui sont liés les uns aux autres. Tous les objets métier sont stockés dans le référentiel d’objets métier de la plate-forme, le référentiel d’objets XDM Core. L&#39;une des principales fonctionnalités de ce référentiel est que les API sont orthogonales par rapport au type d&#39;objet métier. Au lieu d&#39;utiliser une API POST, GET, PUT, PATCH ou DELETE qui indique le type de ressource dans son point de terminaison API, il n&#39;y a que 6 points de terminaison génériques, mais ils acceptent ou retournent un paramètre qui indique le type de l&#39;objet lorsque cette désambiguïfication est nécessaire. Le schéma doit être enregistré dans le référentiel, mais au-delà, le référentiel est utilisable pour un ensemble ouvert de types d&#39;objet.

Chemins d’accès aux points de terminaison pour tous les API du référentiel d’objets de base XDM début `https://platform.adobe.io/data/core/ode/`.

Le premier élément de chemin suivant le point de terminaison est le `containerId`. Cet identifiant est obtenu via le point de terminaison racine du référentiel d’objets de base XDM `GET https://platform.adobe.io/data/core/xcore/`.

## Compilation de modèles de décision

L&#39;activation des entités logiques métier se produit automatiquement et en permanence. Dès qu&#39;une nouvelle option est enregistrée dans le référentiel et qu&#39;elle est marquée comme &quot;approuvée&quot;, elle sera candidate à l&#39;inclusion de l&#39;ensemble d&#39;options disponibles. Dès qu&#39;une règle de décision est mise à jour, l&#39;ensemble de règles est réassemblé et préparé pour l&#39;exécution. À cette étape d’activation automatique, toutes les contraintes définies par la logique métier qui ne dépendent pas du contexte d’exécution seront évaluées. Les résultats de cette étape d’activation sont envoyés dans un cache où ils sont disponibles pour l’exécution du service de prise de décision.

### Effets des placements, des filtres et des états de cycle de vie

Les Offres sont créées en continu, leur état de cycle de vie change ou elles peuvent obtenir de nouvelles représentations de contenu. Le filtre d’offre d’une activité peut changer, correspondre ou filtrer les offres dont les jeux de balises ont été mis à jour. Ce processus peut être relativement impliqué et les demandes et les services doivent savoir quel sera le groupe de candidats à l&#39;activité qui en résultera. L’exécution de la décision fournit une API activité à offre qui filtres les offres qui ne sont pas approuvées, ne correspondent pas au filtre d’offre ou n’ont pas de représentation pour l’emplacement référencé par l’activité.

**Requête**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/offers?activityId={ACTIVITY_URI}' \
  -H 'Accept: application/vnd.adobe.xdm+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

**Réponse**

Le paramètre `activityId` peut être répété dans l’url et jusqu’à 30 références d’activité différentes peuvent être données dans une seule requête. La réponse sera utile pour repérer les circonstances inattendues résultant de la configuration et ressemblera à :

```json
{
  "xdm:activityOffers": [
    {
      "xdm:offerActivity": {
        "@id": "{ACTIVITY_URI}",
        "_links": {
          "self": {
            "href": "{repository_endpoint}/{CONTAINER_ID}/instances/{ACTIVITY_INSTANCE_ID}"
          }
        },
        "repo:etag": "1"
      },
      "xdm:offers": [
        {
          "@id": "{OFFER_URI_1}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_1}"
            }
          },
          "repo:etag": "15"
        },
        {
          "@id": "{OFFER_URI_2}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_2}"
            }
          },
          "repo:etag": "5"
        }
      ],
      "xdm:fallbackOffer": {
        "@id": "{FALLBACK_URI}",
        "_links": {
          "self": {
            "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{FALLBACK_INSTANCE_ID}"
          }
        },
        "repo:etag": "2"
      }
    }
  ]
}
```

Un léger délai de quelques secondes s’écoule entre le moment où les objets ont été mis à jour et celui où la réponse de l’API reflète le mappage activité-offre. La révision de chaque objet est indiquée dans la réponse afin que les clients puissent vérifier s’il existe une mise à jour des objets qui n’a pas été reflétée.

### API de diagnostic et dépannage

Les Activités, offres et règles d&#39;éligibilité sont compilées dans un format interne (catalogue d&#39;offres d’exécution) utilisé par le runtime du service de décision. La compilation peut détecter des erreurs qui n&#39;ont pas été détectées par les vérifications effectuées lorsque les objets ont été stockés et que des liens ont été établis dans le référentiel d&#39;objets de base XDM.

Une API de diagnostic est fournie pour obtenir toutes les erreurs de compilation survenues au cours de cette étape et, au cas où il n’y aurait aucune erreur pour obtenir des informations sur le moment où les règles et les activités ont été recompilées pour la dernière fois.

**Requête**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/diagnostics \
  -H 'Accept: application/vnd.adobe.xdm+json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

Le seul paramètre pour cet appel d&#39;API est `containerId`. Le résultat est toutes les mises à jour de tous les clients qui ont modifié les règles de décision, les offres, les activités ou les filtres d&#39;offre dans ce conteneur. Il y a un léger retard de quelques secondes entre le moment où les objets ont été mis à jour et le moment où la compilation se termine. L&#39;horodatage de la dernière mise à jour et les erreurs éventuelles sont renvoyés dans la réponse à l&#39;appel de diagnostic.

**Réponse**

```json
{
  "xdm:operations": {
    "xdm:offerCatalogUpdate": {
      "xdm:date": "2019-06-19T23:28:44.855Z",
      "xdm:errors": []
    },
    "xdm:activitiesUpdate": {
      "xdm:date": "2019-06-19T23:28:40.114Z",
      "xdm:errors": []
    }
  }
}
```

## Appels de l&#39;API REST pour exécuter les décisions

L’API REST est l’un des itinéraires pour les applications s’exécutant sur la plate-forme afin d’obtenir la meilleure expérience possible en fonction des règles, modèles et contraintes définis par l’entreprise pour ses utilisateurs. Les applications envoient l’une des identités du profil (ID de profil et espace de nommage d’identité) que le service de prise de décision consulte le profil et les informations sont utilisées pour appliquer la logique métier. Des données contextuelles supplémentaires peuvent être transmises à la demande et si elles sont spécifiées dans les règles de fonctionnement, elles seront incluses dans les données pour prendre la décision.

Les applications peuvent obtenir de meilleures performances en demandant une décision pour jusqu&#39;à 30 activités à la fois. Les URI des activités sont transmis dans la même requête. L’API REST est synchrone et renvoie les options proposées pour toutes ces activités ou l’option de secours si aucune option de personnalisation ne satisfait aux contraintes.

Il est possible que deux activités différentes proposent la même option que leur &quot;meilleur&quot;. Pour éviter de répéter une expérience composée, le service de prise de décision arbitre par défaut entre les activités référencées dans la même requête. L&#39;arbitrage signifie que pour chacune des activités, les options du top N sont prises en considération, mais aucune option ne sera proposée à plusieurs reprises dans ces activités. Si deux activités ont la même option classée en tête de liste, l&#39;une d&#39;elles sera élue pour utiliser son deuxième meilleur choix ou son troisième meilleur, etc. Ces règles de déduplication tentent d&#39;éviter que l&#39;une des activités n&#39;utilise son option de secours.

La demande de décision contient les arguments qu&#39;elle contient pour une demande POST. Le corps est formaté en tant que valeur d’ `Content-Type` en-tête JSON. `application/vnd.adobe.xdm+json; schema="{REQUEST_SCHEMA_AND_VERSION}"`

Le schéma de demande et la version pris en charge pour l’instant sont `https://ns.adobe.com/experience/offer-management/decision-request;version=0.9`. À l’avenir, d’autres schémas ou versions de demande seront fournis.

**Requête**

```shell
curl -X POST {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/decisions \
  -H 'Accept: application/json, application/problem+json \
  -H '
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '{
  "xdm:dryRun": {DRY_RUN_TRUE_FALSE},
  "xdm:validateContextData": {VALIDATE_CONTEXT_DATA_TRUE_FALSE},

  "xdm:offerActivities":[
    {
      "xdm:offerActivity": "{ACTIVITY_URI_1}"
    },
  ],
  "xdm:identityMap":{
    "{PROFILE_ID_NAMESPACE_CODE}":[
      {
        "xdm:id":"{PROFILE_ID}"
      }
    ]
  },
  "xdm:profileModel":"{PROFILE_MODEL}",
  "xdm:contextData": [
    {
      "@type": "{CONTEXT_DATASSCHEMA_ID}"
      "xdm:data": { JSON PROPERTIES OF CONTEXT ENTITY }
    }
  ] ,
  "xdm:allowDuplicatePropositions": {
    "xdm:acrossActivities": {DUPLICATE_OFFER_IDS_OF_TRUE_FALSE},
  }
}’
```

- **`xdm:dryRun`** - Lorsque la valeur de cette propriété facultative est définie sur true, la demande de décision obéira à des contraintes de plafonnement mais ne tirera pas réellement ces compteurs, il est prévu que l&#39;appelant n&#39;a jamais l&#39;intention de présenter la proposition au profil. Le Service de prise de décision n&#39;enregistrera pas la proposition comme événement de décision officiel de XDM et n&#39;apparaîtra pas dans les jeux de données de rapports. La valeur par défaut de cette propriété est false et lorsque la propriété est omise, la décision n&#39;est pas considérée comme une série d&#39;essais et doit donc être présentée à l&#39;utilisateur final.
- **`xdm:validateContextData`** - Cette propriété facultative active ou désactive la validation des données contextuelles. Si la validation est activée, pour chaque élément de données contextuelles fourni, le schéma (d’après le `@type` champ) est extrait du registre XDM et l’ `xdm:data` objet est validé par rapport à celui-ci.

La demande par ce schéma contient un tableau d&#39;URI référençant les activités d&#39;offre, une identité de profil et un tableau d&#39;éléments de données contextuelles :

- **`xdm:offerActivities`** - Cette propriété obligatoire est un tableau d&#39;objets où chaque élément contient des données sur l&#39;activité d&#39;offre. L’activité d’offre possède les propriétés suivantes :
   - **`xdm:offerActivity`** - L&#39;identificateur unique (URI) de l&#39;activité. Il s’agit de la valeur de la `@id` propriété de l’activité d’offre.
- **`xdm:identityMap`** - Propriété obligatoire contenant un objet JSON conforme au schéma XDM `https://ns.adobe.com/xdm/context/identitymap`. La propriété définit un mappage où la clé est un code d’espace de nommage d’identité et la valeur est une liste d’identifiants d’utilisateur final dans l’espace de nommage donné. Si m.
- **`xdm:contextData`** - Propriété facultative contenant des éléments décrits par une référence à leur schéma. Chaque élément de données contextuelles du tableau doit avoir les propriétés suivantes :
   - **`@type`** - Propriété obligatoire référençant le schéma XDM de l&#39;objet dans cet élément.
   - **`xdm:data`** - Propriété obligatoire contenant les propriétés d&#39;objet selon le schéma XDM indiqué dans la `@type` propriété.

## Données contextuelles dynamiques dans les demandes de décision

La section précédente indique comment les objets XDM peuvent être transmis à une demande de décision. Voici un exemple de ce tableau d’objets contextuels :

```json
"xdm:contextData": [
  {
    "@type":" https://ns.adobe.com/{TENANT_ID_OF_ORG}/schemas/{NUMERIC_SCHEMA_ID};version=1",
    "xdm:data":{ 
      "{TENANT_ID_OF_ORG}": {
        "productDetails":{ 
          "xdm:gender":      "unisex",
          "xdm:fabrication": "leather",
          "xdm:category":    "wallets",
        }
      }
    }
  }
]
```

Le schéma doit avoir été construit par votre organisation. Pour en savoir plus sur la construction de schémas, consultez le didacticiel [de l&#39;éditeur de](../../xdm/tutorials/create-schema-ui.md)Schémas. Votre schéma sera dans un espace de nommage `https://ns.adobe.com/{TENANT_ID}/schemas`.

Le guide [du développeur de l&#39;API](../../xdm/tutorials/create-schema-api.md) Schéma Registry explique comment accéder aux schémas par programmation et comment un développeur obtient l&#39;ID de client et l&#39;identifiant numérique de votre schéma. Le numéro de version est requis et est également fourni par les API du Registre du schéma.

Un schéma défini par une organisation a généralement une propriété racine nommée `_{TENANT_ID}`, également appelée chaîne d&#39;espace de nommage du client.
Notez que les propriétés utilisées à partir d’un composant de schéma global tel que _`https://ns.adobe.com/xdm/context/product` ont un préfixe d’espace de nommage `xdm:`. Dans ce cas, la propriété définie par l’organisation `productDetails` a été construite avec ce type de données. Bien que les propriétés du client soient imbriquées dans une propriété nommée d’après l’espace de nommage du client, les types de données disponibles dans le monde entier utilisent le préfixe réservé `xdm:` pour empêcher les collisions de noms de propriété.

Plusieurs objets de données peuvent être répertoriés dans la `xdm:contextData` propriété. Chaque objet doit identifier son type via la `@type` propriété.
Les valeurs des objets de données contextuelles peuvent être utilisées dans des expressions PQL, par exemple dans la condition d’une règle d&#39;éligibilité. L&#39;objet de données contextuelles doit être traité par l&#39;expression spéciale de référence de chemin `@{schemaId}`. Les expressions qui suivent cette expression de référence sont des expressions de chemin d’accès régulières qui accèdent aux propriétés de l’objet de données :

```json
{
  "xdm:name": "Eligible for a free gender-specific item of interest",
  "xdm:condition": {
    "xdm:value":
      "gender in (\"female\",\"non-specific\")  
       and (
         select p from
           @{https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}._{TENANT_ID}
         select e from xEvent 
            where e.type = \"productSearch\" 
              and e.category = p.category 
              and p.gender in (\"female\",\"unisex\")
       )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

Dans l’exemple ci-dessus, la variable `p` effectue une itération sur le tableau des objets marqués avec le `@type` = `https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}`.

Notez que la syntaxe PQL n’utilise pas de préfixes dans les noms de propriété. Par défaut, les propriétés globales sont simplement référencées sans le `xdm:` préfixe. Les propriétés définies par votre organisation sont imbriquées dans une propriété **supplémentaire** nommée d’après l’espace de nommage locataire (dans l’exemple indiqué par la variable `{TENANT_ID}`). Pour pouvoir référencer directement les propriétés personnalisées, la variable `p` est liée au résultat du chemin qui déréférence la propriété d’imbrication supplémentaire.

## Utilisation des enregistrements de profil

Tous les enregistrements des entités de événement de profil et d’expérience sont déjà gérés dans le magasin de profils. En transmettant une ou plusieurs identités de profil à la demande, le profil de ces identités sera identifié et consulté à partir du magasin. Les données sont alors automatiquement disponibles pour les règles de décision et les modèles évalués par la stratégie de décision.

Pour récupérer les enregistrements de profil et d’expérience, la stratégie de fusion par défaut est appliquée.
Notez qu&#39;après avoir téléchargé des enregistrements de profil dans la base de données de la plate-forme, il y a un léger retard jusqu&#39;à ce que les enregistrements de profil puissent être recherchés. Il en va de même pour l’assimilation d’enregistrements de profil et d’expérience via les API de diffusion en continu, et ce n’est qu’après quelques secondes que les données seront disponibles pour l’évaluation des règles de décision qui évaluent les données du événement de profil et d’expérience.