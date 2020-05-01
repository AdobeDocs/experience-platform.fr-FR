---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Traitement des demandes de confidentialité dans Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: d3584202554baf46aad174d671084751e6557bbc

---


# Traitement des demandes de confidentialité dans Data Lake

Le service de confidentialité d’Adobe Experience Platform traite les demandes d’accès, de opt-out de vente ou de suppression de leurs données personnelles, conformément aux règles de confidentialité légales et organisationnelles.

Ce document couvre les concepts essentiels liés au traitement des demandes de protection des renseignements personnels pour les données des clients stockées dans le lac Data.

## Prise en main

Avant de lire ce guide, il est recommandé de bien comprendre les services Experience Platform suivants :

* [Privacy Service](../privacy-service/home.md): Gère les demandes des clients pour accéder aux applications Adobe Experience Cloud, les exclure de la vente ou les supprimer.
* [Service](home.md)de catalogue : Système d’enregistrement pour l’emplacement et le lignage des données dans la plateforme d’expérience. Fournit une API qui peut être utilisée pour mettre à jour les métadonnées du jeu de données.
* [Système](../xdm/home.md)de modèle de données d’expérience (XDM) : Cadre normalisé selon lequel la plate-forme d’expérience organise les données d’expérience client.
* [Service](../identity-service/home.md)d&#39;identité : Résout le défi fondamental posé par la fragmentation des données d’expérience client en rapprochant les identités entre les périphériques et les systèmes.

## Comprendre les espaces de nommage d&#39;identité {#namespaces}

Adobe Experience Platform Identity Service relie les données d’identité des clients entre les systèmes et les périphériques. Identity Service utilise des espaces de nommage **** d&#39;identité pour fournir un contexte aux valeurs d&#39;identité en les rattachant à leur système d&#39;origine. Un espace de nommage peut représenter un concept générique tel qu’une adresse électronique (&quot;Adresse électronique&quot;) ou associer l’identité à une application spécifique, telle qu’un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou un Adobe Cible ID (&quot;TNTID&quot;).

Identity Service conserve un stock d&#39;espaces de nommage d&#39;identité définis globalement (standard) et définis par l&#39;utilisateur (personnalisés). Les espaces de nommage standard sont disponibles pour toutes les organisations (par exemple, &quot;Courriel&quot; et &quot;ECID&quot;), tandis que votre organisation peut également créer des espaces de nommage personnalisés en fonction de ses besoins particuliers.

Pour plus d’informations sur les espaces de nommage d’identité dans la plate-forme d’expérience, voir la présentation [de l’espace de nommage](../identity-service/namespaces.md)d’identité.

## Ajout de données d&#39;identité aux jeux de données

Lors de la création de demandes de confidentialité pour Data Lake, des valeurs d&#39;identité valides (et leurs espaces de nommage associés) doivent être fournies pour chaque client afin de localiser ses données et de les traiter en conséquence. Par conséquent, tous les jeux de données qui font l’objet de demandes de confidentialité doivent contenir un descripteur **d’** identité dans leur schéma XDM associé.

>[!NOTE] Les jeux de données basés sur des schémas qui ne prennent pas en charge les métadonnées des descripteurs d’identité (tels que les jeux de données ad hoc) ne peuvent pas actuellement être traités dans les demandes de confidentialité.

Cette section décrit les étapes à suivre pour ajouter un descripteur d&#39;identité au schéma XDM d&#39;un jeu de données existant. Si vous disposez déjà d’un jeu de données avec un descripteur d’identité, vous pouvez passer à la section [](#nested-maps)suivante.

