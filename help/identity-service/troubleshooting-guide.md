---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de dépannage d’Adobe Experience Platform Identity Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Guide de dépannage du service Identity Service

Ce fournit des réponses aux questions les plus fréquentes sur Adobe Experience Platform Identity Service, ainsi qu’un guide de dépannage pour les erreurs courantes. Pour toute question ou dépannage concernant les API de plateforme en général, consultez le guide [de dépannage des API de plateforme](../landing/troubleshooting.md)Adobe Experience Platform.

Les données qui identifient un client unique sont souvent fragmentées entre les différents périphériques et systèmes qu’il utilise pour interagir avec votre marque. **Le service** d’identité rassemble ces identités fragmentées, ce qui permet une compréhension complète du comportement des clients afin que vous puissiez offrir des expériences numériques impactées en temps réel. Pour plus d&#39;informations, consultez la présentation [du service](./home.md)d&#39;identité.

## FAQ

Voici un  de réponses aux questions les plus fréquentes sur Identity Service.

## Qu&#39;est-ce que les données d&#39;identité ?

Les données d’identité sont des données qui peuvent être utilisées pour identifier une personne. Selon le contexte d’utilisation des données au sein de votre entreprise, les données d’identité peuvent inclure des noms d’utilisateur, des adresses électroniques et des ID provenant de systèmes CRM. Les données d’identité ne sont pas limitées aux utilisateurs enregistrés de votre site Web ou service, car les utilisateurs anonymes peuvent également être identifiés par leur appareil ou leur ID de cookie.

## Quel est l’avantage de définir les champs de données comme identités ?

L’étiquetage de certains champs de données comme identités dans vos données d’enregistrement et de série chronologique vous permet de mettre en correspondance les relations d’identité dans la structure naturelle de vos données et de concilier les  de données entre les . See the [Identity Service overview](./home.md) for more information.

## Quelles sont les identités connues et anonymes ?

Une identité **** connue fait référence à une valeur d&#39;identité qui peut être utilisée seule ou avec d&#39;autres informations pour identifier, contacter ou localiser une personne. Les adresses électroniques, les numéros de téléphone et les identifiants CRM sont des exemples d’identités connues.

Une identité **** anonyme fait référence à une valeur d’identité qui ne peut pas être utilisée seule ou avec d’autres informations pour identifier, contacter ou localiser une personne (comme un ID de cookie).

## Qu&#39;est-ce qu&#39;un graphique d&#39;identité privée ?

Un graphique d’identité privée est une carte privée des relations entre les identités recoupées et liées, visible uniquement pour votre entreprise.

Lorsque plusieurs identités sont incluses dans des données assimilées à partir d’un point de fin de diffusion en continu ou envoyées à un jeu de données activé pour Identity Service, elles sont liées dans le graphique d’identité privée. Identity Service utilise ce graphique pour rassembler les identités d&#39;un consommateur ou d&#39;une entité donné, ce qui permet de fusionner les identités et les  d&#39;identité.

## Comment créer plusieurs champs d’identité dans un  XDM ?

[Modèle de données d’expérience (XDM)](../xdm/home.md) prend en charge plusieurs champs d’identité. Tout champ de données de type `string` dans un qui implémente le individuel XDM ou la classe XDM ExperienceEvent peut être étiqueté comme champ d’identité. Une fois étiquetées, toutes les données contenues dans ces champs sont ajoutées à la carte d’identité  du.

Pour savoir comment étiqueter un champ XDM en tant que champ d’identité à l’aide de l’interface utilisateur, consultez la section [](../xdm/tutorials/create-schema-ui.md) Identité du didacticiel de l’éditeur de . Si vous utilisez l’API, reportez-vous à la section [descripteur d’](../xdm/tutorials/create-schema-api.md) identité du didacticiel sur l’API de registre des .

## Y a-t-il des  où certains champs ne doivent pas être identifiés comme identités ?

Les champs d’identité doivent être réservés aux valeurs propres à chaque individu. Prenons l’exemple d’un jeu de données pour un  de fidélité des clients. Le champ &quot;niveau de fidélité&quot; (or, argent, bronze) ne serait pas un champ d’identité utile, tandis que l’ID de fidélité, une valeur unique, le serait.

Les champs tels que les codes postaux et les adresses IP ne doivent pas être marqués comme des identités pour les individus, car ces valeurs peuvent s’appliquer à plusieurs personnes individuelles. Ces types de champs ne doivent être étiquetés que comme identités pour les stratégies marketing au niveau des ménages.

## Pourquoi mes champs d&#39;identité ne sont-ils pas liés comme je m&#39;y attends ?

