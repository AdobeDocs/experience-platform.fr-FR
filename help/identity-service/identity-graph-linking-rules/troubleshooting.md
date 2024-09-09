---
title: Guide de dépannage des règles de liaison de graphique d’identités
description: Découvrez comment résoudre les problèmes courants des règles de liaison de graphiques d’identités.
badge: Version bêta
exl-id: 98377387-93a8-4460-aaa6-1085d511cacc
source-git-commit: 56e2e359812fcbfd011505ad917403d6f5317b4a
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 0%

---

# Guide de dépannage des règles de liaison de graphiques d’identités

>[!AVAILABILITY]
>
>La fonctionnalité des règles de liaison de graphique d’identités est actuellement en version bêta. Contactez votre équipe de compte d’Adobe pour plus d’informations sur les critères de participation. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

Lorsque vous testez et validez des règles de liaison de graphiques d’identités, vous pouvez rencontrer des problèmes liés à l’ingestion de données et au comportement des graphiques. Lisez ce document pour savoir comment résoudre certains problèmes courants que vous pouvez rencontrer lors de l’utilisation de règles de liaison de graphiques d’identités.

## Flux d’ingestion de données - Aperçu {#data-ingestion-flow-overview}

Le diagramme suivant est une représentation simplifiée de la manière dont les données sont transférées dans Adobe Experience Platform et les applications. Utilisez ce diagramme comme référence pour mieux comprendre le contenu de cette page.

![Schéma du flux de l’ingestion des données dans Identity Service.](../images/troubleshooting/dataflow_in_identity.png)

Il est important de noter les facteurs suivants :

* Pour les données en flux continu, Real-Time Customer Profile, Identity Service et le lac de données commenceront à traiter les données lors de l’envoi des données. Toutefois, la latence pour terminer le traitement des données dépend du service. En règle générale, le traitement du lac de données prend plus de temps que dans Profile et Identity Service.
   * Si les données n’apparaissent pas lors de l’exécution d’une requête sur un jeu de données, même au bout de quelques heures, il est probable que les données n’aient pas été ingérées dans Experience Platform.
* Pour les données par lots, toutes les données seront d’abord transmises au lac de données, puis les données seront propagées à Profile et à Identity Service si le jeu de données est activé pour Profile et Identity Service.
* Pour les problèmes liés à l’ingestion, il est important que le problème soit isolé au niveau du service pour un débogage et un dépannage précis. Il existe trois types de problèmes potentiels à prendre en compte :

| Type de problème d’ingestion | Les données sont-elles ingérées dans un lac de données ? | Les données sont-elles ingérées dans Profile ? | Les données sont-elles ingérées dans Identity Service ? |
| --- | --- | --- | --- |
| Problème d’ingestion général | Non | Non | Non |
| Problème graphique | Oui | Oui | Non |
| Problème de fragment de profil | Oui | Non | Oui |

## Problèmes d’ingestion des données {#data-ingestion-issues}

>[!NOTE]
>
>* Cette section suppose que les données ont été correctement ingérées dans le lac de données et qu’il n’y a eu aucune syntaxe ni aucune autre erreur qui empêcherait d’abord l’ingestion des données dans Experience Platform.
>
>* Les exemples utilisent ECID comme espace de noms du cookie et CRMID comme espace de noms de la personne.

### Mes identités ne sont pas ingérées dans Identity Service{#my-identities-are-not-getting-ingested-into-identity-service}

Plusieurs raisons peuvent expliquer cette situation, notamment, mais sans s’y limiter, les suivantes :

