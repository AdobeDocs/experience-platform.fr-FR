---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de dépannage de Adobe Experience Platform Identity Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2225'
ht-degree: 1%

---


# Guide de dépannage d’Identity Service

Ce document fournit des réponses aux questions fréquentes sur l’Adobe Experience Platform [!DNL Identity Service]ainsi qu’un guide de dépannage pour les erreurs courantes. Pour toute question ou dépannage concernant [!DNL Platform] les API en général, consultez le guide [de dépannage de l’API d’](../landing/troubleshooting.md)Adobe Experience Platform.

Les données qui identifient un client unique sont souvent fragmentées entre les divers périphériques et systèmes qu’ils utilisent pour interagir avec votre marque. [!DNL Identity Service] rassemble ces identités fragmentées, ce qui vous permet de comprendre parfaitement le comportement des clients et de proposer des expériences numériques impactées en temps réel. Pour plus d&#39;informations, consultez la présentation [du service](./home.md)d&#39;identité.

## FAQ

Vous trouverez ci-dessous une liste de réponses aux questions fréquemment posées sur [!DNL Identity Service].

## Qu&#39;est-ce que les données d&#39;identité ?

Les données d’identité sont des données qui peuvent être utilisées pour identifier une personne. Selon le contexte d’utilisation des données au sein de votre organisation, les données d’identité peuvent inclure des noms d’utilisateur, des adresses électroniques et des identifiants provenant de systèmes de gestion de la relation client. Les données d’identité ne sont pas limitées aux utilisateurs enregistrés de votre site Web ou service, car les utilisateurs anonymes peuvent également être identifiés par leur appareil ou leur identifiant de cookie.

## Quel est l&#39;avantage de définir les champs de données comme des identités ?

L’étiquetage de certains champs de données en tant qu’identités dans vos données d’enregistrement et de série chronologique vous permet de mettre en correspondance les relations d’identité dans la structure naturelle de vos données et de concilier les données de duplicata entre les canaux. See the [Identity Service overview](./home.md) for more information.

## Quelles sont les identités connues et anonymes ?

Une identité connue désigne une valeur d&#39;identité qui peut être utilisée seule ou avec d&#39;autres informations pour identifier, contacter ou localiser une personne. Les adresses électroniques, les numéros de téléphone et les identifiants CRM sont des exemples d’identités connues.

Une identité anonyme désigne une valeur d&#39;identité qui ne peut pas être utilisée seule ou avec d&#39;autres informations pour identifier, contacter ou localiser une personne (par exemple un identifiant de cookie).

## Qu&#39;est-ce qu&#39;un graphique d&#39;identité privée ?

Un graphique d&#39;identité privé est une carte privée des relations entre les identités recoupées et liées, visible uniquement pour votre entreprise.

Lorsque plusieurs identités sont incluses dans les données ingérées à partir d’un point de terminaison de diffusion en continu ou envoyées à un jeu de données activé pour [!DNL Identity Service], elles sont liées dans le graphique d’identité privée. [!DNL Identity Service] utilise ce graphique pour obtenir des identités pour un consommateur ou une entité donné, ce qui permet d’assembler des identités et de fusionner des profils.

## Comment créer plusieurs champs d&#39;identité dans un schéma XDM ?

[Les schémas de modèle de données d’expérience (XDM)](../xdm/home.md) prennent en charge plusieurs champs d’identité. Tout champ de données de type `string` dans un schéma qui implémente le Profil individuel XDM ou la classe XDM ExperienceEvent peut être étiqueté comme champ d&#39;identité. Une fois étiquetées, toutes les données contenues dans ces champs sont ajoutées à la carte d’identité du profil.

Pour savoir comment étiqueter un champ XDM en tant que champ d’identité à l’aide de l’interface utilisateur, consultez la section [](../xdm/tutorials/create-schema-ui.md) Identité du didacticiel de l’éditeur de Schémas. Si vous utilisez l&#39;API, reportez-vous à la section [descripteur](../xdm/tutorials/create-schema-api.md) d&#39;identité du didacticiel sur l&#39;API de registre de Schéma.

