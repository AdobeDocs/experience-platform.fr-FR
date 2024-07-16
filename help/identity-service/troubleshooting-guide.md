---
keywords: Experience Platform;accueil;rubriques populaires;espace de noms d’identité;Espace de noms d’identité
solution: Experience Platform
title: Guide de dépannage du service d’identités
description: Ce document fournit des réponses aux questions fréquentes sur le service d’identités d’Adobe Experience Platform, ainsi qu’un guide de dépannage pour les erreurs courantes.
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: 3fe94be9f50d64fc893b16555ab9373604b62e59
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 100%

---

# Guide de dépannage du service d’identités

Ce document fournit des réponses aux questions fréquentes sur Adobe Experience Platform [!DNL Identity Service] ainsi qu’un guide de dépannage pour les erreurs courantes. Pour toute question ou tout dépannage concernant les API de [!DNL Platform] en général, reportez-vous au [guide de dépannage des API d’Adobe Experience Platform](../landing/troubleshooting.md).

Les données qui identifient un client unique sont souvent fragmentées sur les différents appareils et systèmes qu’il utilise pour interagir avec votre marque. [!DNL Identity Service] rassemble ces identités fragmentées, ce qui permet une compréhension complète du comportement des clients afin que vous puissiez offrir des expériences digitales percutantes en temps réel. Pour plus d’informations, voir la [Présentation du service d’identités](./home.md).

## FAQ

Voici une liste de réponses aux questions fréquentes sur [!DNL Identity Service].

## Que sont les données d’identité ?

Les données d’identité sont les données pouvant être utilisées pour identifier une personne. Selon le contexte d’utilisation des données au sein de votre organisation, les données d’identité peuvent inclure des noms d’utilisateur, des adresses électroniques et des identifiants provenant de systèmes CRM. Les données d’identité ne sont pas limitées aux utilisateurs enregistrés de votre site web ou de votre service, car les utilisateurs anonymes peuvent également être identifiés par leurs identifiants d’appareil ou de cookie.

## Quel est l’avantage de l’étiquetage des champs de données comme identités ?

L’étiquetage de certains champs de données comme identités dans vos données d’enregistrement et de série temporelle vous permet de mettre en correspondance les relations d’identité dans la structure naturelle de vos données et de réconcilier les duplicatas de données entre les canaux. Pour plus d’informations, voir la [Présentation du service d’identités](./home.md).

## Que sont les identités connues et anonymes ?

Une identité connue fait référence à une valeur d’identité pouvant être utilisée seule ou avec d’autres informations pour identifier, contacter ou localiser une personne. Les adresses électroniques, les numéros de téléphone et les identifiants CRM sont des exemples d’identités connues.

Une identité anonyme fait référence à une valeur d’identité ne pouvant pas être utilisée seule ou avec d’autres informations pour identifier, contacter ou localiser une personne (un identifiant de cookie, par exemple).

## Qu’est-ce qu’un graphique d’identités privé ?

Un graphique d’identités privé est un mappage privé des relations entre les identités associées et liées, visible uniquement par votre organisation.

Lorsque plusieurs identités sont incluses dans des données assimilées à partir d’un point d’entrée de diffusion en continu ou envoyées à un jeu de données activé pour [!DNL Identity Service], elles sont liées dans le graphique d’identités privé. [!DNL Identity Service] utilise ce graphique pour rassembler les identités d’un consommateur ou d’une entité donnée, ce qui permet de combiner les identités et de fusionner les profils.

## Comment créer plusieurs champs d’identité dans un schéma XDM ?

Les schémas de [modèle de données d’expérience (XDM)](../xdm/home.md) prennent en charge plusieurs champs d’identité. Tout champ de données de type `string` dans un schéma qui implémente les classes XDM Individual Profile ou XDM ExperienceEvent peut être étiqueté comme champ d’identité. Une fois étiqueté, toutes les données contenues dans un tel champ sont ajoutées au mappage d’identité du profil.

Pour savoir comment étiqueter un champ XDM en tant que champ d’identité à l’aide de l’interface utilisateur, voir la [section Identité](../xdm/tutorials/create-schema-ui.md) du tutoriel de l’éditeur de schéma. Si vous utilisez l’API, reportez-vous à la [section Descripteur d’identité](../xdm/tutorials/create-schema-api.md) du tutoriel sur l’API Schema Registry.

## Dans quels cas un champ ne doit-il pas être étiqueté comme champ d’identité ?