À l’aide du [`/cluster/members` point de fin](./api/list-cluster-identites.md) de l’API Identity Service, vous pouvez  les identités associées pour un ou plusieurs champs d’identité. Si la réponse ne renvoie pas les identités liées attendues, veillez à fournir les informations d’identité appropriées dans vos données XDM. Pour plus d&#39;informations, consultez la section relative à la [fourniture de données XDM au service](./home.md) d&#39;identité dans l&#39;aperçu du service d&#39;identité.

## Qu&#39;est-ce qu&#39;une identité   ?

Un d&#39;identité   fournit le contexte de la manière dont les champs d&#39;identité se rapportent à l&#39;identité d&#39;un client. Par exemple, les champs d’identité sous le de  &quot;courriel&quot; doivent être conformes à un standard (nom<span>@emailprovider.com), tandis que les champs utilisant le &quot;téléphone&quot; doivent être conformes à un numéro de téléphone standard (par exemple, 987-555-1234 en Amérique du Nord).

  différencie les valeurs d&#39;identité similaires entre différents systèmes CRM. Prenons l’exemple d’un qui contient un identifiant de fidélité numérique associé à votre  de récompenses de. Un  de &quot;Fidélité&quot; séparerait cette valeur d’un ID numérique similaire pour votre système de commerce électronique, qui apparaît également dans le même .

See the [identity namespace overview](./home.md) for more information.

## Comment puis-je associer une identité à une  d&#39;identité  ?

Les champs d’identité doivent être associés à un d’identité  existant  lorsqu’ils sont créés. Tout nouveau  doit être [créé à l’aide de l’API](#how-do-i-create-a-custom-namespace-for-my-organization) avant de l’associer aux champs d’identité.

Pour obtenir des instructions détaillées sur la définition d&#39;un   lors de la création d&#39;un descripteur d&#39;identité à l&#39;aide de l&#39;API, reportez-vous à la section relative à la [création d&#39;un descripteur](../xdm/tutorials/create-schema-ui.md) dans le guide du développeur du Registre de. Pour marquer un champ de  de comme une identité dans l’interface utilisateur, suivez les étapes du didacticiel [de l’éditeur de  de](../xdm/tutorials/create-schema-api.md).

## Quels sont les  d’identité standard les  fournis par Experience Platform ?

Les  standard suivants sont fournis pour l’utilisation par toutes les organisations au sein de la plateforme d’expérience :

| Nom d’affichage | ID | Code | Description |
| ------------ | --- | --- | ----------- |
| CORE | 0 | CORE | nom hérité : &quot;Adobe AudienceManager&quot; |
| ECID | 4 | ECID | alias : &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot; |
| Courriel | 6 | Courriel |  |
| E-mail (SHA256, avec faible précision) | 11 | Emails  |  standard  pour les courriers électroniques préhachés. Les valeurs fournies dans ce   sont converties en minuscules avant le hachage avec SHA-256. |
| Téléphone | 7 | Téléphone |  |
| Windows AID | 8 | WAID |  |
| AdCloud | 411 | AdCloud | alias : Ad Cloud |
| Adobe Target | 9 | TNTID | ID  |
| Identifiant de publicité Google | 20914 | GAID | GAID |
| Apple IDFA | 20915 | IDFA | ID des annonceurs |

## Où puis-je trouver le  d&#39;identité  disponible pour mon organisation?

A l’aide de l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)Identity Service, vous pouvez  tous les  d’identité disponibles pour votre organisation en envoyant une requête GET au `/idnamespace/identities` point de terminaison. Pour plus d&#39;informations, reportez-vous à la section relative à la [liste des disponibles](./api/list-namespaces.md) dans l&#39;aperçu de l&#39;API Identity Service.

## Comment créer un  personnalisé pour mon organisation ?

A l’aide de l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)Identity Service, vous pouvez créer un d’identité  personnalisé pour votre organisation en envoyant une requête POST au `/idnamespace/identities` point de terminaison. Pour plus d’informations, reportez-vous à la section sur la [création d’un](./api/create-custom-namespace.md)  personnalisé dans l’aperçu de l’API Identity Service.

## Que sont les identités composites et les XID ?

Les identités sont référencées dans les appels d’API par leur identité composite ou XID. Une identité **** composite est une représentation d’une identité qui contient une valeur d’ID et un  . Un **XID** est un identifiant à une seule valeur qui représente le même concept qu’une identité composite (un ID et un  ) et qui est automatiquement affecté à de nouvelles identités lorsqu’il est conservé par Identity Service. Pour plus d’informations, consultez la présentation [de l’API](./home.md) Identity Service.

## Comment le service d&#39;identité gère-t-il les informations d&#39;identification personnelle ?