## Y a-t-il des contextes où certains champs ne doivent pas être étiquetés comme identités ?

Les champs d’identité doivent être réservés aux valeurs propres à chaque individu. Prenons l’exemple d’un jeu de données pour un programme de fidélité des clients. Le champ &quot;niveau de fidélité&quot; (or, argent, bronze) ne serait pas un champ d’identité utile, tandis que l’ID de fidélité, une valeur unique, le serait.

Les champs tels que les codes postaux et les adresses IP ne doivent pas être étiquetés comme des identités pour des individus, car ces valeurs peuvent s’appliquer à plusieurs personnes. Ces types de champs ne doivent être étiquetés que comme identités pour les stratégies marketing au niveau des ménages.

## Pourquoi mes champs d&#39;identité ne sont-ils pas liés comme je m&#39;y attends ?

En utilisant le [`/cluster/members` point de terminaison](./api/list-cluster-identites.md) de l&#39;API Identity Service, vous pouvez vue les identités associées pour un ou plusieurs champs d&#39;identité. Si la réponse ne renvoie pas les identités liées attendues, veillez à fournir les informations d’identité appropriées dans vos données XDM. Pour plus d&#39;informations, consultez la section relative à la [fourniture de données XDM au service](./home.md) d&#39;identité dans l&#39;aperçu du service d&#39;identité.

## Qu&#39;est-ce qu&#39;un espace de nommage d&#39;identité ?

Un espace de nommage d&#39;identité fournit le contexte de la manière dont les champs d&#39;identité se rapportent à l&#39;identité d&#39;un client. Par exemple, les champs d’identité sous l’espace de nommage &quot;E-mail&quot; doivent être conformes à un format d&#39;un email standard (name<span>@emailprovider.com), tandis que les champs utilisant l’espace de nommage &quot;Téléphone&quot; doivent être conformes à un numéro de téléphone standard (par exemple, 987-555-1234 en Amérique du Nord).

Les Espaces de nommage distinguent des valeurs d’identité similaires entre différents systèmes de gestion de la relation client. Prenons l’exemple d’un profil qui contient un identifiant de fidélité numérique associé à votre programme de récompenses de société. Un espace de nommage de &quot;Fidélité&quot; séparerait cette valeur d’un ID numérique similaire pour votre système de commerce électronique qui s’affiche également dans le même profil.

See the [identity namespace overview](./home.md) for more information.

## Comment associer une identité à un espace de nommage d&#39;identité ?

Les champs d&#39;identité doivent être associés à un espace de nommage d&#39;identité existant lors de leur création. Tout nouvel espace de nommage doit être [créé à l&#39;aide de l&#39;API](#how-do-i-create-a-custom-namespace-for-my-organization) avant de l&#39;associer aux champs d&#39;identité.

Pour obtenir des instructions détaillées sur la définition d&#39;un espace de nommage lors de la création d&#39;un descripteur d&#39;identité à l&#39;aide de l&#39;API, reportez-vous à la section relative à la [création d&#39;un descripteur](../xdm/tutorials/create-schema-ui.md) dans le guide du développeur du registre des Schémas. Pour marquer un champ de schéma comme une identité dans l’interface utilisateur, suivez les étapes du didacticiel [de l’éditeur de](../xdm/tutorials/create-schema-api.md)Schémas.

## Quels sont les espaces de nommage d&#39;identité standard fournis par l&#39;Experience Platform ?

Les espaces de nommage standard suivants sont fournis à toutes les organisations au sein de l&#39;Experience Platform :

| Nom d’affichage | ID | Code | Description |
| ------------ | --- | --- | ----------- |
| CORE | 0 | CORE | nom hérité : &quot;Adobe AudienceManager&quot; |
| ECID | 4 | ECID | alias : &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot; |
| Email | 6 | Email |  |
| E-mail (SHA256, avec un format réduit) | 11 | Emails  | espace de nommage standard pour les messages électroniques préhachés. Les valeurs fournies dans cet espace de nommage sont converties en minuscules avant le hachage avec SHA-256. |
| Téléphone | 7 | Téléphone |  |
| Windows AID | 8 | WAID |  |
| AdCloud | 411 | AdCloud | alias : Ad Cloud |
| Adobe Target | 9 | TNTID | ID de Cible |
| Identifiant de publicité Google | 20914 | GAID | GAID |
| Apple IDFA | 20915 | IDFA | ID des annonceurs |