Les champs d’identité doivent être réservés aux valeurs propres à chaque individu. Prenons l’exemple d’un jeu de données pour un programme de fidélisation des clients. Le champ « niveau de fidélité » (or, argent, bronze) n’est pas un champ d’identité utile, contrairement à l’identifiant de fidélité, qui est une valeur unique.

Les champs tels que les codes postaux et les adresses IP ne doivent pas être étiquetés comme champs d’identité pour les individus, car ces valeurs peuvent s’appliquer à plusieurs personnes. Ces types de champs doivent être étiquetés comme champs d’identité uniquement pour les stratégies marketing au niveau des foyers.

## Pourquoi mes champs d’identité ne sont-ils pas liés comme je m’y attendais ?

À l’aide du [`/cluster/members`point d’entrée](./api/list-cluster-identites.md) de l’API Service d’identités, vous pouvez afficher les identités associées pour un ou plusieurs champs d’identité. Si la réponse ne renvoie pas les identités liées attendues, veillez à fournir les informations d’identité appropriées dans vos données XDM. Pour plus d’informations, voir la section relative à la [provision de données XDM au service d’identités](./home.md) dans la présentation du service d’identités.

## Qu’est-ce qu’un espace de noms d’identité ?

Un espace de noms d’identité fournit un contexte pour la manière dont les champs d’identité sont associés à l’identité d’un client. Par exemple, les champs d’identité sous l’espace de noms « E-mail » doivent être conformes à un format standard (nom<span>@fournisseurdemessagerie.com), tandis que les champs sous l’espace de noms « Téléphone » doivent être conformes à un format standard de numéro de téléphone (par exemple, 987-555-1234 en Amérique du Nord).

Les espaces de noms différencient les valeurs d’identité similaires entre différents systèmes CRM. Prenons l’exemple d’un profil qui contient un identifiant de fidélité numérique associé au programme de récompenses de votre entreprise. Un espace de noms de « Fidélité » séparerait cette valeur d’un identifiant numérique similaire pour votre système d’e-commerce, qui apparaît dans le même profil.

Pour plus d’informations, voir [Présentation des espaces de noms d’identité](./home.md).

## Comment associer une identité à un espace de noms d’identité ?