* [Le jeu de données n’est pas activé pour Profile](../../catalog/datasets/enable-for-profile.md).
* L’enregistrement est ignoré car il n’y a qu’une seule identité dans l’événement.
* [Un échec de validation s’est produit dans Identity Service](../guardrails.md#identity-value-validation).
   * Par exemple, un ECID peut avoir dépassé la longueur maximale de 38 caractères.
* Par défaut, les [AAID sont bloqués de l&#39;ingestion](../guardrails.md#identity-namespace-ingestion).
* L’identité est supprimée en raison des [barrières de sécurité système](../guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated).

Dans le contexte des règles de liaison de graphiques d’identités, un enregistrement peut être rejeté d’Identity Service, car l’événement entrant comporte au moins deux identités avec le même espace de noms unique, mais une valeur d’identité différente. Ce scénario se produit généralement en raison d’erreurs de mise en oeuvre.

Tenez compte de l’événement suivant avec deux hypothèses :

* Le nom du champ CRMID est marqué comme identité avec l’espace de noms CRMID.
* L’espace de noms CRMID est défini comme un espace de noms unique.

L’événement suivant renvoie un message d’erreur indiquant que l’ingestion a échoué.

<!-- because the ingestion of this erroneous event would have resulted in graph collapse. In the following event, two entities (Alice and Bob) are both associated with the same namespace (CRMID). -->

```json
{ 
  "_id": "random_string", 
  "eventType": "web browsing event", 
  "identityMap": { 
    "ECID": [ 
      { 
        "id": "11111111111111111111111111111111111111", 
        "primary": false 
      } 
    ], 
    "CRMID": [ 
      { 
        "id": "Alice", 
        "primary": true 
      } 
    ] 
  }, 
  "CRMID": "Bob", 
  "timestamp": "2024-08-17T15:22:51+00:00", 
  "web": { 
    "webPageDetails": { 
      "URL": "https://www.adobe.com/acrobat.html", 
      "name": "Adobe Acrobat" 
    } 
  } 
} 
```

**Étapes de dépannage**

Pour résoudre cette erreur, vous devez d&#39;abord collecter les informations suivantes :

* La valeur d’identité (`identity_value`) que vous prévoyez d’ingérer dans le graphique d’identités.
* Jeu de données (`dataset_name`) dans lequel l’événement a été envoyé.

Ensuite, utilisez [Adobe Experience Platform Query Service](../../query-service/home.md) et exécutez la requête suivante :

>[!TIP]
>
>Remplacez `dataset_name` et `identity_value` par les informations que vous avez collectées.

```sql
  SELECT key, col.id as identityValue, timestamp, _id, identityMap, * 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id = 'identity_value' 
```

Après avoir exécuté votre requête, recherchez l’enregistrement d’événement que vous attendiez de générer un graphique, puis validez que les valeurs d’identité sont différentes dans la même ligne. Affichez l’image suivante pour un exemple :

![Requête sans titre qui générait des espaces de noms en double.](../images/troubleshooting/duplicated_unique_namespace.png)

>[!NOTE]
>
>Si les deux identités sont exactement les mêmes et si l’événement est ingéré par flux, Identity et Profile dédupliquent l’identité.

### Mes fragments d’événement d’expérience ne sont pas ingérés dans Profile {#my-experience-event-fragments-are-not-getting-ingested-into-profile}

Plusieurs raisons expliquent pourquoi les fragments d’événement d’expérience ne sont pas ingérés dans Profile, notamment :

* [Le jeu de données n’est pas activé pour Profile](../../catalog/datasets/enable-for-profile.md).
* [Un échec de validation peut s’être produit sur Profile](../../xdm/classes/experienceevent.md).
   * Par exemple, un événement d’expérience doit contenir à la fois un `_id` et un `timestamp`.
   * De plus, le `_id` doit être unique pour chaque événement (enregistrement).

Dans le contexte de la priorité d’espace de noms, Profile rejettera tout événement contenant deux identités ou plus avec la priorité d’espace de noms la plus élevée. Par exemple, si GAID n’est pas marqué comme un espace de noms unique et que deux identités avec un espace de noms GAID et des valeurs d’identité différentes sont entrées, Profile ne stockera aucun des événements.

**Étapes de dépannage**

Pour résoudre cette erreur, lisez les étapes de dépannage décrites dans le guide ci-dessus sur les [erreurs de dépannage concernant les données non ingérées dans Identity Service](#my-identities-are-not-getting-ingested-into-identity-service).

### Mes fragments d’événement d’expérience sont ingérés, mais leur identité principale est &quot;incorrecte&quot; dans Profile.

La priorité d’espace de noms joue un rôle important dans la manière dont les fragments d’événement déterminent l’identité principale.

* Une fois que vous avez configuré et enregistré vos [paramètres d’identité](./identity-settings-ui.md) pour un environnement de test donné, Profile utilisera alors la [priorité d’espace de noms](namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events) pour déterminer l’identité principale. Dans le cas d’identityMap, Profile n’utilisera plus l’indicateur `primary=true`.
* Bien que Profile ne fasse plus référence à cet indicateur, d’autres services sur Experience Platform peuvent continuer à utiliser l’indicateur `primary=true`.

Pour que les [événements d’utilisateur authentifiés](configuration.md#ingest-your-data) soient liés à l’espace de noms de la personne, tous les événements authentifiés doivent contenir l’espace de noms de la personne (CRMID). Cela signifie que même après la connexion d’un utilisateur, l’espace de noms de la personne doit toujours être présent sur chaque événement authentifié.

Vous pouvez continuer à voir l’indicateur &quot;events&quot; `primary=true` lors de la recherche d’un profil dans la visionneuse de profils. Cependant, cette opération est ignorée et ne sera pas utilisée par Profile.

Les AAID sont bloqués par défaut. Par conséquent, si vous utilisez le [connecteur source Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md), vous devez vous assurer que l’ECID a une priorité supérieure à l’ECID afin que les événements non authentifiés aient une identité principale d’ECID.

**Étapes de dépannage**

* Pour vérifier que les événements authentifiés contiennent à la fois l’espace de noms de personne et de cookie, lisez les étapes décrites dans la section [ sur la résolution des erreurs de dépannage concernant les données non ingérées dans Identity Service](#my-identities-are-not-getting-ingested-into-identity-service).
* Pour vérifier que les événements authentifiés possèdent l’identité principale de l’espace de noms de la personne (CRMID, par exemple), recherchez l’espace de noms de la personne dans la visionneuse de profils à l’aide de la stratégie de fusion sans regroupement (il s’agit de la stratégie de fusion qui n’utilise pas de graphique privé). Cette recherche renvoie uniquement les événements associés à l’espace de noms de la personne.

## Problèmes liés au comportement du graphique {#graph-behavior-related-issues}

Cette section décrit les problèmes courants que vous pouvez rencontrer concernant le comportement du graphique d’identités.

### L&#39;identité est liée à la &quot;mauvaise&quot; personne

L’algorithme d’optimisation des identités honorera [les liens les plus récemment établis et supprimera les liens les plus anciens](./identity-optimization-algorithm.md#identity-optimization-algorithm-details). Par conséquent, il est possible qu’une fois cette fonctionnalité activée, les ECID puissent être réaffectés (réliés) d’une personne à une autre. Pour comprendre l’historique des liens entre une identité au fil du temps, procédez comme suit :

**Étapes de dépannage**

>[!NOTE]
>
>Les étapes suivantes permettent de récupérer des informations sous les hypothèses suivantes :
>
>* Un seul jeu de données est en cours d’utilisation (il ne présentera pas de requête pour plusieurs jeux de données).
>
>* Les données ne sont pas supprimées du lac de données en raison d’une suppression effectuée par [Advanced Data Lifecycle Management](../../hygiene/home.md), [Privacy Service](../../privacy-service/home.md) ou d’autres services effectuant la suppression.

Tout d’abord, vous devez collecter les informations suivantes :

* Le symbole d’identité (namespaceCode) de l’espace de noms du cookie (par exemple, ECID) et l’espace de noms de la personne (par exemple, CRMID) qui ont été envoyés.
   * Pour les implémentations du SDK Web, il s’agit généralement des espaces de noms inclus dans identityMap.
   * Pour les mises en oeuvre du connecteur source Analytics, il s’agit de l’identifiant de cookie inclus dans identityMap. L’identifiant de personne est un champ d’eVar marqué comme identité.
* Jeu de données dans lequel l’événement a été envoyé (nom_jeu_de_données).
* La valeur d’identité de l’espace de noms du cookie à rechercher (identity_value).

Les symboles d’identité (namespaceCode) sont sensibles à la casse. Pour récupérer tous les symboles d’identité d’un jeu de données donné dans identityMap, exécutez la requête suivante :

```sql
SELECT distinct explode(*)FROM (SELECT map_keys(identityMap) FROM dataset_name)
```

Si vous ne connaissez pas la valeur d’identité de votre identifiant de cookie et que vous souhaitez rechercher un identifiant de cookie qui aurait été lié à plusieurs identifiants de personne, vous devez exécuter la requête suivante. Cette requête considère ECID comme l’espace de noms du cookie et CRMID comme l’espace de noms de la personne.

>[!BEGINTABS]

>[!TAB Implémentation du SDK Web]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct identityMap['CRMID'][0]['id']) as crmidCount FROM dataset_name GROUP BY identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

>[!TAB Implémentation du connecteur source Analytics]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct personID) as crmidCount FROM dataset_name group by identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

**Remarque :** personID fait référence au chemin d’accès du descripteur. Vous trouverez ces informations sous les schémas.

>[!ENDTABS]

Examinez ensuite l’association de l’espace de noms du cookie par ordre d’horodatage en exécutant la requête suivante :

>[!BEGINTABS]

>[!TAB Implémentation du SDK Web]

```sql
  SELECT identityMap['CRMID'][0]['id'] as personEntity, * 
  FROM dataset_name 
  WHERE identitymap['ECID'][0].id ='identity_value' 
  ORDER BY timestamp desc 
```

>[!TAB Implémentation du connecteur source Analytics]

```sql
SELECT _experience.analytics.customDimensions.eVars.eVar10 as personEntity, * 
FROM dataset_name 
WHERE identitymap['ECID'][0].id ='identity_value' 
ORDER BY timestamp desc 
```

**Remarque** : cet exemple suppose que `eVar10` est marqué comme identité. Pour vos configurations, vous devez modifier l’eVar en fonction de l’implémentation de votre propre organisation.

>[!ENDTABS]

### L’algorithme d’optimisation des identités ne fonctionne pas comme prévu.

**Étapes de dépannage**

Reportez-vous à la documentation sur l’ [algorithme d’optimisation des identités](./identity-optimization-algorithm.md), ainsi que les types de structures graphiques pris en charge.

* Lisez le [guide de configuration graphique](./example-configurations.md) pour obtenir des exemples de structures graphiques prises en charge.
* Vous pouvez également lire le [guide de mise en oeuvre](./configuration.md#appendix) pour obtenir des exemples de structures graphiques non prises en charge. Deux scénarios peuvent se produire :
   * Aucun espace de noms unique sur tous vos profils.
   * Un scénario [&quot;dangling ID&quot;](./configuration.md#dangling-loginid-scenario) se produit. Dans ce scénario, Identity Service ne peut pas déterminer si l’ID de pendaison est associé à l’une des entités de personne dans les graphiques.

Vous pouvez également utiliser l’[outil de simulation graphique de l’interface utilisateur](./graph-simulation.md) pour simuler des événements et configurer vos propres paramètres de priorité d’espace de noms et d’espace de noms uniques. Cela peut vous aider à comprendre de base le comportement de l’algorithme d’optimisation des identités.

Si les résultats de la simulation correspondent aux attentes de comportement du graphique, vous pouvez vérifier si vos [paramètres d’identité](./identity-settings-ui.md) correspondent aux paramètres que vous avez configurés dans votre simulation.

### Je vois toujours des graphiques réduits dans mon environnement de test même après la configuration des paramètres d’identité.

Les graphiques d’identités se conforment à la priorité d’espace de noms et d’espace de noms uniques que vous avez configurée _après l’enregistrement des paramètres._ Les graphiques &quot;réduits&quot; qui existent _avant_ l’enregistrement de vos nouveaux paramètres ne seront pas affectés tant que de nouvelles données n’auront pas été ingérées afin que le graphique réduit soit mis à jour. L’identité principale des fragments d’événement sur Real-time Customer Profile ne sera pas mise à jour même après les modifications de la priorité de l’espace de noms.

**Étapes de dépannage**

Vous pouvez utiliser la [visionneuse de graphiques d’identités](../features/identity-graph-viewer.md) pour vérifier si votre graphique a été ingéré avant ou après vos paramètres. Examinez la dernière date et heure mises à jour sous [!UICONTROL Propriétés du lien] pour savoir quand Identity Service a ingéré le graphique. Si l’horodatage est antérieur à la configuration, cela suggère que le graphique &quot;réduit&quot; a été créé avant d’activer la fonction.

![ La visionneuse de graphiques d’identités avec un exemple de graphique.](../images/troubleshooting/graph_viewer.png)

### Je veux savoir combien de graphiques &quot;réduits&quot; existent dans mon environnement de test.

Utilisez le tableau de bord des identités pour obtenir des informations sur l’état de votre graphique d’identités, telles que le nombre d’identités et de graphiques. Reportez-vous à la mesure &quot;Nombre de graphiques avec plusieurs espaces de noms&quot; pour le nombre de graphiques qui se sont réduits : il s’agit de graphiques qui contiennent deux identités ou plus avec le même espace de noms. En supposant que l’environnement de test ne comporte aucune donnée et que vous ayez configuré un espace de noms (CRMID, par exemple) pour qu’il soit unique, vous vous attendez à ce qu’aucun graphique ne comporte deux ou plusieurs CRMID. Dans l’exemple ci-dessous, deux graphiques contiennent au moins deux adresses électroniques.

![ Le tableau de bord des identités avec des mesures sur le nombre d’identités, le nombre de graphiques, le nombre par espace de noms, le nombre de graphiques par taille et le nombre de graphiques de plus de deux espaces de noms.](../images/troubleshooting/identity_dashboard.png)

Vous trouverez une ventilation détaillée dans le [jeu de données d’exportation instantané de profil](../../dashboards/query.md) dans le lac de données en exécutant la requête ci-dessous :

>[!NOTE]
>
>* Remplacez `dataset_name` par le nom réel de votre jeu de données.
>
>* Les chiffres peuvent ne pas correspondre exactement. Le tableau de bord des identités est basé sur le nombre de graphiques d’identités et la requête suivante est basée sur le nombre de profils avec deux identités ou plus. Les données sont traitées et mises à jour indépendamment par le service.

```sql
  SELECT key, identityCountInGraph, count(identityCountInGraph) as graphCount 
  FROM (SELECT key, cardinality(value) as identityCountInGraph 
  FROM (SELECT explode(identityMap) 
  FROM dataset_name 
  WHERE cardinality(identityMap) > 1)) /* by definition, graphs have 2 or more identities */ 
  WHERE key not in ('ecid', 'aaid', 'idfa', 'gaid') /* filter out common device/cookie namespaces */ 
  GROUP BY 1, 2 
  ORDER BY 1, 2 asc 
```

Vous pouvez utiliser la requête suivante dans le jeu de données d’exportation d’instantanés de profil pour obtenir des exemples d’identités à partir de graphiques &quot;réduits&quot;.

```sql
  SELECT identityMap 
  FROM dataset_name 
  WHERE cardinality(identityMap['CRMID'])>1 /* any graphs with 2+ CRMID. Change CRMID namespace if needed */ 
```

>[!TIP]
>
>Les deux requêtes répertoriées ci-dessus produiront des résultats attendus si l’environnement de test n’est pas activé pour l’approche intermédiaire de l’appareil partagé et se comporte différemment des règles de liaison de graphique d’identités.