## Où puis-je trouver la liste des espaces de nommage d&#39;identité disponibles pour mon organisation ?

A l’aide de l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)Identity Service, vous pouvez liste tous les espaces de nommage d’identité disponibles pour votre organisation en envoyant une demande GET au `/idnamespace/identities` point de terminaison. Pour plus d&#39;informations, consultez la section relative à la [liste des espaces de nommage](./api/list-namespaces.md) disponibles dans l&#39;aperçu de l&#39;API Identity Service.

## Comment créer un espace de nommage personnalisé pour mon entreprise ?

A l’aide de l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)Identity Service, vous pouvez créer un espace de nommage d’identité personnalisé pour votre organisation en envoyant une demande POST au `/idnamespace/identities` point de terminaison. Pour plus d&#39;informations, consultez la section sur la [création d&#39;un espace de nommage](./api/create-custom-namespace.md) personnalisé dans l&#39;aperçu de l&#39;API Identity Service.

## Que sont les identités composites et les XID ?

Les identités sont référencées dans les appels d’API par leur identité composite ou XID. Une identité **** composite est une représentation d&#39;une identité qui contient une valeur d&#39;ID et un espace de nommage. Un **XID** est un identifiant de valeur unique qui représente le même concept qu’une identité composite (un identifiant et un espace de nommage) et qui est automatiquement affecté à de nouvelles identités lorsqu’il est conservé par Identity Service. Pour plus d&#39;informations, consultez la présentation [de l&#39;API](./home.md) Identity Service.

## Comment le service d&#39;identité gère-t-il les informations d&#39;identification personnelle ?

Identity Service crée un hachage cryptographique à sens unique et puissant des informations d’identification personnelle avant la persistance des valeurs. Les données d’identité des espaces de nommage &quot;Téléphone&quot; et &quot;Adresse électronique&quot; sont automatiquement hachées à l’aide de SHA-256, les valeurs &quot;Courriel&quot; étant automatiquement converties en minuscules avant le hachage.

## Dois-je chiffrer toutes les informations d’identification personnelle avant de les envoyer à Platform ?

Il n’est pas nécessaire de chiffrer manuellement les données d’identification personnelle avant de les importer dans Platform. En appliquant le libellé `I1` d’utilisation des données à tous les champs de données applicables, Platform convertit automatiquement ces champs en valeurs d’ID hachées lors de l’assimilation.

Pour savoir comment appliquer et gérer des étiquettes d’utilisation des données, consultez le didacticiel [sur les étiquettes d’utilisation des](../data-governance/labels/user-guide.md)données.

## Y a-t-il des considérations à prendre en compte lors du hachage des identités basées sur les informations d&#39;identification personnelle ?

Si vous envoyez des valeurs d’identification personnelle hachées à Identity Service, vous devez utiliser la même méthode de chiffrement pour vos jeux de données. Ainsi, la même valeur d&#39;identité entre les jeux de données génère les mêmes valeurs hachées et peut être correctement mise en correspondance et liée dans le graphique d&#39;identité.

<!-- Documentation does not show any methods of editing the identityMap directly, and this table never overtly recommends using identityMap anyway. This should probably be removed unless PM thinks otherwise. -->
<!-- ## When should I use the Identity map rather than labeling individual XDM schema fields?

The following table describes when the recommended approach for including identity data in your XDM would be identity map and when an identity field is the better method.

>[!NOTE]
>
>An advantage `identityMap` has is the ability to include multiple identity values for a single namespace.

Write|XDM identity field|`identityMap`
---|---|---
UI|Supported|Supported
Developer|Recommended|Supported
ETL|Recommended|Avoid - While this is supported, data should be formatted naturally when using an ETL, favoring identity fields over `identityMap`.
Internal solutions|Preferred|Common

--- -->