>[!IMPORTANT] Lorsque vous décidez des champs de schéma à définir en tant qu’identités, gardez à l’esprit les [limites de l’utilisation de champs](#nested-maps)de type mappage imbriqués.

Il existe deux méthodes pour ajouter un descripteur d&#39;identité à un schéma de jeux de données :

* [Utilisation de l’interface utilisateur](#identity-ui)
* [Utilisation de l’API](#identity-api)

### Utilisation de l’interface utilisateur {#identity-ui}

Dans l’interface utilisateur de la plateforme d’expérience, l’ _[!UICONTROL Schemas]_espace de travail vous permet de modifier vos schémas XDM existants. Pour ajouter un descripteur d&#39;identité à un schéma, sélectionnez le schéma dans la liste et suivez les étapes pour[définir un champ de schéma en tant que champ](../xdm/tutorials/create-schema-ui.md#identity-field)d&#39;identité dans le didacticiel de l&#39;éditeur de Schémas.

Une fois que vous avez défini les champs appropriés dans le schéma en tant que champs d’identité, vous pouvez passer à la section suivante lors de l’ [envoi des demandes](#submit)de confidentialité.

### Using the API {#identity-api}

>[!NOTE] Cette section suppose que vous connaissez la valeur d&#39;ID URI unique du schéma XDM de votre jeu de données. Si vous ne connaissez pas cette valeur, vous pouvez la récupérer à l’aide de l’API du service de catalogue. Après avoir lu la section [prise en main](./api/getting-started.md) du guide du développeur, suivez les étapes décrites dans la section pour [répertorier](./api/list-objects.md) ou [](./api/look-up-object.md) rechercher des objets Catalogue pour trouver votre jeu de données. L&#39;ID de schéma se trouve sous `schemaRef.id`
>
> Cette section comprend des appels à l&#39;API de registre du Schéma. Pour obtenir des informations importantes sur l’utilisation de l’API, y compris la connaissance de votre concept `{TENANT_ID}` et du concept de conteneur, consultez la section [prise en main](../xdm/api/getting-started.md) du guide du développeur.

Vous pouvez ajouter un descripteur d&#39;identité au schéma XDM d&#39;un jeu de données en envoyant une requête POST au point de `/descriptors` terminaison dans l&#39;API de registre du Schéma.

**Format d’API**

```http
POST /descriptors
```

**Requête**

La requête suivante définit un descripteur d’identité sur un champ &quot;adresse électronique&quot; dans un exemple de schéma.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

| Propriété | Description |
| --- | --- |
| `@type` | Type de descripteur en cours de création. Pour les descripteurs d’identité, la valeur doit être &quot;xdm:descriptorIdentity&quot;. |
| `xdm:sourceSchema` | ID URI unique du schéma XDM de votre jeu de données. |
| `xdm:sourceVersion` | Version du schéma XDM spécifiée dans `xdm:sourceSchema`. |
| `xdm:sourceProperty` | Chemin d’accès au champ de schéma auquel le descripteur est appliqué. |
| `xdm:namespace` | L’un des espaces de nommage [d’identité](../privacy-service/api/appendix.md#standard-namespaces) standard reconnus par Privacy Service, ou un espace de nommage personnalisé défini par votre organisation. |
| `xdm:property` | &quot;xdm:id&quot; ou &quot;xdm:code&quot;, selon l’espace de nommage utilisé sous `xdm:namespace`. |
| `xdm:isPrimary` | Valeur booléenne facultative. Lorsque la valeur est true, cela indique que le champ est une identité principale. Les Schémas ne peuvent contenir qu&#39;une seule identité primaire. La valeur par défaut est false si elle n’est pas incluse. |

**Réponse**

Une réponse réussie renvoie l’état HTTP 201 (Créé) et les détails du descripteur nouvellement créé.

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## Envoi de requêtes {#submit}

>[!NOTE] Cette section traite de la façon de formater les demandes de protection de la vie privée pour le lac Data. Il est vivement recommandé de consulter la documentation de l’interface utilisateur [de](../privacy-service/ui/overview.md) Privacy Service ou de l’API [de](../privacy-service/api/getting-started.md) Privacy Service pour obtenir des instructions complètes sur la façon d’envoyer une tâche de confidentialité, y compris sur la façon de formater correctement les données d’identité d’utilisateur envoyées dans les charges de demande.

La section suivante décrit comment faire des demandes de confidentialité pour Data Lake à l’aide de l’interface utilisateur ou de l’API de Privacy Service.

### Utilisation de l’interface utilisateur

Lors de la création de demandes d&#39;emploi dans l&#39;interface utilisateur, veillez à sélectionner **AEP Data Lake** et/ou **Profil** sous _Produits_ afin de traiter les tâches pour les données stockées dans Data Lake ou dans le Profil client en temps réel, respectivement.

<img src="images/privacy/product-value.png" width="450"><br>

### Utilisation de l’API

Lors de la création de demandes de travaux dans l’API, les demandes `userIDs` fournies doivent utiliser un code spécifique `namespace` et `type` selon le magasin de données auquel elles s’appliquent. Les ID de Data Lake doivent utiliser &quot;non inscrit&quot; pour leur `type` valeur et une `namespace` valeur correspondant à l’une des étiquettes [de](#privacy-labels) confidentialité ajoutées aux jeux de données applicables.

En outre, le `include` tableau de la charge utile de la demande doit inclure les valeurs de produit des différents entrepôts de données auxquels la demande est envoyée. Lorsque vous effectuez des demandes à Data Lake, la baie doit inclure la valeur &quot;aepDataLake&quot;.

La demande suivante crée une nouvelle tâche de confidentialité pour Data Lake, en utilisant l’espace de nommage &quot;email_label&quot; non enregistré. Il inclut également la valeur du produit pour le lac Data dans la `include` baie :

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

## Supprimer le traitement de demande

Lorsqu’Experience Platform reçoit une demande de suppression de Privacy Service, Platform envoie une confirmation à Privacy Service que la demande a été reçue et que les données concernées ont été marquées pour suppression. Les dossiers sont ensuite retirés du lac Data dans les sept jours. Pendant cette période de sept jours, les données sont supprimées à l&#39;écran et ne sont donc accessibles à aucun service de plateforme.

Dans les prochaines versions, Platform enverra une confirmation à Privacy Service après la suppression physique des données.

## Étapes suivantes

En lisant ce document, vous avez été familiarisé avec les concepts importants liés au traitement des demandes de protection de la vie privée pour le lac Data. Il est recommandé de continuer à lire la documentation fournie dans ce guide afin de mieux comprendre comment gérer les données d&#39;identité et créer des tâches de confidentialité.

Consultez le document sur le traitement des demandes de [confidentialité pour le Profil](../profile/privacy.md) client en temps réel pour savoir comment traiter les demandes de confidentialité pour la boutique de Profils.

## Annexe

La section suivante contient des renseignements supplémentaires sur le traitement des demandes de protection de la vie privée dans le lac Data.

### Étiquetage des champs de type de mappage imbriqués {#nested-maps}

Il est important de noter qu’il existe deux types de champs de type carte imbriqués qui ne prennent pas en charge l’étiquetage de confidentialité :

* Un champ de type carte dans un champ de type tableau
* Un champ de type de mappage dans un autre champ de type de mappage

Le traitement de la tâche de traitement de la confidentialité pour l’un ou l’autre des deux exemples ci-dessus échouera. Pour cette raison, il est recommandé d’éviter d’utiliser des champs de type de mappage imbriqués pour stocker des données client privées. Les ID de consommateur pertinents doivent être stockés en tant que type de données non mappé dans le `identityMap` champ (qui est lui-même un champ de type mappé) pour les jeux de données basés sur des enregistrements, ou dans le `endUserID` champ pour les jeux de données basés sur des séries chronologiques.