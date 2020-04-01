---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Utilisation de l’exécution du service de prise de décision à l’aide d’API
topic: tutorial
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Utilisation de l’exécution du service de prise de décision à l’aide d’API

Ce fournit un didacticiel pour travailler avec les services d’exécution de Decisioning Service à l’aide des API Adobe Experience Platform.

## Prise en main

Ce didacticiel nécessite une compréhension pratique des services Experience Platform impliqués dans la prise de décision et la détermination du prochain meilleur  à présenter lors des expériences client. Avant de commencer ce didacticiel, veuillez consulter la documentation relative aux éléments suivants :

- [Service](./../home.md)de prise de décision : Fournit la structure permettant d’ajouter et de supprimer   et de créer des algorithmes pour choisir le meilleur à présenter lors de l’expérience d’un client.
- [Modèle de données d’expérience (XDM)](../../xdm/home.md): Cadre normalisé selon lequel la plateforme organise les données d’expérience client.
- [ langue (PQL)](../../segmentation/pql/overview.md): PQL est utilisé pour définir des règles et des  de.
- [Gérez les objets et les règles de prise de décision à l’aide des API](./entities.md): Avant d’utiliser le runtime des services de prise de décision, vous devez configurer les entités associées.

Les sections suivantes fournissent des informations supplémentaires que vous devez connaître pour pouvoir effectuer des appels aux API de plateforme.

### Lecture des exemples d’appels d’API