## Résolution des problèmes

La section suivante fournit des suggestions de dépannage pour des codes d’erreur spécifiques et le comportement inattendu que vous pouvez rencontrer lors de l’utilisation de l’ [!DNL Identity Service] API.

## [!DNL Identity Service] messages d&#39;erreur

Voici une liste de messages d&#39;erreur que vous pouvez rencontrer lors de l&#39;utilisation de l&#39; [!DNL Identity Service] API.

### Paramètre de requête requis manquant

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Cette erreur s’affiche lorsqu’un paramètre de requête requis n’a pas été inclus dans le chemin d’accès à la requête. Le message `detail` d’erreur indique le nom du paramètre manquant. Les variantes de ce message d’erreur incluent :

- Paramètre de requête requis manquant - nsId
- Paramètre de requête requis manquant - id
- Paramètre de requête requis manquant - xid ou (nsid, id)
- Paramètre de requête requis manquant - targetNs
- Paramètre de requête requis manquant - xids ou compositeXids

Vérifiez que vous incluez correctement le paramètre indiqué dans le chemin d’accès à la requête avant de réessayer.

### L&#39;horodatage doit être compris dans les 180 derniers jours

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] purge les données datant de plus de 180 jours. Ce message d’erreur s’affiche lorsque vous tentez d’accéder à des données antérieures à cette date.

### Il existe une limite de 1 000 XID dans un seul appel.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Ce message d’erreur s’affiche lorsque vous tentez de récupérer des informations d’identité pour plus de [XID](#what-are-composite-identities-and-xids) autorisés dans un seul appel d’API. Réduisez le nombre de XID dans votre requête à un niveau inférieur à la limite affichée pour résoudre ce problème.


### Il existe une limite de 1 000 Xids composite dans un seul appel.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Ce message d’erreur s’affiche lorsque vous tentez de récupérer des informations d’identité pour plus d’identités [](#what-are-composite-identities-and-xids) composites autorisées dans un seul appel d’API. Pour résoudre ce problème, réduisez le nombre d’identités composites dans votre requête jusqu’à ce qu’il soit inférieur à la limite affichée.

### Le type de graphique spécifié n&#39;est pas valide

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Ce message d’erreur s’affiche lorsqu’un paramètre de `graph-type` requête reçoit une valeur non valide dans le chemin d’accès à la requête. Consultez la section sur les graphiques [](./home.md) d&#39;identité dans l&#39; [!DNL Identity Service] aperçu pour savoir quels types de graphiques sont pris en charge.

### Le jeton de service n&#39;a pas d&#39;étendue valide

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Ce message d’erreur s’affiche lorsque votre organisation IMS n’a pas reçu les autorisations appropriées pour [!DNL Identity Service]. Contactez votre administrateur système pour résoudre ce problème.

### Le jeton de service de passerelle n&#39;est pas valide

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

Dans le cas de cette erreur, votre jeton d&#39;accès n&#39;est pas valide. Les Jetons d&#39;accès expirent toutes les 24 heures et doivent être régénérés pour continuer à utiliser [!DNL Platform] les API. Consultez le didacticiel [sur l’](../tutorials/authentication.md) authentification pour obtenir des instructions sur la génération de nouveaux jetons d&#39;accès.

### Jeton de service d&#39;autorisation non valide

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

Dans le cas de cette erreur, votre jeton d&#39;accès n&#39;est pas valide. Les Jetons d&#39;accès expirent toutes les 24 heures et doivent être régénérés pour continuer à utiliser [!DNL Platform] les API. Consultez le didacticiel [sur l’](../tutorials/authentication.md) authentification pour obtenir des instructions sur la génération de nouveaux jetons d&#39;accès.

### Le jeton utilisateur ne dispose pas d&#39;un contexte de produit valide

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Ce message d’erreur s’affiche lorsque votre jeton d&#39;accès n’a pas été généré à partir d’une [!DNL Experience Platform] intégration. Consultez le didacticiel [sur l’](../tutorials/authentication.md) authentification pour obtenir des instructions sur la génération de nouveaux jetons d&#39;accès pour une [!DNL Experience Platform] intégration.