Identity Service crée un hachage cryptographique à sens unique et fort des informations d’identification personnelle avant les valeurs persistantes. Les données d’identité dans les  &quot;Téléphone&quot; et &quot;Courriel&quot; sont automatiquement hachées à l’aide de SHA-256, les valeurs &quot;Courriel&quot; étant automatiquement converties en minuscules avant le hachage.

## Dois-je chiffrer toutes les informations d’identification personnelle avant de les envoyer à Platform ?

Vous n’avez pas besoin de chiffrer manuellement les données d’identification personnelle avant de les importer dans Platform. En appliquant le libellé `I1` d’utilisation des données à tous les champs de données applicables, Platform convertit automatiquement ces champs en valeurs d’ID hachées lors de l’assimilation.

Pour savoir comment appliquer et gérer les étiquettes d’utilisation des données, reportez-vous au didacticiel [sur les étiquettes d’utilisation des](../data-governance/labels/user-guide.md)données.

## Y a-t-il des considérations à prendre en compte lors du hachage des identités basées sur les informations d&#39;identification personnelle ?

Si vous envoyez des valeurs d’identification personnelle hachées à Identity Service, vous devez utiliser la même méthode de chiffrement pour vos jeux de données. Cela permet de s’assurer que la même valeur d’identité entre les jeux de données génère les mêmes valeurs hachées et qu’elle est en mesure d’être correctement mise en correspondance et liée dans le graphique d’identité.

<!-- Documentation does not show any methods of editing the identityMap directly, and this table never overtly recommends using identityMap anyway. This should probably be removed unless PM thinks otherwise. -->
<!-- ## When should I use the Identity map rather than labeling individual XDM schema fields?

The following table describes when the recommended approach for including identity data in your XDM would be identity map and when an identity field is the better method.

>[!NOTE] An advantage `identityMap` has is the ability to include multiple identity values for a single namespace.

Write|XDM identity field|`identityMap`
---|---|---
UI|Supported|Supported
Developer|Recommended|Supported
ETL|Recommended|Avoid - While this is supported, data should be formatted naturally when using an ETL, favoring identity fields over `identityMap`.
Internal solutions|Preferred|Common

--- -->

## Résolution des problèmes

La section suivante fournit des suggestions de dépannage pour des codes d’erreur spécifiques et des comportements inattendus que vous pouvez rencontrer lors de l’utilisation de l’API Identity Service.

## Messages d’erreur du service d’identité

Voici un  de messages d’erreur que vous pouvez rencontrer lors de l’utilisation de l’API Identity Service.

### Paramètre  obligatoire manquant

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Cette erreur s’affiche lorsqu’un paramètre  obligatoire n’a pas été inclus dans le chemin de requête. Le message `detail` d’erreur indique le nom du paramètre manquant. Les variantes de ce message d’erreur incluent :

- Paramètre  obligatoire manquant - nsId
- Paramètre  obligatoire manquant - id
- Paramètre  requis manquant - xid ou (nsid,id)
- Paramètre  requis manquant - targetNs
- Paramètre  requis manquant - xids ou compositeXids

Vérifiez que vous incluez correctement le paramètre indiqué dans le chemin de requête avant de réessayer.

### L’horodatage doit être au cours des 180 derniers jours

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

Le service d’identité purge les données datant de plus de 180 jours. Ce message d’erreur s’affiche lorsque vous tentez d’accéder à des données antérieures à cette date.

### Il existe une limite de 1 000 XID dans un seul appel.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Ce message d’erreur s’affiche lorsque vous tentez de récupérer des informations d’identité pour plus d’un nombre maximal de [XID](#what-are-composite-identities-and-xids) autorisés dans un appel d’API unique. Réduisez le nombre de XID dans votre requête à une valeur inférieure à la limite affichée pour résoudre ce problème.


### Il existe une limite de 1 000 Xids composites dans un seul appel.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Ce message d’erreur s’affiche lorsque vous tentez de récupérer des informations d’identité pour plus d’un nombre maximal d’identités [](#what-are-composite-identities-and-xids) composites autorisé dans un seul appel d’API. Pour résoudre ce problème, réduisez le nombre d’identités composites dans votre requête au-dessous de la limite affichée.