Ce didacticiel fournit des exemples d’appels d’API pour démontrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur la [manière de lire des exemples d’appels](../../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage de la plateforme d’expérience.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [sur l’](../../tutorials/authentication.md)authentification. Le didacticiel sur l’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme illustré ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id : `{IMS_ORG}`

Toutes les ressources de la plateforme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes des API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../../tutorials/authentication.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

Également requis pour les demandes d’exécution :

- x-request-id : `{UUID}`

>[!NOTE] `UUID` est une chaîne au format UUID unique au niveau mondial et ne doit pas être réutilisée pour différents appels d’API.

Le service de prise de décision est contrôlé par un certain nombre d’objets commerciaux qui sont liés les uns aux autres. Tous les objets d’entreprise sont stockés dans le référentiel d’objets d’entreprise de la plate-forme, le référentiel d’objets XDM Core. Une caractéristique clé de ce référentiel est que les API sont orthogonales par rapport au type d’objet métier. Au lieu d’utiliser une API POST, GET, PUT, PATCH ou DELETE qui indique le type de ressource dans son point de terminaison API, il n’y a que 6 points de terminaison génériques, mais ils acceptent ou renvoient un paramètre qui indique le type de l’objet lorsque cette désambiguïté est nécessaire. Le doit être enregistré dans le référentiel, mais au-delà, le référentiel peut être utilisé pour un ensemble illimité de types d’objets.

Chemins d’accès des points de fin de toutes les API du référentiel d’objets de base XDM  avec `https://platform.adobe.io/data/core/ode/`.

Le premier élément de chemin suivant le point de fin est le `containerId`. Cet identifiant est obtenu via le point de terminaison racine du référentiel d’objets de base XDM `GET https://platform.adobe.io/data/core/xcore/`.

## Compilation de modèles de décision

Le  des entités de logique métier se produit automatiquement et en permanence. Dès qu’une nouvelle option est enregistrée dans le référentiel et qu’elle est marquée comme &quot;approuvée&quot;, elle sera candidate pour l’inclusion de l’ensemble des options disponibles. Dès qu’une règle de décision est mise à jour, l’ensemble de règles est réassemblé et préparé pour l’exécution au moment de l’exécution. À cette étape automatique de  , toutes les contraintes définies par la logique métier qui ne dépendent pas du contexte d’exécution seront évaluées. Les résultats de cette   d&#39;étape sont envoyés dans un cache où ils sont disponibles pour le moteur d&#39;exécution du service de prise de décision.

### Effets des placements, des  et des états de cycle de vie

  sont créés en permanence, des modifications se produisent dans leur état de cycle de vie ou de nouvelles représentations de contenu peuvent leur être envoyées. Le filtre de  d’un peut changer ou correspondre ou filtrer lesdont les jeux de balises ont été mis à jour. Ce processus peut être relativement impliqué et les demandes et les services doivent savoir quel sera le jeu de candidats et candidates résultant d&#39;un  de . Le moteur d’exécution de la décision fournit une API  de -à- qui permet desupprimer les non approuvés, qui ne correspondent pas au filtre de du ou qui n’ont pas de représentation pour l’emplacement référencé par le de laprogrammation.

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

Le paramètre `activityId` peut être répété dans l’URL et jusqu’à 30 références  différentes  peuvent être données dans une seule requête. La réponse sera utile pour détecter les circonstances inattendues résultant de la configuration et ressemblera à :

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

Il y a un léger délai de quelques secondes entre le moment où les objets ont été mis à jour et le moment où la réponse de l’API reflète le mappage  de l’ à . La révision de chaque objet est donnée dans la réponse afin que les clients puissent vérifier s’il existe une mise à jour des objets qui n’a pas été reflétée.

### API de diagnostic et dépannage

  de,  de et desont compilés dans un format interne (d’exécution) utilisé par le moteur d’exécution du service de décision. La compilation peut détecter des erreurs qui n’ont pas été détectées par les vérifications effectuées lorsque les objets ont été stockés et que des liens ont été établis dans le référentiel d’objets de base XDM.

Une API de diagnostic est fournie pour obtenir toutes les erreurs de compilation survenues au cours de cette étape et, au cas où il n’y aurait aucune erreur pour obtenir des informations sur le moment où les règles et les  de  ont été recompilées pour la dernière fois.

**Requête**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/diagnostics \
  -H 'Accept: application/vnd.adobe.xdm+json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

Le seul paramètre pour cet appel d’API est `containerId`. Le résultat est toutes les mises à jour de tous les clients qui ont modifié les règles de décision,  ,  de ou de dedans ce. Un léger délai de quelques secondes s’écoule entre le moment où les objets ont été mis à jour et celui où la compilation s’est terminée. L’horodatage de la dernière mise à jour et les erreurs éventuelles sont renvoyées dans la réponse à l’appel de diagnostic.

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

## Appels de l’API REST pour exécuter des décisions

L’API REST est l’un des itinéraires des applications s’exécutant sur la plate-forme afin d’obtenir la meilleure expérience possible en fonction des règles, modèles et contraintes définis par l’entreprise pour ses utilisateurs. Les applications envoient l’une des identités de l’ (ID de et  de l’identité ), le service de prise de décision recherche l’identifiant et les informations sont utilisées pour appliquer la logique métier. Des données contextuelles supplémentaires peuvent être transmises à la requête et, si elles sont spécifiées dans les règles de fonctionnement, elles seront incluses dans les données pour prendre la décision.

Les applications peuvent obtenir de meilleures performances en demandant une décision pour un maximum de 30   à la fois. Les URI du   sont transmis dans la même requête. L’API REST est synchrone et renvoie les options proposées pour tous ces   ou l’option de secours si aucune option de personnalisation ne satisfait aux contraintes.

Il est possible que deux  différents  proposent la même option que leur &quot;meilleur&quot;. Pour éviter de répéter une expérience composée, le service de prise de décision arbitre par défaut entre les   référencées dans la même requête. L&#39;arbitrage signifie que pour chacun des   les options des N premiers sont prises en considération, mais aucune option ne sera proposée plus d&#39;une fois dans ces . Si deux   ont la même option classée en tête, l’un d’eux sera élu pour utiliser son deuxième meilleur choix ou son troisième meilleur et ainsi de suite. Ces règles de déduplication tentent d’éviter que l’un des   ne doive utiliser son option de secours.

La demande de décision contient les arguments qu&#39;elle contient dans une demande POST. Le corps est formaté en tant que valeur d’ `Content-Type` en-tête JSON. `application/vnd.adobe.xdm+json; schema="{REQUEST_SCHEMA_AND_VERSION}"`

La  de requête et la version prises en charge pour le moment sont `https://ns.adobe.com/experience/offer-management/decision-request;version=0.9`. À l’avenir, d’autres  ou versions de demande seront fournies.

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

- **`xdm:dryRun`** - Lorsque la valeur de cette propriété facultative est définie sur true, la demande de décision obéit à des contraintes de plafonnement mais ne tire pas réellement vers le bas ces compteurs, il est prévu que l’appelant n’ait jamais l’intention de présenter la proposition au. Le Service de prise de décision n&#39;enregistrera pas la proposition comme un de décision XDM officiel et n&#39;apparaîtra pas dans les jeux de données de . La valeur par défaut de cette propriété est false et lorsque la propriété est omise, la décision n’est pas considérée comme une série d’essais et doit donc être présentée à l’utilisateur final.
- **`xdm:validateContextData`** - Cette propriété facultative active ou désactive la validation des données contextuelles. Si la validation est activée, pour chaque élément de données contextuelles fourni, le  (basé sur le `@type` champ) est récupéré du registre XDM et l’ `xdm:data` objet est validé par rapport à lui.

La requête en vertu de ce contient un tableau d&#39;URI référençant  de , une identité de et un tableau d&#39;éléments de données contextuelles :

- **`xdm:offerActivities`** - Cette propriété obligatoire est un tableau d&#39;objets dans lequel chaque élément contient des données sur le    de . Le    de  a les propriétés suivantes :
   - **`xdm:offerActivity`** - L&#39;identificateur unique (URI) du  . Il s’agit de la valeur de la `@id` propriété de la    .
- **`xdm:identityMap`** - Une propriété obligatoire contenant un objet JSON conforme au  XDM `https://ns.adobe.com/xdm/context/identitymap`. La propriété définit un mappage où la clé est une identité  le code  du et où la valeur est un des identifiants d’utilisateur final dans le donné. Si.
- **`xdm:contextData`** - Une propriété facultative qui contient des éléments décrits par une référence à leur  de. Chaque élément de données contextuelles du tableau doit avoir les propriétés suivantes :
   - **`@type`** - Une propriété obligatoire référençant le  XDM de l&#39;objet dans cet élément.
   - **`xdm:data`** - Une propriété obligatoire contenant les propriétés de l&#39;objet selon la  XDM donnée dans la `@type` propriété.

## Données contextuelles dynamiques dans les demandes de décision

La section précédente indique comment les objets XDM peuvent être transmis à une demande de décision. Voici un exemple de ce type de tableau d’objets contextuels :

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

Le doit avoir été construit par votre organisation. Pour en savoir plus sur la construction de  de, consultez le [didacticiel](../../xdm/tutorials/create-schema-ui.md)de l&#39;éditeur de  de. Votre  sera dans un  `https://ns.adobe.com/{TENANT_ID}/schemas`.

Le guide [du développeur](../../xdm/tutorials/create-schema-api.md) d&#39;API de Registre  explique comment accéder aux  par programmation et comment un développeur obtient l&#39;ID de locataire et l&#39;identificateur numérique de votre. Le numéro de version est requis et est également fourni par les API de Registre des  de.

Un défini par une organisation a généralement une propriété racine nommée `_{TENANT_ID}`, également appelée chaîne de   de locataire.
Notez que les propriétés utilisées à partir d’un composant  global tel que _`https://ns.adobe.com/xdm/context/product` possèdent un préfixe  de `xdm:`. Dans ce cas, la propriété définie par l’organisation `productDetails` a été construite avec ce type de données. Bien que les propriétés du client soient imbriquées dans une propriété nommée en fonction de l’ du du client, les types de données disponibles dans le monde entier utilisent le préfixe réservé `xdm:` pour empêcher les collisions de noms de propriété.

Plusieurs objets de données peuvent être répertoriés dans la `xdm:contextData` propriété. Chaque objet doit identifier son type via la `@type` propriété.
Les valeurs des objets de données contextuelles peuvent être utilisées dans le  PQL, par exemple dans la condition d’un . L’objet de données contextuelles doit être traité par le biais de la référence de chemin d’accès spéciale   `@{schemaId}`. Les   qui suivent cette référence  les sont des de chemin ordinaires qui accèdent aux propriétés de l’objet de données :

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

Dans l’exemple ci-dessus, la variable `p` effectue une itération sur le tableau des objets marqués par le `@type` = `https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}`.

Notez que la syntaxe PQL n’utilise pas de préfixes dans les noms de propriété. Par défaut, les propriétés globales sont simplement référencées sans le `xdm:` préfixe. Les propriétés définies par votre organisation sont imbriquées dans une propriété **supplémentaire** nommée d’après le  locataire  (dans l’exemple indiqué par la variable `{TENANT_ID}`). Pour pouvoir référencer directement les propriétés personnalisées, la variable `p` est liée au résultat du chemin qui déréférence la propriété d’imbrication supplémentaire.

## Utilisation des enregistrements 

Tous les enregistrements des entités de  et de d’expérience sont déjà gérés dans le magasin de  d’expérience. En transmettant une ou plusieurs  d&#39;identité à la demande, le  ces identités sera identifié et regardé depuis le magasin. Les données sont alors automatiquement disponibles pour les règles de décision et les modèles évalués par la stratégie de décision.

Pour récupérer le  et les enregistrements d’expérience, la stratégie de fusion par défaut est appliquée.
Notez qu’après avoir téléchargé des enregistrements  vers la plate-forme, il y a un léger retard jusqu’à ce que les enregistrements  puissent être recherchés. Il en va de même pour l’assimilation des enregistrements d’ et d’expérience par le biais des API de diffusion en continu. Ce n’est qu’au bout de quelques secondes que les données seront disponibles pour l’évaluation des règles de décision qui évaluent les données de et de l’expérience de base des données de l’.