### Erreur interne lors de l’obtention du XID natif à partir de l’identité et du code d’espace de nommage

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Lorsque [!DNL Identity Service] persiste une identité, l’ID de l’identité et l’ID d’espace de nommage associé se voient attribuer un identifiant unique appelé XID. Ce message s’affiche lorsqu’une erreur se produit lors du processus de recherche du XID pour une valeur et un espace de nommage d’ID donnés.

### L&#39;organisation IMS n&#39;est pas configurée pour [!DNL Identity Service] une utilisation

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Ce message d’erreur s’affiche lorsque votre organisation IMS n’a pas reçu les autorisations appropriées pour [!DNL Identity Service]. Contactez votre administrateur système pour résoudre ce problème.

### Erreur du serveur interne

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Cette erreur s’affiche lorsqu’une exception inattendue se produit dans l’exécution d’un appel de [!DNL Platform] service. La meilleure pratique consiste à programme vos appels automatisés afin de relancer leurs requêtes quelques fois à un intervalle de temps donné lors de la réception de cette erreur. Si le problème persiste, contactez votre administrateur système.

## Codes d&#39;erreur d&#39;importation par lot

[!DNL Identity Service] ingère des données d&#39;identité à partir des données d&#39;enregistrement et de séries chronologiques qui sont téléchargées à l&#39; [!DNL Platform] aide de l&#39;importation par lots. L&#39;assimilation par lot étant un processus asynchrone, vous devez vue les détails d&#39;un lot à des erreurs de vue. Les erreurs s’accumulent au fur et à mesure que le lot avance jusqu’à ce que le lot soit terminé.

Voici une liste de messages d&#39;erreur relatifs à [!DNL Identity Service] votre utilisation de l&#39;API [d&#39;importation de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)données.

### schéma XDM inconnu

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] ne consomme que les identités pour les données d’enregistrement ou de série chronologique conformes aux [!DNL Profile] classes ou [!DNL ExperienceEvent] aux classes, respectivement. Toute tentative d&#39;assimilation de données pour [!DNL Identity Service] lesquelles aucune classe n&#39;adhère à l&#39;une ou l&#39;autre classe déclenchera cette erreur.

### Il y avait 0 identité valide dans les 100 premières lignes du lot traité

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Cette erreur s’affiche lorsque les 100 premières lignes d’un lot ne présentent aucune identité. Cette erreur n&#39;indique toutefois pas de façon concluante qu&#39;aucune identité n&#39;a été trouvée dans les enregistrements ultérieurs.

### Les enregistrements ont été ignorés car ils n&#39;avaient qu&#39;une identité par enregistrement XDM.

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] ne lie que les identités lorsque des enregistrements uniques présentent plusieurs valeurs d’identité. Ce message d&#39;erreur survient une fois pour chaque lot assimilé et affiche le nombre d&#39;enregistrements dans lesquels une seule identité a été trouvée et n&#39;a pas entraîné de modification du graphique d&#39;identité.

### Le code d&#39;Espace de nommage n&#39;est pas enregistré pour cette organisation IMS

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Cette erreur s&#39;affiche lorsqu&#39;un enregistrement assimilé présente une identité dont l&#39;espace de nommage associé n&#39;existe pas ou n&#39;est pas accessible par votre organisation IMS.

### Ignorer l&#39;assimilation par lot en tant qu&#39;organisation IMS n&#39;est pas prévu pour le graphique d&#39;identité privée

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

Lors de l’importation de données par lot, ce message d’erreur s’affiche lorsque votre organisation IMS n’a pas reçu les autorisations appropriées pour [!DNL Identity Service]l’importation. Contactez votre administrateur système pour résoudre ce problème.

### Erreur interne

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

Cette erreur s&#39;affiche lorsqu&#39;une exception inattendue se produit lors de l&#39;assimilation d&#39;un lot. La meilleure pratique consiste à programme vos appels automatisés afin de relancer leurs requêtes quelques fois à un intervalle de temps donné lors de la réception de cette erreur. Si le problème persiste, contactez votre administrateur système.