### Le type de graphique spécifié n&#39;est pas valide

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Ce message d’erreur s’affiche lorsqu’une valeur non valide est attribuée à un paramètre de  `graph-type` dans le chemin de requête. Consultez la section sur les graphiques [d&#39;](./home.md) identité dans l&#39;aperçu du service Identity Service pour savoir quels types de graphiques sont pris en charge.

### Le jeton de service n&#39;a pas d&#39;étendue valide

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Ce message d’erreur s’affiche lorsque votre organisation IMS n’a pas reçu les autorisations appropriées pour Identity Service. Contactez votre administrateur système pour résoudre ce problème.

### Jeton de service de passerelle non valide

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

Dans le cas de cette erreur, votre  de n’est pas valide. Le expire toutes les 24 heures et doit être régénéré pour continuer à utiliser les API de plateforme. Consultez le didacticiel [sur l’](../tutorials/authentication.md) authentification pour obtenir des instructions sur la génération de nouveaux  de.

### Jeton de service d’autorisation non valide

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

Dans le cas de cette erreur, votre  de n’est pas valide. Le expire toutes les 24 heures et doit être régénéré pour continuer à utiliser les API de plateforme. Consultez le didacticiel [sur l’](../tutorials/authentication.md) authentification pour obtenir des instructions sur la génération de nouveaux  de.

### Le jeton utilisateur n’a pas de contexte de produit valide

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Ce message d’erreur s’affiche lorsque votre  de n’a pas été généré à partir d’une intégration de la plateforme d’expérience. Consultez le didacticiel [sur l’](../tutorials/authentication.md) authentification pour obtenir des instructions sur la génération de nouveaux  pour une intégration de la plateforme d’expérience.

### Erreur interne lors de l’obtention du XID natif à partir de l’identité et du code   du

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Lorsque le service d’identité persiste une identité, l’ID de l’identité et l’ID de associé sont associés à un identifiant unique appelé XID. Ce message s’affiche lorsqu’une erreur se produit lors du processus de recherche du XID pour une valeur d’ID donnée et du  de .

### L&#39;organisation IMS n&#39;est pas configurée pour l&#39;utilisation d&#39;Identity Service

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Ce message d’erreur s’affiche lorsque votre organisation IMS n’a pas reçu les autorisations appropriées pour Identity Service. Contactez votre administrateur système pour résoudre ce problème.

### Erreur interne du serveur

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Cette erreur s’affiche lorsqu’une exception inattendue se produit lors de l’exécution d’un appel de service Platform. Il est recommandé de  vos appels automatisés afin de relancer leurs requêtes à un intervalle de temps donné lors de la réception de cette erreur. Si le problème persiste, contactez votre administrateur système.

## Codes d&#39;erreur d&#39;assimilation par lot

Identity Service ingère des données d&#39;identité à partir des données d&#39;enregistrement et de série chronologique qui sont téléchargées sur la plateforme à l&#39;aide de la fonction d&#39;ingestion par lots. Comme l&#39;assimilation par lot est un processus asynchrone, vous devez  les détails d&#39;un lot pour les erreurs . Les erreurs s’accumulent au fur et à mesure que le lot avance jusqu’à ce que le lot soit terminé.

Vous trouverez ci-dessous un de messages d’erreur relatifs au service d’identité que vous pouvez rencontrer lors de l’utilisation de l’API [d’administration des](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)données.

### XDM inconnu

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

Identity Service utilise uniquement les identités pour les données d’enregistrement ou de série chronologique qui sont conformes aux classes  ou ExperienceEvent, respectivement. Toute tentative d&#39;assimilation de données pour Identity Service qui n&#39;adhère à aucune classe déclenchera cette erreur.

### Il y avait 0 identité valide dans les 100 premières lignes du lot traité

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Cette erreur s’affiche lorsque les 100 premières lignes d’un lot ne présentent aucune identité. Cette erreur n&#39;indique toutefois pas de manière concluante qu&#39;aucune identité n&#39;a été trouvée dans les enregistrements ultérieurs.

### Les enregistrements ont été ignorés car ils n&#39;avaient qu&#39;une identité par enregistrement XDM.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

Identity Service lie uniquement les identités lorsque des enregistrements uniques présentent plusieurs valeurs d’identité. Ce message d’erreur survient une fois pour chaque lot assimilé et affiche le nombre d’enregistrements dans lesquels une seule identité a été trouvée et n’a entraîné aucune modification du graphique d’identité.

###  Code  n&#39;est pas enregistré pour cette organisation IMS

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Cette erreur s’affiche lorsqu’un enregistrement assimilé présente une identité dont le  de  associé n’existe pas ou n’est pas accessible par votre organisation IMS.

### L&#39;importation par lot ignorée en tant qu&#39;organisation IMS n&#39;est pas configurée pour le graphique d&#39;identité privée

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

Lors de l’importation de données par lot, ce message d’erreur s’affiche lorsque votre organisation IMS n’a pas reçu les autorisations appropriées pour Identity Service. Contactez votre administrateur système pour résoudre ce problème.

### Erreur interne

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

Cette erreur s’affiche lorsqu’une exception inattendue se produit lors de l’assimilation d’un lot. Il est recommandé de  vos appels automatisés afin de relancer leurs requêtes à un intervalle de temps donné lors de la réception de cette erreur. Si le problème persiste, contactez votre administrateur système.