Les champs d’identité doivent être associés à un espace de noms d’identité existants lorsqu’ils sont créés. Tout nouvel espace de noms doit être [créé à l’aide de l’API](#how-do-i-create-a-custom-namespace-for-my-organization) avant d’être associé à des champs d’identité.

Pour obtenir des instructions détaillées sur la définition d’un espace de noms lors de la création d’un descripteur d’identité à l’aide de l’API, reportez-vous à la section relative à la [création d’un descripteur](../xdm/tutorials/create-schema-ui.md) dans le guide de développement du registre des schémas. Pour marquer un champ de schéma comme identité dans l’interface utilisateur, suivez les étapes du [tutoriel de l’éditeur de schéma](../xdm/tutorials/create-schema-api.md).

## Quels sont les espaces de noms d’identité standards fournis par Experience Platform ? {#standard-namespaces}

Les espaces de noms d’identité standard sont des espaces de noms disponibles pour toutes les organisations. Pour obtenir une liste des espaces de noms standard disponibles, consultez la [présentation des espaces de noms d’identité](./features/namespaces.md).

## Où trouver la liste des espaces de noms d’identité disponibles pour mon organisation ?

À l’aide de l’[API Service d’identités](https://www.adobe.io/experience-platform-apis/references/identity-service), vous pouvez répertorier tous les espaces de noms d’identité disponibles pour votre organisation en envoyant une requête GET au point d’entrée `/idnamespace/identities`. Pour plus d’informations, reportez-vous à la section relative à la [liste des espaces de noms disponibles](./api/list-namespaces.md) dans la présentation de l’API Service d’identités.

## Comment créer un espace de noms personnalisé pour mon organisation ?

À l’aide de l’[API Service d’identités](https://www.adobe.io/experience-platform-apis/references/identity-service), vous pouvez créer un espace de noms d’identité personnalisé pour votre organisation en envoyant une requête POST au point d’entrée `/idnamespace/identities`. Pour plus d’informations, reportez-vous à la section relative à la [création d’un espace de noms personnalisé](./api/create-custom-namespace.md) dans la présentation de l’API Service d’identités.

## Que sont les identités composites et les XID ?

Les identités sont référencées dans les appels API par leur identité composite ou XID. Une identité composite est une représentation d’une identité qui contient une valeur d’identifiant et un espace de noms. Un XID est un identifiant à une seule valeur qui représente le même concept qu’une identité composite (un identifiant et un espace de noms) et qui est automatiquement affecté à de nouvelles identités lorsqu’il est conservé par le service d’identités. Pour plus d’informations, voir la [présentation de l’API Service d’identités](./home.md).

## Comment le service d’identités gère-t-il les données personnelles identifiables (PII) ?

Le service d’identités dispose d’espaces de noms standard pour prendre en charge l’ingestion de valeurs d’identité hachées pour les numéros de téléphone et les e-mails. Cependant, vous êtes vous-même responsable du hachage des valeurs. Pour en savoir plus sur le hachage de données ingérées dans Platform, consultez le [[!DNL Data Prep] guide des fonctions de mappage](../data-prep/functions.md#hashing).

## Y a-t-il des considérations à prendre en compte lors du hachage des identités basées sur les données personnelles identifiables ?

Lorsque vous envoyez des données personnelles identifiables hachées au service d’identités, vous devez utiliser la même méthode de chiffrement pour vos jeux de données. Cela permet de s’assurer qu’une valeur d’identité commune à plusieurs jeux de données génère les mêmes valeurs hachées, et que ces valeurs sont en mesure d’être correctement mises en correspondance et liées dans le graphique d’identités.

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

## Pourquoi ne puis-je pas accéder à la page de graphique d’identité ou aux API ?

Votre administrateur Platform doit vous fournir l’autorisation `view-identity-graph` pour que vous puissiez afficher les données du graphique d’identité. Sans cette autorisation, vous recevrez un message de refus d’autorisation sur la page de la visionneuse de graphiques d’identité et lors de l’appel aux API Platform. Pour plus d’informations sur les autorisations, consultez la [présentation du contrôle d’accès](../access-control/home.md).

## Dépannage

La section suivante fournit des suggestions en matière de dépannage pour les codes d’erreur spécifiques et les comportements inattendus que vous pouvez rencontrer lors de l’utilisation de l’API [!DNL Identity Service].

## Messages d’erreur [!DNL Identity Service]

Voici une liste des messages d’erreur que vous pouvez rencontrer lors de l’utilisation de l’API [!DNL Identity Service].

### Paramètre de requête obligatoire manquant

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Cette erreur s’affiche lorsqu’un paramètre de requête obligatoire n’a pas été inclus dans le chemin de requête. La valeur `detail` du message d’erreur indique le nom du paramètre manquant. Les variantes de ce message d’erreur sont :

- Paramètre de requête obligatoire manquant : nsId
- Paramètre de requête obligatoire manquant : id
- Paramètre de requête obligatoire manquant : xid ou (nsid,id)
- Paramètre de requête obligatoire manquant : targetNs
- Paramètre de requête obligatoire manquant : xids ou compositeXids

Vérifiez que le paramètre indiqué a bien été inclus dans le chemin de requête avant de réessayer.

### La date et l’heure doivent remonter à moins de 180 jours

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] purge les données datant de plus de 180 jours. Ce message d’erreur s’affiche lorsque vous tentez d’accéder à des données antérieures à cette date.

### Il existe une limite de 1 000 XID pour un seul appel

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Ce message d’erreur s’affiche lorsque vous tentez de récupérer des informations d’identité pour un nombre de [XID](#what-are-composite-identities-and-xids) supérieur au nombre maximal autorisé pour un seul appel API. Réduisez le nombre de XID dans votre requête à une valeur inférieure à la limite affichée pour résoudre ce problème.


### Il existe une limite de 1 000 compositeXid pour un seul appel

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Ce message d’erreur s’affiche lorsque vous tentez de récupérer des informations d’identité pour un nombre d’[identités composites](#what-are-composite-identities-and-xids) supérieur au nombre maximal autorisé pour un seul appel API. Réduisez le nombre d’identités composites dans votre requête à une valeur inférieure à la limite affichée pour résoudre ce problème.

### Le type de graphique spécifié n’est pas valide

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Ce message d’erreur s’affiche lorsqu’une valeur non valide est attribuée à un paramètre de requête `graph-type` dans le chemin de requête. Pour connaître les types de graphiques pris en charge, reportez-vous à la section relative aux [graphiques d’identité](./home.md) dans la présentation [!DNL Identity Service].

### Le jeton de service ne possède pas d’étendue valide

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Ce message d’erreur s’affiche lorsque votre organisation n’a pas reçu les autorisations appropriées pour [!DNL Identity Service]. Contactez votre administrateur système pour résoudre ce problème.

### Jeton de service de passerelle non valide

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

Cette erreur indique que votre jeton d’accès n’est pas valide. Les jetons d’accès expirent toutes les 24 heures et doivent être régénérés pour continuer à utiliser les API de [!DNL Platform]. Pour obtenir des instructions sur la génération de jetons d’accès, consultez le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr).

### Jeton de service d’autorisation non valide

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

Cette erreur indique que votre jeton d’accès n’est pas valide. Les jetons d’accès expirent toutes les 24 heures et doivent être régénérés pour continuer à utiliser les API de [!DNL Platform]. Pour obtenir des instructions sur la génération de jetons d’accès, consultez le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr).

### Le jeton utilisateur n’a pas de contexte de produit valide

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Ce message d’erreur s’affiche lorsque votre jeton d’accès n’a pas été généré à partir d’une intégration [!DNL Experience Platform]. Pour obtenir des instructions sur la génération de nouveaux jetons d’accès pour une intégration [!DNL Experience Platform], consultez le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr).

### Erreur interne lors de l’obtention du XID natif à partir d’un code d’identité et d’espace de noms

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Lorsque [!DNL Identity Service] conserve une identité, un identifiant unique appelé XID est attribué à l’identifiant de l’identité et l’identifiant de l’espace de noms qui lui est associé. Ce message s’affiche lorsqu’une erreur se produit lors du processus de recherche de l’XID pour une valeur d’identifiant et un espace de noms donnés.

### L’organisation IMS n’a pas été mise en service pour l’utilisation de [!DNL Identity Service].

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Ce message d’erreur s’affiche lorsque votre organisation n’a pas reçu les autorisations appropriées pour [!DNL Identity Service]. Contactez votre administrateur système pour résoudre ce problème.

### Erreur interne du serveur

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Cette erreur s’affiche quand une exception inattendue se produit lors de l’exécution d’un appel du service [!DNL Platform]. La bonne pratique consiste à programmer vos appels automatisés afin de relancer leurs requêtes à un intervalle de temps donné lors de la réception de cette erreur. Si le problème persiste, contactez votre administrateur système.

## Codes d’erreur d’ingestion par lots

[!DNL Identity Service] ingère des données d’identité à partir des données d’enregistrement et de série temporelle téléchargées dans [!DNL Platform] à l’aide de la fonction d’ingestion par lots. L’ingestion par lots est un processus asynchrone, vous devez afficher les détails d’un lot pour voir les erreurs. Les erreurs s’accumulent au fur et à mesure que le lot avance, jusqu’à ce que le traitement du lot soit terminé.

Voici une liste des messages d’erreur dans [!DNL Identity Service], que vous pouvez rencontrer lors de l’utilisation de l’[API d’ingestion par lots](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).

### Schéma XDM inconnu

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] utilise uniquement des identités pour les données d’enregistrement ou de série temporelle qui sont conformes aux classes [!DNL Profile] ou [!DNL ExperienceEvent], respectivement. Toute tentative d’ingestion de données pour [!DNL Identity Service] qui n’adhère à aucune des classes déclenche cette erreur.

### Aucune identité valide dans les 100 premières lignes du lot traité

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Cette erreur s’affiche lorsque les 100 premières lignes d’un lot ne présentent aucune identité. Cette erreur n’indique toutefois pas de manière concluante qu’aucune identité n’a été trouvée dans les enregistrements ultérieurs.

### Les enregistrements ont été ignorés, car il n’y avait qu’une seule identité par enregistrement XDM

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] lie uniquement les identités lorsque des enregistrements uniques présentent plusieurs valeurs d’identité. Ce message d’erreur survient une fois pour chaque lot ingéré et affiche le nombre d’enregistrements dans lesquels une seule identité a été trouvée et n’a entraîné aucune modification du graphique d’identités.

### Aucun code d’espace de noms enregistré pour cette organisation IMS

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Cette erreur s’affiche lorsqu’un enregistrement ingéré présente une identité dont l’espace de noms associé n’existe pas ou n’est pas accessible pour votre organisation.

### L’ingestion par lots est ignorée en tant que l’organisation IMS n’est pas configurée pour le graphique d’identité privé

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

Lors de l’ingestion de données par lots, ce message d’erreur s’affiche lorsque votre organisation n’a pas reçu les autorisations appropriées pour [!DNL Identity Service]. Contactez votre administrateur système pour résoudre ce problème.

### Erreur interne

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

Cette erreur s’affiche lorsqu’une exception inattendue se produit lors de l’ingestion d’un lot. La bonne pratique consiste à programmer vos appels automatisés afin de relancer leurs requêtes à un intervalle de temps donné lors de la réception de cette erreur. Si le problème persiste, contactez votre administrateur système.
